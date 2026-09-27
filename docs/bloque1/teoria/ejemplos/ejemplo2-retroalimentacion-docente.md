# Ejemplo 2. Una herramienta para reformular retroalimentación docente

**Caso ficticio · Tiempo estimado: 15 minutos, incluido en las 3 horas del Tema 1.**

Una profesora escribe observaciones breves para trabajos de estudiantes y quiere expresarlas de manera clara y constructiva. La herramienta propuesta recibe el borrador de comentario y una rúbrica ya seleccionada por la profesora; devuelve una **propuesta de redacción** que ella revisará antes de enviarla.

## Qué problema resuelve

Partimos de este comentario inventado: «La justificación es vaga; las fuentes no se relacionan con la conclusión. Revisar». La herramienta puede reformularlo así:

> «La propuesta identifica fuentes pertinentes, pero necesita explicar con mayor precisión cómo apoyan la conclusión. Sería útil incorporar un ejemplo concreto que conecte los resultados citados con la afirmación final».

La reformulación resulta más útil si respeta el significado del comentario original. La profesora debe comprobar que «fuentes pertinentes» está realmente respaldado por su revisión; si no lo está, esa frase tendría que corregirse. Una salida amable que inventa méritos no es una buena respuesta.

## Componentes y alcance

| Elemento | Decisión |
|---|---|
| Entrada | Comentario redactado por la profesora y, si procede, criterio de la rúbrica. |
| Instrucciones | Mantener el juicio original, proponer mejoras concretas y no inventar observaciones. |
| Modelo | Generar un borrador alternativo. |
| Aplicación | Mostrar borrador y comentario original uno junto al otro. |
| Validación | La profesora acepta, modifica o descarta el borrador. |
| Límite | No asignar calificaciones ni enviar mensajes automáticamente. |

Aquí **no hace falta una base de conocimientos** si el único propósito es reformular material que ya se ha proporcionado. Sí es importante concretar el alcance de la herramienta: la evaluación académica y la decisión de enviar el comentario corresponden a la profesora. En una implantación real, además, habría que decidir qué datos personales pueden introducirse y qué servicio los procesa.

## Pruebas de comportamiento

Una prueba consiste en proporcionar «Faltan las fuentes de los datos» y comprobar que la salida solicita fuentes sin inventarlas. Otra consiste en dar un comentario que incluya una calificación y comprobar que la herramienta no la altere. Un tercer caso sería introducir «Buen trabajo» sin más información: el sistema podría proponer una redacción más clara, pero no debería atribuir fortalezas concretas que no figuran en la entrada.

<details>
<summary><strong>¿Por qué llamamos sistema a algo tan pequeño?</strong></summary>

Porque alguien ha definido quién lo usa, qué datos admite, qué tarea realiza el modelo, cómo se presenta el borrador y quién autoriza su uso. Aunque la aplicación sea sencilla, esas decisiones forman parte del comportamiento final y pueden evaluarse por separado.

</details>

<!-- IMAGEN OPCIONAL: maqueta propia con dos paneles «Comentario original» y «Propuesta para revisar», más botones «Editar» y «Descartar». Guardar en docs/assets/images/tema1-ejemplo-retroalimentacion.png y enlazar aquí si se produce. -->

**Idea central:** incorporar un modelo a una tarea acotada también exige decisiones de diseño, aunque no haya recuperación de documentos ni automatización externa.

[Volver al Tema 1](../tema1-modelos-y-sistemas.md)
