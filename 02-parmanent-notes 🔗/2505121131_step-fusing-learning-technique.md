# Step Fusing

Step Fusing is a training optimization technique employed in the context of Artificial Neural Networks models,  being one of its benefits not to change training semantics (avoiding to tune other training parameters).
### Tags

#programming #ai #machine_learning #neural_networks #permanent

---
### References

In order to have a better understanding about how this optimization method works, I truly recommend to read:
- [[2505131212_gradient-descent-ml-optimizer]]
- [[2505240851_tensorflow-compilation]]

## Calling Overhead

Although we are getting rid of all python's overhead by applying this compilation step, we have another problem.

Imagine for a second we are training a model with a training compilation function and each of the epochs (iteration in training loop) has 10.000 batches — the calculation of real gradient descent is computationally impossible now a days.

Each time we call the training function we are performing:
1. **Forward pass** (creating predictions with the ANN)
2. **Calculation of loss** (by comparing the predictions with the real labels if we are talking about of an unsupervised learning approach)
3. **Backward pass** (calculate the gradients)
4. **Optimizer step** (update the graph by applying the gradients to each of the weights)

For each epoch in the training process we would need to call 10.000 times the compiled training function, which leads to overhead due to the number of calls (even if the function itself is fully optimized, the calling process is inefficient).

What step fusing does consists on minimizing the number of calls to the compiled function (the compiled function process multiple batches) while keeping the exact same number of batches to process per each epoch while not modifying the semantics or any training parameters at all.
### Sources

- `ChatGPT`