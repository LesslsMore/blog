### 模型转换

由于 pytorch 模型为动态图，转换时需要从算法模型代码引入从 nn.Module 继承的网络结构。

### TorchScript  
TorchScript是PyTorch模型（nn.Module的子类）的中间表示，可以在高性能环境（例如C ++，注意不止是c++）中运行。注意的是TorchScript是可以通过python语言使用和导出的。  
Pytorch模型转TorchScrip进行保存，保存后的pt模型可以在C++等高性能环境中运行

Pytorch 导出 onnx 模型，可用 onnx sim 对结构进行化简优化  
torchscript 模型可由 python 导出，在 c++ 下运行
直接 tune torchscript 转换为 trt 模型

Tune torchscript
Pnnx