# Ejemplo 1. Una explicación para alumnado que comienza la asignatura

**Caso ficticio · Tiempo estimado: 15 minutos, incluido en las 3 horas del Tema 2.**

Una docente necesita un texto breve para explicar por qué las claves primarias importan en una base de datos. El público es alumnado universitario que ya conoce las tablas, pero aún no ha estudiado la integridad referencial. El resultado se incorporará a una página introductoria, por lo que debe ser claro y técnicamente correcto.

## Primera versión del prompt

> «Explica las claves primarias».

Esta instrucción deja sin definir el nivel, la extensión y el propósito. Una respuesta podría ser técnicamente amplia pero poco adecuada para el alumnado. Para mejorar el prompt, no hace falta añadir un personaje grandilocuente; hace falta concretar la tarea.

## Segunda versión

```text
Explica qué es una clave primaria a estudiantes universitarios
que ya saben qué es una tabla, pero todavía no han estudiado
integridad referencial. Usa un ejemplo de una biblioteca.
Incluye por qué no basta con utilizar el nombre de una persona
como identificador. Extensión aproximada: 180 palabras.
```

Ahora podemos verificar si la salida identifica cada fila de manera unívoca, si el ejemplo se comprende y si evita introducir conceptos que todavía no se han explicado. También podemos comprobar si la extensión es apropiada para la página.

### Una posible respuesta que aún habría que revisar

> «En una tabla de préstamos de biblioteca, cada préstamo necesita una forma de distinguirse de los demás. Un número de préstamo puede servir como clave primaria: identifica de forma única cada registro. El nombre de una persona no suele servir, porque dos personas pueden llamarse igual y una misma persona puede realizar varios préstamos. Si la tabla incluyera dos registros con el mismo identificador de préstamo, sería difícil saber a cuál se refiere una consulta concreta».

El fragmento es **una salida ilustrativa redactada para este ejemplo**, no un resultado observado de una prueba. Antes de publicarlo, la docente revisaría si «clave primaria» está explicada con suficiente precisión y si conviene añadir que el valor no puede ser nulo. Si la aplicación generara respuestas para muchas preguntas, sería necesario comprobar otros casos además de este.

<details>
<summary><strong>¿Qué decisión de interacción falta si el sistema permite preguntas libres?</strong></summary>

Habría que decidir qué hacer si el estudiante pregunta por conceptos que la página aún no introduce. Por ejemplo, podría dar una explicación breve y ofrecer una aclaración, o remitir a un apartado posterior. El prompt no debe forzar una explicación interminable por responder a toda costa.

</details>

## De la instrucción a una pequeña prueba

| Caso | Qué queremos observar |
|---|---|
| «¿Por qué no usar el nombre?» | Menciona duplicados y posibles cambios sin atribuir propiedades inexistentes. |
| «¿La clave primaria es siempre un número?» | Reconoce que no tiene por qué serlo. |
| «Explícalo en una frase» | Ajusta la extensión sin perder la idea de identificación única. |

En una revisión, conviene modificar solo el elemento del prompt relacionado con el fallo observado. Si una respuesta incluye vocabulario demasiado avanzado, se puede precisar el nivel esperado; si atribuye propiedades que no aparecen en el material, hay que revisar el fundamento de esas afirmaciones.

<!-- IMAGEN OPCIONAL: dos tarjetas con una instrucción vaga y otra definida, acompañadas por criterios de revisión. Guardar en docs/assets/images/tema2-ejemplo-explicacion.png y enlazar aquí si se crea. -->

**Idea central:** la utilidad del prompt se juzga respecto a una necesidad docente y a varios casos de prueba, no por lo impresionante de una única respuesta.

[Volver al Tema 2](../tema2-prompts-e-interaccion.md)
