# 5.数据绑定，响应式编程和管道

* 数据绑定
* 响应式编程
* 管道

## 数据绑定

### 单向绑定

* 使用插值表达式将一个表达式的值显示在模板上
* 使用方括号将HTML标签的一个属性绑定到一个表达式上
* 使用小括号将组件控制器的一个方法绑定为模板上一个事件的处理器

### 双向绑定变为可选项，而不再是默认行为

## 事件绑定

**事件绑定右侧的表达式可以不是一个函数调用，也可以是一个属性赋值，被绑定的事件既可以是DOM事件，也可以是自定义事件。**

![](../.gitbook/assets/360截图20171022153622894.jpg)

## DOM属性绑定

* 插值表达式和属性绑定一样

![](../.gitbook/assets/360截图20171023092903496.jpg)

渲染之前会把插值表达式编译成属性绑定。

* HTML属性和DOM属性区别

![](../.gitbook/assets/360截图20171023113859568.jpg)

![](../.gitbook/assets/360截图20171023113552840.jpg)

HTML属性指定了初始值，HTML属性初始化DOM属性

DOM属性指定了当前值

DOM属性的值可以改变，HTML属性不能改变

disabled属性的HTML值无关紧要，可以设置DOM的disabled属性

### HTML属性和DOM属性的关系

* 少量HTML属性和DOM属性之间有着1:1的映射，如id。
* 有些HTML属性没有对应的DOM属性，如cosplay。
* 有些DOM属性没有对应的HTML属性，如textHTML。
* 就算名字相同，HTML属性和DOM属性也不是一样东西。
* HTML属性的值指定了初始值；DOM属性的值表示当前值。 DOM属性的值可以改变；HTML属性的值不能改变。
* 模板绑定是通过DOM属性和事件来工作的，而不是HTML属性。

![](../.gitbook/assets/360截图20171023130322503.jpg)

## HTML属性绑定

* 基本HTML属性绑定

`<td [attr.colspan]="tableColspan">Something</td>`

* CSS类绑定
  1. 全有或全无`<div class="aaa" [class]="someExpression">something</div>`替换原来class的值
  2. 样式名和布尔值`<div class="a b" [class.c]="bool">something</div>`
  3. 控制多个CSS类是否显示`<div ngClass="{aaa:isA,bbb:isB}"></div>`

![](../.gitbook/assets/360截图20171023133852147.jpg)

![](../.gitbook/assets/360截图20171023133957236.jpg)

* 样式绑定

![](../.gitbook/assets/360截图20171106102901439.jpg)

`<button [style.color]="isDev?'red':'green'">Red</button>`

![](../.gitbook/assets/360截图20171023134313521.jpg)

`<div [ngStyle]="{'font-style':this.canSAve?'itlaic':'normal'}"></div>`

![](../.gitbook/assets/360截图20171023134606556.jpg)

![](../.gitbook/assets/360截图20171023134752280.jpg)

![](../.gitbook/assets/360截图20171023132451898.jpg)

## 双向绑定

* 单向的数据绑定有：

事件：模板到控制器

属性绑定：从控制器到模板

* 双向绑定

![](../.gitbook/assets/360截图20171023135254954.jpg)

![](../.gitbook/assets/360截图20171023135759053.jpg)

\[\(ngModel\)\]来简化这种写法

![](../.gitbook/assets/360截图20171023140006980.jpg)

常用于表单的处理

注意：要用于特定的表单元素上，文本框，选择框等，用在div,span上是没用的

## 响应式编程

在计算领域，响应式编程一种面向数据流和变化传播的编程范式。这意味着可以在编程语言中很方便地表达静态或动态的数据流，而相关的计算模型会自动将变化的值通过数据流进行传播。

![](../.gitbook/assets/360截图20171023172745353.jpg)

如果观察的足够仔细的话，你会发现console中输出的值其实是 input.target.value，我们观察的对象其实是id为todo的这个对象上发生的keyup事件（Rx.Observable.fromEvent\(todo, 'keyup'\)）。那么其实在订阅的代码段中的input其实是keyup事件才对。好，我们看看到底是什么，将 console.log\(input.target.value\) 改写成 console.log\(input\)，看看会怎样呢？是的，我们得到的确实是KeyboardEvent

