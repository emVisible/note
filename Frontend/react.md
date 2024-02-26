# 命令

脚手架: npm-create-react-app -g
版本: create-react-app --version
创建 create-react-app xxx   (React规范：小写字母+数字+_)

# 相关数据包
- prop-types 检测props数据
- react-jss react css
- axios && qs 网络传输
- blueimp-md5 加密
- fastclick 移动端click事件
- http-proxy-middleware CORS
- lib-flexible 移动端响应式
- postcss-pxtorem 移动端响应式
- cross env 设置env

# 基础知识
React本身是JS的地基, 要理解JS的特性, 作用域、闭包、原型等
- 其它补充
  - camelCase / PascalCase / kababCase (xxx-xxx)
  - React.createElement(el, props, ...children)
    - 其返回的对象既为VDOM | JSX对象 | JSX元素 —— 本质上都是通过JS对象表示的对需要生成的DOM的描述信息
    - 包括$$typeof type props key ref等属性, props中又包含children以及普通props, children通过钩链进行递归操作
    - 其中第三个参数可以直接为VDOM对象 / JSX对象
  - 组件使用CamelCase命名
  - 对象设置 (React组件中, props为只读, 其原因是被冻结)
    - 冻结 Object.freeze() / Object.isFrozen(), 不能进行曾删改劫持以及Object.defineProperty()
    - 密封 Object.seal() / Object.isSealed(),可修改值, 不能增加删除劫持
    - 不可扩展 Object.preventExtensions() / Object.isExtensible, 不可增加成员
  - 类组件中, 构造函数为什么需要super(props)?
    - 在原理中, Component默认接收props并对this进行绑定, 继承后调取实例this指向发生变化, 即指向类组件的实例; 而Component本身需要接收参数, 绑定props到this上, 这样一来, 不传递props就相当于Component在空转, 因为Component没有props数据可以绑定到this上
  - 使用UNSAFE_xxx可以手动指定该方法为不安全方法, 去除console中的warning
  - React.StrictMode 属于React的严格模式, 用于检验React的语法等规范性 / 旧版组件库存在不规范的React语法, 可以不使用React严格模式
  - 周期函数=钩子函数
  - 浏览器渲染队列 && VDOM初次渲染 比较类似, 都是准备好之后, 一次渲染
  - 原生冒泡与捕获的起点和终点为document
  - (模拟触摸事件以去除300ms延迟: onTouchStart/onTouchMove/onTouchEnd)fastclick包 / 手势事件库2
    - 连续点击两下: PC端 2次click + 1次doubleClick; 移动端(300ms延迟): (点一次后300ms内点第二次)只触发doubleClick
  - render方法只是转为真实DOM, 但还需要最后的将其放到浏览器中
  - 特殊的命名规则: 使用useXxx作为自定义Hook命名, 通过jsx解析则会有Hook相关的特性——无法在循环、判断中使用

版本差别
- 渲染
  - 16: React.render()
  - 18: root=React.createRoot(...); root.render()
- setState任务队列
  - 16: 合成事件 && hooks为异步, 其它为同步
  - 18: 均为异步
- SyntheticEvent
  事件缓冲池: get-操作-clean
  - 16: 基于事件缓存池(通过e.persist()可缓存事件对象; 防止重新创建新的合成对象)  事件委托给document, 只对冒泡实现事件委托
  - 18: 无事件缓存池(无事件对象信息清空的问题);   委托给#root, 拆分捕获和冒泡两个阶段, 均实现

- webpack配置项与React的关系——>通过eject命令暴露配置项-> 重新配置webpack配置项
  - 通过配置webpack, 修改默认端口、打包路径等操作
  - 兼容处理
  - 跨域处理
    - 跨域代理模块: http-procy-middleware, 是webpack dev server的底层实现

