# Ejemplo 1. Planificar una sesión en varios turnos

**Caso ficticio · Tiempo estimado: 30 minutos, incluido en las 4 horas del Tema 3.**

Una profesora quiere preparar una sesión introductoria sobre bases de datos. La conversación dura varios turnos y algunas decisiones cambian. El ejemplo permite distinguir entre historial visible, estado de la tarea y contexto que recibe el modelo en cada petición.

## Primer turno: definir las condiciones

> **Profesora:** «Prepara una sesión de 90 minutos para estudiantes de primer curso que conocen las tablas, pero no han trabajado con claves. Quiero introducir la clave primaria con un ejemplo de biblioteca. La sesión será presencial».

La aplicación podría representar el estado vigente de manera explícita:

| Campo | Valor | Procedencia |
|---|---|---|
| Público | Primer curso; conocen las tablas | Petición de la profesora |
| Duración | 90 minutos | Petición de la profesora |
| Objetivo | Introducir la clave primaria | Petición de la profesora |
| Ejemplo | Biblioteca | Petición de la profesora |
| Modalidad | Presencial | Petición de la profesora |

Este estado no es necesariamente una «memoria personal» de la profesora. Son datos **del proyecto de esta sesión**. Si se prepara otra asignatura, no deben heredarse por defecto.

## Segundo turno: una referencia al plan anterior

> **Profesora:** «La actividad inicial es demasiado larga. Redúcela y da más tiempo a que identifiquen errores en una tabla».

Para entender «la actividad inicial», el sistema necesita conocer el plan que acaba de proponer, o al menos sus partes relevantes. En cambio, para mantener la duración total y el nivel debe disponer de las condiciones del primer turno. Si solo recibe el último mensaje, podría hacer una revisión genérica sin respetar los 90 minutos.

Una respuesta pertinente debería **redistribuir** tiempos y comprobar que el total siga siendo 90 minutos. Si desconoce la duración de la actividad inicial, debería pedir el plan o señalar que está elaborando una propuesta nueva en vez de fingir que modifica el anterior.

## Tercer turno: una corrección con prioridad

> **Profesora:** «Finalmente la clase tendrá 60 minutos, no 90. Mantén el análisis de errores y elimina la parte de diseño de tablas».

Ahora el estado debe actualizarse:

| Campo | Valor vigente | Qué ocurre con lo anterior |
|---|---|---|
| Duración | **60 minutos** | 90 minutos queda sustituido. |
| Análisis de errores | Se mantiene | Continúa siendo una prioridad. |
| Diseño de tablas | Se elimina | No debe aparecer en la propuesta final. |

Una síntesis defectuosa diría «La sesión dura entre 60 y 90 minutos»; el historial menciona ambas cifras, pero la **decisión vigente** solo es 60. La profesora debería poder ver y corregir el estado si el sistema ha interpretado mal una instrucción.

<details>
<summary><strong>Posible contexto para la siguiente petición del modelo</strong></summary>

```text
Tarea actual: revisar el plan de la sesión.
Estado confirmado: alumnado de primer curso que conoce las tablas;
objetivo de introducir la clave primaria; ejemplo de biblioteca;
modalidad presencial; duración vigente de 60 minutos.
Decisiones recientes: mantener el análisis de errores;
eliminar el diseño de tablas. La duración de 90 minutos fue sustituida.
Material: versión más reciente del plan generado, si existe.
```

El texto es **un esquema didáctico** del contexto; el diseño real depende de la aplicación. Su principal ventaja es que diferencia las decisiones actuales de las sustituidas.

</details>

## Cuarto turno: detectar información que todavía falta

> **Profesora:** «Incluye un ejemplo con datos de mi grupo actual».

El sistema no dispone de esos datos. La respuesta adecuada sería pedir un conjunto de datos apropiado, proponer datos **ficticios** o aclarar qué información puede utilizarse. No debería suponer que puede acceder a los datos del alumnado ni reutilizar datos personales de otra conversación.

### Para analizar el caso

1. ¿Qué partes de la primera petición son necesarias en el tercer turno?
2. ¿Qué información debería guardarse si se cierra la sesión y la profesora vuelve otro día a este mismo proyecto?
3. ¿Qué parte del historial resultaría poco útil para redactar el plan definitivo?

<details>
<summary><strong>Orientaciones</strong></summary>

El nivel, el objetivo, la modalidad y el ejemplo siguen siendo relevantes; la duración pasa a 60 minutos. Si se permite continuar el proyecto otro día, conviene conservar las decisiones vigentes y el último plan aprobado, con alcance limitado a esta sesión. Las versiones descartadas pueden permanecer en un historial consultable, pero no tienen por qué incluirse completas en cada petición.

</details>

<!-- IMAGEN OPCIONAL: línea de tiempo de cuatro turnos con el cambio 90 min → 60 min destacado. Guardar en docs/assets/images/tema3-ejemplo-planificacion.png y enlazar aquí si se crea. -->

**Idea central:** una conversación coherente necesita conservar decisiones vigentes y aplicar correcciones; guardar todos los mensajes no resuelve por sí solo ese problema.

[Volver al Tema 3](../tema3-contexto-y-memoria.md)
