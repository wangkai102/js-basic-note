## 面向对象

### 首先来说面向对象的三大特性

- 封装

  就是我们把操作数据的具体内容隐藏起来，只暴露对外的接口。比如生活中开车，一脚油门，一脚刹车，我们不用操心脚踩下去车内部做了什么，我们只需来操作油门和刹车到达我们前进和停止的功能即可。

- 继承

  子类继承父类，子类也会具有更具体的特性。

- 多态

  还是源于继承，但是子类和子类之间又会有多样不同的表现，比如`Cat`类和`Dog`类都继承至`Animal`类，他们有相同的特性，比如都是哺乳动物，4 条腿，一个脑袋，还会具有一个叫的方法，但是他们叫的声音就不一样了，当然，猫与狗也还有其他不同的特性。

### 其次来说说`js`里的面向对象

- `ES5`

  在`ES5`时期，`js`原生对于面向对象编程的支持还是比较弱的，我们通常会使用工厂函数来进行，然后使用 new 关键字来实例化。

- `ES6`

  到了`ES6`就不一样了，它为我们提供了 `class `关键字，使用`class`可以来生成一个类，`class`中有`constructor`也就是构造函数，在构造函数里我们可以生成类的属性，如`this.name`、`this.age`，然后使用 `extends `关键字实现继承，使用`static`修饰符修饰方法为静态方法，不需要实例化，直接使用类就可调用。

- `ES7`

  在`ES6`中属性还需要通过构造函数` this.xxx` 来定义，在`ES7`中直接定义，如` age = 123`，同时也提案了通过`static` 修饰属性为静态属性，同样直接使用类就可以调用。

- `TypeScript`

  最后来说说 TS 里面的类，出了上述之外，多了 `public` 、`private`、和` protected` 三种修饰符，`public`修饰的属性和方法都是公有的，在任何地方都可被访问到，`private`修饰的是私有的，不能在声明它的类的外部访问，`protected` 修饰的是受保护的，它和`private `类似，区别是它在子类中是可以访问的。

## 继承

在`ES5`时期，我们通常通过原型来实现继承，常用的方式有组合继承和寄生组合继承。

### 组合继承

组合继承就是将子类的 `prototype` 指向父类的实例，同时在子类内部使用父类`.call`绑定当前子类的`this`实现对父类属性的继承，这种继承方式的优点在于可以使用构造函数进行传参，不会与父类共享属性，还可以复用父类的函数，但是同时也存在一个缺点就是继承父类时调用了父类的构造函数，导致子类的原型上多了不需要的父类属性，造成了内存上的浪费，我们可以使用寄生组合继承来进行优化。

### 寄生组合继承

寄生组合继承在属性的继承上还是与组合继承一致，不同点在于将子类的`prototype`使用`Object.create()`方法来实现，`Object.create() `方法的第一个参数是新建对象的原型对象，我们将其传入父类的`prototype`，第二个参数是新建对象的可枚举属性，我们传入`constructor`，将构造函数设为子类，这样就既解决了无用的父属性问题，还能正确的找到子类的构造函数。

### Class 继承

到了`ES6`，我们有了 class 语法糖，可以使用 `extends` 关键字来实现继承，在子类的构造函数中使用`super`来继承父类的属性，当然，`class`的本质还是函数。

## 模块化

模块化的好处在于解决了命名冲突的问题，其次它提高了代码的复用性和可维护性。

其实在早期的时候是使用立即执行函数来解决命名冲突的问题，后面又有了` AMD/CMD` 规范来进行模块化。

然后现在我们在 node 中一般使用`CommonJS`规范，使用`require`来进行导入，使用`module.exports`来进行导出。

在前端工程开发中使用的`ES Module`的模块化方案，使用`import` 进行导入，使用`export` 和`export default`来进行导出。

`CommonJS`和`ES Module`的区别在于：

- `CommonJS`支持动态导入，也就是在路径中可以写变量，ES Module 则不支持，不过目前也正在提案中。
- `CommonJS`是同步导入，而`ES Module`则是异步，这主要是因为他们使用的环境不同，一个用于服务器，一个用于浏览器。
- `CommonJS`导出是值拷贝，就算导出的值变了，导入的值也不会，除非重新导入，而`ES Module`则采用的实时绑定的方式，导入导出指向是同一个内存地址，导入的值是会随着导出的值变化的。

## 描述一下 this

`this`指向最后调用函数的那个对象，是函数运行时内部自动生成的一个内部对象，只能在函数内部使用。

函数内的 this 是在函数调用时确定的，指向最后调用函数那个对象。

## 进程与线程