- 数据驱动渲染视图 MVC(React) MVVM(Vue)
  - MVC(model, view, controller) / MVVM(model, view, viewModel)
  - 基本思想：不直接操作DOM, 而是通过数据操作DOM -> 规范下, 不应该直接操作DOM
  - 根本原因：重绘导致的性能开销大
  - 核心实现：虚拟DOM->真实DOM, 避免DOM重绘
  - React
    - Controller层：通过View层->人机交互
      - 根据业务需要, 使用React驱动
      - 与vue不同的是, React是单向驱动, view->model的驱动需要手动实现
    - View层：通过Model层->视图渲染
      - 基于JSX语法构建视图
    - Model层：通过Controller->数据更新
      - 根据需要动态变化的数据, 建立相应的数据模型
  - Vue
    - ViewModel层 (Vue核心实现)
      - 与MVC不同的是, vue实现了双向的数据监听, 即视图内容改变, 同时映射到数据中, 实现反向驱动 (双向数据绑定)
    - View层
      - 通过Template语法实现
    - Model层
  - * 引起重绘的原因
  - * 避免重绘


- jsx 基础
  - 只支持js表达式 / createRoot只能指定body的子节点作为root / 根容器 && 根元素的区别
  - React.Fragment: <></> 空文档标记标签, 既提供了根元素, 又不会占据具体位置
  - mustache:
    - 原始值: string / number 其它数据类型渲染均为空
    - 对象: 支持, 数组会flat之后依次渲染 && JSX VDOM渲染 && style 行内样式; 不支持Object渲染
  - 在style内可以用js表达式, 比如三目运算
  - 通过map操作Model时, 需要给循环元素的根元素给添加key(key一般为index或者data item ID)
    - 具体原因：方便对DOM Diff
  - 单独创建循环, 不依赖数据->new Array(n).fill(null), 本质上是创建了一个密集数组
    - 密集数组->每一项都有值, null也可以
    - 稀疏数组->每一项都是empty
- jsx 机制
  - 本质上是语法转换, 将JSX语法转为React代码(Controller), 最终操作真实DOM(Controller -> Model -> View, VDOM->DOM)
  - 1. 创建VDOM
  - 2. 转换为真实DOM
    - 第一次渲染时, 缓存VDOM, 并直接转换为真实DOM
    - 后续更新时, 通过diff比对, 计算PATCH包(差异), 最后只更新PATCH补丁包

- slot
  React中需要手动实现slot机制
  在FunctionComponent中, 接收props.chldren, 随后：
  - 通过React内置函数：React.children.toArray(children)
  - 手动写判断

  - 具名插槽
    - 对子组件
      - 设置数组存放具名插槽位置
      - 对props.children进行filter遍历, 提取具名, 并将其对应child放入数组中
      - JSX渲染数组
    - 对父组件
      - 传递相应的props, 一般叫slot即可

