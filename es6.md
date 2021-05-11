### 基本得 shell 命令

[shell](https://sunny-zz.github.io/mydoc/)

#### 常用命令

- `cd + 路径(必须是文件夹)` 跳转目录
  - ../ 返回上一级目录
  - ./ 当前目录
  - ~ 这个目录存放的是一些软件的配置信息
- `mkdir +文件夹名或者路经加文件夹名` 创建文件夹
- `ls`查看当前路径下的所有内容(不包括隐藏)
  - `a`参数 可以查看隐藏
- `touch +文件名或者路径加文件名` 创建的时候必须带上后缀名
- `rm+文件或文件夹的名称`
  - `r`只有加了改参数才能删除文件夹
  - `f`强制删除(有的时候可能也不好用)
- `cp +文件或文件夹名+新的名字` 拷贝
  - `r`,拷贝文件夹
- `mv + 文件或文件夹+路径/新的名字` 移动或重命名(移动到当前目录就是重命名)
- `pwd`查看当前所在位置,一般用来复制路径
- `cat` 文件名、查看当前文件内的内容

#### 使用技巧

- ctrl +c 终止命令,重新开始
- 直接回车是执行输入的命令
- clear 是清屏命令
- 键盘上的方向键上下是查看历史记录,左右是调整光标位置
- 命令行内的复制粘贴不可使用 ctrl +c 和 ctrl +v ,使用鼠标右键

## es6 知识

### let 和 const

- 创建变量的新语法,替换原来的 var
- const 适用于创建常量,不可修改

#### let const 与 var 的区

- 别自带块级作用域{}代表块
- 没有变量声明提升
- 不允许重复声明
- 定义的变量不属于顶层对象(window)的属性

#### 变量的解构赋值

- 数组的解构赋值

```js
let arr =[131, 182, 156]
let [num1, num2, num3] = arr
console.log(num1)
console.log(num2)
console.log(num3
```

- 对象的解构赋值

```js
let obj = {
  username: "小黑",
  userage: 20,
  sex: "女",
};
//可以换名可以设置默认值
let { userage: age(换名字), username, sex = "男"(设置默认值) } = obj;
console.log(username, age, sex);
```

- 字符串的解构赋值

```js
let str = "hello";
let { a, b, c, d, e } = str;
console.log(a);
console.log(e);
```

- 函数参数的解构赋值

```js
let obj = {
  username: "大白",
};
function say({ username }) {
  const str = "我叫" + username;
  console.log(str);
}
say(obj);
```

#### 字符串的扩展

- 模板字符串(高级字符串拼接)

```js
let htmlstr = `<div class='goods'<h4>${goods.goodsName}</h4><span>${goods.price}</span></div>`;
console.log(htmlstr);
```

- padEnd padStart 填充

```js
  let str = 'hello'
  let newstr = str.padEnd(8, 'a')
  console.log(str) (输出'hello')
  console.log (newstr)(输出'helloaaa')
```

#### 数组的扩展

- flat flatMap 数组的扁平化处理

```js
let arr = [1, 2, [3, 4, [5, 6, [7, 8]]]]
console.log(arr. flat())
console. log(arr.flat(2))
console.log (arr.flat(infinity)) (扁平化所有)
let arr1 = [1, 2]
let newArr1 = arr1.map(function (ele) {return [ele, ele*2]})
console. log (newArr1) 输出 [[1, 2], [2, 4]]
let newArr1 = arr1.flatMap(function(ele){return [ele, ele*2]})
console. log(newArr1)输出[1,2,2,4]
```

- fill 方法使用给定值，填充一个数组。根据指定的数据对数据进行初始化,修改原数组 。

```js
let arr2 = [1,2,3]
console.1og(arr2.fill(''))输出['','','']
//fill 方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
onsole. log(arr2.fill(7, 1, 2))输出 [1,7,3]
```

#### 对象的扩展

属性的简介表示法

```js
let name = 大白;
let age = 18;
let obj1 = {
  //创建对象的时候如果属性值所代表的变量名和属性名相同的话可省略
  // name :name
  name,
  age,
  // say: function(){
  say() {
    console.log(this.name);
  },
};
console.log(obj1);
```

#### 扩展运算符

- 数组的扩展 ...

```js
let arr = [1, 2, 3, 4, 5]
let arr1= arr (相当于复制了房间的钥匙)
arr1.push(6)
console.log(arr) 输出 [1, 2, 3, 4, 5，6]
console. 1og(arr1)  输出 [1, 2, 3, 4, 5，6]
console.log(arr1 === arr) 输出 true 指一个房间地址相同
let arrl= [...arr] 相当于创建新的地址
```

- 对象的扩展

```js
let obj = { a: 18, b: 26 };
let obj1 = { ...obj };
objl.a = 100;
console.log(obj);输出{a: 18, b: 26}
console.log(obj1);输出{a: 100, b: 26}
```

```js
let goodsArr =[
{
  name: '手机',
  price: 1000,
  id: 1
},
{
  name: '平板',
  price: 2000,
  id: 2
},
{
  name: '记本',
  price: 3000,
  id: 3
}
let newArr = [...goodsArr]
newArr[1].price= 2500
console.log (newArr[1]) 输出 {name: '记本',price: 2500,id: 3}
console.log(goodsArr[1]) 输出 {name: '记本',price: 2500,id: 3}
// 只能拷贝一层 拷贝了 goodsArr[]层
```

#### symbol 数据类型

Symbol 值不能与其他类型的值进行运算，会报错。
但是，Symbol 值可以显式转为字符串。Symbol 值也可以转为布尔值，但是不能转为数值

```js
let sym = Symbol("My symbol");
String(sym); // 'Symbol(My symbol)'
sym.toString(); // 'Symbol(My symbol)'
Boolean(sym); // true
!sym; // false
```

创建 Symbol 的时候，可以添加一个描述。

```js
const sym = Symbol("foo");
//上面代码中，sym 的描述就是字符串 foo。
```

- ES2019 提供了一个实例属性 description，直接返回 Symbol 的描述。

```js
const sym = Symbol("foo");
sym.description; // "foo"
```

- 作为属性名的 Symbol

```js
let mySymbol = Symbol();
// 第一种写法
let a = {};
a[mySymbol] = "Hello!";
// 第二种写法
let a = {
  [mySymbol]: "Hello!",
};
```

##### 自变量表示法与构造函数表示法

```js
// 自变量表示法
let arr = [1, 2, 3]
// 构造函数表示法
let arr1 = new Array(1, 2, 3)
console.log(arr == arr1)
console. log(arr1)
// 自变量表示法
let re =/^[0-9]{9}$/
// 构造函数表示法
let rel = new RegExp('^[0-9]{9}$')
console.log(re)
console.1og(re1)
```

#### set 数据结构

- Set 内部不允许出现重复的成员；
  set 属性
- Set.prototype.constructor：构造函数，默认就是 Set 函数。
- Set.prototype.size：返回 Set 实例的成员总数。
- set 数据结构的方法:
  - 1.add 该方法的作用是向内部添加新的成员。
  - 2.delete 删除某个值，返回一个布尔值，表示删除是否成功。
  - 3.has 返回一个布尔值，表示该值是否为 Set 的成员。
  - 4.clear 清除所有成员，没有返回值。
  - 5.Set.prototype.forEach()：使用回调函数遍历每个成员

```js
const s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(function (ele) {
  s.add(ele);
});
console.log(s) 输出[(2, 3, 5, 4)];

let now = new Set([1, 3, 5, 4, 555, 1]);
console.log(now.size);
输出数组去重后的长度;

let arr = [1, 3, 5, 4, 555, 23, 2, 1, 34, 34, 1, 5, 4];
console.log([...new Set(arr)]);
扩展符去重;

上面的方法也可以用于，去除字符串里面的重复字符。
[...new Set('ababbc')].join('')
// "abc"

Array.from方法可以将 Set 结构转为数组。

const items = new Set([1, 2, 3, 4, 5]);
const array = Array.from(items);
这就提供了去除数组重复成员的另一种方法。
function dedupe(array) {
  return Array.from(new Set(array));
}
dedupe([1, 1, 2, 3]) // [1, 2, 3]

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。
let set = new Set([1, 4, 9]);
set.forEach((value, key) => console.log(key + ' : ' + value))
// 1 : 1
// 4 : 4
// 9 : 9
```

#### Map

详见[es6 官方文档](https://es6.ruanyifeng.com/#docs/set-map)

#### class 类的基本语法

- 1.类的内部默认只能写方法
- 2.类的内部必须存在 constructor 函数 ，当 new 的时候 constructor 函数被触发，该方法默认返回实例对象（this）
- 3.除了 constructor 函数之外的函数都相当于共有方法。

```js
常规写法：
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.toString = function () {
  return `(${this.x},${this.y})`;
};
var p = new Point(1, 2);
console.log(p);
console.log(p.toString());

Class类方法:
let _color = "red"
class Point {
    z = 50;
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString(){
      return `(${this.x},${this.y})`
  }
  get 给 color 属性定义初始值
  get color(){
      return _color
  }
  set 给 color 属性设置值， 该函数会在修改 color 属性的时候触发
  set(){
     _color = new_value
  }
  静态方法
  static sayHello(){
      console.log("我是小吴")
  }
}
var p = new Point(1,2)
p.color = "green"
console.log(p)
console.log(p.toString())
Point.sayHello()
```

#### class 的继承

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  sayPoint() {
    console.log(`我是坐标(${this.x},${this.y})`);
  }
}
let p = new Point(100, 20);
console.log(p);
p.sayPoint();

class 继承 使用 extends
class ColorPoint extends Point{
    constructor(x,y,color){
        super(x,y)
        this.color = color;
    }
}
let  colorP = new ColorPoint(100,200,"red")
console.log(colorP)
colorP.sayPoint()
```

#### 函数的扩展

- 函数参数的默认值
  当函数传递实参的时候就是传递的那个值，不传的时候就是默认的那个值

```js
function add(x =10, y = 20) {
  return x + y;
}
let res = add(2);
console.log(res);输出(22)
let = ret = add(1,2) 输出(3)
```

- rest 参数

```js
传形参的时候，如果直接传(...rest) (输出数组[1,,2,3,4])，如果直接传(a,...rest)(输出数组[2,3,4])
function fun([a, ...rest]) {
  // rest 叫剩余参数
  console.log(rest);
fun([1, 2, 3, 4]);
```

#### 箭头函数

- 箭头函数 this 指向
  - 函数的新写法 箭头函数
  - 箭头函数没有 function 不能用 function 创建只能存储到变量中
  - 箭头函数分为箭头左侧和右侧
  1. 左侧是参数部分默认使用()包裹,当只有一个参数的时候可以省路()直接写参数
  2. 右侧是执行部分默认使用{}包裹, 当函数右侧只有返回值的时候可以省路{}直接写返回值也不需要 return.
  - 当函数只返回对象的时候可以直接({})
  - 箭头函数的普通函数的 this 指向问题。
  - 普通函数的 this 指向 谁调用就指向谁
  - 箭头函数的 this 创建的时候就定义好了(一般都指 window)。
  - 对象内定义方法的时候如果方法内部使用了 this 那么这个方法不能使用箭头函数定义

```js
class Point {
constructor(x, y){
this.x =x;
this.y =y;
  }
saypoint = () => {
  console.1og(`我是坐标(${this.x},${this.y})`)
  }
}
let p = new Point(10, 100)
P.sayPoint()
```

- 一般把箭头函数定义在类里面，在类里面 this 指向和普通函数一样

```js
let add = (x, y = 20) => x + y;
let res = add(10);
console.log(res);

let obj = {
  a: 10,
  fun: () => {
    console.log(this);
  },
};
obj.fun();
let fun1 = obj.fun;
fun1();
```

#### Module 的模块语法

- 模块是将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来
  想要在运行 Modlue 语法运行：

1. 在 node 里运行，不在浏览器运行
2. js 编译打包成浏览器认识的语法，(相当于转译 js 文件)然后在浏览器运行

#### 使用 webpack 编译打包 es6 模块语法

- npm 淘宝镜像

* 安装 node,[下载地址](https://nodejs.org/zh-cn/),一种下一步就好了，在命令行分别输入 node -v , npm -v 出现版本号即可
* 安装命令行工具 gitbash
* 新建一个文件夹(webpack-es6)
* 在文件夹内打开命令行工具执行`npm init -y` 命令。该命令的作用是将这个文件夹变成 node 项目,从而可以让这个项目使用 npm 下载对应的包。下载好了以后会生成一个 package.json 文件
* 项目内安装 webpack 执行 `npm install webpack webpack-cli --save-dev` 下载完会生成一个 node_modules 文件夹。
* 在项目的根目录下新建`index.html`,新建一个 src 文件夹里面放编译打包的 js 文件 `src/index.js`,`a.js`,在 a.js 内写一些 es6 模块代码(导出变量),index.js 内导入 a.js 模块内的导出。
* 在项目根目录下打开命令行工具执行`npx webpack`命令。该命令的默认作用是将项目下的 src 文件夹下的 index.js 打包编译到 dist 文件夹下的 main.js,然后 index.html 引入打包好之后的 js 文件,在浏览器中查看。
* 如果更改 index.js 以及 a.js 需要重新执行 npx webpack 编译### es6 模块的导入导出命名默认

#### es6 模块导入导出

- es6 模块的导出
- 模块导出了一个变量 firstName

1. 命名导出
   关键字 export
   可以导出多次
2. 默认导出
   关键字 export default
   只能使用一次

```js
let lastName = "三";
export let firstName = "张";
export { lastName };
export { lastName as laName }; //换名
let a = 10;
let b = 20;
let c = 30;
let d = 10000;
export { a, b, c };
export default d;
```

- es6 模块的导入
- \*表示导出的所有
  as 是换名字

  1. 命名导入
     关键字 import
     导入的名称和导出的名称必须一致
  2. 默认导入
     导入的时候随意命名

当导入模块的时候如果模块是 js 文件可省略后缀

```js
import { firstName, lastName, laName } from "./a";
console.log(firstName);

import * as all from "./a";
import x from "./a";
console.log(all.a);
console.log(all.b);
console.log(all.c);
console.log(all.default); // 取默认导出
console.log(x);
- 将整个 js 文件导入编译打包
 直接 在 index.js文件里 import'地址'，然后在命令行里输入命令 `npx webpack` 打包编译
```

#### ajax

异步的 javascript 请求,再不重新加载整个页面的情况下,向服务器发送请求获取数据进而更新部分网页的艺术。

##### ajax 的形式

- 原生的 ajax
- jquery ajax
- es6
- axios

后台服务器数据接口返回首页文章列表数据[数据库](http://jsonplaceholder.typicode.com/posts)

想要获取后台数据须知

1. 请求类型
2. 请求地址
3. 是否支持跨域
4. 返回值的模版
5. 需要后台提供对应的接口文档

#### 原生的 ajax

XHR
创建请求对象 [详细介绍](https://www.w3school.com.cn/ajax/ajax_xmlhttprequest_create.asp)

##### get 请求

```js
let xhr = new XMLHttpRequest();
// open方法创建相应请求,需要提供请求的类型,请求的地址,以及请求是否异步(必须异步) true就是异步(可以省略)
// 请求类型 GET POST DELETE PUT PAUCH ...
xhr.open("GET", "http://jsonplaceholder.typicode.com/posts");
//  send方法将创建好的请求发出
xhr.send();
// onreadystatechange事件该事件实时监听请求过程, 在请求的各个阶段反馈信息
xhr.onreadystatechange = function () {
  onreadystatechange事件该事件实时监听请求过程, 在请求的各个阶段反馈信息;
  if (xhr.readyState === 4 && xhr.status === 200) {
    // 请求成功相应就绪, 可以获取后台数据
    console.log(JSON.parse(xhr.responseText));
    //获取的数据类型是json字符串类型
    // json数据和我们js的对象很像-
    //我们需要将其转化成对象类型方便我们操作
    // JSON.parse(json串)将json串解析成对象
    // JSON.stringFy(对象)将对象转化成json串
  }
};
```

#### 制作简易的服务器 使用 json-server 模拟本地数据库

- 在命令行输入 `npm i json-server -g` 然后新建一个 json 文件
  json 格式的文件,和对象语法基本一样,但是内部的所有内容必须是双引号,除数字和布尔值之外,每一项的最后一项不可以加逗号
  json 文件还被当作 ajax.请求传递数据的格式
- json-server --watch data.json -p 3008 打开 json 文件

##### post 请求

```js
let xhr = new XMLHttpRequest();
xhr.open("POST", "http://localhost:3008/post");
// 使用原生的ajax发送post请求的时候,需要设置请求头(告知后台我传递的数据类型是json)
xhr.setRequestHeader("Content-type", "application/json");
// 将创建好的请求发出,传递的数据必须是 json数据
xhr.send(
  JSON.stringify({
    title: "小施阿姨",
  })
);
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status >= 200) {
    console.log(JSON.parse(xhr.responseText));
  }
};
```

#### jQuery ajax

### 类型 $.get() $.post()

**参数**,有先后顺序，没有就不写
url: 待载入页面的 URL 地址
data: 待发送 Key / value 参数。
callback: 载入成功时回调函数。
type: 返回内容格式，xml, html, script, json, text, \_default。
get 传递参数可以直接写在地址后面的?部分 也可以直接写在$.get 方法的参数内当成对象传递

```js
$.get("http://localhost:3008/post", function (data) {
  console.log(data);
});
$.post("http://localhost:3008/post", { title: "小李" }, function (data) {
  console.log(data);
});
```

##### $.ajax()

**参数**
url: 一个用来包含发送请求的 URL 字符串。
settings: AJAX 请求设置。所有选项都是可选的。

- $.ajax GET 类型请求

```js
$.ajax({
        请求的地址
      url: "http://localhost:3008/post",
        请求的类型
      type: "GET",
        请求的参数
      data: { id: 1 },
        成功的回调函数
      success: function (data) {
          console.log("请求成功了，看到了数据")
          console.log(data)
      },
        错误的回调函数
      error: function (err) {
          console.log("请求失败了", err)
      },
        请求完成的回调函数
      complete: function () {
          console.log("请求完成了")
      },
  })
