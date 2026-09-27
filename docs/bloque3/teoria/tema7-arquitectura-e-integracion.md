# Tema 7. Arquitectura e integración de sistemas de IA generativa

**Dedicación estimada: 3 horas.** Incluye lectura, análisis de dos ejemplos y comprobación. La [Actividad 5](../actividades/actividad5-integracion.md) y el [proyecto final](../../proyecto-final.md) tienen dedicaciones independientes.

| Recorrido | Tiempo orientativo |
|---|---:|
| 1. De una necesidad a una arquitectura | 20 min |
| 2. Componentes y responsabilidades | 35 min |
| 3. Flujo de datos y decisiones | 45 min |
| 4. Integrar por etapas y observar el sistema | 35 min |
| 5. Dos ejemplos explicados | 30 min |
| 6. Síntesis y comprobación | 15 min |
| **Total** | **180 min** |

En los bloques anteriores se estudiaron la interacción y el contexto, las fuentes externas, la recuperación y los workflows. Diseñar un sistema completo consiste en decidir **qué piezas necesita un caso concreto y cómo se relacionan**, no en incluir todas las tecnologías disponibles. Una arquitectura es una descripción de esas decisiones: componentes, datos que circulan, límites de cada responsabilidad y comportamiento cuando algo falla.

**Al finalizar podrás** proponer una arquitectura mínima para una necesidad profesional, identificar la procedencia de las respuestas, distinguir decisiones del modelo y de la aplicación, y planificar una integración gradual.

## 1. Empezar por la necesidad

Antes de pensar en componentes conviene situar el problema en un contexto concreto. Imaginemos que el equipo docente de una asignatura recibe cada curso numerosas preguntas sobre entregas, extensión de informes y criterios de evaluación. Parte de la documentación es pública para el alumnado y parte corresponde a borradores internos que todavía no deben consultarse.

En ese contexto, «crear un asistente con memoria, RAG y agentes» enumera técnicas, pero todavía no expresa la necesidad. Una formulación más útil sería «ayudar al equipo de una asignatura a responder preguntas frecuentes sobre instrucciones vigentes sin divulgar borradores internos». Esta segunda formulación permite preguntar quién utilizará el sistema, qué fuentes están autorizadas, qué dudas debe resolver y qué hacer cuando no hay una respuesta suficientemente fundamentada.

Para convertir esa necesidad en decisiones de diseño puede utilizarse una ficha inicial. Su finalidad no es decidir todavía la tecnología, sino hacer explícito qué debe resolver el sistema y cuáles son sus límites:

| Pregunta | Decisión que debe quedar explícita |
|---|---|
| ¿Quién usa el sistema? | Grupo destinatario y acceso permitido. |
| ¿Qué problema resuelve? | Una o dos tareas verificables. |
| ¿Qué información recibe? | Petición, estado y fuentes concretas. |
| ¿Qué produce? | Respuesta, borrador o propuesta de acción. |
| ¿Qué no puede hacer? | Decisiones fuera de su ámbito y acciones sin autorización. |
| ¿Cómo sabremos si funciona? | Casos de prueba y criterios de revisión. |

La tabla permite detectar pronto si realmente es necesario construir un sistema de IA generativa. Puede revelar, por ejemplo, que una página de preguntas frecuentes bien mantenida basta. Si se necesitan consultas variadas sobre documentos extensos, tendría sentido estudiar recuperación. Si se repiten tareas con pasos y aprobaciones, podría justificarse un workflow. **La complejidad debe responder al problema**, no al número de tecnologías que sea posible incorporar.

<details>
<summary><strong>¿Por qué no elegir primero el modelo?</strong></summary>

El modelo importa, pero sin una tarea y criterios claros no sabremos qué capacidades comprobar. Una vez definido el problema pueden compararse alternativas según su capacidad para procesar el tipo de entrada, su funcionamiento en las pruebas, el acceso permitido a los datos, el coste y el esfuerzo de mantenimiento. No existe un modelo óptimo para todos los casos.

</details>

## 2. Componentes y responsabilidades

Una vez delimitada la necesidad, podemos identificar las piezas que participan en el sistema. Para razonar sobre ellas resulta útil organizarlas en **capas lógicas**: grupos de funciones con responsabilidades diferenciadas. Una capa lógica no tiene por qué corresponder a un programa, servidor o servicio independiente; es una forma de separar responsabilidades para comprender mejor el sistema y localizar fallos.

La siguiente tabla muestra una posible descomposición. No todos los sistemas necesitan todos estos componentes, y en un prototipo varias responsabilidades pueden estar reunidas en una misma aplicación.