本质上来说，两个名词都 CPU 工作时间片的一个描述。进程描述了 CPU 在运行指令及加载和保存上下文所需时间，放在应用上来说就代表了一个程序。线程是进程中的更小单位，描述了一段指令所需的时间。

举个例子来说，我们在浏览器里打开了一个 tab 网页的时候，就相当于起了一个进程，然后这个进程中又有很多线程，比如`js`引擎线程，渲染线程，`Http`请求线程等等，当发起一个请求时，就是就相当于创建了一个线程，当请求结束后，这个线程就会被摧毁。

## 原型与原型链

## bind、call、apply 区别

这三个方法都是为了改变函数的this指向，

前两者的区别就是call和apply的传参方式不一样，第一个参数都一样，剩余的参数，call接受的是一个参数列表，apply只接受一个参数数组，bind则会返回一个函数，像我们之前的react类组件中，经常会用bind去绑定当前组件的this

## 箭头函数与普通函数（function）的区别是什么？构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么？

箭头函数是普通函数的简写，可以更优雅的定义一个函数，和普通函数相比，有以下几点差异：

1. 函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象。

2. 不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

3. 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。

4. 不可以使用 new 命令，因为：
    没有自己的 this，无法调用 call，apply。
    没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 __proto__

## Event Loop 执行过程

1. 一开始整个脚本作为一个宏任务执行
2. 执行过程中同步代码直接执行，宏任务进入宏任务队列，微任务进入微任务队列
3. 当宏任务执行完出队后，检测微任务列表，有则依次执行，直到执行全部执行完
4. 执行浏览器的`UI`线程的渲染工作
5. 检查是否有`web worker `任务，有则执行
6. 执行完本轮的宏任务，回到第二步，依次循环，直到宏任务和微任务队列都为空

微任务包括 `proces.nextTick` 、 `promise`、`MutationObserver`，其中 `process.nextTick` 为 Node 独有。

宏任务包括 `script` 、`setTimeout` 、`setInterval`、`setImmediate`、`I/O` 、`UI rendering`

## Promise

`Promise`主要是为了解决传统回调地狱的问题，它代表了一个异步操作的最终完成或者失败，它有`pending`、`fulfilled`、`rejected`三种状态，`pending`为初始状态，`fulfuilled`为操作成功完成，`rejected`为操作失败，它的`then`方法和`catch`、`finally`方法会返回一个新的`Promise`允许我们链式调用。

### then 和 catch 方法

- `Promise`的状态一旦经过改变就不能再改变了
- `.then`和`.catch`会返回一个新的`Promise`对象
- `catch`无论被链接到哪里，都能捕获上层未捕获的错误
- 在`Promise`中，返回一个任意的非`Promise`的值都会被包裹成`Promise`对象，如`return 2`就会被包裹成`return Promise.resolve(2)`
- `Promise`的`.then`或者`.catch`可以被调用多次，但如果`Promise`内部的状态一经改变，并且有了一个值，那么后续每次调用`.then`或`.catch`的时候都能直接拿到该值
- `.then`或者`.catch`中`retun`一个`error`对象并不会抛出错误，所以不会被后续的`.catch`捕获
- `.then`或者`.catch`不能返回`Promise`本身，否则会造成死循环
- `.then`或者`.catch`的参数期望是函数，传入非函数则会发生值穿透
- `.then`方法是能接受两个参数的，一个是处理成功的函数，一个是处理失败的函数
- `.finally`方法也是返回一个`Promise`对象，它在`Promise`结束的时候，无论是`resolved`还是`rejected`都会执行里面的回调函数

## \*函数

## async await 函数

## 节流与防抖

### 节流

节流的核心思想就是如果在定时器的时间范围内再次触发，则不予理睬，等当前定时器完成，才能启动下一个定时器任务。这就好比公交车，10分钟一趟，中间有多少人在站台等待不管，10分钟一到，立马发车。

```javascript
function throttle(fn, interval) {
  let flag = true;
  return function(...args) {
    let context = this;
    if (!flag) return;
    flag = false;
    setTimeout(() => {
      fn.apply(context, args);
      flag = true;
    }, interval);
  };
};
```

### 防抖

防抖的核心思想就是每次事件的触发则删除原来的定时器，建立新的定时器。类似于游戏里的回城功能，你反复触发回城也只认你最后一次回城，只从最后一次触发算。

```javascript
function debounce(fn, delay) {
  let timer = null;
  return function (...args) {
    let context = this;
    if(timer) clearTimeout(timer);
    timer = setTimeout(function() {
      fn.apply(context, args);
    }, delay);
  }
};
```



## 浏览器从 url 输入到呈现的过程

