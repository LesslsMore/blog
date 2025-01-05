### DOP Dilution Of Precision
通常为了描述定位误差与伪距误差之间的关系，定义如下精度因子来衡量测量的结果：
几何精度因子(Geometric Dilution Of Precision GDOP)
位置精度因子(Position(3D) Dilution Of Precision PDOP)
水平精度因子(Horizontal Dilution Of Precision HDOP)
垂直精度因子(Vertical Dilution Of Precision VDOP)
钟差精度因子(Time Dilution Of Precision TDOP)

$\sigma_P=\sqrt{\sigma_E^2+\sigma_N^2+\sigma_U^2}$

$\sigma_H=\sqrt{\sigma_E^2+\sigma_N^2}$

$\sigma_U=\sqrt{\sigma_U^2}$

$\sigma_T=\sqrt{\sigma_T^2}$

$PDOP=\frac{\sqrt{\sigma_E^2+\sigma_N^2+\sigma_U^2}}\sigma=\sqrt{D_{11}+D_{22}+D_{33}}$

$HDOP=\frac{\sqrt{\sigma_E^2+\sigma_N^2}}\sigma=\sqrt{D_{11}+D_{22}}$

$VDOP=\frac{\sigma_U^2}\sigma=\sqrt{ D_{33}}$

$TDOP=\frac{\sigma_T^2}\sigma=\sqrt{ D_{44}}$

$\sigma_G=\sqrt{\sigma_E^2+\sigma_N^2+\sigma_U^2+\sigma_T^2} =\sqrt{D_{11}+D_{22}+D_{33}+D_{44}}\sigma$

### 多点定位 Multilateration
TDOA (Time difference of arrival)
FDOA (Frequency difference of arrival)
TOA (Time of arrival, also time of flight) (ToF)
AOA (Angle of arrival)
DOA (Direction Of Arrival)
 
Trilateration 三边测量
Triangulation 三角测量
True-range multilateration      
### 测向交叉定位 三角定位
在这里假设有两个观测站在大地直角坐标系下对目标进行定位，两观测站的位置分别为
$S_0(x_0,y_0,z_0),S_1(x_1,y_1,z_1)$，目标的位置为$S(x,y,z)$，观测站与目标的位置关系如图所示。观测站$S_0$获得目标相对于它的方位角和俯仰角为$(\alpha_0,\beta_0)$，观测站S1获得目标相对于它的方位角和俯仰角为$(\alpha_1,\beta_1)$

<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101104445.png" width="50%">

$x\tan\alpha_0-y=x_0\tan\alpha_0-y_0$

$x\tan\alpha_1-y=x_1\tan\alpha_1-y_1$

$y\tan\beta_0-z\sin\alpha_0=y_0\tan\beta_0-z_0\sin\alpha_0$

$\left[\begin{matrix}\tan\alpha_0 &-1 &0\\\tan\alpha_1 &-1 &0\\0 &\tan\beta_0 &-\sin\alpha_0\end{matrix}\right]\begin{bmatrix}x\\y\\z\end{bmatrix}=\begin{bmatrix}x_0\tan\alpha_0-y_0\\x_1\tan\alpha_1-y_1\\y_0\tan\beta_0-z_0\sin\alpha_0\end{bmatrix}$

### DAE
测物距离D，方向角A和俯仰角E

Matlab Mapping Toolbox 3-D Coordinate Systems
Octave 中有开源实现代码
```c
geodetic2ecef
ecef2geodetic

geodetic2enu
enu2geodetic

ecef2enu
enu2ecef

ecef2acr
aer2ecef

aer2geodetic
geodetic2aer

[lat,lon,h] = aer2geodetic(az,elev,slantRange,lat0,lon0,h0,spheroid)
[az,elev,slantRange] = geodetic2aer(lat,lon,h,lat0,lon0,h0,spheroid)
```
Geometric Geodesy
wgs84Elipsoid

Great-circle navigation
Geodesics on an ellipsoid

经度 lon L
纬度 lat B
great circle track
rhumb line track

### 无人机
<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101104513.png" width="50%">

偏航角=航线角-航向角
空速=地速-风速
### 参考文献
- Matlab官方文档
- 双无人机协同测向时差定位误差分析研究



