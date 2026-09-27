# Tema 1. De los modelos generativos a los sistemas de IA

**Dedicación estimada: 3 horas.** Incluye lectura, exploración de los dos ejemplos y comprobación de lo aprendido. Las actividades del bloque tienen su propia dedicación y no se cuentan aquí.

| Recorrido | Tiempo orientativo |
|---|---:|
| 1. Una necesidad, dos maneras de abordarla | 20 min |
| 2. Qué hace un modelo generativo | 40 min |
| 3. Qué añade un sistema de IA | 45 min |
| 4. Decisiones de diseño y límites | 30 min |
| 5. Dos ejemplos desarrollados | 30 min |
| 6. Síntesis y comprobación | 15 min |
| **Total** | **180 min** |

## 1. Una necesidad, dos maneras de abordarla

Una profesora quiere ayudar a su alumnado a comprender una guía de trabajo final. Puede copiar la pregunta de un estudiante en un asistente de IA y pedir una explicación. También puede diseñar un servicio al que se acceda desde la página de la asignatura, que consulte la versión vigente de la guía, indique en qué apartado se basa la respuesta, reconozca cuándo no encuentra información y derive ciertos casos a la profesora.

En ambas situaciones puede intervenir el mismo **modelo generativo**. En la primera hay una interacción puntual. En la segunda hay una finalidad definida, fuentes, reglas, una interfaz y formas de comprobar el resultado: hay un **sistema de IA generativa**. Este tema distingue lo que puede producir el modelo de las condiciones que debemos diseñar para usarlo en un contexto real.

<details>
<summary><strong>Pregunta inicial: ¿en cuál de los dos casos confiarías para dar información oficial?</strong></summary>

El segundo ofrece mejores condiciones si la guía está actualizada, se recupera el fragmento correcto y se revisa la respuesta. El mero hecho de incorporar documentos no garantiza que todo sea cierto. La confianza depende de fuentes y comprobaciones efectivas.

</details>

**Al terminar el tema podrás** diferenciar modelo y sistema, reconocer los componentes de una aplicación generativa y justificar cuándo hacen falta fuentes, controles y evaluación.

## 2. Qué hace un modelo generativo

Un modelo generativo aprende patrones durante su entrenamiento y produce contenido nuevo a partir de una entrada. Un modelo de lenguaje puede recibir una pregunta, un documento o parte de una conversación y generar una explicación, una reformulación o una tabla. Otros modelos trabajan con imágenes o audio. Su capacidad de producir texto convincente no implica que conozca la versión vigente de una norma o las necesidades de una asignatura concreta.

| Noción | Significado en este curso | Consecuencia para el diseño |
|---|---|---|
| **Entrada** | Pregunta e información que recibe el modelo. | Una pregunta ambigua deja abierta la interpretación. |
| **Contexto** | Instrucciones, mensajes y datos disponibles durante la interacción. | Si la guía no se proporciona, no puede suponerse que el modelo la consulta. |
| **Generación** | Producción de la salida a partir de patrones y del contexto. | Una respuesta fluida puede contener inferencias injustificadas. |
| **Salida** | Texto u otro contenido generado. | Es necesario comprobar pertinencia, formato y exactitud. |

Los modelos de lenguaje procesan internamente *tokens*, unidades de texto que no siempre equivalen a palabras. No necesitamos calcularlos ahora. Sí importa saber que la cantidad de contexto procesable en una interacción es limitada y depende del modelo y su configuración. Proporcionar más texto tampoco asegura un mejor resultado: pueden existir fragmentos irrelevantes, contradictorios o desactualizados.

Imaginemos la pregunta «¿Cuándo hay que entregar la memoria?». Sin la guía actualizada, el modelo podría responder con una fecha plausible que no corresponde al curso. Incluso con la guía, debe determinar a qué memoria se refiere la pregunta, distinguir una fecha definitiva de una provisional y no confundir la entrega escrita con la presentación oral.

<details>
<summary><strong>¿El modelo busca en sus datos de entrenamiento al responder?</strong></summary>

No suele consultar un archivo de documentos originales como lo haría un buscador. El entrenamiento ajusta parámetros a partir de datos; después, la respuesta se genera utilizando esos parámetros y el contexto de la interacción. Una aplicación puede añadir búsqueda de documentos actuales, pero se trata de un componente adicional del sistema.

</details>

<details>
<summary><strong>¿Qué significa que un modelo sea multimodal?</strong></summary>

