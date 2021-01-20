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

## Event Loop 执行过程

1. 一开始整个脚本作为一个宏任务执行
2. 执行过程中同步代码直接执行，宏任务进入宏任务队列，微任务进入微任务队列
3. 当宏任务执行完出队后，检测微任务列表，有则依次执行，直到执行全部执行完
4. 执行浏览器的`UI`线程的渲染工作
5. 检查是否有`web worker `任务，有则执行
6. 执行完本轮的宏任务，回到第二步，依次循环，知道宏任务和微任务队列都为空

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

## 浏览器从 url 输入到呈现的过程

## webpack 常用 loader 和 plugin

## webpack 中 loader 和 plugin 有什么区别

loader，它是一个转换器，将A文件进行编译成B文件，比如：将A.less转换为A.css，单纯的文件转换过程。

plugin是一个扩展器，它丰富了webpack本身，针对是loader结束后，webpack打包的整个过程，它并不直接操作文件，而是基于事件机制工作，会监听webpack打包过程中的某些节点，执行广泛的任务

## http

## react

## 如何在 root 外，生成 react 元素 / 将 react 元素插入 body

## 写 React 项目时为什么要在列表组件中写 key，其作用是什么？

## 什么是防抖和节流？有什么区别？如何实现？

## setTimeout、Promise、Async/Await 的区别

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

## react fiber

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


## 箭头函数与普通函数（function）的区别是什么？构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么？

箭头函数是普通函数的简写，可以更优雅的定义一个函数，和普通函数相比，有以下几点差异：

1. 函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象。

2. 不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

3. 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。

4. 不可以使用 new 命令，因为：
    没有自己的 this，无法调用 call，apply。
    没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 __proto__