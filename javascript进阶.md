## javascript进阶

### 作用域链

作用域链本质上是底层的变量查找机制。 

在函数被执行时，会优先查找当前函数作用域中查找变量 

如果当前作用域查找不到则会依次逐级查找父级作用域直到全局作用域

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

```js
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
```

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
6. 实例方法 `toUpperCase` 用于将字母转换成大写
7. 实例方法 `toLowerCase` 用于将就转换成小写
8. 实例方法 `indexOf`  检测是否包含某字符
9. 实例方法 `endsWith` 检测是否以某字符结尾
10. 实例方法 `replace` 用于替换字符串，支持正则匹配
11. 实例方法 `match` 用于查找字符串，支持正则匹配

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

