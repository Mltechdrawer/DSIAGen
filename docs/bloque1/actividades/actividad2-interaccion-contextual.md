# Actividad 2. Construcción de una interacción contextual

**Dedicación estimada: 4 horas.** Trabajo aplicado del Bloque I, posterior al [Tema 3. Contexto, memoria y conversaciones](../teoria/tema3-contexto-y-memoria.md). Sus cuatro horas son independientes de las de los temas y de la [Actividad 1](actividad1-prompts.md).

En la actividad anterior se compararon instrucciones para una tarea. Ahora se construirá una **interacción de varios turnos**: el sistema debe utilizar decisiones anteriores, actualizar una corrección y reconocer cuándo un dato guardado deja de ser válido. Se puede continuar con el mismo caso, pero no se volverá a realizar la comparación de prompts de la Actividad 1.

## Resultado esperado

Un prototipo sencillo **probado mediante una conversación real con una herramienta de IA generativa**, que muestre **qué contexto recibe el modelo en cada turno**, cómo se mantiene el estado de la tarea y qué sucede cuando aparecen cambios, ambigüedades o datos antiguos. Se acompañará de una breve revisión de su funcionamiento.

**Formas de realización equivalentes:** puedes utilizar un asistente conversacional y preparar manualmente el contexto de cada turno; configurar una herramienta sin código que permita mantener instrucciones y datos; o programar un prototipo pequeño si lo prefieres. Todas las vías deben mostrar las **mismas decisiones y evidencias**. No se requiere suscripción de pago ni acceso a una API. Si una función de memoria de la herramienta no es visible o configurable, no supongas que conserva información: construye y documenta explícitamente el estado que le facilitas.

## 1. Recuperar el caso y fijar el alcance — 25 minutos

Utiliza el caso de la Actividad 1 o define otro de escala similar: apoyo a la elaboración de un documento, consulta de instrucciones aportadas por la persona usuaria, preparación de una sesión o seguimiento de un pequeño proyecto. La interacción debe poder probarse con **datos ficticios** y sin enviar datos personales o material confidencial a servicios externos.

Redacta un objetivo en una frase y señala quién participa, qué puede hacer el sistema y qué no puede decidir por sí mismo. Si reutilizas el prompt final de la Actividad 1, cópialo como punto de partida; no se presupone que una formulación adecuada para una sola respuesta baste para gestionar una conversación.

<details>
<summary><strong>Ejemplo de alcance manejable</strong></summary>

«Ayudar a una docente a planificar una sesión mediante propuestas sucesivas. La docente fija nivel, duración y objetivo; el sistema adapta el plan cuando cambian esas condiciones. No decide el currículo ni accede a información de estudiantes».

La alternativa profesional puede ser un informe, una campaña de comunicación o un proceso documental; importa que exista una **decisión que se mantenga entre turnos** y otra que se corrija después.

</details>

## 2. Diseñar el mapa del contexto — 40 minutos

Antes de iniciar la conversación, prepara una ficha que distinga las siguientes piezas:

| Pieza | Qué anotar en tu caso | Ejemplo |
|---|---|---|
| Instrucciones estables | Función y límites de la interacción. | «Propón planes; pide datos esenciales; no inventes fechas». |
| Solicitud actual | Qué pide la persona en este turno. | «Reduce la sesión a una hora». |
| Estado de la tarea | Decisiones vigentes y su procedencia. | «Duración vigente: 60 min, fijada en turno 3». |
| Historial necesario | Qué parte de los mensajes anteriores afecta a la respuesta. | Última versión del plan. |
| Fuente externa, si se utiliza | Documento y versión que se consultan. | «Programa v2, apartado de objetivos». |
| Datos que se excluyen | Qué no se necesita o no se debe reutilizar. | Borradores descartados y datos personales. |

Define una regla sencilla para el cambio: **una corrección explícita sustituye al valor anterior** en el estado vigente; el historial puede conservar que hubo un cambio, pero no presentar ambos valores como simultáneamente válidos. Define también cuándo pedir una aclaración y cuándo reconocer que falta una fuente. No almacenes una preferencia local como si fuera una propiedad permanente de la persona.

<!-- IMAGEN OPCIONAL: dos zonas «Estado vigente» e «Historial consultable», conectadas al turno actual. Si se crea, guardar en docs/assets/images/actividad2-mapa-contexto.png y enlazar aquí. -->

## 3. Construir cuatro turnos encadenados — 50 minutos

Escribe y ejecuta una conversación de **al menos cuatro turnos de la persona usuaria**:

1. **Inicio:** establece dos o tres condiciones necesarias para la tarea.
2. **Continuidad:** se refiere a algo decidido o generado antes, sin repetir toda la información.
3. **Corrección:** cambia una condición importante; el sistema debe actualizar el estado.
4. **Incertidumbre o conflicto:** falta un dato, aparece una fuente de otra versión o se pide algo fuera del alcance.

Después de cada turno registra **entrada**, **contexto aportado**, **salida observada** y **estado resultante**. Además de las salidas reales, puedes anotar la respuesta esperada para compararla, distinguiendo ambas. Al menos un turno debe requerir decidir qué **no** incorporar al contexto.

