# Ejemplo 1. Consultas fundamentadas en instrucciones breves

**Caso ficticio · 25 minutos incluidos en el Tema 5.** Un pequeño repositorio contiene dos documentos del mismo proyecto:

- **DOC-1, «Preparación del informe», v2, apartado 2:** «El informe tendrá un máximo de seis páginas y se entregará en PDF».
- **DOC-2, «Presentación», v2, apartado 4:** «La exposición durará diez minutos. Puede utilizarse una presentación visual».

Ambos documentos son públicos para los integrantes del proyecto. La aplicación conserva identificador, versión y apartado de cada fragmento. Si se pregunta «¿Cuánto puede ocupar el informe?», se recupera DOC-1. Una respuesta ilustrativa sería «Hasta seis páginas, según DOC-1 v2, apartado 2». Después se verifica que **«seis páginas»** figura realmente en el original.

La segunda pregunta, «¿Hay que entregar las diapositivas antes de la exposición?», es diferente. DOC-2 permite usar una presentación, pero **no fija una entrega previa**. El sistema debería contestar «No consta en los documentos facilitados si hay que entregarlas antes» y ofrecer el apartado consultado. Responder «sí, un día antes» sería inventar un requisito.

| Consulta | Fragmento pertinente | Respuesta respaldada |
|---|---|---|
| Extensión del informe | DOC-1, apartado 2 | Máximo seis páginas. |
| Duración de exposición | DOC-2, apartado 4 | Diez minutos. |
| Entrega previa de diapositivas | No consta en DOC-1 ni DOC-2 | No puede confirmarse. |

<details>
<summary><strong>¿Qué parte de la prueba corresponde a recuperación y cuál a generación?</strong></summary>

**Recuperación:** comprobar que la pregunta sobre extensión entrega DOC-1 y no solo DOC-2; que la pregunta sobre diapositivas permite inspeccionar DOC-2. **Generación:** comprobar que se expresan únicamente las conclusiones apoyadas por esos pasajes y que se reconoce la ausencia de la condición de entrega.

</details>

El ejemplo puede realizarse incluso de forma manual: se seleccionan fragmentos, se aportan al modelo y se contrastan las respuestas con los originales. Eso permite entender el patrón antes de añadir un índice automático.

<!-- IMAGEN OPCIONAL: tres preguntas frente a dos fuentes, indicando «respuesta» o «no consta»; guardar en docs/assets/images/tema5-ejemplo-consultas.png. -->

[Volver al Tema 5](../tema5-sistemas-rag.md)
