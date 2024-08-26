# Ajax

## 初识Ajax

URL地址一般由三部组成

1. 客户端与服务器之间的通信协议
2. 存有该资源的服务器名称 
3. 资源在服务器上具体的存放位置

```js
 https://mbd.baidu.com/newspage/data/index.html
https:  通信协议
mbd.baidu.com  服务器名称
newspage/data/index.html   资源在服务器上具体的存放位置
```

**网页中如何请求数据**

如果要在网页中请求服务器上的数据资源，则需要用到 XMLHttpRequest 对象。XMLHttpRequest（简称 xhr）是浏览器提供的 js 成员，通过它，可以请求服务器上的数据资源。

最简单的用法 

```js
var xhrObj = new XMLHttpRequest()
```

 **资源的请求方式**

客户端请求服务器时，请求的方式有很多种，最常见的两种请求方式分别为get和post请求。

- get 请求通常用于获取服务端资源（向服务器要资源） 

  例如：根据 URL 地址，从服务器获取 HTML 文件、css 文件、js文件、图片文件、数据资源等 

- post 请求通常用于向服务器提交数据（往服务器发送资源） 例如：登录时向服务器提交的登录信息、注册时向服务器提交的注册信息、添加用户时向服务器提交 的用户信息等各种数据提交操作

  Ajax的理解:在网页中利用 XMLHttpRequest` 对象和服务器进行数据交互的方式就是Ajax。

  ![1722529689841](.\typora-user-images\1722529689841.png)

## jQuery中的Ajax

浏览器中提供的 XMLHttpRequest 用法比较复杂，所以 jQuery 对 XMLHttpRequest 进行了封装，提供了一 系列 Ajax 相关的函数，极大地降低了 Ajax 的使用难度。 

jQuery 中发起 Ajax 请求最常用的三个方法如下： 

- $.get() 
- $.post()
- $.ajax()

### $.get()函数

$.get() 函数专门用来发起 get 请求，从而将服务器上的资源请求到客户端来进行使用。

```js
$.get(url, [data], [callback])
//url string 是必选示要请求的资源地址
//data object 不是必选表示请求资源期间要携带的参数
//callback function 不是必选表示请求成功时的回调函数
```

使用 $.get() 函数发起不带参数的请求时，直接提供请求的 URL 地址和请求成功之后的回调函数即可，示例代 码如下：

```js
$.get('http://www.liulongbin.top:3006/api/getbooks', function(res) { 
    console.log(res) // 这里的 res 是服务器返回的数据 
})
```

使用 $.get() 函数发起带参数的请求时，示例代码如下：

```js
$.get('http://www.liulongbin.top:3006/api/getbooks', {id: 1}, function(res) { 
    console.log(res) 
})
```

### $.post()函数

$.post() 函数专门用来发起 post请求，从而将服务器上的资源请求到客户端来进行使用。

```js
$.post(url, [data], [callback])
//url string 是必选示要提交数据的地址
//data object 不是必选表示要提交的数据
//callback function 不是必选表示数据提交成功时的回调函数
```

使用 $.post() 向服务器提交数据的示例代码如下：

```js
$.post('http://www.liulongbin.top:3006/api/addbook', // 请求的URL地址
	{ bookname: '水浒传', author: '施耐庵', publisher: '上海图书出版社' }, // 提交的数据
	function(res) { // 回调函数
	console.log(res)
})
```

### $.ajax()函数 

相比于 `$.get()` 和 `$.post()` 函数，jQuery 中提供的 $.ajax() 函数，是一个功能比较综合的函数，它允许我们对 Ajax 请求进行更详细的配置。

$.ajax() 函数的基本语法如下：

```js
$.ajax({ type: '', // 请求的方式，例如 GET 或 POST 
        url: '', // 请求的 URL 地址 
        data: { },// 这次请求要携带的数据 
        success: function(res) { 
        	//内容
        } // 请求成功之后的回调函数 
})
```

使用 $.ajax() 发起 GET 请求时，只需要将 type 属性的值设置为 'GET' 即可： 

```js
$.ajax({ 
    type: 'GET', // 请求的方式 
    url: 'http://www.liulongbin.top:3006/api/getbooks', // 请求的 URL 地址 
    data: { id: 1 },// 这次请求要携带的数据 
    success: function(res) { 
        // 请求成功之后的回调函数 
        console.log(res) 
    } 
})
```

使用 $.ajax() 发起 POST 请求时，只需要将 type 属性的值设置为 'POST' 即可： 

```js
$.ajax({ type: 'POST', // 请求的方式 
        url: 'http://www.liulongbin.top:3006/api/addbook', // 请求的 URL 地址 
        data: { // 要提交给服务器的数据 
            bookname: '水浒传', author: '施耐庵', publisher: '上海图书出版社' 
        }, 
        success: function(res) { 
            // 请求成功之后的回调函数 console.log(res) 
        } 
})
```

## form表单与模板引擎

### `<form>`标签的属性

`<form>`标签用来采集数据，`<form>`标签的属性则是用来规定**如何把采集到的数据发送到服务器**。

**1.action**

action 属性用来规定当提交表单时，**向何处发送表单数据**。

action 属性的值应该是后端提供的一个 URL 地址，这个 URL 地址专门负责接收表单提交过来的数据。

当 <form> 表单在未指定 action 属性值的情况下，action 的默认值为当前页面的 URL 地址。

**2.target**

target 属性用来规定**在何处打开** **action URL**。它的可选值有5个，默认情况下，target 的值是 _self，表示在相同的框架中打开 action URL。

**3.method**

method 属性用来规定**以何种方式**把表单数据提交到 action URL。

它的可选值有两个，分别是 get 和 post。

默认情况下，method 的值为 get，表示通过URL地址的形式，把表单数据提交到 action URL。

**4.enctype**

enctype 属性用来规定在**发送表单数据之前如何对数据进行编码**。

它的可选值有三个，默认情况下，enctype 的值为 application/x-www-form-urlencoded，表示在发送前编码所有的字符。

- application/x-www-form-urlencoded        在发送前编码所有字符（默认）   
- multipart/form-data        不对字符编码。   在使用包含文件上传控件的表单时，必须使用该值
-  text/plain        空格转换为 "+"   加号，但不对特殊字符编码,（很少用)。   

**注意：**

在涉及到**文件上传**的操作时，**必须**将 enctype 的值设置为 multipart/form-data

如果表单的提交不涉及到文件上传操作，则直接将 enctype 的值设置为 application/x-www-form-urlencoded 即可！

### **表单的同步提交**

通过点击submit按钮，触发表单提交的操作，从而使页面跳转到action URL 的行为，这里指的是login，叫做表单的同步提交。

```html
<form action="/login">
    <input type="text" name="user_name" />
    <input type="password" name="password" />
    <button type="submit">提交</button>
 </form>
