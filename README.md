# 📡 Análisis de Clientes – ConnectaTel

## 🎯 Objetivo del proyecto

Este proyecto analiza el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con datos registrados hasta el año 2024.

El objetivo es construir un **perfil estadístico de los clientes**, detectar comportamientos atípicos y crear segmentos de clientes para:

- Identificar patrones de consumo en llamadas y mensajes.
- Detectar problemas de calidad en los datos y aplicar limpieza.
- Diseñar estrategias de retención basadas en los segmentos encontrados.
- Sugerir mejoras en los planes ofrecidos por la empresa.

---

## 📂 Datasets utilizados

| Archivo | Descripción |
|---|---|
| `plans.csv` | Información de los planes disponibles: precio, minutos incluidos, GB incluidos y costo por extras. |
| `users_latam.csv` | Información de los clientes: edad, ciudad, fecha de registro, plan contratado y estado de churn. |
| `usage.csv` | Detalle del uso real de los servicios: tipo de evento (llamada o mensaje), duración y fecha. |

Los archivos deben ubicarse en la carpeta `/datasets/` para que el notebook los encuentre correctamente.

---

## 🧩 Etapas del análisis

### 1. Carga y exploración inicial
Carga de los tres datasets con `pd.read_csv()`, revisión de las primeras filas, forma y tipos de datos con `.head()`, `.shape` e `.info()`.

### 2. Identificación de problemas de calidad
- Detección de valores nulos y cálculo de proporciones.
- Identificación de sentinels (`-999` en `age`, `'?'` en `city`).
- Revisión y conversión de columnas de fechas; detección de años fuera de rango.

### 3. Limpieza de datos
- Reemplazo del sentinel `-999` en `age` por la mediana.
- Reemplazo del sentinel `'?'` en `city` por `pd.NA`.
- Marcado de fechas fuera de rango como nulas (`pd.NaT`).
- Verificación de nulos MAR (Missing At Random) en `duration` y `length`.

### 4. Estadísticas de uso por usuario
Agregación del dataset `usage` por `user_id` para obtener cantidad de mensajes, llamadas y minutos totales. Merge con `users` para construir el perfil completo (`user_profile`).

### 5. Visualización de distribuciones y outliers
- Histogramas por plan para `age`, `cant_mensajes`, `cant_llamadas` y `cant_minutos_llamada`.
- Boxplots para detección de outliers.
- Cálculo de límites con el método IQR y decisión justificada.

### 6. Segmentación de clientes
- **Por uso**: Bajo uso / Uso medio / Alto uso según cantidad de llamadas y mensajes.
- **Por edad**: Joven (< 30) / Adulto (30–59) / Adulto Mayor (≥ 60).
- Visualización de la distribución de cada segmento con gráficos de barras.

### 7. Análisis ejecutivo
Conclusiones accionables para el negocio: problemas detectados, caracterización de segmentos y recomendaciones estratégicas para mejorar los planes y reducir el churn.

---

## ▶️ Cómo ejecutar el notebook

El notebook está alojado en GitHub y se puede abrir directamente en **Google Colab** sin instalar nada.

1. Ir al repositorio en GitHub.
2. Abrir el archivo `S7_Version-Estudiante-Project-ConnectaTel_COMPLETO.ipynb`.
3. Hacer clic en el botón **"Open in Colab"** (o pegar la URL del archivo en [colab.research.google.com](https://colab.research.google.com)).
4. En Colab, subir los archivos de datos a la carpeta `/datasets/`:
   ```
   from google.colab import files
   import os
   os.makedirs('/datasets', exist_ok=True)
   # Luego subir plans.csv, users_latam.csv y usage.csv
   ```
5. Ejecutar las celdas en orden con **Runtime → Run all** o `Ctrl + F9`.

---

## 🔁 Guía de reproducción

```
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/connectatel-analysis.git
cd connectatel-analysis

# 2. (Opcional) Crear un entorno virtual
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# 3. Instalar dependencias
pip install pandas numpy matplotlib seaborn jupyter

# 4. Colocar los datasets en la carpeta /datasets/
#    plans.csv, users_latam.csv, usage.csv

# 5. Lanzar Jupyter y abrir el notebook
jupyter notebook S7_Version-Estudiante-Project-ConnectaTel_COMPLETO.ipynb
```

> **Nota:** Si se ejecuta en Google Colab, los pasos 2 y 3 no son necesarios, ya que Colab tiene las librerías preinstaladas.

---

## 🛠️ Librerías utilizadas

- `pandas` — manipulación y limpieza de datos
- `numpy` — operaciones numéricas
- `matplotlib` — visualizaciones base
- `seaborn` — visualizaciones estadísticas
