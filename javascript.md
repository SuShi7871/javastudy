# javaScript

## 基础语法

```javascript
prompt() //显示一个对话框,对话框中包含一条文字信息,用来提示用户输入文字
```

**let和var区别:**let为了解决var 的一些问题

- var 声明:可以先使用在声明(不合理)
- var声明过的变量可以重复声明(不合理)
- 比如变量提升.全局变量.没有块级作用域等等

注意:**let变量不允许多次声明同一个变量**

### 模板字符串

模板字符串:拼接字符串和变量,在没有它之前,要拼接变量比较麻烦
语法:${}

```javascript
var name="张三";
document.write(`name:${name}`)
```

注意:**包裹的必须是``**

类型转换

-  显示转换：隐式转换不严谨,而且隐式转换规律并不清晰,大多是靠经验总结的规律。

  1. Number(数据)   转成数字类型
     ​如果字符串里有非数字,转换失败时结果为 NaN(Not a Number)即不是一个数字,NaN也是number类型的数据,代表非数字

  2. parseInt(数据)：只保留整数

  3. parseFloat(数据)：可以保留小数

  4. String(数据):转换为字符型:

     ****

### 操作数组

操作数组:

- push():数组.push()方法将一个或多个元素添加到数组的末尾,并返回该数组的新长度。

- unshift():arr.unshift(新增的内容) 方法将一个或多个元素添加到数组的开头,并返回该数组的新长度
- pop():数组.pop()方法从数组中删除最后一个元素,并返回该元素的值
- shift():数组.shift()方法从数组中删除第一个元素,并返回该元素的值
- splice():数组.splice()方法删除指定元素

- splice(start,count); //start 删除的起始位置,count删除的个数

### 函数

1. 用return返回数据
   ​		return会立即结束当前函数
   ​		函数可以没有return,这种情况函数默认返回值为undefined
2. 作用域:全局作用域.局部作用域.块级作用域;
   ​		局部作用域:作用于函数内的代码环境;
   ​		块作用域由 {} 包括,if语句和for语句里面的{}等;
   ​		根据作用域不同,变量分为：全局变量、局部变量、块级变量
3. 注意:局部变量或者块级变量没有let声明直接赋值的当全局变量看,这种很不提倡
4. 在不同作用域下,可能存在变量命名冲突的情况,采取就近原则的方式来查找变量最终的值,作用域链；

```javascript		
	let num = 10
	function fn() {
		console.log(num)
	}
	fn();  //此处fn的值为20,遵循就近原则
```
匿名函数
​	将匿名函数赋值给一个变量,并且通过变量名称进行调用

```javascript
let fun=function(){
	alert('这就是匿名函数');
}
```

立即执行函数
​	场景介绍: 避免全局变量之间的污染

```javascript
(function () { console.log(111) })();
(function () { console.log(222) })();
```

**注意:多个立即执行函数要用;隔开,要不然会报错**

### 	对象

类比于java中的对象,写法类似与json格式

```javascript
let 对象名={}
```

对象本质是无序的数据集合, 操作数据无非就是增、删、改、查语法:
​	删除对象中的属性:
​		delete 对象.属性
​	遍历对象
​		for k in obj
 		获得对象属性是 k
​		获得对象值是 obj[k]，例如：

```javascript
let obj = {
	uname: '小明',
	age: 18,
	sex: '男'
}
for (const key in obj) {
	console.log(key);//获取属性名
	console.log(obj[key]);//获取属性值
}
```
​	内置对象:即javascript内部提供的对象,包含各种属性和方法给开发者调用；
​	Math对象:

```javascript
生成N-M之间的随机数:Math.floor(Math.random() * (M - N + 1)) + N
```

## web API
### 变量申明

变量声明有三个 var let 和 const

- var老派写法,问题很多,可以淘汰掉，建议const优先,尽量使用const
- const语义化更好,很多变量我们声明的时候就知道他不会被更改了
- 如果变量后期需要修改可以使用let
- 使用建议:
  ​	建议数组和对象使用const来声明
  ​	基本数据类型的值或者引用类型的地址发生变化的时候,需要用let

### webAPI

