# Ejemplo 1. Un asistente para consultar una guía académica

**Caso ficticio · Tiempo estimado: 15 minutos, incluido en las 3 horas del Tema 1.**

Una asignatura publica cada año la guía de su trabajo final. La versión del curso actual indica que la memoria se entrega el **20 de junio** y que la presentación oral se celebra el **30 de junio**. La profesora observa que las preguntas sobre plazos se repiten y quiere facilitar la consulta sin convertir el asistente en una autoridad que modifique la guía.

## Primera aproximación: preguntar a un modelo

> **Estudiante:** «¿Hasta cuándo se entrega el trabajo final?»  
> **Modelo:** «Generalmente, los trabajos finales se entregan a finales de junio. Consulta la plataforma para confirmar la fecha».

La respuesta es prudente, pero no resuelve la pregunta. El modelo no dispone de la guía específica ni sabe si «trabajo final» designa la memoria o la exposición. Tampoco puede garantizar la fecha vigente solo porque responda con soltura.

## Segunda aproximación: definir el sistema

La profesora define que el servicio solo responderá acerca de documentos publicados de la asignatura. La aplicación identifica la guía vigente, localiza los apartados «Entrega de la memoria» y «Presentación oral» y los incluye como contexto de la consulta. Las instrucciones piden distinguir ambos hitos, nombrar el apartado utilizado y reconocer los casos en que los documentos no contienen la respuesta.

Una salida adecuada a la pregunta ambigua sería:

> «Si te refieres a la **memoria escrita**, el plazo es el **20 de junio**, según el apartado “Entrega de la memoria” de la guía del curso. La **presentación oral** está prevista para el **30 de junio**. Si tu consulta se refiere a una prórroga individual, debes dirigirte al profesorado responsable».

El texto anterior es una **respuesta esperada para un ejemplo ficticio**, no una demostración de que cualquier sistema vaya a producirla. El diseño ha mejorado las condiciones para obtenerla, pero todavía habría que probarlo.

| Elemento | Decisión |
|---|---|
| Necesidad | Resolver dudas frecuentes sobre requisitos vigentes. |
| Modelo | Redactar explicaciones a partir del contexto aportado. |
| Documentos | Usar únicamente la guía autorizada del curso actual. |
| Aplicación | Seleccionar fragmentos relevantes y mostrar referencias. |
| Límite | No resolver excepciones personales ni alterar fechas. |
| Supervisión | Profesorado revisa fallos y actualiza documentos. |

## ¿Dónde puede fallar?

Si se selecciona la guía del curso anterior, el sistema puede responder de forma coherente pero equivocada. Si la búsqueda recupera solo el apartado de la exposición, puede confundir ambas fechas. Si aparece una instrucción dentro de un documento que intenta cambiar el comportamiento del asistente, el contenido recuperado no debe tratarse como una orden autorizada. Si no encuentra el plazo, debe reconocer la falta de fundamento.

<details>
<summary><strong>Para pensar: ¿qué revisarías en una prueba?</strong></summary>

Probaría al menos «¿Cuándo se entrega la memoria?», «¿Cuándo es la exposición?», «¿Hasta cuándo se entrega el trabajo final?» y «¿Me concedes una prórroga?». En los tres primeros casos revisaría fecha, apartado citado y versión de la guía. En el cuarto comprobaría que el sistema no promete una excepción que no puede conceder.

</details>

<!-- IMAGEN OPCIONAL: captura ficticia con pregunta, respuesta, versión y apartado de la guía. Guardar en docs/assets/images/tema1-ejemplo-guia.png y añadir aquí ![Consulta a la guía](../../../assets/images/tema1-ejemplo-guia.png). Evitar capturas con datos reales del alumnado. -->

**Idea central:** el modelo redacta, mientras que el sistema determina qué guía se utiliza, cómo se recupera, qué se muestra y cuándo debe intervenir una persona.

[Volver al Tema 1](../tema1-modelos-y-sistemas.md)
