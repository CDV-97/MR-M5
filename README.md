# Clasificación de tumores cerebrales en resonancias magnéticas

Clasificador de imágenes desarrollado con TensorFlow y Keras para cuatro categorías: glioma, meningioma, sin tumor (`notumor`) y tumor hipofisario (`pituitary`).

## Datos y preparación

El notebook descarga la versión 2 de [Brain Tumor MRI Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset/versions/2). Se eliminaron duplicados exactos y se conservaron únicamente en prueba las imágenes que aparecían tanto en entrenamiento como en prueba. Tras la limpieza, quedaron 4,239 imágenes para entrenamiento, 1,060 para validación y 1,579 para prueba.

## Resultados

| Modelo | Accuracy de validación | F1 macro de validación |
| --- | ---: | ---: |
| CNN inicial | 95.66 % | 0.9563 |
| **CNN con aumento de datos** | **96.32 %** | **0.9628** |
| MobileNetV2 congelada | 87.92 % | 0.8763 |
| MobileNetV2 con ajuste fino | 93.87 % | 0.9384 |

Se seleccionó la CNN con aumento de datos por su mayor F1 macro de validación. En prueba obtuvo **85.56 % de accuracy** y **0.8533 de F1 macro**. Clasificó como `notumor` 170 de las 1,179 imágenes etiquetadas con tumor (14.42 %). La separación se realizó por imagen debido a la falta de identificadores de paciente.

## Generar predicciones en Colab

1. Abrir [brain_tumor_classification.ipynb](brain_tumor_classification.ipynb) en Google Colab.
2. Descargar [modelo_final.keras](https://github.com/CDV-97/MR-M5/releases/download/v1.0.0/modelo_final.keras) desde el Release `v1.0.0`.
3. Crear la carpeta `resultados_brain` en el entorno de Colab y subir el modelo junto con [etiquetas.json](resultados_brain/etiquetas.json) y [configuracion.json](resultados_brain/configuracion.json).
4. Ejecutar la siguiente celda antes de la sección 6. Luego, ejecutar las celdas de esa sección para cargar una imagen y obtener su predicción.

```python
from pathlib import Path
import json

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import tensorflow as tf
from PIL import Image
from tensorflow import keras

OUTPUT_DIR = Path("/content/resultados_brain")
```

## Reproducir el entrenamiento

Abrir el notebook en Google Colab y ejecutar las celdas en orden. El notebook incluye la descarga y preparación del dataset, el entrenamiento de los modelos, la comparación en validación y la evaluación en prueba.