Web API:就是使用js去操作浏览器和html,分为:文档对象模型 (DOM)、浏览器对象模型(BOM）
DOM树：将HTML文档以树状结构直观的表现出来,我们称之为文档树或DOM 

![1722139895572](.\typora-user-images\1722139895572.png)

- 作用:文档树直观的体现了标签与标签之间的关系

- DOM的核心思想：把网页内容当做对象来处理

document对象

​		是DOM里提供的一个对象，它提供的属性和方法都是用来访问和操作网页内容的

#### 获取DOM元素

网页所有内容都在document里面，根据CSS选择器来获取DOM元素

选择匹配的第一个元素:

```javascript
document.querySelector('css选择器');
 // 获取匹配的第一个元素
const box = document.querySelector('.box')
```

选择匹配的多个元素

```javascript
document.querySelectorAll('css选择器');
// 获取多个元素
const lis = document.querySelectorAll('ul li')
```

根据CSS选择器来获取DOM元素

querySelectAll()获取过来的也是一个伪数组,获取其中的元素需要遍历即可，哪怕只有一个元素，通过querySelectAll() 获取过来的也是一个伪数组，里面只有一个元素而已

```javascript
const lis = document.querySelectorAll('.nav li')
// console.log(lis)
for (let i = 0; i < lis.length; i++) {
    console.log(lis[i]) // 每一个小li对象
}
```

#### 	操作元素内容

对象.innerText 属性

```javascript
//例:document.write()
const li = document.querySelector('li');
li.innerText = '<b>aaa</b>';//innerText不能解析标签,只是在对应的地方显示文本		
```

对象.innerHTML 属性

```javascript
const ps = document.querySelector('p');
ps.innerHTML=`<b>你好</b>`;		//innnerHTML可以解析标签
```

区别:

- 元素.innerText属性只识别文本,不能解析标签
- 元素.innerHTML属性能识别文本,能够解析标签
- 如果还在纠结到底用谁,你可以选择innerHTML

#### 操作元素属性

##### 	操作元素常用属性	

​		可以通过JS设置修改标签元素
​		语法:
​			对象.属性名=属性值;

```js
<img src="./images/1.webp" alt="">
<script>
    // 1. 获取图片元素
    const img = document.querySelector('img')
    // 2. 修改图片对象的属性   对象.属性 = 值
    img.src = './images/2.webp'
    img.title = 'pink老师的艺术照'
</script>
```

##### 	操作元素样式属性

​	通过style属性操作CSS

```javascript
<script>
    // 1. 获取元素
    const box = document.querySelector('.box')
    //2. 修改样式属性 对象.style.样式属性 = '值'  别忘了跟单位
    box.style.width = '300px'
    // 多组单词的采取 小驼峰命名法
    box.style.backgroundColor = 'hotpink'
    box.style.border = '2px solid blue'
    box.style.borderTop = '2px solid red'
</script>
```

##### 	操作类名

可以通过操作类名的方式操作属性
​语法:
​元素.className='类名'
​使用类名的特点:可以同时修改多个样式,直接使用className赋值会覆盖以前的类名;

```html
 <style>
    div {
      width: 200px;
      height: 200px;
      background-color: pink;
    }

    .nav {
      color: red;
    }

    .box {
      width: 300px;
      height: 300px;
      background-color: skyblue;
      margin: 100px auto;
      padding: 10px;
      border: 1px solid #000;
    }
  </style>
<div class="nav">123</div>
  <script>
    // 1. 获取元素
    const div = document.querySelector('div')
    // 2.添加类名  class 是个关键字 我们用 className
    div.className = 'nav box'
  </script>
```

##### 	classList 操作

​		这个主要是为了解决className赋值覆盖的问题
​		语法:
​			元素.classList.add('类名'); //追加一个类名
​			元素.classList.remove('类名');//删除一个类名
​			元素.classList.toggle('类名');//切换一个类名

```html
<style>
    .box {
      width: 200px;
      height: 200px;
      color: #333;
    }

    .active {
      color: red;
      background-color: pink;
    }
</style>
<div class="box active">文字</div>
  <script>
    // 通过classList添加
    // 1. 获取元素
    const box = document.querySelector('.box')
    // 2. 修改样式
    // 2.1 追加类 add() 类名不加点，并且是字符串
    // box.classList.add('active')
    // 2.2 删除类  remove() 类名不加点，并且是字符串
    // box.classList.remove('box')
    // 2.3 切换类  toggle()  有还是没有啊， 有就删掉，没有就加上
    box.classList.toggle('active')
  </script>
```

##### 	操作表单元素属性

​		表单属性中添加就有效果,移除就没有效果,一律使用布尔值表示 
​		如果为true代表添加了该属性如果是false代表移除了该属性
​		比如:disabled.checked.selected

```html
<!-- <input type="text" value="电脑"> -->
  <input type="checkbox" name="" id="">
  <button>点击</button>
  <script>
    // 1 获取元素
    const uname = document.querySelector('input')
    // 2. 获取值  获取表单里面的值 用的  表单.value
    console.log(uname.value) // 电脑
    console.log(uname.innerHTML)  innertHTML 得不到表单的内容
    // 3. 设置表单的值
    uname.value = '我要买电脑'
    console.log(uname.type)
    uname.type = 'password'

    // 1. 获取
    const ipt = document.querySelector('input')
    // console.log(ipt.checked)  // false   只接受布尔值
    ipt.checked = true
    // ipt.checked = 'true'  // 会选中，不提倡  有隐式转换

    // 1.获取
    const button = document.querySelector('button')
    // console.log(button.disabled)  // 默认false 不禁用
    button.disabled = true   // 禁用按钮

  </script>
```

##### 	自定义属性

​		html5推出来了专门的data-自定义属性
​		在标签上一律以data-开头
​		获取的时候一律用dataset获取

```javascript
<div class="box" data-id="10">黑子</div>
const box=document.querySelector('.box');
console.log(box.dataset.id)
```

#### 	定时器-间歇函数

​		开启定时器
​			setInterVal(函数,间隔时间);
​		关闭定时器
​			cleatInterVal(timer);
​		示例:

```javascript
function fn() {
	console.log('一秒执行一次')
}
let n = setInterval(fn, 1000)
// setInterval('fn()', 1000)
console.log(n)
// 关闭定时器
clearInterval(n)
```
## DOM事件操作

### 	事件监听

元素对象.addEventListener('事件类型','要执行的函数');
​事件监听三要素:

- 事件源:那个dom元素被事件触发了,要获取dom元素
- 事件类型:用什么方式触发,比如鼠标单击click.鼠标经过mouseover等
- 事件调用的函数:要做什么

```javascript
const btn = document.querySelector('.btn');
btn.addEventListener('click',function(){
	alert('点击了');
})
```

### 事件类型

常见的事件类型:

- 鼠标事件:click（鼠标点击）、mouseenter（鼠标经过）、mouseleave（鼠标离开））
- 焦点事件:focus（获得焦点）、blur（失去焦点）
- 键盘事件:keydown（键盘按下触发）、keyup（键盘抬起触发）
- 文本事件:input（用户输入事件）

事件类型决定了事件被触发的方式，如 `click` 代表鼠标单击，`dblclick` 代表鼠标双击。

### 	事件对象

任意事件类型被触发时与事件相关的信息会被以对象的形式记录下来，我们称这个对象为事件对象。
例如:鼠标点击事件中,事件对象就存了鼠标点在哪个位置等信息

```js
元素.addEventListener('事件类型',function(e){
	console.log(e);//此处的e就是事件对象
})
//示例
const btn = document.querySelector('#btn')
        // document.write(btn)

        const text = document.write("等待时间发生")
        btn.addEventListener('click',function(e){
            alert('用户点击了按钮')
            document.write(e) //[object PointerEvent]
        })
```

常用属性

- type：获取当前的事件类型
- clientX/clientY：获取光标相对于浏览器可见窗口左上角的位置
- offsetX/offsetY：获取光标相对于当前DOM元素左上角的位置
- key：用户按下的键盘键

注：在事件回调函数内部通过 window.event 同样可以获取事件对象。

### 	环境对象

环境对象指的是函数内部特殊的变量 `this` ，它代表着当前函数运行时所处的环境。

```html
 <script>
 		// 声明函数
        function sayHi() {
            // this 是一个变量
            console.log(this);
        }
        // 声明一个对象
        let user = {
            name: '张三',
            sayHi: sayHi // 此处把 sayHi 函数，赋值给 sayHi 属性
        }
        let person = {
            name: '李四',
            sayHi: sayHi
        }
        // 直接调用
        sayHi() // window
        window.sayHi() // window
        // 做为对象方法调用
        user.sayHi()// user
        person.sayHi()// person
    </script>
```

结论：

1. `this` 本质上是一个变量，数据类型为对象
2. 函数的调用方式不同 `this` 变量的值也不同
3. 判断 `this` 值的粗略规则【谁调用 `this` 就是谁】
4. 函数直接调用时实际上 `window.sayHi()` 所以 `this` 的值为 `window`

### 	回调函数	

如果将函数A做为参数传递给函数B时,我们称函数A为回调函数
​简单理解:当一个函数当做参数来传递给另外一个函数

```html
<script>
	function bar() {
    	console.log('函数也能当参数...');
  	}
  	// 函数 bar做参数传给了foo函数，bar就是所谓的回调函数
  	foo(bar);
 </script>   
```

结论：

1. 回调函数本质还是函数，只不过把它当成参数使用
2. 使用匿名函数做为回调函数比较常见

## 事件流

事件流指的是事件完整执行过程中的流动路径

![1722145307642](D:\实验室\文档\note\typora-user-images\1722145307642.png)

- 假设页面里有个div，当触发事件时，会经历两个阶段，分别是捕获阶段、冒泡阶段
- 简单来说：捕获阶段是 从父到子  冒泡阶段是从子到父
- 实际工作都是使用事件冒泡为主

### 注册事件

两种注册事件的区别

- 传统on注册（L0）
  多一句没有，少一句不行，用最短时间，教会最实用的技术！
  同一个对象,后面注册的事件会覆盖前面注册(同一个事件)
  直接使用null覆盖偶就可以实现事件的解绑
  都是冒泡阶段执行的
- 事件监听注册（L2）
  语法: addEventListener(事件类型, 事件处理函数, 是否使用捕获)
  后面注册的事件不会覆盖前面注册的事件(同一个事件)
  可以通过第三个参数去确定是在冒泡或者捕获阶段执行
  必须使用removeEventListener(事件类型, 事件处理函数, 获取捕获或者冒泡阶段)
  匿名函数无法被解绑

### 事件捕获

 事件捕获概念：从DOM的根元素开始去执行对应的事件 (从外到里)

```html
document.addlistener(事件类型,事件处理函数,是否使用捕获机制)
```

- addEventListener第三个参数传入 true 代表是捕获阶段触发（很少使用）
- 若传入false代表冒泡阶段触发，默认就是false
- 若是用事件监听，则只有冒泡阶段，没有捕获

### 事件冒泡

事件冒泡: 当一个元素的事件被触发时，同样的事件将会在该元素的**所有祖先元素中依次被触发**。这一过程被称为事件冒泡

```html
//点击fa之后会依次弹出我是爷爷，我是爸爸
//点击son之后会依次弹出爷爷，我是、爸爸、儿子
<div class="father">
    <div class="son"></div>
  </div>
  <script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')
    document.addEventListener('click', function () {
      alert('我是爷爷')
    }, true)
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    }, true)
    son.addEventListener('click', function () {
      alert('我是儿子')
    }, true)

  </script>
```

### 阻止冒泡

事件冒泡会影响到父级元素，若想把事件就限制在当前元素内，就需要阻止事件冒泡，使用以下命令实现这个功能:`事件.stopPropagation()`

```html
<script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')

    document.addEventListener('click', function () {
      alert('我是爷爷')
    })
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    })
    son.addEventListener('click', function (e) {
      alert('我是儿子')
      // 组织流动传播  事件对象.stopPropagation()
      e.stopPropagation()
    })

  </script>
```

注意：此方法可以阻断事件流动传播，不光在冒泡阶段有效，捕获阶段也有效

我们某些情况下需要阻止默认行为的发生，比如 阻止 链接的跳转，表单域跳转,可以使用以下命令进行全局配置。`e.preventDefault()`

### 	事件解绑

传统做法:直接给事件赋值为空即可

```javascript
const btn=document.querySelector('button');
btn.onclick=function(){
	alert('点击率');
	btn.onclick=null;
}
```

解绑事件:`removeEventListener(事件类型, 事件处理函数, [获取捕获或者冒泡阶段])`

```javascript
const btn=document.querySelector('button');
function fn() {
	alert('点击了')
}
btn.addEventListener('click', fn)
// L2 事件移除解绑
btn.removeEventListener('click', fn)
```

注意:匿名函数无法被解绑,所以必须给解绑事件的第二个参数赋值一个函数名

### 	 事件委托

大量的事件监听是比较耗费性能的，比如说，给以下li注册点击事件是特别浪费性能的。

```html
<ul>
    <li>我是第一个</li>
    <li>我是第二个</li>
    <li>我是第三个</li>
    <li>我是第四个</li>
  </ul>
  <script>
    // 给多个li进行注册点击事件
    const list = document.querySelectorAll('ul li')
    for (let i =0;i<list.length;i++){
      list[i].addEventListener('click',function(){
        alert('我被点击了')
      })
    }
  </script>
```

事件委托是利用事件流的特征解决一些开发需求的知识技巧

- 优点：减少注册次数，可以提高程序性能

- 原理：事件委托其实是利用事件冒泡的特点。

  给父元素注册事件，当我们触发子元素的时候，会冒泡到父元素身上，从而触发父元素的事件
  ​实现：事件对象.target.tagName 可以获得真正触发事件的元素

```javascript
  <ul>
    <li>第1个孩子</li>
    <li>第2个孩子</li>
    <li>第3个孩子</li>
    <li>第4个孩子</li>
    <li>第5个孩子</li>
    <p>我不需要变色</p>
  </ul>
  <script>
    // 点击每个小li 当前li 文字变为红色
    // 按照事件委托的方式  委托给父级，事件写到父级身上
    // 1. 获得父元素
    const ul = document.querySelector('ul')
    ul.addEventListener('click', function (e) {
 
      // 我的需求，我们只要点击li才会有效果
      if (e.target.tagName === 'LI') {
        e.target.style.color = 'red'
      }
    })
  </script>
```

事件对象.target. tagName 可以获得真正触发事件的元素

### 	其他事件

#### 	页面加载事件

加载外部资源（如图片.外联CSS和JavaScript等）加载完毕时触发的事件，有些时候需要等页面资源全部处理完了做一些事情
​老代码喜欢把 script 写在 head 中，这时候直接找监听页面所有资源加载完毕：
​给window 添加 load 事件：

```javascript
windows.addEventListener('load',function(){
	//执行操作
})
```

给dom添加load事件

```javascript
div.addEventListener('load',function(){
	//执行操作
})
```

当初始的HTML文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，而无需等待样式表.图像等完全加载

```javascript
document.addEventListener('DOMContentLoaded', function () {
	//执行操作
})
```

#### 	元素滚动事件

滚动条在滚动的时候持续触发的事件
​监听整个页面滚动：
​给window或document添加scroll事件

```javascript
window.addEventListener('scroll', function () {
	//执行操作
})
```

监听某个元素的内部滚动直接给某个元素加即可：
​scrollLeft和scrollTop（属性）
​	获取被卷去的大小
​		获取元素内容往左.往上滚出去看不到的距离
​		这两个值是可读
​document.documentElement.scrollTop
​页面滚动事件-滚动到指定的坐标
​		scrollTo()方法可把内容滚动到指定的坐标
​		语法：	

```javascript
//将页面滚动到离x和y轴相应的位置
window.scrollTo(x,y);
```

#### 	页面尺寸事件

会在窗口尺寸改变的时候触发事件：

```javascript
window.addEventListener('resize', function () {
	//获取页面的宽度
	const w=document.documentElement.clientWidth;
})
```

获取宽高：
​		获取元素的可见部分宽高（不包含边框，margin，滚动条等）
​		clientWidth和clientHeight

#### 	元素尺寸于位置-尺寸

​		offsetWidth和offsetHeight
​		获取出来的是数值,方便计算
​		注意: 获取的是可视宽高, 如果盒子是隐藏的,获取的结果是0
​		offsetLeft和offsetTop注意是只读属性

## DOM节点

DOM节点：DOM树里每一个内容都称之为节点

- 元素节点 比如 div标签
- 属性节点 比如 class属性
- 文本节点 比如标签里
- 对节点进行增删改查

### 查找节点

```javascript
//查找父节点
子节点.parentNode  
//查找子节点
父节点.children 
//注意：此处获得的子节点是一个伪数组
//下一个兄弟节点
nextElementSibling 属性
//上一个兄弟节点
previousElementSibling 属性

// 示例
<body>
  <button class="btn1">所有的子节点</button>
  <!-- 获取 ul 的子节点 -->
  <ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript 基础</li>
    <li>Web APIs</li>
  </ul>
  <script>
    const btn1 = document.querySelector('.btn1')
    btn1.addEventListener('click', function () {
      // 父节点
      const ul = document.querySelector('ul')

      // 所有的子节点
      console.log(ul.childNodes)
      // 只包含元素子节点
      console.log(ul.children)
    })
  </script>
</body>
```

### 删除节点

```javascript
父节点.removeChild(要删除的元素)

// 示例
 <!-- 点击按钮删除节点 -->
  <button>删除节点</button>
  <ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>Web APIs</li>
  </ul>

  <script>
    const btn = document.querySelector('button')
    btn.addEventListener('click', function () {
      // 获取 ul 父节点
      let ul = document.querySelector('ul')
      // 待删除的子节点
      let lis = document.querySelectorAll('li')

      // 删除节点
      ul.removeChild(lis[0])
    })
  </script>
```

### 增加节点

```javascript
//创建节点
document.createElment('元素节点');
//增加节点，要想在界面看到，还得插入到某个父元素
父元素.insertBefore('要插入的元素','在哪个元素前面')
父元素.appendChild('要插入的元素')

// 示例
<h3>插入节点</h3>
  <p>在现有 dom 结构基础上插入新的元素节点</p>
  <hr>
  <div class="box"></div>
  <!-- 点击按钮向 box 盒子插入节点 -->
  <button class="btn">插入节点</button>
  <script>
    // 点击按钮，在网页中插入节点
    const btn = document.querySelector('.btn')
    btn.addEventListener('click', function () {
      // 1. 获得一个 DOM 元素节点
      const p = document.createElement('p')
      p.innerText = '创建的新的p标签'
      p.className = 'info'
      
      // 复制原有的 DOM 节点
      const p2 = document.querySelector('p').cloneNode(true)
      p2.style.color = 'red'

      // 2. 插入盒子 box 盒子
      document.querySelector('.box').appendChild(p)
      document.querySelector('.box').appendChild(p2)
    })
  </script>
```

 特殊情况下，我们新增节点，按照如下操作：  

1. 复制一个原有的节点 
2. 把复制的节点放入到指定的元素内部

cloneNode会克隆出一个跟原标签一样的元素，括号内传入布尔值 

- 若为true，则代表克隆时会包含后代节点一起克隆 
- 若为false，则代表克隆时不包含后代节点 ,默认为false


```javascript
const ul=document.querySelector('ul');
const li1=ul.children[0].cloneNode(true);
ul.appendChild(li1);//追加元素在ul中
```

### M端事件

移动端也有自己独特的地方。比如触屏事件 touch（也称触摸事件），Android 和 IOS 都有。

 常见的触屏事件如下：

![1722266848806](.\typora-user-images\1722266848806.png)

### 重绘和回流

浏览器是如何进行界面渲染的

![1722271966703](.\typora-user-images\1722271966703.png)

-  解析（Parser）HTML，生成DOM树(DOM Tree)
- 同时解析（Parser） CSS，生成样式规则 (Style Rules)
- 根据DOM树和样式规则，生成渲染树(Render Tree)
- 进行布局 Layout(回流/重排):根据生成的渲染树，得到节点的几何信息（位置，大小）
- 进行绘制 Painting(重绘): 根据计算和获取的信息进行整个页面的绘制
- Display: 展示在页面上

回流(重排):当 Render Tree 中部分或者全部元素的尺寸、结构、布局等发生改变时，浏览器就会重新渲染部分或全部文档的过程称为 回流。

重绘:由于节点(元素)的样式的改变并不影响它在文档流中的位置和文档布局时(比如：color、background-color、outline等), 称为重绘。
**重绘不一定引起回流，而回流一定会引起重绘。**

## BOM对象

### js的组成

![1722272186144](.\typora-user-images\1722272186144.png)

- ECMAScript:
  - 规定了js基础语法核心知识。
  - 比如：变量、分支语句、循环语句、对象等等

- Web APIs :
  - DOM   文档对象模型， 定义了一套操作HTML文档的API
  - BOM   浏览器对象模型，定义了一套操作浏览器窗口的API

### window对象

#### BOM(浏览器对象模型) 

BOM(Browser Object Model ) 是浏览器对象模型，像document.alert()、console.log()这些都是window的属性，基本BOM的属性和方法都是window的。

![1722272529676](D:\实验室\文档\note\typora-user-images\1722272529676.png)

##### 定时器-延时函数 

JavaScript 内置的一个用来让代码延迟执行的函数，叫 setTimeout，**setTimeout 仅仅只执行一次**，所以可以理解为就是把一段代码延迟执行, 平时省略window，每一次调用延时器都会产生一个新的延时器

```javascript
let timer=setTimeout(function () {
      img.style.display = 'none' //3秒之后，让图片消失
 }, 3000)
//清除延时函数：
clearTimeout(timer);
```

##### JS执行机制

1. 先执行执行栈中的同步任务。

2. 异步任务放入任务队列中。 

3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待 状态，进入执行栈，开始执行。

   JS 的异步是通过回调函数实现的。 一般而言，异步任务有以下三种类型: 

   ​	1.普通事件，如 click.resize 等 

   ​	2.资源加载，如 load.error 等 

   ​	3.定时器，包括 setInterval.setTimeout 等 异步任务相关添加到任务队列中（任务队列也称为消息队列)。

 由于主线程不断的重复获得任务.执行任务.再获取任务.再执行，所以这种机制被称为事件循环（ event loop) 

