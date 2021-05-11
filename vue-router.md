#### vue-router

### 单页面应用
好处：
不好之处：
#### 安装
1.vue-router 安装方式->vue ui ->在依赖里面安装搜vue-router 安装
1.npm run serve 安装方式 输入 npm i vue-router 安装

#### 创建路由
```js
先导入 vue 然后导入 vue-router
import Vue from "vue"
import VueRouter from "vue-router"
1.需要将路由功能制作成vue中的全局功能 需要 vue的 use 方法
Vue.use(VueRouter)
2.创建路由
1）创建路由数组
路由的地址不要写大写
const routes = [
    {
    / 代表“http://localhost:8080/”(根目录)
        path:'/'，
        component:Home
    }，
     {
        /pins 代表“http://localhost:8080/pins”
        path: '/pins',
        component: Pins
    },
    {
        /books 代表“http://localhost:8080/books”
        path: '/books',
        component: Books
    }

]
1）根据路由数组创建整体的路由
const router =new VueRouter({
    routes :routes(路由数组)
    路由模式 history 完全仿照浏览器history  以后项目上线的话必须给服务器添加配置支持history模式  hash锚点模式
    mode:"history"
})
3).导出使用 在 main.js导入添加到整个vue项目中
export default router 
```

#### 路由的使用 
虽然我们使用了 Vue.use 方法将VueRouter 制作成了，全局功能，但是想要使用我们创建好的路由还需要将创建好的
路由加载到整个 vue 项目中

```js
在main.js中引用
import router from './router'
new Vue({
  router: router,
  router,
  添加router 属性 主要是跟路由相关组件匹配 还有将$route 和 $router 挂载到Vue实例当做公共属性,也就是是说所有
  vue 组件组件中都会有这两个属性
  render: h => h(App),
}).$mount('#app')
```
 #### 在组件中展示使用路由功能,需要使用路由提供的各种组件
##### router-view 
1. router-view  用来展示页面组件的 页面地址和某个路由对象的path匹配的话就会展示对应的页面组件
匹配规则是在routes中 从上到下 严格匹配(不包含查询部分和锚点部分)，只能匹配一个

##### router-link props 属性
router-link 用来实现路由的跳转 也就是页面跳转
- router-link有默认的激活规则,但是这个规则并不能满足所有的需求,可以直接控制class去满足需求

1. 必须传递 to porp 值是跳转的地址，当地址和 to 匹配的时候默认就会添加一些激活的类名
匹配的规则是包含匹配 比如当地址是 /pins de 时候 匹配 /pins 和/
to 属性的属性值也可以是一个对象{path，name,params, query}
path 就是路径 name 就是命名路由的名字 query 就是查询部分，params 动态路由参数

2. replace
类型: boolea 
默认值: false
设置 replace 属性的话，当点击时，会调用 router.replace() 而不是 router.push()，于是导航后不会留下 history 记录。

3. append
类型: boolean 
默认值: false
设置 append 属性后，则在当前 (相对) 路径前添加基路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

4. tag
类型: strin
默认值: "a"
有时候想要 <router-link> 渲染成某种标签，例如 <li>。

5. active-class
类型: string
默认值: "router-link-active"
设置链接激活时使用的 CSS 类名。默认值可以通过路由的构造选项 linkActiveClass 来全局配置。

6. exact-active-class
类型: string
默认值: "router-link-exact-active"
配置当链接被精确匹配的时候应该激活的 class。注意默认值也是可以通过路由构造函数选项 linkExactActiveClass 进行全局配置的。

7. exact
exact
类型: boolean
默认值: false
想要链接使用“精确匹配模式”，则使用 exact 属性：

##### 传递参数
我是路由组件，路由跳转的时候传递了参数或者查询条件，需要根据这些条件，去展示不同的内容
- 传递方式有两种：
1.query是地址栏的查询部分也就是？部分
```html
<router-link :to="{name:'pins',query:{type:'推荐'}}">沸点</router-link>
```
2.params 动态路由参数 只有路由的path 设置了动态参数的时候才可以传递
```js
{
    //  动态路由 就是多个地址 都展示一个页面 ，就需要设置动态路由参数
    // :type 就是地址栏内变量
        /pins/任何 都会匹配
        path: '/pins/:type',
        component: Pins,
        name: "pins"
    }
```
```html
  <router-link :to="{path:'/pins/hot'}">沸点</router-link>
  <router-link :to="{name:'pins',params:{type:'hot'}}">沸点</router-link>
```
#### 在路由组件内如何获取当前路由的相关信息
只要是路由组件那么该组件就会得到一个当前路由信息 存储在this.$route 内
query方法获取
created() {
    this.type = this.$route.query.type;
}
动态组件方法获取
created() {
  this.type = this.$route.params.type;
  }
