# Step Fusing

Step Fusing is a training optimization technique employed in the context of Artificial Neural Networks models,  being one of its benefits not to change training semantics (avoiding to tune other training parameters).
### Tags

#programming #ia #machine_learning #neural_networks #literature

---
### Hint

In order to have a better understanding about how this optimization method works, I truly recommend to read [[2505131212_gradient-descent-brief]] and see all its variants.
## ML Compiled Functions and Graphs

In fact, either we are training or just executing a ANN model all that calculations are performed with a compiled function.

A compiled function is in charge of executing very fast operations with graphs, which are a mathematical way of representing both data (or tensors) and operations. The compilation step reduces all python's overhead by executing directly native code in the hardware devices (CPU or the best case GPU/s,  TPU/s).

###  TensorFlow use case

TensorFlow (an open-source ml library developed by google, also see [[2505051014_tensorflow-brief]]) allows the compilation of functions — mathematical graphs in native code to run on devices, by using the `tf.function` decorator.

```python
import tensoflow as tf

@tf.function
def train_step(batch_data):
    # Forward pass
    # Loss computation
    # Backward pass (compute gradients)
    # Optimizer step
```

> Pseudocode which illustrates how to compile a function in TensorFlow.

## Calling Overhead

Although we are getting rid of all python's overhead by applying this compilation step, we have another problem.

Imagine for a second we are training a model with a training compilation function and each of the epochs (iteration in training loop) have 10.000 batches — the calculation of real gradient descent is computationally impossible now a days.

Each time we call the training function we are performing:
1. **Forward pass** (creating predictions with the ANN)
2. **Calculation of loss** (by comparing the predictions with the real labels if we are talking about of an unsupervised learning approach)
3. **Backward pass** (calculate the gradients)
4. **Optimizer step** (update the graph by applying the gradients to each of the weights)

For each epoch in the training process we would need to call 10.000 times the compiled training function, which leads to overhead due the number of calls (even if the function itself is fully optimized, the calling process is inefficient).

What Step Fusing does is to minimize the number of calls to the compiled function while keeping the exact same number of batches to process per each epoch and not modifying the semantics or other training parameters at all.
### Sources

- `ChatGPT`