1. 进行地址解析，解析出字符串地址中的主机、域名、端口号、参数等
2. 根据解析出来的域名进行DNS解析
3. 根据查询到的ip地址寻找目标服务器

   1. 与服务器进行连接

   2. 进入服务器、寻找对应的请求
4.	浏览器接收到响应码开始处理
5. 浏览器开始渲染dom，下载css、图片等一些资源，直到这次请求完成

## setTimeout、Promise、Async/Await 的区别

## webpack 常用 loader 和 plugin

1. loader： css-loader 、less-loader、url-loader、image-loader、file-loader
2. plugin：ignore-plugin、html-webpack-plugin、clean-webpack-plugin

## webpack 中 loader 和 plugin 有什么区别

loader，它是一个转换器，将A文件进行编译成B文件，比如：将A.less转换为A.css，单纯的文件转换过程。

plugin是一个扩展器，它丰富了webpack本身，针对是loader结束后，webpack打包的整个过程，它并不直接操作文件，而是基于事件机制工作，会监听webpack打包过程中的某些节点，执行广泛的任务

## 简单说说webpack的构建流程

1. 初始化：启动构建，读取与合并配置参数，加载插件，实例化编译器
2. 编译过程：从入口的Entry出发，针对每个模块串行调用对应的loader去翻译文件内容，再找到该模块依赖的模块，递归地调用编译处理
3. 输出过程：将编译后的模块组合成chunk，将chunk转换成文件，输出到文件系统

## http

## React / React fiber

主流浏览器的刷新是60Hz，即1s/60Hz，16.6ms浏览器刷新一次，在这16.6ms中，浏览器需要完成JS脚本执行 ---> 样式布局  ---> 样式绘制工作，而浏览器的GUI渲染线程与JS线程是互斥的，在React v16之前的版本，虚拟dom的diff操作都是同步完成的，这就导致一个问题，如果有大量的DOM操作，diff操作过长，也就是JS脚本执行过长，就会造成页面的交互卡顿，掉帧。

为了解决这个问题，React将 diff 操作变成可中断的，只有当浏览器空闲时再做 diff。避免 diff 更新长时间占据浏览器线程。既然我们以浏览器是否有剩余时间作为任务中断的标准，那我们就需要一种机制，当浏览器有剩余时间的时候通知我们，其实部分浏览器已经实现了这个API，也就是requestIdelCallback。

但是由于兼容性和触发频率等问题，React并没有用，而是自己实现了**Scheduler**（调度器），在之前的版本中，React已经实现了Reconciler（协调器）与Renderer（渲染器），协调器负责diff算法，找出变化的组件，渲染器负责把变化的组件渲染到页面上，现在加上调度器，调度器接受到更新后，会先判断有没有更高优先级的更新，没有就会把更新交给协调器，协调器再为此次需要更新虚拟DOM打上增删改查的标记，而这个过程，可能会由于有更高优先级的更新，或当前帧没有剩余时间而中断。而这个过程不会更新页面上的DOM，用户也就看见更新不完成的DOM。

由于采用了上述的机制来做异步可中断更新，之前的用于递归的虚拟DOM就不能满足需要，React就是实现了一种类似链表的数据结构，也就是React fiber ，将原来的递归diff变成了一直可以next的遍历diff，这样就方便做中断和恢复了。

## 如何在 root 外，生成 react 元素 / 将 react 元素插入 body

## 写 React 项目时为什么要在列表组件中写 key，其作用是什么？

## React v16生命周期

其实现在v16版本已经舍弃了很多如componentWillMount、componentWillReceiveProps等一些生命周期，也加入了一些新的，我就说说现在主要用的：

1. shouldComponentUpdate，这个是判断是否需求更新组件，多用于组件的性能优化

2. componentDidMount 组件挂载后使用，可以在这里进行请求或者订阅

3. componentWillUnmount 组件即将销毁，可以在此处移除订阅，定时器等等

4. render 渲染组件函数

当然现在 hooks 出来 多用useEffect来模拟生命周期函数了

```javascript
class ExampleComponent extends React.Component {
  // 用于初始化 state
  constructor() {}
  // 用于替换 `componentWillReceiveProps` ，该函数会在初始化和 `update` 时被调用
  // 因为该函数是静态函数，所以取不到 `this`
  // 如果需要对比 `prevProps` 需要单独在 `state` 中维护
  static getDerivedStateFromProps(nextProps, prevState) {}
  // 判断是否需要更新组件，多用于组件性能优化
  shouldComponentUpdate(nextProps, nextState) {}
  // 组件挂载后调用
  // 可以在该函数中进行请求或者订阅
  componentDidMount() {}
  // 用于获得最新的 DOM 数据
  getSnapshotBeforeUpdate() {}
  // 组件即将销毁
  // 可以在此处移除订阅，定时器等等
  componentWillUnmount() {}
  // 组件销毁后调用
  componentDidUnMount() {}
  // 组件更新后调用
  componentDidUpdate() {}
  // 渲染组件函数
  render() {}
  // 以下函数不建议使用
  UNSAFE_componentWillMount() {}
  UNSAFE_componentWillUpdate(nextProps, nextState) {}
  UNSAFE_componentWillReceiveProps(nextProps) {}
}
```



