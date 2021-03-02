---
tags: Manim
---
# 初步学习数学视频引擎Manim  
3blue1brown的数学教学视频美观优雅，离不开Manim的强力支持。
根据此篇[Manim教程](https://talkingphysics.wordpress.com/2019/01/08/getting-started-animating-with-manim-and-python-3-7/)记一下笔记.。
Manim其实是Python的一个库，可以通过写代码来实现视频的制作。
安装库的过程可真的是**烦**，从各种网站下载各种包-_-。
<br>
<!--more-->

## 生成视频
```shell
python manim.py -m test.py <classname> -pl 
```
再shell中执行命令会把你创建的类以及类的各种动作(函数)，渲染成为动画。

## 基本概念
1. ###### 导入库是当然的
```python
from manim.imports import *
```
2. ###### 定义要渲染的类
```python
class Shape(Scene):
```
注意需要继承**Scene**对象
3. ###### ```construct()```方法
```python
def construct(self):
```
4. ###### 分两步，先创建要渲染的形状，再渲染
```python
circle=Circle()
square=Square()
```
```python
self.add(circle)
self.play(FadeOut(square))
```

使用```add()```方法静态添加，```play()```方法动态渲染(需要指明动画的类型e.g. ```Transform()```，``` ShowCreation()```)

## 更多知识
### 形状
|代码|形状|
|--|--|
|Circle|圆|
|Square|正方形|
|Line|线|
|Polygon|多边形|
|Ellipse|椭圆|
|Annulus|环|
|Rectangle|矩形|
|Arrow|箭头|
|CurvedArrow|曲线箭头|
形状都会在屏幕的中心创建，线段需要特殊的指定起始点

> 在创建实例的时候可指定颜色

```python
circle=Circle().set_color(RED)
```

### 动画
|代码|动画|
|--|--|
|FadeOut|淡出|
|FadeIn|淡入|
|Rotating|旋转|
|GrowArrow|增长箭头|
|GrowFromCenter|从中心增长|
|Transform|两个形状的变化|
|ShowCreation()|显示创建动画|
<br>
**可以```self.wait(3)```来等待

### 方向向量

UP，DOWN，LEFT，RIGHT，IN，OUT
使用```move_to()```或者```shift()```方法来改变形状的初始位置

```python
circle.move_to(2*DOWN+3*LEFT)
rext.shift(2*DOWN)
```
把圆移到从中心向下两个单位，想左三个单位
**定义域是⑧，最多移动八个单位(整个屏幕)**



### 形状的定位
```circle.next_to(square,UP+RIGHT)```
```circle.surround(Rect)```

###  多个动画同时渲染

```python
play(Transform(circle,rect),FadeOut(Ellipse))
```
**用逗号隔开**

### 创建文字

还是一如既往得来创建对象
```python
text=TextMobject("This is Manim!!!")
```

### 文字的位置
```python
next_to()
to_edge()
to_corner()
```

### 文字的大小
指定大小：
```python
text.scale(0.75)
```

变换大小
```python
text.scale(.5)
####
text.scale(.25)
```
先$\times0.5$，再$\times0.25$

### 文字颜色
```python
text.set_color(GREEN)
text.set_color_by_gradient(RED,YELLOW)
```

### 文字的动画
```python
self.play(Write(text))
```

### 旋转
```python
rotate(TAU/n)
```
rotate方法指定旋转的角度，$TAU=2\pi$

### 数学公式
```python
text=TextMobject("$\\vec{F}=m\\cdot \\vec{a}$")
#或者
text=TexMobject(r"\vec{F}=m\cdot\vec{a}")##注意是TexMobject
```
或者再$\LaTeX$中插入普通字符：```\\text{}```

### 排列方程和大括号(brace)
> 注意```VGroup()```类可以用来组合多种mobject形成向量对象

在方程的渲染中主要是方程的排版
主要方法：```next_to()```和```align_to()```
```python
#next_to()
eq1B=eq1A.next_to(RIGHT)
#align_to()
eq2A=eq1A.align_to(LEFT)
```
在```align_to()```中需传入在左端还是右端对齐
<br>
最后用```VGroup(eq1A,eq2A)```来生成两个方程的联立
再用```Brace(group,LEFT)```来用大括号将其括起来
<br>
当然了，大括号前面有文字的话可以使用```get_text()```方法来添加
```python
braces.get_text("ExampSentences")
```
## 画图  
###### 基于GraphScene对象  
**重点：CONFIG{}字典**
```python
class PlotFunction(GrapgScene):
	CONFIG={
	"x_min":-10,
	"x_max":10.3,
	"y_min":-1.5,
	"y_max":1.5,
	"graph_origin":ORIGIN,
	"function_color":RED,
	"axes_color":GREEN,
	"x_label_nums":range(-10,12,2),
	}
	def construct(self):
	
```
