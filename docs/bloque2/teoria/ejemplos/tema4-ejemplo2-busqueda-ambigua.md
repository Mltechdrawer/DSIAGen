# Ejemplo 2. Una búsqueda que encuentra el pasaje equivocado

**Caso ficticio · 15 minutos incluidos en el Tema 4.** Una persona pregunta «¿Puede modificarse la fecha del seminario?». El repositorio contiene dos fragmentos:

> **Documento A, “Programa de seminarios”, sección 3:** «Los cambios de fecha deben solicitarse a la coordinación con una semana de antelación. La coordinación confirmará si son posibles».  
> **Documento B, “Aviso de calendario”, sección 1:** «El seminario del grupo B se trasladó al viernes 10».

Una búsqueda que dé mucho peso a las palabras «fecha del seminario» puede mostrar primero B. Pero B informa sobre **un cambio ya realizado**, mientras que la pregunta trata de **si se permite solicitar otro**. Para responder hay que recuperar A, distinguir «solicitar» de «autorizar» y citar el apartado adecuado.

| Interpretación de la respuesta | ¿Se apoya en A? |
|---|---|
| «Puede solicitarse un cambio con al menos una semana de antelación». | Sí. |
| «Cualquier cambio solicitado será aprobado». | No. |
| «Todos los seminarios pasan al viernes 10». | No; B habla de un grupo concreto. |

Una respuesta cuidadosa diría que el cambio **puede solicitarse**, indicaría el plazo previsto en A y aclararía que la coordinación debe confirmarlo. Si no se conoce el grupo o el seminario, puede hacerse una pregunta adicional. El pasaje B quizá resulte útil para otra consulta, pero su cercanía temática no le concede autoridad sobre el procedimiento.

<details>
<summary><strong>¿Qué fallo se intenta diagnosticar aquí?</strong></summary>

Un fallo de **selección e interpretación de evidencia**, no necesariamente un fallo de redacción. Cambiar el prompt del modelo no arregla por sí solo una búsqueda que nunca entrega la sección 3 del Documento A.

</details>

<!-- IMAGEN OPCIONAL: resultados A y B con las expresiones «solicitar» y «cambio ya realizado» resaltadas; guardar en docs/assets/images/tema4-ejemplo-busqueda.png. -->

[Volver al Tema 4](../tema4-conocimiento-externo.md)
