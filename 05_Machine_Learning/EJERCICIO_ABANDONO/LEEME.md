# Dataset de clasificación: abandono de una plataforma de formación

Caso sintético para trabajar limpieza, imputación, codificación, escalado, fuga de información y evaluación de un clasificador en una misma práctica.

**3.000 clientes únicos, 3.102 filas en el CSV y 22 columnas.** La variable objetivo es `abandona`, con valores `si` y `no`. En la referencia, el 25,73 % causa baja durante octubre.

## El caso

Una plataforma de microcursos quiere identificar, al cierre del 30 de septiembre de 2026, qué clientes activos causarán baja durante octubre. Todas las suscripciones son mensuales. El fichero que entrega la empresa reúne información de actividad, perfil, facturación y cierre de cuentas. Es necesario decidir qué información habría estado disponible al hacer la predicción.

Los registros y los errores son ficticios. El generador establece relaciones entre características antes de sortear el abandono. La etiqueta tiene ruido y no queda determinada por una sola característica disponible en septiembre.

## Qué entregar al alumnado

Distribuye únicamente la carpeta [alumnado](alumnado/), con:

- [clientes_formacion.csv](alumnado/clientes_formacion.csv): dataset que se debe analizar.
- [LEEME.md](alumnado/LEEME.md): contexto, reglas del negocio y recorrido de la práctica.
- [diccionario_variables.md](alumnado/diccionario_variables.md): significado, unidades y disponibilidad de las 22 columnas.
- [practica.ipynb](alumnado/practica.ipynb): cuaderno de inicio con la carga de datos y apartados por completar.

## Material para el docente

La carpeta [docente](docente/) contiene la referencia sin errores de exportación, el registro de cada alteración, el mapa de filas, la guía de decisiones, el generador reproducible y su verificador. La referencia conserva las ausencias que tienen sentido en el negocio y la columna posterior que permite estudiar la fuga: no es directamente una matriz lista para entrenar.

Consulta [guia_docente.md](docente/guia_docente.md) para los recuentos, las soluciones conceptuales, las comprobaciones de coherencia y el resultado de control.

## Formato

CSV con separador coma, punto decimal, UTF-8 sin BOM, sin índice y campos vacíos para los ausentes. Las filas completamente vacías conservan los delimitadores: `pandas.read_csv` las carga y permite detectarlas.

```python
import pandas as pd
df = pd.read_csv("alumnado/clientes_formacion.csv")
```
