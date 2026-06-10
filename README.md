# Generalización cross-age en biometría de oreja

Este repositorio contiene el código utilizado en el Trabajo de Fin de Grado **"Generalización cross-age en biometría de oreja: evaluación entre población adulta e infantil"**, desarrollado por **Rafael Suárez Saavedra** en el Grado en Ciencia e Ingeniería de Datos de la **Universidad de Las Palmas de Gran Canaria (ULPGC)**.

El objetivo principal del trabajo es estudiar la capacidad de generalización de modelos de *Deep Learning* para reconocimiento biométrico de oreja cuando existe una diferencia de edad entre los datos de entrenamiento y los datos de evaluación. En concreto, se entrenan modelos con imágenes de población adulta y se evalúan sobre imágenes infantiles.

## Contenido del proyecto

El proyecto está desarrollado principalmente en un notebook de Jupyter/Google Colab:

```text
codigo_TFG_Rafael_Suárez.ipynb
```

El notebook incluye las siguientes partes principales:

1. **Descarga y preparación de datos**  
   Descarga del conjunto de datos comprimido y generación de los metadatos necesarios para los experimentos.

2. **Preprocesado de datos**  
   Normalización de nombres, unificación de imágenes y creación de archivos CSV para los conjuntos AMI, BIPLab, UERC y EICZA.

3. **Desarrollo del modelo base**  
   Definición de datasets, transformaciones, arquitectura de extracción de embeddings y funciones de evaluación.

4. **Experimentos base**  
   Entrenamiento y evaluación de modelos mediante clasificación con Cross-Entropy.

5. **Triplet Loss**  
   Entrenamiento mediante aprendizaje métrico usando tripletes.

6. **Ajuste de hiperparámetros**  
   Comparación de distintas configuraciones de margen, dimensión del embedding y tasa de aprendizaje.

7. **Comparación de backbones**  
   Evaluación de distintas arquitecturas convolucionales ligeras como ResNet18, MobileNetV2, MobileNetV3 y EfficientNet.

8. **Fusión simple de embeddings**  
   Combinación de embeddings generados por dos modelos distintos mediante concatenación y posterior normalización.

## Conjuntos de datos utilizados

El trabajo utiliza varios conjuntos de datos de oreja:

- **AMI**: imágenes de oreja de población adulta en condiciones relativamente controladas.
- **BIPLab**: conjunto adulto con imágenes de oreja y mayor variabilidad que AMI.
- **UERC**: conjunto adulto con imágenes más heterogéneas y condiciones menos controladas.
- **EICZA**: conjunto infantil utilizado para evaluar el escenario cross-age.

Tras el preprocesado, el notebook genera un archivo unificado de metadatos:

```text
metadata_unificado_final.csv
```

Este archivo se utiliza como entrada para los experimentos.

## Requisitos

Se recomienda ejecutar el proyecto en **Google Colab con GPU activada**, ya que los entrenamientos se realizan con PyTorch y modelos convolucionales preentrenados.

Para instalar las dependencias principales en un entorno local o en Colab, se puede usar:

```bash
pip install -r requirements.txt
```

En Google Colab, algunas librerías como `torch`, `torchvision`, `numpy`, `pandas` o `matplotlib` suelen venir instaladas por defecto, pero se incluyen igualmente en el archivo de requisitos para facilitar la reproducibilidad.

## Ejecución recomendada

1. Abrir el notebook en Google Colab.
2. Activar GPU desde:

```text
Entorno de ejecución > Cambiar tipo de entorno de ejecución > GPU
```

3. Ejecutar las celdas iniciales de importación y descarga de datos.
4. Ejecutar el apartado de preprocesado de datos.
5. Ejecutar el apartado de desarrollo del modelo.
6. Ejecutar el bloque experimental que se quiera reproducir.

También se puede ejecutar el notebook completo, aunque el tiempo de ejecución será mayor.

## Ejecución en Google Colab