Que, según sus capacidades, puede procesar o generar diferentes modalidades, como texto, imágenes o audio. Por ejemplo, una aplicación podría admitir una fotografía de un gráfico y pedir una explicación textual. La interpretación seguiría necesitando revisión, especialmente si el gráfico se utiliza para tomar una decisión.

</details>

![Entrada, modelo generativo y salida](../../assets/images/tema1-modelo-generativo.png){ width="350" style="display:block; margin:auto;" }

<small><strong>Imagen.</strong> <em>Del modelo de IA a la aplicación con la que interactúa el usuario.</em></small>

### Capacidad y fiabilidad son preguntas diferentes

Un modelo puede redactar con claridad, resumir y transformar formatos. Ninguna de esas capacidades demuestra que una afirmación sea verdadera. Conviene separar «¿se expresa bien?» de «¿podemos usar su respuesta con fundamento?». Para explicar un concepto puede bastar una revisión docente. Para comunicar una fecha oficial es necesario identificar la fuente vigente y comprobar la coincidencia exacta. Una decisión que afecte a una persona requiere criterios y supervisión adicionales.

## 3. Qué añade un sistema de IA generativa

Llamaremos **sistema de IA generativa** al conjunto de componentes y reglas que emplea uno o varios modelos para una función concreta. Puede ser pequeño o complejo. Lo decisivo es que el comportamiento final depende de decisiones que van más allá del modelo.

En un servicio que responda preguntas sobre la guía, el recorrido podría ser: el estudiante escribe una pregunta; la aplicación identifica la guía vigente; un componente selecciona los fragmentos pertinentes; se construye el contexto enviado al modelo; se genera una respuesta; la aplicación comprueba el formato y presenta una referencia que la persona pueda consultar. Si no hay información suficiente, informa de ello y ofrece un canal humano. Cada paso puede fallar de una manera distinta.

La siguiente tabla resume los principales **componentes que pueden formar parte de una aplicación basada en IA generativa**. Para cada uno se indica su función y una **decisión de diseño** que conviene plantearse al construir el sistema. No todas las aplicaciones necesitarán todos estos componentes: su elección y configuración dependerán del propósito, los datos y el nivel de autonomía de la solución.

| Componente posible | Función | Decisión de diseño |
|---|---|---|
| **Interfaz** | Recibe preguntas y muestra respuestas. | ¿Qué puede solicitar la persona usuaria? |
| **Instrucciones** | Delimitan tarea, tono y comportamiento esperado. | ¿Qué hacer si no hay información suficiente? |
| **Modelo** | Genera o transforma contenido. | ¿Qué capacidades requiere la tarea? |
| **Contexto y estado** | Mantienen información relevante de la interacción. | ¿Qué debe recordarse y durante cuánto tiempo? |
| **Fuentes externas** | Aportan documentos y datos. | ¿Qué fuente es válida y cuál es su versión? |
| **Herramientas** | Consultan servicios o ejecutan acciones. | ¿Con qué permisos y confirmaciones? |
| **Comprobación** | Contrasta las salidas y registra problemas. | ¿Qué errores deben detectarse? |
| **Responsables** | Atienden incidencias y actualizan el servicio. | ¿Quién supervisa el resultado? |

La tabla es una guía de posibles componentes, no una lista de requisitos obligatorios. Para reformular un texto aportado por la persona usuaria quizá no hacen falta fuentes externas. Para responder sobre una normativa cambiante sí pueden resultar imprescindibles.

![Componentes de un sistema de IA generativa](../../assets/images/tema1-sistema-ia.png){ width="450" style="display:block; margin:auto;" }

<small><strong>Imagen.</strong> <em>Flujo de interacción entre la persona usuaria, la aplicación y el modelo generativo.</em></small>

<details>
<summary><strong>¿Una conversación en una aplicación comercial ya es un sistema?</strong></summary>

Sí. El producto tiene interfaz, modelo y otros componentes. La diferencia didáctica es <strong>qué parte diseña quien hace la consulta</strong>. Una conversación individual utiliza un sistema existente; crear un servicio para una institución exige definir sus fuentes, permisos, pruebas y responsables.

</details>

<details>
<summary><strong>¿Basta con escribir instrucciones muy precisas?</strong></summary>

Las buenas instrucciones ayudan a encuadrar la tarea y serán el centro del Tema 2. Por sí solas no incorporan la versión actualizada de una norma, no verifican las citas ni impiden todos los errores. Si la necesidad exige datos actuales, control de acceso o comprobación independiente, habrá que diseñar esos componentes.

</details>

