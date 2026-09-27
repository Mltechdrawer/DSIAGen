# Tema 4. Incorporación y recuperación de conocimiento

**Dedicación estimada: 3 horas.** Incluye lectura, análisis de dos ejemplos y comprobación. La [Actividad 3](../actividades/actividad3-prototipo-con-conocimiento.md) tiene una dedicación propia de cinco horas.

| Recorrido | Tiempo orientativo |
|---|---:|
| 1. Por qué un sistema necesita conocimiento externo | 25 min |
| 2. Elegir y describir fuentes | 35 min |
| 3. Recuperar fragmentos pertinentes | 45 min |
| 4. Preparar evidencia para responder | 30 min |
| 5. Ejemplos de selección y recuperación | 30 min |
| 6. Síntesis y comprobación | 15 min |
| **Total** | **180 min** |

El [Bloque I](../../bloque1/index.md) abordó instrucciones, contexto y continuidad. Ahora aparece una necesidad distinta: responder sobre información que **no debe suponerse presente en los parámetros del modelo**, como una instrucción que ha cambiado esta semana o un conjunto de documentos propios. Incorporar conocimiento externo significa identificar las fuentes adecuadas y hacer llegar a la interacción la información pertinente. En este tema nos concentramos en **la selección y recuperación**; el [Tema 5](tema5-sistemas-rag.md) integrará esos resultados en un sistema RAG.

**Al finalizar podrás** distinguir fuente y respuesta, valorar autoridad y vigencia de documentos, comparar formas sencillas de recuperación y reconocer cuándo la información encontrada no basta para contestar.

## 1. Una pregunta que el modelo no puede resolver solo

Imaginemos un laboratorio universitario que participa en un proyecto de investigación en el que se recogen y analizan muestras biológicas. El equipo utiliza distintos procedimientos internos para garantizar que las muestras se obtienen, conservan y transportan correctamente. Una investigadora que acaba de incorporarse al proyecto necesita preparar una nueva recogida y pregunta: «¿Qué versión del protocolo de recogida de muestras se aplica al proyecto actual?».

Un modelo generativo puede describir procedimientos habituales para la recogida de muestras, pero no tiene por qué conocer el protocolo interno del laboratorio ni disponer de su versión vigente. Incluso si durante su entrenamiento hubiera procesado información semejante, no hay base para confiar en que conozca el documento concreto aprobado para ese proyecto.

La aplicación puede intervenir: consultar un repositorio autorizado, recuperar el documento del proyecto, localizar la información relevante y aportar el fragmento correspondiente a la petición. Este recorrido obliga a separar tres cuestiones: **qué fuente se permite consultar**, **qué fragmento responde a la pregunta** y **qué se puede afirmar a partir de él**. Un error en cualquiera de las tres puede producir una respuesta convincente pero equivocada.

<details>
<summary><strong>¿No bastaría con adjuntar todos los documentos?</strong></summary>

En un caso pequeño puede funcionar adjuntar unos pocos archivos. Cuando hay muchas versiones, contenido extenso o accesos diferentes, hace falta seleccionar. Aun cuando todo quepa en la ventana de contexto, el sistema debe poder justificar qué versión utilizó y si el fragmento era pertinente. Más información disponible no garantiza mejor evidencia.

</details>

## 2. Elegir y describir fuentes

Una **base de conocimiento** es el conjunto organizado de fuentes que una aplicación puede utilizar para localizar información sobre un ámbito determinado. Puede incluir, por ejemplo, documentos, páginas web, manuales o registros internos. No es solo una carpeta llena de archivos: las fuentes deben estar **identificadas, autorizadas y mantenidas** para la finalidad del sistema.

Antes de incorporar documentos a una base de conocimiento, conviene **describir cada fuente de forma explícita**. No basta con saber qué contiene: también necesitamos identificar quién es responsable de ella, cuál es su versión vigente, a qué ámbito se aplica, quién puede consultarla y dónde se encuentra el original. La siguiente tabla muestra algunos de los datos que pueden utilizarse para caracterizar una fuente antes de integrarla en el sistema.

| Dato sobre la fuente | Pregunta que resuelve | Ejemplo ficticio |
|---|---|---|
| Identificador y título | ¿Qué documento es? | PROT-07, «Recogida de muestras». |
| Responsable | ¿Quién puede corregirlo? | Coordinación del laboratorio. |
| Versión y fecha | ¿Cuál es la vigente? | v3, revisión de septiembre. |
| Ámbito | ¿A qué proyecto se aplica? | Estudio piloto A. |
| Acceso | ¿Quién puede consultarlo? | Equipo autorizado. |
| Ubicación | ¿Dónde está el original? | Repositorio institucional. |