El notebook está diseñado para ser completamente funcional por sí solo en Google Colab. Para reproducir el proyecto no es necesario preparar manualmente los datos antes de la ejecución, ya que las primeras celdas se encargan de descargar el archivo comprimido con los datos necesarios, descomprimirlo y generar la estructura de carpetas utilizada por el resto del código.

Por este motivo, la forma recomendada de ejecutar el proyecto es abrir el notebook `codigo_TFG_Rafael_Suárez.ipynb` en Google Colab, activar la GPU y ejecutar las celdas en orden. El propio notebook incluye las fases de descarga, preparación de datos, preprocesado, entrenamiento, evaluación y generación de resultados.

La estructura de datos mostrada en este README corresponde a la organización que se obtiene después de ejecutar las primeras celdas del notebook.

## Configuración de experimentos

Cada bloque experimental incluye una sección de configuración con parámetros como:

```python
TRAIN_DATASETS = ["AMI"]
TEST_DATASETS = ["EICZA"]
TRAIN_AGE_GROUP = "adulto"
TEST_AGE_GROUP = "niño"
BACKBONE_NAME = "resnet18"
IMG_SIZE = 224
BATCH_SIZE = 64
EPOCHS = 20
LR = 1e-4
EMBEDDING_DIM = 512
```

Modificando estos valores se pueden lanzar distintos experimentos sin cambiar el resto del código.

## Resultados generados

Durante la ejecución del notebook, los resultados de cada experimento se almacenan en la carpeta `runs/`. Dentro de esta carpeta se guardan, según el experimento ejecutado:

- Modelos entrenados en formato `.pt`.
- Métricas de entrenamiento, validación y test.
- Puntos de las curvas ROC.
- Curvas CMC.
- Gráficas comparativas.
- Archivos CSV con resultados individuales y comparativos.

Además, el archivo `all_experiments_results.csv` recoge un resumen global de los experimentos realizados, incluyendo métricas como ROC-AUC, EER, Rank-1 y Rank-5.

En este repositorio se incluye también la carpeta `results/`, donde se muestran algunos resultados obtenidos en varios de los experimentos realizados. Estos archivos sirven como ejemplo de las salidas esperadas al ejecutar el notebook.

## Métricas utilizadas

El sistema se evalúa mediante métricas propias de reconocimiento biométrico:

- **ROC-AUC**: mide la capacidad de separación entre pares genuinos e impostores.
- **EER**: punto en el que la tasa de falsos aceptados y falsos rechazados se igualan. Cuanto menor sea, mejor.
- **Rank-1**: porcentaje de casos en los que la identidad correcta aparece en la primera posición.
- **Rank-5**: porcentaje de casos en los que la identidad correcta aparece entre las cinco primeras posiciones.

## Estructura esperada de datos

Tras descargar y descomprimir los datos, se espera una estructura similar a:

```text
Datos_TFG_Rafael/
├── AMI/
├── BIPLab/
├── UERC/
└── dataset_EICZA/
```

Durante el preprocesado se generan carpetas auxiliares como:

```text
images/
individual_metadata/
```

Estas carpetas contienen las imágenes copiadas con nombres normalizados y los metadatos individuales de cada conjunto de datos.

## Modelos utilizados

El código permite trabajar con distintos backbones preentrenados de `torchvision`, entre ellos:

- ResNet18
- ResNet50
- MobileNetV2
- MobileNetV3 Small
- MobileNetV3 Large
- EfficientNet-B0
- EfficientNet-B1
- DenseNet121

En el trabajo se priorizan modelos relativamente ligeros, adecuados para un estudio experimental con recursos limitados y más cercanos a posibles escenarios de despliegue.

## Nota sobre reproducibilidad

El notebook fija una semilla aleatoria para reducir la variabilidad entre ejecuciones:

```python
SEED = 42
```

Aun así, al trabajar con GPU, librerías de Deep Learning y modelos preentrenados, pueden existir pequeñas diferencias entre ejecuciones, especialmente si cambia el entorno, la versión de CUDA o la versión de PyTorch.

## Autor

**Rafael Suárez Saavedra**  
Grado en Ciencia e Ingeniería de Datos  
Universidad de Las Palmas de Gran Canaria