### Un recorrido visible y otro interno

Para quien pregunta, la experiencia puede reducirse a escribir y leer. Internamente se seleccionan documentos, se decide qué información enviar al modelo y se controla cómo presentar el resultado. Un buen diseño hace comprensible a la persona usuaria lo que necesita saber: qué tipo de preguntas puede resolver el servicio, de dónde procede la respuesta y cuándo acudir a una persona responsable.

Esta distinción ayuda a localizar fallos. Una fecha equivocada puede proceder de un documento desactualizado, una recuperación incorrecta, una pregunta ambigua o una interpretación errónea del modelo. Sustituir el modelo sin investigar la causa podría dejar el problema intacto.

## 4. Decisiones de diseño y límites

«Crear un chatbot para la asignatura» es una solución posible. «El alumnado no encuentra con facilidad los requisitos vigentes del trabajo final» expresa una necesidad. Formular primero la necesidad permite comparar soluciones, incluida una página clara de preguntas frecuentes.

Utilizaremos un **chatbot basado en IA generativa** como primer ejemplo. Un chatbot no es, por definición, un sistema de IA generativa: puede construirse mediante reglas u otras técnicas. En nuestro ejemplo, sin embargo, incorporaremos un modelo generativo y algunos componentes adicionales para **plantear un sistema de IA generativa muy sencillo**. Esto nos permitirá identificar sus elementos básicos antes de abordar sistemas más complejos.

La siguiente tabla concreta las **primeras decisiones de diseño** para el sistema de IA generativa del ejemplo. Antes de decidir cómo implementarlo, es necesario delimitar **quién lo utilizará, qué podrá resolver, qué quedará fuera de su alcance y qué fuentes podrá emplear**. También se establece cómo deberá actuar ante situaciones de incertidumbre y cómo se comprobará posteriormente que sus respuestas son adecuadas.

| Pregunta inicial | Respuesta posible para el ejemplo |
|---|---|
| ¿Quién lo usará y para qué? | Estudiantes que buscan requisitos del trabajo final. |
| ¿Qué puede resolver? | Cuestiones tratadas en documentos publicados y vigentes. |
| ¿Qué queda fuera? | Calificar trabajos, resolver casos personales o cambiar plazos. |
| ¿Qué fuentes utilizará? | Guía del curso e instrucciones oficiales autorizadas. |
| ¿Qué hará cuando dude? | Indicar que no puede confirmar la respuesta y dónde consultar. |
| ¿Cómo se comprobará? | Pruebas con respuestas esperadas y revisión de las referencias. |

Esto obliga a concretar **alcance**, **procedencia de la información** y **responsabilidad**. Si una respuesta cita una fuente, debe ser posible identificarla y verificarla. Si aparece un error, alguien debe poder actualizar el contenido o intervenir.

<details>
<summary><strong>Una afirmación convincente pero incorrecta</strong></summary>

El sistema responde «La entrega termina el 30 de junio». Pero el 30 de junio corresponde a la exposición y la memoria se entrega el 20 de junio. Hay que localizar el apartado pertinente, aclarar cuál de las dos entregas pregunta el estudiante y contrastar la respuesta. Solicitar al modelo «sé preciso» no realiza automáticamente estas comprobaciones.

</details>

<details>
<summary><strong>¿Qué cambia si el sistema puede actuar?</strong></summary>

Responder una duda y modificar una reserva de tutoría tienen consecuencias distintas. Para ejecutar acciones hacen falta permisos delimitados, confirmaciones, registro de lo sucedido y manejo de errores. Más adelante estudiaremos herramientas y automatización. Por ahora importa distinguir <strong>generar una propuesta</strong> de <strong>efectuar una acción</strong>.

</details>


<details>
<summary><strong>💡 Metáfora · Del consejo a la acción</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

Pedir consejo sobre qué plato elegir en un restaurante no es lo mismo que pedir que hagan el pedido por nosotros. En el primer caso recibimos una recomendación y seguimos teniendo el control sobre la decisión. En el segundo, alguien actúa en nuestro nombre y la decisión tiene consecuencias reales.

Del mismo modo, un sistema puede <strong>generar una propuesta</strong> o puede estar autorizado para <strong>ejecutar una acción</strong>. En este último caso necesitamos establecer claramente qué puede hacer, cuándo debe pedir confirmación y qué ocurre si algo sale mal.

</div>

</details>

### Pensar en el fallo desde el principio

