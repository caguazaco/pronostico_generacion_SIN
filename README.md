# pronostico_generacion_SIN
Pipeline de procesamiento, entrenamiento y evaluación para el pronóstico de corto plazo (horizonte de 7 días) de la generación de energía eléctrica del Sistema Interconectado Nacional (SIN) de Colombia.

## Descripción del Proyecto

El objetivo principal es predecir la generación total diaria del SIN empleando tanto series históricas de generación (hidráulica, térmica) y precios de bolsa, como variables exógenas de precios de oferta de gas natural y carbón.

La particularidad técnica de este proyecto radica en su enfoque:
1. **Rama secuencial:** Procesa las series de tiempo y variables de calendario directamente mediante redes recurrentes ('LSTM', 'GRU', 'BiLSTM' o 'CNN-LSTM').
2. **Codificación visual de series temporales:** Transforma los datos unidimensionales en imágenes empleando técnicas como:
   * Gramian Angular Summation/Difference Fields (GASF/GADF)
   * Markov Transition Fields (MTF)
   * Recurrence Plots (RP)
   * Escalogramas (CWT)
   * Espectrogramas (STFT)
3. **Rama de imágenes (Modelos CNN & ViT):** Extrae patrones visuales bidimensionales a partir de las codificaciones anteriores mediante transferencia de aprendizaje ('MobileNetV2', 'EfficientNetB0', 'ResNet50V2') o Vision Transformers (ViT).

## Metodología y modelos

El notebook implementa y compara tres arquitecturas principales:
* **Modelos secuenciales:** Redes neuronales recurrentes sobre las series temporales.
* **Modelos convolucionales / ViT:** Redes de visión artificial aplicadas únicamente a las codificaciones visuales de las series temporales.
* **Modelos multimodales:** Integran de forma conjunta el procesamiento secuencial y las características visuales extraídas mediante mecanismos de fusión por concatenación o atención.

Adicionalmente, se incluye una metodología de calibración mediante bandas conformales para estimar intervalos de predicción no paramétricos con coberturas probabilísticas del 80% y 90%.

## Datos
* **Fuente:** XM S.A. E.S.P. (Operador del SIN).
* **Frecuencia:** Diaria.
* **Rango:** 01 de enero de 2006 al 31 de diciembre de 2025.
