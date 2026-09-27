# Proyecto final

**Dedicación estimada: 18 horas**, incluidas en el Bloque III y en el total de 75 horas de la microcredencial. Las **6 horas de evaluación y cierre** que figuran en la página de Inicio se contabilizan por separado; aquí se incluye la **preparación** de la presentación, sin sumar dos veces la exposición y el cierre.

El proyecto consiste en **diseñar, desarrollar y evaluar un prototipo de sistema de IA generativa** que responda a una necesidad realista de un ámbito docente, investigador o profesional. Cada participante elige un caso acorde con su perfil. Se espera un prototipo delimitado y verificable, no una aplicación lista para despliegue institucional.

## 1. Elegir un problema concreto

El caso debe poder describirse en términos de **persona destinataria, necesidad, información disponible y resultado útil**. Algunos ejemplos son consultar instrucciones de un proyecto, preparar borradores fundamentados en documentos, apoyar la organización de un curso o supervisar un pequeño flujo de trabajo. Pueden elegirse otros casos si permiten justificar sus decisiones y probarlos con datos autorizados.

Un sistema debe ofrecer algo más que una pregunta aislada a un chatbot. Debe integrar una interacción definida y **al menos otra capacidad que resulte necesaria para el caso**, como estado contextual, recuperación de fuentes o pasos de automatización supervisados. La elección se justifica por la necesidad; no se exige añadir todas las capacidades solo para marcar una lista. Se valorará también la explicación de **por qué se excluyen** otras piezas.

<details>
<summary><strong>Ejemplo de delimitación</strong></summary>

«El equipo de un proyecto recibe preguntas sobre la última versión de sus instrucciones. El prototipo identifica el documento vigente, recupera el apartado relevante, propone una respuesta con referencia y reconoce cuándo no consta. No resuelve excepciones individuales ni envía mensajes automáticamente».

La descripción identifica una necesidad y un límite. La calidad del proyecto dependerá después de que la selección de fuentes y las respuestas **funcionen en pruebas**, no solo de que el objetivo suene pertinente.

</details>

## 2. Trabajo previsto y dedicación

| Etapa | Trabajo principal | Tiempo orientativo |
|---|---|---:|
| Delimitar caso y arquitectura | Necesidad, alcance, fuentes, datos, componentes y riesgos principales. | 3 h |
| Desarrollar el prototipo | Integrar interacción y capacidades seleccionadas; documentar configuración y versiones. | 7 h |
| Probar y corregir | Ejecutar casos normales, ambiguos y de fallo; reparar al menos un problema importante. | 5 h |
| Preparar comunicación | Informe breve, demostración y presentación oral. | 3 h |
| **Total** | | **18 h** |

Los materiales y pruebas de las actividades anteriores pueden aprovecharse como **punto de partida**. Las 18 horas del proyecto corresponden al desarrollo y revisión adicionales del prototipo final; el tiempo ya invertido en las actividades tiene su propia asignación.

### Arquitectura mínima que debe poder explicarse

Identifica entradas, salida, instrucciones, estado si se utiliza, fuentes y su versión si se recuperan, herramientas y permisos si se automatiza, y puntos de revisión humana. Explica el recorrido de **una petición real** entre esos componentes. Una tabla o diagrama sencillo con descripción de decisiones suele ser suficiente.

<!-- IMAGEN OPCIONAL: ejemplo genérico y propio de arquitectura con «Persona → Interfaz → Orquestación → Modelo», y conexiones condicionales a contexto, fuentes, herramientas y revisión. Guardar en docs/assets/images/proyecto-arquitectura.png y enlazar aquí solo si se crea. -->

## 3. Prototipo y condiciones de trabajo

Se puede realizar con un entorno conversacional configurado, una herramienta sin código o una aplicación sencilla. No es obligatorio programar ni emplear servicios de pago. Sí debe existir **una ejecución observable**, con entradas y salidas reales del componente generativo; las herramientas externas que no se conecten se marcarán como simuladas. Una presentación de la idea sin prototipo probado no completa el trabajo.

Si el caso requiere documentos, utiliza material público, propio y autorizado o versiones ficticias representativas. Si implica decisiones sobre personas, evita automatizarlas sin supervisión: delimita el prototipo a propuestas revisables. No introduzcas datos personales o información reservada en herramientas externas para demostrar el funcionamiento.

<details>
<summary><strong>¿Qué significa «desarrollar» si no se programa?</strong></summary>

