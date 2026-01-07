# TensorFlow/Keras Reference Guide

Complete reference for TensorFlow and Keras - deep learning framework.

---

## Installation and Import

### Installation
```bash
pip install tensorflow
```

### Import
```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers
```

---

## Building Models

### Sequential API (Simple)

**Description:** Linear stack of layers  
**Use:** Simple models with one input and one output

```python
model = keras.Sequential([
    layers.Dense(64, activation='relu', input_shape=(input_dim,)),
    layers.Dense(32, activation='relu'),
    layers.Dense(1, activation='sigmoid')
])
```

### Functional API (Flexible)

**Description:** More flexible, allows complex architectures  
**Use:** Multi-input/output models, shared layers

```python
inputs = keras.Input(shape=(input_dim,))
x = layers.Dense(64, activation='relu')(inputs)
x = layers.Dense(32, activation='relu')(x)
outputs = layers.Dense(1, activation='sigmoid')(x)

model = keras.Model(inputs=inputs, outputs=outputs)
```

---

## Common Layers

### `layers.Dense()`
**Description:** Fully connected layer  
**Syntax:** `layers.Dense(units, activation=None)`

```python
layers.Dense(64, activation='relu')
layers.Dense(10, activation='softmax')  # For multi-class classification
```

### `layers.Dropout()`
**Description:** Randomly drop units to prevent overfitting  
**Syntax:** `layers.Dropout(rate)`

```python
layers.Dropout(0.5)  # Drop 50% of units
layers.Dropout(0.3)  # Drop 30% of units
```

### `layers.BatchNormalization()`
**Description:** Normalize layer inputs  
**Syntax:** `layers.BatchNormalization()`

```python
layers.BatchNormalization()
```

### `layers.Flatten()`
**Description:** Flatten input to 1D  
**Syntax:** `layers.Flatten()`

```python
layers.Flatten()  # Convert 2D/3D to 1D
```

---

## Convolutional Layers (for Images)

### `layers.Conv2D()`
**Description:** 2D convolution layer  
**Syntax:** `layers.Conv2D(filters, kernel_size, activation=None)`

```python
layers.Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1))
layers.Conv2D(64, (3, 3), activation='relu')
```

### `layers.MaxPooling2D()`
**Description:** Max pooling operation  
**Syntax:** `layers.MaxPooling2D(pool_size=(2, 2))`

```python
layers.MaxPooling2D((2, 2))
```

### `layers.AveragePooling2D()`
**Description:** Average pooling operation  
**Syntax:** `layers.AveragePooling2D(pool_size=(2, 2))`

```python
layers.AveragePooling2D((2, 2))
```

---

## Recurrent Layers (for Sequences)

### `layers.LSTM()`
**Description:** Long Short-Term Memory layer  
**Syntax:** `layers.LSTM(units, return_sequences=False)`

```python
layers.LSTM(50, return_sequences=True)  # Return full sequence
layers.LSTM(50)  # Return only last output
```

### `layers.GRU()`
**Description:** Gated Recurrent Unit layer  
**Syntax:** `layers.GRU(units, return_sequences=False)`

```python
layers.GRU(50, return_sequences=True)
```

### `layers.SimpleRNN()`
**Description:** Simple recurrent layer  
**Syntax:** `layers.SimpleRNN(units)`

```python
layers.SimpleRNN(50)
```

---

## Compiling Models

### `model.compile()`
**Description:** Configure model for training  
**Syntax:** `model.compile(optimizer, loss, metrics)`

```python
# Binary classification
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)

# Multi-class classification
model.compile(
    optimizer='adam',
    loss='categorical_crossentropy',  # or 'sparse_categorical_crossentropy'
    metrics=['accuracy']
)

# Regression
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)

# Custom learning rate
model.compile(
    optimizer=keras.optimizers.Adam(learning_rate=0.001),
    loss='mse'
)
```

---

## Training Models

### `model.fit()`
**Description:** Train the model  
**Syntax:** `model.fit(x, y, epochs, batch_size, validation_split)`

```python
# Basic training
history = model.fit(X_train, y_train, epochs=50, batch_size=32)

# With validation split
history = model.fit(
    X_train, y_train,
    epochs=50,
    batch_size=32,
    validation_split=0.2
)

# With separate validation data
history = model.fit(
    X_train, y_train,
    epochs=50,
    batch_size=32,
    validation_data=(X_val, y_val),
    verbose=1
)
```

---

## Callbacks

### `EarlyStopping`
**Description:** Stop training when metric stops improving  
**Syntax:** `keras.callbacks.EarlyStopping(monitor, patience)`

```python
early_stop = keras.callbacks.EarlyStopping(
    monitor='val_loss',
    patience=5,
    restore_best_weights=True
)

model.fit(X_train, y_train, epochs=100, callbacks=[early_stop])
```

