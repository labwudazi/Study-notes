## TypeScript

### 基础数据类型

布尔值 数字 字符串 数组 元组 枚举 any void null undefined Never object

- 使用：类型 规定数据类型

##### 布尔值

```js
let bool: boolean = true;
bool = false;
```

##### 数字

```js
let num: number = 1;
num = 2;
```

##### 字符串

```js
let username: string = "bob";
username = "smith";
```

##### 数组

**数字数组 数组里面必须放数字**

```js
let arr: number[] = [1, 2, 3, 4];
// 字符串数字
// let arr1:string [] = ["a","b","c"]
let arr1: Array<string> = ["a", "b", "c"]; //数组泛型
```

##### 元组

- 元组类型允许表示一个已知元素数量和类型数组

```js
let x: [string, number] = ["哈喽", 100];
x[0] = "haha";
```

// 越界的元组数据，默认会使用联合类型替代
// 比如 x 数把 x[3] 可以赋值成数字或字符串

##### 枚举 enum

- 枚举类型数据 Color
- 需要先创建一个枚举类型的数据
- npm install -g typescript 下载 typescript 插件
- 使用指令 tsc 文件名.ts 查看

```ts
enum Color {
  Red,
  Green,
  Blue,
}
let color: Color = Color.Green;
console.log(color);
console.log(Color);
```

tsc 文件名.ts 编译后

```js
var Color;
(function (Color) {
  Color[(Color["Red"] = 0)] = "Red";
  Color[(Color["Green"] = 1)] = "Green";
  Color[(Color["Blue"] = 2)] = "Blue";
})(Color || (Color = {}));
console.log(Color);
// 输出{0: "Red", 1: "Green", 2: "Blue", Red: 0, Green: 1, Blue: 2}
```

#### 类型推论

- 在有些没有明确指出类型的地方，类型推论会帮助提供类型。
- 当没有给变量声明类型,却赋值了,那么 ts 会自动根据值,给这个变量提供对应的类型,相当于进行了类型声明

```ts
-  let number = 1 //被推断成数字类型
-  number = "q" //错误的
// **最佳通用类型**
// -当需要从几个表达式中推断类型时候，会使用这些表达式的类型来推断出一个最合适的通用类型。例如
let xs = [0, 1, null];//被推论成数字数组
```

### 函数

为函数定义类型

- 1.参数类型
- 2.返回值类型
- 3.整个函数的类型
- 定义了参数和返回值类型

```ts
function add(x: number, y: number): number {
  return x + y;
}
const z: number = add(1, 2);
```

- 整个函数类型的声明 --> : (x: number, y: number) => number

```ts
let add: (x: number, y: number) => number = (xx: number, yy: number): number =>
  xx + yy;
let add1: (x: number, y: number) => number = function (
  x: number,
  y: number
): number {
  return x + y;
};
```

- 返回值无类型 也就是 void 类型

```ts
let showInfo = (info: string) => {
  console.log(info);
};
```

- **? 表示可选参数**，可有可无 但是一般在设置返回值的时候都会加判断

```ts
function buildName(firstName: string, lastName?: string) {
  return lastName ? firstName + "" + lastName : firstName;
}
const fullName = buildName("张");
console.log(fullName);
```

**函数默认值**

```ts
function buildName1(firstName: string, lastName = "李") {
  return lastName ? firstName + "" + lastName : firstName;
}
const fullName1 = buildName1("张");
console.log(fullName1);
```

**剩余参数**

```ts
function ass(...rest: number[]) {
  console.log(rest);
}
ass(1, 2, 3, 4, 5);
```

#### 接口

- 对象的详细类型定义

```ts
const obj: {username: string, password: string} ={
username: 'sunnyzz'
password: '1234561'
}
```

**用接口定义对象的规则**

- 接口名称一般首字母大写

