## Quantization work flows in PyTorch
PyTorch는 아래와 같이 세 가지 모드의Quantization을 지원한다.

### Post Training Dynamic Quantization
이 방법은 가장 간단하게 양자화를 적용하는 방법으로 weight는 미리 양자화를 수행하지만 Activation의 경우, inference 중에 동적으로 양자화된다. 이 방법은 모델 수행 시간이 실제 계산하는데 걸리는 시간보다 메모리로부터 weight를 로딩하는데 걸리는 시간이 더 두드러지는 상황에서 주로 사용된다. 작은 사이즈의 batch를 가지는 LSTM과 Transformer model에 적합하다. 동적인 quantization을 모델 전체에 적용하는 것은 torch.quantization.quantize_dynamic()으로 한방에 할 수 있으며  자세한 내용은 quantization tutorial에 포함되어 있다.

### Post Training Static Quantization
이 방법은 weight는 미리 양자화 되지만 Activation tensor는 scale factor와 bias가 calibration process과정을 거치며 model의 특성을 기반으로 미리 계산되는 모델에 사용되기 좋다. Post Training Quantization은 보통 CNN과 같이 Memory bandwidth와 Computing saving 두 개를 모두 신경써야 하는 경우에 사용되기 좋다. 일반적인 순서는 아래와 같다.
#### Procedure
1. Prepare the model
2. Fuse Operation
3. Specify the configuration of the quantization methods
4. Insert obserber to check activation tensors
5. Calibrate the model
6. Convert Model

### Quantization Aware Training
가끔 Post training quantization이 만족할만한 결과를 보여주지 못할 때, "Fake quantize"를 사용한 simulated quantization으로 해결할 수 있다. 계산은 FP32로 계산하지만 값은 INT8 quantization의 효과를 시뮬레이션 하기 위해 값이 고정되고 반올림 된다. 순서는 앞선 Static Quantization과 매우 유사하다.

#### Procdure
1. (1), and (2) are identical
2. Specify the configuration of the fake quantization methods
3. Insert modules to simulate quantization during training
4. Train or fine tune the model
5. Identical to step (6) for static quantization

이에 대해 자세한건 마찬가지


Observer가 Scale factor, Bias를 선택하는 기본적인 구현을 제공하지만 개발자는 본인임 ㅏㄴ든걸 추가할 수도 있다. Quantization은 모델의 특정 파트에대해 선택적으로 적용할 수 있으며, 파트마다 다르게 적용할 수도 있다.

현재 채널별로 지원하는 함수는 conv2d, conv3d, linear 정도이다.