Significa construir y probar el comportamiento del sistema: definir instrucciones, preparar fuentes o estado, configurar pasos, ejecutar consultas y registrar qué información recibió el modelo y qué produjo. La herramienta elegida no sustituye la explicación de esas decisiones ni la evidencia de las pruebas.

</details>

## 4. Plan mínimo de evaluación

Antes de ejecutar las pruebas, define qué debería ocurrir en **al menos seis casos** adaptados a tu sistema:

| Caso | Pregunta que debe responder la prueba |
|---|---|
| Ordinario | ¿Resuelve una petición habitual con información suficiente? |
| Variación | ¿Mantiene un resultado adecuado si cambia la formulación? |
| Incompleto o ambiguo | ¿Pide aclaración o indica el límite? |
| Fuente o decisión corregida | ¿Utiliza la versión vigente? |
| Fuera de alcance | ¿Se abstiene de tomar una decisión no autorizada? |
| Fallo controlado | ¿Comunica que una fuente o herramienta no está disponible? |

Si el caso no usa fuentes ni herramientas, adapta esos casos a sus componentes; por ejemplo, una corrección de estado o un dato de entrada contradictorio. Registra **entrada, contexto, esperado, observado y juicio**. Comprueba las citas cuando las haya, repite el caso más problemático tras una corrección y comunica qué **no se ha probado**. Los seis casos sirven para detectar fallos del prototipo; no justifican afirmar una fiabilidad estadística general.

Las observaciones deben cubrir, en la medida pertinente, **adecuación**, **fidelidad a fuentes y datos**, **robustez** ante variaciones, **seguridad y permisos** de las acciones, y **trazabilidad**. Para guiar las pruebas pueden consultarse el [Tema 8](bloque3/teoria/tema8-calidad-y-evaluacion.md) y la [Actividad 5](bloque3/actividades/actividad5-integracion.md).

## 5. Entregables y presentación

El trabajo se comunicará mediante:

1. **Prototipo o demostración reproducible:** acceso o instrucciones suficientes para ejecutar el recorrido principal; si no puede compartirse la herramienta, capturas o registro que permitan comprobarlo.
2. **Informe escrito breve:** aproximadamente **3–4 páginas**, sin contar portada y anexos opcionales. Debe incluir necesidad y destinatarios; arquitectura y decisiones; pruebas con resultados y una corrección; limitaciones y siguiente mejora. Puede remitir a un anexo de instrucciones o salidas, en lugar de copiar transcripciones largas en el cuerpo.
3. **Presentación oral de 10–15 minutos:** contexto y necesidad, recorrido del prototipo, dos pruebas reveladoras —una de ellas puede ser un fallo y su corrección—, límites y conclusión. Se reserva tiempo para mostrar el funcionamiento o una demostración registrada.

La presentación no necesita repetir página por página el informe. Conviene mostrar qué problema resuelve el prototipo y **qué evidencia sostiene** la valoración del resultado.

<details>
<summary><strong>Guion orientativo para 10–15 minutos</strong></summary>

**2 min:** necesidad y destinatarios. **3 min:** componentes y recorrido de datos. **4–5 min:** demostración y dos pruebas. **2–3 min:** error, corrección y límites. **1–2 min:** conclusión y posible siguiente paso. Los tiempos se ajustan a la demostración, sin exceder el intervalo total.

</details>

## 6. Criterios orientativos de revisión

| Dimensión | Evidencia que se espera encontrar |
|---|---|
| Pertinencia del caso | Necesidad concreta y alcance razonable. |
| Coherencia del diseño | Componentes justificados y flujo comprensible. |
| Funcionamiento | Recorrido ejecutado y resultados observables. |
| Evaluación | Pruebas variadas, esperado frente a observado, diagnóstico y corrección. |
| Responsabilidad | Fuentes y permisos adecuados, supervisión y límites explícitos. |
| Comunicación | Informe conciso y presentación que permite entender la evidencia. |

Estos criterios describen qué revisar en el trabajo y **no asignan porcentajes ni sustituyen la rúbrica oficial**. Las fechas, el modo de entrega y la calificación se indicarán en el Campus Virtual.

### Comprobación antes de presentar

- ¿La necesidad elegida está alineada con el perfil profesional de quien presenta?
- ¿Se sabe qué hace cada componente y de dónde procede la información?
- ¿La demostración distingue salidas reales de pasos simulados?
- ¿Se muestran un fallo o límite y su tratamiento?
- ¿El informe breve y la presentación caben en el tiempo previsto?

[Volver al Bloque III](bloque3/index.md)