- 组件
  - 组件封装
    - 实现: slot + 规则校验(使用PropTypes包)
  - 静态组件(函数组件)
    静态组件无法基于内部实现视图更新
    应用场景: 不需要动态更新; 只需要渲染一次
    - 函数属于静态组件:
      - 初次渲染: 从函数作用域中解析props(冻结), 最后对VDOM渲染
      - 后续操作: 只更新作用域中的数据, 并不触发组件内容的更新渲染
      - 转为动态:
        - 在父组件中传递不同的props, 并调用, 父组件更新, 子组件也会相应更新
        - Hooks + 函数组件, 实现静态组件动态化
  - 动态组件
    类组件, Hooks组件
    - 类组件
      初次渲染: getDefaultProps-getInitialState-componentWillMount-render-componentDidMount
      后续更新: componentShouldUpdate-componentWillUpdate-render-componentDidUpdate 后续更新只在初次new的实例上, 重新调用render

      - (ES6)class xxx extends React.Component || class xxx extends React.PureComponent; (ES5) 组合寄生
        - constructor可以不写, React会自动将属性绑定到实例上
        - constructor写出来, 一般用于添加动态计算的属性 / 额外属性
      - 覆盖render方法
        - render渲染时, 基于type不同: str-标签; function-执行&&属性绑定; constructor-执行(new)&&属性绑定到实例
        - 每次调用类组件都创建单独的实例
        - render方法返回的VDOM作为视图渲染

      - 状态初始化(state)
        重要的思想是通过状态的变化进行编程, 状态值与视图的更新之间的关系
        - state会自动挂载到实例上,默认为null
        - React中直接修改状态不会使视图更新——对比vue, vue通过对状态进行数据劫持, 会在set函数中通知视图更新
          需要通过特定的方法进行视图更新, 需要基于React本身提供的方法
          - setState() 设置state值并更新视图
          - forceUpdate() 强制更新

        - 初始化时依次的Hooks顺序, 常用
          - componentWillMount 第一次渲染前
          - render 第一次渲染
          - componentDidMount 第一次渲染完毕, 可获取到DOM
        - 后续状态——组件更新逻辑
          - shouldComponentUpdate(previousState, nextState) previousState为改变的当前值, nextState为要更新的值
            - 若使用了forceUpdate(), 会跳过校验
          - componentWillUpdate(previousState, nextState) (Unsafe)状态未修改
          - render, 生成new VDOM -> Diff对比 -> 渲染差异部分为真实DOM

        - 父组件的渲染遵循深度优先:
          - 父组件初次渲染:
            - (Father)componentWillMount -> (Father)render ->  (Father)componentDidMount
            - 其中, FatherComponent render = [((Child))willMount -> (Child) render -> ((Child)) didMount]
            - 整体是深度优先遍历
          - 父组件的更新:
            - (Father) shouldComponentUpdate -> (Father) componentWillUpdate ->  (Father)render -> (Father)componentDidUpdate
            - 其中, (Father)componentWillUpdate = [(Child)componentWillRecieveProps->(Child) shouldComponentUpdate->(Child) componentWillUpdate->(Child)render-> (Child)componentDidUpdate]
          - 父组件卸载:
            - (Father)componentWillUnmound->销毁
            - 其中, (Father) componentWillUnmound = [(Child)componentWillUnmound -> 销毁]

- PureComponent
  - 类组件继承后, 会增加一个shouldComponentUpdate Hook, 所以在继承了它之后, 显式使用shouldComponentUpdate会出现警告
  - 其中, shouldComponentUpdate会添加一个浅对比(对Object只进行第一层对比, 先对比数量, 再对比属性值), 确定组件是否需要更新

- 受控组件与非受控组件
  - 受控组件：通过修改数据->视图更新
  - 非受控组件：通过Ref获取DOM元素->实现具体的需求和效果
    原理: render时根据VDOM的ref属性类别, 若为string, 则将其push到this.refs中; 若为function则执行;
    1. 给DOM元素设置ref, 通过this.refs.xxx获取
    2. 给DOM元素的ref=(dom)=>{this.xxx = dom}, 在组件内部设置reference
    3. 通过const ref = React.createRef()创建ref对象, 并在DOM的ref={ref}; 此时ref.current为当前的DOM对象
  - 在父组件中, 当ref指向子组件(类组件)时, 则获取的是组件实例
  - 父组件中, 函数组件不能直接通过ref获取引用, 会报错; 需要将函数组件包裹在React.forwardRef()中, 函数组件自动获取两个params: props和ref, 通过间接传递ref可以在父组件中获取一个子组件的引用

- React在组件上按照类型划分(函数组件 && 类组件), Vue在组件上按照作用域划分(局部组件 && 全局组件)

