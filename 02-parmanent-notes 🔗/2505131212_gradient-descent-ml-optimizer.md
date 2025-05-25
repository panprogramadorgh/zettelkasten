# Gradient Descent

Gradient descent (an optimization algorithm) is one of the key components in backward pass when training an ANN model. It's in charge taking the gradients calculated by backward pass, reverse their direction and update the network's weights. It doesn't update the weights, it just computes the required partial derivates.

### Tags

#ai #machine_learning #neural_networks #permanent

---

### Aside

It's important to note that backward pass doesn't necessarily need to be implemented with an optimization algorithm based on gradient descent — although lots of them are based on it.

## Variants

Calculate the average loss for all network's parameters and thus compute gradients, specially with big networks, is a computationally expensive task; this is the reason why we have three main variants for gradient descent optimizers, requiring each of which different system capabilities.

1. **Batch Gradient Descent** — Is considered as the standard version of gradient descent. After a forward pass over the network, backward pass takes all the losses for each parameter, calculates the gradients and finally this _GD_ variant updates the weights. This variant is the most effective if we are talking about a problem where the opposite direction of the gradients for each parameter directly points to the global minimum, that is, there aren't misleading curves

2. **Stochastic Gradient Descent** — Is a lightweight and much less accurate version of the classical gradient descent optimizer which updates all the network's parameters by calculating an individual loss for randomly-chosen weight per iteration in the training loop. May be worth it in problems with a high rate of noise (not clear curves that leads to the global minimum) or when we don't have much data to train with.

3. **Mini-Batch Gradient Descent** — Consists of a combination of the two previous approaches where we take a constant number of network's parameters — what we formally call a batch; backward pass calculates the average loss for them and finally this _GD_ variant updates the network's weights.

> It's important to note that in the last _GD_ variants, we update all the weights in the network architecture, not only those that did belong to the batch. Batches are just the reference point from which we calculate the gradients, but we have to update the entire network.

### Sources

- `CS50's Lecture 5`

- `ChatGPT`