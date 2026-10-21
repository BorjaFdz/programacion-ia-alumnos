# Predecir el abandono de una plataforma de formación

La plataforma ficticia **Aula Continua** ofrece microcursos mediante tres planes mensuales. La empresa quiere anticipar bajas para entender mejor a sus clientes.

Tu tarea es construir un clasificador que, **con la información disponible al cierre del 30 de septiembre de 2026**, estime si un cliente activo causará baja entre el 1 y el 31 de octubre. `abandona` es la variable objetivo y sus etiquetas son `si` y `no`.

El fichero integra varios sistemas de la empresa y contiene problemas que debes diagnosticar. También incluye información que no necesariamente resulta adecuada para ese momento de predicción. Todos los datos son sintéticos.

## Reglas del negocio

- Una observación válida corresponde a un cliente activo al corte. `id_cliente` identifica a esa persona, no una medición o una transacción.
- Todos los planes se pagan por meses. Las tarifas base son: **esencial, 19 €; avanzado, 39 €; premium, 69 €**.
- `descuento_pct` es un porcentaje entre 0 y 30. La cuota registrada es el importe mensual final, aplicando exclusivamente ese descuento a la tarifa base. No hay impuestos ni recargos adicionales en este caso.
- La actividad reciente abarca **del 1 al 30 de septiembre**, ambos incluidos. La ventana anterior abarca **del 2 al 31 de agosto**: son dos ventanas consecutivas de 30 días.
- Un acceso es una sesión autenticada. Varias sesiones pueden producirse el mismo día. Los días activos nunca pueden superar los accesos ni los 30 días de la ventana.
- Si no hay accesos recientes, no hay días activos ni horas de uso recientes y el último acceso ocurrió hace al menos 30 días. Un cero puede ser un dato válido.
- Los cursos que se cuentan como completados son únicamente los iniciados dentro de la misma ventana. Cada uno requiere al menos dos horas de uso. No se incluyen finalizaciones de cursos iniciados antes.
- La valoración del tutor solo se recoge entre clientes Premium que usan la tutoría y responden a la encuesta. Un campo vacío puede significar que no aplica o que no hubo respuesta.
- El nivel de satisfacción tiene el orden `baja`, `media`, `alta`. El plan y la provincia se pueden tratar como variables nominales en esta práctica.
- Las cuentas de baja al cierre de octubre corresponden a clientes cuya baja se hizo efectiva durante ese mes. Al cierre de septiembre todos seguían activos.

Consulta las definiciones completas en [diccionario_variables.md](diccionario_variables.md).