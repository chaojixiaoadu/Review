# HTML5

标签： 复习

---

## HTML5 简介

> 为 HTML5 建立的一些规则：
新特性应该基于 HTML、CSS、DOM 以及 JavaScript。
减少对外部插件的需求（比如 Flash）;
更优秀的错误处理;
更多取代脚本的标记;
HTML5 应该独立于设备;
开发进程应对公众透明;

* 新特性

> HTML5 中的一些有趣的新特性：
用于绘画的 canvas 元素;
用于媒介回放的 video 和 audio 元素;
对本地离线存储的更好的支持;
新的特殊内容元素，比如 `article`、`footer`、`header`、`nav`、`section`;
新的表单控件，比如 `calendar`、`date`、`time`、`email`、`url`、`search`;

## 拖放

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>HTML5 拖放</title>
    <style type="text/css">
        #div1, #div2 {
            float: left;
            width: 198px;
            height: 66px;
            margin: 10px;
            padding: 10px;
            border: 1px solid #aaaaaa;
        }
    </style>
    <script type="text/javascript">
        function allowDrop(ev) {
            ev.preventDefault();
        }

        function drag(ev) {
            ev.dataTransfer.setData("Text", ev.target.id);
        }

        function drop(ev) {
            ev.preventDefault();
            var data = ev.dataTransfer.getData("Text");
            ev.target.appendChild(document.getElementById(data));
        }
    </script>
</head>
<body>

<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
    <img src="http://www.w3school.com.cn/i/eg_dragdrop_w3school.gif" draggable="true" ondragstart="drag(event)" id="drag1"/>
</div>
<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>

</body>
</html>
```

* 把 `draggable` 属性设置为 `true` 设置元素为可拖放;

```
<img draggable="true" />
```

* `ondragstart` 属性调用了一个函数，`drag(event)`，它规定了被拖动的数据。`dataTransfer.setData()` 方法设置被拖数据的数据类型和值：

```
function drag(ev){
    ev.dataTransfer.setData("Text",ev.target.id);
}
```

* `ondragover` 事件规定在何处放置被拖动的数据。通过调用 `ondragover` 事件的 `event.preventDefault()` 方法：

```
event.preventDefault()
```

* 当放置被拖数据时，会发生`drop`事件。`ondrop`属性调用了一个函数，`drop(event)`：

```
function drop(ev){
    ev.preventDefault();
    var data=ev.dataTransfer.getData("Text");
    ev.target.appendChild(document.getElementById(data));
}
```

* 代码解释：

> 调用 `preventDefault()` 来避免浏览器对数据的默认处理（`drop` 事件的默认行为是以链接形式打开）
通过 `dataTransfer.getData("Text")` 方法获得被拖的数据。该方法将返回在 `setData()` 方法中设置为相同类型的任何数据。
被拖数据是被拖元素的 `id ("drag1")`
把被拖元素追加到放置元素（目标元素）中

## HTML 5 应用程序缓存

> HTML5 引入了应用程序缓存，这意味着web应用可进行缓存，并可在没有因特网连接时进行访问。

* 应用程序缓存为应用带来三个优势：

> 离线浏览 - 用户可在应用离线时使用它们
速度 - 已缓存资源加载得更快
减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。

* 实例

> 如需启用应用程序缓存，在文档的 <html> 标签中包含 manifest 属性：

```
<!DOCTYPE HTML>
<html manifest="demo.appcache">

<body>
The content of the document......
</body>

</html>
```
### Manifest 文件

> manifest 文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。

* manifest 文件可分为三个部分：

> CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存
NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存
FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）

* 完整的manifest文件

```
CACHE MANIFEST    // CACHE MANIFEST，是必需的：
# 2012-02-21 v1.0.0
/theme.css   // 无论用户何时与因特网断开连接，这些资源依然是可用。
/logo.gif
/main.js

NETWORK:   // NETWORK小节规定文件永远不会被缓存,且离线时是不可用的
login.asp

FALLBACK:
/html5/ /404.html    // 第一个 URI 是资源，第二个是替补。
```

* 更新缓存

> 一旦应用被缓存，它就会保持缓存直到发生下列情况：
用户清空浏览器缓存
manifest 文件被修改
由程序来更新应用缓存

* 注意:
    * 一旦文件被缓存，则浏览器会继续展示已缓存的版本，即使修改了服务器上的文件。为了确保浏览器更新缓存，需要更新 manifest 文件。
    * 浏览器对缓存数据的容量限制可能不太一样（某些浏览器设置的限制是每个站点 5MB）。