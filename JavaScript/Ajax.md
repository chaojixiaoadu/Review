# Ajax

标签： 复习

---

## 创建 XMLHttpRequest 对象

    XMLHttpRequest 用于在后台与服务器交换数据。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

```
var xmlhttp;
if (window.XMLHttpRequest){
// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
}else {
// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
```

## 向服务器发送请求

    将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法：
    
```
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```
<table class="dataintable">
<tbody><tr>
<th style="width:40%;">方法</th>
<th>描述</th>
</tr>

<tr>
<td>open(<i>method</i>,<i>url</i>,<i>async</i>)</td>
<td>
	<p>规定请求的类型、URL 以及是否异步处理请求。</p>
	<ul class="listintable">
	<li><i>method</i>：请求的类型；GET 或 POST</li>
	<li><i>url</i>：文件在服务器上的位置</li>
	<li><i>async</i>：true（异步）或 false（同步）</li>
	</ul>
	</td>
</tr>

<tr>
<td>send(<i>string</i>)</td>
<td>
	<p>将请求发送到服务器。</p>
	<ul class="listintable">
	<li><i>string</i>：仅用于 POST 请求</li>
	</ul>
</td>
</tr>
</tbody></table>

> GET 还是 POST？


    与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。然而，在以下情况中，请使用 POST 请求：
    
* 无法使用缓存文件（更新服务器上的文件或数据库）
* 向服务器发送大量数据（POST 没有数据量限制）
* 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

### GET 请求

    通过 GET 方法发送信息，请向 URL 添加信息：
    
```
xmlhttp.open("GET","demo_get2.asp?fname=Bill&lname=Gates",true);
xmlhttp.send();
```

### POST 请求

    使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：
    
```
xmlhttp.open("POST","ajax_test.asp",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Bill&lname=Gates");
```

### 异步请求

    在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：
    
```
xmlhttp.onreadystatechange=function(){
    if (xmlhttp.readyState==4 && xmlhttp.status==200){
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```

## 服务器响应

    获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。
    
<table class="dataintable">
<tbody><tr>
<th style="width:25%;">属性</th>
<th>描述</th>
</tr>

<tr>
<td>responseText</td>
<td>获得字符串形式的响应数据。</td>
</tr>

<tr>
<td>responseXML</td>
<td>获得 XML 形式的响应数据。</td>
</tr>
</tbody></table>

### responseText 属性

    responseText 属性返回字符串形式的响应。
    
```
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```

### responseXML 属性

    来自服务器的响应是 XML，而且需要作为 XML 对象进行解析，请使用 responseXML 属性：
    
```
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++){
  txt=txt + x[i].childNodes[0].nodeValue + "<br/>";
  }
document.getElementById("myDiv").innerHTML=txt;
```

## onreadystatechange 事件

    当请求被发送到服务器时，我们需要执行一些基于响应的任务。
    每当 readyState 改变时，就会触发 onreadystatechange 事件。
    readyState 属性存有 XMLHttpRequest 的状态信息。
    下面是 XMLHttpRequest 对象的三个重要的属性：
    
<table class="dataintable">
<tbody><tr>
<th style="width:25%;">属性</th>
<th>描述</th>
</tr>

<tr>
<td>onreadystatechange</td>
<td>存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。</td>
</tr>

<tr>
<td>readyState</td>
<td>
	<p>存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。</p>
	<ul class="listintable">
	<li>0: 请求未初始化</li>
	<li>1: 服务器连接已建立</li>
	<li>2: 请求已接收</li>
	<li>3: 请求处理中</li>
	<li>4: 请求已完成，且响应已就绪</li>
	</ul>
</td>
</tr>

<tr>
<td>status</td>
<td><p>200: "OK"</p><p>404: 未找到页面</p></td>
</tr>
</tbody></table>

>在 `onreadystatechange` 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

    当 readyState 等于 4 且状态为 200 时，表示响应已就绪：

```
xmlhttp.onreadystatechange=function(){
  if (xmlhttp.readyState==4 && xmlhttp.status==200){
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```

## 完整的例子

```
<script type="text/javascript">
    // 创建ajax对象
    var oAjax = null;
    if (window.XMLHttpRequest) {
        oAjax = new XMLHttpRequest();
    } else {
        oAjax = new ActiveXObject('Microsoft.XMLHTTP');
    }
    // 连接服务器
    
    
    // get---------------------------------------
    oAjax.open('GET', addURLParam('http://106.14.213.216:8080/positions', 'key', 'value'), true);
    // 发送请求
    oAjax.send(null);
    // 如果不需要传送数据，则必须放置null。因为部分浏览器要求必须要加null。
    
    
    // post---------------------------------------
    oAjax.open("POST","ajax_test.asp",true);
    oAjax.setRequestHeader("Content-type","application/x-www-form-urlencoded");
    oAjax.setRequestHeader("token","value");
    oAjax.send("id=001&name=Gates");
    // -------------------------------------------
    
    oAjax.onreadystatechange = function () {
        if (oAjax.readyState == 4) {
            if (oAjax.status >= 200 && oAjax.status < 300 || oAjax.status == 304) {
                console.log(oAjax.responseText);
            } else {
                console.log('error');
            }
        }
    };

    // 通过 GET 方法发送信息，请向 URL 添加信息 但是url加的查询字符串必须使用 encodeURICompent()进行编码才能加入。
    function addURLParam(url, name, value) {
        url += (url.indexOf("?") == -1) ? "?" : "&";
        url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
        return url;
    }
</script>
```