#### $router 
$router 是路由添加给所有组件的属性可以直接访问， 这个属性指的是整个路由实例，
路由实例下有很多方法
1.push('地址')实现路由的跳转
2.back()实现历史记录返回
3.go(数字)实现历史记录的前进后退 go(-1) 就是back()
4.replace('地址') 和 push()一样但是没有历史记录
5.forward
#### 嵌套路由
当父路由匹配的时候, 默认某一个子路由也需要匹配
当子路由地址是空的时候父路由匹配默认展示
当给了父路由设置了name的时候, 如果有默认子路由,请把name给默认子路由设置
嵌套路由的path 前面不要加 / 或者说前面不要加父路由path m默认会自动添加 
```js
{
path: '/',
component: Home,
嵌套路由
children: [
    {
        path: '',
        component: List,
        name: "home"
    },
    {
        path: ':category',
        component: List,
    }
]
    }
```
#### 自定向和别名
网站改版了网址由pins改变成了pin 但是想输入pins也可以访问该网页就可用到重定向实现和别名实现
- 从定向 
```js
{
    path: '/pin/:type',
    component: Pins,
    name: "pins"
},
  {
    path: "/pins/:type",
    redirect: "/pin/:type",      
},{
    path: "/pins/:type",
    redirect: { name: "pins"   
},{
    path: "/pins/:type",
    redirect: to => {
        if (to.path === "/pins/xxxxxx") {
             return "/"
        }
            return '/pin/:type'
    }
},
```
- 别名 给路由组件添加alias属性 /a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样。
```js
const routes = [
    {
    path: '/pin/:type',
    component: Pins,
    alias: '/pins/:type',
    name: "pins"  
    }
]
```
#### 404页面
```html
<template>
  <div>
    <div v-if="!isNot" class="home">
      <div class="home-head">
        <router-link to="/recommended">推荐</router-link>
        <router-link to="/frontend">前端</router-link>
        <router-link to="/backend">后端</router-link>
      </div>
      <router-view />
    </div>
    <Not v-else />
  </div>
</template>
```
```js
<script>
import Not from "./Not";
export default {
  name: "Home",
  components: { Not },
  data() {
    return {
      isNot: false
    };
  },
  生命周期钩子写法
  created() {
    console.log(1111);
    const { category } = this.$route.params;
    console.log(category);
    !(["recommended", "frontend", "backend"].includes(category) || !category) &&
      (this.isNot = true);
  }

  侦听器写法
  watch: {
    "$route.params.category": {
      handler(newValue) {
        this.isNot = false;
        console.log(newValue);
        !(
          ["recommended", "frontend", "backend"].includes(newValue) || !newValue
        ) && (this.isNot = true);
      },
      immediate: true
    }
  }
};
</script>
```
#### Notfount 页面
1. 
```js
 {
    path: "*", 所有地址都匹配（与上边不匹配的这里都会匹配到）
    必须写在route 路由数组的最后一项
    component: Not
    }
```
2. 
```js
  {
        path: "/error",
        component: Not
    },
    {
        path: '*',
        将所以后匹配到的地址都重定向到 '/error'
        redirect: "/error"
    }
```
#### 路由组件传参
如果 props 是一个对象，它会被按原样设置为组件属性。当 props 是静态的时候有用。
当这个路由被匹配的时候是没有动态路由参数的其实组件内获取的是props是undefined ,我们想让组件获取recommended
直接将props写成对象类型即可 
对象传参
props: {category: 'recommended'}
布尔值传参
当路由对象给了props属性并且 props属性的属性值是true的话,那么route.params将会被设置为组件属性,也就是说params对象下的属性会当做prop传递给组件
所以我们可以使用props替代sroute在组件内获取动态路由参数

        props: true

函数传参
```js
const routes =[
    {
      path: '/category',
      component: List,
      props: route => ({ category: route.params.category })
    }
]
```

### 路由进阶
#### 路由懒加载
```js
 const routes = [{
    path: '/about',
    name: 'About',
    //路由懒加载,匹配到时候导入,当路由不匹配到 about 页面的时候 about组件就不会导入
    component: () => import('../views/About.vue')
  }]
```
- 注意
如果您使用的是 Babel，你将需要添加 syntax-dynamic-import 插件，才能使 Babel 可以正确地解析语法。
#### 导航守卫
* 弄一个所有组件都能知道的登录状态
1. app的data组件使用$parent获取
2. app的data使用provide向下提供
3. vuex
4. 浏览器的本地存储(常用)
 localStorage 和 sessionStorage 属性允许在浏览器中存储 key/value 对的数据。
sessionStorage 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。
提示: 如果你想在浏览器窗口关闭后还保留数据，可以使用 localStorage 属性， 该数据对象没有过期时间，
今天、下周、明年都能用，除非你手动去删除。
- 注意：只能存字符串、布尔值，数字
 ```js
//  保存数据语法：
 sessionStorage.setItem("key", "value");
//  读取数据语法：
var lastname = sessionStorage.getItem("key");
// 删除指定键的数据语法：
sessionStorage.removeItem("key");
// 删除所有数据：
sessionStorage.clear();
 ```

#### 路由原信息
可以设置权限问题 可以用$route.matched 拿
匹配的路由$route下有一个matched属性
该属性是一个数组,记录了当前地址匹配到的路由记录
路由记录可以直接使用$route访问到当前路由
在路由记录内可以访问到对应的路由的路由元信息就是meta字段
通过路由元信息,添加权限属性,实现权限处理问题
实现的就是当前地址会匹配到很多路由(包括嵌套的子路由),只要某一个路由通过路由元信息设置了权限, 那么就需要遍历$route.matched去查询
最好去路由的全局前置守卫去判断
