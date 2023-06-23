* Vue*

---

- nvm 版本切换
- npm 软件安装
  - 设置镜像 --cnmp从国内下载
  - nmp -v

- con + shift + x  vscode插件

---

## 逻辑

- 有数据时读取数据



## 名词

- sea.js
- require.js
- cdn
- es6模块



## 命令

- data(){}

  - 在export default里使用外界的方法或者函数必须要在data里挂载注册

- methods:{}

  - 复杂逻辑时使用方法
  - 人为传递事件对象----$event传到参数里

- mounted(){}

  - 生命周期函数

- watch{}

  - watch下的方法参数 第一个为新的值，第二个为旧的值。
    - 只设置一个时，默认为新值

- Vue.createApp({})
  - ~.component({})
  - mount 挂载

- v-for=""

  - in循环和of循环
  - 可遍历数字
  - 可遍历对象
  - value key index    属性值 属性名 索引值

- v-text =={{}}
  - 动态计算

- v-html        对代码进行原样解析

- 子组件修改数据影响父组件：

  - v-model:value
    - 简写：v-model=“”

  - 子组件中需要有的元素：props(传递父子组件间的数据)，$emit自定义事件

- 数据绑定：v-bind
  
  - 使用后属性为表达式，不为原始值   
  - 简写：:id
  - 属性动态计算： :[xxx]=""
  
- v-show 是否显示内容

- v-once 只渲染一次i

- v-on:

  - 可以一次使用多个方法
  - 简写：  @
  - click=""

- 阻止默认行为
  - event.preventDefault()

- 修饰符：
  - .xxx
  - 例如：@click.prevent
  - $event    在前台中传递参数，把event传递进去、

- v-if & v-show
  - 切换/交互频率高 使用 v-show   : v-if
  - v-show 不可使用template和v-else
  - 条件判断

- $attr.xxx

- 取消渲染 template标签

- 事件修饰符

  - 鼠标事件
    - capture 捕获：从捕获阶段输出
    - stop：阻止冒泡
    - self:  捕获的最底层执行
    - once:只执行一次
    - prevent:阻止默认行为
    - ★passive：跳过js对默认行为阻止判断的逻辑代码，在滚动这种高频事件中使用可以提高性能意思是：我不阻止默认行为，不需要判断。即后续如果写阻止默认行为的代码会失效
    - 特殊按键
      - left     按鼠标左键
      - right  按鼠标右键
      - enter  提交异步发送数据

  - 键盘事件
    - *绝大多数情况下结合表单使用*
    -  @keyup.<某个字母> 表示只有按<某个字母>时才触发
      - 组合键定义 keyup.xxx.xxx  表示组合按键才触发
      - control在组合定义里必须写成ctrl

  - 键盘+鼠标事件
    - @click.alt
    - input的name一般不用
    - 使用.exact修饰符，表示只按当前设置的键触发，对设置的键包容的按键不触发

- 表单相关

  - 文本域textarea 和input发生变化时，使用v-mdel双向绑定，就是在修改data里的数据。

  - v-model，双向绑定input输入数据

    - ★.lazy     unfocus时发送同步数据
    - ★本身具有性能消耗，每次都同步会对异步请求影响

  - 通过input本身的状态可以对data中的布尔值进行改变

  - true-value&false-value 对icheckbox的true和false定制其返回值（在复选的时候，为其设置值可以根据是否选中给数组中添加和删除可选的元素，否则的话，默认值为“on”）

  - 格式：

    label 循环数据 =》 input使用数据

  - input:r快速建立单选框

    - 单选特点：当value为当前设定的值时，选中后无法返回，默认为'on'所以设置多个单选时，value都为'on'无法实现真正的单选
    - 通过设置vlaue = 0 或 1 等数字进行单选
    - value="" 填入的数据，在darta里是字符串，使用数据绑定后，:value=""填入的数据就是数字
    - select下拉列表
      - multiple属性
      - option设置选项
        - 设置value值，可以设置为对象。设置multiple的时候绑定的数据必须为数组

  - 表单中的内容为字符串，输入的数字为'12222467'类似

  - 修饰符

    - v-model.lazy  鼠标unfocus时触发
    - v-model.number  将数据作为数字而非字符串同步更新
    - v-model.trim   去除左右两边的空格   //空格在input中占长度     提交到后台时空格也会存在里边