<details>
<summary><strong>Plantilla breve para registrar cada turno</strong></summary>

```text
Turno n.º:
Petición de la persona usuaria:
Información previa incluida y procedencia:
Información previa excluida y motivo:
Estado antes del turno:
Respuesta observada / respuesta esperada (indicar cuál):
Estado después del turno:
Punto que debería verificarse:
```

Es suficiente registrar lo relevante para explicar la decisión. No es necesario copiar todo el historial si se facilita un enlace o anexo que permita consultarlo.

</details>

## 4. Probar la continuidad y detectar fallos — 65 minutos

Somete el prototipo a **cuatro comprobaciones**. Utiliza el mismo objetivo del caso, pero varía el contexto para que la prueba revele si el sistema respeta el estado.

| Prueba | Pregunta que debe poder responderse al revisar el resultado |
|---|---|
| **Recuerdo relevante** | ¿Usa una condición anterior que sigue vigente? |
| **Corrección** | ¿Aplica el valor nuevo y deja de utilizar el sustituido? |
| **Dato ausente o ambiguo** | ¿Pregunta o señala el supuesto cuando afecta a la respuesta? |
| **Versión o alcance** | ¿Detecta una fuente obsoleta o una solicitud que excede su función? |

Para cada prueba anota **esperado / observado / juicio / cambio propuesto**. Indica el fragmento preciso que respalda el juicio. Por ejemplo, «menciona 90 minutos tras la corrección a 60» identifica un fallo; «no mantiene el contexto» es demasiado general. Si la herramienta produce salidas variables, consérvalas y explica la variación.

En la vía sin código, puedes hacer el experimento de forma manual: antes de cada respuesta, proporciona una ficha de estado actualizada y el último fragmento útil del historial. En la vía programada, el programa puede construir esa ficha. En ambos casos, la pregunta central es **qué información llegó a la petición actual**, no la sofisticación de la plataforma.

<details>
<summary><strong>Si una conversación parece recordar todo sin que aportes contexto</strong></summary>

No atribuyas automáticamente el comportamiento a una memoria persistente. Puede tratarse del historial de la conversación actual, de un estado gestionado por la plataforma o de una coincidencia plausible. Para analizarlo, abre una conversación nueva si la herramienta lo permite, repite una petición dependiente del turno anterior y documenta la diferencia. Respeta siempre las condiciones de uso y privacidad del servicio.

</details>

## 5. Revisar el diseño y explicitar sus límites — 40 minutos

Elige el fallo más importante y realiza **una corrección del diseño**: actualizar un campo de estado, indicar la versión de una fuente, descartar información sustituida, pedir una aclaración antes de responder o cambiar cómo se resume la conversación. Repite la prueba afectada y registra si el resultado mejora. Si no mejora, explica qué componente adicional sería necesario; no atribuyas todos los problemas al prompt.

Define también cómo se terminaría la interacción: ¿qué información de esta tarea tendría sentido conservar para continuar mañana?, ¿cuál no debería utilizarse en otros proyectos?, ¿cómo corregiría la persona un dato almacenado? No se exige implantar una base de datos de memoria; sí **justificar las reglas de conservación y actualización** que necesitaría el sistema.

## 6. Preparar la evidencia de la actividad — 20 minutos

Organiza un documento o equivalente con:

1. Caso, alcance y modalidad de realización (herramienta, configuración sin código, pequeño programa o simulación).
2. Mapa del contexto y regla de actualización del estado.
3. Cuatro turnos con contexto aportado, respuesta **observada**, y estado resultante.
4. Cuatro pruebas con los resultados y una corrección repetida.
5. Límites: datos que no se conservarían, fuente que se comprobaría y trabajo pendiente para un sistema real.

Añade el registro de conversación o capturas legibles, evitando datos privados. Si una limitación técnica impide completar una prueba, identifica la prueba afectada y describe qué ocurrió; no inventes salidas para suplirla. **La modalidad de entrega y los criterios oficiales de calificación se publicarán en el Campus Virtual**; esta página no establece una ponderación de nota.

### Comprobación antes de terminar

- ¿Se distinguen las instrucciones, la petición actual, el estado y las fuentes?
- ¿Se sabe qué valor vigente sustituyó a cuál?
- ¿Hay al menos un caso en que el sistema pregunta, reconoce un límite o detecta una versión incorrecta?
- ¿Se diferencia claramente una salida observada de una respuesta redactada como ejemplo?
- ¿Puede otra persona repetir las cuatro comprobaciones con los datos proporcionados?

**Relación con el proyecto final:** la ficha de estado y las pruebas pueden informar el diseño posterior del [prototipo aplicado](../../proyecto-final.md). No se presupone que el proyecto necesite memoria persistente: depende del caso.

### Material de apoyo

- [Tema 3. Contexto, memoria y conversaciones](../teoria/tema3-contexto-y-memoria.md).
- [Ingeniería de Contexto](https://mltechdrawer.github.io/ChatGPT/3_IC/), material docente introductorio.
- [OpenAI: gestión del estado de conversación](https://developers.openai.com/api/docs/guides/conversation-state), ejemplo técnico de distintas formas de conservar contexto.

[Volver a la presentación del bloque](../index.md)
