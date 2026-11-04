# Clasificación de tumores cerebrales en resonancias magnéticas

Clasificador de imágenes desarrollado con TensorFlow y Keras. La red neuronal convolucional distingue cuatro categorías: glioma, meningioma, tumor hipofisario (`pituitary`) y sin tumor (`notumor`).

**Autor:** Carlos Manuel Delgado Vázquez

## Archivos de la entrega

| Archivo | Contenido |
| --- | --- |
| [Notebook ejecutado](brain_tumor_classification.ipynb) | Preparación de datos, entrenamiento, ajustes, evaluación, conclusiones y demostración de predicción. |
| [Modelo entrenado](https://github.com/CDV-97/MR-M5/releases/download/v1.0.0/modelo_final.keras) | Arquitectura y pesos de la CNN seleccionada, disponibles en el Release `v1.0.0`. |
| [Etiquetas](resultados_brain/etiquetas.json) y [configuración](resultados_brain/configuracion.json) | Orden de las clases y parámetros de procesamiento para la inferencia. |

## Datos y preparación

El notebook incluye el código para descargar la versión 2 de [Brain Tumor MRI Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset/versions/2). Se eliminaron duplicados exactos y se conservaron únicamente en prueba las imágenes que aparecían en ambas particiones originales.

Después de la limpieza, quedaron **4,239 imágenes de entrenamiento**, **1,060 de validación** y **1,579 de prueba**. Las imágenes se ajustaron a 128 × 128 píxeles con relleno para conservar su proporción.

## Entrenamiento y ajustes

La CNN inicial utiliza tres bloques convolucionales con capas de agrupación máxima. El primer ajuste incorporó rotaciones, traslaciones y cambios de escala suaves durante el entrenamiento. También se evaluó MobileNetV2 con la base congelada y con ajuste fino.

| Modelo | Exactitud en validación | F1 macro en validación |
| --- | ---: | ---: |
| CNN inicial | 95.66 % | 0.9563 |
| **CNN con aumento de datos** | **96.32 %** | **0.9628** |
| MobileNetV2 congelada | 87.92 % | 0.8763 |
| MobileNetV2 con ajuste fino | 93.87 % | 0.9384 |

## Evaluación en prueba

La CNN con aumento de datos se seleccionó por su mayor F1 macro en validación. En prueba obtuvo **85.56 % de exactitud** y **0.8533 de F1 macro**.

El principal patrón de error fue predecir `notumor` para imágenes etiquetadas con tumor. Esto ocurrió en **170 de 1,179 imágenes con tumor (14.42 %)**. La separación se realizó por imagen debido a la falta de identificadores de paciente.

## Reproducir el entrenamiento

1. Abrir el notebook en Google Colab.
2. Ejecutar en orden las celdas de preparación, entrenamiento y evaluación.
3. Consultar las tablas, las curvas de aprendizaje y la matriz de confusión en las salidas del notebook.

## Usar el modelo entrenado

1. Descargar `modelo_final.keras` desde el enlace de la entrega.
2. Colocar el archivo junto con `etiquetas.json` y `configuracion.json` en la carpeta `resultados_brain/` del entorno de Colab.
3. Consultar la sección 6 del notebook para revisar la función `predict_image` y el ejemplo ejecutado. Con el entorno del notebook inicializado, ejecutar las celdas de esa sección para cargar una imagen y obtener su categoría predicha y las puntuaciones de las cuatro clases.