```

- $.ajax GET 类型请求

```js
$.ajax({
  请求的地址
  url: "http://localhost:3008/post",
  请求的类型
  type: "POST",
  请求的参数
  data: { title:"小北爱吃肉" },
  成功的回调函数
  success: function (data) {
  console.log("请求成功了，看到了数据")
  console.log(data)
  },
  错误的回调函数
  error: function (err) {
  console.log("请求失败了", err)
  },
  请求完成的回调函数
  complete: function () {
  console.log("请求完成了")
  },
  })
```

#### 原生的 fetch 请求 [查找地址](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)

```js
**get 请求**
第一种写法
fetch('http://localhost:3008/post')
// 第一部分根据请求取响应
.then(function (response) {
response 请求成功的响应，响应里有一个 json 方法
return response.json();
})
// 第二部分根据响应取数据
.then(function (data) {
console.log(data);
});

第二种写法

fetch('http://localhost:3008/post', {
method: "GET"
})
.then(response => response.json()) // 代表请求结束了，
// 请求出错了
.catch(error => console.log("Error", error))
// 请求成功了
.then(data => console.log("Success", data))

**post 请求**
fetch('http://localhost:3008/post', {
method: "POST",
// 向后台传递 json 数据
body: JSON.stringify({ title: "傻呆呆" }),
// 设置请求头
headers: new Headers({
'content-type': 'application/json'
})
})
.then(response => response.json())
.catch(error => console.log("Error", error))
.then(data => console.log("Success", data))
```

#### axios 请求 专门发送请求的插件 是基于 promise 制作的

[查询地址](http://www.axios-js.com/zh-cn/docs/)

- get 请求

```js
axios
  // get请求传递参数可以直接写在地址的?部分,也可以写在第二个参数对象内,但是需要写在对象下的params属性下
  .get("http://localhost:3008/post?id=1")
  .get("http://localhost:3008/post", { params: { id: 1 } })
  .get("http://localhost:3008/post")
  //   成功的回调函数
  .then((res) => {
    // 返回的res 并不是真正想要的数据，而是经过axios封装之后的数据，
    // 里面的data属性才是后台反馈的数据，这个封装好的数据包含请求的一些信息
    console.log(res);
  })
  // 失败的回调函数
  .catch((error) => console.log(error));
