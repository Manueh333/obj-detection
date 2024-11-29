Para poder entrenar una red neuronal, debemos tener antes un dataset, un conjunto de datos con los que poder enseñar al modelo lo que queremos que detecte.

En el caso de detección de objetos los datos que vamos a necesitar son imágenes con sus correspondientes etiquetas. En las etiquetas vienen definidos los píxeles a los que pertenece el objeto u objetos que aparecen en las imágenes.

Hay varios tipos de etiquetas pero vamos ha desarrollar únicamente dos:
- [[Creación de un Dataset#Object Detection|| Object Detection (Detección de objetos)]]
- [[Creación de un Dataset#Instance Segmentation|| Instance Segmentation (Segmentación de instancias)]]
A su vez también existen varios formatos en los que se pueden escribir estas etiquetas, pero nos centraremos únicamente en los formatos [COCO](https://cocodataset.org/) y en el formato de YOLO

Estos tipos de anotación nos permiten crear etiquetas para los dos tipos que vamos a ver.
# Object Detection
La detección de objetos es una tarea que implica detectar la posición y la clase de los objetos que aparezcan en una imagen.![[elefante_od.png]]

Las etiquetas necesarias para Object Detection son los rectángulos que incluyen al objeto en su interior estos se definen normalmente por su esquina, altura y anchura.
```json title=Elefante.json
"annotations": [{ 
	"id": 1, 
	"image_id": 1, 
	"category_id": 1, 
	// Aquí es donde ponemos la esquina y su altura y anchura en el formato
	// [x_min, y_min, width, height]
	"bbox": [100, 200, 300, 400], 
	// Y aquí el area (width * height)
	"area": 120000, 
	"segmentation": [], 
	"iscrowd": 0 
	}]
```
# Instance Segmentation
 La segmentación de instancias va un pasa más lejos y en vez de dar solo la posición y clase también se detecta la silueta del objeto.

![[elefante_id.png]]
```json title=Elefante.json
"annotations": [{ 
	"id": 1, 
	"image_id": 1, 
	"category_id": 1, 
	"bbox": [100, 200, 300, 400], 
	"area": 120000, 
	// La segmentación se pone como el conjunto de puntos del poligono que
	// envuelve al objeto [x1, y1, x2, y2, ..., xn, yn]
	"segmentation": [[410, 510, 450, 530, 480, 640, 420, 650]], 
	"iscrowd": 0 
	}]
```

Obviamente, no vamos a etiquetar las imágenes picando código, para ello existen aplicaciones que nos facilitan el trabajo, os voy a hablar sobre dos:
- [[Creación de un Dataset#LabelStudio|LabelStudio]]
- [[Creación de un Dataset#Roboflow|Roboflow]]
# [LabelStudio](https://labelstud.io)
LabelStudio es una herramienta que debemos ejecutar localmente en nuestro ordenador con python.

Para ello debemos instalar el paquete de LabelStudio con pip
```pip
pip install label-studio
```

Y después ejecutarlo con el comando
```pip
label-studio
```

Para interactuar con la aplicación debemos entrar en [http://localhost:8080](http://localhost:8080)

Nos registramos y creamos un proyecto:
Le ponemos nombre, importamos las imágenes a etiquetar y seleccionamos el tipo de etiquetación que deseemos. Para comenzar podemos probar Object Detection with Bounding Boxes. Añadimos las clases que vayamos a utilizar, y comenzamos a anotar.

Para ello seleccionamos la imagen a anotar y luego procedemos a seleccionar la clase en cuestión, y pinchamos en una esquina donde queremos poner el rectángulo y luego movemos  el ratón y volvemos a pinchar en la otra esquina.

Luego al finalizar de anotar podemos exportar el dataset con el botón exportar y elegimos entre COCO o YOLOv8
# Roboflow
Roboflow es una herramienta online que nos permite etiquetar, dividir y exportar nuestro dataset.

