# JavaScript

标签： 模拟面试

---

## 1、	介绍一下JS的基本数据类型？

* Undefined
* Null
* Boolean
* Number
* String

## 2、	谈谈对this的理解。

* this总是指向函数的直接调用者（而非间接调用者）；
* 如果有new关键字，this指向new出来的那个对象；
* 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象Window；

## 3、	如何判断一个对象是否属于某个类？

* typeof

> 返回有function、undefined、Number、object、string、boolean
    
```
typeof(function(){});   //返回function
typeof(undefined);      //返回undefined
typeof(NaN)、typeof(1); //返回Number
typeof(null)、typeof(object)、typeof([]);    //返回object
```

* constructor

```
var  a=New Function(){};
console.log(a.constructor())//function anonymous(){};
```

* instanceof

```
var arr=[];
console.log(arr instanceof Array)// true;
```

* Object.prototype.toString.call()

```
var a=[];
console.log(Object.prototype.toString.call(a));//[object Array]
```

## 4、	什么是闭包？为什么要用它？

    闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。

* 闭包的特性：
    1.函数内再嵌套函数
    2.内部函数可以引用外层的参数和变量
    3.参数和变量不会被垃圾回收机制回收

> //li节点的onclick事件都能正确的弹出当前被点击的li索引

```
 <ul id="testUL">
    <li> index = 0</li>
    <li> index = 1</li>
    <li> index = 2</li>
    <li> index = 3</li>
</ul>
<script type="text/javascript">
    var nodes = document.getElementsByTagName("li");
    for(i = 0;i<nodes.length;i+= 1){
        nodes[i].onclick = function(){
            console.log(i+1);//不用闭包的话，值每次都是4
        }(i);
    }
</script>
```

> 执行say667()后,say667()闭包内部变量会存在,而闭包内部函数的内部变量不会存在使得Javascript的垃圾回收机制GC不会收回say667()所占用的资源因为say667()的内部函数的执行需要依赖say667()中的变量这是对闭包作用的非常直白的描述。

```
 function say667() {
   // Local variable that ends up within closure
   var num = 666;
   var sayAlert = function() {
       alert(num);
   }
   num++;
   return sayAlert;
}

 var sayAlert = say667();
 sayAlert()//执行结果应该弹出的667
```

## 5、	Js代码开头的use strict是什么意思？

    use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。

* 默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
* 全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
* 消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;

* 提高编译器效率，增加运行速度；
* 为未来新版本的Javascript标准化做铺垫。

## 6、	Ajax有哪些方法？

* open(method, url, async) 方法需要三个参数;
* send() 方法可将请求送往服务器。
* onreadystatechange：存有处理服务器响应的函数，每当 readyState 改变时，onreadystatechange 函数就会被执行。
* readyState：存有服务器响应的状态信息。
    * 0: 请求未初始化
    * 1: 服务器连接已建立
    * 2: 请求已接收
    * 3: 请求处理中
    * 4: 请求已完成，且响应已就绪
    
* responseText：获得字符串形式的响应数据。
* setRequestHeader()：POST传数据时，用来添加 HTTP 头，然后send(data)，注意data格式；GET发送信息时直接加参数到url上就可以，比如url?a=a1&b=b1。

## 7、	如何实现继承？

    1. 构造继承
    2. 原型继承
    3. 实例继承
    4. 拷贝继承

* 原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。

```
function Parent(){
    this.name = 'wang';
}

function Child(){
    this.age = 28;
}
Child.prototype = new Parent();//继承了Parent，通过原型

var demo = new Child();
alert(demo.age);
alert(demo.name);//得到被继承的属性
```

## 8、	解释一下==和===的区别？

> `==` 表示值相等，不比较类型。`===` 不仅要值相等，类型也要相等。

## 9、	什么是事件冒泡？如何阻止？

    事件的传播是有方向的，当点击一个按钮时所产生的事件从这个按钮处开始向上传播。
    
* 阻止冒泡
```
event.stopPropagation();
```

## 10、	JS中定义对象的方法有哪些？

* 使用内置对象
```
var str = new String("实例初始化String");
```
* 使用JSON符号
```
{name:"刘德华",age:"25",sex:"男"}
```
* 自定义对象构造
```
function Girl() { 
    this.name = "big pig"; 
    this.age = 20; 
    this.standing;  
    this.bust; 
    this.waist; 
    this.hip; 
}
```