- setState
  队列 && 一次渲染(异步批处理)
  React18中, 均为异步操作; React16中, 合成事件 && hooks中为异步, Timer, DOM等为同步
  - this.setState(partialState, callback), 回调函数能够精准地对部分状态更新后触发, componentDidUpdate则类似于广播, 任何更新都会执行
    - callback机制类似于vue中的$nextTick
  - 注意异步更新+渲染机制
  - 更新逻辑: shouldComponentUpdate-componentWillUpdate-更新数据-render-componentDidUpdate-[callback]
  - setState通过任务队列updater, 对状态进行异步批处理(所有代码操作结束则开始清空队列 ), 当多个setState连续执行且指向相同的patialState, 则会一次执行, 只触发一次渲染
  - 减少更新次数, 提高渲染效率, 对状态有效进行批处理
  - import {flushSync} from 'react-dom'; 方法可以让状态更新队列updater立即处理; 具体使用: 包裹在setState中
  - 1. this.setState({}); 渲染一次,
  - 2. this.setState((prevState)=>{}); 渲染一次, 实现多个重复操作——将多个回调添加到队列中

- SyntheticEvent
  以onXxx开头的事件, 通过React内部进行了封装
  流程: 属性赋值-#root绑定(触发时先原生冒泡+捕获, 再到组合冒泡+捕获)-回调
  - 为处理事件传参: 绑定普通函数到类组件中, this为undefined: bind && arrow function; 接收param: SyntheticBaseEvent
    - 当传递额外参数后, 事件对象本身为最后的参数
  - 机制: 事件委托(而不是事件绑定, 除根容器之外, React不对具体的元素做事件绑定); 事件委托的基础是浏览器事件传递机制, 在此基础上封装, 实现事件委托, 并增加了一些事件处理;
    - 委托对象: R16及之前委托给document, 只对冒泡进行了事件委托; R17及之后委托给#root;
    - 最后对#root做事件绑定(捕获 && 冒泡); 这样达到任何事件的传递都会经过#root元素, 并触发其捕获和冒泡;
    - 委托机制: 为元素设置onXxx属性后, 通过#root的事件委托; 在相应的阶段触发属性对应的函数, 类似于回调
      通过e.path获取相对事件传递路径; 执行前对原生事件对象进行this重定向 && 合成对象处理
      - 冒泡: path.forEach(e=>{e.onclick && e.onclick()})
      - 捕获: [...path].reverse().forEach(e=>{e.onClickCapture && e.onCLickCapture()})
  - 合成事件中的stopPropagation
    阻止原生 && 合成事件的事件传播 (向上阻止原生事件e.nativeEvent.stopPropagation, 向下阻止合成事件)
    e.nativeEvent.stopImmediatePropagation()阻止同级合成事件
  - Vue中的循环事件绑定无事件委托机制, 有多少个事件就绑定了多少个; React则只对根容器绑定事件, 元素只添加属性, 委托给根容器

## React Hooks Component
Hooks组件本质是函数组件, 基于函数作用域, 是动态组件与静态组件的折中
函数组件更新的本质:
- 重新执行函数, 即创建函数作用域, 生成函数内的闭包, 消耗内存, 声明函数内部的地址空间

### useState
使用: 不需要变化的初始值, 直接传递; 需要加工的初始值, 通过函数传递;
特点
- 不支持部分状态修改 useState实现部分状态更改: setXxx([...Xxx, newState])
- (React18)异步批处理执行——异步+更新队列——单次渲染
- 可结合flushSync.
  ```js
  const [num, setNum] = useState(1)
  for (let i = 0; i < 10; i++){
    flushSync(()=>{
      setNum(num+1) // result: 11
    })
  }
  ```
- 自带性能优化机制: 每次修改状态值时, 进行componentShouldUpdate比较(Object.is)
状态改变时, 即值改变, 同时通知视图渲染
返回数组, index0为value, index1为set function
每次更新都是重新执行函数->传递props-产生作用域-Diff(初次更新无Diff)-Update, 产生新的作用域, 基于closure
```js
var _state;
function useState(initialValue){
  if (typeof initialValue === 'undefined') _state = initalValue
  var setState = function setState(value) {
    _state = value
  }
  return [_state, setState]
}
```
### useEffect
在函数组件中使用生命周期函数
使用:
- 不设置依赖(获取最新value)
  - useEffect(callback), 相当于componentDidMount
  - 第一次渲染 && 视图刷新执行
