## 笔记

我的记笔记方式 markdown preview Enhanced

- 1
- 2
- 3

[百度](http://www.baidu.com)

```html
<div></div>
```

```css
.box {
  width: 100px;
}
```

#### 原生 js 介绍

```js
变量  存储数据的容器
将一个数据存储起来，然后须要使用的时候再去拿。
var 的作用是 声明
创建一个变量的时候必须使用 var 声明
 = 该符号的意思是赋值 会将符号右边的值给到左边。

 变量的命名规范：只能以字母、下滑线、$开头，只能以数字、字母、下滑线就、$构成。
不能使用关键字和保留字命名（关键字 js本身的语法使用的关键字 保留字 js 下一个版本可能被当做关键字的词。）
语义化命名
小驼峰（多个单词组合后面的首字母大写）
var num = 1
console.log(num)
```

#### js 数据类型

```js
数字(number) 字符串(string)  布尔值(boolean)  underfined  null  对象(object)   symbol(新增的)

var userName = "测试";
Uncaught ReferenceError: 测试 is not defined
因为你写的 测试 两个字没有加 '' 那么 js 就会认为他是一个变量，变量没有声明就会报错 not defined
var bool = true;
undefined 的意思是 变量声明未赋值就使用就会得到 undefined 不会创建变量，只是为了查错。
- 当访问对象不存在属性的时候返回的是 undefined
var x;
console.log(x)
null 和 对象(object)
数据类型的基础检测方法(typeof 数据)会得到该数据的数据类型(使用英文字符串表示的)
例子：
var num = "10"
console.log(typeof num) (会输出string)
```

#### 点击减号实现 input 内的数字减 1

```js
$('.sub').click(function(){
var number = $(".number").val();
number = number * 1 - 1;（*1-1 获得 input 内的字符串转换成数字 再运算。）
$('.number').val(number);
})

1.获取input内的数字;
2.将数字运算。
3.将结果重新给input；
jquery 的方法 .val() 获取 input 内的 value 值;
.val(值) 设置 input 内的 value 值;
```

## 数据类型之间的转换

- 字符串转换为数字

  1.可借助隐式转换，用的多的\*1；

##### 默认隐式转换

a. \* - / %(取余) 可以将符号左右的数据转化成数字，使用的方法是 Number()。

        例子：
        var str = "10"
        var num = str * 1
        var num1 = str % 13

b. + 只要是符号左右出现了字符串，那么就会将不是字符串的数据转化成字符串，然后实现拼接运算。

        例子：
        var num = 100;
        var str = "哈哈";
        console.log(typeof (num + str));(输出的数据类型是字符串)

c. 判断语句值中条件内的隐式转换，只要是写在了条件里的内容都会默认使用 Boolean() 转化为布尔值。

        var a = 100;
        if (a) {
                console.log("做梦");
        } else {
                console.log("非常对");
        }

2.使用 js 的三种方法。
(1).parseInt() 只能转化为整数。规则是一个字符一个字符的转换，直到不能转换为之。
(2).parseFloat() 可以转换为小数。规则是一个字符一个字符的转换，直到不能转换为之。

        例子:
        var str = "10.214"
        var num = parseInt(str)  (获取的值是数字10)
        var num =parseFloat(str) (获取的值是数字10.214)

(3).Number() 整体看能不能转化成数字，能就转，不能就是 NaN

        例子:
        var str = false (console.log(str) 输出的值是数字 1 )
        var num = parseInt(str); (输出的值是NaN )
        var num1 = Number(str) (输出的值是数字 1 )

- 数据转化为字符串 (偶尔会用到)

  1.String(value)
  2.value.toString()

          例子：
          var num = true
          num = String(mum)
          num = num.toString()

- 数据转化为布尔值。

  1.Boolean(value)
  只有数字 0、字符串空 null undefined NaN 转化为布尔值的时候是 false 其它都是 true

          例子：
          var num = -1
          num = Boolean(num)

##### js 执行顺序。

从上到下依次执行
事件外声明的变量事件内可以获取，事件内声明的变量事件外不能获取

```js
$(".btn").click(function () {
  console.log(a);
  var b = 1000;
});
var a = 100;
console.log(a);
console.log(b);
报错;
```

### 运算符

- a. + 、 - 、\* 、/ 、=。
- b.> 、 < 、 >= 、 <= 、 == 、 === 、 !=(不相等) 、!==(不相等)

        var str = "10";
        var num = 10;
        console.log(str === num);(输出的值是false)
        console.log(str !== num);(输出的值是true)

* == 和 === 都是判断是否相等，后者要求高必须满足值和类型都相同, 以后判断必须都使用 ===。
* != 和 !== 都是判断不相等，而后者也会判断数据类型。

- c. && 、 || 、 ! 。 !(一般用于布尔值取反)

```js
        例子：
        var num = 0;

        if (!num) {
        console.log("666");
        }
```

- d. ++、--、+=、-=、\*=、/=、%=。

        var num = 100;
        num++;  等价于  num= num + 1
        ++num; 等价于  num= num + 1
        num += 1; 等价于  num= num + 1

  - ++ 和 -- 在使用的时候，直接被当做值输出了,非常之少,
    ++放前面先运算，放后面先用值后计算。
    var num = 100;
    console.log(num++);(输出的值是 100)
    console.log(++num);(输出的值是 101)

e. 三目运算符 if+else 语句的简写

##### 三目运算符

-      if+else 写法

       var status(变量名"状态") = true;
       if (status) {
       console.log("将要执行关闭操作");
       console.log("关闭之后干点别的事");
       } else {
       console.log("将要执行打开操作");
       }

- 使用三目简化: 条件 ? 成立做的事 : 不成立做的事
  status(条件)
  ? (console.log("将要执行关闭操作"), console.log(222)) //写多个语句需要加小括号语句之间需要使用 逗号
  : console.log("将要执行打开操作");

         例子2:
         if+else 方法:
         var cj = 80;
         if (cj >= 60) {
         var result(变量名“结果”) = "及格";
         } else {
         var result = "不及格";
         }
         console.log(result);

         三目简化方法:
         var result = cj >=60 ? "及格" : "不及格"

- f. 位运算符 做进制运算 不做讲解(原生 js 参考文档 mdn)

      运算符的优先级(原生 js 参考文档   mdn)

### 语句

1.顺序。 2.分支。

- if 语句
  if 、if+else 、if + else if + else if ......+else(可有可无)

          例子1：
          var num = 66
          if(num>60){
                  console.log("及格")
          }
          else{
                  console.log("不及格")
          }

- 多种条件判断，只会生效一种，那么最好使用 if + else if。

        例子2：
        var num = 66
        if(num < 60){
                console.log("不及格")
        }
        else if(num > 60 && num < 70){
                console.log('及格')
        }
        else if(num > 70 && num < 80){
                console.log('良好')
        }
        else{
                console.log('优秀')
        }

        三目运算符：
        var num = 19
        num < 60
        ? console.log("不及格")
        : num >60 && num < 70
        ? console.log("及格")
        : num > 70 && num < 80
        ? console.log("良好")
        : console.log("优秀")

- if 语句简写

        var state = false
        if (state) console.log("关灯"),console.log("关灯以后睡觉");(条件和要做的事必须要写在一行)
        else console.log("开灯")

- switch 语句。(也是判断语句,if 语句是判断区间，switch 语句是判断等于)

        例子：
        var day = 1
        switch (day){
        case 1 :
        (当 day 等于 1 的时候)
        console.log("打麻将");
        console.log("吃火锅")
        break;
        case 2 :
        console.log("钓鱼");
        break;
        case 3 :
        console.log("逛街");
        default:
        console.log("睡觉");
        }
        注释：
        * 每有一种条件就设置一个 case ，而且判断成功的语句后面必须加上 break 关键字用于跳出 switch。
        * switch 语句的判断使用的 ===

3. 循环

for 语句

        for (var i = 1; i < 10; i++) {
        // 循环做的事
        console.log("循环语句执行了", i);
        }
        console.log(i);

        * for 循环语句的执行顺序

        1. 定义初始次数 i 并赋值初始值为 0
        2. 判断 i 的值是否满足条件
        3. 满足执行花括号内的操作,不满足的话直接结束循环语句
        4. 执行 i++
        5. 重复第二、三步

- 1+2+3+4+.....100 求和。

```js
var num = 0;
for (i = 1; i <= 100; i++) {
  num = num + i;
}
console.log(num);
```

- 1 到 100 奇数求和。

```js
方法1：
var num = 0;
for (i = 1; i <= 100; i+=2) {
  num = num + i;
}
console.log(num);

方法2：
var num = 0;
for (i = 1; i <= 100; i++) {
  if(i % 2){
    num = num + i;
  }
}
console.log(num);

方法3：
var num = 0;
for (i = 1; i <= 50; i++) {
  num = num + 2 * i - 1;
}
console.log(num);
```

- 简易计算器

```html
<div class="jisuanqi">
  <input class="show" type="text" />
  <div class="numbers">
    <button>0</button>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>4</button>
    <button>5</button>
    <button>6</button>
    <button>7</button>
    <button>8</button>
    <button>9</button>
  </div>
  <div class="signs">
    <button>+</button>
    <button>-</button>
    <button>*</button>
    <button>/</button>
  </div>
  <div class="btns">
    <button class="equal">=</button>
    <button class="clear">C</button>
  </div>
</div>
```

```js
<script>
      var num1 = "";
      var num2 = "";
      var sign = "";
      var res = "";
      $(".numbers>button").click(function () {
        var num = $(this).text();
        if (sign) {
          num2 = num2 + num;
          $(".show").val(num1 + sign + num2);
        } else {
          if (res !== "") {
            num1 = "";
            res = "";
          }
          num1 = num1 + num;
          $(".show").val(num1);
        }
      });
      $(".signs>button").click(function () {
        if (num2 !== "") {
          switch (sign) {
            case "+":
              res = num1 * 1 + num2 * 1;
              break;
            case "-":
              res = num1 * 1 - num2 * 1;
              break;
            case "*":
              res = num1 * 1 * num2 * 1;
              break;
            case "/":
              res = (num1 * 1) / (num2 * 1);
              break;
          }
          num1 = res;
          num2 = "";
        }
        sign = $(this).text();
        $(".show").val(num1 + sign);
      });
      $(".equal").click(function () {
        switch (sign) {
          case "+":
            res = num1 * 1 + num2 * 1;
            break;
          case "-":
            res = num1 * 1 - num2 * 1;
            break;
          case "*":
            res = num1 * 1 * num2 * 1;
            break;
          case "/":
            res = (num1 * 1) / (num2 * 1);
            break;
        }
        num1 = res;
        num2 = "";
        sign = "";
        $(".show").val(res);
      });
      $(".clear").click(function () {
        num1 = "";
        num2 = "";
        res = "";
        sign = "";
        $(".show").val("");
      });
    </script>
```

## 函数

函数 就是一个存储一系列语句的地方 ---> 存储某个功能的代码块
创建 函数创建的时候不执行，调用的时候才执行
a. 函数式创建

    function fun() {
      装功能的地方
      console.log("lgd 加油1");
      console.log("lgd 加油2");
      console.log("lgd 加油3");
    }

b. 变量式创建 将一个匿名函数赋值给一个变量
var addFun = function (a, b) {
var res = a + b;
console.log(res);
return res;
};

设置参数 a , b ,我们讲函数创建的时候写的参数称为 形参。
创建形参就相当于在函数内部声明了两个变量但是没有赋值，调用的时候传递了实参就相当于给变量赋值
函数内部创建的变量，只有在函数内部才能获取。

- 当外界(函数之外)想要获取函数内部计算的结果需要给函数添加 返回值将需要的值暴露
  return 必须写在函数最后面，因为 return 之后的语句就不会执行了
  return 的作用是暴露返回值和跳出函数

调用 ： 函数名()

- 实现求和函数，给你任意两个数字，通过函数运算得到结果
  需要外界提供参数，然后根据参数做功能

```html
<div class="wrap">
  <div>
    <input type="text" />
    <br />
    <input type="text" />
    <button class="add">add</button>
    <div>结果是：<span>00</span></div>
  </div>
  <hr />
  <hr />
  <div>
    <input type="text" />
    <br />
    <input type="text" />
    <button class="add">add</button>
    <div>结果是：<span>00</span></div>
  </div>
</div>
br 换行; hr 横线分割线
```

```js
var addFun = function (x, y) {
      var res = x + y;
      console.log(res);
      return res;
      };

  $(".add").click(function () {
    var num1 = $(this).parent().find("input").eq(0).val() * 1;
    var num2 = $(this).parent().find("input").eq(1).val() * 1;
    var res = addFun(num1, num2);
    函数调用的时候传递的参数称为实参
    当函数设置了返回值的时候 函数调用这句话先执行函数内部的操作，然后整句话变成返回的那个值
    jquery 修改或者获取标签内的文本内容使用 text
    $(this).next().find("span").text(res);
  });
```

- 1.js 内作用域

分为两种：1.全局作用域。 2.局部作用域。
目前只有函数存在局部作用域。
全局作用域的意思就是在该作用域下定义的内容，在任何地方都可以访问。
局部作用域的意思就是在该作用域下定义的内容只有本身作用域和后代作用域可以访问。

```js
var num = 100;
$(".btn").click(funciton(){
  var num = 0 (输出的值是0 ，num取值找最近的作用域取值)
  console.log(num);
  console.log("我是第一个按钮")

  var num1 = 200
});
console.log(num)   (输出的值是100（全局作用域）)
console.log(num1)  (输出的值是"num1 is not defined"(因为num1在click事件里))

```

- 变量的声明会直接提升到当前作用域的顶端(变量声明提升)

      console.log(str);(输出的值是 undefined，变量 str 会提升到 console 的上面但是变量声明未赋值所以输出 undefinded)
      var str = "hello";

- 函数式创建的函数会直接提升到当前作用域的顶端

      fun();(执行函数输出的值是 100，函数 fun 会提升到调用函数的前面)
      function fun() {
       var num = 100;
      console.log(num);
      }

变量式函数会变量声明提升

    xx();(输出的是 xx is not a function ----->  xx 不是一个函数)
    var xx = function () {
      console.log("我是 xx 函数");
    };

.只有在函数才有局部作用域

    var fenshu = 50;
    if (fenshu < 60) {
    var hero = "托儿索";
    } else {
    var hero = "亚索";
    }
    console.log(hero);(输出的值是“托儿索”)

- 全局是可以获取到 外部链接 内定义的 内容

### 对象(object)

object 语法 {属性名:属性值,名:值,...}
对象(object)： 属性的无序集合

    表示一个商品的信息 包括 名称 单价 库存 ...
    var goods = {
      goodsName: "iphone",
      price: 9999,
      inventory: 10000
    };
    console.log(goods);
    var price = goods.price;(对象.属性名  就是获取对应的属性值)
    console.log(price);
    goods.inventory = 9000;(直接对属性进行重新赋值就是修改)
    console.log(goods);
    goods.imgSrc =
      "https://img1.360buyimg.com/n6/jfs/t1/89881/7/6345/122550/5df1f1b5E7307a7af/92677a9cd911b760.jpg";(直接给新的属性赋值就是添加新属性)
    console.log(goods);

    * 使用 delete 关键字删除某个属性
    delete goods.imgSrc;
    console.log(goods);

创建一个 小猫 对象

    var cat = {
    name: "大花儿",
    age: 2,
    * 当属性的属性值是一个函数的时候 我们也称这个属性为 方法
    say: function (a, b) {
    console.log("我是大花儿，我会 喵喵喵");
    console.log("求和结果:", a + b);
    }
    };
    调用对象内的 say 方法
    cat.say(100, 200)

上述都是自定义对象

### js 内置对象 (js 内部内置了很多使用的对象，提供给开发者)

#### 内置对象分为：

1.数组 Array  
2.日期 date  
3.正则表达式 RegExp  
4.数学 Math  
5.字符串 String  
6.数字 Number  
7.布尔值 Boolean

##### 1.数组 array: 数据的有序集合。

    var users = ["赵四", "王五", "张三"];
    var nums = [1, 2, 3, 4, 5, 6, 7, 8];
    var goodsArr = [
    { goodsNmae: "iphone", goodsPrice: 9999 },
    { goodsNmae: "HuaWei", goodsPrice: 19999 }
    ];
    var arr = [
    [1, 2],
    [3, 4]
    ];
    var nums = [1, 2, 3, 4, 5, 6];
    数组的顺序从 0 开始 也叫元素的下标 索引
    获取第六个数字
    var sixNum = nums[5];
    console.log(sixNum);
    nums[7] = 100;
    console.log(nums[6]);

对于对象来说 一般都拥有属性和方法:

    var numArr = [5, 6, 7, 8, 9];
    console.log(numArr);

- 数组属性
  length 属性 获取数组的长度 也就是元素个数
  var len = numArr.length;
  console.log(len)
  numArr.length = 3; 如果直接给 length 属性赋值的话，就是想数组内增加 empty 或者 删除后面的元素 ，一般不会使用
  console.log(numArr);

###### 数组的方法

- 方法四要素 1.该方法是哪个谁(哪个对象)的 2.该方法干什么的(功能) 3.该方法的返回值 4.该方法修不修改原来的对象。

1. Array 下的方法:

- Array.isArray(值) 检测这个值是否是数组，如果是返回 ture ,如果不是返回 false;

      var str = "hello" ;
      var res = Array.iArray(res);
      console.log(res) (返回的值是false ,因为str不是数组)

- Array.form() 用的少，以后再说
- Array.of() 用来创建数组的 用的相对少。

2. 创建好的数组下的方法。

```js

1.对象.push(值，值，值....) 向数组后面添加一个或者多个元素，并返回数组的新长度，修改了原数组。
    var arr = [1,2,3,4,5,6]
    例子：var num = arr.push(7,8,9,10)
    console.log(arr)(输出数组arr[1,2,3,4,5,6,7,8,9,10])
    console.log(num)(输出的是数组的新长度 10)

2. 对象.pop()  删除数组内的最后一个元素，并返回被删除的元素，修改了原数组。
    var arr = [1,2,3,4,5,6]
    例子： var num = arr.pop()
    console.log(arr)(输出的数组arr[1,2,3,4,5])
    console.log(num)(输出的是被删元素 6)

3.对象.unshift(值，值，值。。。。) 向数组前面添加一个或者多个元素，并返回数组的新长度，修改了原数组。
     var arr = [1,2,3,4,5,6]
     例子：var num = arr.unshift(-1,0)
     console.log(arr)(输出数组arr[-1,0,1,2,3,4,5,6])
     console.log(num)(输出的是数组的新长度 8)

4. 对象.shift()删除数组内的第一个元素，并返回被删除的元素，修改了原数组。
    var arr = [1,2,3,4,5,6]
    例子：var num = arr.shift()
    console.log(arr)(输出数组arr[2,3,4,5,6])
    console.log(num)(输出被删除元素 1)

5.对象.splice(a,b,c)数组的删除或者添加。并返回被删元素组成的数组或者空数组，修改了原数组。
a.代表删除或者添加的起始位置 b.代表删除元素的个数 c.代表添加的元素，c 可以省略或者多个。
    var arr = [1,2,3,4,5,6]
    var num = arr.splice(0,2,11,22)
    console.log(arr)(输出数组arr[11,22,3,4,5,6])(在a位置删除b个元素并添加上c )
    console.log(num)(输出被删除的数组[1,2])

6.对象.reverse() 颠倒数组顺序，返回结果，修改了原数组。
   var arr = [1,2,3,4,5,6]
   var num = arr.reverse()
   console.log(arr)(输出数组arr[6,5,4,3,2,1])
   console.log(num)(输出数组[6,5,4,3,2,1])

7.对象.sort(函数或者不写) 将数组进行排序，不写的话按照首字符(从小到大)排序 ，修改了原数组。
 写的话要写成 function(a,b){return a-b} 从小到大排序； function(a,b){return a-b} 从大到小排序
 a 和 b 分别代表数组内相邻的元素
   var arr = [1,3,2,55,6,44]
   var num = arr.sort()
   console.log(arr)(输出数组arr[1,2,3,44,55,6])
   console.log(num)(输出数组arr[1,2,3,44,55,6])

   var arr = [1,3,2,55,6,44]
   var num = arr.sort(function(a,b){return a-b})
   console.log(arr)(输出数组arr[1,2,3,6,44,55])
   console.log(num)(输出数组arr[1,2,3,6,44,55])

8.对象.slice(begin,end) 数组的截取，返回截取后的数组，原数组不变。
begin和end都代表数组内元素的索引值，begin是截取的开始，end是截取的结尾，规则是包括开始不包括结尾。
如果括号内是负数代表倒数几个数的截取。
end可以省略 那么就截取到末尾。
    var arr = [1,2,3,4,5,6]
    var num = arr.slice(1,5)
    console.log(arr)(输出数组arr[1,2,3,4,5,6])
    console.log(num)(输出数组[2,3,4,5])
    var num1 = arr.slice(-2)
    console.log(num1)(输出数组[5,6])

9.对象.concat(一个或者多个数组) 数组的拼接，返回拼接后的数组，原数组不变。
    var arr = [1,2,3,4,5,6]
    var num = arr.concat([7,8,9])
    console.log(arr)(输出数组arr[1,2,3,4,5,6])
    console.log(num)(输出数组arr[1,2,3,4,5,6,7,8,9])

10.对象.indexOf(值) 检测该值在数组中是否存在，如果存在返回该值的索引值，如果不存在返回-1， 原数组不变。
   var arr = [1,2,3,4,5,6]
   var num = arr.indexOf(5)
   console.log(arr)(输出数组arr[1,2,3,4,5,6])
   console.log(num)(输出该值索引值4)

11.对象.includes(值) 检测该值在数组中是否存在，如果存在返回 true 如果不存在 返回 false  ,原数组不变。
    var arr = [1,2,3,4,5,6]
    var num = arr.includes(5)
    console.log(arr)(输出数组arr[1,2,3,4,5,6])
    console.log(num)(输出布尔值 true)

12.对象.join(值) 将数组使用该值拼接成字符串，返回新的字符串，不设置值使用 拼接  原数组不变。
    var arr = [1, 2, 3, 4, 5, 6];
    var str = arr2.join(8);
    console.log(arr)(输出数组arr[1,2,3,4,5,6])
    console.log(str);(输出字符串 18283848586)
    注释：如果括号里是空则输出1, 2, 3, 4, 5, 6 ，括号里是"" 则输出 123456 。
```

- 给 users 数组按照年龄排序

```js
    var users = [
        {
          username: "小张",
          age: 25,
          gl: 10,
        },
        {
          username: "小王",
          age: 26,
          gl: 16,
        },
        {
          username: "小赵",
          age: 24,
          gl: 4,
        },
      ];
      users.sort(function (a, b) {
        return a.age - b.age ;
      });
      console.log(users[2] === { username: "小赵", age: 28 });`
      上述结果是 false
      当对象类型的数据进行比较的时候，比较的是数据的地址并不是里面的值
      对象数据类型在浏览器中存储方式和普通的数据存储方式不一样，对象存储的是地址，而其他存储的是值
```

- 当对象类型的数据进行比较的时候，比较的是数据的地址并不是里面的值
- 对象数据类型在浏览器中存储方式和普通的数据存储方式不一样，对象存储的是地址，而其他存储的是值

forEach every find findindex filter map some reduce 原数组不变。

```js
1.对象.forEach(函数) 数组的遍历
以此查找数组内的元素，每次查找到执行 function 内的内容 function 可以设置三个参数(形参)
1.element查找到的元素  2.index 该元素的索引值  3.原数组
   var arr = [1,2,3,4,5,6]
   arr.forEach(function(element,index,Array){
     console.log(element)(依次输出1,2，3,4,5,6)
     console.log(arr)
   })
2.对象.every(函数) 检测数组内所有元素是否满足条件，条件写在函数的返回值内 返回 true 或者 false ;
   var arr = [1,2,3,4,5,6]
   var num = arr.every(function(ele){
     return ele % 2 === 1
   })
   console.log(num)(输出false)

3.对象.some(函数)检测数组内是否存在满足条件(至少一个即可)的元素，条件写在函数的返回值内 返回 true 或者 false ;
   var arr = [1,2,3,4,5,6]
   var num = arr.some(function(ele){
     return ele > 5
   })
   console.log(num)(输出 true)

4.对象.find(函数) 查找数组中第一个满足条件的元素。
   var arr = [1,2,3,4,5,6]
   var res = arr.find(function(ele){
    return ele > 3
   })
   console.log(res)(输出元素4)

5.对象.findIndex(函数) 查找数组中第一个满足条件的元素的索引。
   例子1：var arr = [1,2,3,4,5,6]
   var res = arr.findIndex(function(ele){
    return ele > 3
   })
   console.log(res)(输出元素4索引值3)

   例子2:
      var users = [
        {
          name: "小二",
          age: 24
        },
        {
          name: "小二1",
          age: 18
        },
        {
          name: "小二2",
          age: 30
        }
      ];
      var res = users.findIndex(function (ele) {
        return ele.age > 20;
      });
      console.log(res);(输出索引值 0)
      console.log(users[res])(输出结果与find的方法一样)

6.对象.filter() 数组的筛选，筛选出满足条件的元素组成的数组。
   例子1：var arr = [1,2,3,4,5,6]
   var res = arr.filter(function(ele){
    return ele > 3
   })
   console.log(res)(输出数组[4,5,6])

7.对象.map(函数) 映射(一一对应)根据给定条件生成新数组。map 函数的返回值就是对应的新数组内的元素。
   例子1：var arr = [1,2,3]
   var res = arr.map(function(ele){
    return ele * ele
   })
   console.log(res)(输出数组[1,4,9])

8.对象.reduce(函数) 方法接收两个参数。
写法 对象.reduce(function(参数(a,b,c,d)){},参数(函数初始值))
第一个参数是函数 该函数可接收四个参数  a 最终结果(累加器)  bcd 分别代表 ele  ind  array,该函数必须设置一个返回值，这个返回值是新的最终结果
第二个参数是最终结果的初始值    你想要获取什么内容，就设置对应的初始值
         reduce求和
   例子：var arr = [1,2,3,4]
   var num = arr.reduce(function(res,ele){
      return res + ele
   },0)
   console.log(num)(输出元素和 10)

         forEach求和
   例子：var arr = [1,2,3,4]
   var res = 0
   var num = arr.forEach(function(ele){
     res = res + ele
   })
    console.log(res)(输出元素和 10)

        for循环求和
  例子：var arr = [1,2,3,4]
   var res = 0
   for(var i = 0 ; i < arr.length ;i++ ){
    res = res + arr[i]
   }
    console.log(res)(输出元素和 10)

      filter筛选
  例子：var arr = [1,2,3,4]
  var num = arr.filter(function(ele){
    return ele % 2 === 1
  })
  console.log(num)

      reduce筛选
  例子：var arr = [1,2,3,4]
  var num = arr.reduce(function(res,ele){
    if(ele % 2 === 1){
      res.push(ele)
    }
    return res
  },[])
 console.log(num)
```

- 创建一个空标签

```js
var ul = $("<ul>");
.append() 向标签内的最后添加子标签
清空 li 内的内容
$("<li>").html("")
$("<li>").empty()
```

```css
border-collapse: collapse (合并单元格);
```

#### 冒泡排序

```js
var arr = [23, 5, 78, 3, 5, 90, 35, 69, 1, 8];
for (var m = 0; m < arr.length - 1; m++) {
  for (var i = 0; i < arr.length - 1 - m; i++) {
    if (arr[i] > arr[i + 1]) {
      var dashu = arr[i];
      arr[i] = arr[i + 1];
      arr[i + 1] = dashu;
      console.log(arr);
    }
  }
}
冒泡排序延伸;
for (var m = 0; m < arr.length - 1; m++) {
  for (var i = m; i < arr.length; i++) {
    if (arr[m] > arr[i]) {
      var dashu = arr[m];
      arr[m] = arr[i];
      arr[i] = dashu;
      console.log(arr);
    }
  }
}
```

#### 去重

```js
var arr = [1, 2, 3124, 12, 1, 1, 1, 1, 2, 451, 23, 313, 4, 5, 1, 11];
第一种方法;
for (var m = 0; m < arr.length - 1; m++) {
  for (var i = 1 + m; i < arr.length; i++) {
    if (arr[m] === arr[i]) {
      arr.splice(i, 1);
      i--;
      console.log(arr);
    }
  }
}
第二种方法;
for (var m = 0; m < arr.length - 1; m++) {
  for (var i = arr.length - 2 - m; i >= 0; i--) {
    if (arr[arr.length - 1 - m] === arr[i]) {
      arr.splice(i, 1);
    }
  }
}
console.log(arr);
第三种方法;
arr.sort(function (a, b) {
  return a - b;
});
for (var i = 0; i < arr.length - 1; i++) {
  if (arr[i] === arr[i + 1]) {
    arr.splice(i, 1);
    i--;
  }
}
第四种方法;
var res = [];
for (var i = 0; i < arr.length; i++) {
  // if (res.indexOf(arr[i]) === -1) {
  //   res.push(arr[i]);
  // }
  if (!res.includes(arr[i])) {
    res.push(arr[i]);
  }
}
console.log(res);
```

#### 数组的拷贝

```js
  slice  map  filter
  var arr = [1, 2, 3];
  var arr1 = arr.slice(0);
  var arr3 = arr.map(function (ele) {
    return ele;
  });
  var arr4 = arr.filter(function (ele) {
    return true;
  });
  console.log(arr1);
  console.log(arr === arr3);
  console.log(arr4);

var books = [
        {
          bookName: "红楼梦",
          date: "xx-xx-xx",
        },
        {
          bookName: "西游记",
          date: "aa-aa-aa",
        },
        {
          bookName: "水浒传",
          date: "bb-bb-bb",
        },
      ];
      var newBooks = books.slice(0);
      newBooks[0].date = "yy-yy-yy";
      console.log(newBooks === books);(不相等因为截取创建的数组和原数组地址不同)
      console.log(newBooks[0] === books[0]);(相等因为截取后数组内对象的地址未改变)
      console.log(books[0]);
```

### 时间

```js

  var date = new Date();
  console.log(date);(获得时间的对象)

时间的方法
  var year = date.getFullYear();(获取年份)
  console.log(year);
  var month = date.getMonth() + 1;
  console.log(month);(获取月份)
  var hou = date.getDate();
  console.log(hou);(获取日)
  var xingqi = date.getDay();
  console.log(xingqi);(获取星期)
  var hour = date.getHours();
  console.log(hour);(获取小时)
  var minute = date.getMinutes();
  console.log(minute);(获取分钟)
  var second = date.getSeconds();
  console.log(second);(获取秒)
  var milliSecond = date.getMilliseconds();
  console.log(milliSecond);(获取毫秒)
上述方法 在get 后加上 UTC 就是获取当前世界时间
get 换成 set 就是设置当前时间
  var time = date.getTime();
  console.log(time);(获得格林威治时间)
  1970 年 1.1 0 : 0 : 0 到现在的毫秒数
  可以作为一个唯一性的不重复的数字
  var strTime = Date();
  console.log(typeof strTime);(真正获得一个当前时间的字符串)
```

- 时间获取(电子表)

```html
<div>
  <span class="hour">0</span>
  <span> : </span>
  <span class="minute">0</span>
  <span> : </span>
  <span class="second">0</span>
  <br />
  <button class="stop">stop。。。</button>
  <br />
  <button class="begin">开始</button>
</div>
```

```js
//  setInterval 计时器 定时器
var showTime = function () {
  var date = new Date();
  var hour = date.getHours();
  if (hour < 10) {
    hour = "0" + hour;
  }
  $(".hour").text(hour);
  var minute = date.getMinutes();
  if (minute < 10) {
    minute = "0" + minute;
  }
  $(".minute").text(minute);
  var second = date.getSeconds();
  if (second < 10) {
    second = "0" + second;
  }
  $(".second").text(second);
};
showTime();
var res = setInterval(function () {
  showTime();
}, 500);
// 将 计时器调用的返回值 设置成变量 使用 clearInterval(返回值) 停止该变量
// 而且每一个定时器返回值基本上都不一样
$(".stop").click(function () {
  clearInterval(res);
});
$(".begin").click(function () {
  res = setInterval(function () {
    showTime();
  });
});
```

- setTimeout

```js
//setTimeout 延迟执行 clearTimeout 停止 setTimeout
// 用法和 setIntervar 一样
setTimeout(function () {
  console.log("aaa");
}, 1000);

function fun(a) {
  console.log(a);
}
var num = 10;
// 1.
// setTimeout(function () {
//   fun(10);
// });
// 2.
setTimeout(fun(num), 1000);
```

### 同步操作和异步操作

异步 jquery 动画 js 计时器 ajax
同步阻塞异步非阻塞
同步代码必须等上一个同步执行完毕之后才执行下一个
异步不会影响其他代码的执行
异步和同步都出现的时候，异步操作肯定会在同步之后执行完毕

```js
setTimeout(function () {
  console.log("我是异步操作1");
}, 10);
setTimeout(function () {
  console.log("我是异步操作");
}, 0);
for (var i = 0; i < 10000; i++) {
  console.log(i);
}
console.log("循环结束");
```

- 倒计时

```html
<h3>14:00点场 倒计时</h3>
<div>
  <span class="hour">0</span>
  <span> : </span>
  <span class="minute">0</span>
  <span> : </span>
  <span class="second">0</span>
</div>
```

```js
<script>
      // 数学运算   Math 使用数学对象下的一些方法
      // 上进  Math.ceil(值)
      // 下舍   Math.floor(值)
      // 四舍五入  Math.round(值)
      // 随机数  0-1  Math.random()
      // 绝对值 Math.abs(值)
      var targetHour = 21;
      var targetMinute = 15;
      var targetSecond = 20;
      var targetAllseconds =
        targetHour * 3600 + targetMinute * 60 + targetSecond;
      var showTime = function () {
        var date = new Date();
        var hour = date.getHours();
        var minute = date.getMinutes();
        var second = date.getSeconds();
        var newAllsecond = hour * 3600 + minute * 60 + second;
        var showAllsecond = targetAllseconds - newAllsecond;
        if (showAllsecond < 0) {
          $("h3").text("倒计时结束");
          clearInterval(run);
        } else {
          hour = Math.floor(showAllsecond / 3600);
          if (hour < 9) {
            hour = "0" + hour;
          }
          minute = Math.floor((showAllsecond % 3600) / 60);
          if (minute < 9) {
            minute = "0" + minute;
          }
          second = Math.floor(showAllsecond % 60);
          if (second < 9) {
            second = "0" + second;
          }
          $(".hour").text(hour);
          $(".minute").text(minute);
          $(".second").text(second);
        }
      };
      showTime();
      var run = setInterval(function () {
        showTime();
      }, 1000);
    </script>
```

#### 日期格式化 用 moment.js 插件

```js
  <script src="js/moment.js"></script>
    <script src="js/moment-with-locales.js"></script>
    <script>
        moment.locale("zh-cn");(更换语言)
        var Time = moment().format("MMMM Do YYYY, h:mm:ss a");(获取时间)
        console.log(Time);
        var Time1 = moment().format("MMM");(单独获取)
        console.log(Time1);

        已知时间格式化时间;
        moment.locale("zh-cn");
        var time = "2020-11-07T01:43:40.655Z";
        var time2 = moment(time).fromNow();
        console.log(time2);
        var time1 = moment(time).format("YYYY年MM月DD日");
        console.log(time1);
    </script>
```

### 正则表达式

```js
内置对象 正则表达式(RegExp)  字符串对象(string)
正则表达式其实就是一种规则 用来检测字符串或者是数字的规则。
包含一位大写字母 A
  var re = /A/;
  var str = "hello";
  re.test(str);
  方法:
 test()  返回 true false
 exec()  返回类数组(第一项是字符串内满足正则表达式的部分，可以使用[0]获取)，或者null。

创建带变量的正则
在 RegExp() 括号内写我们正则表达式，其实就是将原来创建方式 / / 里面的内容当作字符串写在 RegExp()  括号内
var newRe = new RegExp(searchValue);
console.log(newRe);

规则
^ 设置开头
$ 设置结尾
[]代表一位 例如[123]检测一位1或2或3.
[a-z] [A-Z] 一位字母 [A-z]一位字母或者下划线
[0-9] 一位数字
{数字}多少位  {10}数位  {1，}简写成 + 至少一位  {0,1}简写成？ 没有或者一位
{2，5} 2-5位 {0,}简写*有或没有都可以 注意{}只对前面的一位生效。
| 运算
() 分组 var re = /a(b|c)/
\d 一位数字 \D 一位非数字
  var re = /^\d+/;
  var str = "124ab123456789";
  console.log(re.exec(str));
\w 一位数字字母下划线 相当于[a-zA-Z0-9_] \W 一位非字母数字下划线
\s 一位空白符 (空格 tab)  \S 反义
/[^abcdefg]/  一位非小写字母 a、b、c、d、e、f、g   相当于括号内容取反
分组内的一个特殊写法   y(?=x)  后面紧跟着 x 的
var re2 = /a(?=[ab])/;
console.log(re2.exec("abaac"));
 . 代表任意字符
想要匹配正则内的一些带规则的字符就可以直接使用转义符转义
js 内  \  转义符
console.log("'\"");
var re4 = /\\/;
console.log(re4.exec("\\"));

字面量表示法
var re = /a/;()
构造函数创建,创建带变量的正则
var re1 = new RegExp("a");
console.log(re);
console.log(re1);
不能纯数字

/[^\d]/  检测出来非数字
/^\d+$/  检测出纯数字

判断重复
/^(\d)\1+$/  全部是相同的数字
()\1    前面括号内的相同的
var re = /^(ab)\1+$/;
var str = "ab";
console.log(re.test(str));

汉字的规则
var re = /[\u4e00-\u9fa5]/;
console.log("\u4e00");
console.log("\u9fa5");

 正则内的标志参数
 i 不区分大小写
 g 代表全局匹配

电话号正则规则
 133、149、153、173、177、180、181、189、190、191、193、199
中国联通号段
130、131、132、145、155、156、166、167、171、175、176、185、186、196
中国移动号段
134(0-8)、135、136、137、138、139、1440、147、148、150、151、152、157、158、159、172、178、182、183、184、187、188、195  、197、198

1     第一位
3(0-9)    4(45789)    5(012356789)   6(67)   7(1235678)    8(0-9)   9(01356789)

134(0-8)    144(0)    特殊

手机号规则
var phoneRe = /^1(3[012356789]|4[5789]|5[012356789]|6[67]|7[1235678]|8\d|9[01356789])\d{8}$/;
var phoneRe1 = /^(134[0-8]|1440)\d{7}$/;

var phoneRe = /^1(3[012356789]\d|4[5789]\d|5[012356789]\d|6[67]\d|7[1235678]\d|8\d{2}|9[01356789]\d|34[0-8]|440)\d{7}$/;
var str = "14408585721";
console.log(phoneRe.test(str) || phoneRe1.test(str));
console.log(phoneRe.test(str));
```

```css
background-attachment: fixed;
滚动页面图片不动
transform-origin: center bottom;定义旋转中心
```

```html
&nbsp;空格
```

### 字符串

##### 内置对象 String

```js
var str = "hello";  字符串
- 属性 length 获取字符串长度
console.log(str.length);
- 方法
1. charAt(index) 获得字符串内对应的字符，index 代表字符的索引值
 var str1 = str.charAt(2);
   console.log(str1);12
   +  +

 for (var i = 0; i < str.length; i++) {
   console.log(str.charAt(i));
 }
2. concat() 字符串和字符拼接，不常用还不如 +
3. endsWith(str) 判断当前字符串是否以某个字符串结尾，返回 true false
   console.log(str.endsWith("llo"));
4. startsWith(str) 判断当前字符串是否以某个字符串开始，返回 true false
   console.log(str.startsWith("he"));
5.includes(str) 判断当前字符串是否包含某个字符串，返回 true false
   console.log(str.includes("hell"));
var str2 = "helloll";
6.indexOf(str) 判断当前字符串是否包含某个字符串，返回开始位置 或者-1
    console.log(str2.indexOf("ll"));
输出索引值 2;
7.lastIndexOf(str) 用法和 indexOf 相同 indexOf 从前面开始数，lastIndexOf 从后面开始数
    console.log(str2.lastIndexOf("ll"));
    输出索引值 5;
    var str = " hello ";
    console.log(str);
    var newStr = str.trimStart();
    console.log(newStr);
8. trim 清空字符串左右的空白，返回清空之后的字符串，原来的不变。
9. trimStrat 清空字符串左的空白，返回清空之后的字符串，原来的不变。
10. trimRight 清空字符串右的空白，返回清空之后的字符串，原来的不变。
11. toUpperCase() 转换成大写(字母)，返回新的字符串，原来的不变。
12. toLowerCase() 转换成小写字母，返回新的字符串，原来的不变。
     console.log(str.toUpperCase());
     console.log(str.toLowerCase());

13.split 将字符串使用某个字符拆分成数组，返回数组，原字符串不变 (对应数组的join() 方法)
      var str3 = "2020-11-17";
      var str4 = str3.split("-");
      var str5 = str4.join("-");
      console.log(str4);
      console.log(str5);
14.slice(a,b) 字符串的截取包含a,不包含b
      console.log(str3.slice(2));
15.repeat(n) 重复n 次
      var i = "67";
      var m = i.repeat(4);
      console.log("新" + m, "旧" + i);
16.padEnd(添加到的长度，内容) 向字符串后面内填充内容，填充到指定长度。
      //   padStart(添加到的长度，内容) 向字符串前面内填充内容，填充到指定长度。
      console.log(i.padEnd(10, "ab"));
      console.log(i.padStart(10, "cd"));
17.search 检测字符串内是否存在某个字符串，返回位置。
      var phone = "我的1123146544";
      console.log(phone.search(/\d{2}/));
18.match 检测字符串内是否存在某个字符串，返回类数组，(就相当用了正则 exec 方法)
        match 的正则带了 g 的标志的话，会返回匹配到的所有字符串组成的数组
      var str6 = "我的电话号码是15813145678,我家里电话是 12345678765";
      console.log(str6.match(/\d{11}/g));
19.replace 将字符串内的某些字符替换成别的，
    replace(要被替换的内容(可以写内容也可以是正则)，被替换成什么)
      var str = "hello 2019,hello 2018";
      var newStr = str.replace(/\d{4}/g, "2020");
      console.log(newStr);
      console.log(str);
```

### 数学对象(math)

```js
数学对象   Math

var arr = [1, 2, 3];
var arr = new Array(1, 2, 3);
arr.push(4);
console.log(arr);

属性   很多数学里面常用的一些常数
PI
console.log(Math.PI);
方法
abs  绝对值
console.log(Math.abs(-10));
ceil 上进
console.log(Math.ceil(3.000001));
floor 下舍
console.log(Math.floor(3.99999));
round 四舍五入
console.log(Math.round(3.5));
random  0-1随机数 不包括0和1
console.log(Math.random());
max
var arr = [1, 2, 4123, 4, 124, 25, 1, 41, 4, 123]
var num1 = 100
var num2 = 100
var num3 = 100
console.log(Math.max(num1,num2,num3));
min

随机数  random   0-1
3-5 随机整数
Math.random()*3      上进     +2

console.log(Math.ceil(Math.random() * 3) + 2);

var num3 = 10.1111;
var num1 = num3.toFixed(1);
console.log(num1);
定义数字后面的小数括号里是几就是几位小数
```

#### 浏览器对象 window

- 为什么 script 可以解析 HTML 标签节点？
  因为浏览器向外提供了一些接口，让 js 等语言 可以处理 html
- window 浏览器全局对象, js 内你声明的全局变量以及全局函数都是属于这个全局对象的属性或方法
  我们原来可以直接写的一些方法就是 window 提供 只不过 window. 可以省略
  例如：setInterval、setTimeout

##### window 下的属性和方法

属性：console onresize (该属性是监听窗口变化的事件函数) 浏览器窗口大小(innerHeight innerWidth outerWidth outerHeight) scrollX scrollY screen location onhashchange history
当用户手动调整了窗口大小，前端需要根据窗口大小调整一些样式,使用 onresize 监听窗口是否改变。
window.onresize = function () {
console.log("窗口变化了");
};

- 原生的页面滚动条事件 onscroll

```js
window.onscroll = function () {
  console.log("滚动条事件触发");
  // 滚动条距离顶部的距离
  var x = window.scrollX;
  // 别称 pageXOffset
  var y = window.scrollY;
  // 别称 pageYOffset
  console.log(x, y);
};
```

- screen 是返回屏幕的一些信息
  screen 其实也是一个对象 里面包含一部分屏幕相关的属性

- location 是页面地址的信息 也是一个对象
  console.log(window.location);

```js
    file:///D:/digitalcity%E6%8E%88%E8%AF%BE/2020/2003/1122/index.html
  // 一个地址：   https://developer.mozilla.org:80/zh-CN/docs/Web/API/Window/screen?name=aaaa&x=1

地址栏地址的组成      url    协议、主机(域名)、端口、路径
www.xxx.com:8080
$("button").click(function () {
  location.href = "http://www.baidu.com";
});
属性
href   获取或者设置当前页面的地址
hash   获取或者设置当前页面地址的锚点
host   获取主机(域名)和端口号(如果后面带了)
hostname 获取主机(域名)
port   获取端口号
pathname 获取路径部分    /
search 获取或者设置查询部分   ?
$(".location").click(function () {
  // console.log(location.host);
  location.hash = "#test";
  // location.assign("./xxx.html");
});

方法
assign    跳转
replace   替换  无历史记录
reload    刷新
```

- window.onhashchange 锚点事件监听

```js
window.onhashchange = function () {
  console.log("锚点改变了");
};
```

- history 浏览器的历史记录 也是一个对象

```js
  属性   length
  方法   back()后退     go前进或后退     forward 前进
  $(".history").click(function () {
    console.log(history.length);
    history.go(0);
  });
```

navigator 获取的是当前浏览器的一些信息
当网页在不同的平台打开时可以使用 navigator 获取一些打开该页面的应用程序的信息

```js
$(".navigator").click(function () {
  console.log(navigator.appCodeName);
  console.log(navigator.appName);
});
```

方法：setInterval、setTimeout clear open close alert confirm propmt

1. open 方法打开一个新的窗口
   open("http://www.baidu.com");
   <a href="http://" target="_blank"></a> a 标签加 target="\_blank"也可以实现
   open 方法接受三个参数 1. 地址 2. 新打开的窗口名称 3.窗口的配置

   ```js
   $(".test").click(function () {
     // console.log("1");
     var newWindow = open(
       "./test.html",
       "测试的窗口名称",
       "width=300,height=300,resizable,left=100,top=100"
     );
   });
   ```

2. close 关闭当前窗口
3. 浏览器的三个窗口方法 alert 提示弹窗; confirm 确认弹窗; propmt 输入弹窗;

- confirm
  var res = confirm("是否关闭");
  console.log(res);
  当你点击确定的时候 confirm 方法返回 true 否则返回 false
- prompt
  var res = prompt("请输入密码", "admin");
  console.log(res);
  当你点击确定的时候 prompt 方法返回 输入的内容 否则返回 null
- requestAnimationFrame 让浏览器帮助你反复执行一件事，执行的时候每秒限定次数 每秒 60 次

```js
var num = 0;
// 递归 函数内部调用函数本身         就是类似循环
// requestAnimationFrame   让浏览器帮助你反复执行一件事，执行的时候每秒限定次数   每秒60次
function step() {
  num++;
  if (num < 100) {
    console.log("111");
    window.requestAnimationFrame(step);
    // 使用window下的requestAnimationFrame 方法 调用step函数
    // step()
  }
}
window.requestAnimationFrame(step);
```

### 浏览器对象下的 document 属性

原生 dom ：document 、 object 、 model 文档对象模型
浏览器提供给 js 的工具 可以让其他的语言修改或者获取文档的内容

dom 树 将文档分类 分成很多节点

1. 元素节点 标签
2. 属性节点 标签的属性
3. 文本节点 标签内的文本内容

获取元素节点

```js
// 1.  通过 id 名 获取 getElementById
var box = document.getElementById("box");
// 2.  通过 class 名 获取 getElementsByClassName 获取的是 标签集合(类数组)
// 3.  通过标签名获取 getElementsByTagName 获取的是 标签集合(类数组)
// 4.  通过标签的 name 属性获取 getElementsByName
// 5.  querySelector 通过选择器获取 获取匹配到的第一个 单一元素
// 6.  querySelectorAll 通过选择器获取 获取的是 标签集合(类数组)
var box = document.getElementById("box");
var box = document.getElementsByClassName("box")[1];
var box = document.querySelector(".box");
var box = document.querySelectorAll(".box")[0];
console.log(box);
```

## 事件绑定

原生 dom 元素.onclick = function(){点击做的事}
onclick onfocus onblur onchange oninuput onkeydown onkeypress onkeyup
onmouseenter onmouseleave onscroll onresize onhashchange onmousemove ondblclick onload onwhell

事件对象 event
document.querySelector(".btn").onclick = function () {
// console.log("点击事件触发");
};

#### 事件对象 event

- 事件对象 event 事件函数触发的时候默认会接收一个参数 这个参数就是事件对象
- 事件函数就是(对象.事件 = 函数 )后边的函数就是事件函数

```js
document.querySelector(".input").onkeydown = function (event) {
获取键盘码 根据键盘码判断到底的是什么键
需要通过事件对象 event
// event.preventDefault() 阻止默认行为
// event.pageX 距离文档左部的距离
// event.pageY 距离文档顶部的距离
// event.target 鼠标真正接触的元素 区分和 this 的区别this指的是调用事件本身的对象，而event.target指的是 本身和自己的子级
// event.type 事件类型
// event.keyCode 键盘码
// event.which 按键码 鼠标左键 1
// event.timeStamp 进入浏览器的时间
// event.stopPropagation 阻止事件冒泡
console.log("键盘按下 事件触发", event);
};
document.querySelector(".box").onmousemove = function (event) {
console.log(event.pageX);
};
```

- **onchange 事件和 oninput 事件的区别**

```js
document.querySelector(".input").onchange = function () {
onchange 就是域的内容发生改变的时候触发
// 在 input 上失去焦点的时候触发
console.log("change 事件触发");
};
document.querySelector(".input").oninput = function () {
// oninput 就是域的内容发生改变的时候触发
// 只在能输入 input
console.log("input 事件触发");
};

```

当我们在元素节点引入自己写的 js 时，如果直接引用因为代码从上到下执行顺序我们将不能获得元素节点那么我们就可以通过下面方法实现获取

```js
-当页面准备好的时候;

$(document).ready(function () {});

$(function () {})(上面的简写);

window.onload = function () {};
```

例如

```js
var a = 1000;
window.onload = function () {
  document.querySelector(".btn").onclick = function () {
    console.log(a);
  };
};
$(function () {
  console.log("我是小白");
});
$(document).ready(function () {
  document.querySelector(".input").onclick = function () {
    console.log(2222);
  };
});
```

创建一个函数简化获取 dom 节点
实现 document.querySelector('.btn') ===> getEle('.btn')

```js
var getEle = function (selector) {
  return document.querySelector(selector);
};
var getAllEle = function (selector) {
  return document.querySelectorAll(selector);
};
```

#### 修改行内样式和属性

- 使用 dom 元素.style 获取该元素的行内样式表对象 这个对象内的属性可以直接修改 也可以获取

```js
 var box = getEle(".box");
  getEle(".btn").onclick = function () {
    // console.log("11111");
   ** 修改行内样式**
    // 使用 dom元素.style  获取该元素的行内样式表对象 这个对象内的属性可以直接修改   也可以获取
    var styleObj = box.style;
    // console.log(styleObj);
    styleObj.width = "300px";
    styleObj.backgroundColor = "red";
    // styleObj["background-color"] = "red";
    // console.log(styleObj);
    **修改属性**
    // 原生dom元素.setAttribute(名,值)
    box.setAttribute("title", "我是box");
    // 添加title属性时，鼠标放到元素节点是 会出现title属性的属性值
    **获取属性**
    // 原生dom元素.getAttribute(名)
    console.log(box.getAttribute("class"));
    **删除属性**
    // 原生dom元素.removeAttribute(名)   跟设置成空类似
    box.removeAttribute("title");
```

**修改文本内容**

```js
原生 dom.innerText 原生 dom.innerHTML 属性
box.innerText = "哈哈哈哈哈";
box.innerHTML = "<span>哈哈哈哈哈</span>";
获取
console.log(box.innerText);
console.log(box.innerHTML);

// dom(父级).insertBefore(新的元素节点,存在的元素节点(父级的子级))
// 给父级添加一个孩子，在已有的孩子之前添加
 var li = document.createElement("li");
 li.innerText = "666";
document
 .querySelector("ul")
.insertBefore(li, document.querySelector("ul > li:nth-child(1)"));
```

**访问对象下的属性 可以使用 []**

```js
var obj = {
  "a-b": 10,
  x: 1000,
};
var x = "x";
// 访问对象下的属性 可以使用 []
console.log(obj[x]); // 1000
console.log(obj["a-b"]); // 10
console.log(obj["x"]); // 1000
console.log(obj.x); // 1000
```

### 如何创建一个元素节点

```js
var liEle = document.createElement("li");(创建元素节点)
var liTxtNode = document.createTextNode("666");(创建文本节点)
原生 dom.innerText 原生 dom.innerHTML 文本
document.createAttribute('src')
setAttribute 属性
liEle.innerText = "888";
liEle.setAttribute("title", "888");
console.log(liEle);
```

#### 添加子元素节点 添加成最后一个

```js
父元素.appendChild(子元素)
父元素.append(子元素) 子元素可以使字符串或者元素节点 ie 不支持
liEle.append("888");
document.querySelector(".comment-list").append(liEle);
```

#### 删除子元素节点

```js
父元素.removeChild(子元素) 删除子元素
元素.remove() 删除元素 ie 不支持
document
  .querySelector(".comment-list")
  .removeChild(document.querySelector(".comment-list li:nth-child(2)"));
document.querySelector(".comment-list li:nth-child(2)").remove();
```

#### 查找的用法

- .parentNode 属性 查找父级
- dom.tagName 元素的标签名 获取到大写的字符串
- dom.className 元素的 class 名 获取到的是 class 属性的属性值

#### 直接使用 innerHTML 属性 创建

```js
var liEle = document.createElement("li");
liEle.innerHTML = '<span>888</span><button class="del">删除</button>';
document.querySelector(".comment-list").append(liEle);
```

#### 元素.trigger 模拟事件触发

```js
$(".btn").click(function () {
  console.log("点击事件触发");
});

setInterval(function () {
  $(".btn").trigger("click");
  //  ( 模拟点击事件;)
}, 1000);
```

#### 事件绑定

```html
<button class="btn">绑定事件</button>
<!-- 直接定义事件函数 在 html 内绑定事件 -->
<button onclick="fun()" class="btn">html绑定事件</button>
<!-- onclick="delFun(event)"    ===>   del3.onclick = function(event){ this delFun(this)} -->
<script>
  // 一般写法 如果对同一个事件进行操作，下面的会覆盖上面的操作
  document.querySelector(".btn").onclick = function () {
    console.log("111");
  };
  // 添加事件监听 可以对一个事件多次操作，而且不糊被覆盖
  var fun = function () {
    console.log("aaa");
  };
  document.querySelector(".btn").addEventListener("click", fun);
  // 移除事件绑定
  document.querySelector(".btn").removeEventListener("click", fun);

  // 直接定义事件函数 在 html 内绑定事件
  // 给 html 元素添加一个 onclick 属性 属性值是全局函数的调用
  var fun = function () {
    console.log("测试 html 内事件绑定");
  };
</script>
```

```html
<!-- 通过给html添加onclick属性 添加事件绑定 -->
<button onclick="fun(this)" class="del">删除</button>
<script>
  // onclick="delfun(this)" 相当于del元素.onclick = function(event){ this
  delFun(this)}
  // 所有在delfun函数中不能直接使用this,需要给delFun函数传递this从而在onclick函数内拿到this
</script>
```

#### 事件运行机制

- 事件捕获：
  事件从最不精确的对象(document 对象)开始触发，然后到最精确
- 事件冒泡：
  事件会从最内层的元素开始发生，一直向上传播，直到 document 对象。

```html
<div class="box">
  <div class="box1"></div>
</div>
<script>
  document.querySelector(".box1").onclick = function () {
    console.log("我是小盒子");
    // 阻止事件冒泡
    // event.stopPropagation();
  };
  document.querySelector(".box").onclick = function () {
    console.log("我是大盒子");
  };
  // 当点击小盒子是大盒子的点击事件也会触发
</script>
```

- 阻止事件冒泡 event.stopPropagation();

#### 事件委托

- 将某个元素的事件委托给父级或祖先绑定

#### this.指向

- 在对象的方法内的 this 当方法执行(调用)的时候 this 指的就是这个对象
- 函数内的 this 指向的是调用该函数的对象
  };

```js
var obj = {
  name: "小黑",
};
obj.say = function () {
  console.log("我是" + this.name);
  // var b = this
  function x(y) {
    console.log(y.name);
  }
  //  x(b);
  x(this);
  // 函数内的 this 指向的是调用该函数的对象
};
obj.say();
```

#### if 判断里哪些值是 false

- "" 、null 、undefined、 NaN 、0

```css
/* 属性选择器 */
input[type] {
  width: 100px;
}
/* 伪类选择器 */
/* a:visited 过去的
      a:hover
      a:active
      a:focus */
```

#### 表单

```html
<form>
    <!--type 值为 text	定义单行的输入字段，用户可在其中输入文本。默认宽度为 20 个字符。 -->
    <input type="text" value="" />
    <!-- type 值为 password	定义密码字段。该字段中的字符被掩码。 -->
    <input type="password" name="pwd" />
    <!-- type 值为 radio	定义单选按钮。 -->
    <input type="radio" name="sex" id="" checked />
    <input type="radio" name="sex" id="" />
    <!-- type 值为 checkbox 定义复选框。 加checked属性默认为选中状态-->
    <input type="checkbox" name="vehicle" value="Bike" checked /> I have a bike
    <input id="agree" type="checkbox" name="vehicle" value="Car" /> I have a car
    <!--type 值为 submit	定义提交按钮。提交按钮会把表单数据发送到服务器。 -->
    <input type="submit" value="测试" />
  </form>
</form>
<script>
  //  .value   获取或者设置 value 值
  //  .checked 获取或设置选中状态
  // jquery 获取checked 状态 $('#argee').prop('checked')
  var username = document.querySelector("#username");
  document.querySelector("#agree").checked = false;
  // console.log(status, true);
</script>
```

### 拖拽事件

- 拖到何处 - ondragover 事件规定被拖动的数据能够被放置到何处。
- 进行放置 - ondrop 当放开被拖数据时，会发生 drop 事件。
- 拖放的内容 - ondragstart 和 setData() 然后，规定当元素被拖动时发生的事情。
- dataTransfer.setData() 方法设置被拖动数据的数据类型和值
  [拖拽事件](./照片/拖拽.png)

#### call apply\bind 修改 this 指向

#### bind

- bind 方法的作用是生成一个和某个函数一模一样的函数 并且可以修改函数内的 this 指向
- 无论什么时候调用该函数 this 指向基本上不会改变了
- 用法 xxx.bind(newThis) xxx 代表的是要拷贝的函数 newThis 代表的是替换成别的对象

```js
var a = 10;
function fun() {
  console.log(this.a);
}
var obj = {
  a: 100,
};
// fun();
//
var obj1 = {
  a: 200,
};
var newFun = fun.bind(obj);
console.log(newFun); //this指的是obj

obj1.fun = newFun;
obj1.fun(); //this指的是obj
```

##### call apply

- 替代某个函数执行，并且将函数内的 this 指向改了
- **call 和 apply 的区别**仅限于当需要给函数传递参数的时候有区别:
  - xxFun.call(newThis,参数 1,参数 2,...)
  - xxFun.apply(newThis,[参数 1,参数 2,...])

```js
var obj = {
  b: 100,
};
var b = 200;

var fun1 = function (x, y, z) {
  console.log(this);
  console.log(x + y + z);
  console.log(this.b);
};
fun1.call(obj, 1, 2, 3);
fun1.apply(obj, [1, 2, 3]);

fun1(3, 4, 5);
```

##

```html
<!-- <div onclick="handleClick.bind(this)()">测试</div> -->
<div onclick="handleClick.apply(this)">测试</div>
<script>
  function handleClick() {
    console.log(this);
  }
</script>
```

### apply 的技巧型应用

- 利用 apply 可以替代函数执行并且传参方式换成数组

```js
var arr = [1, 123, 124, 12, 3, 235, 23, 65, 52, 35, 246];
// Math.max 数学中找最大数的方法 max 函数操作的时候 没有用到 this
console.log(Math.max(1, 123, 124, 12, 3, 235, 23, 65, 52, 35, 246));
// 输出最大值;
// max 函数操作的时候 没有用到 this 所有 这里的this是什么都可以
var maxNum = Math.max.apply(null, arr); //apply 替max函数执行
console.log(maxNum);
```

#### 函数进阶

##### 函数内的 关键字 arguments

- 指的是 函数的实参集合 也就是将函数的实参组成一个类数组
- 类数组 只能 .length 或者 [n] -> 选择类数组的第几个数

```js
var fun = function () {
  console.log(arguments);
};
fun(1, 2, 3, 4);
// 输出类数组[1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

- 案例：根据 arguments 实现实参的求和

```js
var res = 0
function fun1() {
  for (let i = 0; i < arguments.length; i++) {
    res += arguments[i];
  }
  return fun1;
}
**函数的返回值**
var a = fun1(1, 2, 4, 5)(2, 2, 2);//因为函数fun1函数的返回值是一个函数 所以后面可以无限加括号
console.log(a); //输出的是fun1函数
console.log(res); //输出括号内实参的和
```

### 函数的分类

#### 匿名函数 不会自己创建 一般都是当作参数传递

- 函数拥有作用域
- 匿名函数立即执行 主要作用是封装作用域
- 因为全局变量越多就会污染全局环境

```js
// 将写好的js文件封装起来然后引入到html文件中
(function () {
  var loop = "一顿操作";
  window.loop = loop;
  // 给window添加一个属性 将作用域内的loop暴露出去(全局的)
})();
```

#### 回调函数

- 当一个函数被当做参数传递的时候 这个函数就是回调函数
  例如： 事件内的函数 动画回调 计时器回调

#### 递归函数

- 函数内部调用函数本身

```js
var num = 0;
function sub() {
  if (num < 100) {
    num++;
    console.log(num);
    sub();
  }
}
sub();
```

递归面试题 非波拉契数列

```js
var fib = function (n) {
  if (n <= 2) {
    return 1;
  }
  return fib(n - 1) + fib(n - 2);
};

console.log(res); //输出2
```

**递归函数实现查找 二叉树的查找**

- 给你一个 id 找到 id 的这个对象

```js
var arr = [
  {
    id: 1,
    label: "一级 1",
    children: [
      {
        id: 2,
        label: "二级 1-1",
        children: [
          {
            id: 3,
            label: "三级 1-1-1",
          },
        ],
      },
    ],
  },
  {
    id: 4,
    label: "一级 2",
    children: [
      {
        id: 5,
        label: "二级 2-1",
        children: [
          {
            id: 6,
            label: "三级 2-1-1",
          },
        ],
      },
      {
        id: 7,
        label: "二级 2-2",
        children: [
          {
            id: 8,
            label: "三级 2-2-1",
          },
        ],
      },
    ],
  },
  {
    id: 9,
    label: "一级 3",
    children: [
      {
        id: 10,
        label: "二级 3-1",
        children: [
          {
            id: 11,
            label: "三级 3-1-1",
          },
        ],
      },
      {
        id: 12,
        label: "二级 3-2",
        children: [
          {
            id: 13,
            label: "三级 3-2-1",
          },
        ],
      },
    ],
  },
];
```

```js
function findObjById(arr, id) {
  var currentObj = arr.find(function (item) {
    return item.id === id;
  });
  if (currentObj) {
    return currentObj;
  } else {
    for (let i = 0; i < arr.length; i++) {
      if (arr[i].children && arr[i].children.length) {
        // 当形成递归的时候 递归函数内声明的变量是不可以相互访问的 需要递归函数设置返回值
        currentObj = findObjById(arr[i].children, id);
        if (currentObj) {
          return currentObj;
        }
      }
    }
  }
}
var res = findObjById(arr, 2);
console.log(res);
```

#### 闭包函数

- 函数内嵌套函数就形成了闭包
- 作用域的嵌套 而且嵌套关系永远存在
- 闭包外层定义的变量会一直存储在内存中，等待闭包内层作用域访问
- 内存占用比较大

```js
function fun() {
  var num = 10;
  function fun1() {
    num++;
    console.log(num);
  }
  return fun1;
}

var newFun = fun(); // 因为fun函数返回的是fun1函数 所以直接fun()拿不到值
newFun(); //输出11
newFun(); //输出12，闭包外层定义的变量会一直存储在内存中，等待闭包内层作用域访问，
```

**闭包小应用**
解决异步问题

```js
// 一秒后输出 0,1,2,3,4
for (var i = 0; i < 5; i++) {
  (function (j) {
    setTimeout(function () {
      console.log(j);
    }, 1000);
  })(i);
}
// 一秒后输出5个5
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

页面中 ul > 5 个 li 点击 li 分别输出对应索引

```js
var liEle = document.querySelectorAll("ul li");
for (var i = 0; i < liEle.length; i++) {
  (function (j) {
    liEle[i].onclick = function () {
      console.log(j);
    };
  })(i);
}

// 或者;
for (var i = 0; i < liEle.length; i++) {
  liEle[i].onclick = (function (j) {
    return function () {
      console.log(j);
    };
  })(i);
}
```

**闭包小测试**

```js
function fun(n, o) {
  console.log(o);
  return {
    fun: function (m) {
      return fun(m, n);
    },
  };
}
var a = fun(0);
undefined;
a.fun(1); //0
a.fun(2); //0
a.fun(3); // 0
var b = fun(0).fun(1).fun(2).fun(3); // undefined 0 0 0
var c = fun(0).fun(1); // undefined 0
c.fun(2); // 1;
c.fun(3); //1;
```

#### 构造函数

- 构造函数 用于创建对象的函数
- 所有内置对象都有对应的构造函数
- 构造函数 依然是一个函数 函数名首字母必须大写

```js
// 构造函数创建对象
function CreateCat(name, age) {
  // 构造函数内部使用 this 向创建好的对象内添加属性或方法
  // this 指向的就是 new  CreateCat 的时候的实例化对象
  this.name = name;
  this.age = age;
}
// 构造函数拥有一个原型属性 prototype ,该属性是一个对象 这个对象内创建的内容是相当于给所有的实例化对象创建的公有属性(方法)
// 原型内的属性和方法会在实例化对象下的 __proto__ 属性内找到
// 构造函数的原型对象    CreateCat.prototype  该对象内的属性和方法就是公共的属性或方法
// 所以我们可以通过 对构造函数的原型对象进行修改 从而给实例化对象创建公共的属性或者方法
// 构造函数的原型对象内默认会有一个 constructor 方法，该方法指的就是构造函数本身
CreateCat.prototype.say = function () {
  // this 指向的就是 new  CreateCat 的时候的实例化对象
  console.log(this.name);
};
// 使用构造函数创建实例化对象
// 创建好的实例化对象下 默认存在一个 __proto__ 属性，该属性指的就是 创建该实例化对象的构造函数的原型对象
var catOne = new CreateCat("大白", 2);
var catTwo = new CreateCat("大白1", 1);
console.log(catOne);
// 调用实例化对象下构造函数原型下的say方法
catOne.say();
console.log(catTwo);
catTwo.say();
```

#### 构造函数的继承

```js
function SystemUser(username, userage) {
  User.call(this, username, userage);
  // 只是将 User 的构造函数内的属性或方法继承了
}
// 还需要继承 User.prototype 里面的内容

// 使用对象合并的方式比较好
Object.assign(SystemUser.prototype, User.prototype);

SystemUser.prototype.sayHi = function () {
  console.log("我是管理员");
};
var systemUser1 = new SystemUser("大 a", 30);
console.log(systemUser1);
```

#### 合并数组的方法

```js
var obj = { name: '哈哈哈', a: 'hello', age: 20 }
var obj1 = { age: 0 }

1. for in 语句 遍历对象
for (var key in obj) {
  // key 代表属性名
  // 当对象的属性名存在了一个变量内 想要访问属性值  obj[变量]
  // console.log(obj[key])
  obj1[key] = obj[key]
}
console.log(obj1)


2. Object.keys(对象)  获取对象内的 所有属性名的集合

console.log(Object.keys(obj))
var keys = Object.keys(obj)
for (let i = 0; i < keys.length; i++) {
  // console.log(keys[i])
  obj1[keys[i]] = obj[keys[i]]
}
console.log(obj1)

3. Object.assign(obj1,obj2,obj3......)
// 将第一个参数后面的所有对象合并到第一个参数内 重名的属性后面的覆盖前面的
Object.assign(obj1, obj)
console.log(obj1)

4. 使用高级 js 语法  ...  展开运算符
合并 obj1 和 obj 给到 newObj
var newObj = { ...obj1, ...obj }
console.log(newObj)
```
