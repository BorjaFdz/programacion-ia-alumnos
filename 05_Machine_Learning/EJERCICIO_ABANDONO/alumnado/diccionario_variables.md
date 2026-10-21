# Diccionario de variables

Una fila válida representa un cliente activo al cierre del **30 de septiembre de 2026**. El objetivo es predecir si causará baja efectiva durante octubre. Los vacíos del CSV se leen como valores ausentes; nunca implican automáticamente cero.

Las columnas de actividad de 30 días se refieren al 1–30 de septiembre. La ventana previa es el 2–31 de agosto.

| Columna | Tipo conceptual y unidad | Significado y reglas | Cuándo se conoce |
|---|---|---|---|
| `id_cliente` | Texto identificador | Código sintético de cliente. La misma persona conserva el ID en todas sus apariciones. No es una característica de comportamiento. | Al corte |
| `edad` | Entero, años cumplidos | Edad del titular. La plataforma trabaja con titulares adultos. | Al corte |
| `provincia` | Categórica nominal | `Madrid`, `Barcelona`, `Valencia`, `Sevilla`, `Bizkaia`, `A_Coruna`, `Zaragoza`, `Malaga` u `otra`. | Al corte |
| `situacion_laboral` | Categórica nominal | `estudiante`, `empleado`, `autonomo`, `desempleado` o `jubilado`. Situación principal declarada. | Al corte |
| `canal_captacion` | Categórica nominal | `busqueda`, `redes_sociales`, `recomendacion` o `email`. Canal original de alta. | Desde el alta |
| `plan` | Categórica nominal | `esencial`, `avanzado` o `premium`. Todos tienen facturación mensual. Premium incluye tutoría opcional. | Al corte |
| `descuento_pct` | Numérica, puntos porcentuales | Descuento vigente: 0, 10, 20 o 30. El valor 20 significa un 20 %, no 0,20 %. | Al corte |
| `cuota_mensual_eur` | Numérica, euros/mes | Importe final mensual. Tarifa del plan × `(1 − descuento_pct / 100)`, redondeado a céntimos. | Al corte |
| `antiguedad_meses` | Entero, meses completos | Antigüedad de la suscripción actual. Todos los clientes llevan al menos dos meses de alta y disponen de ambas ventanas de seguimiento. | Al corte |
| `accesos_30d_previos` | Entero, sesiones | Sesiones autenticadas en la ventana anterior de 30 días. Puede ser cero. | Antes del corte |
| `accesos_30d` | Entero, sesiones | Sesiones autenticadas en los últimos 30 días. Puede haber varias en un mismo día. | Al corte |
| `dias_activos_30d` | Entero, días | Días distintos con al menos una sesión. Entre 0 y 30 y no superior a los accesos. | Al corte |
| `horas_uso_30d` | Numérica, horas | Tiempo acumulado de aprendizaje autenticado en la ventana. Se redondea a dos decimales. Sin accesos, es cero. | Al corte |
| `dias_desde_ultimo_acceso` | Entero, días | Diferencia entre el 30 de septiembre y el día del último acceso. Cero significa acceso el propio día 30. Si no hay accesos recientes, es al menos 30. | Al corte |
| `cursos_iniciados_30d` | Entero, cursos | Microcursos distintos iniciados en los últimos 30 días. En este caso no se inicia más de uno por acceso. | Al corte |
| `cursos_completados_30d` | Entero, cursos | Subconjunto de los cursos anteriores que también se completaron dentro de la ventana. No incluye cursos empezados antes. Cada uno requiere al menos dos horas. | Al corte |
| `incidencias_soporte_30d` | Entero, incidencias | Número de incidencias abiertas en soporte durante la ventana. Incluye consultas sobre funcionamiento y cuenta. | Al corte |
| `satisfaccion` | Categórica ordinal | Respuesta de la encuesta de septiembre: `baja < media < alta`. Ausente si la respuesta no se incorporó al fichero. | Al corte |
| `valoracion_tutor` | Numérica, puntos de 0 a 10 | Valoración de tutoría dada por usuarios Premium que utilizaron el servicio y respondieron. Para otros clientes puede no aplicar; también puede faltar por no respuesta. | Al corte, si existe |
| `telefono_secundario` | Texto opcional | Campo de contacto adicional del CRM. La disponibilidad depende de la integración y de la información proporcionada por el cliente. | Al corte, si existe |
| `estado_cuenta_31_octubre` | Categórica nominal | Estado al cierre del 31 de octubre: `activa` o `baja`. No se incluyen suspensiones ni cierres administrativos ajenos al abandono en este caso. | Al cierre de octubre |
| `abandona` | Categórica binaria, objetivo | `si` si la baja se hizo efectiva entre el 1 y el 31 de octubre; `no` en caso contrario. | Al cerrar el periodo objetivo |

La presencia de una columna en una exportación histórica no garantiza que esté disponible al realizar una predicción. Los rangos y relaciones anteriores describen el negocio; el fichero recibido puede incumplirlos por errores de integración.
