## 模型服务化(Model Serving)
模型服务化是指将**模型部署**在服务器上作为微服务对外提供接口服务 

比如互联网企业需要深度学习对**音、视、图、文**进行**推荐、识别、审核（内容理解）**，因此需要将模型服务化，从而形成**算法平台（AI 中台）**  

由于算力并不一致饱和，许多互联网企业将算法平台开放出来，对外出售机器资源和人工智能服务接口，类似以下**模型门户**网站  
https://platform.openmmlab.com/home/ 

### 美团实践分享   
[算法平台在线服务体系的演进与实践](https://tech.meituan.com/2021/05/13/turing-os-online-serving.html)  

### 服务化框架  
[TorchServe](https://pytorch.org/serve/)  
[TensorFlow Serving](https://www.tensorflow.org/tfx/guide/serving)  
[Triton](https://github.com/triton-inference-server/server)

## 模型部署、推理框架
模型在训练框架训练完成后，为了降低时延、提高吞吐，需要将模型部署在推理框架上。

### 训练框架
|训练框架|支持的模型与格式|简介|
|-|-|-|
|Pytorch|.pt .pth|脸书
|tensorflow|.tf|谷歌
|Paddle|.pdiparams|百度 ocr 较为知名

### 推理框架
| 推理框架         | 模型                       | 简介                         |
| ------------ | ------------------------ | -------------------------- |
| ONNX runtime | .onnx                    | 微软专为 ONNX 格式的模型设计的高性能推理引擎。 |
| OpenVINO     | .onnx .xml .bin .mapping | 针对英特尔 CPU GPU 优化           |
| TensorRT     | .engine                  | 针对英伟达 GPU 优化               |

### mobile 推理框架
阿里的MNN、腾讯的NCNN
https://github.com/Tencent/ncnn
https://github.com/alibaba/MNN

## 模型转换
而为了实现模型从训练框架到推理框架的转换，Facebook、Microsoft 开发了 ONNX

### [ONNX](https://onnx.ai/index.html)

ONNX，Open Neural Network Exchange，是一种通用的神经网络交换格式。

它是统一各种模型格式的中间表示，是各种模型相互转换的桥梁。

如需将 pytorch 模型转换为 tensorRT 模型，则先需要将 pytorch 模型转换为 onnx，再将 onnx 转换为 tensorRT 模型。

一般模型都支持转换为 onnx 。
### 模型可视化工具 Netron
https://github.com/lutzroeder/netron  
可以查看 ONNX 等模型内部的算子与计算图的构成

## 模型部署整体流程
![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153238.png)

mmdeploy 部署流程
![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153256.png)
## AI、深度学习编译器
受编译器原理启发，业界正通过类似原理实现 AI 编译器，从而实现各个平台模型运行的统一  

- llvm 编译器原理
![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153542.png)

- AI 编译器原理
![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153601.png)

以下是两种 AI 编译器：

- [TVM (Tensor Virtual Machine)](https://tvm.apache.org/)  
陈天奇领头，apache 基金管理
![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153623.png)

- [MLIR (Multi-Level Intermediate Representation)](https://onnx.ai/onnx-mlir/)
https://github.com/onnx/onnx-mlir