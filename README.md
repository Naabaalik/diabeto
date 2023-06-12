#### Session 2 - Binary Classification
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import tensorflow as tf

## Split into training and testing

from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test=train_test_split(X,y,
                                  test_size=0.2,random_state=100)
X_train.shape,X_test.shape,y_train.shape,y_test.shape

## Building the model

model_1=tf.keras.Sequential()
model_1.add(tf.keras.layers.Dense(8,activation='relu')) ## Adding a layer
model_1.add(tf.keras.layers.Dense(1,activation='sigmoid'))  ## Adding another layer

## Compiling the model

model_1.compile(optimizer=tf.keras.optimizers.Adam(),
                loss=tf.keras.losses.BinaryCrossentropy(),
                metrics=['accuracy'])

## Model Training

tf.random.set_seed(100)
history=model_1.fit(X_train,y_train,epochs=50)
hist=pd.DataFrame(history.history)
hist.plot();

## Summary of the model

model_1.summary()

## Predictions

model_1.predict(X_test)

##### Session 3 – Feed Forward Neural Network


### Standardization

from sklearn.preprocessing import StandardScaler

sc=StandardScaler()

X_scaled=sc.fit_transform(X)
X_scaled


### Splitting
from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test=train_test_split(X_scaled,
                      y, test_size=0.2, random_state=100)


X_train.shape,X_test.shape,y_train.shape,y_test.shape


### Model building
model_1=tf.keras.Sequential()
model_1.add(tf.keras.layers.Dense(20,activation='relu'))
model_1.add(tf.keras.layers.Dense(1))

### Compiling the model

model_1.compile(optimizer=tf.keras.optimizers.Adam(),
                loss=tf.keras.losses.MeanSquaredError(),
                metrics=['mae'])


### Training the model

tf.random.set_seed(100)
history=model_1.fit(X_train,y_train,epochs=100)
hist=pd.DataFrame(history.history)
hist.plot();

### Model Summary

model_1.summary()

### Model Evaulation

test_mse,test_mae=model_1.evaluate(X_test,y_test)
print('Test MSE:',test_mse)
print('Test MAE:', test_mae)

### Prediction using the model

y_pred=model_1.predict(X_test)
print('The predicted house prices:\n',y_pred)

y_test


## Session 4 – Multi-Class Classification
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import tensorflow as tf

### Building the model

fashion_1=tf.keras.Sequential()
fashion_1.add(tf.keras.layers.Flatten())
fashion_1.add(tf.keras.layers.Dense(300,activation='relu'))
fashion_1.add(tf.keras.layers.Dense(10,activation='softmax'))

### Compiling the model

fashion_1.compile(loss=tf.keras.losses.SparseCategoricalCrossentropy(),
                  optimizer=tf.keras.optimizers.Adam(),
                  metrics=['accuracy'])

### Training the model

tf.random.set_seed(100)
history_1=fashion_1.fit(X_train,y_train,epochs=25)
pd.DataFrame(history_1.history).plot();

### Evaluation of the model

test_loss,test_accuracy=fashion_1.evaluate(X_test,y_test)

print('The Test Loss:',test_loss)
print('The Test Accuracy:',test_accuracy)

### Improving the model by adding one more layer
fashion_2=tf.keras.Sequential()
fashion_2.add(tf.keras.layers.Flatten()) --- use this only when data has images. Else, remove this line
fashion_2.add(tf.keras.layers.Dense(300,activation='relu'))

fashion_2.add(tf.keras.layers.Dense(100,activation='relu'))## Adding a layer of 100 units

fashion_2.add(tf.keras.layers.Dense(10,activation='softmax'))


### Compiling the model again

fashion_2.compile(loss=tf.keras.losses.SparseCategoricalCrossentropy(),
                  optimizer=tf.keras.optimizers.Adam(),
                  metrics=['accuracy'])

tf.random.set_seed(100)
history_2=fashion_2.fit(X_train,y_train,epochs=25)
pd.DataFrame(history_2.history).plot();

### Evaluating the model

test_loss,test_accuracy=fashion_2.evaluate(X_test,y_test)

print('Test Loss:',test_loss)

print('Test accuracy:',test_accuracy)

### Improving the model by adding another hidden layer

fashion_3=tf.keras.Sequential()
fashion_3.add(tf.keras.layers.Flatten())
fashion_3.add(tf.keras.layers.Dense(300,activation='relu'))
fashion_3.add(tf.keras.layers.Dense(100,activation='relu'))## Adding a layer of 100 units

# Adding a layer of 25 units
fashion_3.add(tf.keras.layers.Dense(25,activation='relu'))## Adding a layer of 100 units

fashion_3.add(tf.keras.layers.Dense(10,activation='softmax'))


### Compiling the model

fashion_3.compile(loss=tf.keras.losses.SparseCategoricalCrossentropy(),
                  optimizer=tf.keras.optimizers.Adam(),
                  metrics=['accuracy'])

tf.random.set_seed(100)
history_3=fashion_3.fit(X_train,y_train,epochs=25)
pd.DataFrame(history_3.history).plot();

### Improving the model by increasing the number of units
fashion_4=tf.keras.Sequential()
fashion_4.add(tf.keras.layers.Flatten())

# Changing the no of units 
fashion_4.add(tf.keras.layers.Dense(200,activation='relu'))

fashion_4.add(tf.keras.layers.Dense(100,activation='relu'))## Adding a layer of 100 units

fashion_4.add(tf.keras.layers.Dense(10,activation='softmax'))

### Compiling the model
fashion_4.compile(loss=tf.keras.losses.SparseCategoricalCrossentropy(),
                  optimizer=tf.keras.optimizers.Adam(),
                  metrics=['accuracy'])

tf.random.set_seed(100)
history_4=fashion_4.fit(X_train,y_train,epochs=25)
pd.DataFrame(history_4.history).plot();

### Evaluating the model

test_loss,test_accuracy=fashion_4.evaluate(X_test,y_test)

print('Test Loss:',test_loss)
print('Test Accuracy:',test_accuracy)

### model summary

fashion_2.summary()

### Prediction
y_pred=fashion_2.predict(X_test)
y_pred
