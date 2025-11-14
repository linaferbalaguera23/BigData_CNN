# Nombre: Lina Fernanda Rodríguez Balaguera, Código: 20252695007

## Proyecto Final: Inventario de Salón de Cómputo

Este proyecto es una aplicación web (`index.html`) que utiliza un modelo de *deep learning* para detectar y contar 6 tipos de objetos en un salón de cómputo. La predicción se ejecuta 100% local en el navegador usando TensorFlow.js.

## 1. Modelo Utilizado

* **Arquitectura:** YOLOv8-Nano (n)
* **Por qué se eligió:** Se seleccionó este modelo por su **excelente equilibrio entre precisión y eficiencia**. Al ser un modelo "nano", su archivo de parámetros es extremadamente pequeño (**6.3 MB**), cumpliendo con el requisito principal de eficiencia.
* **Precisión (mAP50):** El modelo final alcanzó un **87.8%** de mAP50 en el conjunto de pruebas.

## 2. Entrenamiento

* **Plataforma de Datos:** Se utilizó [Roboflow](https://roboflow.com/) para el etiquetado, preprocesamiento (Resize 640x640) y aumentación de datos (Flip, Rotation, Brightness).
* **Dataset:** Se generó un dataset de 104 imágenes originales, dividido en Train (82), Valid (11) y Test (11).
* **Entorno de Entrenamiento:** El modelo se entrenó en **Google Colab** utilizando una **GPU T4** para acelerar el proceso (100 épocas).
* **Framework:** Ultralytics YOLOv8.

## 3. Uso de la Aplicación

1.  Abrir el archivo `index.html` en un navegador web (Chrome/Firefox recomendado).
2.  Hacer clic en el botón **'Seleccionar archivo'** y subir una imagen `.jpg` del salón.
3.  Esperar a que el modelo procese la imagen (aparecerá un mensaje "Procesando...").
4.  Los resultados aparecerán automáticamente:
    * Una imagen con las cajas de detección en **color azul** y el **ID numérico** de la clase.
    * Un conteo total de cada objeto encontrado.
