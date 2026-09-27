# Actividad 5. Integración y plan de evaluación

**Dedicación estimada: 6 horas.** Actividad aplicada de los [Temas 7](../teoria/tema7-arquitectura-e-integracion.md) y [8](../teoria/tema8-calidad-y-evaluacion.md). Sus horas son independientes de las **18 horas del [proyecto final](../../proyecto-final.md)**.

Esta actividad ensaya, en una escala controlada, la unión de componentes estudiados a lo largo de la microcredencial. No exige terminar el proyecto final: aquí se construye **un recorrido mínimo**, se prueban casos que pueden revelar fallos y se redacta un plan de mejora. El mismo caso y los resultados obtenidos podrán aprovecharse más tarde, sin contar dos veces el trabajo realizado.

## Resultado esperado

Un esquema de arquitectura, un recorrido ejecutado con **al menos dos componentes funcionales** —por ejemplo, interacción y fuentes, o contexto y workflow— y **seis pruebas documentadas**. Se debe ejecutar realmente la parte generativa en una herramienta de IA. Las herramientas externas con efectos sobre terceros se representarán mediante salidas simuladas, identificadas como tales.

## 1. Delimitar un recorrido y la necesidad — 35 minutos

Elige un caso de los bloques previos o formula uno nuevo que pueda probarse con información pública o ficticia. Escribe en cuatro frases: persona destinataria, necesidad, entrada, salida y límite más importante. Delimita **una sola tarea principal**. Si pretendes responder dudas sobre documentos, no añadas además publicación automática de avisos a menos que sea indispensable para ese recorrido.

<details>
<summary><strong>Dos recorridos admisibles</strong></summary>

**Consulta documental:** pregunta → identificación del ámbito → recuperación de un pasaje vigente → generación de respuesta con fuente → comprobación.<br>
**Preparación de un borrador:** ficha → comprobación de campos → generación de borrador → aprobación humana simulada → versión lista para publicar, sin envío real.

En ambos casos se integran varias funciones. El diseño de un prompt aislado no bastaría para cumplir la actividad.

</details>

## 2. Describir arquitectura, datos y responsables — 50 minutos

Elabora una tabla o diagrama con **componentes, entradas, salidas y quién decide**. Indica qué información es instrucción de la aplicación, cuál procede de la persona usuaria y cuál es una fuente externa. Señala si el estado de la tarea debe conservarse entre turnos y qué datos no deberían guardarse.

| Componente | Entrada | Salida | Control o responsable |
|---|---|---|---|
| Interfaz o conversación | Petición | Consulta identificada | Persona usuaria puede aclararla. |
| Fuente o estado | Documento, decisión vigente | Contexto pertinente | Versión y acceso comprobados. |
| Modelo | Tarea + contexto | Borrador o respuesta | Se revisa su fidelidad. |
| Herramienta, si existe | Propuesta de operación | Resultado confirmado o error | Aplicación valida permisos. |
| Revisión | Salida + evidencia | Aprobar, corregir o detener | Persona responsable. |

No todos estos componentes tienen que implementarse mediante software independiente. Una selección manual de fragmentos es válida si se registra qué se seleccionó y de qué versión. Si una función no es necesaria, exclúyela expresamente y explica por qué.

<!-- IMAGEN OPCIONAL: diagrama propio del recorrido elegido con flechas etiquetadas «petición», «pasaje», «respuesta» y «revisión». Guardar en docs/assets/images/actividad5-arquitectura.png y enlazar aquí. -->

## 3. Ejecutar el recorrido mínimo — 85 minutos

Prepara un caso ordinario y recórrelo de principio a fin. Ejecuta el paso del modelo en una herramienta real y registra la instrucción y la salida. Añade por lo menos otra función del sistema: **selección de fuente con identificador**, **estado corregible entre turnos** o **bifurcación de un workflow**. Muestra qué información recibió cada componente y qué salió de él.

Si el caso exige una herramienta que escribiría en otro servicio, usa una **respuesta simulada** de esa herramienta, claramente etiquetada. No conectes el prototipo a cuentas ajenas ni realices envíos para demostrar el diseño. Si tomas como punto de partida una actividad anterior, modifica o integra una función que antes no se había probado en conjunto; no basta con volver a presentar una captura antigua.

<details>
<summary><strong>Registro mínimo del recorrido</strong></summary>

