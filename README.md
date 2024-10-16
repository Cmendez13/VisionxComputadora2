# VisionxComputadora2

Carlos Méndez

Carlos Villalobos

En este repositorio se encuentra el trabajo práctico realizado para la asignatura de Visión por Computadora 2.

El dataset seleccionado para este trabajo fue el siguiente:

<mark> https://www.kaggle.com/datasets/prasunroy/natural-images </mark>

Este dataset contiene 6,899 imagenes de 8 distintas clases (que proviene de distintas fuentes). 

Las clases incluidas en el mencionado dataset son: airplane, car, cat, dog, flower, fruit, motorbike, person.


<img src=/images/muestra_imagenes.png alt="Muestra" width="300" height="300">
<li> Dimensiones heterogeneas</li> 

Luego de inspeccionar la data se pudo evidenciar que la dimensión de las imagenes eran bastante dispares entre clases.

<img src=/images/scatterplot_dimensiones.png alt="Scatter Dimensiones" width="300" height="300">

<li> Desbalanceo de clases</li> 

```
# Cargar el dataset
dataset = torchvision.datasets.ImageFolder(root=root_path)

# Verificar la distribución de las clases
class_counts = torch.bincount(torch.tensor(dataset.targets))
print(f'Distribución original de clases: {class_counts}')

```

Distribución original de clases: tensor([ 727,  968,  885,  702,  843, 1000,  788,  986])

<h1> El problema </h1>

El problema a resolver es un problema de clasificación. 

Para ello hubo considerar algunos puntos para la resolución


> [!NOTE]
> Resize de las imagenes para homegeneizar las dimensiones de las imagenes
> 
> Balanceo entre clases usando técnicas de RandomSampler (en particular **WeightedRandomSampler** - from torch.utils.data)
>
> Se realizaron algunas transformaciones para mejorar el desempeño del modelo y aumentar la data

Para la implementación asociada se planteo una arquitectura de red convolucional

<h1>Definición de la red convolucional</h1>

Se planteo una red con la siguiente arquitectura con cuatro capas de convolución:

<img src=/images/arquitectura.png alt="Muestra" width="208" height="692">

<h1> Puntos de mejora </h1>

<li> Un posible punto de mejora refiere a considerar el tamaño de la imagen en el resize como un hiperparámetro, para nuestro caso realizamos varias pruebas [(224, 224), (256,256), (300, 300)]   </li>


Estas selecciones fueron hechas teniendo en cuenta el costo computacional, sin embargo, parecia razonable evaluar un criterio más estadístico (Un histograma del promedio de pixels o la distribución promedio de las imagenes como criterio).

<li> Optimización del uso de las transformaciones de Pytorch</li>


Inicialmente no se hicieron transformaciones y luego se fueron agregando algunas lo que se tradujo en mejoras en el **accuracy**.  Agregar otro tipo de transformaciones puede ser testeadas.

<li> Mayor profundidad a la red </li>


<h1> Transfer Learning </h1>

Se realizó una prueba con arquitectura pre-entrenada - **resnet** - donde se evidenciaron mejores resultados

La selección de la arquitectura se erige como un punto de especial atención para la solución de problemas de **clasificación**.