## 单页面

前后端分离

从后台一次性请求所有资源，后续请求拦截。

根据路由渲染页面

## 多页面

服务器端渲染数据

一次请求一次响应



## 学习顺序

视频->文档



### template覆盖

template在使用数据时会产生覆盖



## 花括号内写js表达式





Vue对容器本身不做修改，容器只是个容器，是对容器的下属进行修改

## xss攻击

- 反射形---诱导点击，窃取cookiie钓鱼
- 存储形----服务器端，在服务器相应请求时加载
- dom-base形---客户端，修改dom结构，js自身缺陷



## 计算属性

单独提取出来

- 使用方式与data的属性是一样的，都可以使用{{}}和v-text

- 只有当使用响应式数据时，才会发生变化
- 动态进行计算，主要根据vue里的data。动态计算数据
- 计算属性等同于一个动态的data数据

## 监听器

- 当某个数据发生变化时，后续进行的一系列操作

- 监听器的对象就是data里定义的数据

  

## vite&yarn&npm包管理工具

yarn create vite <project name> --template vue

cd 

yarn

yarn dev







## 处理css格式文件正交性

- 为其组件声明父级，通过css预处理器进行嵌套。

- scoped



## css属性修改

使用:class=“｛｝”

使用:id="[]"

根据data的布尔值进行二元判断

多个样式使用数组

data对象+:class数组绑定 一次定义多个样式，进行多个样式的控制

## 安装Sass

yarn add -D sass

## 



## 不使用vite构建工具

Vue.createApp({

}).mount()

组件声明和使用vm.component({component_name,methods})

## 命名方式的不同

html解析会自动转为小写

当文件名出现大写字母时，不使用vite/webpack情况下，其名称例如：

hdXj  需要写为:<hd-xj>。只有在vite/webpack中写<hdXj>才可运行





## 接收数据



```
前台设置
:data="<循环的每个对象>"
后台设置
export default {
	props:['data'],
	template:``
}
```

props内的数据为什么，App中标签的属性的就相对应的可以填入什么



## 单项数据流

- 父组件=>子组件传递数据
- 注意引用类型

---

## ★数据传递

父组件：

​	![image-20221002110645234](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221002110645234.png)

子组件：

![image-20221002110722028](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221002110722028.png)

1. 父组件通过v-bind  将父组件中的数据传递到子组件中

2. 子组件通过props开放数据接收端口，子组件即可使用父组件传递的数据
3. props内定义的数据相当于子组件中data定义的数据，都是数据，只不过是父组件传递的数据.

---

## 非Proprs属性

- 父级设置的，会自动放在子级根元素标签上

- 在子组件中指定属性位置放置，在其标签上设置

- 注意：非props属性可以自动传递，在未禁用默认传递时，父组件@click会自动传递到自组件中。属性是也类似，可以利用这个特性，直接在父组件上使用@作为非props传递而非v-bind作为绑定数据传递。如果禁用了默认传递，子组件使用v-bind接收，如下。

  ```js
  inheritAttrs:false			阻止默认传递
  
  v-bind="%attrs"  			批量设置
  :id="xxx"					单独设置
  ```

---

## 方法与属性传递

- 总的思路有两种
  - 一是通过$attrs，使用父子组件默认传递 + inheritAttrs ：false
  - 二是通过emits

- 父级组件设置方法=>通过v-bind=""绑定属性或者方法
- 子组件在props里接收
  - 如果是方法，其type为Function
  - 如果是属性，其type为String
- 方法在子组件触发

---

## 事件传递(非emit)

- 本质上比较粗暴，属性会被全部压入