##### location对象 

location (地址) 它拆分并保存了 URL 地址的各个组成部分， 它是一个对象

常用属性和方法： 

![1722272762500](D:\实验室\文档\note\typora-user-images\1722272762500.png)

##### navigator对象

navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息

通过 userAgent 检测浏览器的版本及平台

```js
// 检测 userAgent（浏览器信息）
(function () {
  const userAgent = navigator.userAgent
  // 验证是否为Android或iPhone
  const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
  const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
  // 如果是Android或iPhone，则跳转至移动站点
  if (android || iphone) {
    location.href = 'http://m.itcast.cn'
  }})();
```

##### histroy对象

history 的数据类型是对象，主要管理历史记录， 该对象与浏览器地址栏的操作相对应,如前进.后退.历史记录等history对象一般在实际开发中比较少用，但是会在一些OA 办公系统中见到

### 本地存储

本地存储：将数据存储在本地浏览器中

好处：

1、页面刷新或者关闭不丢失数据，实现数据持久化

2、容量较大，sessionStorage和 localStorage 约 5M 左右

#### **本地存储简单数据类型**localStorage（重点）

localStorage 把数据存储的浏览器中 ，可以将数据永久存储在本地(用户的电脑), 除非手动删除，否则关闭页面也会存在。

```javascript
//存储数据：
localStorage.setItem(key, value)
//获取数据
localStorage.getItem(key)
//删除数据
localStorage.removeItem(key)

//示例
<script>
    // 本地存储 - localstorage 存储的是字符串 
    // 1. 存储
    localStorage.setItem('age', 18)

    // 2. 获取
    console.log(typeof localStorage.getItem('age'))

    // 3. 删除
    localStorage.removeItem('age')
  </script>
```

