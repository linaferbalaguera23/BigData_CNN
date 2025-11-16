# Nombre: Lina Fernanda Rodriguez Balaguera, Codigo: 20252695007

# Proyecto Final: Inventario de Salón de Cómputo

Este proyecto implementa un sistema web (`index.html`) que utiliza un modelo de *deep learning* para detectar y contar 6 objetos en un salón de cómputo. La predicción se ejecuta 100% local en el navegador usando TensorFlow.js.

## 1. Aplicación Final

La aplicación está desplegada en GitHub Pages y es 100% funcional.

* **Enlace de Prueba:** **[https://linaferbalaguera23.github.io/BigData_CNN/Inventario/index.html](https://linaferbalaguera23.github.io/BigData_CNN/Inventario/index.html)**

### Instrucciones de Uso

1.  Abrir el enlace en un navegador (Chrome/Firefox).
2.  Esperar unos segundos a que el botón "Seleccionar archivo" se active (esto indica que el modelo de 6.3 MB se cargó en memoria).
3.  Subir una imagen `.jpg` del salón.
4.  La aplicación procesará la imagen (usando la GPU del navegador vía `webgl`) y mostrará los resultados.

---

## 2. Modelo y Entrenamiento

Se siguió un proceso de experimentación para encontrar el modelo con el mejor balance entre precisión y eficiencia.

### Arquitectura Seleccionada

* **Modelo:** **YOLOv8-Nano (`yolov8n.pt`)**
* **Justificación:** Se seleccionó esta arquitectura por su **excelente balance entre eficiencia y precisión**. El modelo final exportado a TensorFlow.js pesa solo **6.3 MB**, cumpliendo sobradamente con el requisito del 40% de la nota por "tamaño del archivo".

### Dataset y Experimentación

Se utilizó [Roboflow](https://roboflow.com/) para el etiquetado, preprocesamiento (`Resize 640x640`) y aumentación de datos.

Se probaron múltiples datasets, concluyendo que el "Mejor Modelo" se obtuvo con un dataset enfocado de **104 imágenes** (80/10/10 split) y aumentaciones ligeras (`Flip`, `Rotation`, `Brightness`).

Experimentos posteriores con datasets más grandes (144+ imágenes) y aumentaciones agresivas (`Mosaic`) resultaron en un mAP inferior, demostrando que el primer dataset era de mayor calidad y menos ruidoso.

### Entrenamiento y Resultados (El Modelo Campeón)

El modelo final se entrenó en Google Colab (GPU T4) durante **100 épocas**.

* **Precisión (mAP50):** El modelo alcanzó un **mAP50 (Mean Average Precision) general de 87.8%**.
* **Tamaño:** 6.3 MB

El desglose de precisión por clase fue el siguiente:

| Clase | mAP50 |
| :--- | :---: |
| **all** | **87.8%** |
| Teclado (5) | 97.7% |
| Mesa (1) | 95.3% |
| CPU (0) | 90.6% |
| Mouse (2) | 88.0% |
| Pantalla (3) | 85.9% |
| Silla (4) | 69.1% |

---

## 3. Stack Tecnológico

* **Entrenamiento:** Google Colab, Ultralytics YOLOv8, Roboflow.
* **Aplicación Web:** HTML5, CSS3.
* **Inferencia Local:** **TensorFlow.js (TF.js)** con backend `webgl` para aceleración por GPU en el navegador.
1.  Abrir el archivo `index.html` en un navegador web (Chrome/Firefox recomendado).
2.  Hacer clic en el botón **'Seleccionar archivo'** y subir una imagen `.jpg` del salón.
3.  Esperar a que el modelo procese la imagen (aparecerá un mensaje "Procesando...").
4.  Los resultados aparecerán automáticamente:
    * Una imagen con las cajas de detección en **color azul** y el **ID numérico** de la clase.
    * Un conteo total de cada objeto encontrado.