Esta descripción permite distinguir entre **tener documentos disponibles y disponer de fuentes adecuadas para el sistema**. Identificar su procedencia, vigencia, ámbito y condiciones de acceso ayuda a decidir qué información puede utilizarse y a detectar situaciones en las que una fuente está desactualizada, no corresponde al caso consultado o no debería estar disponible para determinadas personas. La selección de fuentes es, por tanto, una decisión de diseño de la base de conocimiento.

Los datos que describen una fuente —por ejemplo, su título, versión, fecha, ámbito o responsable— se denominan **metadatos**. No constituyen necesariamente el contenido que queremos consultar, sino información sobre la propia fuente que permite identificarla, organizarla y decidir cuándo resulta aplicable.

Los metadatos ayudan a evitar que dos documentos con títulos parecidos se traten como equivalentes. También permiten retirar o reemplazar material obsoleto. Si una fuente no tiene fecha o responsable identificable, quizá pueda orientar una búsqueda, pero no debería presentarse sin más como instrucción oficial.

### Autoridad, vigencia y permisos

Para una cuestión de procedimiento, una versión aprobada por la unidad responsable tiene un valor distinto de una nota personal o de un borrador. El documento más reciente tampoco es siempre el aplicable: puede corresponder a **otro proyecto**. Y aunque una fuente sea correcta, el sistema no debe exponerla a personas sin acceso autorizado. La pertinencia temática no sustituye la verificación de procedencia y permisos.

<details>
<summary><strong>Fuente primaria y fuente secundaria</strong></summary>

La instrucción oficial de un proyecto es una fuente primaria para sus requisitos. Un resumen elaborado por una persona del equipo puede ayudar a localizarla, pero una respuesta sobre un plazo debería contrastarse con el original vigente. La relación cambia según la pregunta: para estudiar cómo se interpretó una instrucción, el resumen también podría ser el objeto de análisis.

</details>

<details>
<summary><strong>💡 Metáfora · El horario del vuelo</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

Imagina que una persona te dice que tu vuelo sale a las ocho de la mañana. Esa información puede ser útil y quizá sea correcta, pero si necesitas saber <strong>con certeza</strong> a qué hora debes estar en el aeropuerto, consultarás la información actualizada de la compañía aérea o tu tarjeta de embarque.

La persona que te informó actúa como una <strong>fuente secundaria</strong>: transmite o resume una información procedente de otro lugar. La información oficial del vuelo funciona como <strong>fuente primaria</strong> para comprobar el horario vigente.

Esto no significa que una fuente secundaria sea poco útil. Puede ayudarnos a localizar, resumir o comprender la información. La cuestión es <strong>qué fuente debemos utilizar para responder a cada pregunta</strong>.

</div>

</details>

![Metadatos de una fuente de conocimiento](../../assets/images/tema4-fuentes.png){ width="450" style="display:block; margin:auto;" }

<small><strong>Imagen.</strong> <em>Comprobación de la adecuación de una fuente según su versión, ámbito, fecha y responsabilidad.</em></small>

## 3. Recuperar fragmentos pertinentes

Supongamos que un laboratorio universitario utiliza el protocolo ficticio **PROT-07, «Recogida de muestras»**, para establecer cómo debe actuar el personal investigador durante la recogida, conservación y transporte de las muestras de un proyecto. El protocolo forma parte de la documentación interna del laboratorio y se actualiza cuando cambian los procedimientos. Hemos seleccionado este documento como fuente y comprobado que corresponde a la versión vigente del proyecto.

Si el documento es extenso, no siempre resulta conveniente utilizarlo completo cada vez que alguien formula una pregunta. Podemos prepararlo para que el sistema pueda localizar únicamente las partes que resulten relevantes.


### Del documento a los fragmentos

Una forma de preparar el contenido consiste en dividirlo en unidades más pequeñas denominadas **fragmentos** (*chunks*). Un fragmento puede corresponder, por ejemplo, a un párrafo, varios párrafos o una sección del documento. No es necesariamente una división que ya exista en la fuente: es una unidad que se crea para facilitar la recuperación posterior de información.

En un sistema real, quien lo diseña establece la **estrategia de fragmentación** (*chunking*), pero normalmente no separa manualmente cada fragmento. El software puede procesar los documentos siguiendo las reglas definidas: respetar párrafos o secciones, utilizar una longitud aproximada o mantener cierto solapamiento entre fragmentos para evitar que una información importante quede separada de su contexto.

