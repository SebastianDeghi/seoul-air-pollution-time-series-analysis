# 🌍 Análisis de series temporales de contaminantes atmosféricos en Seúl (2017-2020)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-notebook-orange)](https://jupyter.org/)
[![Geopandas](https://img.shields.io/badge/geopandas-mapping-green)](https://geopandas.org/)
![Visitas](https://komarev.com/ghpvc/?username=SebastianDeghi&repo=seoul-air-pollution-time-series-analysis&color=blue&style=flat)

### 👥 Colaboradores: **David Abba, Eduardo Andreozzi, Pablo Astoreca y Eduardo Castro Luna.**

***

## 📝 Descripción General

Análisis exploratorio y limpieza de datos de calidad del aire en Seúl (2017-2020), abarcando 25 estaciones de monitoreo y 6 contaminantes (PM10, PM2.5, SO2, NO2, O3, CO). Se identificaron patrones temporales, estacionales y diferencias geográficas, así como errores instrumentales (picos idénticos por saturación de sensores, valores negativos). Se implementaron estrategias de limpieza y visualización interactiva de series temporales.

***

## 📁 Estructura del Proyecto

La organización de los archivos en este repositorio es la siguiente:

```
seoul-air-pollution-time-series-analysis/
├── Seoul_Air_Pollution_Analysis.ipynb   # Notebook principal
├── requirements.txt                     # Dependencias
├── LICENSE                              # Licencia MIT
├── .gitignore                           # Archivos ignorados
└── README.md                            # Este archivo
```

***

## 📊 Descripción del Dataset

El dataset **Air Pollution in Seoul**, creado por Bappekim en Kaggle, contiene mediciones horarias de calidad del aire en Seúl, Corea del Sur, entre 2017 y 2020.

- **Estaciones:** 25 estaciones de monitoreo distribuidas en distritos urbanos, suburbanos, cercanos a ríos y montañosos.
- **Contaminantes:** 6 contaminantes (PM10, PM2.5, SO2, NO2, O3, CO).
- **Variables:** Mediciones horarias de concentración para cada contaminante.
- **Archivos:**
    - `Measurement_summary.csv` - Datos agregados por fecha y contaminante
    - `Measurement_station_info.csv` - Ubicación e información de estaciones
    - `Measurement_item_info.csv` - Descripción y umbrales de cada contaminante
    - `Measurement_info.csv` - Lecturas originales por estación y contaminante

**Fuente original:** Seoul Metropolitan Government (Seoul Open Data Plaza)  
**Licencia:** Creative Commons Attribution (CC-BY)

***

## 🚀 Contaminantes Analizados

| Contaminante | Fuente Principal | Unidad | Umbral "Bad" (malo) |
| :--- | :--- | :--- | :--- |
| **PM10** | Polvo, construcción, tráfico | µg/m³ | 150 |
| **PM2.5** | Combustión, industria | µg/m³ | 75 |
| **SO2** | Industria, calefacción | ppm | 0.15 |
| **NO2** | Tráfico vehicular | ppm | 0.20 |
| **O3** | Formación fotoquímica | ppm | 0.15 |
| **CO** | Combustión incompleta | ppm | 15 |

**Conclusión Clave:** El NO₂ muestra un patrón diario claro asociado al tráfico (picos en horas pico 8-9 AM y 6-7 PM). Las estaciones cercanas a autopistas presentan valores ~20-30% más altos. O₃ presenta anticorrelación con NO₂ (formación fotoquímica en horas de mayor radiación solar). PM10 y PM2.5 muestran episodios agudos asociados a tormentas de polvo asiático y estancamiento atmosférico.

***

## 🗺️ Visualizaciones Implementadas

- **Mapa satelital** con las 25 estaciones de monitoreo geolocalizadas
- **Gráficos de barras** de umbrales de calidad del aire (Good, Normal, Bad, Very Bad)
- **Series temporales** por estación y contaminante (antes y después de limpieza)
- **Patrones horarios de NO₂** con marcado de horas pico de tráfico
- **Análisis espectral** (periodograma) para detectar ciclos diarios en NO₂
- **Comparación** de estaciones cerca vs lejos de autopistas

***

## 🔧 Instalación y Uso

Sigue estos pasos para clonar el repositorio, configurar el entorno y ejecutar el análisis en tu máquina local.

### 1. Clonar el repositorio

Abre tu terminal y ejecuta:
```bash
git clone https://github.com/SebastianDeghi/seoul-air-pollution-time-series-analysis.git
cd seoul-air-pollution-time-series-analysis
```

### 2. Crear y activar un entorno virtual (recomendado)

- En **Windows**:
  ```bash
  python -m venv venv
  venv\Scripts\activate
  ```
- En **macOS/Linux**:
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

### 3. Instalar dependencias

Con el entorno virtual activo, instala los paquetes necesarios:
```bash
pip install -r requirements.txt
```

**Nota:** El archivo `requirements.txt` incluye las siguientes librerías:
- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `geopandas`
- `contextily`
- `scipy`
- `statsmodels`
- `kagglehub`
- `jupyter`
- `tqdm`
- `session-info`

### 4. Ejecutar el notebook

Finalmente, lanza Jupyter Notebook para abrir el archivo principal:
```bash
jupyter notebook Seoul_Air_Pollution_Analysis.ipynb
```

### 5. (Opcional) Descargar el dataset

El notebook descargará automáticamente el dataset desde Kaggle usando `kagglehub`. Si es la primera vez, asegúrate de tener configuradas tus credenciales de Kaggle.

***

## 📈 Hallazgos Principales

| Contaminante | Hallazgo Clave |
|--------------|----------------|
| **PM10 y PM2.5** | Picos agudos (>150 µg/m³) por eventos de polvo asiático; las estaciones urbanas muestran promedios más altos |
| **NO2** | Patrón diario de tráfico claro (picos a las 8-9 AM y 6-7 PM); estaciones cerca de autopistas muestran valores ~20-30% más altos |
| **O3** | Anticorrelación con NO2 (formación fotoquímica); máximo durante el mediodía en verano |
| **SO2 y CO** | Generalmente bajos debido a políticas ambientales exitosas; pequeños picos en invierno por calefacción |

### Problemas de Calidad de Datos Detectados y Corregidos

- Picos idénticos extremadamente altos en PM10/PM2.5 (saturación de sensores >950 µg/m³) → reemplazados por NaN
- Valores negativos en SO2 (errores instrumentales) → reemplazados por NaN

***

## 🗺️ Visualizaciones Incluidas

- Mapa satelital con las 25 estaciones de monitoreo
- Gráficos de series temporales por estación y contaminante
- Gráficos de barras de umbrales de calidad del aire (Bueno, Normal, Malo, Muy Malo)
- Patrones horarios de NO2 con marcado de horas pico de tráfico
- Análisis espectral (periodograma) para ciclos diarios de NO2
- Comparación de estaciones cerca vs. lejos de autopistas

***

## 📚 Dependencias

- `numpy`, `pandas`, `matplotlib`, `seaborn`
- `geopandas`, `contextily`, `shapely` (para mapas)
- `scipy`, `statsmodels` (para análisis espectral y series temporales)
- `kagglehub` (para descarga del dataset)
- `jupyter`, `session-info`

***

## 📄 Licencia

Este proyecto está bajo la **Licencia MIT**. Consulta el archivo [LICENSE](LICENSE) para más detalles.

***

## 🙏 Agradecimientos

- **Bappekim** por publicar el dataset en Kaggle
- **Gobierno Metropolitano de Seúl** por proporcionar los datos abiertos
- **Seoul Open Data Plaza** y **Air Quality Analysis Center**

***

## 👤 Autor

**Sebastián Deghi**

- GitHub: [@SebastianDeghi](https://github.com/SebastianDeghi)
- LinkedIn: [@sebastian-deghi](https://www.linkedin.com/in/sebastian-deghi/)
- Google Scholar: [@Sebastian E. Deghi](https://scholar.google.com/citations?user=3Nq5hTIAAAAJ&hl=en)