```text
Versión del prototipo y fecha de prueba:
Entrada de la persona usuaria:
Instrucciones de la aplicación:
Fuente o estado disponible (con procedencia):
Pasaje/decisión seleccionado:
Respuesta observada del modelo:
Resultado de herramienta externa: real / simulado / no utilizado
Revisión humana y resultado final:
```

Si algún dato no está disponible, consígnalo. Una respuesta esperada escrita por quien realiza la actividad no debe presentarse como salida observada de un modelo.

</details>

## 4. Diseñar seis pruebas antes de ejecutarlas — 75 minutos

Redacta el resultado esperado y la evidencia necesaria para estos seis casos, adaptados a tu sistema:

| Caso | Qué pone a prueba |
|---|---|
| 1. Ordinario | Resuelve la tarea con datos completos. |
| 2. Reformulado | Mantiene el resultado ante otra manera de preguntar. |
| 3. Dato ausente | Reconoce falta de información o pide aclaración. |
| 4. Versión o decisión corregida | Usa el dato vigente y deja de utilizar el sustituido. |
| 5. Fuera de alcance o instrucción insertada en una fuente ficticia | No adopta órdenes procedentes de datos no autorizados. |
| 6. Fallo de herramienta o fuente | Informa de estado incierto y no finge éxito. |

Ejecuta los casos que permitan las funciones del prototipo. Si una herramienta real no está conectada, **simula su resultado o error** y prueba cómo continúa el sistema; señala qué parte no se ha verificado en una integración real. Registra pregunta, contexto, respuesta observada, resultado esperado y juicio. Una tabla de seis filas basta si conserva lo necesario para reproducir la prueba.

<details>
<summary><strong>Escala sencilla para revisar cada caso</strong></summary>

**Cumple:** comportamiento observado coincide con lo esperado y hay evidencia. **Cumple parcialmente:** conserva la idea principal, pero falla un dato, una cita o una aclaración. **No cumple:** contradice el resultado esperado, inventa un dato esencial, ejecuta una acción improcedente o finge confirmación. Añade una frase diagnóstica; la etiqueta por sí sola no explica el fallo.

</details>

## 5. Diagnosticar y repetir un caso — 65 minutos

Selecciona **el fallo de mayor impacto** o, si los seis casos se superan, una limitación que no hayas podido comprobar. Sitúalo en el componente responsable: entrada, fuente, recuperación, estado, generación, permiso, herramienta o presentación. Cambia **una decisión** de diseño y repite el caso afectado; registra antes y después. Si el problema no puede repararse en esta actividad, redacta el cambio necesario para el proyecto final.

Separa **hechos observados** de hipótesis. «La respuesta citó una versión archivada» es una observación; «la búsqueda no filtró por versión» es una explicación probable que debe confirmarse inspeccionando el pasaje recuperado.

### Plan breve de evaluación posterior

Indica qué otras preguntas o perfiles deberían probarse antes de un uso real, quién revisaría las salidas y qué resultado impediría poner el sistema en funcionamiento. No es necesario diseñar una evaluación estadística extensa con seis casos; sí comunicar con precisión las conclusiones limitadas del ensayo.

## 6. Preparar la evidencia — 50 minutos

Organiza un documento breve o equivalente con:

1. Caso y arquitectura: componentes, flujo y exclusiones justificadas.
2. Registro del recorrido ejecutado y salida real del modelo.
3. Seis pruebas con esperado, observado y diagnóstico.
4. Un cambio de diseño, repetición de la prueba y límite pendiente.
5. Plan para ampliar la evaluación y posible relación con el proyecto final.

Adjunta fragmentos de fuentes ficticias y capturas o transcripción cuando sean necesarios para comprobar las afirmaciones. **La entrega y los criterios oficiales de calificación se indicarán en el Campus Virtual**; esta página establece el trabajo práctico, sin asignar porcentajes.

### Comprobación final

- ¿Se han integrado al menos dos funciones, además de redactar un prompt?
- ¿Se puede seguir la procedencia de datos y decisiones relevantes?
- ¿Se distinguen salidas reales, simuladas y esperadas?
- ¿El fallo de mayor impacto tiene un diagnóstico y una acción posterior?

**Continuación:** el [proyecto final](../../proyecto-final.md) desarrollará y evaluará el caso elegido con más profundidad, a partir de estas observaciones.

[Volver a la presentación del bloque](../index.md)