![](../.gitbook/assets/360截图20171023173434169.jpg)

这是要过滤出 keyCode=32 的事件，keyCode是Ascii码，那么这就是要把空格滤出来

![](../.gitbook/assets/360截图20171023173443583.jpg)

map这个操作符做的事情就是允许你对原数据流中的每一个元素应用一个函数，然后返回并形成一个新的数据流，这个数据流中的每一个元素都是原来的数据流中的元素应用函数后的值。

类似 .map\(ev=&gt;ev.target.value\) 的场景太多了，以至于rxjs团队搞出来一个专门的操作符来应对，这个操作符就是 pluck。这个操作符专业从事从一系列嵌套的属性种把值提取出来形成新的流。比如上面的例子可以改写成下面的代码，效果是一样的。那么如果其中某个属性为空怎么办？这个操作符负责返回一个 undefined 作为值加入流中。

在Javascript中我们同样方法得到按钮的DOM对象以及声明对此按钮点击事件的观察者：

![](../.gitbook/assets/360截图20171023173919575.jpg)

由于点击事件没有什么可见的值，所以我们利用一个操作符叫 mapTo 把对应的每次点击转换成字符 clicked。其实它也是一个 map 的简化操作。

* combineLatest操作符

![](../.gitbook/assets/360截图20171023174514789.jpg)

combineLatest 操作符其实是在组合2个源数据流中选择最新的2个数据进行配对，如果其中一个源之前没有任何数据产生，那么结果流也不会产生数据。

* zip操作符

zip 和 combineLatest 非常像，但重要的区别点在于 zip 严格的需要多个源数据流中的每一个的相同顺序的元素配对。

zip 要求源1的第一个数据和源2的第一个数据组成一对，产生结果流的第一个数据；源1的第二个数据和源2的第二个数据组成一对，产生结果流的第二个数据。而 combineLatest 不需要等待另一个源数据流产生数据，只要有一个产生，结果流就会产生。

zip 这个词在英文中有拉链的意思，记住这个有助于我们理解这个操作符，就像拉链一样，它需要拉链两边的齿一一对应。从效果角度上讲，这个操作符有减缓发射速度的作用，因为它会等待合并序列中最慢的那个。

![](../.gitbook/assets/360截图20171023175622529.jpg)

创建类操作符:通常来讲，Rx团队不鼓励新手自己从0开始创建Observable，因为状态太复杂，会遗漏一些问题。Rx鼓励的是通过已有的大量创建类转换操作符来去建立Observable。我们其实之前已经见过一些了，包括 from 和 fromEvent。

from操作符:from 可以支持从数组、类似数组的对象、Promise、iterable 对象或类似Observable的对象（其实这个主要指ES2015中的Observable）来创建一个Observable。这个操作符应该是可以创建Observable的操作符中最常使用的一个，因为它几乎可以把任何对象转换成Observable。

fromEvent操作符:这个操作符是专门为事件转换成Observable而制作的，非常强大且方便。对于前端来说，这个方法用于处理各种DOM中的事件再方便不过了。

![](../.gitbook/assets/360截图20171024021446674.jpg)

### 观察者模式与Rxjs

![](../.gitbook/assets/360截图20171024022512062.jpg)

异步数据流编程

![](../.gitbook/assets/360截图20171024023510405.jpg)

rxjs:javascript响应式编程包

#### 模板本地变量

![](../.gitbook/assets/360截图20171024024021600.jpg)

#### ReactiveFormsModule模块

做响应式编程的一个模块，它的对象FormControl

![](../.gitbook/assets/360截图20171024102134987.jpg)

## 管道

![](../.gitbook/assets/360截图20171023144753609.jpg)

整数位.小数位最少-小数位最多

async异步管道

### 自定义管道

ng g pipe pipe/multiple

![](../.gitbook/assets/360截图20171023145721814.jpg)

![](../.gitbook/assets/360截图20171023145545899.jpg)

