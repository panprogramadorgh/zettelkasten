# TensorFlow Keras Callbacks

The keras interface from TensorFlow includes a submodule call as this note (`tf.keras.callbacks`). It is in charge of allowing interface consumers define callback utilities in order to customize and control the process of training a model with keras (callbacks acts like hooks).

Callbacks are associated to certain events when training a model (like the beginning or end of an epoch or batch) and by using of them we can trigger actions.

### Tags

#programming #ai #neural_networks #machine_learning #python #tensorflow #permanent 

---

## Built-in Callbacks

Keras already brings you some callbacks with some predefined behavior (which may be parametrized), avoiding you to create a subclass of `tf.keras.callbacks.Callback` (which is what you should do in order to create your own callbacks).

Here are some common callbacks and their use case:

1. `EarlyStopping` — Stop training when some metric has stopped to improve (validation loss) and avoid overfitting.

2. `ModelCheckpoint` — Allow saving the model or its weights sporadically or if some metric has improved significantly if training is interrupted.

3. `ReduceLROnPlateau` — Reduce model's learning rate when a metric has stopped to improve, helping with plateau stages.

4. `TensorBoard` — Visualize loss and accuracy metrics during training (supports debugging and model performance tracking)

```python
from tensorflow.keras.callbacks import EarlyStopping

early_stop = EarlyStopping(monitor='val_loss', patience=3)

model.fit(X_train, y_train, epochs=50, validation_split=0.2, callbacks=[early_stop])

```

> Python example of `tf.keras.callbacks` interface to track validation loss and consequently interrupt model's training.

### Sources

- `ChatGPT`
