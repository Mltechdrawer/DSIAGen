# Actividad 4. Workflow con IA

**Dedicación estimada: 4 horas.** Actividad aplicada del [Tema 6. Automatización, herramientas y workflows con IA](../teoria/tema6-automatizacion.md). Sus horas se cuentan aparte de las cuatro del tema.

Se diseñará y probará un **workflow pequeño** en el que la IA generativa realice una tarea delimitada y el resto del proceso tenga entradas, decisiones y responsables explícitos. Puede ser un flujo manual guiado por una ficha, una automatización visual sin código o un programa breve. **No se realizarán envíos ni cambios en servicios reales** durante esta actividad: las acciones externas se simularán y se documentará cuándo ocurrirían y quién tendría que autorizarlas.

## Resultado esperado

Un flujo con al menos **cuatro pasos, una bifurcación y un punto de revisión humana**, más pruebas de funcionamiento normal y de fallo. Se utilizará una herramienta de IA para ejecutar realmente al menos el paso de generación o análisis; los demás pasos pueden representarse mediante una tabla de estados y datos ficticios. Diseñar un diagrama sin probar una ejecución no completa la actividad.

## 1. Elegir un proceso acotado — 30 minutos

Selecciona una necesidad de tu entorno o continúa con el caso de la [Actividad 3](actividad3-prototipo-con-conocimiento.md). Escribe una frase que describa el disparador y otra que describa el resultado esperado. Ejemplos posibles:

- Recibir una ficha de novedad, verificar campos, generar un borrador de boletín y enviarlo a revisión.
- Recibir una solicitud de información, localizar un documento vigente, proponer una respuesta y enviarla para aprobación antes de publicarla.
- Recibir un borrador docente, comprobar que incluye los requisitos, generar una versión clara y dejarla pendiente de validación.

Evita un proceso que obligue a conectar herramientas de pago o a compartir documentos privados. Es importante que haya **al menos una acción propuesta que no se ejecute sin confirmación**.

## 2. Dibujar pasos, decisiones y estados — 40 minutos

Prepara una tabla como esta, adaptada a tu caso:

| Paso | Responsable | Entrada | Salida | Si falla |
|---|---|---|---|---|
| Recibir | Persona o formulario simulado | Ficha | Ficha registrada | Solicitar datos faltantes. |
| Verificar | Regla explícita | Ficha | Completa / incompleta | Detener proceso. |
| Redactar | Modelo generativo | Ficha completa | Borrador | Marcar para revisión. |
| Revisar | Persona responsable | Borrador y fuente | Aprobar / corregir | Volver a redactar. |
| Publicar, solo simulado | Servicio externo hipotético | Versión aprobada | Confirmación simulada | Comprobar antes de reintentar. |

Registra el **estado** de cada paso: pendiente, completado, fallido o en espera de aprobación. Elige una bifurcación real, por ejemplo «si falta la fuente, detener», y explica qué información recibe la persona que revisa. No delegues al modelo una comprobación simple que puede formularse mediante una regla verificable si no hay motivo para hacerlo.

<details>
<summary><strong>Plantilla de una operación que modificaría un servicio</strong></summary>

```text
Nombre de la acción hipotética:
Datos que necesitaría:
Quién autorizaría su ejecución:
Comprobaciones previas:
Confirmación que debería devolver el servicio:
Qué haría el sistema si no hubiera confirmación:
```

En esta actividad no hace falta conectar el servicio. La ficha obliga a diferenciar «el modelo propuso actuar» de «una herramienta confirmó la acción».

</details>

## 3. Preparar datos e instrucciones — 55 minutos

Construye **dos entradas ficticias**: una completa y otra con un campo obligatorio ausente o contradictorio. Define el mensaje que utilizarás en el paso de IA: qué debe producir, con qué datos, qué debe conservar y cómo debe señalar incertidumbre. Por ejemplo: «A partir de la ficha autorizada, redacta un boletín de 120 palabras. Conserva exactamente nombres y fechas. No conviertas propuestas en hechos confirmados. Señala al final los datos que faltan».

