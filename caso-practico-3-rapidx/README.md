# 🚖 Caso Práctico 3 — RapidX: Pipeline JSON → Parquet → BI

Pipeline completo de datos: **JSON operacionales → enriquecimiento → Parquet particionado → consultas SQL** sobre datos sintéticos de una plataforma de movilidad urbana en 5 ciudades españolas.

## 📁 Estructura

```
caso-practico-3-rapidx/
├── caso-practico-3-rapidx.ipynb   ← Notebook principal (este caso)
├── README.md                       ← Este archivo
├── json_raw/                       ← Se crea al ejecutar Parte 3 (7 ficheros JSON)
└── salida/                         ← Se crea al ejecutar Parte 7
    └── parquet_bi/                 ← Parquet particionado por ciudad
        ├── ciudad=Madrid/
        ├── ciudad=Barcelona/
        ├── ciudad=Sevilla/
        ├── ciudad=Valencia/
        └── ciudad=Bilbao/
```

## ▶️ Cómo ejecutarlo

1. Abre `caso-practico-3-rapidx.ipynb` en VS Code (kernel **Almond / Scala**).
2. Ejecuta las celdas **en orden**, de arriba abajo.
3. **No necesitas descargar nada**: los 7 ficheros JSON se generan en la Parte 3 dentro de la propia carpeta del caso.

## 📊 Lo que incluye

- **Parte 1-2**: Inicialización Spark + creación de carpetas locales.
- **Parte 3**: Generación de **7 JSON sintéticos** (51 viajes en Madrid, Barcelona, Sevilla, Valencia y Bilbao).
- **Parte 4**: Lectura masiva con `spark.read.json("json_raw/*.json")` (multi-line).
- **Parte 5**: Enriquecimiento con **10 columnas calculadas** (`franja_horaria`, `importe_total`, `precio_por_km`, `segmento_conductor`...) usando funciones nativas (`when`, `to_timestamp`, `round`).
- **Parte 6**: Selección BI eliminando campos operacionales (`_batch_id`, `_sys_version`).
- **Parte 7**: Escritura **Parquet particionado por `ciudad`** con `repartition` previo (buena práctica anti-OOM en local).
- **Parte 8**: Vista SQL `viajes_rapidx` para consultas analíticas.
- **Parte 9**: **7 consultas BI** (ingresos por ciudad, demanda por franja, top conductores, métodos de pago, surge, cancelaciones...).
- **Parte 10**: Respuestas a las preguntas de reflexión.

## 🛠️ Requisitos

- VS Code con la extensión de Jupyter.
- Kernel **Almond** (Scala 2.13).
- Spark 4.1.1 (se descarga automáticamente vía Coursier).

## 💡 Notas técnicas

- **Caso autocontenido**: las rutas son relativas (`val rutaBase = "."`), por lo que el caso es portable: copia la carpeta a cualquier sitio y funcionará.
- **Datos sintéticos**: no se descarga nada externo; todo el dataset se genera dentro del notebook.
- El cierre final usa `SparkSession.getActiveSession` defensivo para no fallar si el kernel se ha reiniciado.