```

如果使用表单提交数据，则会导致以下两个问题：

- 页面会发生跳转
- 页面之前的状态和数据会丢失

解决方案：

表单只负责采集数据，**Ajax** 负责将数据提交到服务器。

### ajax提交表单数据

在 jQuery 中，可以使用如下两种方式，监听到表单的提交事件：

```js
$('#form1').submit(function(e) {
 alert('监听到了表单的提交事件')
 })
 $('#form1').on('submit', function(e) {
 alert('监听到了表单的提交事件')
 })

//示例
<script>
	$(function(){
            //方式1
            $('#tijiao').submit(function(){
                alert(111)
            })
            //方式2
            $('#tijiao').on('submit',function(){
                alert(222)
            })
	})
</script>
```

当监听到表单的提交事件以后，可以调用事件对象的 `event.preventDefault()` 函数，来阻止表单的提交和页面的跳转

```js
$('#form1').submit(function(e) {
 // 阻止表单的提交和页面的跳转
   e.preventDefault()
 })
 $('#form1').on('submit', function(e) {
 // 阻止表单的提交和页面的跳转
   e.preventDefault()
 })
```

### 快速获取表单中的数据

为了简化表单中数据的获取操作，jQuery 提供了 serialize() 函数， serialize() 函数可以一次性获取到表单中的所有的数据。

```js
$(selector).serialize()
//示例
$(function(){
            $('#tijiao').submit(function(e){
                e.preventDefault()
                const data = $('#tijiao').serialize()
                console.log(data)         
            })
})
```

注意：在使用 serialize() 函数快速获取表单数据时，**必须为每个表单元素添加 name 属性！**

### 模板引擎

模板引擎，顾名思义，它可以根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面

![1722661215074](.\typora-user-images\1722661215074.png)

使用模板引擎主要有以下几个好处

- 减少了字符串的拼接操作
- 使代码结构更清晰
- 使代码更易于阅读与维护

#### art-template模板引擎

art-template 是一个简约、超快的模板引擎。中文官网首页为
`http://aui.github.io/art-template/zh-cn/index.html`

