
YOLO (You Only Look Once) es un modelo de detección de objetos, en este caso vamos a utilizar la version 11 en su formato nano, pero existen otros formatos (n, s, m, l, x) a su vez también cuenta con distintas versiones para detección de objetos, segmentación de instancias, detección de pose, etc.

La empresa Ultralytics es la que esta actualizando YOLO, para más información sobre los distintos modelos de YOLO pincha [aquí](https://docs.ultralytics.com/models/yolo11/) 

# Entrenamiento de YOLO

Para entrenar a YOLO vamos a utilizar la API de Ultralytics

Para ellos debemos instalarla en un entorno de Python:
```pip 
pip install ultralytics
```

Antes de entrenar al modelo necesitamos un dataset, para crear uno revise el capitulo [[Creación de un Dataset]]

Una vez tengamos el dataset usaremos este código para entrenar al modelo.
```python title=train.py
# Importamos la libreria de Ultralytics
from Ultralytics import YOLO

# Importamos el modelo que vamos a utilizar (por defecto)
model = YOLO("yolo11-n.pt") 

# Entrenamos el modelo con el dataset creado anteriormente
results = model.train(data="/path/to/data.yaml", epochs="100") 
```

Puede informarse sobre los parámetros que pueden usarse en model.train() pinchado [aquí](https://docs.ultralytics.com/modes/train/#train-settings)