- 子组件调用父组件方法
  - 子组件 inheritAttrs :false ，通过$attrs批量绑定数据到某个标签上
  - 父组件引入数据，设置数据处理方法，通过单项数据流传递到子组件，方法在子组件触发

---

## ★emit

- 使用数组接收不对其进行验证，使用对象接收对其验证
- 在子组件内部自定义事件处理
- 父组件通过@xxx="/methods/"传递方法，子组件通过$emit('/methods/')接收
- 书写：emit:['','','']
- 验证
  - emits:{ xxx(v){   /验证代码/ }}



- 声明事件=>注册事件=>子组件通过emit调用=>执行父组件传递的方法

---

## v-model表单绑定

- 双向绑定实现

  - 总体思路：单向绑定+同步事件监听

  ```js
  <input type="text" 
  :value="testMsg"       													单向绑定
  @input="this.testMsg = $event.target.value">							事件监听
  ```

- 简写 ： v-model="" 

  - 实际为： v-model:modelValue=""
  - 需要子组件挂载，定义。返回



---

## 插槽

- summary:

  ```
  子组件:<component :is="xxx">
  父组件:<slot/>  // <slot></slot>
  ```

  

- 留空白写成自闭合标签：

  ```
  <slot/>
  ```

- 插槽内设置的标签，作用域在本页面内部

- 父组件=>子组件

  - 使用props，单项绑定数据传递

- 子组件=>父组件



- 默认值

  - text节点

  ```vue
  <slot>默认值</slot>
  ```

- name属性

  - 不传递name时，默认会插入默认插槽里 即 <slot name="default"/ >里

- 实操：

  - 父组件： <templatev v-slot:xxx>
  - 子组件：<slot name="xxx"></slot>

- 简写： #

- 删除实现

  ```
  //1父级删除
  //父级设置删除事件，通过emit传递到子组件中，子组件设置emit接收
  del(lesson){
  	const index = this.lessons.findIndex(l=>l.id == lessons.id)
  	this.lessons.splice(idnex,1)
  }
  
  //2插槽删除
  //通过插槽进行父子组件数据传递
  父
  <lesson v-for="lesson in lessons" key="lesson.id" :lesson_item="lesson">
  	<template #default="id">
  		<button @click="del(id)">删除</button>
  	</template>
  </lesson>
  子
  <div>
  	<slot :id="lesson_item.id"> <slot/>
  </div>
  ```

  - ![image-20221005200025780](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221005200025780.png)

  - 分开接收/全部接收

- 独占默认插槽
  - 父级标签上添加属性 #default="{xxx}"  子组件只有一个slot时才适用 

---

## ★文件归档

- apis 存放复用的api,interface，type接口

---

## 组件动态渲染

- 父组件引入所有子组件=>使用<component :is=""/>标签 
  - 通过data数据的更新来调整组件的动态渲染
  - :is的值即为组件的名称，is修改，渲染的组件也随之修改
  - 经常配合v-if进行筛选判断

- 全局组件声明

  - 在入口的脚本文件中挂载 

    ```
    const app = Vue.createApp(APP)
    
    app.component('xxx',xxx)
    
    app.mount(#app)
    ```

- ★数据穿透

  - 响应式数据
    1. 原始数据类型：从Vue中导入computed，对数据进行包裹
    2. 转变为引用类型数据
  - provide				父组件使用provide传递给子组件
    - 当provide是数组时，不可以读取data里的数据
    - provide为函数时，像data一样返回数据，可以读取data里的数据
  - inject                   子组件使用inject接收

  - 技巧：
    - 传入配置项，通过provide传递给所有子组件

- 数据缓存

  - keep-alive

- ★ref

  - 将基本数据类型进行包裹，使其具有引用特性，以便于数据响应
  - 标签设置属性 ref="xxx"
  - 调用时，使用this.$refs.xxx 进行调用
  
  - 小技巧：
    - 对component标签设置ref，对其动态定位
  

## 生命周期

- 创建
  - beforeCreate(){}
  - created(){}
- 挂载
  - beforeMount()
  - mounted(){}                           真正挂载