Por ejemplo, una versión simplificada de PROT-07 podría dar lugar a fragmentos como estos:

```text
FUENTE
PROT-07 · Recogida de muestras · v3

FRAGMENTO 1
Preparación de las muestras
Las muestras deberán identificarse antes de iniciar
el procedimiento...

FRAGMENTO 2
Conservación
Las muestras deberán mantenerse refrigeradas hasta
su traslado...

FRAGMENTO 3
Transporte
El transporte al laboratorio deberá realizarse antes
de que transcurran...
```

Los tres fragmentos proceden de la misma fuente y deben conservar información que permita identificar su origen. Ante una consulta concreta, el sistema podrá intentar recuperar aquellos que estén relacionados con la pregunta sin tener que utilizar necesariamente el documento completo.

El tamaño y los límites de los fragmentos constituyen una decisión de diseño. Un fragmento demasiado pequeño puede perder información necesaria para interpretar su contenido; uno demasiado grande puede mezclar temas diferentes y dificultar la recuperación. Por ello, no existe un tamaño adecuado para todos los documentos y situaciones.

<details>
<summary><strong>💡 Metáfora · Las páginas de un libro</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

Imagina una biblioteca en la que, para localizar rápidamente una información, pudiéramos consultar por separado determinadas páginas de los libros. Sería mucho más rápido que revisar cada libro completo.

Pero esas páginas solo serían realmente útiles si conserváramos <strong>de qué libro proceden, a qué capítulo pertenecen y dónde estaban situadas</strong>. Una página aislada podría contener una frase cuyo significado depende de lo explicado antes o después.

Dividir un documento en fragmentos sigue una lógica parecida: permite <strong>recuperar únicamente las partes que pueden ser relevantes para una consulta</strong>, pero cada fragmento debe mantener su relación con la fuente original y suficiente contexto para poder interpretarlo correctamente.

</div>

</details>

### Preparar los fragmentos para poder encontrarlos

Una vez creados los fragmentos, necesitamos poder localizarlos cuando llegue una consulta. Para ello se prepara una estructura que permita buscarlos, que podemos denominar de forma general **índice**. No se trata necesariamente del índice de capítulos que encontramos al comienzo de un libro, sino de una estructura preparada para localizar posteriormente información dentro de una colección.

<details>
<summary><strong>💡 Metáfora · El catálogo de una biblioteca</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

Una biblioteca puede contener miles de libros, pero para encontrar uno no necesitamos recorrer físicamente todas las estanterías. El <strong>catálogo</strong> organiza información que permite localizar qué materiales pueden interesarnos y dónde encontrarlos.

Un índice utilizado por un sistema de recuperación cumple una función parecida. Los documentos ya han sido preparados y el sistema dispone de una estructura que le permite <strong>localizar qué fragmentos pueden estar relacionados con una consulta</strong> sin tener que revisar desde cero todo el contenido cada vez que alguien formula una pregunta.

</div>

</details>

Dependiendo del sistema, el índice puede facilitar búsquedas por palabras, por significado o mediante características asociadas a los fragmentos. Los metadatos que hemos descrito anteriormente —como versión, fecha, ámbito o procedencia— también pueden utilizarse para limitar qué contenido puede recuperarse.

Es importante distinguir dos operaciones:

- **Fragmentar** significa preparar previamente los documentos dividiéndolos en unidades que puedan recuperarse.
- **Recuperar** significa seleccionar, cuando llega una consulta, qué fragmentos de los disponibles pueden ser útiles para responderla.

Por tanto, los fragmentos no se crean de nuevo para cada pregunta. El sistema dispone de contenido previamente preparado y, ante una consulta, busca qué partes resultan pertinentes.

### Distintas formas de recuperar información

Una vez organizada la base de conocimiento, el sistema necesita decidir cómo localizar la información relevante para cada consulta. No todas las estrategias de búsqueda funcionan del mismo modo: algunas buscan coincidencias entre términos, otras intentan recuperar fragmentos relacionados por su significado y otras utilizan características de las propias fuentes para restringir los resultados. Cada método aporta ventajas, pero también puede recuperar información inadecuada o dejar fuera contenido relevante. La siguiente tabla compara estas estrategias atendiendo a qué buscan, qué ventajas pueden aportar y qué problemas pueden presentar.

