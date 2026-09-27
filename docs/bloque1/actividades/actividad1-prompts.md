# Actividad 1. Diseño y evaluación de prompts

**Dedicación estimada: 4 horas.** Trabajo aplicado del Bloque I, posterior a los [Temas 1](../teoria/tema1-modelos-y-sistemas.md) y [2](../teoria/tema2-prompts-e-interaccion.md). El tiempo de esta actividad es independiente de las horas de estudio de los temas.

En esta actividad se diseña una instrucción para una necesidad profesional concreta, se prueba con entradas diferentes y se revisa a partir de los resultados. El producto principal no es «el prompt perfecto», sino una **decisión de diseño justificada con pruebas**. El caso elegido puede servir después como punto de partida para la [Actividad 2](actividad2-interaccion-contextual.md) y para el [proyecto final](../../proyecto-final.md).

## Resultado esperado

Al terminar dispondrás de un caso de uso acotado, dos versiones de un prompt, un pequeño conjunto de pruebas comunes a ambas, una comparación razonada de resultados y una versión seleccionada con límites explícitos.

No hace falta programar ni contratar una herramienta. Puede utilizarse cualquier sistema de IA generativa al que se tenga acceso autorizado. Si la interfaz permite controlar modelo y parámetros, es preferible mantenerlos iguales en la comparación. Si no los muestra, indícalo al documentar la prueba. Los resultados de modelos generativos pueden variar entre ejecuciones; las observaciones no deben interpretarse como una medida universal del modelo.

## 1. Elegir una necesidad y delimitarla — 30 minutos

Selecciona un caso cercano a tu ámbito docente, investigador o profesional. Podría tratarse de explicar instrucciones de una tarea, mejorar la claridad de comentarios académicos, organizar información que tú proporcionas o preparar un borrador de comunicación interna. Elige una función que pueda probarse con **ejemplos breves y ficticios**, sin necesidad de aportar datos personales, documentos reservados o decisiones de consecuencias importantes.

Formula el caso en cuatro frases: quién usará el resultado, qué problema resuelve, qué material recibirá el sistema y qué queda fuera de su alcance. Por ejemplo:

> «Una profesora quiere reformular instrucciones de prácticas para estudiantes de primer curso. Aporta el texto original de cada instrucción. El sistema propone una versión más clara sin cambiar requisitos ni fechas. La profesora comprueba el resultado antes de publicarlo».

Si ya has escogido una necesidad para el proyecto final, puedes utilizarla. No es obligatorio cerrar ahora la arquitectura de ese proyecto: aquí nos concentramos en **una tarea y una interacción**.

<details>
<summary><strong>¿Qué tipos de casos conviene evitar en esta primera prueba?</strong></summary>

Evita tareas que requieran información que no tienes, que obliguen a compartir datos sensibles o que pidan al modelo tomar decisiones sobre personas. Una petición como «decide automáticamente quién aprueba» no permite atribuir al prompt la responsabilidad académica. En cambio, «reformula un comentario ficticio conservando la evaluación realizada por el profesorado» ofrece un alcance más claro.

</details>

## 2. Definir criterios y casos de prueba — 35 minutos

Antes de probar el prompt, prepara **cuatro entradas** para la misma tarea:

1. Una petición ordinaria con toda la información necesaria.
2. Una petición ambigua para la que resulte importante pedir aclaración o indicar un supuesto.
3. Una entrada incompleta o con un dato que no consta.
4. Un caso límite relevante: dos requisitos contradictorios, una fecha que no debe modificarse o una solicitud fuera del alcance.

Escribe para cada una qué tendría que hacer una respuesta aceptable. No es necesario redactar de antemano una respuesta completa; basta con señalar datos que debe conservar, errores que debe evitar y cuándo tendría que detenerse.

| Criterio | 0: no conseguido | 1: parcial | 2: conseguido |
|---|---|---|---|
| Adecuación a la tarea | No responde a la necesidad. | Responde solo en parte. | Resuelve la necesidad definida. |
| Fidelidad a la entrada | Inventa o altera información esencial. | Hay alguna imprecisión. | Conserva los datos esenciales. |
| Manejo de dudas | Afirma sin base o ignora la ambigüedad. | Reconoce parte del problema. | Señala la falta de datos o pregunta cuando procede. |
| Claridad para la persona destinataria | Resulta difícil de usar. | Requiere edición notable. | Se comprende y permite revisión. |
| Alcance y formato | Incumple límites o formato relevantes. | Cumple algunos. | Respeta lo solicitado. |

Esta escala de **0 a 2 por criterio** es una herramienta de análisis de la actividad, **no una calificación oficial**. Adáptala al caso: para una extracción de fechas, la fidelidad debe pesar especialmente; para una explicación introductoria, el nivel de lenguaje puede ser decisivo. Escribe qué contarás como error esencial antes de ver los resultados.

<details>
<summary><strong>Ejemplo de cuatro pruebas para el caso de las instrucciones</strong></summary>

**Ordinaria:** «La memoria se entrega el día 18 de mayo en formato PDF». La fecha y el formato deben conservarse.<br>
**Ambigua:** «La entrega final será al terminar el módulo». Debe señalarse que falta una fecha concreta si se necesita comunicarla.<br>
**Incompleta:** «Entregar la memoria antes de la fecha indicada». No puede inventarse la fecha.<br>
**Límite:** «La entrega es el 18 de mayo, pero puedes poner otra fecha para que suene mejor». El sistema no debe modificar la fecha para mejorar el estilo.