```

- post 请求

```js
axios
  .post("http://localhost:3008/post", { tltle: "小李是个混子" })
  .then((res) => {
    console.log(res.data);
  })
  .catch((error) => console.log(error));
```

##### axios 并发多个请求 axios.a11

- 有两个请求我们想要在两个请求全部结束之后再去执行其他操作

```js
axios.get("http://localhost:3008/post?id=1").then((res) => {
  console.log(res.data);
});
axios.get("http://localhost:3008/post?id=2").then((res) => {
  console.log(res.data);
});

这时我们需要将多个请求添加到数组中，然后使用 axios.all 方法并发

axios.all([axios.get('http://localhost:3008/post?id=1'), axios.get('http://localhost:3008/post?id=2')])
.then(res => {
// 这个 res 是两个请求的返回结果组成的数组
console.log(res[0].data[0])
console.log(res[1].data[0])
})
```

#### 拦截器 先设置拦截器再发请求

- 请求拦截:
  可以理解为请求拦截，意义就是在发送请求或者响应请求之前做一些我们需要判断的事情

```js
添加请求拦截器;
axios.interceptors.request.use(
  function (config) {
    // 在发送请求之前做些什么
    // axios 请求的配置,可以根据配置,去对应的修改一些配置然后将新修改之后的配置 return
    return config; //配置;
  },
  function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  }
);
axios.get("http://localhost:3008/post?id=2").then((res) => {
  console.log(res);
});
```

```js
// 响应拦截器
// 添加响应拦截器
axios.interceptors.response.use(
  function (response) {
    // 对响应数据做点什么
    // response指的就是请求的结果(axios封装之后结果)
    // return 一个新的数据就会修改请求的结果
    return response.data; //如果我return response.data，那么在下面请请求的时候直接能拿到数据不用在用.data去取
  },
  function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  }
);
axios.get("http://localhost:3008/post?id=2").then((res) => {
  console.log(res);
});
```

#### promise 对象

```js
// promise 对象 异步解决方案
// new Promise 的时候传递的参数会自动执行
const promise = new Promise(function (resolve, reject) {
  let a = 10;
  setTimeout(() => {
    a++;
    if (a > 10) {
      console.log("异步操作执行成功");
      resolve("value"); //将数据传给.then的形参
    } else {
      console.log("异步操作执行失败");
      reject("error"); //将数据传给.catch的形参
    }
  }, 1000);
});
// then传递的函数其实传递给了promise中的resolve catch传递的函数传递给了reject
promise
  .then((res) => {
    console.log("异步操作执行完毕后，执行其它的操作");
    console.log(res);
  })
  .catch((err) => {
    console.log(err);
  });
