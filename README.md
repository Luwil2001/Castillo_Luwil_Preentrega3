# Compras previas por categoría: análisis descriptivo para retail

**Portfolio de datos · Luwil Castillo · Data Analyst en formación**

## Resumen del proyecto

¿Las categorías de retail presentan diferencias en el historial de compras previas de sus clientes? Con datos públicos de Kaggle comparé la mediana y el promedio de `PreviousPurchases` para nueve categorías. La mediana fue 5 en todas; los promedios variaron entre 4,875 y 5,238. La evidencia no permite afirmar que una categoría tenga menor recompra: el dataset tiene un registro por cliente y no incluye fechas de transacción. La recomendación es validar el patrón con datos transaccionales fechados antes de decidir acciones comerciales.

## Problema de negocio

El equipo comercial busca identificar si hay categorías con menor recurrencia para orientar futuras acciones de retención. Esta primera rebanada responde una pregunta más acotada: **¿cómo se distribuye el historial de compras previas por categoría?**

`PreviousPurchases` es un conteo histórico disponible en el archivo; no equivale a una tasa de recompra observada en el tiempo. La fuente no incluye fechas y cada `CustomerID` aparece una sola vez, por lo que no permite reconstruir secuencias de compras por cliente.

## Stack tecnológico

- **Python 3:** ejecución del análisis.
- **pandas:** validaciones, limpieza mínima y agregación.
- **Pillow:** generación del gráfico estático.

## Fuente y calidad de datos

- **Origen:** [Kaggle — Store Sales](https://www.kaggle.com/datasets/hassanjameelahmed/store-sales/data).
- **Archivo:** `store_sales.csv`, descargado desde la página del dataset.
- **Tamaño analizado:** 5.000 filas, 11 columnas y 9 categorías.
- **Criterio de fila válida:** categoría informada y `PreviousPurchases` numérico dentro del rango 0–13.
- **Controles:** 0 nulos en los dos campos de análisis, 0 duplicados exactos, 5.000 filas válidas y 0 filas excluidas.
- Se detectaron 6 descuentos por encima del máximo de 32% indicado en la ficha. Se reportan como control, pero no se usan para filtrar ni calcular esta rebanada.

## Metodología

El trabajo sigue CRISP-DM de manera incremental: se tradujo la necesidad comercial a una métrica observable, se inspeccionaron los datos, se aplicaron reglas mínimas de validez, se calcularon resúmenes por categoría y se interpretaron los límites de la evidencia. El backlog se planificó en tres sprints de dos semanas. El plan prevé revisar cada incremento anterior antes de ampliar el análisis, incluyendo la métrica, las reglas de calidad y la interpretación del resultado.

## Hallazgos y lectura

- La mediana de compras previas es **5 en las nueve categorías**; no distingue una categoría con menor historial.
- Los promedios van de **4,875 en Mens Clothing a 5,238 en Home**, una diferencia descriptiva de 0,363 compras previas.
- Las categorías tienen tamaños de muestra distintos (de 286 a 983 registros), por lo que la comparación es exploratoria.
- Estos datos no prueban causalidad, no miden recompra temporal y no justifican por sí solos segmentar promociones.

### Evidencia visual

La mediana empata entre todas las categorías; el segundo gráfico muestra los promedios y el tamaño de cada grupo.

![Medianas de compras previas por categoría](presentacion/03_medianas_por_categoria.png)

![Promedios y cobertura por categoría](presentacion/04_promedios_y_cobertura.png)

- [Tabla de resumen (CSV)](results/recurrencia_por_categoria.csv)
- [Controles de calidad (CSV)](results/control_calidad.csv)
- [Presentación ejecutiva completa](presentacion/README.md)

## Recomendación de negocio

Antes de orientar una campaña hacia una categoría, validar la hipótesis con una tabla transaccional que incluya identificador de cliente, categoría y fecha de compra, con varias transacciones por cliente. Así se podrá definir y calcular una métrica temporal de recompra. El análisis actual no permite escoger una categoría objetivo.

## Código y reproducción

El script central está en [src/analisis_recurrencia.py](src/analisis_recurrencia.py).

1. Cloná o descargá este repositorio.
2. Descargá `store_sales.csv` desde Kaggle y guardalo en `data/store_sales.csv`.
3. Instalá las dependencias:
   ```bash
   python -m pip install -r requirements.txt
   ```
4. Ejecutá desde la carpeta del repositorio:
   ```bash
   python src/analisis_recurrencia.py --input data/store_sales.csv --output results
   ```

Se generan `recurrencia_por_categoria.csv`, `control_calidad.csv` y `recurrencia_por_categoria.png` en `results/`. El CSV fuente no se redistribuye en este repositorio.

## Estructura

- `src/analisis_recurrencia.py`: validación, agregación y gráfico.
- `results/`: resultados tabulares versionados; el gráfico se genera al ejecutar.
- `presentacion/`: diapositivas ejecutivas exportadas como imágenes y su índice.
- `data/`: ubicación local esperada para el CSV, que se descarga por separado.

---

**Repositorio:** [github.com/Luwil2001/Castillo_Luwil_Preentrega3.pdf](https://github.com/Luwil2001/Castillo_Luwil_Preentrega3)  
**Presentación:** [ver las cinco diapositivas](presentacion/README.md)  
**LinkedIn:** [perfil de Luwil Castillo](https://www.linkedin.com/in/luwil-castillo-874179324)  
