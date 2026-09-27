# Ejemplo 1. Evaluar respuestas basadas en documentos

**Caso ficticio · 25 minutos incluidos en el Tema 8.** Un prototipo responde preguntas sobre las instrucciones de un proyecto. Las fuentes ficticias establecen: «El informe tiene un máximo de seis páginas» y «La exposición dura diez minutos». No fijan una fecha de entrega.

Antes de probarlo se definen tres resultados esperados:

| Consulta | Resultado esperado | Fuente o conducta |
|---|---|---|
| «¿Cuánto puede ocupar el informe?» | Seis páginas. | Apartado del informe. |
| «¿Cuándo se entrega?» | No consta. | Reconocer ausencia de dato. |
| «¿Cuántos minutos tengo para la exposición?» | Diez minutos. | Apartado de presentación. |

Supongamos que, al ejecutar el sistema, se obtienen estas **salidas inventadas para analizar el método**: la primera acierta y cita el apartado correcto; la segunda inventa «viernes a las 18:00»; la tercera da diez minutos pero cita por error el apartado de páginas. Los tres casos no equivalen a «dos respuestas correctas de tres». La segunda produce una afirmación no fundamentada; la tercera acierta el dato pero falla en **trazabilidad**.

| Prueba | Dato | Cita | Diagnóstico inicial |
|---|---|---|---|
| Informe | Correcto | Correcta | Caso superado. |
| Entrega | Inventado | Ausente | Fallo de abstención o generación. |
| Exposición | Correcto | Incorrecta | Fallo de presentación o atribución de fuente. |

<details>
<summary><strong>¿Qué revisarías para reparar la segunda respuesta?</strong></summary>

Primero si el sistema recibió algún fragmento que pudiera contener la fecha. Después la instrucción para responder «no consta» cuando falta evidencia y, finalmente, un control que compare las afirmaciones con las fuentes. Repetiría la misma prueba tras el cambio. Sin conocer el pasaje recibido no puede atribuirse el fallo con seguridad a una sola etapa.

</details>

**Conclusión limitada:** en estos casos ficticios aparece un fallo crítico sobre una fecha y otro de cita. No permite estimar una tasa general de éxito.

<!-- IMAGEN OPCIONAL: tabla de tres pruebas con columnas dato/cita y marcas de fallo, guardar en docs/assets/images/tema8-ejemplo-documentos.png. -->

[Volver al Tema 8](../tema8-calidad-y-evaluacion.md)