## 11、 事件绑定有哪些方法？
* 在DOM元素中直接绑定
```
<input onclick="alert('谢谢支持')" type="button" value="点击我，弹出警告框" />
```
* 在JavaScript代码中绑定事件
```
<input  id="demo"  type="button"  value="点击我，显示 type 属性" />  
<script type="text/javascript">  
    document.getElementById("demo").onclick=function(){  
        alert(this.getAttribute("type"));  //  this 指当前发生事件的HTML元素，这里是<div>标签  
    }  
</script>
```
* 绑定事件监听函数
```
elementObject.addEventListener(eventName,handle,useCapture);//使用addEventListener（IE8.0及其以下版本不支持）
elementObject.attachEvent(eventName,handle);//使用attachEvent（IE8.0及其以下版本使用）
```

## 12、	怎样得到一个节点的值？

    使用document对象获取

```
document.getElementById('id').nodeType;
```

## 13、	如何消除数组中的重复元素?

* 方法一:用到了数组的indexOf()方法，此方法主要用来查找元素在数组中第一次出现的位置。比较浪费资源和时间。
```
Array.prototype.method1 = function(){  
    var arr[];    //定义一个临时数组  
    for(var i = 0; i < this.length; i++){    //循环遍历当前数组  
        //判断当前数组下标为i的元素是否已经保存到临时数组  
        //如果已保存，则跳过，否则将此元素保存到临时数组中  
        if(arr1.indexOf(this[i]) == -1){  
            arr.push(this[i]);  
        }  
    }  
    return arr;  
}
```
* 方法二:使用hash表，把已经出现过的元素通过下标形式写入到一个object内，下标的引用要比用数组indexOf()方法搜索节省时间。
```
Array.prototype.method2 = function(){  
    var h{};    //定义一个hash表  
    var arr[];  //定义一个临时数组            
    for(var i = 0; i < this.length; i++){    //循环遍历当前数组  
        //对元素进行判断，看是否已经存在表中，如果存在则跳过，否则存入临时数组  
        if(!h[this[i]]){  
            //存入hash表  
            h[this[i]] = true;  
            //把当前数组元素存入到临时数组中  
            arr.push(this[i]);  
        }  
    }  
    return arr;  
}
```
* 方法三：用到了数组的indexOf()方法，此方法主要用来查找元素在数组中第一次出现的位置。比较浪费资源和时间。
```
Array.prototype.method3 = function(){  
    //直接定义结果数组  
    var arr[this[0]];  
    for(var i = 1; i < this.length; i++){    //从数组第二项开始循环遍历此数组  
        //对元素进行判断：  
        //如果数组当前元素在此数组中第一次出现的位置不是i  
        //那么我们可以判断第i项元素是重复的，否则直接存入结果数组  
        if(this.indexOf(this[i]) == i){  
            arr.push(this[i]);  
        }  
    }  
    return arr;    
}
```
* 方法四：先将数组排序，然后一次比较相邻的两个元素的值，排序使用的是js原生的sort()方法。
```
Array.prototype.method4 = function(){  
    //将数组进行排序  
    this.sort();  
    //定义结果数组  
    var arr[this[0]];  
    for(var i = 1; i < this.length; i++){    //从数组第二项开始循环遍历数组  
        //判断相邻两个元素是否相等，如果相等说明数据重复，否则将元素写入结果数组  
        if(this[i] !== arr[arr.length - 1]){  
            arr.push(this[i]);  
        }              
    }  
    return arr;            
}
```

## 14、	如何统计字符串中某个字符的个数？

* 使用正则
```
<script>
function getCount(str1,str2)
{
    var r=new RegExp('\\'+str2,"gi");//注意字符串中需要转义的字符
    return str1.match(r).length;
}
alert(getCount("AB/C/C/B/AA.ABB","/"));
</script>
```
* 循环匹配
```
<script>
    function getlen(str,ch){
        var ret=0;
        for(var i=0;i<str.length;i++){
            if(str.charAt(i)==ch)	  ret++;
        }
        return ret;
    }
    alert(getlen('abcdab','a'));
</script>
```
## 15、	伪数组如何转换成标准数组？

