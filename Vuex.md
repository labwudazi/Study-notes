## Vuex

[地址](https://vuex.vuejs.org/zh/)
下载 Vuex 依赖

- 新建一个 store 文件夹 里面新建一个 inde.js 文件
- 创建一个 store

```js
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);
const store = new Vuex.Store({
  //  state 相当于data的返回值
  state: {
    count: 10,
  },
  // store 中的数据要修改的话需要定义 mutation 函数
  // mutation 函数就是用来修改store数据的
  // 而且 mutation 函数只能接收两个参数
  // 每一个mutation 函数默认第一个参数接收的是store内的state，
  // 想要修改哪个数据直接修改即可
  // mutatian 函数的第二个以及后面的参数 称为载荷数据(payload) 用来修改或者
  //   添加vuex里store里的数据,组件中传什么就改成什么
  mutations: {
    add(state) {
      state.count++;
    },
    sub(state) {
      //   if(state.count > 0){
      //       state.count--
      //   }
      state.count > 0 && state.count--;
    },
    change(state, newCount) {
      state.count = newCount;
    },
    // 定义好mutation函数之后，在组件内可以使用store的commit方法来触发对应的mutation函数
    // 比如 this.$store.commit('add')
    // 比如 this.$store.commit({type:"add"})
    //   mutation 传参的写法
    // this.$store.commit('add',payload) 接收的时候payload 就是第二个参数
    // this.$store.commit({type:'add',count:值}) 接收的时候commit 传递的对象就是第二个参数
  },
});
// 2.导出
export default store;
// 3.组件的使用
// a.在main.js中导入，然后挂载到new Vue 中
// b.在组件中直接使用 this.$store.state.count访问
```

#### state

- 相当于 data 的返回值
- 在组件中使用 this.$store.state.属性名 拿数据

#### mutations

**就是用来修改 store 数据的函数**

- store 里的数据在 vue 组件里使用

1. this.$store.commit("add")
2. this.$store.commit({type:"add"})

- 每一个 mutation 函数默认第一个参数接收的是 store 内的 state， 想要修改哪个数据直接在函数内修改即可
- mutatian 函数的第二个以及后面的参数 称为载荷数据(payload) 用来修改或者
  添加 vuex 里 store 里的数据,组件中传什么就改成什么

##### mutation 传参的写法

```js
 this.$store.commit('add',payload) 接收的时候payload 就是第二个参数
 this.$store.commit({type:'add',count:值}) 接收的时候commit 传递的对象就是第二个参数
```

```js
store 里接收参数
 mutations: {
      addComment(state,{comment}){
      state.articleComment.push(comment)
    },
}
```

```js
组件里传参
methods: {
    sub() {
      const { text } = this;
      if (text) {
        this.$store.commit({
          type: "addComment",
          comment: {
            id: new Date().getTime(),
            text,
          },
        });
      }
      this.text = "";
    },
}
```

- 对象的新增属性操作不能引起视图变化

```js
updateObject(state,age){
        // state.testObject.age = age 对象的新增属性操作不能引起视图变化
        // 需要使用 vue 的 set 方法添加
        Vue.set(state.testObject,"age",age)
        // 或者直接对原来的对象从新赋值
        // state.testObject = {...state.testObject,age}
    }
```

##### 使用 v-for 循环一个对象

```html
<!-- object是一个对象 vulue代表属性值 key 代表属性名 -->
<div v-for="(value, key) in object" :key="key">
  <p>
    <span>{{ key }}</span>:
    <span>{{ value }}</span>
  </p>
</div>
```

#### state 的计算属性 getters

- **在组件中使用 this.$store.getters.commentNum(getters 里的函数)**
- getter 函数默认接收 state 作为第一个参数，函数返回值就是计算属性的值
- 接收 getter 作为第二个参数 该参数指所有的 getter
- **传参的 getter 使用的时候需要当成函数调用**
  getter 函数要返回一个函数， 返回的函数必须设置返回值，这个返回值是计算属性
  返回的函数 接收组件内使用 getter 的参数

```js
- state 的计算属性
getter: {
    commentNum(state,getter){
        console.log(getter.a)//组件内传递commentNum后会输出10
    return state.articleComment.length
    },
    a(){
        return 10
    },
//   传参的 getter
  getCommentById: (state) => (id) =>
    state.articleComment.find((item) => item.id === id);
}
```

```js
- 组件里的传参数
 methods: {
    getCommentById() {
      console.log(this.$store.getters.getCommentById(2));
    },
  },
```

#### action

action 函数 ，存放更新 store 数据的异步操作
异步执行之后 使用 commit 提交 dispatch

```js
getComments: async ({commit})=>{
    // 发请求获取评论数据 然后使用 commit 提交 mutation
   const res = await axios.get("/comments?articleId=1")
   commit("getComments",res)
  },
```

- 在组件中使用 dispatch 触发 action this.$store.dispatch('action函数名')
 比如 this.$store.dispatch('getComment')
- action 函数的函数名一般设置成和对应的 mutation 函数名相同
- acation 函数默认第一个参数是 context 它与 store 实例具有相同的属性和方法，我们可以从该对象找那个获取 commit 方法

#### modlues

- 一个 store 模块就是一个对象，这个对象下可以写 state mutation getters actions

```js
import axios from "../../publics/axios";
const article = {
  // 模块内的state需要写成函数返回一个对象
  state: () => ({
    data: null,
  }),
  mutations: {
    getContent: (state, contents) => {
      state.data = contents;
    },
  },
  actions: {
    getContent: async (x) => {
      const res = await axios.get("/articleConent/1");
      x.commit("getContent", res);
    },
  },
};
export default article;
```

然后导入 Vuex 内

```js
import article from "./modlues/article"
// 用来合并模块
modlues:{
  article:article
  属性名自定义 属性值是我们导入的store模块
}
```

- 在组件中使用数据的时候 this.$store.state.(modluse模块的属性名).(模块里state的属性值)
比如 this.$store.state.article.data
- 尽管分了模块 如果模块没有命名的话，matation action 都是全局的，也就是说在组件里 commit 和 dispatch 触发对应的函数的时候和原来没有区别。

##### 命名空间 namespaced: true

- 当模块添加里命名空间 空间的名称是在 store 中合并的时候的属性名
- 组件内访问该空间写的所有内容是需要 指定空间名
- 例如

```js
执行 action 时 this.$store.dispatch('空间名/action函数名')
执行 getter 时 this.$store.getters['空间名/getter名']
```

- actions 一个模块内的 action 函数内的第一个参数中可以获取到 commit dispatch getters, rootGetters 前两者局部数据 后两者全局的

- 模块内的 getter 函数默认接收三个参数 stare getters rootState, rootGetters 前两者局部数据 后两者全局的

##### mapstate 辅助函数

借助 mapstate 辅助函数获取 store 中的 state 数据
mapstate 函数调用之后会返回一个对象, 该对象下的属性就相当于组件的计算属性
mapstate 函数地用的时候传递参数有两种 
1.对象
2·数组

```js
import {mapState} from "vuex"
computs:{
...mapState({
  // 对象写法
  // 1. 箭头函数写法
   comments：state => state.commentModlues.comments
  // 2. 普通函数写法 普通函数可以内可以使用 this 获取组件
  comments(state){
    return state.commentModlues.comments}
})
}
```

```js
computed:{
  // 对象写法
...mapState({article:"article"})
// 对象写法
...mapState(["article"])
}
// 区别在与就算属性的名称 数组写法有局限性
```

##### mapGetters 辅助函数
写法跟mapState类似
```js
import {mapGetters} from "vuex"
// 没有mapGetters前
// commputed:{
//   commentNum(){return this.$store.getters["commentsModules/commentNum"]}
  ...mapGetters({
    commentNum:"commentsModules/commentNum"
  })
   ...mapGetters(["a"])
}
```
##### mapAction 辅助函数
```js
import {mapAction } from "vuex"
created:{
  // this.$store.dispatch("getArticle")
  this.getArticle()
}
metcheds:{
getArticle(){
//   this.$store.dispatch("getArticle")
// }
 ...mapActions(["getArticle"])
}
```