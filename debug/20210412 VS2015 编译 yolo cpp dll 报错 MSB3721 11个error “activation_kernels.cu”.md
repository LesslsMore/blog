### VS2015 编译 yolo cpp dll 报错 MSB3721 11个error “activation_kernels.cu”
11个error详细的位置
```cpp
activation_kernels.cu" />
avgpool_layer_kernels.cu" />
blas_kernels.cu" />
col2im_kernels.cu" />
convolutional_kernels.cu" />
crop_layer_kernels.cu" />
deconvolutional_kernels.cu" />
dropout_layer_kernels.cu" />
im2col_kernels.cu" />
maxpool_layer_kernels.cu" />
network_kernels.cu" />
```
使用平台是GTX960
看了多篇回答都是将 

![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105154011.png)

compute_30,sm_30；compute_75,sm_75；后面的 compute_75,sm_75 删除
因为这个是代表显卡算力的数值，但是试过之后，发现没用
终于在一篇文章中找到启发
[https://blog.csdn.net/u011779224/article/details/111869286](https://blog.csdn.net/u011779224/article/details/111869286)
参考下图，GTX960对应的算力是5.0，于是把 compute_30,sm_30；改为 compute_50,sm_50；
最后终于编译通过！
[英伟达官方显卡算力表](https://developer.nvidia.com/cuda-gpus#collapseOne)

![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105154035.png)


