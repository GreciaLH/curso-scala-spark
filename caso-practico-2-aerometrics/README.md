# ✈️ Caso Práctico 2 — AeroMetrics: Benchmark de formatos

## 📥 Descarga del dataset (paso obligatorio antes de ejecutar el notebook)

**Fuente Kaggle:** <https://www.kaggle.com/datasets/yuanyuwendymu/airline-delay-and-cancellation-data-2009-2018>

10 ficheros CSV (uno por año 2009-2018), ≈ 6 GB en total.

**Para este caso práctico es suficiente con 3 años** (`2016.csv`, `2017.csv`, `2018.csv` ≈ 17 M filas, ~1.7 GB). El benchmark sigue siendo plenamente representativo y los tiempos son manejables en local.

### Pasos

1. Crear cuenta gratuita en Kaggle si no la tienes.
2. Descargar los 3 (o 10) CSV deseados.
3. Crear la carpeta destino **dentro de esta misma carpeta del caso práctico** (PowerShell, desde la raíz del repo):

   ```powershell
   New-Item -ItemType Directory -Force -Path ".\caso-practico-2-aerometrics\csv_raw"
   ```

4. Mover los CSV descargados a `caso-practico-2-aerometrics\csv_raw\`.

### Estructura final esperada (autocontenida)

```text
caso-practico-2-aerometrics\
  caso-practico-2-aerometrics.ipynb
  README.md
  csv_raw\
    2016.csv
    2017.csv
    2018.csv
  salida\           # se generará al ejecutar el notebook
```

## ▶️ Ejecución

Abrir [caso-practico-2-aerometrics.ipynb](caso-practico-2-aerometrics.ipynb) y ejecutar las celdas en orden.

| Parte | Requiere CSV descargados |
| --- | --- |
| 1 — Inicialización Spark | ❌ |
| 2 — Funciones benchmark | ❌ |
| 3 — Crear carpetas | ❌ |
| 4 — Schema manual | ❌ |
| **5 — Lectura CSV** | ✅ |
| 6 a 13 | ✅ |

## 💾 Salidas generadas

Tras ejecutar el notebook completo se crearán en `caso-practico-2-aerometrics\salida\` (relativo a la carpeta del caso):

- `consolidado_csv/` — copia consolidada en CSV
- `parquet_sin_partir/` — Parquet sin particionar
- `orc/` — ORC
- `avro/` — Avro
- `parquet_particionado/` — Parquet particionado por `ANIO=`

## ⚠️ Notas

- El notebook **no descarga** automáticamente el dataset (requiere autenticación de Kaggle).
- Si solo descargas algunos años, ajusta `val anioConsulta = 2018` en la celda 9.5.
- Las salidas pueden ocupar varios GB de disco; libera espacio antes de ejecutar.
