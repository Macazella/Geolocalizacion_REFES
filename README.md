Perfecto. A continuación te presento el `README.md` completo y estructurado para el proyecto:

# 🗺️ Proyecto de Geolocalización de Establecimientos Sanitarios Públicos (REFES)

Este proyecto implementa un pipeline completo de procesamiento y geolocalización de datos de establecimientos asistenciales de Argentina, utilizando fuentes oficiales del Registro Federal de Establecimientos de Salud (REFES) publicado por el Ministerio de Salud en [datos.gob.ar](https://datos.gob.ar/ja/dataset/salud_336cf4d9-447a-44c4-8e34-0ba1fc293d55).

---

## 🎯 Objetivo

Georreferenciar, depurar y visualizar los registros del padrón nacional de efectores sanitarios, priorizando aquellos con mayor criticidad (PRIORIDAD_CORREGIDA 1 a 6), para su análisis espacial en herramientas como Power BI o mapas interactivos en HTML.

---

## 📁 Estructura del Proyecto

```

PROJ005/
├── 01\_INPUTS/
│   └── establecimientos-asistenciales-asentados.xlsx
├── 02\_REFERENCIAS/
│   └── abreviaturas\_direcciones.csv
├── 03\_SCRIPTS/
│   └── *.py  ← Scripts de procesamiento secuencial
├── 04\_OUTPUTS/
│   ├── GEODATASETS/
│   │   ├── refes\_latlong.csv
│   │   └── mapa\_establecimientos\_ok.html
│   ├── ARCHIVOS\_INTERMEDIOS/
│   │   └── checkpoint\_*.csv
│   └── REINTENTOS/
│       └── errores\_reintentos.csv
└── README.md

````

---

## 🧪 Dependencias

Instalar requerimientos con:

```bash
pip install -r requirements.txt
````

**Principales librerías:**

* `pandas`
* `geopy`
* `folium`
* `tqdm`
* `matplotlib`
* `python-dotenv`

---

## 🔁 Flujo de trabajo

| Orden | Script                                | Descripción                                          |
| ----- | ------------------------------------- | ---------------------------------------------------- |
| 1️⃣   | `crear_estructura.py`                 | Crea carpetas base del proyecto.                     |
| 2️⃣   | `eda_refes.py`                        | Carga y genera la columna `UBICACION_SUGERIDA`.      |
| 3️⃣   | `normalizar_ubicacion.py`             | Limpia y estandariza direcciones.                    |
| 4️⃣   | `geocodificar_nominatim.py`           | Geocodifica con Nominatim + checkpoints automáticos. |
| 5️⃣   | `reintentar_geolocalizacion.py`       | Reintenta errores con más tolerancia.                |
| 6️⃣   | `analizar_resultados_reintentos.py`   | Resume rendimiento de los reintentos.                |
| 7️⃣   | `analizar_errores_geocodificacion.py` | Agrupa y clasifica errores por tipo y región.        |
| 8️⃣   | `exportar_errores_para_validar.py`    | Exporta errores para revisión manual.                |
| 9️⃣   | `generate_map.py`                     | Crea mapa interactivo con registros OK.              |

---

## 🔐 Uso de API

Si se emplea Google Maps API, debe colocarse la API key en un archivo `.env`:

```
GOOGLE_API_KEY=tu_api_key_aqui
```

---

## 🌐 Fuente de datos

* **Nombre:** Establecimientos Asistenciales Registrados – REFES
* **URL directa:** [Descargar dataset](https://datos.gob.ar/ja/dataset/salud_336cf4d9-447a-44c4-8e34-0ba1fc293d55/archivo/salud_5d5710df-cf3f-4d91-b9c5-aecab1e06018)
* **Entidad:** Ministerio de Salud de la Nación Argentina

---

## 📊 Resultados esperados

* Archivos `.csv` con coordenadas latitud/longitud limpias.
* Reportes de error automatizados para revisión manual.
* Mapa interactivo para visualización exploratoria.
* Base lista para conectar con Power BI o Microsoft Fabric.

---

## 🧠 Créditos

Proyecto desarrollado por [@Macazella](https://github.com/Macazella) como ejercicio de integración de datos públicos, procesamiento geoespacial y automatización de flujos con Python.

