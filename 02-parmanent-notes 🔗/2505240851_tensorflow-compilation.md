## Compiled ANN Models

Either we are training or just executing an ANN all that calculations are performed after a compilation step of the model.

### Tags

#programming #ai  #machine_learning #neural_networks #permanent

---

## Compiled Functions

In the context of TensorFlow and more specifically graph execution, compiled functions are a mechanism to translate python code into neural networks graphs.

In mathematics, graphs are a form of representation of both data (encoded as tensors) and operations against the first; but in the context of machine learning and TensorFlow, they also allow us to perform very efficient computation.

The compilation step reduces all python's overhead by executing directly native code in the hardware devices (CPU or the best case GPU/s,  TPU/s).

The python interface of TensorFlow provides the `tf.function` decorator to compile python logic into graphs to be executed by the TensorFlow's engine.

```python
import tensoflow as tf

@tf.function
def train_step(batch_data):
    # your tensorflow code here
```