* 使用Array.prototype.slice.call()或[].slice.call()
```
Array.prototype.slice.call({  
    0:"hello",  
    1:12,  
    2:true,  
    length:3  
});  
//["hello", 12, true]
```
* 使用ES6中Array.from方法
```
Array.from({  
    0:"hello",  
    1:12,  
    2:2013,  
    3:"大学",  
    length:4  
});  
//["hello", 12, 2013, "大学"]
```

## 16、	快速排序如何实现？
```
var quickSort = function(arr) {
    if (arr.length <= 1) { return arr; }
    var pivotIndex = Math.floor(arr.length / 2) ;
    var pivot = arr.splice(pivotIndex, 1)[0];
    var left = [];//用来存放一左一右的两个子集。
    var right = [];
    for(let i =0;i<arr.length;i++){
        if(arr[i]<pivot){
            left.push(arr[i]);
        }else{
            right.push(arr[i])
        }
    }
    return quickSort(left).concat([pivot], quickSort(right));
};
```

## 17、	谈一下JS的作用域链，和原型链？

* 作用域链

        全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。
        当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，直至全局函数，这种组织形式就是作用域链。
        
* 原型链

        每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。

> 关系：instance.constructor.prototype = instance.__proto__

    特点：
    JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。


当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
 
```
function Func(){}
Func.prototype.name = "Sean";
Func.prototype.getInfo = function() {
  return this.name;
}
var person = new Func();//现在可以参考var person = Object.create(oldObject);
console.log(person.getInfo());//它拥有了Func的属性和方法
//"Sean"
console.log(Func.prototype);
// Func { name="Sean", getInfo=function()}
```

## 18、	怎样给一个对象添加属性和方法？

    1. 在定义对象时，直接把属性和方法添加; 
    2. 通过原型prototype模式给对象添加属性和方法;
    
## 19、	如何删除、添加和查找节点？

```
removeChild()//删除节点
appendChild()//添加节点
insertBefore()//在。。前插入节点
insertAfter()//在。。后插入节点
```

## 20、	JS跨域访问的方法有哪些？

* 通过jsonp跨域

        在js中，我们直接用XMLHttpRequest请求不同域上的数据时，是不可以的。但是，在页面上引入不同域上的js脚本文件却是可以的，jsonp正是利用这个特性来实现的。
        
* 在nodejs中使用中间件`Access-Control-Allow-Origin`来设置允许访问的域。

## 21、	我们给一个DOM同时绑定两个点击事件，一个用捕获一个用冒泡会执行几次事件会先执行哪种？

        绑定在被点击元素的事件是按照代码顺序发生，其他元素通过冒泡或者捕获“感知”的事件，按照W3C的标准，先发生捕获事件，后发生冒泡事件。
        所有事件的顺序是：其他元素捕获阶段事件 -> 本元素代码顺序事件 -> 其他元素冒泡阶段事件 。
    
## 22、	简述同步和异步的区别？

        同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程将会一直等待下去，直到收到返回信息才继续执行下去；
        异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程进行处理，这样可以提高执行的效率。
        
## 23、	一次完整的HTTP事务是怎样的过程？

    域名解析 --> 发起TCP的3次握手 --> 建立TCP连接后发起http请求 --> 服务器响应http请求，浏览器得到html代码 --> 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等） --> 浏览器对页面进行渲染呈现给用户
    
## 24、	jQuery中的bind，live，delegate和on方法的区别是什么？

    jQuery中提供了四种事件监听方式，分别是bind、live、delegate、on，对应的解除监听的函数分别是unbind、die、undelegate、off。
    
* 区别

        1. bind() 方法为被选元素添加一个或多个事件处理程序，并规定事件发生时运行的函数;
        
        2.on() 方法事件处理程序到当前选定的jQuery对象中的元素;
        
        3.delegate() 方法为指定的元素（属于被选元素的子元素）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数;
        
        4.live() 方法为被选元素附加一个或多个事件处理程序，并规定当这些事件发生时运行的函数;
        
## 25、	jQuery一个对象可以同时绑定多个事件，这是如何实现的？

```
$("#id").click(func1).mouseover(func2)//方法连写，func为方法的名字

$("#id").click(function(){//你的具体方法实现}),mouser(function(){//你的具体方法实现});

$("#id").on("click mouseover",func)//两个事件中间有空格 ，func为方法的名字

$("#id").bind("load scroll",function(){//你的具体方法实现});
```