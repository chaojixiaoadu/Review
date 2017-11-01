# DOM复习

标签（空格分隔）： 复习

---
### DOM简介
> DOM（ Document Object Module）是针对HTML和XML文档的一个API（应用程序接口）。

1998年DOM1规范成为W3C的推荐标准。

![DOM树][1]
  [1]: http://www.runoob.com/images/htmltree.gif
                    DOM树

### Node类型

 - 常用节点的NodeType,节点类型
> 元素节点  >>>> 1
属性节点 >>>> 2
文本节点 >>>> 3
注释节点 >>>> 8
文档节点 >>>> 9

 - 常用节点的NodeName,【只读】
 > 元素节点的NodeName与标签名相同;
属性节点的NodeName与属性名相同;
文本节点的NodeName始终是#text;
文档节点的NodeName始终是#document;
 
 - 常用节点的NodeValue,【节点值】
 > 元素节点的NodeValue是undefined或null;
文本节点的NodeValue是文本本身;
属性节点的NodeValue是属性值;

### 伪数组转换数组【arguments】
```
function toArray(nodes) {
        var array = null;
        try {
            aray = Array.prototype.slice.call(nodes, 0); // 针对非IE浏览器
        } catch (err) {
            array = new Array();
            for (var i = 0; i < nodes.length; i++) {
                array.push(nodes[i]);
            }
        }
        return;
}
```
> 通过`try-catch`块来捕获错误!

### 操作节点
> 
`appendChild()`	把新的子节点添加到指定节点。
`removeChild()`	删除子节点。
`replaceChild()`	替换子节点。
`insertBefore()`	在指定的子节点前面插入新的子节点。
`cloneNode()`       克隆节点,这个方法只复制特性!

### Document 类型
> document对象是HTMLDocument的一个实例,表示整个HTML页面。

#### 查找元素
* 参数区分大小写!!
>`getElementById()`	返回带有指定 ID 的元素。
`getElementsByTagName()`	返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。
`getElementsByName()` 返回包含带有指定name的所有元素的节点列表（集合/节点数组）。
`getElementsByClassName()`	返回包含带有指定类名的所有元素的节点列表。【H5后添加】

### Element 类型

> Element 类型通常用于变现HTML元素,提供对元素标签名,子节点及特性访问。

#### HTML元素

> 五个可以直接`.`的元素:id,title,lang,dir,className

#### attribute 方法

* getAttribute(),setAttribute(),removeAttribute()

> `createAttribute()`	创建属性节点。
`createElement()`	创建元素节点。
`createTextNode()`	创建文本节点。
`getAttribute()`	返回指定的属性值。
`setAttribute()`	把指定属性设置或修改为指定的值。

#### DocumentFragment 属性
* 在所有节点类型中,只有DocumentFragment在文档中没有对应的标记。

> nodeType 的值为 11;
nodeName 的值为 #document-fragment;
nodeValue 的值为 null;

* 不能把文档片段直接添加到文档中,但可以将它作为一个仓库来使用。

```
var fragment = document.createDocumentFragment();
    var ul = document.getElementById('ul');
    for (var i = 0; i < 5; i++) {
        var li = document.createElement('li');
        li.appendChild(document.createTextNode('i' + (i + 1)));
        fragment.appendChild(li);
}
    ul.appendChild(fragment);
```
### DOM操作技术

#### 动态脚本

```
function loadscript(url){
    var script =  document.createElement("script");
    script.type = "text/javascript";
    script.src = url;
    document.body.appendChild(script);
}
```

#### 动态样式

```
function loadStyles(url) {
    var link = document.createElement('link');
    link.rel = 'stylesheet';
    link.type = 'text/css';
    link.href = url;
    var head = document.getElementsByTagName('head')[0];
    head.appendChild(link);
}
```

## DOM扩展【querySelector()】
    
    #### 自定义数据属性
    
> HTML5 规定可以为元素添加非标准的属性,但要加前缀 `data-` 。