```

##### 使用 promise 封装一个原生的 ajax get 请求

- .then .catch 两个方法是属于 promise 构造函数原型下的方法
- 封装好的 getPost 就是一个原生的 get 请求方法

```js
let getPost = (url) =>
  new Promise(function (resolve, reject) {
    let xhr = new XMLHttpRequest();
    xhr.open("GET", url), xhr.send();
    // onreadystatechange 是属于监听请求的整个过程，onload 是属于监听请求是否成功
    xhr.onload = () => {
      if (xhr.readyState === 4 && xhr.status === 200) {
        // 请求成功了
        console.log("异步操作执行成功");
        resolve(JSON.parse(xhr.responseText));
      } else {
        console.log("异步操作执行失败");
        reject("error");
      }
    };
  });
getPost("http://localhost:3008/p0ost?id=2")
  .then((res) => {
    console.log(res);
    // then 方法内的函数如果设置返回新的promise 实例的话，那么相当于给then 方法设置了返回值
    return getPost("http://localhost:3008/post?id=2");
  })
  .catch((err) => {
    console.log(err);
    // catch 方法也会返回一个新的promise 这个pomise 内什么都没有，会自动向下执行then
  })
  .then((res) => {
    console.log(res);
    return getPost("http://localhost:3008/post?id=2");
  })
  .then((res) => {
    console.log(res);
  });
