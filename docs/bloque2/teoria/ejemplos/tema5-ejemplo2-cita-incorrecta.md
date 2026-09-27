# Ejemplo 2. Una cita que no respalda la respuesta

**Caso ficticio · 30 minutos incluidos en el Tema 5.** Un sistema recibe la pregunta «¿La evaluación final puede realizarse en grupo?». Recupera una instrucción que dice:

> **Apartado 5, “Presentación”:** «La presentación de resultados puede realizarse por equipos de hasta tres personas».

El modelo responde: «Sí, la evaluación final puede realizarse en grupos de hasta tres personas» y cita el apartado 5. La cita existe, pero el apartado habla de **la presentación**, no necesariamente de **toda la evaluación final**. La respuesta ha ampliado indebidamente el alcance de la fuente.

### Diagnóstico por etapas

| Etapa | Pregunta | Observación |
|---|---|---|
| Colección | ¿Hay una guía vigente de evaluación? | Hay que comprobarlo. |
| Recuperación | ¿Se recuperó el apartado sobre evaluación final? | Solo se muestra «Presentación». |
| Generación | ¿La respuesta preserva el alcance? | No: equipara presentación y evaluación. |
| Cita | ¿Respalda toda la afirmación? | No: la referencia es real, pero insuficiente. |

La corrección no consiste en añadir más referencias al final. Si existe otra sección sobre evaluación, hay que recuperarla y contrastarla. Si no existe, una salida fundamentada sería: «El apartado 5 permite realizar **la presentación** en equipos de hasta tres personas; el material recuperado no confirma si el resto de la evaluación se realiza en grupo».

<details>
<summary><strong>¿Y si el mismo apartado dice también «La memoria es individual»?</strong></summary>

El fragmento debe conservar ambas frases. Si la división del documento solo recupera la primera, aparece además un fallo de fragmentación. La respuesta debería distinguir memoria individual y presentación en equipo, sin reducirlo todo a una etiqueta «evaluación grupal».

</details>

**Para analizar:** ¿qué evidencia adicional necesitarías para contestar sin reservas a la pregunta original? ¿Qué cambiarías en la búsqueda y qué cambiarías en la instrucción de generación?

<!-- IMAGEN OPCIONAL: afirmación y pasaje con términos «evaluación» y «presentación» resaltados para mostrar diferencia de alcance; guardar en docs/assets/images/tema5-ejemplo-cita.png. -->

[Volver al Tema 5](../tema5-sistemas-rag.md)
