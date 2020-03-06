## Quantization work flows in PyTorch
PyTorch는 아래와 같이 세 가지 모드의Quantization을 지원한다.

### Post Training Dynamic Quantization

### Post Training Static Quantization

#### Procedure
1. Prepare the model
2. Fuse Operation
3. Specify the configuration of the quantization methods
4. Insert obserber to check activation tensors
5. Calibrate the model
6. Convert Model

### Quantization Aware Training


#### Procdure
1. (1), and (2) are identical
2. Specify the configuration of the fake quantization methods
3. Insert modules to simulate quantization during training
4. Train or fine tune the model
5. Identical to step (6) for static quantization