```

##### Promise 实例 下的方法 常用 then catch finally all

```js
getPost("http://localhost:3008/post?id=2")
  .then((res) => {
    console.log(res);
  })
  .catch((err) => {
    console.log(err);
  })
  .finally(() => {
    console.log("请求完成之后执行的");
  });
const allP = Promise.all([
  getPost("http://localhost:3008/post?id=1"),
  getPost("http://localhost:3008/post?id=2"),
  getPost("http://localhost:3008/post?id=3"),
]);
allP.then((res) => {
  // 全部成功，获取到的是所有 resolve 函数的参数集合
  console.log(res);
});
```

#### async: Generator 函数的语法糖。异步解决方案

```js
const getPosts = async () => {
  const res = await axios.get("http://localhost:3008/post/1");
  console.log(res.data);
};
getPosts();
```

```js
const getPosts = async () => {
  await 后面一般跟着promise;
  // res 就会得到成功的返回值，并且 await 之后的操作都必须在 await 后面的异步执行完毕之后在执行
  const res = await axios.get("http://localhost:3008/post/1");
  return res.data;
};
// async 函数返回一个promise 对象
// async 函数内部 return 语句返回的值，会成为then方法回调函数的参数
getPosts()
  .then((res) => {
    console.log(res);
  })
  //  捕获失败
  .catch((err) => {
    console.log(err);
  });