## 为什么虚拟 dom 会提高性能?

虚拟 dom 相当于在 JS 和真实 dom 中间加了一个缓存，利用 diff 算法避免了没有必要的 dom 操作，从而提高性能。

## React 组件间有那些通信方式?

### 父组件向子组件通信

1.  通过 props 传递

### 子组件向父组件通信

2.  主动调用通过 props 传过来的方法，并将想要传递的信息，作为参数，传递到父组件的作用域中

### 跨层级通信

1.  使用 react 自带的 Context 进行通信，createContext 创建上下文， useContext 使用上下文。
2.  使用 Redux/dva 或者 Mobx 等状态管理库

## React 父组件如何调用子组件中的方法？

1.  如果是在方法组件中调用子组件（>= react@16.8），可以使用 useRef 和 useImperativeHandle:
2.  如果是在类组件中调用子组件（>= react@16.4），可以使用 createRef

## React 有哪些优化性能的手段?

### 类组件中的优化手段

1.  使用纯组件 PureComponent 作为基类。
2.  使用 React.memo 高阶函数包装组件。
3.  使用 shouldComponentUpdate 生命周期函数来自定义渲染逻辑。

### 方法组件中的优化手段

1.  使用 useMemo。
2.  使用 useCallBack。

### 其他方式

1.  在列表需要频繁变动时，使用唯一 id 作为 key，而不是数组下标。
2.  必要时通过改变 CSS 样式隐藏显示组件，而不是通过条件判断显示隐藏组件。
3.  使用 Suspense 和 lazy 进行懒加载

## react diff 算法

## react setState是同步还是异步

1. 在react合成事件中是异步
2. 在钩子函数中是异步 两次调用会合并只触发一次调用
3. 在原生事件中是同步 addEventListener
4. 在setTimeout/setInterval 是同步

## 分析以下代码输出

```javascript
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2() {
  console.log('async2');
}
console.log('script start');
setTimeout(function () {
  console.log('setTimeout');
}, 0);
async1();
new Promise(function (resolve) {
  console.log('promise1');
  resolve();
}).then(function () {
  console.log('promise2');
});
console.log('script end');
```

'script start'
'async1 start'
'async2'
'promise1'
'script end'
'async1 end'
'promise2'
'setTimeout'

### 本题重点

#### Promise 和 async 中的立即执行
我们知道 Promise 中的异步体现在 then 和 catch 中，所以写在 Promise 中的代码是被当做同步任务立即执行的。而在 async/await 中，在出现 await 出现之前，其中的代码也是立即执行的。那么出现了 await 时候发生了什么呢？

#### await 做了什么
从字面意思上看 await 就是等待，await 等待的是一个表达式，这个表达式的返回值可以是一个 promise 对象也可以是其他值。

很多人以为 await 会一直等待之后的表达式执行完之后才会继续执行后面的代码，实际上 await 是一个让出线程的标志。await 后面的表达式会先执行一遍，将 await 后面的代码加入到 microtask 中，然后就会跳出整个 async 函数来执行后面的代码。

由于因为 async await 本身就是 promise+generator 的语法糖。所以 await 后面的代码是 microtask。所以对于本题中的

```javascript
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
```

等价于

```javascript
async function async1() {
  console.log('async1 start');
  Promise.resolve(async2()).then(() => {
    console.log('async1 end');
  });
}
```

## 冒泡排序

冒泡排序的原理如下，从第一个元素开始，把当前元素和下一个索引元素进行比较。如果当前元素大，那么就交换位置，重复操作直到比较到最后一个元素，那么此时最后一个元素就是该数组中最大的数。下一轮重复以上操作，但是此时最后一个元素已经是最大数了，所以不需要再比较最后一个元素，只需要比较到 `length - 1` 的位置。

## 快排

快排的原理如下。随机选取一个数组中的值作为基准值，从左至右取值与基准值对比大小。比基准值小的放数组左边，大的放右边，对比完成后将基准值和第一个比基准值大的值交换位置。然后将数组以基准值的位置分为两部分，继续递归以上操作。