```ts
interface Userobj {
  //必须有 age,属性值是数字
  age: number;
  // 可选属性 sex， 属性值是字符串
  // 只读属性 readonly 不可更改
  readonly sex?: string;
  // 任意的属性名 属性值是任意的值
  [propName: string]: any;
}
// myobj 对象也需满足我们设定的接口
let myobj: Userobj = { sex: "男", age: 10, hobby: ["篮球"] };
printAge(myobj);
//这个函数接收的参数是对象,而且对象里面必须有一个 age 属性属性值是数字
//函数的参数需要满足 Userobj
function printAge(userobj: Userobj) {
  console.log(userobj.age);
}
```

```ts
// todo 的data对象
interface Todo {
  readonly id: string;
  text: string;
  isDone?: boolean;
}
const todos: Todo[] = [
  {
    id: "111",
    text: "222",
  },
];
```

**额外的属性检查**

```ts
interface SquareConfig {
color?: string;
width?: number;
}
function createSquare(config: SquareConfig): { color: string; area: number } {
const width = config.width && 100
return {
color: config.color && "red",
area: width \* width
}
}
// 正常应该不会检查 colour 因为 ts 有额外的属性检查相似的属性名进行额外的检查
// 可以使用类型断言绕过额外的检查
let mySquare = createSquare({ colour: "red", width: 100 }); //错误
// 使用类型断言绕过额外的检查绕过了
let mySquare = createSquare({ colour: "red", width: 100 } as SquareConfig);
```

### 类

```ts
类;
class Cat {
  //  类的属性需要使用属性的从新写法对属性进行类型声明
  type = "猫科类";
  catAge: number;
  catName: string;
  // 构造函数原型对象里面默认有contructor属性 constructor指的是构造函数本身
  // new Cat() 实例化 自动执行constructor函数
  constructor(catNmame: string, catAge: number) {
    this.catAge = catAge;
    this.catName = catNmame;
  }
  say() {
    console.log("喵喵");
  }
}
const catOne = new Cat("小白", 2);
console.log(catOne);
```

**类的继承**

```ts
class Animal {
  name: string;
  age: number;
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
  move(distance: number) {
    console.log(`${this.name}移动了${distance}米`);
  }
}
// 创建一个子类 Cat
class Cat extends Animal {
  constructor(name: string, age: number) {
    super(name, age);
  }
}
const catOne = new Cat("小白", 1);
console.log(catOne);
console.log(catOne.move);
// 继承
// 继承的关键字 extends 实现的是
// 1.super 关键字 将继承的类的 constructor在子类的constructor内执行，并且将函数内部的this 替换成子类的this
// 2.将继承的类的原型对象给子类的原型的__proto__
// 当实例化类访问一个属性的时候
// 先找constructor
// 然后找 类的实例化对象
// 看有没有继承，有继承的话类的实例化对象的__proto__
// 找到最后一层__proto__指的就是Object 构造函数的原型，再往上__proto__ 就是null
// 实例对象的__proto__ 指的就是创建这个实例对象的构造函树(类)的原型对象
// 原型对象 __proto__  指的就继承的构造函数(类)的原型对象
```

- 用类的类型声明一个变量

```ts
// 创建一个类
class Point {
  x: number;
  y: number;
}
// 用类的类型声明一个变量
const pointA: Point = {
  x: 11,
  y: 20,
};
```

- 接口继承类

```ts
class Point {
  x: number;
  y: number;
}
// 接口继承类
interface Point3d extends Point {
  z: number;
}
let point3d: Point3d = { x: 1, y: 2, z: 3 };
```

- 接口继承接口 使用 extends 关键字

```ts
// 创建一个接口
interface Shape {
  color: string;
}
// 创建一个接口
interface Penstroke {
  penWidth: number;
}
// 接口继承接口，使用extends 关键字
interface Square extends Shape, Penstroke {
  sidelength: number;
}
const square: Square = {
  color: "red",
  penWidth: 30,
  sidelength: 30,
};
```

// 混合类型

### 泛型

