# Ejemplo 2. Consultar disponibilidad antes de reservar

**Caso ficticio · 25 minutos incluidos en el Tema 6. No se efectúa ninguna reserva real.**

Una persona dice: «Necesito la sala de seminarios el martes de 10:00 a 11:00. ¿Está libre?». La aplicación ofrece al modelo una herramienta de **consulta** de disponibilidad, pero no le concede automáticamente permiso para reservar.

```text
Estado inicial: consulta pendiente.
Modelo: propone consultar_disponibilidad(sala, martes, 10:00, 11:00).
Aplicación: valida parámetros y ejecuta la consulta autorizada.
Servicio: devuelve «Sala libre» o un error.
Modelo: informa del resultado confirmado; no afirma haber reservado.
```

Si la herramienta devuelve «Sala libre», una respuesta apropiada sería «La sala figura como disponible; todavía no está reservada. ¿Quieres que prepare la solicitud de reserva?». Incluso con una herramienta de reserva disponible, la aplicación debería comprobar permisos, pedir confirmación de los datos y **verificar después** la respuesta del servicio.

| Situación | Estado que debe comunicar el sistema |
|---|---|
| El modelo propone una consulta, pero aún no se ejecuta. | Disponibilidad desconocida. |
| La consulta devuelve «libre». | Disponible en el momento consultado; no reservado. |
| La aplicación solicita reservar, sin respuesta del servicio. | Reserva no confirmada. |
| El servicio devuelve identificador de reserva. | Reserva confirmada, según ese servicio. |
| El servicio no responde. | Estado pendiente de comprobación; no reintentar a ciegas. |

<details>
<summary><strong>¿Qué ocurriría si llega otra petición idéntica mientras la primera está pendiente?</strong></summary>

La aplicación debe comprobar si ya existe una operación en curso o completada para esa solicitud. Si envía dos reservas independientes podría duplicar la acción. Registrar un identificador de la solicitud y consultar el resultado permite actuar con más seguridad que confiar en una frase generada.

</details>

**Para analizar:** identifica qué pasos son de lectura, cuáles modifican un servicio y en qué punto se requiere una confirmación de la persona. La frase «sí, ya está reservado» solo está justificada cuando la herramienta responsable lo ha confirmado.

<!-- IMAGEN OPCIONAL: estados «Consulta», «Disponible», «Solicitud pendiente», «Reserva confirmada»; guardar en docs/assets/images/tema6-ejemplo-reserva.png. -->

[Volver al Tema 6](../tema6-automatizacion.md)