| Componente | Responsabilidad | Ejemplo de fallo que le corresponde |
|---|---|---|
| Interfaz | Recibir la petición y mostrar límites y fuentes. | Oculta a qué versión pertenece la respuesta. |
| Control de acceso | Determinar qué datos puede consultar la persona. | Entrega un documento restringido. |
| Orquestación | Seleccionar pasos y construir el contexto de la petición. | Mezcla tareas o estados de proyectos distintos. |
| Estado de conversación | Conservar decisiones vigentes y correcciones. | Reutiliza una duración sustituida. |
| Recuperación | Localizar pasajes autorizados y pertinentes. | Trae una guía archivada. |
| Modelo | Generar o transformar el contenido aportado. | Añade una condición no presente en la fuente. |
| Herramientas | Leer o modificar servicios externos con permiso. | Repite un envío tras perder la confirmación. |
| Revisión y registro | Permitir comprobar y corregir resultados. | No queda rastro de qué pasaje se utilizó. |

La tabla no debe interpretarse como una plantilla que haya que reproducir completa. Una función puede combinarse con otra en un prototipo. Por ejemplo, la selección de pasajes puede hacerse manualmente y quedar registrada en una tabla. Lo esencial es reconocer **quién o qué asume cada responsabilidad**, qué información recibe y quién verifica el resultado cuando sea necesario.

### Un límite claro para las acciones

Conviene separar «el modelo propone consultar» de «la aplicación ejecuta la consulta» y de «el servicio confirma la operación». Del mismo modo, una propuesta de correo es una salida del modelo; enviarlo es una acción que exige controles adicionales. Estas diferencias se estudiaron en el [Tema 6](../../bloque2/teoria/tema6-automatizacion.md) y adquieren importancia cuando se integran todas las piezas.

![Componentes lógicos de un sistema de IA generativa](../../assets/images/tema7-arquitectura.png){ width="400" style="display:block; margin:auto;" }

<small><strong>Imagen.</strong> <em>Organización lógica de los componentes de un sistema de IA generativa y de las responsabilidades que intervienen en su funcionamiento.</em></small>

## 3. Seguir el recorrido de los datos

Una arquitectura se entiende mejor si seguimos **una petición concreta** de principio a fin. Retomemos el caso del equipo docente. Un estudiante accede al asistente y pregunta: «¿Cuál es el máximo de páginas del informe de este curso?». El sistema debe responder utilizando únicamente la documentación vigente y accesible para ese estudiante. El recorrido podría ser:

1. La interfaz identifica la pregunta y el curso al que se refiere.
2. El control de acceso determina qué documentos puede consultar la persona.
3. La recuperación filtra la edición vigente y selecciona el apartado de extensión.
4. La orquestación entrega al modelo la pregunta, instrucciones y pasaje con versión.
5. El modelo redacta una respuesta provisional con referencia al apartado.
6. Un control comprueba que la afirmación no excede lo que dice la fuente; la interfaz muestra la respuesta y su procedencia.

Si falta el curso, el sistema podría pedir aclaración antes del paso 3. Si no encuentra fuente, debería indicarlo. Si una herramienta externa falla, no debe inventarse su resultado. **Estas bifurcaciones son parte de la arquitectura**, aunque se representen en una tabla y no en código.

<details>
<summary><strong>¿Dónde interviene la memoria?</strong></summary>

Solo si aporta valor al caso. Puede conservar la edición elegida durante la conversación o preferencias necesarias para la tarea. Debe quedar claro su alcance: no se debe llevar automáticamente la edición de una asignatura a otra conversación. El <a href="../../../bloque1/teoria/tema3-contexto-y-memoria">Tema 3: Contexto y memoria  desarrolla esa distinción.</a>

</details>

### Contratos entre componentes

Cuando varias piezas colaboran, no basta con saber qué hace cada una: también hay que definir **qué información entrega una a la siguiente y en qué forma**. A ese acuerdo sobre entradas y salidas lo llamaremos aquí **contrato entre componentes**. No implica necesariamente un contrato técnico formal; sirve para especificar qué puede esperar cada parte del sistema.

Por ejemplo, una recuperación útil puede devolver, además del texto, **identificador de fuente, versión, sección y estado de acceso**. La generación recibe esos pasajes delimitados y devuelve una respuesta que pueda revisarse. La interfaz, a su vez, debería presentar la referencia y reflejar adecuadamente la incertidumbre: no debe transformar «no se ha encontrado» en una afirmación concluyente.

<details>
<summary><strong>💡 Metáfora · El relevo</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

En una carrera de relevos no basta con que cada corredor sea rápido: el testigo debe pasar correctamente de uno al siguiente. En una arquitectura ocurre algo parecido. Cada componente puede funcionar bien por separado, pero si entrega información incompleta o ambigua al siguiente, el sistema puede fallar. El <strong>contrato</strong> especifica qué testigo debe entregarse y qué información debe acompañarlo.

</div>

</details>

Un prototipo que solo intercambia párrafos sin procedencia puede parecer funcional hasta que se cambia un documento. Entonces resulta difícil determinar por qué respondió de una manera u otra. Definir estas entradas y salidas desde el principio facilita tanto la integración como el diagnóstico posterior.

## 4. Integrar por etapas y observar el sistema