| Método | Qué busca | Ejemplo de ventaja | Posible fallo |
|---|---|---|---|
| Búsqueda por palabras | Coincidencias de términos. | Encuentra una referencia exacta a «PROT-07». | Puede no recuperar un sinónimo. |
| Búsqueda semántica | Fragmentos relacionados por su significado. | Puede relacionar «plazo» con «fecha límite». | Puede traer un texto parecido pero de otro ámbito. |
| Filtros por metadatos | Fuentes que cumplen determinadas condiciones. | Limita a la versión vigente del proyecto A. | Metadatos incorrectos ocultan o incluyen documentos. |
| Combinación y reordenación | Integra diferentes señales y revisa los candidatos recuperados. | Distingue coincidencia literal y pertinencia. | Añade complejidad sin resolver fuentes defectuosas. |

Estas estrategias pueden combinarse para mejorar la recuperación. Una búsqueda puede localizar candidatos por su significado y, al mismo tiempo, aplicar filtros que limiten los resultados a determinadas versiones, fechas o ámbitos. El objetivo no es recuperar la mayor cantidad posible de información, sino seleccionar los fragmentos más pertinentes y adecuados para la consulta que debe resolver el sistema.

### Búsqueda semántica y representaciones vectoriales

La búsqueda por palabras resulta útil cuando conocemos los términos que aparecen en el documento. Sin embargo, una misma idea puede expresarse de formas diferentes. Una persona podría preguntar «¿Puedo cambiar la fecha del seminario?» mientras que el documento utiliza la expresión «modificación de la programación».

La **búsqueda semántica** intenta localizar contenido relacionado por su significado, aunque la consulta y el documento no utilicen exactamente las mismas palabras. Para hacerlo, el contenido de los fragmentos y de la consulta puede transformarse en una representación numérica denominada habitualmente **embedding**. Estas representaciones son vectores que permiten estimar qué contenidos se encuentran próximos por su significado.

Esta transformación se realiza automáticamente mediante un modelo preparado para generar estas representaciones; quien diseña el sistema no tiene que escribir manualmente los valores del vector.

No necesitamos calcular estos vectores en este tema. Lo importante es comprender la idea: el sistema puede comparar la representación de una pregunta con las representaciones de los fragmentos disponibles para localizar aquellos que parecen semánticamente relacionados.

Sin embargo, «se parece a la pregunta» no significa «contiene la respuesta correcta». Un fragmento sobre otro curso, otra versión o un procedimiento diferente puede estar muy próximo semánticamente y, aun así, ser inaplicable. Por ello, la búsqueda semántica puede combinarse con filtros por metadatos y con otras comprobaciones.

### Recuperar no significa todavía responder

Volvamos a la pregunta «¿Puedo cambiar la fecha del seminario?». El sistema podría recuperar un fragmento que habla de «modificación de la programación». Ese resultado es un candidato relevante, pero todavía debemos comprobar qué afirma realmente: puede explicar cómo **solicitar un cambio**, quién puede **autorizarlo** o simplemente cómo debe **comunicarse** una modificación ya aprobada.

Recuperar un fragmento pertinente es, por tanto, un paso para obtener la información necesaria, pero no garantiza por sí solo que dispongamos de evidencia suficiente para responder. En el siguiente apartado veremos cómo comprobar los fragmentos recuperados antes de utilizarlos para fundamentar una respuesta.

## 4. Preparar evidencia para una respuesta

En este contexto llamaremos **evidencia** a la información recuperada de las fuentes que, después de comprobar su procedencia, vigencia y relación con la consulta, puede utilizarse para fundamentar una respuesta. Por tanto, **un fragmento recuperado no constituye automáticamente evidencia suficiente**: primero debemos comprobar qué afirma realmente y si resulta aplicable al caso.

Después de buscar conviene revisar si los resultados son **suficientes**, **compatibles** y **autorizados**. Un pasaje que menciona una fecha no confirma necesariamente de qué entrega se trata. Dos fuentes que se contradicen pueden indicar un cambio de versión o un conflicto pendiente. La aplicación debería ofrecer al modelo el fragmento, su procedencia y la pregunta, manteniendo distinguibles **instrucciones del sistema** y **contenido de los documentos**.

Una ficha mínima de evidencia puede contener: pregunta, documento y versión, pasaje localizado, sección o página, fecha de consulta y duda pendiente. Esto permite comprobar después qué se usó. No es una promesa de que el modelo citará bien: habrá que comparar la respuesta con el fragmento original.

