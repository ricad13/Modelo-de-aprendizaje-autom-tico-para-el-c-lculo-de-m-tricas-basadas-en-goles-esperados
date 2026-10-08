# XGNet 

Modelo de aprendizaje automático para la predicción de **Expected Goals (xG)** en fútbol mediante técnicas de **Deep Learning**.

XGNet utiliza una red neuronal de tipo **Multilayer Perceptron (MLP)** para estimar la probabilidad de que un disparo termine en gol, combinando información espacial, contextual y técnica de cada acción de disparo.

## Descripción

El objetivo de este proyecto es desarrollar y evaluar un modelo predictivo capaz de estimar la probabilidad de gol de los disparos realizados durante partidos de fútbol.

El proyecto parte de datos abiertos de **StatsBomb** y realiza un proceso completo de tratamiento y transformación de los datos, incluyendo:

* Limpieza y estructuración de los datos.
* Selección de variables relevantes.
* Ingeniería de características.
* Incorporación de información espacial mediante `freeze frame`.
* Creación de variables geométricas.
* Análisis exploratorio de los datos.
* Entrenamiento de modelos de Machine Learning.
* Desarrollo y optimización de una red neuronal profunda.
* Evaluación y comparación de los modelos.
* Almacenamiento del modelo entrenado y del escalador.

El conjunto de datos final utilizado contiene **87.111 registros y 56 variables**, centrados principalmente en acciones de disparo.

## Objetivos

Los principales objetivos del proyecto son:

1. Recopilar y procesar datos de eventos de fútbol.
2. Identificar las variables que influyen en la probabilidad de gol.
3. Crear nuevas características espaciales y geométricas.
4. Desarrollar un modelo de Deep Learning para la predicción de xG.
5. Comparar el modelo con algoritmos clásicos de Machine Learning.
6. Evaluar los modelos mediante métricas como **MSE, Log Loss y AUC**.
7. Crear un flujo de trabajo reproducible que permita realizar predicciones sobre nuevos datos.

## Modelo XGNet

El modelo principal, denominado **XGNet**, está basado en una red neuronal **Multilayer Perceptron (MLP)**.

La arquitectura cuenta con:

```text
Entrada
   │
   ▼
256 neuronas — ReLU — Dropout 30%
   │
   ▼
128 neuronas — ReLU — Dropout 20%
   │
   ▼
64 neuronas — ReLU
   │
   ▼
1 neurona — Sigmoid
   │
   ▼
Probabilidad de gol (xG)
```

La salida del modelo es un valor entre **0 y 1**, interpretable como la probabilidad estimada de que el disparo termine en gol.

### Configuración del entrenamiento

* **Arquitectura:** MLP
* **Capas ocultas:** 256 → 128 → 64
* **Activación:** ReLU
* **Regularización:** Dropout y Weight Decay
* **Función de pérdida:** MSE
* **Optimizador:** Adam
* **Learning rate inicial:** 0.001
* **Weight decay:** 10⁻⁴
* **Scheduler:** ReduceLROnPlateau
* **Early stopping:** 10 épocas
* **División:** 80% entrenamiento / 20% validación
* **Normalización:** StandardScaler

## Variables utilizadas

Entre las características utilizadas se encuentran:

* Posición del disparo.
* Distancia a portería.
* Ángulo de disparo.
* Seno y coseno del ángulo.
* Distancia al cuadrado.
* Interacción entre distancia y ángulo.
* Presión defensiva.
* Portería abierta.
* Parte del cuerpo utilizada.
* Técnica de disparo.
* Tipo de disparo.
* Patrón de juego.
* Número de compañeros cercanos.
* Número de rivales cercanos.
* Posición del portero.
* Información espacial procedente del `freeze frame`.

Estas variables permiten representar tanto las características del disparo como el contexto en el que se produce.

## Datos

Los datos proceden del repositorio abierto de **StatsBomb** y están disponibles en formato JSON.

Para este proyecto se analizaron los partidos disponibles hasta mayo de 2025, centrando el estudio en los eventos de tipo **Shot**.

El `freeze frame` permite incorporar información sobre la posición de jugadores y portero en el momento del disparo, proporcionando contexto espacial adicional para el modelo.

## Modelos comparados

Además de XGNet, el proyecto contempla modelos clásicos de Machine Learning como:

* Regresión Logística
* Random Forest
* Gradient Boosting

El objetivo es comparar el rendimiento de estos enfoques con el modelo basado en Deep Learning.

## Evaluación

Los modelos se evalúan utilizando diferentes métricas:

* **MSE (Mean Squared Error)**
* **Log Loss**
* **AUC (Area Under the ROC Curve)**

Estas métricas permiten evaluar la calidad de las probabilidades generadas por los diferentes modelos y comparar su capacidad predictiva.

##  Flujo del proyecto

```text
Datos StatsBomb
       │
       ▼
Extracción de eventos Shot
       │
       ▼
Limpieza y tratamiento
       │
       ▼
Ingeniería de características
       │
       ▼
Análisis exploratorio
       │
       ▼
Preparación de los datos
       │
       ├───────────────┐
       ▼               ▼
Modelos clásicos    XGNet
       │               │
       └───────┬───────┘
               ▼
          Evaluación
               │
               ▼
       Comparación de modelos
               │
               ▼
       Modelo final + Scaler
```

## Tecnologías

El proyecto utiliza principalmente:

* **Python**
* **Pandas**
* **NumPy**
* **Scikit-learn**
* **PyTorch**
* **Matplotlib**
* **Seaborn**

Python se utiliza como lenguaje principal para la gestión, transformación, análisis y modelización de los datos.


## Aplicaciones

Un modelo de xG puede utilizarse como herramienta de apoyo para:

* Análisis táctico.
* Evaluación del rendimiento de jugadores.
* Scouting.
* Evaluación de oportunidades de gol.
* Análisis de equipos.
* Investigación en analítica deportiva.
* Desarrollo de futuras aplicaciones de predicción en tiempo real.

El trabajo plantea también la posibilidad de integrar este tipo de modelos en plataformas de visualización y análisis deportivo.

## Contexto del proyecto

Este repositorio contiene el desarrollo asociado a un proyecto académico sobre la evaluación de modelos de aprendizaje automático para el cálculo de métricas basadas en goles esperados.

El proyecto combina **fútbol, ciencia de datos, Machine Learning y Deep Learning** para estudiar cómo diferentes características de un disparo pueden utilizarse para estimar su probabilidad de convertirse en gol.

## Autor

**Adrián Rico Hernández**

Proyecto académico — Analítica deportiva y Machine Learning.

---

⭐ Si te resulta interesante el proyecto, puedes darle una estrella al repositorio.