¿Qué hace el servicio si falta la guía? ¿Y si hay dos versiones contradictorias? ¿Cómo responde a una pregunta ajena a su ámbito? Las respuestas a estas preguntas son parte del diseño. Una demostración que funciona una vez no equivale a un sistema fiable: hay que comprobar casos ordinarios, ambiguos y situaciones en las que debe reconocer que no dispone de una respuesta fundamentada.

<details>
<summary><strong>💡 Metáfora · ¿Y si algo no sale como estaba previsto?</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

Volvamos al restaurante. ¿Qué ocurre si el plato que nos han recomendado ya no está disponible? ¿Y si dos camareros nos dan información contradictoria sobre sus ingredientes? ¿O si preguntamos por algo que el restaurante no puede ofrecer? Un buen servicio no consiste únicamente en responder cuando todo sucede como estaba previsto: también debe saber <strong>cómo actuar ante la falta de información, la contradicción o una petición que queda fuera de su alcance</strong>.

Del mismo modo, al diseñar un sistema de IA generativa debemos prever no solo cómo responderá en los casos habituales, sino también <strong>qué hará cuando no disponga de información suficiente o fiable para responder</strong>.

</div>

</details>

## 5. Dos ejemplos desarrollados

Ambos casos son **ficticios**. Sus fechas y documentos sirven para analizar el diseño, no para informar de una asignatura real.

1. [Ejemplo 1. Un asistente para consultar una guía académica](ejemplos/ejemplo1-asistente-guia-academica.md): compara una respuesta libre con una respuesta apoyada en fuentes comprobables.
2. [Ejemplo 2. Una herramienta para reformular retroalimentación docente](ejemplos/ejemplo2-retroalimentacion-docente.md): muestra un sistema pequeño sin búsqueda documental, con alcance y revisión humana definidos.

Al leerlos, identifica la necesidad, los datos que recibe el modelo, una decisión que corresponde a la aplicación y un caso en que se deba pedir revisión.

## 6. Síntesis y comprobación

La capacidad generativa indica **qué contenido puede producir un modelo**. El diseño del sistema establece **en qué condiciones se utiliza esa capacidad**, con qué información, por quién y con qué comprobaciones.

1. Si dos aplicaciones usan el mismo modelo, ¿por qué pueden responder de manera distinta a la misma pregunta?
2. ¿Qué habría que añadir para contestar sobre un documento que cambia cada curso? ¿Qué conviene comprobar después?
3. ¿En qué se diferencia sugerir una respuesta de ejecutar una acción en nombre de alguien?
4. ¿Qué preguntarías antes de decidir que hay que construir un chatbot?

<details>
<summary><strong>Orientaciones para contrastar las respuestas</strong></summary>

<p>1. Pueden variar las instrucciones, el contexto, las fuentes, los controles y la interfaz.</p>
<p>2. Habría que facilitar la versión vigente, comprobar su selección, el fragmento recuperado y la correspondencia con la respuesta.</p>
<p>3. Una acción modifica un servicio o tiene efectos externos; requiere permisos, confirmaciones y tratamiento de incidencias.</p>
<p>4. Conviene averiguar qué necesidad concreta existe y si una solución más sencilla la resuelve.</p>

</details>

**Para continuar:** el [Tema 2](tema2-prompts-e-interaccion.md) desarrolla las instrucciones y la interacción; el [Tema 3](tema3-contexto-y-memoria.md) aborda la continuidad de las conversaciones.

### Lecturas para ampliar

- [Competencia Digital e IA Aplicada: fundamentos de IA](https://mltechdrawer.github.io/CompetenciaDigitalIA/bloque1/sesion2/) y [diseño de workflows](https://mltechdrawer.github.io/CompetenciaDigitalIA/bloque2/sesion4/). Materiales docentes previos para relacionar el uso de IA con el diseño de procesos.
- [ChatGPT: Ingeniería de Prompts](https://mltechdrawer.github.io/ChatGPT/2_IP/). Antecedente del trabajo específico del Tema 2.
- [Google for Developers: introducción a los modelos de lenguaje grandes](https://developers.google.com/machine-learning/crash-course/llm?hl=es-419). Tokens, contexto y funcionamiento general.
- [Google for Developers: qué es el aprendizaje automático](https://developers.google.com/machine-learning/intro-to-ml/what-is-ml). Marco general de la IA generativa.
- [OWASP: riesgos de las aplicaciones con modelos de lenguaje](https://genai.owasp.org/llm-top-10/). Material complementario sobre riesgos del sistema.

[Volver a la presentación del bloque](../index.md)