**注意：存储的时候，如果原来有这个键，则是改，如果么有这个键是增**

#### 本地存储复杂数据类型

本地只能存储字符串,无法存储复杂数据类型，如果需要存储复杂数据类型则需要类型转换，将复杂数据类型转换为json字符串存储在本地中。

```javascript
const obj = {
      uname: '张老师',
      age: 18,
      gender: '女'
    }
//本地只能存储字符串,无法存储复杂数据类型，需要解析成json格式
localStorage.setItem('obj', JSON.stringify(obj));
alert(localStorage.getItem('obj'))
```

浏览器要使用数据的时候，因为，本地存储里面取出来的是字符串，不是对象，无法直接使用。所以，需要将json字符串再转换为字符串。

```javascript
const str = JSON.parse(localStorage.getItem('obj'));
```

#### sessionStorage

特性：

- 用法跟localStorage基本相同
- 区别是：当页面浏览器被关闭时，存储在 sessionStorage 的数据会被清除

存储：sessionStorage.setItem(key,value)

获取：sessionStorage.getItem(key)

删除：sessionStorage.removeItem(key)

#### 数组中的相关方法

##### map方法迭代数组

map 可以处理数据，并且返回新的数组

```javascript
const arr = ['张三', '李四', '王五'];
const newArr = arr.map(function (item, index) {
      console.log(item)
      console.log(index)
      return item + '老师';
 })
```

