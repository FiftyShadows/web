# 1.逻辑梳理与API初探

## 模块分解-game.js

* 游戏全局的入口文件，是微信小游戏必须有的一个文件

## 模块分解-Main.js

* 程序主类，主要用来初始化canvas和一些全局对象，各个精灵和绑定点击事件

## 模块分解-Direactor.js

* 程序导演类，用来控制游戏的逻辑和精灵的创建与销毁，控制游戏主循环

## 模块分解-DataStore.js

* 存储游戏需要长期保存的变量和需要定时销毁的变量

## 模块分解-Resource.js

* 游戏的资源

## 模块分解-ResourceLoader.js

* 资源加载器，保证游戏是在图片加载完成后开始主循环

## 模块分解-Sprite.js

* 游戏精灵的基类，背景，陆地，铅笔，小鸟等都是它的子类

## Background.js

* 背景类

## Land.js

* 陆地类

## UpPencil.js

* 上半部分铅笔类

## DomnPencil.js

## Birds.js

## Score.js

## StartButton.js

## 使用es6在浏览器里执行

1. 要在script标签上加type='module'
2. import引入文件要加后缀名

## 工厂方法？

## 单例模式

* 基于es6实现单例模式

```text
export class Director{
    constructor(){
        console.info('构造器初始化');
    }
    static getInstance(){
        if(!Director.instance){
            Director.instance = new Director;
        }
        return Director.instance;
    }
}
```

## drawImage

* 要在图片onLoad之后才能在canvas绘制

this.ctx.drawImage = {  
image对象，  
image的x起始位置，  
image的y起始位置，  
image.width,  
image.height,  
放置在画布的位置0,  
0，  
image.width, //使用图片的大小 image.height  
};

## 精灵基类，负责初始化精灵加载的资源和大小以及位置

