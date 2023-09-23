### 旋转矩阵
左手系、右手系
左乘、右乘
特殊欧氏群$SE(n)$ $n$维欧氏变换
特殊正交群$SO(n)$旋转矩阵群
相似变换$Sim(3)$
$SO(3)$三维空间的旋转
罗德里格斯公式 （Rodrigues’s Formula）
$R^T=R^{-1}$

##### Trigonometric identities
$\sin \theta=-\sin (-\theta)=-\cos(\theta+90^\circ)=\cos(\theta-90^\circ)$
$\cos \theta=\cos (-\theta)=\sin(\theta+90^\circ)=-\sin(\theta-90^\circ)$

$\sin(\theta_1+\theta_2)=s_1c_2+c_1s_2=s_{12}$
$\sin(\theta_1-\theta_2)=s_1c_2-c_1s_2$
$\cos(\theta_1+\theta_2)=c_1c_2-s_1s_2=c_{12}$
$\cos(\theta_1-\theta_2)=c_1c_2+s_1s_2$


##### 二维旋转矩阵
$R(\theta)={\begin{bmatrix}\cos \theta &-\sin \theta \\\sin \theta &\cos \theta \\\end{bmatrix}}=\cos \theta \begin{bmatrix}1 &0\\0 &1\\\end{bmatrix}+\sin \theta \begin{bmatrix}0 &-1\\1 &0\\\end{bmatrix}=\exp(\theta \begin{bmatrix}0 &-1\\1 &0\\\end{bmatrix})$

##### 三维旋转矩阵 Euler Rotations
$R_{x}(\theta_x)={\begin{bmatrix}1 &0 &0\\0 &\cos \theta_x &-\sin \theta_x \\0 &\sin \theta_x &\cos \theta_x \\\end{bmatrix}}=\exp(\begin{bmatrix}0 &0 &0\\0 &0 &-\theta_x\\0 &\theta_x &0\end{bmatrix})=roll$

$R_{y}(\theta_y )={\begin{bmatrix}\cos \theta_y &0&\sin \theta_y \\0&1&0\\-\sin \theta_y &0&\cos \theta_y \\\end{bmatrix}}=\exp(\begin{bmatrix}0 &0 &\theta_y\\0 &0 &0\\-\theta_y &0 &0\end{bmatrix})=pitch$

$R_{z}(\theta_z )={\begin{bmatrix}\cos \theta_z &-\sin \theta_z &0\\\sin \theta_z &\cos \theta_z &0\\0&0&1\\\end{bmatrix}}=\exp(\begin{bmatrix}0 &-\theta_z &0\\\theta_z &0 &0\\0 &0 &0\end{bmatrix})=yaw$

$M=R_z(\theta_z)R_y(\theta_y)R_x(\theta_x)=\exp(\begin{bmatrix}0 &-\theta_z &\theta_y\\\theta_z &0 &-\theta_x\\-\theta_y &\theta_x &0\end{bmatrix})$

###### matlab
eul = [0 pi/2 0]; % z y x
rotmZYX = eul2rotm(eul)

##### 微分旋转矩阵
$M_0=\begin{bmatrix}1 &-\theta_z &\theta_y\\\theta_z &1 &-\theta_x\\-\theta_y &\theta_x &1\end{bmatrix}$

##### “偏航-俯仰-滚转”（yaw-pitch-roll）
1.绕物体的Z 轴旋转， 得到偏航角yaw；
2.绕旋转之后 的Y 轴旋转， 得到俯仰角pitch；
3.绕旋转之后 的X 轴旋转， 得到滚转角roll。


### 东北天、站心坐标系
Local east, north, up (ENU) coordinates
<img src="https://img-blog.csdnimg.cn/20200915195548935.png" width="50%">

Local north, east, down (NED) coordinates
<img src="https://img-blog.csdnimg.cn/20200915195548919.png" width="50%">

${\displaystyle R={\begin{bmatrix}-\sin(\phi )\cos(\lambda )&-\sin(\lambda )&-\cos(\phi )\cos(\lambda )\\-\sin(\phi )\sin(\lambda )&\cos(\lambda )&-\cos(\phi )\sin(\lambda )\\\cos(\phi )&0&-\sin(\phi )\end{bmatrix}}}$

#### Matlab
3-D Coordinate and Vector Transformations
geodetic2enu
enu2geodetic
#### Geodetic and ECEF Coordinate Systems
BLH2XYZ
Geodetic coordinates (latitude ${\displaystyle\ \phi }$, longitude ${\displaystyle \ \lambda }$, height ${\displaystyle h}$) can be converted into ECEF coordinates using the following equation:

${\displaystyle {\begin{aligned}X&=\left(N(\phi )+h\right)\cos {\phi }\cos {\lambda }\\Y&=\left(N(\phi )+h\right)\cos {\phi }\sin {\lambda }\\Z&=\left({\frac {b^{2}}{a^{2}}}N(\phi )+h\right)\sin {\phi }\end{aligned}}}$
where
${\displaystyle N(\phi )={\frac {a^{2}}{\sqrt {a^{2}\cos ^{2}\phi +b^{2}\sin ^{2}\phi }}}={\frac {a}{\sqrt {1-e^{2}\sin ^{2}\phi }}},}$
其中
${\displaystyle e^{2}=1-{\frac {b^{2}}{a^{2}}}}$


$\left\{\begin{array}{l}B=\arctan \left[\frac{z_{e}+\left(e^{\prime}\right)^{2} \cdot b \cdot \sin ^{3} U}{\sqrt{x_{e}^{2}+y_{e}^{2}}-a \cdot e^{2} \cdot \cos ^{3} U}\right]\\\\L=\arctan \frac{y_e}{x_e}\\\\H=\frac{\sqrt{x_{e}^{2}+y_{e}^{2}}}{\cos B}-N\\\end{array}\right.$

<img src="https://img-blog.csdnimg.cn/20200915195748587.jpg" width="75%">

$R_z(-(90+L))R_x(-(90-B))$

${\displaystyle {\begin{aligned}{\begin{pmatrix}dX\\dY\\dZ\end{pmatrix}}&={\begin{pmatrix}-\sin \lambda &-\sin \phi \cos \lambda &\cos \phi \cos \lambda \\\cos \lambda &-\sin \phi \sin \lambda &\cos \phi \sin \lambda \\0&\cos \phi &\sin \phi \\\end{pmatrix}}{\begin{pmatrix}dE\\dN\\dU\end{pmatrix}},\\[3pt]{\begin{pmatrix}dE\\dN\\dU\end{pmatrix}}&={\begin{pmatrix}\left(N(\phi )+h\right)\cos \phi &0&0\\0&M(\phi )+h&0\\0&0&1\\\end{pmatrix}}{\begin{pmatrix}d\lambda \\d\phi \\dh\end{pmatrix}},\end{aligned}}}$

${\displaystyle M(\phi )={\frac {a\left(1-e^{2}\right)}{\left(1-e^{2}\sin ^{2}\phi \right)^{\frac {3}{2}}}}}$

$\begin{bmatrix}x\\y\\z\end{bmatrix}=\begin{bmatrix}E\\N\\U\end{bmatrix}$

### 地心坐标系
大地坐标系（φ,λ,h），geodetic
地心地固坐标系（Earth-Centered, Earth-Fixed，简称ECEF）简称地心坐标系
WGS-84椭球模型

##### From ECEF to ENU
${\displaystyle {\begin{bmatrix}x\\y\\z\end{bmatrix}}={\begin{bmatrix}-\sin \lambda _{r}&\cos \lambda _{r}&0\\-\sin \phi _{r}\cos \lambda _{r}&-\sin \phi _{r}\sin \lambda _{r}&\cos \phi _{r}\\\cos \phi _{r}\cos \lambda _{r}&\cos \phi _{r}\sin \lambda _{r}&\sin \phi _{r}\end{bmatrix}}{\begin{bmatrix}X_{p}-X_{r}\\Y_{p}-Y_{r}\\Z_{p}-Z_{r}\end{bmatrix}}}$

##### From ENU to ECEF
${\displaystyle {\begin{bmatrix}X\\Y\\Z\end{bmatrix}}={\begin{bmatrix}-\sin \lambda &-\sin \phi \cos \lambda &\cos \phi \cos \lambda \\\cos \lambda &-\sin \phi \sin \lambda &\cos \phi \sin \lambda \\0&\cos \phi &\sin \phi \end{bmatrix}}{\begin{bmatrix}x\\y\\z\end{bmatrix}}+{\begin{bmatrix}X_{r}\\Y_{r}\\Z_{r}\end{bmatrix}}}$

### 单应变换(Homography)、射影变换、仿射变换
$\begin{bmatrix}u\\v\\1\end{bmatrix}=\begin{bmatrix}h_{11}&h_{12}&h_{13}\\h_{21}&h_{22}&h_{23}\\h_{31}&h_{32}&h_{33}\\\end{bmatrix}\begin{bmatrix}x\\y\\z\end{bmatrix}$

$\begin{bmatrix}h_{11}&h_{12}&h_{13}\\h_{21}&h_{22}&h_{23}\\h_{31}&h_{32}&h_{33}\\\end{bmatrix}^{-1}\begin{bmatrix}u\\v\\1\end{bmatrix}=\begin{bmatrix}x\\y\\z\end{bmatrix}$

3对点根据上式求出9个方程

UTM undergraduate texts in mathematics
GTM graduate texts in mathematics 
