### 等距变换(Isometries)
$\left[\begin{matrix}x'\\y'\\1\\\end{matrix}\right]=
\left[\begin{matrix}\sigma\cos\theta&-\sin\theta&x_0\\\sigma\sin\theta&\cos\theta&y_0\\0&0&1\\\end{matrix}\right]
\left[\begin{matrix}x\\y\\1\\\end{matrix}\right]$

$\sigma=\pm1$

### 欧式变换(Euclidean)
在等距变换(1.4.1)中，如果矩阵 U 是一个旋转矩阵，则这个等距变换称为欧氏变换。

$\left[\begin{matrix}x'\\y'\\1\\\end{matrix}\right]=H_e\mathbf{x}=
\left[\begin{matrix}R&t\\0&1\end{matrix}\right]
\left[\begin{matrix}x\\y\\1\\\end{matrix}\right]$

### 相似变换(Similarity)
相似变换是等距变换与均匀伸缩变换的合成变换，所谓均匀伸缩变换是指下述变换：

$\left[\begin{matrix}x'\\y'\\1\\\end{matrix}\right]=
\left[\begin{matrix}s&0&0\\0&s&0\\0&0&1\\\end{matrix}\right]
\left[\begin{matrix}x\\y\\1\\\end{matrix}\right]$

其中 s 是均匀伸缩因子。

相似变换，顾名思义，它是保持图形相似的变换。在初等几何中，相似分为旋转相似(保向)和对称相似(逆向)。旋转相似是欧氏变换与均匀伸缩变换的合成，而对称相似是反射等距变换与均匀伸缩变换的合成。

在计算机视觉中最关心的是旋转相似，它可用下面的矩阵形式来表示：

$\left[\begin{matrix}x'\\y'\\1\\\end{matrix}\right]=
\left[\begin{matrix}s\cos\theta&-s\sin\theta&x_0\\s\sin\theta&s\cos\theta&y_0\\0&0&1\\\end{matrix}\right]
\left[\begin{matrix}x\\y\\1\\\end{matrix}\right]$