Los enunciados son **ficticios** y se ofrecen como orientación. Puedes sustituirlos por otros acordes con tu caso.

</details>

## 3. Redactar una primera versión — 45 minutos

Escribe un prompt inicial que especifique la tarea, el público, el material disponible, las restricciones y el formato. No tiene que ser largo: debe permitir comprobar lo que se espera. Para separar instrucción y contenido a transformar, utiliza etiquetas legibles como `INSTRUCCIÓN` y `TEXTO DE ENTRADA`.

```text
Tarea: [qué debe hacer el sistema].
Destinatario: [para quién será la salida].
Material: [qué se facilita y dónde empieza y termina].
Conserva: [datos o decisiones que no deben cambiar].
Si falta información o hay ambigüedad: [conducta esperada].
Devuelve: [formato y extensión útiles].
```

Prueba esta primera versión con las cuatro entradas. Guarda el **texto exacto del prompt** y, si es posible, las salidas completas. No modifiques las entradas entre una versión y otra: de lo contrario, será más difícil atribuir la diferencia al cambio de instrucciones. Si no puedes obtener una salida por una limitación del servicio, registra el hecho; no completes la respuesta manualmente como si la hubiera generado.

## 4. Examinar errores y revisar el prompt — 55 minutos

Aplica los criterios de la tabla a cada salida. Anota al menos un acierto y un fallo o límite relevante. Después selecciona **dos cambios concretos** del prompt y explica qué problema intentan resolver. Por ejemplo: «añadir la instrucción de conservar fechas literalmente» y «pedir que señale la información ausente». Evita cambiar a la vez el modelo, las entradas y la instrucción si quieres observar el efecto de la revisión.

Redacta la versión 2 y repite las cuatro pruebas. Si un caso produce respuestas variables, puedes ejecutarlo otra vez y señalar la variación. No elijas solo la salida más favorable: documenta la evidencia que sustenta tu conclusión.

| Caso | V1: observación | Cambio aplicado | V2: observación | ¿Mejoró? |
|---|---|---|---|---|
| Ordinario | … | … | … | Sí / Parcial / No |
| Ambiguo | … | … | … | Sí / Parcial / No |
| Incompleto | … | … | … | Sí / Parcial / No |
| Límite | … | … | … | Sí / Parcial / No |

<details>
<summary><strong>Si ambas versiones ofrecen una respuesta correcta en todos los casos</strong></summary>

Esto no demuestra que sean equivalentes en cualquier situación. Busca una entrada adicional que ponga a prueba el límite de tu caso, o compara claridad, longitud y facilidad de revisión. No añadas pruebas solo para conseguir que falle una versión: deben ser plausibles para las personas que utilizarían el sistema.

</details>

## 5. Elegir y describir la versión que conservarías — 45 minutos

Selecciona la versión mejor sustentada por las pruebas. Puede ser la primera, la segunda o una tercera revisión breve si has detectado un fallo común. Explica **por qué** y señala al menos una limitación que permanece. Si la tarea requiere documentos actualizados, verificación independiente o acceso a información del usuario, indica que el prompt por sí solo no cubre esa necesidad; corresponderá al diseño del sistema.

Prepara un registro breve con el nombre y la fecha de la versión, la finalidad, las cuatro entradas de prueba, el resultado de la comparación y la decisión. La fecha identifica **tu versión de trabajo**, no garantiza la vigencia de los datos de las entradas.

## 6. Preparar la evidencia de la actividad — 30 minutos

Organiza la evidencia en un **documento breve** o formato equivalente aceptado por el Campus Virtual:

1. Descripción del caso y límites de uso.
2. Prompt V1 y prompt V2, íntegros.
3. Cuatro pruebas y resultados observados, con indicación de herramienta/modelo si consta.
4. Comparación según los criterios elegidos.
5. Versión seleccionada, justificación y fallo pendiente.

Se pueden añadir las salidas completas como anexo o mediante un enlace accesible para la docencia, si las condiciones de entrega lo permiten. **La entrega concreta y su evaluación oficial se indicarán en el Campus Virtual**; esta página describe el trabajo de aprendizaje, no fija una ponderación en la nota.

### Comprobación antes de terminar

- ¿Las dos versiones se probaron con las mismas cuatro entradas?
- ¿Las observaciones señalan contenido verificable y no solo «me gusta más»?
- ¿Se distingue un límite del prompt de un problema de fuentes o de datos?
- ¿Puede otra persona entender por qué se seleccionó la versión final?

<!-- IMAGEN OPCIONAL: esquema propio «Necesidad → Prompt V1 → cuatro pruebas → revisión → Prompt V2 → decisión». Si se crea, guardar en docs/assets/images/actividad1-ciclo-prompts.png y enlazar aquí. -->

**Siguiente trabajo del bloque:** en la [Actividad 2](actividad2-interaccion-contextual.md) se utilizarán las decisiones de interacción en una conversación de varios turnos, con contexto y correcciones explícitas.

### Material de apoyo

- [Tema 2. Diseño de prompts e interacción avanzada](../teoria/tema2-prompts-e-interaccion.md).
- [Ingeniería de Prompts](https://mltechdrawer.github.io/ChatGPT/2_IP/), material docente de referencia.
- [Google AI for Developers: estrategias de diseño de instrucciones](https://ai.google.dev/gemini-api/docs/prompting-strategies?hl=es).

[Volver a la presentación del bloque](../index.md)