```ts
// 不用泛型的话，这个函数可能是下面这样
function identity(arg: any): any {
  return arg;
}
// 使用any类型会导致这个函数可以接收任何类型的arg参数，这样就丢失了一些信息：传入的类型与返回的类型应该是相同的。
// 如果我们传入一个数字，我们只知道任何类型的值都有可能被返回。

// <T> 就是泛型  T 可以换成其它的名字
// 一旦泛型规定了某个类型，那么后续的所有泛型都是这个泛型
// 在变量名之后定义某个泛型 `变量名<T>` 定义了一个泛型 T
function identity<T>(arg: T): T {
  return arg;
}
// 要求 该函数参数和返回值是同一个类型 不能用 any
// 使用泛型解决
// 泛型的使用
const res = identity<string>("hello");
// 泛型会自动推论
const res = identity("hello");
```

### vue 中使用 ts

- 主要创建的类组件， 使用了装饰器语法，使用了官方土推荐的 `vue-property-decorator`,`vue-class-component`

### 装饰器语法的使用

#### @component

- 组件注册 components

```js
import TodoWrap from "./components/TodoWrap.vue";
@Component({
  components: {
    TodoWrap,
  },
```

- 生命周期(推荐写在类里面 使用``提供的 Hooks 语法)
- 计算属性(推荐写在类里面,参考下面的计算属性语法)
- data 值写在类里面 变量赋值 例如： count = 100;

#### @Prop

父组件传 子组件使用 vue-property-decorator 的 Prop 装饰器

```ts
// title! :string 的意思是非空断言 !:非空断言声明
@Prop(String) title!: string;
```

#### @Emit

```ts
//  重名的自定义事件接收
  // changeCount1 名字必须和父组件传递的自定义事件名称相同
  // 注意传递的名写法是烤串写法 xx-xx-xx
  // 接收的时候可以使用小驼峰
  @Emit()
  // 使用@Emit 接收父子间传递的自定义事件
  // 接收到的事件和我们定义的事件会自动合并
  changeCount1(value: number) {
    console.log(1111);
  }
```

#### @PropSync

```ts
 @PropSync("count", { type: Number }) SyncCount!: number;
//  相当于以前的
 // prop:{
  //     count:{
  //         type:Number
  //     }
  // },
  // computed:{
  //     syncedCount:{
  //         get(){
  //             return this.count
  //         },
  //         set(value){
  //             this.$emit("update:count",value)
  //         }
  //     }
  // }
```

#### @Model

```ts
// @Model('事件名'，{prop 的类型检验}) value !:string 用value 接收 prop
  // 事件名的作用是修改传递来的事件的名 默认是input 事件可以修改成 change 事件
  // prop 检验类型 可以写成字符串或者布尔值
  @Model("change", { type: String }) value!: string;
  //   因为 @Model 也接收了change 事件所以 可以直接在装饰器下面写函数合并装饰器接收的函数
  //   changeText(value: string) {}
  // 使用 @Emit 接收父组件利用 v-model传递的自定义事件
  // 因为使用 @Model 将事件名修改成了change 接收的时候可用change
  @Emit("change")
  changeText(value: string) {}
```

#### @ModelSync

```ts
@ModelSync("value", "change", { type: String }) readonly text!: string;
// xxx表示的是这个组件接收到的prop名
// aaa表示的是这个组件接收到的自定义事件名
// message表示的是这个组件的计算属性这个计算属性
// 有get和set
// get的返回值就是刚才接受的prop set执行的就是刚才接收的自定义事件
@ModelSync('xxx', 'aa', ftype: String} message!: string

```

#### @Watch

```ts
// @Watch 的使用
  // @Watch ("监听的数据",{监听的配置可以设置 immediate 和 deep})
  // @Watch紧跟着的函数就是数据的监听函数，数据发生改变就会触发
  // 一个数据可以有多个监听
  @Watch("question", { immediate: true })
  onQuestionChange1(newValue: string, oldValue: string) {
    console.log("初始化的时候就监听" + newValue);
    setTimeout(() => {
      const questionLen = newValue.length;
      this.answer =
        newValue.length === 0 ? "" : questionLen % 2 === 0 ? "是" : "否";
    }, 500);
  }
```
