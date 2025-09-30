## Deep-Learning-Exp3

**DL-Convolutional Deep Neural Network for Image Classification**

## AIM:

To develop a convolutional neural network (CNN) classification model for the given dataset.

## THEORY

The MNIST dataset consists of 70,000 grayscale images of handwritten digits (0-9), each of size 28×28 pixels. The task is to classify these images into their respective digit categories. CNNs are particularly well-suited for image classification tasks as they can automatically learn spatial hierarchies of features through convolutional layers, pooling layers, and fully connected layers.

## Neural Network Model

Include the neural network model diagram.

## DESIGN STEPS

**STEP 1:** Preprocess the MNIST dataset by normalizing pixel values to the range [0,1], reshaping the images to (28,28,1), and converting the labels into one-hot encoded format.

**STEP 2:** Build a convolutional neural network (CNN) model with specified architecture using TensorFlow Keras

**STEP 3:** Compile the model using the categorical cross-entropy loss function, Adam optimizer, and accuracy as the evaluation metric.

**STEP 4:** Train the compiled model on the preprocessed training data for 5 epochs with a batch size of 64, while validating on the test set.

**STEP 5:** Evaluate the trained model by:Plotting training vs validation accuracy and loss ,Generating a confusion matrix and classification report.

**STEP 6:** Test the model with external custom digit images by resizing them to 28x28, converting them to grayscale, scaling pixel values, and predicting their labels using the trained CNN.

## PROGRAM:

**Name:** Hariharan S

**Register Number** 2305001009

```
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers
from tensorflow.keras.datasets import mnist
import tensorflow as tf
import matplotlib.pyplot as plt
from tensorflow.keras import utils
import pandas as pd
from sklearn.metrics import classification_report,confusion_matrix
from tensorflow.keras.preprocessing import image

(X_train, y_train), (X_test, y_test) = mnist.load_data()
X_train.shape
X_test.shape
single_image= X_train[0]
single_image.shape
plt.imshow(single_image,cmap='gray')
y_train.shape
X_train.min()
X_train.max()
X_train_scaled = X_train/255.0
X_test_scaled = X_test/255.0
X_train_scaled.min()
X_train_scaled.max()
y_train[0]
y_train_onehot = utils.to_categorical(y_train,10)
y_test_onehot = utils.to_categorical(y_test,10)
type(y_train_onehot)
y_train_onehot.shape
single_image = X_train[500]
plt.imshow(single_image,cmap='gray')
y_train_onehot[500]
X_train_scaled = X_train_scaled.reshape(-1,28,28,1)
X_test_scaled = X_test_scaled.reshape(-1,28,28,1)

model = keras.Sequential()
model.add(layers.Input(shape=(28,28,1)))
model.add(layers.Conv2D(filters=32,kernel_size=(3,3),activation='relu'))
model.add(layers.MaxPool2D(pool_size=(2,2)))
model.add(layers.Flatten())
model.add(layers.Dense(32,activation='relu'))
model.add(layers.Dense(64,activation='relu'))
model.add(layers.Dense(10,activation='softmax'))

model.summary()

model.compile(loss='categorical_crossentropy',
              optimizer='adam',
              metrics='accuracy')

model.fit(X_train_scaled ,y_train_onehot, epochs=5,
          batch_size=64,
          validation_data=(X_test_scaled,y_test_onehot))

metrics = pd.DataFrame(model.history.history)
metrics.head()
print("Rithiga Sri.B 212221230083")
print("Rithiga Sri.B 212221230083")
metrics[['accuracy','val_accuracy']].plot()
print("Rithiga Sri.B 212221230083")
metrics[['loss','val_loss']].plot()

x_test_predictions = np.argmax(model.predict(X_test_scaled), axis=1)
print("Rithiga Sri.B 212221230083")
print(confusion_matrix(y_test,x_test_predictions))

print("Rithiga Sri.B 212221230083")
print(classification_report(y_test,x_test_predictions))

img = image.load_img('/content/img.jpeg')
type(img)

img = image.load_img('/content/six.png')
plt.imshow(img)
img_tensor = tf.convert_to_tensor(np.asarray(img))
img_28 = tf.image.resize(img_tensor,(28,28))
img_28_gray = tf.image.rgb_to_grayscale(img_28)
img_28_gray_scaled = img_28_gray.numpy()/255.0
x_single_prediction = np.argmax(model.predict(img_28_gray_scaled.reshape(1,28,28,1)),axis=1)

print("Rithiga Sri.B 212221230083")
print(x_single_prediction)
plt.imshow(img_28_gray_scaled.reshape(28,28),cmap='gray')

img1 = image.load_img('/content/zero.jfif')
plt.imshow(img1)
img_tensor1 = tf.convert_to_tensor(np.asarray(img1))
img_28_gray1 = tf.image.resize(img_tensor1,(28,28))
img_28_gray1 = tf.image.rgb_to_grayscale(img_28_gray1)
img_28_gray_inverted1 = 255.0-img_28_gray1
img_28_gray_inverted_scaled1 = img_28_gray_inverted1.numpy()/255.0

x_single_prediction1 = np.argmax(model.predict(img_28_gray_inverted_scaled1.reshape(1,28,28,1)),axis=1)
print("Rithiga Sri.B 212221230083")
print(x_single_prediction1)
plt.imshow(img_28_gray_inverted_scaled1.reshape(28,28),cmap='gray')
```

# OUTPUT

**Training Loss per Epoch**

<img width="1211" height="222" alt="image" src="https://github.com/user-attachments/assets/979bdcd8-f60f-4d77-846c-f99c854d296d" />


**Confusion Matrix**

<img width="825" height="235" alt="image" src="https://github.com/user-attachments/assets/c92c4a0e-acbe-4ebf-9832-1e6684f54b39" />


**Classification Report**

<img width="874" height="357" alt="image" src="https://github.com/user-attachments/assets/33660858-243b-42fd-8f56-6a9789915fba" />

**New Sample Data Prediction**

<img width="1330" height="511" alt="image" src="https://github.com/user-attachments/assets/6f1ca7fd-058b-49de-9fb6-21275503f3e7" />
<img width="1437" height="522" alt="image" src="https://github.com/user-attachments/assets/493e4096-795d-4541-aae6-da24f05299f3" />
<img width="1236" height="482" alt="image" src="https://github.com/user-attachments/assets/76087a74-0167-4bad-bd25-ea3f97bed905" />
<img width="1040" height="522" alt="image" src="https://github.com/user-attachments/assets/a5057cd0-975c-4aa6-8e42-535b19602655" />





## RESULT
Thus, a Convolutional deep neural network for digit classification and to verify the response for scanned handwritten images is developed successfully.