- 更新
  - 数据触发重新渲染时，实时聊天
  - beforeUpdate(){}                                        更新前可以对组件进行控制
  - updated(){}
- 卸载
  - 播放器，定时器
  - beforeUnmounted
  - unmounted
- ★使用
  - 除了没有**创建**的声明周期函数，其它的都有
  - 挂载
    - onBeforeMuont
    - onMounted

  - 更新
    - onBeforeUpdate
    - onUpdated

  - 卸载
    - onBeforeUnmounted
    - onUnmounted


创建过程，从外到内。挂载过程从内到外

---

## ★★组合API

- ★可选链
  - 语句结尾加上?

- Summary:

  ```
  const {emit,expose,attrs,slots} = context
  ```

  - setup的声明周期位于beforeCreate和 created之间

- 组合api中不要使用计算属性

- 响应式数据

  - 引入ref

  - 读取值的时候需要使用xxx.value

    ```
    import {ref} from 'vue'
    
    export default{
    	setup(){
    	xxx
    	xxx
    	return {xxx,xxx}
    	}
    }
    ```

- methods

  ```
  let xxx = ()=>{}
  let xxx = function(){}
  ```

  

- watch

  ```
  import {watch} from 'vue'
  watch(target,callback)
  ```

- watchEffect

  - 启用时自执行，通过watchEffect设置初始值
  - 后续只在使用了响应式数据时执行
  - 让监听在某些情况下失效

  ```vue
  import {watchEffect} from 'vue'
  const stop = watchEffect(()=>{})
  
  使用返回值时，使watch监听失效
  stop()
  ```

- props

  ```
  与setup同级,子组件父组件写法与optionsApi类似
  props:{}
  setup(props){
  	let component = ref(props.xxx)
  }
  ```

- emits

  ```
  父组件传递事件，子组件emits接收
  emits:['xxx']
  setup(props,context){
  	const {emit} = context
  	
  	let func = ()=> emit('xxx',xxx)
  	return {func}
  }
  ```

- context

  - 通过对context解构，可以提取其中的属性

  ![image-20221009085900566](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221009085900566.png)

- ★ref

  ```
  1 组件获取：
  
  <template>
  	<yFunc ref="xxxxx"></yFunc>
  </template>
  
  <script>
  	export default{
  		setup(){
  			const xxxxx = ref()						将变量名设置成标签ref参数
  			const xxxFunc = (v)=>xxxxx.value?.num   这里的问号表示如果存在再返回
  		}
  	}
  </script>
  
  2 组件返回
  return {xxxFunc}
  
  通过ref获取到的组件，使用xxxxx.value.xxx可以获取在子组件中返回的属性
  ```

- expose限制暴露

  ```
  setup(){
  	const {emit,expose} = context
  	expose({xxx})										//只对外暴露的属性
  	return {xxx,xxx,xxx}
  }
  ```

- 引入生命周期组件

  ```
  import {onMounted} from 'vue'
  setup(){
  	onMounted(()=>{
  		...
  	})
  }
  ```

- slot

  ```
  使用slots接收所有default，在子组件中定义slot位置，在父组件中引入
  
  子组件
  const {slots} = context
  const defaults = slots.default()
  return {defaultSlot}
  
  <template>
  	<component :is="defaults[0]">
  	xxx
  	xxx
  	xxx
  	<component :is="defaults[1]">
  </template>
  
  
  父组件
  <yDIY>
  	<h1></h1>
  	<p></p>
  </yDIY>
  ```

- computed

  ```
  根据响应式数据发生动态变化，说白了是依赖响应式数据，响应式数据变了计算属性也跟着变化。
  以响应式数据为基础
  
  引入
  import {computed} from 'vue'
  声明
  let sum = ()=>num.value + 100;
  返回
  return {sum}
  ```

