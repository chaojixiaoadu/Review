# Ionic 组件
### 1. 布局
> 12 栅格
```
<ion-grid>
  <ion-row>
    <ion-col col-6>苏州</ion-col>
    <ion-col col-6 style="text-align: right" >...</ion-col>
  </ion-row>
</ion-grid>
```

> **tabs**

* 默认情况下，导航到“选项卡”页面将选择第一个选项卡。可以通过改变所选择的选项卡selectedIndex 上的 `<ion-tabs>` 元素：

```
// 通过 selectedIndex 选择选项卡;

<ion-tabs selectedIndex="2">
  <ion-tab [root]="tab1Root"></ion-tab>
  <ion-tab [root]="tab2Root"></ion-tab>
  <ion-tab [root]="tab3Root"></ion-tab>
</ion-tabs>
```
* 还可以抓取Tabs实例并调用该select() 方法选择选项卡。
```
// 抓取Tabs实例并调用该select() 方法选择选项卡。

<ion-tabs #myTabs>
  <ion-tab [root]="tab1Root"></ion-tab>
  <ion-tab [root]="tab2Root"></ion-tab>
  <ion-tab [root]="tab3Root"></ion-tab>
</ion-tabs>

// 在 ts 中,导入模块

    import { Component,ViewChild } from '@angular/core';
export class TabsPage {

// 创建参数对象  

@ViewChild('myTabs') tabRef: Tabs;

ionViewDidEnter() {
  this.tabRef.select(2); // 默认选项;从0开始。
}

}
```

### 2. 页面跳转

> 使用navCtrl跳转

1.导入页面跳转模块
    
```
import { NavController, NavParams } from 'ionic-angular';
```
    
2.创建跳转对象
    
```
constructor(
  public navCtrl: NavController,
  public navParams: NavParams,
) {
}
```

3.在事件中跳转 + 传参数
    
```
// 跳转
this.navCtrl.push(TabsPage,{userId:'001'});
// 后退
this.navCtrl.pop(Pages);
```
    
4.在目标页中取参数
    
```
//导入模块
import { NavController, NavParams } from 'ionic-angular';
//创建参数对象
private navParma:NavParams

//生命周期函数
ionViewDidEnter() {
this.tabRef.select(0);
let id=this.navParma.get('userId');
console.log(id);
}
```
> 使用viewCtrl

* <font color="#ff0000">注意:</font>
> 关闭的是栈中页面,再次进入需要重新打开;
如果当前栈中只有一个页面则<font color="#ffff00">无法</font>使用。

* 在页面ts中导入模块
```
import { ViewController } from 'ionic-angular';
```
* 创建参数对象
```
constructor(public viewCtrl: ViewController) {}
```
* 使用`dismiss`关闭当前页面
```
this.viewCtrl.dismiss();
```
    
### 3. 图片轮播

*   最好把图片轮播放在页面的头部
    
```
// autoplay 自动切换时间,毫秒;
// loop true||false 是否循环; 
<ion-slides autoplay="2000" loop="true" (ionSlideDidChange)="slideChanged()" #slides>
    <ion-slide *ngFor="let item of imgs" >
        <img src="assets/img/{{item}}" alt="" (click)="showImg(item)">
    </ion-slide>
</ion-slides>
```
    
*    事件

>  获取轮播控件对象
    
```
// 导入模块
    import { Component,ViewChild } from '@angular/core';
// 创建参数对象    
    @ViewChild(Slides) slides: Slides;
```
```
slideChanged(){
    let activeIndex=this.slides.getActiveIndex();
    console.log(activeIndex);
    this.slides.startAutoplay();
}
showImg(img){
    console.log(img);
}
```

### 4.列表（list）
* 无左右滑动
```
<ion-list no-lines>
    <ion-item *ngFor="let item of items" (click)="itemSelected(item)">
      <ion-avatar item-start>
        <img src="{{item?.icon_url}}">
      </ion-avatar>
      <h2>{{item?.post}}</h2>
      <h3>{{item?.salary}}</h3>
      <ion-grid>
        <ion-row>
          <ion-col col-4>苏州</ion-col>
          <ion-col col-4>猎聘</ion-col>
          <ion-col col-4 style="text-align: right" >...</ion-col>
        </ion-row>
      </ion-grid>
    </ion-item>
</ion-list>
```
* 左右滑动
```
<ion-list>
  <ion-item-sliding> // 滑动
  /*=========================================*/
    <ion-item> // 显示列表
      <ion-avatar item-start>
        <img src="img/slimer.png">
      </ion-avatar>
      <h2>Slimer</h2>
    </ion-item>
/*=========================================*/
    <ion-item-options side="left"> // 向右划,左侧显示
      <button ion-button color="primary">
        <ion-icon name="text"></ion-icon> // 图标
        Text
      </button>
      <button ion-button color="secondary">
        <ion-icon name="call"></ion-icon> // 图标
        Call
      </button>
    </ion-item-options>
 /*=========================================*/
    <ion-item-options side="right"> // 向左划,右侧显示 
      <button ion-button color="primary">
        <ion-icon name="mail"></ion-icon> // 图标
        Email
      </button>
    </ion-item-options>
 /*=========================================*/
  </ion-item-sliding>
</ion-list>
```
### 5.弹出提示框

