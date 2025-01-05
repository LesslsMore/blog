从下面OpenCV中文件移植
`E:\0-Technic\4-OpenCV\OpenCV-410\opencv-4.1.0\modules\highgui\src`
\window_QT.cpp

Qt New Functions
High-level GUI

![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105154138.png)

主要为以下功能移植：
1、	图像按鼠标所在位置进行缩放
2、	滚轮实现缩放
3、	拖动并有预览窗格
4、	缩放后仍能鼠标获取图像像素位置

class DefaultViewPort: public QGraphicsView | //,public ViewPort
-------- | -----
void DefaultViewPort::updateImage (Mat* arr) |	传入Mat图像，Qimage转换
void DefaultViewPort::resizeEvent(QResizeEvent* evnt) |	鼠标缩放事件，更新 ratioX Y
void DefaultViewPort::mousePressEvent(QMouseEvent* evnt) |	鼠标点击事件
void DefaultViewPort::mouseReleaseEvent(QMouseEvent* evnt) |	
void DefaultViewPort::mouseMoveEvent(QMouseEvent* evnt) |	
void DefaultViewPort::paintEvent(QPaintEvent* evnt) |	param_matrixWorld矩阵，重画显示图像
void DefaultViewPort::controlImagePosition() |	控制图像移动时不越界
void DefaultViewPort::moveView(QPointF delta) |	
void DefaultViewPort::scaleView(qreal factor,QPointF center) |	
void DefaultViewPort::icvmouseEvent(QMouseEvent* evnt) |	
void DefaultViewPort::icvmouseProcessing(QPointF pt, int cv_event, int flags) |	给OpenCV的GUI设置鼠标接口
void DefaultViewPort::draw2D(QPainter *painter) |	
void DefaultViewPort::drawImgRegion(QPainter *painter) |	
void DefaultViewPort::drawViewOverview(QPainter *painter) |	画缩略图

显示窗口宽高
图像行列
窗口变换矩阵	param_matrixWorld	鼠标滚轮改变时 相应 ratio 更新

```js
ratioX = width() / float(image2Draw_mat->cols);
ratioY = height() / float(image2Draw_mat->rows);
```

![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105154218.gif)

源代码链接如下
[https://download.csdn.net/download/Tom995083162/13195532](https://download.csdn.net/download/Tom995083162/13195532)

