## 面向对象

### 首先来说面向对象的三大特性

- 封装

  就是我们把操作数据的具体内容隐藏起来，只暴露对外的接口。比如生活中开车，一脚油门，一脚刹车，我们不用操心脚踩下去车内部做了什么，我们只需来操作油门和刹车到达我们前进和停止的功能即可。

- 继承

  子类继承父类，子类也会具有更具体的特性。

- 多态

  还是源于继承，但是子类和子类之间又会有多样不同的表现，比如Cat类和Dog类都继承至Animal类，他们有相同的特性，比如都是哺乳动物，4条腿，一个脑袋，还会具有一个叫的方法，但是他们叫的声音就不一样了，当然，猫与狗也还有其他不同的特性。

### 其次来说说js里的面向对象

- ES5

  在ES5时期，js原生对于面向对象编程的支持还是比较弱的，我们通常会使用工厂函数来进行，然后使用 new 关键字来实例化。

- ES6

  到了ES6就不一样了，它为我们提供了 class 关键字，使用class可以来生成一个类，class中有constructor也就是构造函数，在构造函数里我们可以生成类的属性，如this.name、this.age，然后使用 extends 关键字实现继承，使用static修饰符修饰方法为静态方法，不需要实例化，直接使用类就可调用。

- ES7

  在ES6中属性还需要通过构造函数 this.xxx 来定义，在ES7中直接定义，如 age = 123，同时也提案了通过static 修饰属性为静态属性，同样直接使用类就可以调用。

- TypeScript

  最后来说说TS里面的类，出了上述之外，多了 public 、private、和 protected 三种修饰符，public修饰的属性和方法都是公有的，在任何地方都可被访问到，private修饰的是私有的，不能在声明它的类的外部访问，protected 修饰的是受保护的，它和private 类似，区别是它在子类中是可以访问的。

  

## 继承

 在ES5时期，我们通常通过原型来实现继承，常用的方式有组合继承和寄生组合继承。

### 组合继承

组合继承就是将子类的 prototype 指向父类的实例，同时在子类内部使用父类 .call 绑定当前子类的this实现对父类属性的继承，这种继承方式的优点在于可以使用构造函数进行传参，不会与父类共享属性，还可以复用父类的函数，但是同时也存在一个缺点就是继承父类时调用了父类的构造函数，导致子类的原型上多了不需要的父类属性，造成了内存上的浪费，我们可以使用寄生组合继承来进行优化。

### 寄生组合继承

寄生组合继承在属性的继承上还是与组合继承一致，不同点在于将子类的prototype使用Object.create()方法来实现，Object.create() 方法的第一个参数是新建对象的原型对象，我们将其传入父类的prototype，第二个参数是新建对象的可枚举属性，我们传入 constructor ，将构造函数设为子类，这样就既解决了无用的父属性问题，还能正确的找到子类的构造函数。

### Class继承

到了ES6，我们有了class语法糖，可以使用 extends 关键字来实现继承，在子类的构造函数中使用super来继承父类的属性，当然，class的本质还是函数。