### `ModelCheckpoint`
**Description:** Save model during training  
**Syntax:** `keras.callbacks.ModelCheckpoint(filepath, monitor, save_best_only)`

```python
checkpoint = keras.callbacks.ModelCheckpoint(
    'best_model.h5',
    monitor='val_loss',
    save_best_only=True,
    verbose=1
)

model.fit(X_train, y_train, epochs=100, callbacks=[checkpoint])
```

### `ReduceLROnPlateau`
**Description:** Reduce learning rate when metric plateaus  
**Syntax:** `keras.callbacks.ReduceLROnPlateau(monitor, factor, patience)`

```python
reduce_lr = keras.callbacks.ReduceLROnPlateau(
    monitor='val_loss',
    factor=0.5,
    patience=3,
    min_lr=0.00001
)

model.fit(X_train, y_train, epochs=100, callbacks=[reduce_lr])
```

---

## Prediction and Evaluation

### `model.predict()`
**Description:** Generate predictions  
**Syntax:** `model.predict(x)`

```python
predictions = model.predict(X_test)

# For classification, get class labels
predicted_classes = (predictions > 0.5).astype(int)  # Binary
predicted_classes = np.argmax(predictions, axis=1)   # Multi-class
```

### `model.evaluate()`
**Description:** Evaluate model on test data  
**Syntax:** `model.evaluate(x, y)`

```python
loss, accuracy = model.evaluate(X_test, y_test)
print(f"Test Loss: {loss}")
print(f"Test Accuracy: {accuracy}")
```

---

## Model Inspection

### `model.summary()`
**Description:** Print model architecture  
**Syntax:** `model.summary()`

```python
model.summary()
```

### Get Weights

```python
# Get all weights
weights = model.get_weights()

# Get layer weights
layer_weights = model.layers[0].get_weights()
```

---

## Saving and Loading Models

### Save Entire Model

```python
# Save
model.save('my_model.h5')
model.save('my_model')  # SavedModel format

# Load
loaded_model = keras.models.load_model('my_model.h5')
```

### Save Only Weights

```python
# Save weights
model.save_weights('model_weights.h5')

# Load weights
model.load_weights('model_weights.h5')
```

---

## Data Augmentation (for Images)

### `ImageDataGenerator`
**Description:** Generate batches of augmented image data  
**Syntax:** `keras.preprocessing.image.ImageDataGenerator(**kwargs)`

```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

datagen = ImageDataGenerator(
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    horizontal_flip=True,
    zoom_range=0.2,
    fill_mode='nearest'
)

# Fit on training data
datagen.fit(X_train)

# Train with augmented data
model.fit(
    datagen.flow(X_train, y_train, batch_size=32),
    epochs=50
)
```

---

## Common Activation Functions

```python
# ReLU (most common for hidden layers)
layers.Dense(64, activation='relu')

# Sigmoid (binary classification output)
layers.Dense(1, activation='sigmoid')

# Softmax (multi-class classification output)
layers.Dense(10, activation='softmax')

# Tanh
layers.Dense(64, activation='tanh')

# Linear (regression output)
layers.Dense(1, activation='linear')  # or activation=None
```

---

## Loss Functions

```python
# Binary classification
loss='binary_crossentropy'

# Multi-class classification (one-hot encoded)
loss='categorical_crossentropy'

# Multi-class classification (integer labels)
loss='sparse_categorical_crossentropy'

# Regression
loss='mse'  # Mean Squared Error
loss='mae'  # Mean Absolute Error
```

---

## Optimizers

```python
# Adam (most common)
optimizer='adam'
optimizer=keras.optimizers.Adam(learning_rate=0.001)

# SGD
optimizer='sgd'
optimizer=keras.optimizers.SGD(learning_rate=0.01, momentum=0.9)

# RMSprop
optimizer='rmsprop'

# Adagrad
optimizer='adagrad'
```

---

## Example: Complete CNN for Image Classification

```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers

# Build model
model = keras.Sequential([
    layers.Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)),
    layers.MaxPooling2D((2, 2)),
    layers.Conv2D(64, (3, 3), activation='relu'),
    layers.MaxPooling2D((2, 2)),
    layers.Conv2D(64, (3, 3), activation='relu'),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dropout(0.5),
    layers.Dense(10, activation='softmax')
])

# Compile
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# Train
history = model.fit(
    X_train, y_train,
    epochs=10,
    batch_size=32,
    validation_split=0.2
)

# Evaluate
test_loss, test_acc = model.evaluate(X_test, y_test)
print(f"Test accuracy: {test_acc}")

# Predict
predictions = model.predict(X_test)
```

---

**Back to the Topic:** [Libraries & Tools](3_Libraries_and_Tools.md)
