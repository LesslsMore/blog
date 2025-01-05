### 直接线性变换(Direct Linear Transform,DLT)
$s\begin{bmatrix} u \\ v \\ 1 \end{bmatrix} =\begin{bmatrix} r_{11} & r_{12} & r_{13} & t_x \\ r_{21} & r_{22} & r_{23} & t_y \\ r_{31} & r_{32} & r_{33} & t_z  \end{bmatrix} \begin{bmatrix} X_{w} \\ Y_{w} \\ Z_{w} \\ 1 \end{bmatrix}$

由于 RT 一共有12维，因此，最少通过6对匹配点即可实现矩阵 RT 的==线性求解==，这种方法称为直接线性变换（Direct Linear Transform，DLT）。当匹配点大于6对时，也可以使用SVD等方法对超定方程求最小二乘解。

但由于 R 是一个旋转矩阵，其内部存在约束$R^T=R^{-1},RR^T=I,det(R)=1$，实际只需要三个变量就能表示。参考==罗德里格斯公式（Rodrigues’s Formula）==。

旋转矩阵有一些特别的性质。 事实上， 它是一个行列式为1的正交矩阵 $R^T=R^{-1}$。 反之，行列式为1的正交矩阵也是一个旋转矩阵。 所以， 可以把旋转矩阵的集合定义如下：

$SO(n)=\{R\in \mathbb{R}^{n \times n}|RR^T=I,det(R)=1\}$

当只有3对点时，可以考虑如下约束，进行==非线性求解==

$\left[\begin{matrix}r_{11} & r_{12} & r_{13}\\ r_{21} & r_{22} & r_{23} \\ r_{31} & r_{32} & r_{33} \end{matrix}\right]\left[\begin{matrix}r_{11} & r_{12} & r_{13}\\ r_{21} & r_{22} & r_{23} \\ r_{31} & r_{32} & r_{33} \end{matrix}\right]^T=I$

整理得：

$\left\{\begin{matrix}r_{11}^2+r_{12}^2+r_{13}^2=1\\r_{11}r_{21}+r_{12}r_{22}+r_{13}r_{23}=0\\r_{11}r_{31}+r_{12}r_{32}+r_{13}r_{33}=0\\r_{21}^2+r_{22}^2+r_{23}^2=1\\r_{21}r_{31}+r_{22}r_{32}+r_{23}r_{33}=0\\r_{31}^2+r_{32}^2+r_{33}^2=1\end{matrix}\right.$

共6个方程，再加上3对点的6个方程，从而可以利用 LM 算法求解。

### 三点透视问题(Perspective-Three-Point Problem,P3P)
<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101104952.png" width="50%">

可以利用三角几何关系列方程求解，与非线性求解等价。

在求解P3P问题时，将三个三元二次方程，转换为两个二元二次方程，最终化为一个一元四次方程，从而求出了该问题的闭式解。

### RANSAC(RANdom SAmple Consensus)
RANSAC的特点主要是可以从包含大量误差的数据中拟合出较为准确的模型。

该算法不同于最小二乘法，并没有将全部数据进行计算，而是类似于==剔除粗大误差==将计算为有效的点用来估计模型，从而使得估计更加准确。可以将其与==Kmeans算法==相结合用于数据模型的估计。

位置确定问题（Location Determination Problem, LDP）中的应用：即已知一组空间点的坐标，且给定了一张图像，并知道图像中点与空间点的对应关系，求图像的透视中心点在空间中的位置与姿态。

### 相机标定(Camera Calibration)
如果显示器模拟图像空间姿态变换用以标定相机，那么就说明已经知道了这个单应矩阵，因此该方法用于标定相机理论不可行。

### 对极约束
<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101105031.png" width="50%">

$x_2^Tt^\wedge Rx_1=0$

$p_2^TK^{-T}t^\wedge RK^{-1}p_1=0$

这两个式子都称为对极约束，它以形式简洁著名。它的几何意义是O1,P,O2三者共面。对极约束中同时包含了平移和旋转。我们把中间部分记作两个矩阵：基础矩阵（Fundamental Matrix）F和本质矩阵（Essential Matrix）E，于是可以进一步简化对极约束：

$E=t^\wedge R, F=K^{-T}EK^{-1}, x_2^TEx_1=p_2^TFp_1=0$

由于E和F只相差了相机内参，而内参在SLAM中通常是已知的，所以实践当中往往使用形式更简单的E。

### 本质矩阵(Essential Matrix)
由于平移和旋转各有3个自由度，故 $t^\wedge R$ 共有6个自由度。但由于尺度等价性，故 E 实际上有5个自由度。

E具有5个自由度的事实，表明我们最少可以用==5对点==来求解E。但是，E的内在性
质是一种非线性性质，在求解线性方程时会带来麻烦，因此，也可以只考虑它的尺度
等价性，使用8对点来估计E——这就是经典的==八点法（Eight-point-algorithm）==[38,39]
。八点法只利用了E的线性性质，因此可以在线性代数框架下求解。

$\left[\begin{matrix}u_1&v_1&1\\\end{matrix}\right]
\left[\begin{matrix}e_1&e_2&e_3\\e_4&e_5&e_6\\e_7&e_8&e_9\\\end{matrix}\right]
\left[\begin{matrix}u_2\\v_2\\1\\\end{matrix}\right]=0$

OpenCV 中还有 7-point algorithm
### 参考文献
- 视觉SLAM十四讲：从理论到实践
- 视觉测量原理与方法
- OpenCV官方文档
- [Fischler81]Random Sample Consensus A Paradigm for Model Fitting with Applications to Image Analysis and Automated Cartography
- k-means++: The Advantages of Careful Seeding
- Complete Solution Classification for the Perspective-Three-Point Problem
- A Flexible New Technique for Camera Calibration
- 1997-PAMI-Richard I. Hartley-In Defense of the Eight-Point Algorithm



