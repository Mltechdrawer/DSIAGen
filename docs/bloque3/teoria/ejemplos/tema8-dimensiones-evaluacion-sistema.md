# Dimensiones de evaluación del sistema

La evaluación de un sistema de IA generativa no debe limitarse únicamente a la calidad de la respuesta producida por el modelo. Es necesario analizar también la información de entrada, las fuentes utilizadas y las acciones que el sistema puede ejecutar.

La siguiente matriz propone tres dimensiones de evaluación —**calidad**, **robustez** y **seguridad**— aplicadas a cuatro componentes del sistema: **entrada**, **fuentes**, **generación** y **acción**.

|  | **Calidad** | **Robustez** | **Seguridad** |
|---|---|---|---|
| **Entrada** | **🔍 Revisión de la entrada**<br>¿La petición contiene información suficiente, clara y bien estructurada? | **◔ Estabilidad ante variaciones**<br>¿El sistema maneja entradas incompletas, ambiguas o inesperadas? | **🛡 Protección de la entrada**<br>¿Detecta datos sensibles, instrucciones maliciosas o intentos de manipulación? |
| **Fuentes** | **📄 Calidad de la información**<br>¿Las fuentes son pertinentes, fiables y actuales? | **🔍 Comprobación de disponibilidad**<br>¿El sistema sigue funcionando si una fuente falla o devuelve información incompleta? | **🛡 Control de acceso**<br>¿Las fuentes están autorizadas y se controla el acceso a datos sensibles? |
| **Generación** | **✓ Validación de la respuesta**<br>¿La respuesta es correcta, coherente y adecuada al contexto? | **◔ Estabilidad de la generación**<br>¿La respuesta se mantiene razonablemente estable ante pequeñas variaciones de la petición? | **🛡 Seguridad de la respuesta**<br>¿Evita generar contenido inseguro, revelar datos o seguir instrucciones no permitidas? |
| **Acción** | **✓ Validación del resultado**<br>¿La acción ejecutada responde correctamente al objetivo? | **◔ Gestión de fallos**<br>¿Se gestionan errores, fallos de herramientas o resultados inesperados? | **🛡 Control de permisos**<br>¿La acción requiere los permisos adecuados y se evita ejecutar operaciones peligrosas? |

### Leyenda de los iconos

- 🔍 **Revisión o comprobación detallada**: indica que debe analizarse la información o el comportamiento del sistema.
- 📄 **Evaluación de documentos o fuentes**: representa la revisión de la calidad, pertinencia y procedencia de la información utilizada.
- ✓ **Validación del resultado**: señala la comprobación de que una respuesta o una acción cumple el objetivo previsto.
- ◔ **Robustez, estabilidad y gestión de variaciones**: representa la capacidad del sistema para mantener un comportamiento adecuado ante cambios, errores o situaciones inesperadas.
- 🛡 **Seguridad, protección y control de permisos**: identifica aspectos relacionados con datos sensibles, accesos, acciones autorizadas y prevención de comportamientos inseguros.

!!! tip "Idea clave"
    Evaluar un sistema de IA generativa implica revisar **todo el sistema**, no solo el modelo. Una respuesta puede ser correcta y, aun así, proceder de una fuente inadecuada, depender de un proceso poco robusto o desencadenar una acción no segura.