##### 数组中join方法

join() 方法用于把数组中的所有元素转换一个字符串，数组元素是通过参数里面指定的分隔符进行分隔的；

```javascript
const arr = ['张三', '李四', '王五'];
arr.join('*');
console.log( arr.join(';')) //张三;李四;王五
```

### 正则

#### 基本使用

~~~JavaScript
const reg =  /表达式/
~~~

其中` / / `是正则表达式字面量，正则表达式也是对象 

test()方法用来查看正则表达式与指定的字符串是否匹配，如果正则表达式与指定的字符串匹配 ，返回true，否则false

~~~html
 <script>
    // 正则表达式的基本使用
    const str = 'web前端开发'
    // 1. 定义规则
    const reg = /web/
    // 2. 使用正则test()
    console.log(reg.test(str))  // true  如果符合规则匹配上则返回true
    console.log(reg.test('java开发'))  // false  如果不符合规则匹配上则返回false
  </script>
~~~

#### 元字符

元字符是一些具有特殊含义的字符，可以极大提高了灵活性和强大的匹配功能。

比如，规定用户只能输入英文26个英文字母，换成元字符写法： /[a-z]/  

```javascript
  <script>
	const reg=/[a-z]/;
 	const str='sdsvfd';
 	console.log(reg.test(str));//true
  </script>
```

#### 边界符

正则表达式中的边界符用来提示字符所处的位置,主要有两个字符`^`和`$`,其中`^`表示匹配开头,而`$`表示匹配结尾

~~~html
<body>
  <script>
    // 元字符之边界符
    // 1. 匹配开头的位置 ^
    const reg = /^web/
    console.log(reg.test('web前端'))  // true
    console.log(reg.test('前端web'))  // false
    // 2. 匹配结束的位置 $
    const reg1 = /web$/
    console.log(reg1.test('web前端'))  //  false
    console.log(reg1.test('前端web'))  // true
    // 3. 精确匹配 ^ $
    const reg2 = /^web$/
    console.log(reg2.test('web前端'))  //  false 
  </script>
</body>
~~~

#### 量词

量词用来设定某个模式重复次数

- **\+ 表示重复至少 1 次**
-  **? 表示重复 0 次或1次** 

- **表示重复 0 次或多次**
- **{m, n} 表示复 m 到 n 次**

~~~html
<body>
  <script>
    // 元字符之量词
    // 1. * 重复次数 >= 0 次
    const reg1 = /^w*$/
    console.log(reg1.test(''))  // true
    console.log(reg1.test('w'))  // true
    console.log(reg1.test('ww'))  // true
    // 2. + 重复次数 >= 1 次
    const reg2 = /^w+$/
    console.log(reg2.test(''))  // false
    console.log(reg2.test('w'))  // true
    console.log(reg2.test('ww'))  // true
    // 3. ? 重复次数  0 || 1 
    const reg3 = /^w?$/
    console.log(reg3.test(''))  // true
    console.log(reg3.test('w'))  // true
    console.log(reg3.test('ww'))  // false
    // 4. {n} 重复 n 次
    const reg4 = /^w{3}$/
    console.log(reg4.test(''))  // false
    console.log(reg4.test('w'))  // flase
    console.log(reg4.test('ww'))  // false
    console.log(reg4.test('www'))  // true
    console.log(reg4.test('wwww'))  // false
  // 5. {n,} 重复次数 >= n 
    const reg5 = /^w{2,}$/
    console.log(reg5.test(''))  // false
    console.log(reg5.test('w'))  // false
    console.log(reg5.test('ww'))  // true
    console.log(reg5.test('www'))  // true
  // 6. {n,m}   n =< 重复次数 <= m
    const reg6 = /^w{2,4}$/
    console.log(reg6.test('w'))  // false
    console.log(reg6.test('ww'))  // true
    console.log(reg6.test('www'))  // true
    console.log(reg6.test('wwww'))  // true
    console.log(reg6.test('wwwww'))  // false
  </script>