- 设置依赖
  - useEfeect(callback, []), 类似于componentDidMount
    - 仅在第一次渲染执行
  - useEffect(callback, [param]), 同上
    - 第一次渲染 && 依赖更新时执行
  - useEffect(()=>{return ()=>{}}) (获取上一次的value)
    - 组件施放时执行, 返回小函数
    - 若组件更新, 执行上一次的小函数, 返回小函数
原理:
- 通过mountEffect, 将callback以及相关信息添加到链表队列
- 视图渲染完毕后, 通过updateEffect, 将链表按相应的hook执行
执行顺序:
- 如果有基于return的函数, 优先执行
- 其它则按规则执行
细节:
- 需要在组件的最外层作用域中使用, 不能通过if for等作用域中嵌套
- async修饰function后, 默认返回Promise Instance;
  - 而useEffect如果使用异步callback, 则需要手动将返回值重写 / 相应步骤封装为异步函数, 再通过await执行 / 通过.then方法重构;
- 初次渲染完毕后会触发useEffect, 激活Effect链表, 从而重新渲染真实DOM, 当频繁激活时, 会出现内容闪烁
- useLayoutEffect:在初次render之前, 对状态修改并合并VDOM, 最后一次渲染; 触发上优先于useEffect
  - 改善使用useEffect中, 状态值多次切换导致多次渲染的问题
  - 区别就是useLayoutEffect会阻止真实DOM渲染, 优先执行Effect链表中的callback; useEffect不阻塞浏览器渲染真实DOM, 在渲染的过程中同时执行callback
- 无论是useEffect, 还是useLayoutEffect, 均不会影响DOM的获取;真实DOM已经创建, 区别只是浏览器是否渲染;
- 视图更新的步骤:
   1. 基于React将JSX转为createElement格式; (MVC中的C)
   2. 基于React, 创建出VDOM (MVC中的M)
   3. 基于React(render), 将VDOM转为真实DOM(DOM-DIFF)
   4. 浏览器将其结果进行绘制 // useLayoutEffect改变优先级, 优先同步执行callback, 再进行绘制; useEffect异步同时进行callback和绘制;

### useRef
ref的基本功能: 获取真实DOM的引用, 获取子组件实例(子-类组件、子-函数组件-forwardRef)
ref的基本使用(类组件): this.refs.xxx(不推荐); ref = {r=>this.xxx=r}; this.xxx = createRef() && <div ref={this.xxx}></div>
ref转发: const Child = React.forwardRef(function(props, ref){...}); 获取子组件特定元素
- *父组件获取子组件内部状态或方法——基于React.forwadRef(), 使用useImperativeHandle
  ```js
  useImperativeHandle(ref, ()=>{
    // return的内容被父组件接收, 使用该hook会覆盖父组件中的ref.current对象, 以此达到子(状态 && 方法)->父的传递
    return {
      stateA,
      StateB,
      MethodA,
      ...
    }
  })
  ```
组件中使用: useRef
对比:
- useRef在更新渲染前后的引用对象均为同一个对象, 性能开销小
- createRef在更新渲染后会创建新的引用对象, 性能开销大

### useMemo——栈内存缓存(原始值, 多用于string, number)
使用场景: 消耗性能 / 时间的计算操作 && 算法
目的: 减少函数组件更新时的不必要的性能开销, 当非依赖项改变时拥有缓存而不必重新计算耗时操作
原因: 基于函数组件更新的原理——每次更新重新执行函数全部的内容, 并基于引用构建闭包
诉求: 只有当依赖的状态改变时, 视图刷新
使用: useMemo(callback, [dependencies])
效果: 初次渲染时, callback执行; 依赖状态改变时, callback执行; 每次执行完毕, 将结果赋值给变量, 达到缓存的效果; 类似于Vue中的计算属性
useMemo可以多使用

