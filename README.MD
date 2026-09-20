# ¿Puede un mapa de calor decirle a la policía dónde patrullar?

Análisis de focalización del delito mediante datos geográficos y estimación de densidad por kernel.

**Maestría en Inteligencia Analítica de Datos (MIAD) — Aprendizaje No Supervisado**
Módulo 7: Análisis de Puntos Calientes Geográficos

## Descripción

Este proyecto evalúa cinco procedimientos de focalización del delito usando datos georreferenciados de
homicidios y robos en Chicago (verano de 2019), con el fin de recomendar a la Policía Metropolitana de
Bogotá qué procedimiento adoptar y qué aprendizajes son transferibles entre ciudades.

## Preguntas de negocio

1. ¿Qué procedimiento de focalización debería adoptar la Policía Metropolitana de Bogotá?
2. ¿Qué elementos del enfoque de focalización del delito son generalizables entre contextos urbanos distintos?

## Estructura del repositorio

miad-ans-actividad-datos-geoespaciales-hotspot/
├── data/ # Datos de entrada
│ ├── Chicago_delitos_verano_2019.csv
│ ├── Areas_comunitarias_Chicago/ # Shapefile de las 77 áreas comunitarias
│ └── comercio_chicago.gpkg # Uso comercial del suelo (descargado de OSM)
├── output/ # Figuras generadas para la presentación
├── main.ipynb # Cuaderno de análisis
├── requirements.txt
└── README.md


## Metodología

El análisis sigue siete pasos:

1. **Exploración:** carga de datos, unión espacial y ranking por conteo.
2. **Correlación entre delitos:** robos vs. homicidios por área.
3. **Visualización:** conteo vs. densidad normalizada por superficie.
4. **Distancia al centro:** KDE univariado con validación cruzada.
5. **Puntos calientes:** KDE bivariado (normal_reference vs. cv_ml).
6. **Uso del suelo:** correlación del comercio (OpenStreetMap) con el delito.
7. **Ranking y recomendación:** comparación de procedimientos y transferencia a Bogotá.

## Requisitos

- Python 3.11
- Ver `requirements.txt` para las dependencias.

## Instalación y ejecución

```bash
# Crear y activar entorno virtual
python -m venv .venv
.venv\Scripts\activate        # Windows
# source .venv/bin/activate   # Linux/Mac

# Instalar dependencias
pip install -r requirements.txt

# Abrir el cuaderno
jupyter notebook main.ipynb
```

## Reproducibilidad

- Todos los procesos con aleatoriedad usan `random_state = 123`.
- Los datos se cargan mediante rutas relativas a la carpeta `data/`.
- Los datos de OpenStreetMap se descargan una vez y se guardan en `data/comercio_chicago.gpkg`
  para garantizar que el análisis sea reproducible con los mismos elementos.

## Hallazgo principal

Robos y homicidios tienen geografías distintas en Chicago: los robos se concentran en el centro
comercial y los homicidios en el oeste y el sur. El procedimiento recomendado es la estimación de
densidad por kernel bivariada, aplicada por separado a cada tipo de delito.

