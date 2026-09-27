# Ejemplo 2. Un borrador de informe de investigación con aprobación

**Caso ficticio · 15 minutos incluidos en el Tema 7.** Un equipo quiere preparar un resumen de avances trimestrales. Aporta tres notas de trabajo con referencias identificadas. El sistema produce un borrador, pero **no lo publica ni lo envía**. Una persona responsable revisa afirmaciones y autoriza la versión final.

El recorrido previsto es:

1. Recibir notas con identificador y fecha. Una nota sin procedencia queda pendiente.
2. Seleccionar solo las notas del trimestre actual y preparar fragmentos con sus fuentes.
3. Pedir al modelo un borrador que distinga resultado confirmado y trabajo previsto.
4. Mostrar el borrador junto a los fragmentos originales.
5. Registrar cambios de la persona revisora; dejar el texto aprobado para una publicación posterior y separada.

| Regla de arquitectura | Motivo |
|---|---|
| El modelo no accede al repositorio completo sin selección. | Evita incorporar notas ajenas al informe. |
| Cada frase verificable remite a una nota. | Facilita la revisión del contenido. |
| No hay herramienta de publicación en el prototipo. | Separa borrador y difusión. |
| Una corrección humana se conserva en la versión vigente. | Evita repetir el error en el mismo informe. |

Si una nota dice «Se espera realizar veinte entrevistas», no sería correcto escribir «Se realizaron veinte entrevistas». Ese error puede detectarse aunque el documento correcto haya sido recuperado: correspondería a la **generación o a la revisión**, no necesariamente a la búsqueda.

<details>
<summary><strong>¿Qué pasaría si una de las tres notas cambia?</strong></summary>

Se identifica la versión sustituida, se vuelve a generar o revisar el apartado afectado y se registra cuál de las dos versiones fundamenta el texto aprobado. No se presupone que un resumen anterior siga siendo válido tras actualizar su fuente.

</details>

**Para analizar:** indica un control previo al modelo, uno posterior y una condición que obligaría a detener el flujo.

<!-- IMAGEN OPCIONAL: notas identificadas → borrador → comparación → aprobación humana; guardar en docs/assets/images/tema7-ejemplo-informe.png. -->

[Volver al Tema 7](../tema7-arquitectura-e-integracion.md)
