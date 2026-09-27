# Ejemplo 2. Unas instrucciones de proyecto que cambian de versión

**Caso ficticio · Tiempo estimado: 30 minutos, incluido en las 4 horas del Tema 3.**

Un asistente acompaña a un equipo que prepara informes de un proyecto de investigación. Las instrucciones iniciales indicaban que el informe de avance no debía superar **diez páginas**. Meses después, la coordinación publica una versión nueva que establece **seis páginas**. Una integrante del equipo ya había conversado con el asistente antes del cambio y ahora pregunta: «¿Cuál es la extensión máxima?».

Las instrucciones y los límites del caso son inventados. El interés está en identificar **qué información conserva validez** y qué fuente debe utilizarse.

## Tres fragmentos que no tienen la misma autoridad

| Fragmento disponible | Qué representa | Uso apropiado |
|---|---|---|
| «Antes dijiste que eran diez páginas». | Historial de una respuesta anterior. | Ayuda a reconocer que puede existir un cambio. |
| «Prefiero las respuestas en español». | Preferencia atribuida a la persona, si se guardó con autorización. | Puede orientar el idioma, si sigue siendo pertinente. |
| «Instrucciones vigentes: máximo seis páginas». | Documento actual y autorizado del proyecto. | Fundamenta el límite que debe comunicarse. |

El historial no se convierte en una fuente oficial por ser extenso ni por estar guardado. Una respuesta anterior puede haber sido correcta en su momento o contener un error. Para contestar ahora conviene confirmar **a qué proyecto y a qué versión se refiere la persona**. Si la pregunta se plantea desde el espacio del proyecto actual, se puede usar ese contexto; si trabaja en varios proyectos, habrá que pedir aclaración.

### Una respuesta ilustrativa

> «Para el informe de avance del proyecto actual, la extensión máxima es de **seis páginas**, según el apartado “Formato” de las instrucciones vigentes. El límite de **diez páginas** procedía de una versión anterior. Si te refieres a otro informe, indícamelo para comprobar las instrucciones que le corresponden».

Es una **salida esperada redactada para el ejemplo**. En un sistema real habría que comprobar que se ha seleccionado el documento autorizado, que el apartado contiene ese límite y que se ha identificado el informe correcto.

## Dónde puede confundirse el sistema

Un resumen antiguo podría decir «Máximo diez páginas» sin marcar la versión de las instrucciones. Si se incluye después como memoria permanente, podría desplazar el dato vigente. También puede suceder que dos documentos actuales indiquen límites distintos. El sistema no debe decidir arbitrariamente cuál prevalece: debería informar del conflicto, indicar ambos documentos y derivar la consulta a quien tenga autoridad para resolverlo.

<details>
<summary><strong>¿Ayudaría una ventana de contexto enorme?</strong></summary>

Permitiría incluir más historial y más documentos, pero seguiría siendo necesario distinguir versiones, fechas de vigencia y autoridad de las fuentes. Una ventana más grande aumenta la capacidad de aportar información; no resuelve automáticamente las contradicciones entre ella.

</details>

## Un modo de representar el estado

```text
Consulta actual: extensión máxima del informe.
Proyecto e informe: identificar antes de responder si hay ambigüedad.
Fuente autorizada: instrucciones vigentes, apartado «Formato».
Dato extraído: seis páginas.
Historial: existe una respuesta anterior con diez páginas
que corresponde a una versión sustituida.
```

El estado no tiene que mostrarse necesariamente con este formato a la persona usuaria. Sí debería permitir que quien supervisa el sistema investigue por qué se respondió con un límite determinado. Si cambian las instrucciones, el dato extraído deberá revisarse.

### Para analizar el caso

1. ¿Por qué una respuesta previa no basta para responder a la pregunta actual?
2. ¿Qué harías si no se conoce el informe al que se refiere la persona?
3. ¿Qué tendría que pasar con la memoria si unas instrucciones nuevas modifican otra vez la extensión?

<details>
<summary><strong>Orientaciones</strong></summary>

La respuesta anterior puede referirse a otra versión. Si no se identifica el informe, conviene aclararlo antes de dar una cifra. Si cambian las instrucciones, hay que actualizar la fuente y los datos derivados que dependan de ella; el historial puede conservarse según la finalidad del servicio, pero no debe presentarse como información vigente.

</details>

<!-- IMAGEN OPCIONAL: dos tarjetas «Versión inicial: diez páginas» y «Versión vigente: seis páginas», con una flecha hacia «Verificar versión antes de responder». Guardar en docs/assets/images/tema3-ejemplo-versiones.png y enlazar aquí si se crea. -->

**Idea central:** la continuidad de la conversación debe conservar la procedencia y la vigencia; recordar algo no es lo mismo que poder respaldarlo hoy.

[Volver al Tema 3](../tema3-contexto-y-memoria.md)