Especifica qué parte del flujo entrega esa ficha al modelo y quién cotejará la salida con la fuente. Si el proceso usa documentos de la Actividad 3, registra qué versión se recupera y qué pasaje llega al paso de generación. Una salida generada no se convierte automáticamente en una fuente válida para el siguiente paso.

<!-- IMAGEN OPCIONAL: workflow con una bifurcación antes de generar y aprobación antes de publicar; guardar en docs/assets/images/actividad4-workflow.png y enlazar aquí si se crea. -->

## 4. Ejecutar y comprobar dos recorridos — 65 minutos

Realiza un **recorrido normal** con la ficha completa y un **recorrido de fallo** con la ficha incompleta o contradictoria. Ejecuta en una herramienta de IA el paso generativo al menos para el recorrido normal. Para el caso de fallo, comprueba si el flujo lo detecta **antes** de generar; si lo detecta, documenta que el modelo no debería recibir esa entrada y representa el estado «detenido». No lo fuerces a responder solo para disponer de otra salida.

Registra en cada paso entrada, salida observada o **simulada** —etiquetadas de forma diferente—, estado y decisión. Comprueba además una tercera situación: **la revisión humana rechaza el borrador**. El sistema debe regresar al paso adecuado sin publicar nada. Si tu flujo incluye una operación que podría duplicarse (por ejemplo, enviar o guardar), describe cómo comprobarías el resultado antes de reintentarla.

| Escenario | Resultado esperado | Evidencia necesaria |
|---|---|---|
| Entrada completa | Borrador pendiente de revisión. | Ficha, salida real del modelo y estado. |
| Falta dato obligatorio | Flujo detenido o solicitud de aclaración. | Regla que detecta el dato y estado. |
| Borrador rechazado | Vuelve a revisión o redacción. | Decisión de rechazo y ruta seguida. |
| Acción sin confirmación | Estado incierto; no se declara éxito. | Paso que consultaría el estado antes de repetir. |

<details>
<summary><strong>¿Cuenta como prueba una salida inventada para ilustrar el flujo?</strong></summary>

Puede utilizarse como **simulación de una herramienta externa** si se marca claramente. El paso generativo sí debe tener al menos una salida real de una herramienta de IA. Una captura de un diagrama o una respuesta esperada redactada por quien realiza la actividad no sustituye esa prueba.

</details>

## 5. Revisar un fallo y mejorar el flujo — 30 minutos

Identifica un defecto concreto observado o revelado por las simulaciones: falta de una bifurcación, ausencia de confirmación antes de una acción, borrador que inventa una fecha o revisión que no ve la fuente original. Corrige el diagrama o la regla correspondiente y repite el paso afectado si puede ejecutarse. Indica qué cambió y qué límite permanece.

No es necesario convertir el prototipo en un agente autónomo. Si el workflow definido resuelve la necesidad, añadir elecciones de herramienta gobernadas por el modelo podría incrementar la complejidad sin aportar utilidad.

## 6. Preparar la evidencia — 20 minutos

Entrega un documento breve o equivalente que incluya:

1. Necesidad, disparador y resultado esperado.
2. Tabla o diagrama de pasos, responsables, decisiones y estados.
3. Instrucción utilizada y dos entradas ficticias.
4. Registro de los recorridos: salida **real** del paso de IA y resultados **simulados** de herramientas externas, correctamente identificados.
5. Punto de revisión humana, tratamiento del fallo y corrección realizada.

Incluye capturas o transcripción cuando sean necesarias para comprobar el paso generativo. No conectes servicios reales para enviar correos, reservar recursos o modificar registros durante esta actividad. **El formato de entrega y la evaluación oficial se indicarán en el Campus Virtual**; esta página no asigna porcentajes de nota.

### Comprobación final

- ¿Se sabe qué componente ejecuta cada paso?
- ¿Se distingue la propuesta del modelo de una acción confirmada?
- ¿El recorrido de fallo tiene un estado y una salida definidos?
- ¿Puede una persona detener o corregir el flujo antes de una acción externa?

**Relación con el proyecto final:** el flujo probado puede integrarse en el [prototipo aplicado](../../proyecto-final.md) si responde a una necesidad real. El proyecto requerirá revisar de nuevo permisos, fuentes y controles según su alcance.

[Volver a la presentación del bloque](../index.md)
