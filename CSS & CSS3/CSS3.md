# CSS3

标签： 复习

---

## @font-face 规则

```
<style> 
@font-face{
    font-family: myFirstFont;   // 必须首先定义字体的名称
    src: url('Sansation_Light.ttf'),
         url('Sansation_Light.eot'); /* IE9+ */
}

div{
    font-family:myFirstFont;
}
</style>
```

## 2D 转换

### translate() 方法
> 通过 `translate()` 方法，元素从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标） 位置参数：

```
//  把元素从左侧移动 50 像素，从顶端移动 100 像素。
div {
    transform: translate(50px,100px);
    -ms-transform: translate(50px,100px);		/* IE 9 */
    -webkit-transform: translate(50px,100px);   /* Safari and Chrome */
    -o-transform: translate(50px,100px);		/* Opera */
    -moz-transform: translate(50px,100px);		/* Firefox */
}
```
### rotate() 方法

> 通过 `rotate()`方法，元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转。

```
//  把元素顺时针旋转 30 度。
div {
    transform: rotate(30deg);
    -ms-transform: rotate(30deg);		/* IE 9 */
    -webkit-transform: rotate(30deg);	/* Safari and Chrome */
    -o-transform: rotate(30deg);		/* Opera */
    -moz-transform: rotate(30deg);		/* Firefox */
}
```

### scale() 方法

> 通过 `scale()` 方法，元素的尺寸会增加或减少，根据给定的宽度（X 轴）和高度（Y 轴）参数：

```
// 把宽度转换为原始尺寸的 2 倍，把高度转换为原始高度的 4 倍。
div {
    transform: scale(2,4);
    -ms-transform: scale(2,4);	/* IE 9 */
    -webkit-transform: scale(2,4);	/* Safari 和 Chrome */
    -o-transform: scale(2,4);	/* Opera */
    -moz-transform: scale(2,4);	/* Firefox */
}
```

### skew() 方法

> 通过 skew() 方法，元素翻转给定的角度，根据给定的水平线（X 轴）和垂直线（Y 轴）参数：

```
// 围绕 X 轴把元素翻转 30 度，围绕 Y 轴翻转 20 度。
div {
    transform: skew(30deg,20deg);
    -ms-transform: skew(30deg,20deg);	/* IE 9 */
    -webkit-transform: skew(30deg,20deg);	/* Safari and Chrome */
    -o-transform: skew(30deg,20deg);	/* Opera */
    -moz-transform: skew(30deg,20deg);	/* Firefox */
}
```

### matrix() 方法

> `matrix()` 方法把所有 2D 转换方法组合在一起。
`matrix()` 方法需要六个参数，包含数学函数，允许：旋转、缩放、移动以及倾斜元素。

```
div {
    transform:matrix(0.866,0.5,-0.5,0.866,0,0);
    -ms-transform:matrix(0.866,0.5,-0.5,0.866,0,0);		/* IE 9 */
    -moz-transform:matrix(0.866,0.5,-0.5,0.866,0,0);	/* Firefox */
    -webkit-transform:matrix(0.866,0.5,-0.5,0.866,0,0);	/* Safari and     Chrome */
    -o-transform:matrix(0.866,0.5,-0.5,0.866,0,0);		/* Opera */
}
```

## 3D转换

### rotateX() 方法,rotateY() 方法

> 通过 `rotateX()` 方法，元素围绕其 X 轴以给定的度数进行旋转。
通过 rotateY() 方法，元素围绕其 Y 轴以给定的度数进行旋转。

```
// 围绕 X 轴旋转 120度。
div {
    transform: rotateX(120deg);
    -webkit-transform: rotateX(120deg);	/* Safari 和 Chrome */
    -moz-transform: rotateX(120deg);	/* Firefox */
}
```

## 过渡

> CSS3 过渡是元素从一种样式逐渐改变为另一种的效果。

* 要实现这一点，必须规定两项内容：

> 规定您希望把效果添加到哪个 CSS 属性上;
规定效果的时长

```
// 用于宽度属性的过渡效果，时长为 2 秒：
div {
    transition: width 2s;
    -moz-transition: width 2s;	/* Firefox 4 */
    -webkit-transition: width 2s;	/* Safari 和 Chrome */
    -o-transition: width 2s;	/* Opera */
}
```

> `transition`	简写属性，用于在一个属性中设置四个过渡属性。	
`transition-property`	规定应用过渡的 CSS 属性的名称。	
`transition-duration`	定义过渡效果花费的时间。默认是 0。	
`transition-timing-function`	规定过渡效果的时间曲线。默认是 "ease"。
//============================================
`linear`	规定以相同速度开始至结束的过渡效果
`ease`	规定慢速开始，然后变快，然后慢速结束的过渡效果
`ease-in`	规定以慢速开始的过渡效果。
`ease-out`	规定以慢速结束的过渡效果。
`ease-in-out`	规定以慢速开始和结束的过渡效果。
`cubic-bezier(n,n,n,n)` 在cubic-bezier函数中定义自己的值。可能的值是 0 至 1 之间的数值。
//============================================
`transition-delay`	规定过渡效果何时开始。默认是 0。

```
div {
    transition-property: width;
    transition-duration: 1s;
    transition-timing-function: linear;
    transition-delay: 2s;
}
```