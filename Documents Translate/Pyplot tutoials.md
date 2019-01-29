# Pyplot tutorials
pyplot 接口介绍
## Intro to pyplot(pyplot 导读)
<a href=https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot>matplotlib.pyplot</a>是一组命令样式函数，使得matplotlib像MATLAB一样工作，每一个pyplot函数都会都图像做一些改动，例如，创建图形，在图形中创建绘图区域，在绘图区域绘制线条，使用标签来装饰图形等等。
在调用matplotlib.pyplot函数时，图像的各种状态都会保存，所以从始至终它都会一直跟踪当前图形和绘图区域，绘图函数也都指向当前的坐标轴（`axis`）,<font color='red'>**需要注意的是，这里和我们文档大部分地方的'axis'都指的是所绘制图形的轴部分，而不是多个坐标轴的严格的数学术语</font>。

> Note:我们这里面讲的pyplot接口（API）没有面向对象接口灵活，您在这里面看到的绝大部分函数调用都可以作为Axes对象方法调用，我们建议您浏览教程和示例以了解其工作原理。  

使用matplotlib生成可视化的图像非常容易，看看如下代码：   
```python   
import matplotlib.pyplot as plt   
plt.plot([1,2,3,4])
plt.ylabel('some numbers')   
plt.show()
```
<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_001.webp/>   
您可能很好奇为什么x轴的范围是0-3，而y轴的范围是1-4，如果您只为plot()函数传入单个列表和数组，matplotlib就假定它是一组y的值，并自动为您生成x轴，由于Python中的范围一般是以0开头，所以虽然x与y的长度相同，但是却是以0开头，因此x的值是[0,1,2,3]   
plot()是一个功能强大的函数，可以以任意数字作为参数，例如，如果需要绘制x与y的关系图，您可以发出命令：   

```python   
plt.plot([1,2,3,4],[1,4,9,16])   
```
<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_002.webp/>   
## (Formatting the style of your  plot)格式化图形样式
对于每一对xy参数，都有一个可供选择的第三个参数，是一个用来指定颜色和线条类型的*格式化字符串*，格式化字符串的字母与数字都是来自MATLAB，您可以把代表颜色的字符串和代表拍线条样式的字符串连接（concatenate）在一起，默认的字符串格式是'b-'，它代表的是一条红色的实线。例如，您可以使用红色的圆圈来重新画一下上面的图形：

```python
plt.plot([1,2,3,4],[1,4,9,16],'ro')
plt.axis([0,6,0,20])
plt.show()
```
<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_003.webp>
有关plot()线条类型和相对应的格式字符串的完整列表，请参阅 [plot()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot) 的官方文档,上面例子中的axis()命令以一个列表[xmin,xmax,ymin,ymax]为参数，用来指定图中xy轴的可视范围。如果matplotlib仅限于使用列表，那么它对于数字处理来说将变得毫无用处。通常情况下，您都可以使用numpy 矩阵，事实上，所有的序列都会在matplotlib的内部被转换成numpy矩阵，下面的一个例子演示了使用矩阵和一个pyplot命令绘制的多个样式不同的线条。

```python
import numpy as np

t = np.arange(0,5,0.2)
plt.plot(t,t,'r--',t,t**2,'bs',t,t**3,'g^')
plt.show()
```

<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_004.webp/>

## Plotting with keyword strings(使用关键字字符串绘图)

在某些情况下，有时候您的数据是需要通过字符串来获取变量的格式，比如说numpy.recarry或者是numpy.DataFrame.

matplotlib允许您使用data关键字来提供这样的一个对象，如果条件允许的话（格式正确），你可以通过这些字符串来访问相对应的字符串，进而绘制图形。

```python
data = {'a':np.arange(50),
         'c':np.random.randint(0,50,50),
         'd':np.random.randn(50)}
data['b'] = data['a']+10*np.random.randn(50)
data['d']=np.ads(data['d'])*100

plt.scatter('a','b',c='c',s='d',data=data)
plt.xlabel('entry a')
plt.ylabel('entry b')
plt.show()
```

<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_005.webp/>

## Plotting with categorical variables(使用分类变量绘图)

在matplotlib中，您也可以使用分类变量来进行绘图，Matplotlib允许您直接将分类变量直接传给许多绘图函数，例如：

