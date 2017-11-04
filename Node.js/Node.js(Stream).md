# Node.js(Stream)

标签： 复习

---

* Node.js，Stream 有四种流类型：
    * Readable - 可读操作。
    * Writable - 可写操作。
    * Duplex - 可读可写操作.
    * Transform - 操作被写入数据，然后读出结果。
* 所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：
    * data - 当有数据可读时触发。
    * end - 没有更多的数据可读时触发。
    * error - 在接收和写入过程中发生错误时触发。
    * finish - 所有数据已被写入到底层系统时触发。

> 输入流,输出流,管道流,链式流

* 写入

```
var fs = require("fs");
var data = '菜鸟教程官网地址：www.runoob.com';

// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');

// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');

// 标记文件末尾
writerStream.end();

// 处理流事件 --> data, end, and error
writerStream.on('finish', function() {
    console.log("写入完成。");
});

writerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

* 读取

```
var fs = require("fs");

// 创建一个可读流
var readerStream = fs.createReadStream('input.txt');

// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt');

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream);

console.log("程序执行完毕");
```