这里只是对art-template这个模板引擎简单了解一下

####  art-template标准语法

art-template 提供了 {{ }} 这种语法格式，在 {{ }} 内可以进行变量输出，或循环数组等操作，这种 {{ }} 语法在 art-template 中被称为标准语法。

```js
 {{value}}
 {{obj.key}}
 {{obj['key']}}
 {{a ? b : c}}
 {{a || b}}
 {{a + b}}
//如果要输出的value值中，包含了HTML 标签结构，则需要使用原文输出语法，才能保证HTML标签被正
//常渲染。
{{@ value }}
```

在 {{ }} 语法中，可以进行变量的输出、对象属性的输出、三元表达式输出、逻辑或输出、加减乘除等表达式输出。

## XMLHttpRequest的基本使用

 XMLHttpRequest（简称xhr）是浏览器提供的Javascript 对象，通过它，可以请求服务器上的数据资源。之
前所学的jQuery 中的Ajax 函数，就是基于xhr 对象封装出来的。

![1722662786275](.\typora-user-images\1722662786275.png)

### 使用xhr发起GET请求

```javascript
 <script>
        //创建xhr对象
        const xhr = new XMLHttpRequest()
        //使用xhr发送get请求
        xhr.open('GET', 'https://ajax-base-api-t.itheima.net/api/getbooks')
        //发起请求
        xhr.send()
        //监听onreadystatechange事件
        xhr.onreadystatechange = function () {
            //4.1监听xhr对象的请求状态readyState；与服务器响应的状态 status
            if (xhr.readyState === 4 && xhr.status === 200) {
                //4.2打印服务器响应回来的数据
                console.log(xhr.responseText)
            }
        }
 </script>
```

XMLHttpRequest 对象的 readyState 属性，用来表示当前 Ajax 请求所处的状态。每个 Ajax 请求必然处于以
下状态中的一个：

| 值   | 状态             | 描述                                                |
| ---- | ---------------- | --------------------------------------------------- |
| 0    | UNSENT           | XMLHttpRequest 对象已被创建，但尚未调用 open方法    |
| 1    | open。           | open() 方法已经被调用。                             |
| 2    | HEADERS_RECEIVED | send() 方法已经被调用，响应头也已经被接收           |
| 3    | LOADING          | 数据接收中，此时 response 属性中已经包含部分数据。  |
| 4    | DONE             | Ajax 请求完成，这意味着数据传输已经彻底完成或失败。 |

###  使用xhr发起带参数的GET请求

使用 xhr 对象发起带参数的 GET 请求时，只需在调用 xhr.open期间，为 URL 地址指定参数即可：

```js
<script>
	const xhr  = new XMLHttpRequest()
        xhr.open('GET', 'https://ajax-base-api-t.itheima.net/api/getbooks?id=1')
        xhr.send()
        xhr.onreadystatechange = function(){
            if(xhr.readyState ===4 && xhr.status ===200){
                console.log(xhr.responseText)
            }
      }
</script>
```

