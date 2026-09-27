# Ejemplo 1. Preparar y aprobar un boletín de proyecto

**Caso ficticio · 25 minutos incluidos en el Tema 6.** La coordinación de un proyecto quiere publicar cada mes un boletín interno. Recibe tres novedades, genera un borrador y lo revisa antes de difundirlo. Los textos de entrada son inventados para el ejemplo.

| Paso | Responsable | Entrada → salida | Control |
|---|---|---|---|
| 1. Recibir novedades | Aplicación | Tres fichas → registro con fecha y procedencia. | Rechazar fichas sin fuente. |
| 2. Preparar síntesis | Modelo | Fichas autorizadas → borrador. | Conservar nombres y fechas; no añadir logros. |
| 3. Verificar | Coordinación | Borrador + fichas → correcciones o aprobación. | Contrastar afirmaciones con fichas. |
| 4. Publicar | Herramienta de envío | Versión aprobada → entrega. | Verificar destinatarios y confirmación. |

La IA redacta un **borrador**; no decide que ya está aprobado. Si una ficha dice «se propondrá una reunión en octubre», el boletín no debe anunciar «reunión confirmada para el 10 de octubre». La persona revisora necesita ver simultáneamente el borrador y las fichas para detectar esa alteración.

### Bifurcaciones necesarias

Si falta una fuente, el registro queda **pendiente** y no se genera el boletín definitivo. Si la coordinación rechaza un párrafo, se revisa solo el borrador afectado. Si el servicio de envío no devuelve confirmación, se investiga antes de intentar publicar otra vez para no enviar duplicados.

<details>
<summary><strong>¿Dónde pondrías la confirmación humana?</strong></summary>

Antes del paso 4, después de comparar borrador y fichas. La confirmación debe corresponder al contenido **y** a la lista de destinatarios. Pulsar «aprobar» sin esos datos visibles no aporta un control verificable.

</details>

En una versión inicial de este flujo puede representarse manualmente la revisión y el envío: el aprendizaje consiste en especificar estados, decisiones y límites, sin necesidad de conectar un servicio de correo real.

<!-- IMAGEN OPCIONAL: flujo «Ficha → Borrador → Revisión» con dos salidas «Corregir» y «Publicar», guardar en docs/assets/images/tema6-ejemplo-boletin.png. -->

[Volver al Tema 6](../tema6-automatizacion.md)
