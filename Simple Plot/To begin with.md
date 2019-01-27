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

### 1.4.2.2. Instantiating defaults
在下面的代码中，我们把一些影响我们画图的一些默认设置列了出来（都用#符号注释了）。  
这些设置都明确地设置成了自己的默认模式，但是现在我们可以交互地改变这些值来看一下效果。
（）
```.py
import numpy as np
import matplotlib.pyplot as plt

# Create a figure of size 8x6 inches, 80 dots per inch
plt.figure(figsize=(8, 6), dpi=80)

# Create a new subplot from a grid of 1x1
plt.subplot(1, 1, 1)

X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
C, S = np.cos(X), np.sin(X)

# Plot cosine with a blue continuous line of width 1 (pixels)
plt.plot(X, C, color="blue", linewidth=1.0, linestyle="-")

# Plot sine with a green continuous line of width 1 (pixels)
plt.plot(X, S, color="green", linewidth=1.0, linestyle="-")

# Set x limits
plt.xlim(-4.0, 4.0)

# Set x ticks
plt.xticks(np.linspace(-4, 4, 9, endpoint=True))

# Set y limits
plt.ylim(-1.0, 1.0)

# Set y ticks
plt.yticks(np.linspace(-1, 1, 5, endpoint=True))

# Save figure using 72 dots per inch
# plt.savefig("exercice_2.png", dpi=72)

# Show result on screen
plt.show()
```
> 小提示：官方文档
> .[Customizing matplotlib](http://matplotlib.org/users/customizing.html)


### 1.4.2.3. Changing colors and line widths
第一步，我们想把cos函数图像变成蓝色，把sin函数图像换成红色，然后把两条线都变粗一点。  
最后，我们稍微改变一下图像的大小，让函数图像和之前看起来更平一点。
```.py
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-np.pi,np.pi,256,endpoint=True)
y1,y2 = np.sin(x),np.cos(x)

plt.figure(figsize=(10,6),dpi=80)
plt.plot(x,y1,color='red',linewidth=2.5,linestyle='-')
plt.plot(x,y2,color='blue',linewidth=2.5,linestyle='-')

plt.show()
```
<center>
  <img width=400 height=300 title="图1.4.2.3" src=https://github.com/laiangpuao/matplotlib/blob/master/image/1.4.2.3.png/>
</center>