Una integración razonable comienza con el camino más simple que resuelve el caso y añade componentes solo cuando aportan una capacidad necesaria. En el asistente de la asignatura, por ejemplo, podríamos avanzar de forma gradual:

- **Primer recorrido:** petición, fuente elegida manualmente y respuesta revisada.
- **Segundo recorrido:** recuperación automática y referencia verificable.
- **Tercer recorrido:** estado conversacional y actualización de decisiones.
- **Cuarto recorrido, solo si procede:** una herramienta o un workflow con aprobación.

Esta progresión permite comprobar cada incorporación antes de añadir la siguiente. El orden exacto depende del proyecto: quizá otro sistema no necesite memoria o nunca llegue a ejecutar acciones. Añadir varios componentes al mismo tiempo puede hacer difícil atribuir un error. Conviene conservar preguntas de prueba constantes y registrar qué cambió de una versión a otra.

### Aspectos de uso que también se diseñan

Una arquitectura viable necesita considerar tiempos de respuesta, recursos necesarios, continuidad si un servicio falla, actualización de fuentes y quién atenderá incidencias. No hace falta calcular cifras universales: en un prototipo basta identificar dónde se producirían esperas, costes por consulta o dependencias de un proveedor.

Además, necesitamos poder **observar qué ha ocurrido dentro del sistema** cuando una respuesta es incorrecta o una acción falla. Para ello se conservan determinados registros que permiten reconstruir el recorrido seguido, siempre dentro de la finalidad y los permisos establecidos. La siguiente tabla recoge algunas señales especialmente útiles:

| Señal que conviene registrar | Para qué ayuda |
|---|---|
| Versión de instrucciones y del corpus | Reproducir una respuesta. |
| Pasaje recuperado y fuente | Diagnosticar citas y vigencia. |
| Herramienta llamada y resultado | Separar solicitud y ejecución. |
| Corrección o aprobación humana | Conocer qué se publicó realmente. |
| Error y momento del fallo | Priorizar una reparación. |

Estos registros ayudan a distinguir, por ejemplo, si el problema estaba en la fuente recuperada, en la generación o en una herramienta externa. Sin embargo, **observar el sistema no significa registrar todo**. Los datos conservados deben limitarse a lo necesario para la finalidad del servicio y respetar los permisos adecuados; registrar información indiscriminadamente también sería una mala decisión de diseño.

<details>
<summary><strong>¿Arquitectura y diagrama son lo mismo?</strong></summary>

El diagrama ayuda a comunicar la arquitectura, pero no la agota. También hay que explicar reglas como «solo se consulta la edición vigente» o «ninguna respuesta se envía sin aprobación». Una tabla de componentes, un recorrido de datos y unas pruebas pueden ser más informativos que un diagrama complejo sin decisiones explícitas.

</details>

## 5. Dos ejemplos desarrollados

1. [Ejemplo 1. Asistente de información para una asignatura](ejemplos/tema7-ejemplo1-asistente-asignatura.md). Selecciona componentes y sigue una consulta concreta.
2. [Ejemplo 2. Preparación de un informe de investigación](ejemplos/tema7-ejemplo2-informe-investigacion.md). Muestra un sistema con borrador, fuente y aprobación, sin agentes autónomos.

Ambos son casos **ficticios**. Sus decisiones ilustran posibilidades; cada proyecto requiere comprobar fuentes, acceso y necesidades reales.

## 6. Síntesis y comprobación

Una arquitectura traduce la necesidad en componentes, flujos de datos y reglas de actuación. Integrar no equivale a sumar técnicas; significa que cada pieza cumpla una función, intercambie información verificable y permita localizar fallos.

1. ¿Qué componente revisarías primero si el pasaje aportado procede de un curso anterior?
2. Si el modelo redacta «correo enviado», ¿qué evidencia faltaría para afirmar que se envió?
3. ¿Qué se perdería si el recuperador devolviera texto sin identificador ni versión?
4. ¿Cuándo estaría justificado añadir memoria entre sesiones?

<details>
<summary><strong>Orientaciones de respuesta</strong></summary>

<p>1. Filtro de ámbito y versión de la recuperación, además del inventario de documentos.</p>
<p>2. La confirmación del servicio de envío y la autorización correspondiente.</p>
<p>3. Capacidad de comprobar, reproducir y actualizar la respuesta.</p>
<p>4. Cuando una necesidad concreta requiera continuidad y se hayan definido alcance, conservación y corrección de los datos.</p>

</details>

**Para continuar:** el [Tema 8](tema8-calidad-y-evaluacion.md) establece criterios y pruebas para el sistema integrado; la [Actividad 5](../actividades/actividad5-integracion.md) permitirá revisar una arquitectura y ensayar su evaluación.

### Lecturas de referencia

- [Microsoft Learn: visión general de RAG](https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview). Arquitectura de recuperación y respuesta.
- [OpenAI: uso de herramientas](https://developers.openai.com/api/docs/guides/tools). Posibles integraciones; su configuración depende de la plataforma elegida.

[Volver a la presentación del bloque](../index.md)
