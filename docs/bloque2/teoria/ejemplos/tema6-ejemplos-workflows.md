# Ejemplos de workflows con IA generativa

Los siguientes ejemplos muestran procesos que pueden construirse con un
asistente de IA y herramientas conectadas. No representan una
implementación concreta ni implican que todas las plataformas dispongan
de las mismas integraciones. Su finalidad es identificar con claridad el
**disparador**, los pasos del proceso, las decisiones, las acciones y
los puntos en los que puede ser necesaria una revisión humana.

## 1. Revisión y organización del correo electrónico

**Disparador:** llegada de nuevos mensajes o revisión programada del
buzón.

**Workflow:** revisar los correos recibidos → identificar remitente y
asunto → clasificarlos según criterios definidos → detectar cuáles
requieren atención → preparar un resumen organizado.

El sistema podría, por ejemplo, separar mensajes informativos,
solicitudes que requieren respuesta y comunicaciones urgentes. La
clasificación no debería implicar automáticamente acciones como
archivar, eliminar o responder, salvo que esas acciones formen parte
explícita del flujo y estén autorizadas.

## 2. Preparación de respuestas a correos

**Disparador:** llegada de un correo que cumple determinados criterios.

**Workflow:** analizar el mensaje → identificar qué solicita →
consultar, si es necesario, información relacionada → preparar una
propuesta de respuesta → solicitar revisión → enviar únicamente si el
flujo contempla esa acción y existe autorización.

Este ejemplo permite distinguir con claridad entre **generar un
borrador** y **enviar un mensaje**. El modelo puede preparar el
contenido, mientras que el envío constituye una acción con efectos
externos que puede requerir confirmación.

## 3. Envío diario de la agenda del día siguiente

**Disparador:** una hora determinada de cada día.

**Workflow:** consultar el calendario del día siguiente → seleccionar
las citas relevantes → ordenarlas cronológicamente → preparar un resumen
→ enviar el correo o dejarlo preparado para revisión.

El flujo puede incorporar información adicional, como la hora, el lugar
o los participantes de cada reunión, siempre que esos datos estén
disponibles y su utilización esté autorizada.

## 4. Revisión de páginas de noticias y elaboración de un resumen

**Disparador:** una periodicidad definida, por ejemplo una vez al día.

**Workflow:** consultar un conjunto de páginas seleccionadas →
identificar contenidos nuevos → filtrar los relacionados con los temas
de interés → resumirlos → incluir las fuentes → preparar o enviar un
correo con el resumen.

Este workflow combina recuperación de información, selección, generación
y una posible acción final. También permite comprobar qué ocurre cuando
una página no está disponible, no contiene novedades o presenta
información duplicada.

## 5. Preparación de una reunión

**Disparador:** proximidad de una reunión incluida en el calendario.

**Workflow:** consultar los datos de la reunión → recuperar
documentación relacionada → identificar asuntos pendientes → preparar un
resumen previo → presentarlo a la persona usuaria.

El objetivo no es tomar decisiones en nombre de las personas
participantes, sino reunir la información que puede resultar útil para
preparar la reunión.

## 6. Seguimiento posterior a una reunión

**Disparador:** finalización de una reunión o incorporación de sus notas
o transcripción.

**Workflow:** analizar la información disponible → identificar acuerdos
→ extraer tareas y responsables cuando consten explícitamente → detectar
asuntos pendientes → preparar un resumen → generar un borrador de correo
de seguimiento.

Este caso permite comprobar cómo una salida generada puede convertirse
en entrada de otro paso y por qué conviene mantener la referencia a la
información original.

## 7. Seguimiento de convocatorias o ayudas

**Disparador:** revisión periódica de un conjunto de fuentes.

**Workflow:** consultar las fuentes seleccionadas → detectar
convocatorias nuevas o modificadas → comprobar criterios definidos →
seleccionar las potencialmente relevantes → preparar un resumen con
enlaces y fechas importantes → notificar a la persona usuaria.

La detección de una convocatoria no implica que una persona cumpla
automáticamente sus requisitos. El workflow puede localizar candidatos,
pero la comprobación de elegibilidad puede requerir pasos adicionales.

## 8. Vigilancia bibliográfica

**Disparador:** ejecución periódica de una búsqueda.

**Workflow:** consultar fuentes bibliográficas → localizar publicaciones
nuevas sobre un tema → eliminar resultados duplicados → seleccionar los
que cumplen los criterios establecidos → preparar un resumen con sus
referencias → generar un informe periódico.

Este ejemplo resulta útil para distinguir entre **localizar
información** y **valorarla**. Una publicación recuperada por coincidir
con los criterios de búsqueda no tiene por qué ser necesariamente
relevante para el objetivo final.

## 9. Resumen periódico de actividad

**Disparador:** final de una semana o de otro periodo establecido.

**Workflow:** recopilar información de las fuentes autorizadas →
identificar novedades, tareas realizadas y asuntos pendientes →
organizar la información → generar un informe → solicitar revisión antes
de distribuirlo.

Puede utilizarse, por ejemplo, para preparar un resumen interno de un
proyecto sin obligar a una persona a recopilar manualmente información
dispersa.

## 10. Seguimiento de cambios en páginas web

**Disparador:** comprobación periódica de páginas previamente
seleccionadas.

**Workflow:** consultar las páginas → comparar su contenido con la
revisión anterior → detectar cambios → valorar cuáles son relevantes
según los criterios establecidos → resumirlos → notificar únicamente
cuando exista una modificación de interés.

Este workflow muestra que un proceso automatizado no tiene por qué
producir siempre una salida para la persona usuaria: si no se detecta
ningún cambio relevante, puede finalizar sin enviar una notificación.

------------------------------------------------------------------------

Estos ejemplos pueden representarse utilizando la misma estructura
estudiada en el tema:

**disparador → entradas → pasos y decisiones → herramientas →
supervisión → salida y registro**

Al diseñar cualquiera de ellos conviene preguntar qué pasos puede
realizar automáticamente el sistema, cuáles requieren una comprobación y
qué debe ocurrir cuando una fuente, una herramienta o una acción no
produce el resultado esperado.