~~~

**注意：{n,m}   n =< 重复次数 <= m中，逗号两侧千万不要加空格否则会匹配失败**

#### 范围

表示字符的范围，定义的规则限定在某个范围，比如只能是英文字母，或者数字等等，用表示范围

~~~html
 <script>
    // 元字符之范围  []  
    // 1. [abc] 匹配包含的单个字符， 多选1
    const reg1 = /^[abc]$/
    console.log(reg1.test('a'))  // true
    console.log(reg1.test('d'))  // false
    console.log(reg1.test('ab'))  // false
    // 2. [a-z] 连字符 单个
    const reg2 = /^[a-z]$/
    console.log(reg2.test('a'))  // true
    console.log(reg2.test('A'))  // false
    // 想要包含小写字母，大写字母 ，数字
    const reg3 = /^[a-zA-Z0-9]$/
    console.log(reg3.test('B'))  // true
    console.log(reg3.test('b'))  // true
    console.log(reg3.test(9))  // true
    console.log(reg3.test(','))  // flase
    // 用户名可以输入英文字母，数字，可以加下划线，要求 6~16位
    const reg4 = /^[a-zA-Z0-9_]{6,16}$/
    console.log(reg4.test('abcd1'))  // false 
    console.log(reg4.test('abcd12'))  // true
    console.log(reg4.test('ABcd12'))  // true
    console.log(reg4.test('ABcd12_'))  // true
    // 3. [^a-z] 取反符
    const reg5 = /^[^a-z]$/
    console.log(reg5.test('a'))  // false 
    console.log(reg5.test('A'))  // true
    console.log(reg5.test(8))  // true
  </script>
</body>
~~~

#### 字符类

某些常见模式的简写方式，区分字母和数字

```bash
\d # 匹配0-9的任意数字，相当于[0-9]
\D # 匹配0-9以外数字，相当于[^0-9]
\w # 匹配任意的数字和字符和下划线，相当于[a-zA-Z0-9_]
\W # 与上面的\w相反 [^a-zA-Z0-9_]
\s # 匹配所有的空格.换行符.制表符
\S # 与上面相反
```

#### 替换和修饰符

replace 替换方法，可以完成字符的替换

~~~html
 <script>
    // 替换和修饰符
    const str = '欢迎大家学习前端，相信大家一定能学好前端，都成为前端大神'
    // 1. 替换  replace  需求：把前端替换为 web
    // 1.1 replace 返回值是替换完毕的字符串
  const strEnd = str.replace(/前端/, 'web') 只能替换一个
  </script>
~~~

修饰符约束正则执行的某些细节行为，如是否区分大小写.是否支持多行匹配等

- i 是单词 ignore 的缩写，正则匹配时字母不区分大小写
- g 是单词 global 的缩写，匹配所有满足正则表达式的结果

~~~javascript
  <script>
    // 替换和修饰符
    const str = '欢迎大家学习前端，相信大家一定能学好前端，都成为前端大神'
    // 1. 替换replace需求：把前端替换为 web
    // 1.1 replace 返回值是替换完毕的字符串
    const strEnd = str.replace(/前端/, 'web') //只能替换一个
    // 2. 修饰符 g 全部替换
    const strEnd = str.replace(/前端/g, 'web')
    console.log(strEnd) 
  </script>
~~~

## javascript进阶

### 5.1.作用域链

作用域链本质上是底层的变量查找机制。 

Ø 在函数被执行时，会优先查找当前函数作用域中查找变量 

Ø 如果当前作用域查找不到则会依次逐级查找父级作用域直到全局作用域

注意：

1. 嵌套关系的作用域串联起来形成了作用域链 
2. 相同作用域链中按着从小到大的规则查找变量
3. 子作用域能够访问父作用域，父级作用域无法访问子级作用域

### 5.2.JS垃圾回收机制

垃圾回收机制(Garbage Collection) 简称 GC，JS中内存的分配和回收都是自动完成的，内存在不使用的时候会被垃圾回收器自动回收。

JS环境中分配的内存, 一般有如下生命周期： 

内存分配：当我们声明变量、函数、对象的时候，系统会自动为他们分配内存 

内存使用：即读写内存，也就是使用变量、函数等 

内存回收：使用完毕，由垃圾回收自动回收不再使用的内存 

说明 

全局变量一般不会回收(关闭页面回收)； 

一般情况下局部变量的值, 不用了, 会被自动回收掉；

### 5.3.闭包 

概念：一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域 

简单理解：闭包 =  内层函数 + 外层函数的变量

```javascript
//闭包的使用  
function count(){
    //此处如果i为全局变量，那么变量的值就很容易被修改，
    //但是如果是使用闭包，那么就可以保证数据不容易被轻易修改
  let i=0;
  function fun(){
   i++;
   console.log(`函数被调用了${i}次数`)
  }
  return fun
}
const sum= count();
```

注意：

闭包的作用 

Ø 封闭数据，实现数据私有，外部也可以访问函数内部的变量 

Ø 闭包很有用，因为它允许将函数与其所操作的某些数据(环境)关联起来 

闭包可能引起的问题 

内存泄漏

### 5.3.变量提升

变量提升是 JavaScript 中比较“奇怪”的现象，它允许在变量声明之前即被访问（仅存在于var声明变量）

```javascript
console.log(str+'hello');
var str='javascript';
```

### 5.4.函数提升

函数提升与变量提升比较类似，是指函数在声明之前即可被调用

总结： 

1. 函数提升能够使函数的声明调用更灵活 
2. 函数表达式不存在提升的现象 
3. 函数提升出现在相同作用域当中

```javascript
foo();
function foo(){
    console.log('申明之前调用');
}
foo2();
const foo2=function(){
    console.log(' 函数表达式不存在提升的现象');//错误的写法，不能够这样表示
}
```

### 5.5.函数参数

#### 动态参数 

arguments 是函数内部内置的伪数组变量，它包含了调用函数时传入的所有实参

