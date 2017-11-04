# Node.js(EventEmitter)

标签： 复习

---

## 简介

    EventEmitter 的核心就是事件触发与事件监听器功能的封装。

* 实例

```
//event.js 文件
var EventEmitter = require('events').EventEmitter; 
var event = new EventEmitter(); 
event.on('some_event', function() { 
    console.log('some_event 事件触发'); 
}); 
setTimeout(function() { 
    event.emit('some_event'); 
}, 1000); 
```

    EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件，EventEmitter 支持 若干个事件监听器。
    当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。
    
```
//event.js 文件
var events = require('events'); 
var emitter = new events.EventEmitter(); 
emitter.on('someEvent', function(arg1, arg2) { 
    console.log('listener1', arg1, arg2); 
}); 
emitter.on('someEvent', function(arg1, arg2) { 
    console.log('listener2', arg1, arg2); 
}); 
emitter.emit('someEvent', 'arg1 参数', 'arg2 参数'); 
```

> `emitter` 为事件 `someEvent` 注册了两个事件监听器，然后触发了 `someEvent` 事件。
运行结果中可以看到两个事件监听器回调函数被先后调用。 这就是`EventEmitter`最简单的用法。
`EventEmitter` 提供了多个属性，如 `on` 和 `emit`。`on` 函数用于绑定事件函数，`emit` 属性用于触发一个事件。

* 运行结果

```
$ node event.js 
listener1 arg1 参数 arg2 参数
listener2 arg1 参数 arg2 参数
```

<table class="reference">
<tbody><tr><th>序号</th><th>方法 &amp; 描述</th></tr>
<tr><td>1</td><td><b>addListener(event, listener)</b><br>
为指定事件添加一个监听器到监听器数组的尾部。</td></tr>
<tr><td>2</td><td><b>on(event, listener)</b><br>为指定事件注册一个监听器，接受一个字符串 event 和一个回调函数。
<pre class="prettyprint prettyprinted" style=""><span class="pln">server</span><span class="pun">.</span><span class="pln">on</span><span class="pun">(</span><span class="str">'connection'</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">function</span><span class="pln"> </span><span class="pun">(</span><span class="pln">stream</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
  console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'someone connected!'</span><span class="pun">);</span><span class="pln">
</span><span class="pun">});</span></pre>

</td></tr>
<tr><td>3</td><td><b>once(event, listener)</b><br>为指定事件注册一个单次监听器，即 监听器最多只会触发一次，触发后立刻解除该监听器。
<pre class="prettyprint prettyprinted" style=""><span class="pln">server</span><span class="pun">.</span><span class="pln">once</span><span class="pun">(</span><span class="str">'connection'</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">function</span><span class="pln"> </span><span class="pun">(</span><span class="pln">stream</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
  console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'Ah, we have our first user!'</span><span class="pun">);</span><span class="pln">
</span><span class="pun">});</span></pre>

</td></tr>
<tr><td>4</td><td><b>removeListener(event, listener)</b><br><p>移除指定事件的某个监听器，监听器必须是该事件已经注册过的监听器。</p><p>它接受两个参数，第一个是事件名称，第二个是回调函数名称。</p>
<pre class="prettyprint prettyprinted" style=""><span class="kwd">var</span><span class="pln"> callback </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">function</span><span class="pun">(</span><span class="pln">stream</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
  console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'someone connected!'</span><span class="pun">);</span><span class="pln">
</span><span class="pun">};</span><span class="pln">
server</span><span class="pun">.</span><span class="pln">on</span><span class="pun">(</span><span class="str">'connection'</span><span class="pun">,</span><span class="pln"> callback</span><span class="pun">);</span><span class="pln">
</span><span class="com">// ...</span><span class="pln">
server</span><span class="pun">.</span><span class="pln">removeListener</span><span class="pun">(</span><span class="str">'connection'</span><span class="pun">,</span><span class="pln"> callback</span><span class="pun">);</span></pre>

</td></tr>
<tr><td>5</td><td><b>removeAllListeners([event])</b><br>移除所有事件的所有监听器， 如果指定事件，则移除指定事件的所有监听器。</td></tr>
<tr><td>6</td><td><b>setMaxListeners(n)</b><br>默认情况下， EventEmitters 如果你添加的监听器超过 10 个就会输出警告信息。
setMaxListeners 函数用于提高监听器的默认限制的数量。</td></tr>
<tr><td>7</td><td><b>listeners(event)</b><br>返回指定事件的监听器数组。</td></tr>
<tr><td>8</td><td><b>emit(event, [arg1], [arg2], [...])</b><br>按参数的顺序执行每个监听器，如果事件有注册监听返回 true，否则返回 false。</td></tr>
</tbody></table>