###  查询字符串

定义：查询字符串（URL 参数）是指在 URL 的末尾加上用于向服务器发送信息的字符串（变量）。
格式：将英文的 ?放在URL 的末尾，然后再加上 参数＝值 ，想加上多个参数的话，使用 &符号进行分隔。以
这个形式，可以将想要发送给服务器的数据添加到 URL 中。

```js
// 不带参数的 URL 地址
http://www.liulongbin.top:3006/api/getbooks
 // 带一个参数的 URL 地址
http://www.liulongbin.top:3006/api/getbooks?id=1
 // 带两个参数的 URL 地址
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记
```

无论使用 `$`.ajax()，还是使用 `$.get()`，又或者直接使用 xhr 对象发起 GET 请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到 URL 地址的后面，发送到服务器的。

```js
$.get('url', 
      {name: 'zs', age: 20}, 
      function() {}
     )
// 等价于
$.get('url?name=zs&age=20', 
      function() {}
     )
$.ajax({ 
    method: 'GET', url: 'url', 
    data: {name: 'zs', age: 20}, 
    success: function() {} 
})
// 等价于
$.ajax({ 
    method: 'GET', 
    url: 'url?name=zs&age=20', 
    success: function() {} 
})
```

### URL编码与解码

URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在 URL 地址中不允许出现中文字符。
如果 URL 中需要包含中文这样的字符，则必须对中文字符进行编码（转义）。
URL编码的原则：使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。
URL编码原则的通俗理解：使用英文字符去表示非英文字符。

```js
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记
// 经过 URL 编码之后，URL地址变成了如下格式：
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=%E8%A5%BF%E6%B8%B8%E8%AE%B0

```

浏览器提供了 URL 编码与解码的 API，分别是：

- encodeURI()  编码的函数
- decodeURI()  解码的函数

```javascript
<script>
    var str = '杜兰特'
    var str2 = encodeURI(str)
    console.log(str2)
    console.log('----------')
    var str3 = decodeURI('%E9%BB%91%E9%A9%AC')
    console.log(str3)
  </script>
```

由于浏览器会自动对 URL 地址进行编码操作，因此，大多数情况下，程序员不需要关心 URL 地址的编码
与解码操作。

### 使用xhr发起POST请求

```javascript
<script>
        // 1. 创建 xhr 对象
        var xhr = new XMLHttpRequest()
        // 2. 调用 open 函数
        xhr.open('POST', 'https://ajax-base-api-t.itheima.net/api/addbook')
        // 3. 设置 Content-Type 属性
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
        // 4. 调用 send 函数
        xhr.send('bookname=水浒传&author=施耐庵&publisher=上海图书出版社')
        // 5. 监听事件
        xhr.onreadystatechange = function () {
            if (xhr.readyState === 4 && xhr.status === 200) {
                console.log(xhr.responseText)
            }
        }
    </script>
```

## 数据交换格式

数据交换格式，就是服务器端与客户端之间进行数据传输与交换的格式。经常提及的两种数据交换格式分别是 XML和 JSON。其中 XML 用的非常少.

### XML和HTML

XML 和 HTML 虽然都是标记语言，但是，它们两者之间没有任何的关系。

- HTML 被设计用来描述网页上的内容，是网页内容的载体
- XML 被设计用来传输和存储数据，是数据的载体

![1722675836918](.\typora-user-images\1722675836918.png)

xml有以下两个问题:

-  XML 格式臃肿，和数据无关的代码多，体积大，传输效率低
- 在 Javascript 中解析 XML 比较麻烦

### JSON

JSON 就是 Javascript 对象和数组的字符串表示法，它使用文本表示一个 JS 对象或数组的信息，因此，
JSON 的本质是字符串。
作用：JSON 是一种轻量级的文本数据交换格式，在作用上类似于 XML，专门用于存储和传输数据，但
是 JSON 比 XML 更小、更快、更易解析。
现状：JSON 是在 2001 年开始被推广和使用的数据格式，到现今为止，JSON 已经成为了主流的数据交
换格式。