```javascript
//解决传入不定个数个参数时的函数
function sum(){
    let s=0;
    for(let i=0;i<arguments.length;i++){
      s+=arguments[i]
    }
    console.log(s)
  }
  sum(12,434)//446
  sum(12,3,23,4,55)//97
```

1. arguments 是一个伪数组，只存在于函数中 
2. arguments 的作用是动态获取函数的实参 
3. 可以通过for循环依次得到传递过来的实参

#### 剩余参数

用于获取多余的实参

```javascript
function getSum(...other){
	console.log(other);//12,23,45,33
}
getSum(12,23,45,33);
```

总结：

1. `...` 是语法符号，置于最末函数形参之前，用于获取多余的实参
2. 借助 `...` 获取的剩余实参，是个真数组

#### 展开运算符

展开运算符(…),将一个数组进行展开，不会修改原数组；

典型运用场景： 求数组最大值(最小值)、合并数组等

```javascript
const arr=[12,3,4,5,6];
console.log(...arr);//12,3,4,5,6
console.log(Math.max(...arr));//12
const arr1=[6,7,8,9];
const arr3=[...arr,...arr1];//12,3,4,5,6,6,7,8,9
```

### 5.6.箭头函数

箭头函数是一种声明函数的简洁语法，它与普通函数并无本质的区别，差异性更多体现在语法格式上。

```javascript
const fn=()=>{
    console.log('1234')
}
fn()
const onlyOne=x=>{       //只有一个形参的时候，可以省略小括号
    console.log(x)
}
onlyOne(3)
// 3. 只有一行代码的时候，我们可以省略大括号
const fns = x => console.log(x)
fns(1)
// 4. 只有一行代码的时候，可以省略return
const fnn = x => x + x
console.log(fnn(1))
// 5. 箭头函数可以直接返回一个对象
const fn = (uname) => ({ uname: uname })
console.log(fn('刘德华'))
```

总结：

1. 箭头函数属于表达式函数，因此不存在函数提升
2. 箭头函数只有一个参数时可以省略圆括号 `()`
3. 箭头函数函数体只有一行代码时可以省略花括号 `{}`，并自动做为返回值被返回

#### 参数

箭头函数中没有 `arguments`，只能使用 `...` 动态获取实参

~~~js
 <script>
    // 1. 利用箭头函数来求和
    const getSum = (...arr) => {
      let sum = 0
      for (let i = 0; i < arr.length; i++) {
        sum += arr[i]
      }
      return sum
    }
    const result = getSum(2, 3, 4)
    console.log(result) // 9
  </script>
~~~

#### 箭头函数 this

箭头函数不会创建自己的this,它只会从自己的作用域链的上一层沿用this。

```js
//箭头函数的this是上一层作用域的this 指向
const fn = () => {
   console.log(this)  // window
}
fn()
// 对象方法箭头函数 this
const obj = {
   uname: 'pink老师',
   sayHi: () => {
   		console.log(this)  // this 指向谁？ window
   }
}
obj.sayHi()
```

### 5.7.解构赋值

解构赋值是一种快速为变量赋值的简洁语法，本质上仍然是为变量赋值，分为数组解构、对象解构两大类型。

#### 数组解构

数组解构是将数组的单元值快速批量赋值给一系列变量的简洁语法，如下代码所示：

```js
let arr=[1,2,4];
// 批量声明变量 a b c 
// 同时将数组单元值 1 2 3 依次赋值给变量 a b c
let [a,b,c]=arr;
console.log(a)//1
console.log(b)//2
console.log(c)//4
```

总结：

1. 赋值运算符 `=` 左侧的 `[]` 用于批量声明变量，右侧数组的单元值将被赋值给左侧的变量
2. 变量的顺序对应数组单元值的位置依次进行赋值操作
3. 变量的数量大于单元值数量时，多余的变量将被赋值为  `undefined`
4. 变量的数量小于单元值数量时，可以通过 `...` 获取剩余单元值，但只能置于最末位
5. 允许初始化变量的默认值，且只有单元值为 `undefined` 时默认值才会生效

注：支持多维解构赋值，比较复杂后续有应用需求时再进一步分析

#### 对象解构

对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法，如下代码所示：

```html
<script>
  // 普通对象
  const user = {
    name: '小明',
    age: 18
  };
  // 批量声明变量 name age
  // 同时将数组单元值 小明  18 依次赋值给变量 name  age
  const {name, age} = user
  console.log(name) // 小明
  console.log(age) // 18
</script>
```

总结：

1. 赋值运算符 `=` 左侧的 `{}` 用于批量声明变量，右侧对象的属性值将被赋值给左侧的变量
2. 对象属性的值将被赋值给与属性名相同的变量
3. 对象中找不到与变量名一致的属性时变量值为 `undefined`
4. 允许初始化变量的默认值，属性不存在或单元值为 `undefined` 时默认值才会生效

注：支持多维解构赋值

## 6.深入对象

### 6.1.构造函数

构造函数是专门用于创建对象的函数，如果一个函数使用 `new` 关键字调用，那么这个函数就是构造函数。

```html
<script>
  // 定义函数
  function foo() {
    console.log('通过 new 也能调用函数...');
  }
  // 调用函数
  new foo;
</script>
```

总结：

2. 使用 `new` 关键字调用函数的行为被称为实例化
3. 实例化构造函数时没有参数时可以省略 `()`
4. 构造函数的返回值即为新创建的对象
5. 构造函数内部的 `return` 返回的值无效！

注：实践中为了从视觉上区分构造函数和普通函数，习惯将构造函数的首字母大写。

### 6.2.实例成员

通过构造函数创建的对象称为实例对象，实例对象中的属性和方法称为实例成员。

```html
<script>
  // 构造函数
  function Person() {
    // 构造函数内部的 this 就是实例对象
    // 实例对象中动态添加属性
    this.name = '小明'
    // 实例对象动态添加方法
    this.sayHi = function () {
      console.log('大家好~')
    }
  }
  // 实例化，p1 是实例对象
  // p1 实际就是 构造函数内部的 this
  const p1 = new Person()
  console.log(p1)
  console.log(p1.name) // 访问实例属性
  p1.sayHi() // 调用实例方法
</script>
```

总结：

1. 构造函数内部 `this` 实际上就是实例对象，为其动态添加的属性和方法即为实例成员
2. 为构造函数传入参数，动态创建结构相同但值不同的对象

注：构造函数创建的实例对象彼此独立互不影响。

### 6.3.静态成员

在 JavaScript 中底层函数本质上也是对象类型，因此允许直接为函数动态添加属性或方法，构造函数的属性和方法被称为静态成员。

