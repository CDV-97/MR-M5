# Clasificación de tumores cerebrales en imágenes de resonancia magnética

Proyecto académico desarrollado con TensorFlow y Keras. El modelo clasifica imágenes en cuatro categorías: `glioma`, `meningioma`, `notumor` y `pituitary`.

## Datos y ejecución

El notebook descarga la versión 2 de [Brain Tumor MRI Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset/versions/2), elimina duplicados exactos y prepara las particiones de entrenamiento, validación y prueba.

Para reproducir el entrenamiento, abre `brain_tumor_classification.ipynb` en Google Colab y ejecuta las celdas en orden. La sección 6 incluye la función `predict_image` y un ejemplo de carga de imágenes. Para usar el modelo ya entrenado, coloca `modelo_final.keras`, `etiquetas.json` y `configuracion.json` en la carpeta `resultados_brain` del entorno de Colab y ejecuta las celdas de inferencia con sus importaciones.

## Resultados

La CNN con aumento de datos obtuvo el mayor F1 macro de validación (0.9628) entre las configuraciones evaluadas. En las 1,579 imágenes de prueba obtuvo 85.56 % de accuracy y 0.8533 de F1 macro.

El modelo clasificó como `notumor` 170 de las 1,179 imágenes de prueba etiquetadas con tumor (14.42 %). La separación se realizó por imagen debido a la falta de identificadores de paciente. La aplicación tiene un propósito académico.