```
// 导入模块
import { AlertController } from 'ionic-angular';
//创建参数对象
constructor(public alertCtrl: AlertController) {}
// 调用函数
showConfirm() {
    let confirm = this.alertCtrl.create({
      title: 'Use this lightsaber?', //标题
      message: 'Do you agree to use this lightsaber to do good across the intergalactic galaxy?',  //内容
      // 按钮
      buttons: [
        {
          text: 'Disagree', // 取消
          handler: () => {
            console.log('Disagree clicked');
          }
        },
        {
          text: 'Agree',  // 确认
          handler: () => {
            console.log('Agree clicked');
          }
        }
      ]
    });
    confirm.present(); // 调用confirm,使提示框出现
}
```
### 6.模态窗口(modal)

> 可以隐藏底部 tabs

```
// 导入模块
import { ModalController } from 'ionic-angular';
// 创建参数对象
export class MyPage {
  constructor(public modalCtrl: ModalController) {
  }
// 函数对象
presentModal() {
    let modal = this.modalCtrl.create(ModalPage);
    modal.present();    //使模态窗口出现
  }
}
```

### 7.下拉刷新

* API:Refresher

```
<!--用法-->
<ion-content>

  <ion-refresher (ionRefresh)="doRefresh($event)">
    <ion-refresher-content></ion-refresher-content>
  </ion-refresher>

</ion-content>

<!--在 ts 中-->
@Component({...})
export class NewsFeedPage {

  doRefresh(refresher) {
    console.log('Begin async operation', refresher);

    setTimeout(() => {
      console.log('Async operation has ended');
      refresher.complete();
    }, 2000);
  }

}
```
* 更改默认图标和微调
```
<ion-content>

  <ion-refresher (ionRefresh)="doRefresh($event)">
    <ion-refresher-content
      pullingIcon="arrow-dropdown" // 下拉图片
      pullingText="释放立即刷新" // 下拉提示文本
      refreshingSpinner="circles" // 加载图片
      refreshingText="正在努力加载中..."> // 加载提示文本
    </ion-refresher-content>
  </ion-refresher>

</ion-content>
```
### 8.下拉加载

* API:InfiniteScroll

```
<!--用法-->
<ion-content>

 <ion-list>
   <ion-item *ngFor="let i of items">{{i}}</ion-item>
 </ion-list>

 <ion-infinite-scroll (ionInfinite)="doInfinite($event)">
   <ion-infinite-scroll-content></ion-infinite-scroll-content>
 </ion-infinite-scroll>

</ion-content>
<!--在 ts 中-->
@Component({...})
export class NewsFeedPage {
  
  constructor() {}

  doInfinite(infiniteScroll) {

    setTimeout(() => {
      for (let i = 0; i < 30; i++) {
        this.items.push( this.items.length ); // 向尾部添加数据 
      }
    
      infiniteScroll.complete();
    }, 500);
  }
}
```
* 如果异步使用 `waitFor` InfiniteScroll的方法

```
<!--用法-->
<ion-content>

 <ion-list>
   <ion-item *ngFor="let item of items"></ion-item>
 </ion-list>

 <ion-infinite-scroll (ionInfinite)="$event.waitFor(doInfinite())">
   <ion-infinite-scroll-content></ion-infinite-scroll-content>
 </ion-infinite-scroll>

</ion-content>
<!--在 ts 中-->
@Component({...})
export class NewsFeedPage {

  constructor() {}

  doInfinite(): Promise<any> {

    return new Promise((resolve) => {
      setTimeout(() => {
        for (var i = 0; i < 30; i++) {
          this.items.push( this.items.length ); // 向末尾push数据
        }

        resolve();
      }, 500);
    })
  }
}
```
* 自定义提示图标文字
```
<ion-content>

  <ion-infinite-scroll (ionInfinite)="doInfinite($event)">
    <ion-infinite-scroll-content
      loadingSpinner="bubbles" // 提示图标
      loadingText="正在努力加载..."> // 提示文本
    </ion-infinite-scroll-content>
  </ion-infinite-scroll>

</ion-content>
```

## 存储（storage）

* 安装

```
$ npm install --save @ionic/storage
```
* 接下来，将它添加到src/app/app.module.ts声明中的导入列表中:

```
// 导入模块
import { IonicStorageModule } from '@ionic/storage';

@NgModule({
  declarations: [
    // ...
  ],
  imports: [      
    BrowserModule,
    IonicModule.forRoot(MyApp),
    IonicStorageModule.forRoot() // 声明IonicStorageModule
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    // ...
  ],
  providers: [
    // ...
  ]
})
export class AppModule {}
```
* 最后，将其注入任何组件或页面：

```
// 导入模块
import { Storage } from '@ionic/storage';

export class MyApp {
// 创建参数对象
  constructor(private storage: Storage) { }

  ...

  // 保存
  storage.set('name', 'Max');

  // 读取（异步处理）
  storage.ready().then(() => {
    storage.get('age').then((val) => {
      console.log('Your age is', val);
    });
  })；
}
```

