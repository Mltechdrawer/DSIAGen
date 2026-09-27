# Ejemplo 1. Un asistente para organizar las prácticas de una asignatura

**Caso ficticio · 15 minutos incluidos en el Tema 7.** Un grupo docente quiere responder preguntas sobre qué material debe prepararse antes de cada práctica y permitir que el alumnado continúe una consulta durante la misma sesión. La página de la asignatura contiene un calendario vigente y las fichas de prácticas. El sistema **no** califica ejercicios ni cambia fechas.

| Componente | Función en este caso |
|---|---|
| Interfaz | Recibe la pregunta e indica que se consultan las fichas vigentes. |
| Estado local de conversación | Mantiene la práctica de la que se habla durante la sesión. |
| Recuperación | Selecciona calendario y ficha de esa práctica, con versión. |
| Modelo | Formula una respuesta comprensible desde los fragmentos. |
| Comprobación | Permite revisar si material y fecha proceden de documentos correctos. |

> **Estudiante:** «¿Qué necesito para la práctica 3?»  
> **Sistema:** recupera el apartado «Preparación» de la ficha 3 y muestra una respuesta con enlace a ese apartado.  
> **Estudiante:** «¿Y cuánto dura?»  
> **Sistema:** utiliza que la conversación se refiere todavía a la práctica 3; comprueba la duración en su ficha antes de responder.

La segunda pregunta requiere **estado**, pero no memoria permanente de la persona. Si se abre después otra asignatura, la referencia «práctica 3» no debe heredarse. Si falta el número de práctica al iniciar una nueva conversación, el sistema debe pedirlo.

<details>
<summary><strong>¿Qué componente añadirías si las fichas se publican cada semana?</strong></summary>

Un mecanismo de actualización y control de versiones de las fuentes. No basta con conservar un índice inicial si las fichas cambian. Debe poder comprobarse qué versión se recuperó y cuándo se sustituyó.

</details>

**Para analizar:** identifica un error que podría proceder de la búsqueda y otro que podría proceder de la gestión del estado. ¿Sería necesaria una herramienta con permiso de escritura? Para las funciones descritas, **no**.

<!-- IMAGEN OPCIONAL: recorrido de dos turnos conectado al estado «práctica 3» y a la ficha vigente; guardar en docs/assets/images/tema7-ejemplo-asignatura.png. -->

[Volver al Tema 7](../tema7-arquitectura-e-integracion.md)