- provide&inject

  ```
  数据在父组件中修改
  在子组件中修改，传递方法进行修改(必须为响应式数据)
  provide('xxx',(newValue)=>{xxx.value = newValue})
  
  
  父组件引入provide,子组件引入inject
  import {provide} from 'vue'
  import {inject} from 'vue'
  
  使用
  provide('发送','发送的值')
  const user = inject('接收','如果接收为空时的默认值')
  
  返回(子组件)
  return {user}
  
  以上是发送静态数据，响应式数据需要用ref进行包裹,如下：
  	相应的，获取值的时候使用msg.value
  
  let msg = ref('xxx')
  provide('xxx',msg)
  ```

- reactive

  - 通过reactive调用的变量，不能改变其引用地址，即设置另一个引用对象
  - Vue只对数据进行检测，不对数据中的属性进行检测；需要进行二级相应,二级响应时需要加上value值
    - 方法1：
      - let obj =reactive({name:'young'})
      - let name = ref(obj.name)
    - 方法2：torefs()
      - let obj = reactive({name:'young'})
      - return {...toRefs(obj)}

  ```
  ref对基本数据类型进行包装，需要用~.value获取其值
  reactive对引用类型进行包装，其调用时不需要通过~.value的形式，如：
  	let arr = reactive([])
  	arr.push('xxx')
  import {reactive} from 'vue'
  
  对数据进行展开
  ```

  

- return {...toRefs(xxx)}

---



## ★json-server

- npm安装，yarn安装失败

  - 安装postman，设置全局环境配置

    ```
    http://127.0.0.1:3003
    ```

  - ```
    json-server --watch --port 3003 --host 127.0.0.1 db.json
    ```

- 批量生成中文数据

  - 初始化

    ```
    yarn init
    ```

  - 安装mockjs

    ```
    yarn add mockjs
    ```

- 查看官方文档生成各类数据

## setup语法糖

优点：不必将数据手动返回，接口文件不必挂载

- ★组件全局异步

  ```
  <suspense>
      <template #default>
        <div>
          //component
        </div>
      </template>
      <template #fallback>Loding...</template>
    </suspense>
    
    两个插槽
  
  - 在异步加载完毕后
  - 在加载过程中
  ```

- defineProps({})

- defineEmits([])

- ★vue样式继承

  - 子组件的样式会默认继承父组件，css属性查找比class和id要慢很多倍，性能上不好

  - 解决方法：

    - 设置class，id等属性，不使用vue默认提供的属性选择器查找，不使用scoped
    
    ```vue
    解决方法1：在子组件中，最外侧加上标签
    <section>
        <div>
        	<input type="text" :value="todo.title">
        <button>删除</button>
      </div>
    </section>
    
    解决方法2：对样式设置类，具体化样式
    
    ```



## animation

> yarn add animate.css

- <transition></transition>

  ```
  .v-enter-from {}
  .v-enter-active {}
  .v-enter-to{}
  ```

  ```
  .v-leave-from{}
  .v-leave-active{}
  .v-leave-to{}
  ```

- 样式优化

  ```
  .v-enter-from ,
  .v-leave-from{}
  
  .v-enter-active,
  .v-leave-active{}
  
  .v-enter-to,
  .v-leave-to{} 
  ```

- 命名

  ```
  <transition name="xxx"></transition>
  
  .xxx-enter/leave-from/active/to{}
  ```

- keyframe动画

  ```
  .xxx-enter/leave-from/active/to{
  	animation: xxx .xs xxx;
  	
  }
  @keyframes xxx{
  	...
  }
  ```

- 自定义动画类名

  - 自定义后的动画类名可以更好地与CSS动画库结合
  - 自定义动画类名 + 动画库  实现较好的动画和可维护性

  ```
  <transition
  	enter-from-class="",
  	enter-active-class="",
  	enter-to-class="",
  	leave-from-class="",
  	leave-active-class="",
  	leave-to-class=""
  ></transition>
  
  
  
  
      enter-from-class=""
  	enter-active-class=""
  	enter-to-class=""
  	leave-from-class=""
  	leave-active-class=""
  	leave-to-class=""
  ```

- 设置初始自动渲染

  - transition中设置appear属性

