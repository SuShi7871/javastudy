# Ajax

### 1.初识Ajax

URL地址一般由三部组成： 

​		① 客户端与服务器之间的通信协议

​		② 存有该资源的服务器名称 

​		③ 资源在服务器上具体的存放位置

```js
https://mbd.baidu.com/newspage/data/index.html
https:  通信协议
mbd.baidu.com  服务器名称
newspage/data/index.html   资源在服务器上具体的存放位置
```

 get 请求通常用于获取服务端资源（向服务器要资源） 

​		例如：根据 URL 地址，从服务器获取 HTML 文件、css 文件、js文件、图片文件、数据资源等 

post 请求通常用于向服务器提交数据（往服务器发送资源） 

​		例如：登录时向服务器提交的登录信息、注册时向服务器提交的注册信息、添加用户时向服务器提交的用户信息等各种数据提交操作

Ajax的理解:在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式，就是Ajax。

### 2.jQuery中的Ajax

浏览器中提供的 XMLHttpRequest 用法比较复杂，所以 jQuery 对 XMLHttpRequest 进行了封装，提供了一 系列 Ajax 相关的函数，极大地降低了 Ajax 的使用难度。 

jQuery 中发起 Ajax 请求最常用的三个方法如下： 

- $.get() 
- $.post()
- $.ajax()

#### $.get()函数

jQuery 中 $.get() 函数的功能单一，专门用来发起 get 请求，从而将服务器上的资源请求到客户端来进行使用。

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

#### $.post()函数

jQuery 中 $.post() 函数的功能单一，专门用来发起 post请求，从而将服务器上的资源请求到客户端来进行使用。

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

#### $.ajax()函数 

相比于 $.get() 和 $.post() 函数，jQuery 中提供的 $.ajax() 函数，是一个功能比较综合的函数，它允许我们对 Ajax 请求进行更详细的配置。 

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

### 3.axios使用

使用 axios 函数

- 传入配置对象
- 再用 .then 回调函数接收结果，并做后续处理

```js
//引入 axios.js：https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
axios() { 
    url: '目标资源地址' 
}.then((result)=>{
	// 对服务器返回的数据做后续处理
})
```

示例

```js
axios({
    url:"http://hmajax.itheima.net/api/province"
}).then(result=>{
    console.log(result)//获取到result对象
    console.log(result.data.list)//获取到result对象里面的数据
})
```

#### axios－查询参数 

语法：使用 axios 提供的 params 选项 

注意：axios 在运行时把参数名和值，会拼接到 url?参数名=值

```js
axios({ 
    url:'目标资源地址', 
    params:{参数名:值}}).then(result=>{ 
    // 对服务器返回的数据做后续处理 
})
```

示例

```js
axios({
    url:"http://hmajax.itheima.net/api/city",
    params:{
     pname:'甘肃省'
    }
	}).then(result=>{
    console.log(result.data.list)//['兰州市', '嘉峪关市', '金昌市', '白银市', '天水市', '武威市', '张掖市', '平凉市', 								// '酒泉市', '庆阳市', '定西市', '陇南市', '临夏回族自治州', '甘南藏族自治州']
})
```

#### 常用请求方法 

请求方法：对服务器资源，要执行的操作 

请求方法		   操作 

- GET 		    获取数据 
- POST          数据提交 
- PUT             修改数据（全部） 
- DELETE       删除数据 
- PATCH        修改数据（部分）

##### 数据提交

axios 请求配置

- url：请求的 URL 网址 
- method：请求的方法，
- GET可以省略（不区分大小写） 
- data：提交数据

```js
axios({
    url: '目标资源地址',
    method: '请求方法',
	data: {
		参数名: 值
	}
}).then((result) => { // 对服务器返回的数据做后续处理 })
```

示例：

```js
<button class="btn">注册用户</button>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
	document.querySelector('.btn').addEventListener('click', () => {
  	axios({
    	url: 'http://hmajax.itheima.net/api/register',
    	method: 'POST',
    	data: {
      		username: 'itheima007',
      		password: '7654321'
    	}
  	})
})
</script>
```

#### axios 错误处理

语法：在 then 方法的后面，通过点语法调用 catch 方法，传入回调函数并定义形参

```js
axios({ 
    // 请求选项 
}).then(result => {
    // 处理数据 
}).catch(error => { 
    // 处理错误 
})
```

示例

```js
axios({
    url: 'http://hmajax.itheima.net/api/register',
    method: 'post',
    data: {
     	username: '张佳亮123123',
     	password: '2234343'
    }
   }).then(result => {
    	console.log(result.data)
   }).catch(errror => {
    	console.log(error)
    	console.log(error.response.data.message)
    	alert(error.response.data.message)
   })
  })
```

#### form-serialize 插件

作用：快速收集表单元素的值

```js
/**
          * 2. 使用serialize函数，快速收集表单元素的值
          * 参数1：要获取哪个表单的数据
          *  表单元素设置name属性，值会作为对象的属性名
          *  建议name属性的值，最好和接口文档参数名一致
          * 参数2：配置对象
          *  hash 设置获取数据结构
          *    - true：JS对象（推荐）一般请求体里提交给服务器
          *    - false: 查询字符串
          *  empty 设置是否获取空值
          *    - true: 获取空值（推荐）数据结构和标签结构一致
          *    - false：不获取空值
*/   
const form = document.querySelector('.example-form')
const data = serialize(form, { hash: true, empty: true })
```

