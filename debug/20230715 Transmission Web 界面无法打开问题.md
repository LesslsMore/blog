![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153800.png)

404: Not Found
Couldn't find Transmission's web interface files!

Users: to tell Transmission where to look, set the TRANSMISSION_WEB_HOME environment variable to the folder where the web interface's index.html is located.

Package Builders: to set a custom default at compile time, `#define PACKAGE_DATA_DIR in libtransmission/platform.c` or tweak tr_getClutchDir() by hand.

### 解决方法
安装时未选择相应功能  
注意先设置安装路径到 D 盘  
再选择 Web interface  
不然会默认安装到 C 盘

![](https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250105153820.png)
