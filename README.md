# 🏃‍♂️ GPS Biomechanics: Análisis de Curvas vs. Rectas

Este repositorio contiene un flujo de trabajo avanzado en Python (compatible con Quarto/Jupyter) para el procesamiento, filtrado y análisis biomecánico de datos GPS/GNSS en deportes.

El objetivo principal es descomponer la aceleración del atleta en componentes vectoriales (**Tangencial** y **Normal**) para cuantificar el rendimiento físico diferenciando entre carrera lineal y carrera en curva (Curved Sprinting).

## 🎯 Características Principales

* **Procesamiento de Cinemática Inversa:** Convierte coordenadas GPS (`lat`, `lon`) en métricas biomecánicas precisas sobre un plano tangente.
* **Comparativa de Algoritmos:** Implementa y compara 3 métodos de filtrado para calcular aceleraciones y radios de giro (M1, M2.1, M2.2).
* **Perfilado Aceleración-Velocidad (AS):** Generación de perfiles *in-situ* considerando el radio de giro.
* **Análisis de Envolventes:** Cálculo de máximos de rendimiento (P99) para aceleración total, tangencial y normal en función del radio.
* **Visualización Avanzada:**
    * Superficies 3D (Velocidad vs Radio vs Aceleración).
    * Heatmaps de "Jerk" (Brusquedad/Impulsividad).
    * Matrices de correlación y validación cruzada entre métodos.

## 🧠 Métodos de Cálculo Implementados

El código compara tres enfoques matemáticos para limpiar la señal del GPS:

| Método | Descripción | Detalle Técnico |
| :--- | :--- | :--- |
| **M1: Híbrido** | Combina la velocidad reportada por el dispositivo con el cambio de dirección calculado por coordenadas. | Utiliza filtros Gaussianos y calcula la velocidad angular ($\omega$) basada en el *heading* y la velocidad Doppler suavizada. |
| **M2.1: Media Móvil** | Método posicional puro basado en ventanas deslizantes ("Rolling Mean"). | Considerado método *Legacy*. Tiende a generar ruido en las derivadas debido a la naturaleza del suavizado simple. |
| **M2.2: Gaussiano** | Método recomendado basado en filtros gaussianos y derivación pitagórica. | Calcula la aceleración Normal vía Pitágoras ($a_n = \sqrt{a_{tot}^2 - a_{tan}^2}$) y filtra aceleraciones "imposibles" (>15 m/s²) antes de recombinar componentes. |

## 📦 Requisitos

El proyecto utiliza librerías estándar de ciencia de datos en Python:

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn plotly dataframe_image
