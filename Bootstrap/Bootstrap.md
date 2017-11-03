# Bootstrap

标签： 复习

---

## 简介

        目前最受欢迎的前端框架。Bootstrap 是基于HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。

## 移动优先

> Bootstrap框架包含了贯穿于整个库的移动设备优先的样式。

        为了让Bootstrap开发的网站对移动设备友好，确保适当的绘制和触屏缩放，需要在网页的 head 之中添加 viewport meta 标签，
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

        在移动设备浏览器上，通过为viewportmeta标签添加user-scalable=no 可以禁用其缩放（zooming）功能。通常情况下，maximum-scale=1.0 与 user-scalable=no 一起使用。这样禁用缩放功能后，用户只能滚动屏幕，就能让您的网站看上去更像原生应用的感觉。
   
```
<meta name="viewport" content="width=device-width,initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```

## CSS
        Bootstrap使用了一些HTML5元素和CSS属性。为了让这些正常工作，您需要使用 HTML5 文档类型（Doctype）。 因此，需要在使用 Bootstrap 项目的开头包含下面的代码段。
        
```
<!DOCTYPE html>
<html>
....
</html>
```

### 响应式图像

        通过添加 img-responsive class 可以让 Bootstrap 3 中的图像对响应式布局的支持更友好。可以让图像按比例缩放，不超过其父元素的尺寸。

```
<img src="..." class="img-responsive" alt="响应式图像">
```
> 如果需要让使用了 `.img-responsive` 类的图片水平居中，请使用 `.center-block` 类，不要用 `.text-center`。

### 十二栅格

    移动设备优先策略

* 内容
    * 决定什么是最重要的。
* 布局
    * 优先设计更小的宽度。
    * 基础的 CSS 是移动设备优先，媒体查询是针对于平板电脑、台式电脑。
* 渐进增强
    * 随着屏幕大小的增加而添加元素。
    
### 媒体查询

```
/* 超小设备（手机，小于 768px） */
/* Bootstrap 中默认情况下没有媒体查询 */

/* 小型设备（平板电脑，768px 起） */
@media (min-width: @screen-sm-min) { ... }

/* 中型设备（台式电脑，992px 起） */
@media (min-width: @screen-md-min) { ... }

/* 大型设备（大台式电脑，1200px 起） */
@media (min-width: @screen-lg-min) { ... }
```

> 媒体查询有两个部分，先是一个设备规范，然后是一个大小规则。

```
媒体查询有两个部分，先是一个设备规范，然后是一个大小规则。
```

### 偏移列

    偏移是一个用于更专业的布局的有用功能。它们可用来给列腾出更多的空间。

>  .col-md-offset-* 类。这些类会把一个列的左外边距（margin）增加 * 列，其中 * 范围是从 1 到 11。

```
<div class="col-xs-6 col-md-offset-3" style="background-color:#dedef8;box-shadow: inset 1px -1px 1px #444, inset -1px 1px 1px #444;">
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
</div>
```

### 列排序

        改变带有 .col-md-push-* 和 .col-md-pull-* 类的内置网格列的顺序，其中 * 范围是从 1 到 11。可以互换列的顺序。
    
```
    <p>排序前</p>
    <div class="col-md-4" style="background-color: #dedef8; box-shadow: inset 1px -1px 1px #444, inset -1px 1px 1px #444;">
        我在左边
    </div>
    
    <div class="col-md-8" style="background-color: #dedef8; box-shadow: inset 1px -1px 1px #444, inset -1px 1px 1px #444;">
        我在右边
    </div>
    
    <br>
    
    <p>排序后</p>
    <div class="col-md-4 col-md-push-8" style="background-color: #dedef8; box-shadow: inset 1px -1px 1px #444, inset -1px 1px 1px #444;">
        我在左边
    </div>
    <div class="col-md-8 col-md-pull-4" style="background-color: #dedef8; box-shadow: inset 1px -1px 1px #444, inset -1px 1px 1px #444;">
        我在右边
    </div>
```
    
### button

```
<!-- 标准的按钮 -->
<button type="button" class="btn btn-default">默认按钮</button>
<!-- 提供额外的视觉效果，标识一组按钮中的原始动作 *蓝色* -->
<button type="button" class="btn btn-primary">原始按钮</button>
<!-- 表示一个成功的或积极的动作 *绿色* -->
<button type="button" class="btn btn-success">成功按钮</button>
<!-- 信息警告消息的上下文按钮 *淡蓝色* -->
<button type="button" class="btn btn-info">信息按钮</button>
<!-- 表示应谨慎采取的动作 *黄色* -->
<button type="button" class="btn btn-warning">警告按钮</button>
<!-- 表示一个危险的或潜在的负面动作 *红色* -->
<button type="button" class="btn btn-danger">危险按钮</button>
<!-- 并不强调是一个按钮，看起来像一个链接，但同时保持按钮的行为 -->
<button type="button" class="btn btn-link">链接按钮</button>
```

### Bootstrap 图片

    Bootstrap 提供了三个可对图片应用简单样式的 class：
    
> .img-rounded：添加 border-radius:6px 来获得图片圆角。
.img-circle：添加 border-radius:50% 来让整个图片变成圆形。
.img-thumbnail：添加一些内边距（padding）和一个灰色的边框。

### 显示/隐藏

<table class="reference">
      <thead>
        <tr>
          <th></th>
          <th>
            超小屏幕<br>
            手机 (&lt;768px)
          </th>
          <th>
            小屏幕<br>
            平板 (≥768px)
          </th>
          <th>
            中等屏幕<br>
            桌面 (≥992px)
          </th>
          <th>
            大屏幕<br>
            桌面 (≥1200px)
          </th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>.visible-xs-*</td>
          <td>可见</td>
          <td>隐藏</td>
          <td>隐藏</td>
          <td>隐藏</td>
        </tr>
        <tr>
          <td>.visible-sm-*</td>
          <td>隐藏</td>
          <td>可见</td>
          <td>隐藏</td>
          <td>隐藏</td>
        </tr>
        <tr>
          <td>.visible-md-*</td>
          <td>隐藏</td>
          <td>隐藏</td>
          <td>可见</td>
          <td>隐藏</td>
        </tr>
        <tr>
          <td>.visible-lg-*</td>
          <td>隐藏</td>
          <td>隐藏</td>
          <td>隐藏</td>
          <td>可见</td>
        </tr>
      </tbody>
      <tbody>
        <tr>
          <td>.hidden-xs</td>
          <td>隐藏</td>
          <td>可见</td>
          <td>可见</td>
          <td>可见</td>
        </tr>
        <tr>
          <td>.hidden-sm</td>
          <td>可见</td>
          <td>隐藏</td>
          <td>可见</td>
          <td>可见</td>
        </tr>
        <tr>
          <td>.hidden-md</td>
          <td>可见</td>
          <td>可见</td>
          <td>隐藏</td>
          <td>可见</td>
        </tr>
        <tr>
          <td>.hidden-lg</td>
          <td>可见</td>
          <td>可见</td>
          <td>可见</td>
          <td>隐藏</td>
        </tr>
      </tbody>
    </table>
    
### IE 兼容模式
    
        IE 支持通过特定的 <meta> 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。
        
```
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```