<details>
<summary><strong>¿Qué hacer si no aparece evidencia suficiente?</strong></summary>

Declarar que no se ha localizado una base fiable para responder, solicitar precisión sobre la pregunta o derivar la consulta a la fuente responsable. Una respuesta general del modelo puede ser útil como explicación de un concepto, pero no debe disfrazarse de dato confirmado del repositorio.

</details>

<details>
<summary><strong>💡 Metáfora · Las piezas antes de montar el puzle</strong></summary>

<div style="background-color: #FFF9EC; padding: 12px 16px;">

Imagina que intentas reconstruir una imagen a partir de las piezas de un puzle. Haber encontrado varias piezas no significa que ya puedas saber qué muestra la imagen: algunas pueden pertenecer a otra zona, faltar piezas importantes o incluso haberse mezclado piezas de otro puzle.

Preparar la evidencia para una respuesta se parece a <strong>comprobar las piezas antes de utilizarlas</strong>. Hay que verificar que corresponden al problema que queremos resolver, que son compatibles entre sí y que disponemos de suficientes elementos para sostener la interpretación.

Si faltan piezas esenciales, lo adecuado no es imaginar qué debería haber en el hueco, sino <strong>reconocer qué información falta</strong>. Del mismo modo, un sistema de IA generativa no debería convertir una evidencia insuficiente en una respuesta aparentemente confirmada.

</div>

</details>

![Selección de fragmentos con procedencia](../../assets/images/tema4-recuperacion.png){ width="500" style="display:block; margin:auto;" }

<small><strong>Imagen.</strong> <em>Selección y comprobación de la evidencia necesaria para fundamentar una respuesta.</em></small>

## 5. Ejemplos para analizar

Los dos casos son ficticios y están desarrollados en archivos aparte:

1. [Ejemplo 1. Dos versiones de un protocolo de proyecto](ejemplos/tema4-ejemplo1-versiones-protocolo.md). Permite decidir qué documento es aplicable antes de buscar dentro de él.
2. [Ejemplo 2. Una búsqueda que encuentra el pasaje equivocado](ejemplos/tema4-ejemplo2-busqueda-ambigua.md). Compara coincidencia temática y evidencia suficiente.

Durante la lectura identifica un dato de procedencia que evita un error y una pregunta que el sistema todavía no debería responder.

## 6. Síntesis y comprobación

Incorporar conocimiento externo supone **seleccionar y describir las fuentes, preparar su contenido para poder localizarlo, recuperar los fragmentos pertinentes y comprobar si proporcionan evidencia suficiente**. El proceso puede resumirse así:

**fuentes → metadatos → fragmentación → indexación → consulta → recuperación → comprobación de la evidencia**

La calidad de la recuperación no se mide solo por encontrar texto relacionado, sino por aportar información aplicable, vigente y verificable. En el siguiente tema veremos cómo incorporar la evidencia recuperada al contexto del modelo para generar una respuesta.

1. ¿Por qué un fragmento muy similar a la pregunta podría ser inadecuado?
2. ¿Qué metadatos mínimos guardarías para diferenciar dos versiones de una guía?
3. Si dos documentos oficiales vigentes ofrecen requisitos distintos, ¿debería escoger el sistema uno por su cuenta?
4. ¿Qué diferencia una fuente disponible en el repositorio de un fragmento que llega al modelo en la petición actual?

<details>
<summary><strong>Orientaciones de respuesta</strong></summary>

<p>1. Puede corresponder a otro curso, otra versión o un ámbito diferente.</p>
<p>2. Identificador, versión, fecha, ámbito, responsable y referencia al original.</p>
<p>3. No sin una regla de precedencia autorizada; hay que señalar el conflicto y consultar a quien corresponda.</p>
<p>4. La selección y el acceso son pasos separados: el modelo solo puede utilizar el material efectivamente aportado por la aplicación o por una herramienta disponible.</p>

</details>

**Para continuar:** el [Tema 5](tema5-sistemas-rag.md) estudia cómo integrar la recuperación con la generación de respuestas; la [Actividad 3](../actividades/actividad3-prototipo-con-conocimiento.md) permitirá probar un prototipo con fuentes controladas.

### Lecturas de referencia

- [OpenAI: recuperación y búsqueda semántica](https://developers.openai.com/api/docs/guides/retrieval). Ejemplo de indexación y búsqueda sobre archivos.
- [Microsoft Learn: introducción a RAG](https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview). Relación entre recuperación, fuentes y generación.

[Volver a la presentación del bloque](../index.md)
