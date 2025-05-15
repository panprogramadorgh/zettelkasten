# Keras Data Loading Guide

Keras  data loading utilities, which are located in `tf.keras.utils`, help you go from raw data stored in disk to useful `tf.keras.Database` instances, that can be used to train efficiently a model.

These loading utilities can be combined with preprocessing layers to further transform you input dataset before training.

### Tags

#programming #ia #machine_learning #neural_networks #image_processing #literature

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

Next we will take a look at an example of machine learning classification problem where we have to load images labeled under specific names in order to train a model.

### Sources
- [Official TensorFlow's Docs Regarding to Datasets](https://www.tensorflow.org/api_docs/python/tf/data/Dataset)