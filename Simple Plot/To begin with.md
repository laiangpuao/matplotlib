## Simple Plot
在这一小节中，我们将要绘制sin函数和cos函数的简单图像，从默认的设置开始，然后慢慢丰富和美化我们的图形，让它们看起来更符合我们的审美。
第一步就是为我们的sin和cos函数定义数据：

```.py
import numpy as np
x = linspace(-np.pi,np.pi,256,endpoint=True)
y1,y2 = np.sin(x),np.cos(x)
```
现在x是一个拥有从-π到+π之间的256个数值的numpy数组，y1是x当中每一个对应值的sin函数值组成的numpy数组，y2则是cos函数值组成的numpy数组

### 1.4.2.1 Plotting with default settings
matplotlib 附带了一系列的默认设置，这也允许我们自定义所有属性，你可以控制你可以控制matplotlib中的所有属性：图像大小、分辨率，线条宽度、颜色，和样式，坐标轴、坐标和网格属性，文本和字体等等。

```.py
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-np.pi,np.pi,256,endpoint=True)
y1,y2 = np.sin(x),cos(x)

plt.plot(x,y1)
plt.plot(x,y2)

plt.show()
```
<center>
<img width=300 heigh=300 title='图1.4.2.1' src="https://github.com/laiangpuao/matplotlib/blob/master/image/1.4.2.1.png"/>
</center>

> 小提示:官方文档
> - [plot tutorial](http://matplotlib.org/users/pyplot_tutorial.html)
> - [plot() command](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot)