```

#### node 的简单介绍

js 的运行环境 node 其实是主要为让 js 可以实现后台的功能。
作为前端使用 node ,一般使用 node 的 npm 工具,这个工具提供了所有前端相关的包可以下载(并且这些包都享有模块功能),
而且使用这个工具下载的话项目必须是 node 项目

##### node 项目

- 好处 : npm 下载包 帮你管理你的项目依赖(就是你下载的插件)

- **如何创建 node 项目** :直接给文件夹执行"npm init-y 命令即可,会自动生成一个 package.json 文件
- **如何下载包**
- npm install 包名@版本
- 执行下载命令的时候可以添加一些命令参数
  - -save 参数项目必须依赖包(dependencies)安装的参数
  - -S 项目必须依赖包(dependencies)安装的参数
  - --save-dev 参数 项目工具包(devDependencies)安装的参数
  - -D 项目工具包(devDependencies)安装的参数
  - -g 全局安装
- 作为 node 项目,可以使用 package.json 内的 script 字段设置该项目的命令行简化命令,使用 npm 替你去执行一些命令

```js
"scripts": {
    "build": "node index.js"
  },
  // 直接在命令行输入npm run build 即可执行 node index.js
```

- **如何卸载** npm uninstall 包名
  卸载的时候也可以添加上述参数执行
  `npm i 命令可以将之前记录在 package.json 中的所有包全部下载下来。
  所以说项目合作的时候只需要除 nodemodules 文件即可

##### node 的导入导出

作为 npm 下载的属于第三方模块,导入的时候基本上都是默认导入
import $ from jquery
node 模块的导入

- 将模块分为三大类

1.  node 核心模块,无需下载直接使用,导入的时候直接使用模块名称
    let http = require('http')
    console. log(http)
2.  第三方模块,使用 npm 工具下载的。导入的时候直接使用模块名称
    let $ = require('jquery')
    console. log($)
3.  - 自定义模块,就是新建的 js.文件,导入的时候需要使用相对路径
      js 模块导入的时候可以省略后缀
      let x = require('./about')
      console.log(x)
    - 自定义模块 node 模块的导出 三种导出方式
      let a= 100
      let b = 200
      1. module.exports = a
      2. module. exports = {a,b}
      3. module.exports.a =a 等同于 module. exports = {a}
