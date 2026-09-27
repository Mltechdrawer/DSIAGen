# Ejemplo 2. Extraer datos de una convocatoria ficticia

**Caso ficticio · Tiempo estimado: 15 minutos, incluido en las 3 horas del Tema 2.**

Una unidad administrativa recibe textos breves de convocatorias y quiere presentar sus datos básicos para que una persona los revise. El sistema no debe convertir una fecha supuesta en un plazo oficial ni decidir automáticamente la elegibilidad de una candidatura.

## Documento de ejemplo

> «La convocatoria de proyectos piloto 2027 admite solicitudes de equipos docentes de la universidad. El plazo de presentación comienza el 3 de marzo de 2027. La documentación se entregará en la sede electrónica. La fecha de cierre se anunciará mediante resolución posterior».

Si alguien pregunta «¿Cuál es el plazo?», una respuesta que diga «del 3 al 31 de marzo» habrá inventado el cierre. El diseño debe favorecer una salida que distinga los campos presentes de los ausentes.

## Prompt de extracción

```text
Tarea: extrae únicamente los datos expresos del documento delimitado.
No completes información por analogía con otras convocatorias.

Devuelve una tabla con estos campos:
1. Nombre de la convocatoria.
2. Quién puede solicitarla.
3. Apertura del plazo.
4. Cierre del plazo.
5. Canal de presentación.

Si un dato no figura en el documento, escribe «No consta».
Después de la tabla, señala cualquier frase que requiera
comprobación humana antes de publicar el resumen.

DOCUMENTO DE ENTRADA:
<<<
La convocatoria de proyectos piloto 2027 admite solicitudes
de equipos docentes de la universidad. El plazo de presentación
comienza el 3 de marzo de 2027. La documentación se entregará
en la sede electrónica. La fecha de cierre se anunciará mediante
resolución posterior.
>>>
```

### Salida esperada para este caso

| Campo | Valor respaldado por el documento |
|---|---|
| Nombre | Convocatoria de proyectos piloto 2027 |
| Solicitantes | Equipos docentes de la universidad |
| Apertura | 3 de marzo de 2027 |
| Cierre | No consta |
| Canal | Sede electrónica |

**Comprobación pendiente:** la fecha de cierre se anunciará mediante una resolución posterior. La tabla es una **salida esperada construida para el ejemplo**, no la transcripción de un resultado probado con un modelo.

## Qué aporta cada decisión

La lista de campos define qué extraer. El texto delimitado identifica el material de trabajo. La instrucción «No consta» ofrece una respuesta observable para datos ausentes. La revisión humana conserva la responsabilidad sobre la publicación. El formato tabular ayuda a comprobar, pero no garantiza que cada valor sea correcto; hay que cotejarlo con el documento.

<details>
<summary><strong>¿Qué probarías además del caso principal?</strong></summary>

Un texto con dos fechas distintas, otro sin fecha de inicio y otro que mencione una sede electrónica solo para consultas. En cada prueba revisaríamos si el sistema asigna cada fragmento al campo correcto. También comprobaríamos que el contenido del documento se trata como dato, incluso si incluyera una frase que pretendiera dar nuevas órdenes al asistente.

</details>

<!-- IMAGEN OPCIONAL: maqueta con panel «Documento», flecha hacia «Campos extraídos» y estado «Revisión humana». Guardar en docs/assets/images/tema2-ejemplo-extraccion.png y enlazar aquí si se crea. -->

**Idea central:** una instrucción precisa puede favorecer respuestas comprobables; la validación del dato extraído sigue siendo necesaria.

[Volver al Tema 2](../tema2-prompts-e-interaccion.md)