#### JSON的两种结构

JSON 就是用字符串来表示 Javascript 的对象和数组。所以，JSON 中包含对象和数组两种结构，通过这
两种结构的相互嵌套，可以表示各种复杂的数据结构

对象结构

对象结构在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

```json
{
 "name": "zs",
 "age": 20,
 "gender": '男',
 "address": undefined,
 "hobby": ["吃饭", "睡觉", '打豆豆']
 say: function() {}
 }
```

数组结构

数组结构在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

```json
 [ "java", "python", "php" ]
 [ 100, 200, 300.5 ]
 [ true, false, null ]
 [ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]
 [ [ "苹果", "榴莲", "椰子" ], [ 4, 50, 5 ] ]
```

json注意事项：

- 属性名必须使用双引号包裹
- 字符串类型的值必须使用双引号包裹
- JSON 中不允许使用单引号表示字符串
- JSON 中不能写注释
-  JSON 的最外层必须是对象或数组格式
- 不能使用 undefined 或函数作为 JSON 的值
- JSON 的作用：在计算机与网络之间存储和传输数据。
- JSON 的本质：用字符串来表示 Javascript 对象数据或数组数据

####  JSON和JS对象的互转

要实现从 JSON 字符串转换为 JS 对象，使用 JSON.parse() 方法：

```js
var obj = JSON.parse('{"a": "Hello", "b": "World"}')
//结果是 {a: 'Hello', b: 'World'}
```

要实现从 JS 对象转换为 JSON 字符串，使用 JSON.stringify() 方法：

```js
var json = JSON.stringify({a: 'Hello', b: 'World'})
//结果是 '{"a": "Hello", "b": "World"}'
```

##### 序列化和反序列化

把数据对象转换为字符串的过程，叫做序列化，例如：调用 JSON.stringify() 函数的操作，叫做 JSON 序列化。
把字符串转换为数据对象的过程，叫做反序列化，例如：调用 JSON.parse() 函数的操作，叫做 JSON 反序列化。

##  XMLHttpRequest Level2的新特性

旧版XMLHttpRequest的缺点
① 只支持文本数据的传输，无法用来读取和上传文件
② 传送和接收数据时，没有进度信息，只能提示有没有完成

###  设置HTTP请求时限

有时，Ajax 操作很耗时，而且无法预知要花多少时间。如果网速很慢，用户可能要等很久。新版本的 
XMLHttpRequest 对象，增加了 timeout 属性，可以设置 HTTP 请求的时限：

```js
xhr.timeout = 3000
```

最长等待时间设为 3000 毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个 
timeout 事件，用来指定回调函数：

```js
xhr.ontimeout = function(event){
alert('请求超时！')
}
```

简单示例：

```js
<script>
        const xhr = new XMLHttpRequest()
        xhr.timeout=3000
        xhr.ontimeout = function(){
            alert('请求超时了怎么办')
        }
        xhr.open('GET', 'https://ajax-base-api-t.itheima.net/api/getbooks')
    xhr.send()

    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText)
      }
    }
</script>
```

### FormData对象管理表单数据

Ajax 操作往往用来提交表单数据。为了方便表单处理，HTML5 新增了一个 FormData 对象，可以模拟表单操作：

```js
<script>
    // 1. 创建 FormData 实例
    var fd = new FormData()
    // 2. 调用 append 函数，向 fd 中追加数据
    fd.append('uname', 'zs')
    fd.append('upwd', '123456')

    var xhr = new XMLHttpRequest()
    xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
    xhr.send(fd)

    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(JSON.parse(xhr.responseText))
      }
    }
  </script>
```

FormData对象也可以用来获取网页表单的值，示例代码如下：