- 使用js进行动画设置

  ```
  支持的事件种类
  <transition
  	@before-enter="",
  	@enter="",
  	@afterEnter="",
  	@before-leave="",
  	@leave="",
  	@after-leave=""
  >
  </transition>
  
  
  <script>
  	const xxx = ()=>{}
  </script>
  ```

- 多元素切换

  ```
  默认同步执行
  mode='out-in'
  mode='in-out'
  ```

- 组动画

  - ![image-20221023084835211](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221023084835211.png)



- 
  - todo-move
    - 原理上使用transition![image-20221023085332278](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221023085332278.png)

----

# vue router

## 基础知识

- router

  - index.js设置路由规则

    ```js
    import { createRouter ,createWebHistory} from 'vue-router'
    import Home from '../views/Home.vue'
    import Article from '../views/Article.vue'
    
    const router = createRouter({
      history: createWebHistory(),
      routes:[
        {
          path:'/',
          name:'home',
          component:Home
        },
        {
          path:'/article',
          name:'article',
          component:Article
        }
      ]
    })
    export default router
    ```

    v

- views

  - 设置渲染的页面(组件)

- App.vue

  - 注册使用

    ```
    <router-link to=""></router-link>
    <router-view></routerview>
    ```


```
yarn add vue-router@4
```

```
import {createRouter} from 'vue-router'
```

```
import {createWebHistory,createWebHashHistory}

createWebHistory 使用首页渲染vue，对SEO更好，但有与后台地址冲突的隐患
createWebHashHistory 使用锚点渲染vue，对SEO不友好

使用路由前缀
```

- 连接跳转

  ```
  <router-link to=""></router-link>
  ```

- 视图渲染

  ```
  <router-view>
  ```





切换点击时的颜色

- 打开chrome，调试找到相对应的css类名---使用系统提供的类

  ```
  <template>
    <div class="navigation">
      <router-link :to="{ name: 'home' }">Home</router-link>
      <router-link :to="{ name: 'article' }">Article</router-link>
    </div>
  </template>
  
  <script setup lang="ts">
  
  </script>
  
  <style lang="scss" scoped>
  .navigation {
    a {
      background-color: #fdcb6e;
      padding: 5px 10px;
      color:#dfe6e9;
      &.router-link-active {
        color: white
      }
    }
  }
  </style>
  ```

- 使用props

  ```
  嵌套路由
  非嵌套路由
  ```

  

- linkActive class 

  - 父子级关系中存在

- linkExractActive class

  - 明确点击的
  - 在路由配置中，可以修改linkExtractActiveClass

---

- 别名 alias

  - vite.config.ts中设置alias别名，省去相对路径的问题

    ```
     import path from 'path'
     
     resolve: {
        alias: { '@': path.resolve(path.resolve(__dirname,'src')) }
      }
    ```


---



## 视图

使用视图，说白了就是在渲染组件的时候增添判断

```
        <router-view name="navigation" #default="{Component}">
          <component :is="Component ?? navigation"></component>
        </router-view>
```

---

## 路由跳转

钩子函数：

- 组件守卫

  ```
  beforeRouteEnter		其它的路由进入到此路由的之前   这时
  beforeRouteUpdate
  beforeRouteLeave
  ```

- 全局守卫

  ```
  beforeEach				全局前置
  beforeResolve			全局解析
  afterEach				全局后置
  ```

- 路由守卫

  ```
  beforeEnter
  ```

  

情况一：跳转页面，路由改变的时候

- 全局守卫的三个必然执行 

  ```
  beforeEach		
  beforeResolve	
  afterEach	
  ```

情况二：渲染当前页面，仅参数发生变化时

- 只执行全局守卫+组件更新守卫

  ```
  beforeEach		
  beforeRouteUpdate
  beforeResolve	
  afterEach	
  ```

其它情况：

```
离开
beforeRouterLeave 
全局+路由+组件
beforeEach
beforeEnter
beforeRouteEnter
beforeResolve
afterEach

```

---

watch监听中的渲染时就立即执行

```
watch(obj,()=>{},{immediate: true})
```

