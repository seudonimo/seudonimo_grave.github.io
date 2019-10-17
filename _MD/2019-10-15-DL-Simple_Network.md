# How to make your own NN(Neural Network)
이 문서는 간단한 네트웍을 생각하고 구성하고, 훈련하고 그리고 테스트 하는 과정을 순서대로 나열해본 기록이다. 인터넷에 좋은 예제들도 많지만 그냥 따라하기 보다는 생각을 하면서 해보고 싶었던 걸 기록해 보았다.

목표 : 간단한 구조의 NN을 

TODO : 간단한 구조의 network를 keras로 모델링, 훈련, 확인한다.

Dataset : MNIST Digit data
Network : Convolution + FC Layer 
## Data
### Dataset : MNIST Digit data
- Train Images
  - 6만장의 28 by 28 이미지
- Test Images
  - 1만장의 28 by 28 이미지

```python
from keras.datasets import mnist
from keras import models
from keras import layers
from keras.utils import to_categorical
(_train_images, _train_labels), (_test_images, _test_labels) = mnist.load_data()

#Scaling from zero to one
train_images = _train_images.reshape((60000, 28 * 28))
train_images = train_images.astype('float32') / 255
test_images = _test_images.reshape((10000, 28 * 28))
test_images = test_images.astype('float32') / 255
```

```python
print(_test_labels)
train_labels = to_categorical(_train_labels)
test_labels = to_categorical(_test_labels)
print("after on-hot encoding, \n", test_labels)
```

## Modeling
### Network
- Input
  - 28 by 28 image
- 1st Layer
  - Conv2d
- 2nd Layer
  - Conv2d
- 3rd Layer
  - FC
- Output
  - FC
  
```python
model = models.Sequential()

#model.add(layer.Conv2d(12, (3, 3), padding='valid', activation='relu', input_shape=(28, 28, 1))
#model.add(layer.Conv2d
```

## Training
### Dataset
### Hypothesis
### Cost function
### ...


## Prediciton
