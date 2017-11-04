# CSS & CSS3

标签： 模拟面试

---

## 1.如何实现垂直居中?

> 为实现良好的兼容性，PC端实现垂直居中的方法一般是通过绝对定位，`table-cell`，负边距等方法。

```
 // HTML结构：
<div class="box box1">
    <span>垂直居中</span>
</div>
```

* 方法1：table-cell

```
// CSS:
.box1{
    display: table-cell;
    vertical-align: middle;
    text-align: center;        
}
```
* 方法2：display:flex
```
.box2{
    display: flex;
    justify-content:center; // 主轴
    align-items:Center;  // 交叉轴
}
```
* 方法3：绝对定位和负边距
```
.box3{position:relative;}
.box3 span{
    position: absolute;
    width:100px;
    height: 50px;
    top:50%;
    left:50%;
    margin-left:-50px;
    margin-top:-25px;
    text-align: center;
}
```
* 方法4：绝对定位和0
```
.box4 span{
  width: 50%; 
  height: 50%; 
  background: #000;
  overflow: auto; 
  margin: auto; 
  position: absolute; 
  top: 0; left: 0; bottom: 0; right: 0; 
}
```
* 方法5：translate
```
.box6 span{
    position: absolute;
    top:50%;
    left:50%;
    width:100%;
    transform:translate(-50%,-50%);
    text-align: center;
}
```
* 方法6：display:inline-block
```
.box7{
  text-align:center;
  font-size:0;
}
.box7 span{
  vertical-align:middle;
  display:inline-block;
  font-size:16px;
}
.box7:after{
  content:'';
  width:0;
  height:100%;
  display:inline-block;
  vertical-align:middle;
}
```
* 方法7：display:flex和margin:auto
```
.box8{
    display: flex;
    text-align: center;
}
.box8 span{margin: auto;}
```
* 方法8：display:-webkit-box
```
.box9{
    display: -webkit-box;
    -webkit-box-pack:center;
    -webkit-box-align:center;
    -webkit-box-orient: vertical;
    text-align: center
}
```
* 方法9：display:-webkit-box
```
<div class="floater"></div>  
<div class="content"> Content here </div>  

// CSS
.floater {
    float:left; 
    height:50%; 
    margin-bottom:-120px;
}
.content {
    clear:both; 
    height:240px; 
    position:relative;
}
```
## 2. 什么是FOUC?如何解决？

> 如果使用import方法对CSS进行导入,会导致某些页面在Windows 下的Internet Explorer出现一些奇怪的现象:以无样式显示页面内容的瞬间闪烁,这种现象称之为文档样式短暂失效(Flash of Unstyled Content),简称为FOUC。

* 原因大致为：

> 1，使用import方法导入样式表。
2，将样式表放在页面底部
3，有几个样式表，放在html结构的不同位置。

其实原理很清楚：当样式表晚于结构性html加载，当加载到此样式表时，页面将停止之前的渲染。此样式表被下载和解析后，将重新渲染页面，也就出现了短暂的花屏现象。

* 解决方法：
> 使用LINK标签将样式表放在文档HEAD中;或将css文件放在CDN服务器上。

```
<link rel="stylesheet" href="style.css">
```

## 3. 什么是DIV高度塌陷？，如何解决？

* 如果父元素只包含浮动元素，且父元素未设置高度和宽度，那么它的高度就会塌缩为零，也就是所谓的“高度塌陷”。

> 解决“高度塌陷”问题的方法：

1.浮动父级元素，父级元素的高度就会扩大，直到完全包含它里面的浮动元素。如果使用这种方法，一定要在该元素的下个元素添加`clear:both`,确保浮动元素落到父级元素的下方。 

2.使用`overflow:hidden,zoom:1`,`overflow:hidden`属性会强制父级元素扩大到包含浮动元素，`zoom:1`只是触发IE6的`hasLayout`模式，不会对其他浏览器产生影响。
```
{ 
　　overflow:hidden; 
　　zoom:1; 
}
```

3.使用`:after`伪类清除，不会影响其他任何样式，通用性强。
```
.clearfix{ 
　　zoom:1; 
} 
.clearfix:after{ 
　　content:''; 
　　display:block; 
　　height:0; 
　　clear:both; 
　　overflow:hidden; 
}
```

## 4、如何实现中间div宽度固定，两端div自适应宽度？说出2种方法
* float法

> 通过使两边的div左右浮动，脱离文档流，再为中间的div设置margin-left,margin-right值为左右div的宽度即可.此处应该注意的是中间div在代码中的位置，应该放在最后。存在问题：在屏幕宽度减少至一定程度后，右边div会错位，另起一行。
```
/*float法*/
.float .left {
    float: left;
    height: 200px;
}
.float .center {
    margin: 0 400px;
    height: 200px;
}
.float .right {
    float: right;
    height: 200px;
}
```

* display:flex法

```
<style type="text/css">
    .container{
        width: 100%;
        height: 500px;
        display: flex;
    }
    .div01,.div03{
        background: black;
        flex: auto;
    }
    .div02{
        background: red;
        width: 220px;
    }
  </style>  

<div class="container">
    <div class="div01"></div>
    <div class="div02"></div>
    <div class="div03"></div>
</div>


// 使用"display: flex"声明使用弹性盒布局。
        
        
//  CSS 属性声明"flex-direction"用来确定主轴的方向:
// row（默认值）主轴为水平方向。排列顺序与页面的文档顺序相同。如果文档顺序是 ltr，则排列顺序是从左到右；如果文档顺序是rtl，则排列顺序是从右到左。
// row-reverse	主轴为水平方向。排列顺序与页面的文档顺序相反。
// column	主轴为垂直方向。排列顺序为从上到下。
// column-reverse	主轴为垂直方向。排列顺序为从下到上。

        
// CSS 属性"flex-wrap"用来声明当容器中条目的尺寸超过主轴尺寸时应采取的行为。
// nowrap（默认值）容器中的条目只占满容器在主轴方向上的一行，可能出现条目互相重叠或超出容器范围的现象。
// wrap	当容器中的条目超出容器在主轴方向上的一行时，会把条目排列到下一行。下一行的位置与交叉轴的方向一致。
// wrap-reverse	与wrap的含义类似，不同的是下一行的位置与交叉轴的方向相反。
```




