#  CPU和GPU

## CPU和GPU工作流程

APP主线程开始在CPU中计算显示内容，比如视图的创建、布局计算、图片解码、文本绘制等。随后CPU将计算好的内容提交给GPU，有GPU进行变换、合成、渲染。随后GPU会把渲染好的结果提交到帧缓冲区中，等下一次Vsync信号到来时显示到屏幕上。

## 界面卡顿的原因

由于垂直同步信号机制，在一个Vsync时间内，CPU或GPU没有完成内容提交，则那一帧会被丢弃，等待下一次机会显示，而这时显示屏会保留之前内容不变。这就是界面卡顿的原因

界面卡顿原因在两个方面：CPU 和 GPU 。

## CPU资源消耗原因和解决方案


* 用轻量级对象代替重量的对象。例如：在不需要交互视图使用CALayer代替UIView。
* 避免使用Storyboard创建界面，因为消耗资源比代码要多。
* 尽量复用对象，缓解重复创建和销毁的开销。
* 避免频繁调整对象。
* 视图布局计算，Autolayout用性能问题。

## GPU资源消耗原因和解决方案

* 纹理的渲染，避免在短时间内大量显示图片，尽可能将多张图片合成一张显示
* 视图的混合，GPU会将重叠的视图混合比较耗GPU资源，尽量减少视图数量和层次。
* CALayer的border、圆角、阴影等会触发离屏渲染，尽量使用带圆角的图片替换。


# 库

* [Texture](http://texturegroup.org/docs/getting-started.html)


# 参考

* [iOS 保持界面流畅的技巧](https://blog.ibireme.com/2015/11/12/smooth_user_interfaces_for_ios/)
