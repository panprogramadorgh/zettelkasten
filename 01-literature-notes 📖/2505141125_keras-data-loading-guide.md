# Keras Data Loading Guide

Keras  data loading utilities, which are located in `tf.keras.utils`, help you go from raw data stored in disk to useful `tf.keras.Database` instances, that can be used to train efficiently a model.

These loading utilities can be combined with preprocessing layers to further transform you input dataset before training.

### Tags

#programming #ai #machine_learning #neural_networks #image_processing #literature

---
## Meaning of Tensor

A tensor is a multidimensional data structure that stores numerical values. 

- **First order tensors** (with $0$ dimensions) — Also known as `Scalar`	
	For instance: `5`

- **First dimension tensors** (x) — Called `Vectors`
	A list of numbers:
	`[1, 2, 3]`

- **Second dimension tensors** (x * y) — What we call `Matrix`
	A 2D board that shape a grayscale image:
	`[[255, 100, 0], [0, 20, 255], [0, 100, 50]]`

- **Third or more dimensions Tensors** (x * y * z * ...) — Multidimensional Tensors
	A regular image that contains three different channels (red, green and blue):
	`[[[255, 255, 0], [255, 220, 0], [200, 100, 50]], [[255, 255, 0], [255, 220, 0], [200, 100, 50]], [[255, 255, 0], [255, 220, 0], [200, 100, 50]]]`

## Meaning of Graph

A graph is a mathematical representation of nodes and their relationships, that, in the context of GNNs (graphs neural networks) can be represented by tensors.

For instance we may have an artificial neural network with $128$ different nodes and each of those could contain, in turn, a feature map of $64$ numerical elements.

Programming libraries such us `TensorFlow` or `PyTorch` optimizes and eases the creation of GNNs through the use of tensors and mathematical operations regarding to them — that can be run on devices (GPUs, TPUs or just generalists CPUs).

![graphs-explanation-context-anns.excalidraw](graphs-explanation-context-anns.excalidraw.png)

## TensorFlow `tf.data.Dataset` Tool

TensorFlow offers a general-purpose, scalable and composable tool to represent input data in a streaming fashion way — which may be used to represent the initial data in the program, apply transformations to it and finally be part of the training for some model.

As mentioned before, this tool works in a streaming fashion way, which means the entire dataset isn't completely loaded in memory at the same time; instead, data only iterates.

### Common Terms

1. **Element** — A single output from calling next() on a dataset iterator. Elements may contains nested structures. For example, the element `(1, (3, "watermelon 🍉"))` has a nested element (which is a tuple) and three different components: `1, 3 and "watermelon 🍉"`.

2. **Components** — The leaf in the nested structure of an element.

3.  **Supported Types** — Elements may be compound of nested tuples, named tuples and dictionaries. In the other hand, lists aren't trat as nested elements but rather as components. Components can be of any type representable by `tf.TypeSpec`:

- `tf.Tensor` (the main object that is manipulated and passed around)
- `tf.data.Dataset`
- `tf.sparse.SparseTensor`
- `tf.RaggedTensor`
- `tf.TensorArray`

```python
a = 1 # Integer element
b = 2.0 # Float element
c = (1, 2) # Tuple element with 2 components
d = {"a": (2, 2), "b": 3} # Dict element with 3 components
Point = collections.namedtuple("Point", ["x", "y"])
e = Point(1, 2) # Named tuple
f = tf.data.Dataset.range(10) # Dataset element
```

## Brief Introduction Example

Lets take a look at an introduction example of TensorFlow's input data utilities, specifically we will be working with images.

> Since TensorFlow works with `pillow` under the hood, the supported images format are: `jpeg, jpg, png, bpm and gif`.

In this example we will process and categorize images under different class names. The images format will be `.jpg` (but might be any of above) and the class associated to each image will be given based on the files structure described next.

- First of all we will have a directory called `training_ds`, which will be the main directory in the training input dataset, in the other hand

- `training_ds` will contain multiple subdirectories, each of which associated with different classes, finally

- Each subdirectory will contain a whole bunch of images related with its class name.

The files structure should look like follows:

```
training_ds/
..class_a/
....a_00.jpg
....a_01.jpg
..class_b/
....b_00.jpg
....b_01.jpg
```

Fortunately, TensorFlow Keras offers a built-in function to create a `tf.data.Dataset`  labeling images under class names though a files structure like above. It is called `keras.utils.image_dataset_from_directory` — for further details read the [official docs regarding to this routine](https://keras.io/api/data_loading/image/#image_dataset_from_directory-function).

This function actually takes a lot of arguments, but in the case we will cover some of them:
- `directory` — Specifies the path for the very parent directory (the one that wraps the entire training images dataset)

- `labels` — Gives name to the training images dataset classes. Although  we can pass the value "inferred" to let the internal implementation automatically read the subdirectories and know what classes will the training dataset have.

- `label_mode` — It completely depends on the loss function we will use, and thus it depends on the kind of problem. In this particular case we will use "categorical", since our neural network is pretended to return discrete values that regards to this class names.

- `batch_size` — The number of units we will use to calculate the gradients and avoid local minimums when training an ANN model.

- `image_size`  — The shape of a second dimension board that contains the `height` and `width` of the images that belongs to the dataset. Note that the images will have three different channels (reed, green and blue) but we will not specify that here.

```python
import keras

dataset = keras.utils.image_dataset_from_directory(

  directory=DIR,

  label="inferred",

  label_mode="categorical",

  batch_size=64,

  image_size=(256, 256)

)
```


## Load Images

... next we will explain how to load images in ppm format

### Sources
- [Official TensorFlow's Docs Regarding to Datasets](https://www.tensorflow.org/api_docs/python/tf/data/Dataset)