```html
<script>
  // 构造函数
  function Person(name, age) {
    // 省略实例成员
  }
  // 静态属性
  Person.eyes = 2
  Person.arms = 2
  // 静态方法
  Person.walk = function () {
    console.log('^_^人都会走路...')
    // this 指向 Person
    console.log(this.eyes)
  }
</script>
```

总结：

1. 静态成员指的是添加到构造函数本身的属性和方法
2. 一般公共特征的属性或方法静态成员设置为静态成员
3. 静态成员方法中的 `this` 指向构造函数本身

### 6.4.内置构造函数

在 JavaScript 中**最主要**的数据类型有 6 种，分别是字符串、数值、布尔、undefined、null 和 对象，常见的对象类型数据包括数组和普通对象。其中字符串、数值、布尔、undefined、null 也被称为简单类型或基础类型，对象也被称为引用类型。

在 JavaScript 内置了一些构造函数，绝大部的数据处理都是基于这些构造函数实现的， `Date` 函数就是内置的构造函数。

```html
<script>
  // 实例化
	let date = new Date();
  // date 即为实例对象
  console.log(date);
</script>
```

甚至字符串、数值、布尔、数组、普通对象也都有专门的构造函数，用于创建对应类型的数据。

#### Object

`Object` 是内置的构造函数，用于创建普通对象。

```html
<script>
  // 通过构造函数创建普通对象
  const user = new Object({name: '小明', age: 15})
  // 这种方式声明的变量称为【字面量】
  let student = {name: '杜子腾', age: 21}
  // 对象语法简写
  let name = '小红';
  let people = {
    // 相当于 name: name
    name,
    // 相当于 walk: function () {}
    walk () {
      console.log('人都要走路...');
    }
  }
  console.log(student.constructor);
  console.log(user.constructor);
  console.log(student instanceof Object);
</script>
```

总结：

1. 推荐使用字面量方式声明对象，而不是 `Object` 构造函数
2. `Object.assign` 静态方法创建新的对象
3. `Object.keys` 静态方法获取对象中所有属性
4. `Object.values` 表态方法获取对象中所有属性值

#### Array

`Array` 是内置的构造函数，用于创建数组。

```html
<script>
  // 构造函数创建数组
  let arr = new Array(5, 7, 8);
  // 字面量方式创建数组
  let list = ['html', 'css', 'javascript']
</script>
```

数组赋值后，无论修改哪个变量另一个对象的数据值也会相当发生改变。

总结：

1. 推荐使用字面量方式声明数组，而不是 `Array` 构造函数

2. 实例方法 `forEach` 用于遍历数组，替代 `for` 循环 (重点)

3. 实例方法 `filter` 过滤数组单元值，生成新数组(重点)

4. 实例方法 `map` 迭代原数组，生成新数组(重点)

5. 实例方法 `join` 数组元素拼接为字符串，返回字符串(重点)

6. 实例方法  `find`  查找元素， 返回符合测试条件的第一个数组元素值，如果没有符合条件的则返回 undefined(重点)

7. 实例方法`every` 检测数组所有元素是否都符合指定条件，如果**所有元素**都通过检测返回 true，否则返回 false(重点)

8. 实例方法`some` 检测数组中的元素是否满足指定条件   **如果数组中有**元素满足条件返回 true，否则返回 false

9. 实例方法 `concat`  合并两个数组，返回生成新数组

10. 实例方法 `sort` 对原数组单元值排序

11. 实例方法 `splice` 删除或替换原数组单元

12. 实例方法 `reverse` 反转数组

13. 实例方法 `findIndex`  查找元素的索引值


#### 包装类型

在 JavaScript 中的字符串、数值、布尔具有对象的使用特征，如具有属性和方法，如下代码举例：

```html
<script>
  // 字符串类型
  const str = 'hello world!'
 	// 统计字符的长度（字符数量）
  console.log(str.length)
  // 数值类型
  const price = 12.345
  // 保留两位小数
  price.toFixed(2) // 12.34
</script>
```

之所以具有对象特征的原因是字符串、数值、布尔类型数据是 JavaScript 底层使用 Object 构造函数“包装”来的，被称为包装类型。

#### String

`String` 是内置的构造函数，用于创建字符串。

```html
<script>
  // 使用构造函数创建字符串
  let str = new String('hello world!');

  // 字面量创建字符串
  let str2 = '你好，世界！';

  // 检测是否属于同一个构造函数
  console.log(str.constructor === str2.constructor); // true
  console.log(str instanceof String); // false
</script>
```

总结：

1. 实例属性 `length` 用来获取字符串的度长(重点)
2. 实例方法 `split('分隔符')` 用来将字符串拆分成数组(重点)
3. 实例方法 `substring（需要截取的第一个字符的索引[,结束的索引号]）` 用于字符串截取(重点)
4. 实例方法 `startsWith(检测字符串[, 检测位置索引号])` 检测是否以某字符开头(重点)
5. 实例方法 `includes(搜索的字符串[, 检测位置索引号])` 判断一个字符串是否包含在另一个字符串中，根据情况返回 true 或 false
5. 实例方法 `toUpperCase` 用于将字母转换成大写
7. 实例方法 `toLowerCase` 用于将就转换成小写
8. 实例方法 `indexOf`  检测是否包含某字符
9. 实例方法 `endsWith` 检测是否以某字符结尾
10. 实例方法 `replace` 用于替换字符串，支持正则匹配
13. 实例方法 `match` 用于查找字符串，支持正则匹配

注：String 也可以当做普通函数使用，这时它的作用是强制转换成字符串数据类型。

#### Number

`Number` 是内置的构造函数，用于创建数值。

```html
<script>
  // 使用构造函数创建数值
  let x = new Number('10')
  let y = new Number(5)
  // 字面量创建数值
  let z = 20
</script>
```

总结：

1. 推荐使用字面量方式声明数值，而不是 `Number` 构造函数
2. 实例方法 `toFixed` 用于设置保留小数位的长度

### 6.5.封装

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。同样的将变量和函数组合到了一起并能通过 this 实现数据的共享，所不同的是借助构造函数创建出来的实例对象之间是彼此不影响的。

```html
<script>
  function Person() {
    this.name = '佚名'
    // 设置名字
    this.setName = function (name) {
      this.name = name
    }
    // 读取名字
    this.getName =() => {
      console.log(this.name)
    }
  }
  // 实例对像，获得了构造函数中封装的所有逻辑
  let p1 = new Person()
  p1.setName('小明')
  console.log(p1.name);//小明
  // 实例对象
  let p2 = new Person()
  console.log(p2.name)//佚名
</script>
```

总结：

​		构造函数体现了面向对象的封装特性

​		构造函数实例创建的对象彼此独立、互不影响