```html
<form id="form1">
    <input type="text" name="uname" autocomplete="off" />
    <input type="password" name="upwd" />
    <button type="submit">提交</button>
  </form>

  <script>
    // 1. 通过 DOM 操作，获取到 form 表单元素
    var form = document.querySelector('#form1')
    form.addEventListener('submit', function (e) {
      // 阻止表单的默认提交行为
      e.preventDefault()

      // 创建 FormData，快速获取到 form 表单中的数据
      var fd = new FormData(form)

      var xhr = new XMLHttpRequest()
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
      xhr.send(fd)

      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          console.log(JSON.parse(xhr.responseText))
        }
      }
    })
  </script>
```

### 上传文件

```html
    <!-- 1. 文件选择框 -->
  <input type="file" id="file1" />
  <!-- 2. 上传文件的按钮 -->
  <button id="btnUpload">上传文件</button>
  <br />
  <!-- 3. img 标签，来显示上传成功以后的图片 -->
  <img src="" alt="" id="img" width="800" />
    <script>
        // 1. 获取到文件上传按钮
    var btnUpload = document.querySelector('#btnUpload')
    btnUpload.addEventListener('click',function(){
        //获取到用户所选择的文件列表
        var files = document.querySelector('#file1').files
        if (files.length <=0){
            alert('请选择要上传到文件')
        }
        // 将用户选择的文件，添加到 FormData 中
        var fd = new FormData()
        fd.append('avatar', files[0])

        var xhr = new XMLHttpRequest()
      xhr.open('POST', 'https://ajax-base-api-t.itheima.net/api/upload/avatar')
      xhr.send(fd)
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          var data = JSON.parse(xhr.responseText)
          if (data.status === 200) {
            // 上传成功
            document.querySelector('#img').src = 'https://ajax-base-api-t.itheima.net' + data.url
          } else {
            // 上传失败
            console.log('图片上传失败！' + data.message)
          }
        }
      }

    })
    </script>
```

## axios

 Axios 是专注于网络数据请求的库。相比于原生的 XMLHttpRequest 对象，axios 简单易用。相比于 jQuery，axios 更加轻量化，只专注于网络数据请求

使用 axios 函数

- 传入配置对象
- 再用 .then 回调函数接收结果，并做后续处理

### axios发起GET请求

语法格式：

```js
axios.get(
    'url', 
    { 
        params: {/*参数*/ }
    }
).then(callback)
```

示例

```js
var paramsObj = { name: 'zs', age: 20 }
axios.get('https://ajax-base-api-t.itheima.net/api/get', { params: paramsObj }).then(function (res) {
     console.log(res.data)
})
```

### axios发起POST请求

语法格式：

```js
axios.post('url', {/*参数*/ }).then(callback)
```

示例

```js
axios.post('https://ajax-base-api-t.itheima.net/api/post',{ address: '北京', location: '顺义区' }).then(function(res){
                console.log(res.data)
})
```

### 直接使用axios发起请求

axios 也提供了类似于 jQuery 中 $.ajax() 的函数，语法如下：

```js
//直接用axios发起get请求 
axios({
        method: 'get',
        url:'https://ajax-base-api-t.itheima.net/api/get',
        data:{
             name: '钢铁侠', age: 35
        }
  }).then(function(res){
        console.log(res.data)
})
//直接拥axios发起post请求
axios({
       method: 'POST',
        url: 'https://ajax-base-api-t.itheima.net/api/post',
        data: { 
            address: '北京', 
            location: '顺义区'
        }}).then(function (res) {
        console.log(res.data)
})
```

## 跨域与JSONP

### 同源策略

如果两个页面的协议，域名和端口都相同，则两个页面具有相同的源

```js
相对于http://www.test.com/index.html 页面的同源检测：
http://www.test.com/other.html			是	同源（协议、域名、端口相同）
https://www.test.com/about.html			否	协议不同（http与 https）
http://blog.test.com/movie.html			否	域名不同（www.test.com 与 blog.test.com）
http://www.test.com:7001/home.html		否	端口不同（默认的 80端口与 7001端口）
http://www.test.com:80/main.html		是	同源（协议、域名、端口相同）
```