### useCallback——堆内存缓存(引用值, 主要用于组件内部函数)
应用场景: 父子组件嵌套时, 使得子组件按需更新
使用: useCallback(callback, [dependencies])
效果: 初次渲染, callback执行; 依赖状态改变, callback执行;  每次执行完毕, 将结果赋值给变量, 达到缓存的效果; 类似于Vue中的计算属性

useCallback只在高频修改时使用

使子组件按需更新:
- 对父组件传递的属性 && 方法: 使用useCallback
- 对子组件:
   方法1: 类组件: 继承React.PureComponent(对新/旧属性比较——shouldComponentUpdate)
   方法2: 函数组件: React.memo包裹


### 组件通讯
单向数据流:
- 父组件---props && method--->子组件 ok; 反之不可
- 基于子组件修改父组件需要有父组件的支持——传递给子组件需要处理的信息, 即父组件本身要有处理自己的功能, 并将其传递给子组件


---


# 结构
React项目
结构
|- node modules
|- src
|- public (存放页面模板)
  |-index.html
|- ...

package.json
- React：核心框架
- React-dom：师徒渲染核心-构建WebApp页面
- react-scripts：打包命令的封装。webpack相关程序隐藏到了node_modules下

# 修改脚手架配置
eject命令
yarn eject

---

babel-preset-env es6+react语法转为es5

create-react-app脚手架使用的是sass

使用less

```
yarn add less less-loader@8
yarn remove sass-loader
```

---

# React Cook Book

## 创建应用程序

### 1 经典

```
npx create-react-app --template typescript xxx

yarn
cd yarn
yarn start

yarn build

yarn eject
```

### 2 Gatsby

内容丰富；生成静态网页版本；高相应速度

Ts支持；自动路由获取；插件丰富；

离线缓存；渐进式Web应用 PWA

SEO友好

```
npx gatsby new xxx

cd xxx
yarn dev

yarn build
```

引入动态内容

- Headless CMS 无界面内容管理系统
- GraphQL
- 静态数据源

### 3 Razzle

通用应用程序——既可以在服务器也可以在客户端上执行；快速构建demo，推迟对构建和部署应用的决定；

可配置插件构成，适应性强；扩展性强；

```
npx create-razzle-app xxx

同时构建客户端和服务器段代码
yarn start:pord

yarn build
```

构建应用程序时需要考虑的东西

- 要创建SFC吗
- 性能关键吗
  - 是否用SSR呢
- 需要用哪种部署平台呢
- 使用js还是ts呢

### 4 next

全栈框架；默认路由约定；无需管理路由配置

少量配置提升交付速度；低服务端需求友好；

*打包后不包括服务端api

```
npx create-next-app xxx

cd xxx
yarn dev

生成静态版本
node_modules/.bin/next export
```

### 5 preact / inferno

轻量级react；(notools方式下)核心preact不支持jsx，babel——不支持高级语法；

- 当作notools方式，在页面中当作独立的库使用
- 当作一个框架构建整个应用程序

```
npx preact-cli create default xxx

cd xxx
yarn dev

yarn build
```

### 6 nwb组件库

组件库可以保证风格一致；构建组件项目；

```
yarn add -g nwb
创建单独组件
 nwb new react-component xxx
创建完整应用
nwb new react-app/preact-app/inferno-app/vanilla-app xxx
```

### *7 webpacker给rails添加react

rails

- 传统开发模型
- 小型服务器框架
- 快速开发，适用于小型项目
- 缺乏交互

### *8 preact自定义HTML标签

### 9 组件开发中使用 StoryBook

检查组件运行情况；单独集中战士组件；提供组件属性示例；

可视化单元测试；

周边生态 add-ons

- 检查可访问性；
- 添加交互式属性设置控件
- 包含每个story内联文档
- 记录HTML快照，测试程序更改产生的影响

### 10 Cypress测试

浏览器运行；无需外部驱动；通过网络接口直接与浏览器通信；Jest格式

react项目普遍的测试库

- @testing-library/react
- Preact_Enzyme

而更好的做法是在浏览器中直接测试