$\mathbf{x'}=H_e\mathbf{x}=
\left[\begin{matrix}sR&t\\0&1\end{matrix}\right]\mathbf{x}$

旋转相似变换有 4 个自由度，因为它比欧氏变换多一个均匀伸缩因子。

### 仿射变换(Affine)
$\left[\begin{matrix}x'\\y'\\1\\\end{matrix}\right]=
\left[\begin{matrix}A&t\\0&1\end{matrix}\right]
\left[\begin{matrix}x\\y\\1\\\end{matrix}\right]=
\left[\begin{matrix}a&b&x_0\\c&d&y_0\\0&0&1\\\end{matrix}\right]
\left[\begin{matrix}x\\y\\1\\\end{matrix}\right]$

其中 A 是一个 2 阶可逆矩阵。仿射变换有 6 个自由度， 3 个不共线的点对应唯一确定仿射变换。仿射变换的全体也构成一个变换群，称为仿射变换群。 相似变换群是它的子群。

### 射影变换(Projective)
$\mathbf{x'}=H\mathbf{x}=
\left[\begin{matrix}A&t\\v^T&k\end{matrix}\right]\mathbf{x}$

$H=H_SH_AH_P=
\left[\begin{matrix}sR&t/k\\0&1\end{matrix}\right]
\left[\begin{matrix}K&0\\0&1\end{matrix}\right]
\left[\begin{matrix}I&0\\v^T&k\end{matrix}\right]$

矩阵$H_SH_AH_P$分别是相似变换、仿射变换和射影变换

变换$H_P$属于节A5.3 ( p430）所介绍的一种有约束的透视变换

<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101104657.png" width="70%">

<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101104724.png" width="70%">

### 单应变换(Homography)、透视变换(Perspective)
单应变换即是指具有对应关系的两幅图像之间的映射关系，一般的，单应变换的变换矩阵是一个3*3的矩阵H，H虽然具有9个元素，但是具有8个自由度。

$\left[\begin{matrix}u_2\\v_2\\1\\\end{matrix}\right]=H
\left[\begin{matrix}u_1\\v_1\\1\\\end{matrix}\right]=
\left[\begin{matrix}h_1&h_2&h_3\\h_4&h_5&h_6\\h_7&h_8&h_9\\\end{matrix}\right]
\left[\begin{matrix}u_1\\v_1\\1\\\end{matrix}\right]$

$\left\{\begin{matrix}u_2=\frac{h_1u_1+h_2v_1+h_3}{h_7u_1+h_8v_1+h_9}\\v_2=\frac{h_4u_1+h_5v_1+h_6}{h_7u_1+h_8v_1+h_9}\\\end{matrix}\right.$

在实际处理中通常乘以一个非零因子使得h_9=1，于是有：

$\left\{\begin{matrix}h_1u_1+h_2v_1+h_3-h_7u_1u_2-h_8v_1u_2=v_2\\h_4u_1+h_5v_1+h_6-h_7u_1v_2-h_8v_1v_2=v_2\\\end{matrix}\right.$

这样一组匹配点对就可以构造出两项约束，于是自由度为8的单应矩阵可以通过4对匹配特征点算出（注意，这些特征点不能有三点共线的情况）。

$\left[\begin{matrix}u_1^1 &v_1^1 &1 &0 &0 &0 &-u_1^1u_2^1 &-v_1^1u_2^1\\0 &0 &0 &u_1^1 &v_1^1 &1 &-u_1^1v_2^1 &-v_1^1v_2^1\\u_1^2 &v_1^2 &1 &0 &0 &0 &-u_1^2u_2^2 &-v_1^2u_2^2\\0 &0 &0 &u_1^2 &v_1^2 &1 &-u_1^2v_2^2 &-v_1^2v_2^2\\u_1^3 &v_1^3 &1 &0 &0 &0 &-u_1^3u_2^3 &-v_1^3u_2^3\\0 &0 &0 &u_1^3 &v_1^3 &1 &-u_1^3v_2^3 &-v_1^3v_2^3\\u_1^4 &v_1^4 &1 &0 &0 &0 &-u_1^4u_2^4 &-v_1^4u_2^4\\0 &0 &0 &u_1^4 &v_1^4 &1 &-u_1^4v_2^4 &-v_1^4v_2^4\\
\end{matrix}\right]\left[\begin{matrix}h_1\\h_2\\h_3\\h_4\\h_5\\h_6\\h_7\\h_8\end{matrix}\right]=\left[\begin{matrix}u_2^1\\v_2^1\\u_2^2\\v_2^2\\u_2^3\\v_2^3\\u_2^4\\v_2^4   
\end{matrix}\right]$

### 总结
- 欧式变换的特性是保持欧式距离不变，有一个旋转角度，两个平移变换共三个自由度。

- 相似变换在欧式变换的基础上增加了一个各向同性的尺度变换，共有四个自由度，保持距离的比例不变。

- 仿射变换包含了两个旋转角度，两个各向异性的尺度变换，一共有六个自由度，变换后的平行线依然保持平行，平行线所分割的线段及区域成比例。

- 射影变换（单应变换）在仿射变换的基础增加了两个自由度，使得图像在不同的位置具有不同的尺度变换，变换后保持原有的三点共线特性。

- 透视投影则是3D到2D的射影变换，是一个3*4的矩阵，有11个自由度，可以分解为5个自由度的相机内参和6个自由度的表示相机姿态的外参。

需要求解单应矩阵的场景主要有相机标定，计算相机焦距，主点，镜头畸变，相机位姿；三维重建，场景结构，相机位姿；视觉测量；立体视觉，计算多视图场景的深度；场景理解，修正相机的摇动、倾斜和变焦等等。

单应矩阵的估计算法。直接线性变换（DLT），直接使用四对点进行计算不准确或类似于过拟合，通常使用正则化的方法进行泛化，更具有一般性。在计算的过程中选择不同的损失（代价）函数，使其最小化。常用的损失函数有==代数距离、几何距离、重投影误差、Sampson误差==等。

选取的特征也不一定是对应点也可以是对应线和对应的二次曲线。处理离群点通常使用的方法有==RANSAC==、==LMedS==(Least Median of Squares Regression)等。
### 参考文献
- Multiple View Geometry in Computer Vision (Second Edition) 计算机视觉中的多视图几何
- 计算机视觉中的数学方法-吴福朝
- 视觉SLAM十四讲：从理论到实践
- 学习OpenCV 3
- Homography Estimation
- Least Median of Squares Regression