同源策略（英文全称 Same origin policy）是浏览器提供的一个安全功能。
MDN 官方给定的概念：同源策略限制了从**同一个源加载的文档或脚本如何与来自另一个源的资源进行交互**。这是一个用于**隔离潜在恶意文件的重要安全机制**。
通俗的理解：浏览器规定，A 网站的 JavaScript，不允许和非同源的网站 C 之间，进行资源的交互，例如：

- 无法读取非同源网页的 Cookie、LocalStorage和 IndexedDB
- 无法接触非同源网页的 DOM
- 无法向非同源地址发送 Ajax 请求

### 跨域

同源指的是两个 URL 的协议、域名、端口一致，反之，则是跨域。
出现跨域的根本原因：浏览器的同源策略不允许非同源的 URL 之间进行资源的交互。
网页：`http://www.test.com/index.html`
接口：`http://www.api.com/userlist`

![1722755468945](.\typora-user-images\1722755468945.png)

注意：浏览器允许发起跨域请求，但是，跨域请求回来的数据，会被浏览器拦截，无法被页面获取到！

###  如何实现跨域数据请求

实现跨域数据请求，最主要的两种解决方案，分别是 JSONP和 CORS。

- JSONP：出现的早，兼容性好（兼容低版本IE）。是前端程序员为了解决跨域问题，被迫想出来的一种临时解决方案。缺点是只支持 GET 请求，不支持 POST 请求。
- CORS：出现的较晚，它是 W3C 标准，属于跨域 Ajax 请求的根本解决方案。支持 GET 和 POST 请求。缺点是不兼容某些低版本的浏览器。

### JSONP

 jsonp是 json的一种"使用模式"，可用于解决主流浏览器的跨域数据访问的问题

由于浏览器同源策略的限制，网页中无法通过 Ajax 请求非同源的接口数据。但是,`<script> `标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。

因此，jsonp的实现原理，就是通过`<script> `标签的 src 属性，请求跨域的数据接口，并通过函数调用的形式，接收跨域接口响应回来的数据。

```js
<script>
    function success(data) {
      console.log('拿到了Data数据：')
      console.log(data)
    }
 </script>

 <script>
    success({ name: 'zs', age: 20 })
 </script>

// 方式二
 <script>
    function abc(data) {
      console.log('拿到了Data数据：')
      console.log(data)
    }
  </script>

  <script src="./js/getdata.js?callback=abc"></script>
```

由于 jsonp是通过`<script>` 标签的 src 属性，来实现跨域数据获取的，所以，jsonp只支持 GET 数据请求，不支持 POST 请求

注意：jsonp和 Ajax 之间没有任何关系，不能把 jsonp请求数据的方式叫做 Ajax，因为 jsonp没有用到 
XMLHttpRequest 这个对象。

####  jQuery中的JSONP

jQuery 提供的 $.ajax() 函数，除了可以发起真正的 Ajax 数据请求之外，还能够发起 JSONP 数据请求,默认情况下，使用 jQuery 发起 JSONP 请求，会自动携带一个 callback=jQueryxxx的参数，jQueryxxx是随机生成的一个回调函数名称。

```js
<script>
	$(function () {
            // 发起JSONP的请求
            $.ajax({
                url: 'https://ajax-base-api-t.itheima.net/api/jsonp?name=zs&age=20',
                // 代表我们要发起JSONP的数据请求
                dataType: 'jsonp',
                success: function (res) {
                    console.log(res)
                }
            })
        })
</script>
```

在使用 jQuery 发起 JSONP 请求时，如果想要自定义 JSONP 的参数以及回调函数名称，可以通过如下两个参数来指定：

```js
<script>
	$.ajax({
 		url:'https://ajax-base-api-t.itheima.net/api/jsonp?name=zs&age=20',
 		dataType:'jsonp',
 		//发送到服务端的参数名称，默认值为callback
 		jsonp:'callback',
 		//自定义的回调函数名称，默认值为jQueryxxx格式
   		jsonpCallback:'abc',
 		success:function(res){
 			console.log(res)
 		}
 	})
</script>
```