```python
names = ['group_a','group_b','group_c']
values = [1,10,100]

plt.figure(1,figsize=(9,3))

plt.subplot(131)
plt.bar(names,values)
plt.subplot(132)
plt.scatter(names,values)
plt.subplot(133)
plt.plot(names,values)
plt.subtitle('Categorical Plotting')
plt.show()
```

<img width=750 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_006.webp/>

## Controlling line propertities(控制线条属性)

在matplotlib里线条有各种属性，这些属性我们都可以进行设置：linewidth,dash style, antialiased等等，更多属性，查阅[matplotlib.lines.line2D](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D),我们在这里提供了多种方法来设置这些线条属性。

* 使用关键字参数（keyword args）   

```python
plt.plot(x,y,linewidth=2.0)
```

* 使用line2D实例的setter方法，plot会返回一个line2D对象的列表；例如，`line1,line2 = plot(x1,y1,x2,y2)`，在下面的代码中，我们假设只有一条线，所以返回的列表长度为1，我们对line使用tuple unpacking来获取列表当中的第一个元素。

```python
line, = plt.plot(x,y,'-')
line.set_antialiased(False)
```

* 使用 [setp](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.setp.html#matplotlib.pyplot.setp) 命令，下面的一个例子中，我们使用了MATLAB风格的命令来对一系列的线条设置多个属性，setp”透明地“处理一个对象列表或者是一个对象，你既可以使用keyword args（关键字参数），也可以使用MATLAB风格的（字符串/值）对：

```python
lines = plt.plot(x1,y1,x2,y2)
plt.setp()
#使用关键字参数
plt.setp(lines,color='r',linewidth=2.0)
#MATLAB风格
plt.setp(lines,'color','r','linewidth',2.0)
```

以下是一些可用的line2D属性

| Property               | Value Type                                                |
| ---------------------- | :-------------------------------------------------------- |
| alpha                  | float                                                     |
| animated               | [True \| False]                                           |
| antialiased or aa      | [True \| False]                                           |
| clip_box               | a matplotlib.transform.Bbox instance                      |
| clip_on                | [True \| False]                                           |
| clip_path              | a Path instance and a Transform instance, a Patch         |
| color or c             | any matplotlib color                                      |
| contains               | the hit testing function                                  |
| dash_capstyle          | [`'butt'` | `'round'` | `'projecting'`]                   |
| dash_joinstyle         | [`'miter'` | `'round'` | `'bevel'`]                       |
| dashes                 | sequence of on/off ink in points                          |
| data                   | (np.array xdata, np.array ydata)                          |
| figure                 | a matplotlib.figure.Figure instance                       |
| label                  | any string                                                |
| linestyle or ls        | [ `'-'` | `'--'` | `'-.'` | `':'` | `'steps'` \| ...]     |
| linewidth or lw        | float value in points                                     |
| lod                    | [True \| False]                                           |
| marker                 | [ `'+'` | `','` | `'.'` | `'1'` | `'2'` | `'3'` | `'4'` ] |
| markeredgecolor or mec | any matplotlib color                                      |
| markeredgewidth or mew | float value in points                                     |
| markerfacecolor or mfc | any matplotlib color                                      |
| markersize or ms       | float                                                     |
| markevery              | [ None \| integer \| (startind, stride) ]                 |
| picker                 | used in interactive line selection                        |
| pickradius             | the line pick selection radius                            |
| solid_capstyle         | [`'butt'` | `'round'` | `'projecting'`]                   |
| solid_joinstyle        | [`'miter'` | `'round'` | `'bevel'`]                       |
| transform              | a matplotlib.transforms.Transform instance                |
| visible                | [True \| False]                                           |
| xdata                  | np.array                                                  |
| ydata                  | np.array                                                  |
| zorder                 | any number                                                |

如果要获取可设置的属性列表，只要line2D对象作为set()函数的参数即可

```python
lines = plt.plot([1,2,3])
plt.setp(lines)
  alpha: float
  animated: bool
  antialiased: bool
    ...
```

## Working with multiple figures and axes(使用多个窗口和轴绘图)

MATLAB和matplotlib都有"当前图形"和"当前轴"的概念，所有的绘图命令都作用在哪当前轴上，gca()(matplotlib.axes.Axes 实例对象)函数把当前轴作为返回值，gcf()(matplotlib.figure.Figure 实例对象)，把当前图像作为返回值，通常情况你不必为此而担心，因为这所有的一切都在幕后进行，下面是一个创建了两个子图的脚本：

```python
def f(t):
    return np.exp(-t),np.cos(2*np.pi*t)

t1 = np.arange(0.0,5.0,0.1)
t2 = np.arange(0.0,5.0,0.02)

plt.figure(1)
plt.subplot(2,1,1)
plt.plot(t1,f(t1),'bo',t2,f(t2),'k')

plt.subplot(2,1,2)
plt.plot(t2,np.cos(2*np.pi*t2),'r--')
plt.show()
```
<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_007.webp/>




## Working with text(使用文本)

`text()`命令可以在任意位置添加文本，`xlabel`,`ylabel`,`title`则被用来在指定的位置添加文本(更多内容尽在[Text in Matplotlib Plots](https://matplotlib.org/tutorials/text/text_intro.html),里面有更加详细的关于text的例子)

```python
mu, sigma = 100,15
x = mu + sigma*np.random.randn(10000)

#绘制直方图(histogram)
n,bins,patches = plt.hist(x,50,density=1,facecolor='g',alpha=0.75)

plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title('Histogram of IQ')
plt.text(60,0.025,r'$\mu=100,\ \sigma=15$')
plt.axis([40,160,0,0.03])
plt.grid(True)
plt.show()
```

<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_008.webp/>

所有的`text()`命令都返回一个matplotlib.text.Text的实例对象，就和上面讲的线条属性一样，你也可以通过在`text()`函数里使用关键字参数（keyword args）来自定义属性，或者是使用`setp()`

```python
t = plt.xlabel('my data',fontsize=14,color='red')
```

[Text properties and layout](https://matplotlib.org/tutorials/text/text_props.html) 中更详细地介绍了这些属性

### (Using mathematical expressions in text)在文本中使用数学表达式

matplotlib在任何的文本表达式中都支持TeX方程表达式，例如如果你想要在标题中写出表达式 
$$
\sigma_i = 15
$$
你可以编写一个由两个美元$符号包裹起来的TeX表达式：

```python
plt.title(r'$\sigma_i = 15$')
```

需要注意的是，表达式最前面的一个字母‘r’很关键，这意味着这是一个原始字符串（raw string），所以反斜杠不被当成Python当中的逃逸特殊符号的特使特殊功能，matplotlib有一套内置的TeX解释器和布局引擎，并提供自己的字体，详情请参见[Writing mathematical expression](https://matplotlib.org/tutorials/text/mathtext.html) ；因此即使你的电脑上没有下载TeX，你也可以跨平台地使用这些数学表达式。

### Annotating text(注释文本)

从上面的例子中，我们可以看出，`text()`命令的基本用法就是在将一串文本放在整个Axes的任意位置上，文本还有一个常见用法是对图上的某个特殊部分进行注释，`annotate()`方法提供一种辅助函数功能使这些注释变得很简单，在注释中，有两个点需要考虑，参数xy表示需要注释的点的位置，xytext表示注释文本的位置，两个参数都是(x,y)元组

```python
ax = plt.subplot(111)

t = np.arange(0.0,0.5,0.01)
s = np.cos(2*np.pi*t)
line, = plt.plot(x,y,lw=2)

plt.annotate('local max',xy=(2,1),xytext=(3,1.5),
            arrowprops=dict(facecolor='black',shrink=0.05))

plt.ylim(-2,2)
plt.show()
```

<img width=450 height=350 src=https://github.com/laiangpuao/matplotlib/blob/master/image/Pyplot%20Tutorial/sphx_glr_pyplot_009.webp/>

在这个基本的例子中，xy(箭头提示)和xytext(文本位置)都在数据坐标(Data coordinates)中，你也可以选择各种其他的坐标系统，更多内容[Base Annotation](https://matplotlib.org/tutorials/text/annotations.html#annotations-tutorial),   [Advanced Annotation](https://matplotlib.org/tutorials/text/annotations.html#plotting-guide-annotation),  你也可以在[Annotating Plots](https://matplotlib.org/gallery/text_labels_and_annotations/annotation_demo.html)中找到更多关于注释的例子。
