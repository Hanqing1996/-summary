## JS基础

#### [No2：['1', '2', '3'].map(parseInt) what & why ?](https://muyiy.cn/question/js/2.html)
* [将字符串数组中的元素转为Number型，为什么不能直接用ParseInt](https://github.com/Hanqing1996/JavaScript-advance/tree/master/%E5%85%B6%E5%AE%832#%E5%B0%86%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E5%85%83%E7%B4%A0%E8%BD%AC%E4%B8%BAnumber%E5%9E%8B%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E8%83%BD%E7%9B%B4%E6%8E%A5%E7%94%A8parseint)
* [map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
```
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
 // Return element for new_array 
}[, thisArg])
```
* [parseInt](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
```
parseInt(string, radix);
// 返回从给定的字符串中解析出的一个整数。
```
* 注意点
radix 的值域为[2,36]。<strong>在radix为 undefined，或者radix为 0 或者没有指定的情况下</strong>，JavaScript 作如下处理（以下的基数指的就是进制）：
1. 如果字符串 string 以"0x"或者"0X"开头, 则基数是16 (16进制).
2. 如果字符串 string 以"0"开头, 基数是8（八进制）或者10（十进制），那么具体是哪个基数由实现环境决定。ECMAScript 5 规定使用10，但是并不是所有的浏览器都遵循这个规定。因此，永远都要明确给出radix参数的值。
3. 如果字符串 string 以其它任何值开头，则基数是10 (十进制)。
* parseInt('14', 2) 为什么是1
parseInt从参数的第一个字符开始解析，遇到无法解析的则忽略，'14'中的1在二进制中可以解析，而4则无法解析，因)此parseInt('14',2) 相当于parseInt('1', 2)，计算出结果是1
```
parseInt('1', 0) //radix为0时，且string参数不以“0x”和“0”开头时，按照10为基数处理。这个时候返回1
parseInt('2', 1) //基数为1（1进制）表示的数中，最大值小于2，所以无法解析，返回NaN
parseInt('3', 2) //基数为2（2进制）表示的数中，最大值小于3，所以无法解析，返回NaN
```
* 变形
```
let unary = fn => val => fn(val)
let parse = unary(parseInt)
console.log(['1.1', '2', '0.3'].map(parse))
````
等价于
```
['1.1', '2', '0.3'].map((currentValue)=>parseInt(currentValue))

parseInt('1.1') // 1：parseInt 解析"1",忽略".1",十进制下的1是1
parseInt('2') // 2：2的十进制
parseInt('0.3') // 0: parseInt 解析"1",忽略".3",十进制下的0是0
```
---
#### No.4 介绍下 Set、Map、WeakSet 和 WeakMap 的区别？

#### Set
* Same-value-zero equality
> 向 Set 加入值的时候，不会发生类型转换，所以5和"5"是两个不同的值。Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于精确相等运算符（===），主要的区别是Same-value-zero equality 认为NaN等于自身，而精确相等运算符认为NaN不等于自身。
```
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
set // Set {NaN}
```
* 将 Set 结构转为数组
> Array.from 方法可以将 Set 结构转为数组
```
const items = new Set([1, 2, 3, 2])
const array = Array.from(items)
console.log(array)	// [1, 2, 3]
// 或
const arr = [...items]
console.log(arr)	// [1, 2, 3]
```
* 用 set 实现 交集（Intersect）、并集（Union）、差集（Difference）
```
let set1 = new Set([1, 2, 3])
let set2 = new Set([4, 3, 2])

let intersect = new Set([...set1].filter(value => set2.has(value)))
let union = new Set([...set1, ...set2])
let difference = new Set([...set1].filter(value => !set2.has(value)))

console.log(intersect)	// Set {2, 3}
console.log(union)		// Set {1, 2, 3, 4}
console.log(difference)	// Set {1}
```
#### WeakSet
* WeakSet 与 Set 的区别：
> WeakSet 只能储存对象引用，不能存放值，而 Set 对象都可以
* weak
> meaning references to objects in a WeakSet are held weakly.WeakSet 对象中储存的对象值都是被弱引用的，即如果没有其他的变量或属性引用这个对象值，则这个对象将会被垃圾回收掉（不考虑该对象还存在于 WeakSet 中），所以，WeakSet 对象里有多少个成员元素，取决于垃圾回收机制有没有运行，运行前后成员个数可能不一致，遍历结束之后，有的成员可能取不到了（被垃圾回收了），WeakSet 对象是无法被遍历的（ES6 规定 WeakSet 不可遍历），也没有办法拿到它包含的所有元素

#### WeakMap
> The WeakMap object is a collection of key/value pairs in which the keys are weakly referenced. The keys must be objects and the values can be arbitrary values.键名必须是对象类型且为弱引用，键值可以是任意的
* WeakMap 的 key 是不可枚举的。
---
#### No.7【TODO】 ES5/ES6 的继承除了写法以外还有什么区别？

#### 什么是原型
* 参考:
[JavaScript深入之从原型到原型链](https://github.com/mqyqingfeng/Blog/issues/2)
* 什么是原型
```
function Person() {}
var person = new Person();
```
Person.prototype 和 person.__proto__  访问的是同一个东西，我们将其称为：原型

![aL61KO.png](https://s1.ax1x.com/2020/08/11/aL61KO.png)
* 原型和原型之间的关系
> 原型也是一个对象，对象与对象之间的继承关系，应该用 _proto_来表示

![aLcRTH.png](https://s1.ax1x.com/2020/08/11/aLcRTH.png)
* constructor 的作用
> 由原型指向构造函数。
```
function Person() {}
console.log(Person === Person.prototype.constructor); // true
```
[![aL62in.png](https://s1.ax1x.com/2020/08/11/aL62in.png)](https://imgchr.com/i/aL62in)

---
#### No.26 介绍模块化发展历程
> 可从IIFE、AMD、CMD、CommonJS、UMD、webpack(require.ensure)、ES Module、<script type="module"> 这几个角度考虑。

* 参考：[ES6 系列之模块加载方案](https://github.com/mqyqingfeng/Blog/issues/108)

#### AMD
> AMD是RequireJS 在推广过程中对模块定义的规范化产出。
* AMD 是先执行模块代码，导出的对象不急用，CMD 是需要用到模块导出对象时才执行模块代码并导出对象
* 浏览器端一般采用 AMD 规范。

#### CMD
> CMD 其实就是 SeaJS 在推广过程中对模块定义的规范化产出。

#### AMD 与 CMD 的区别
1. CMD 推崇依赖就近，AMD 推崇依赖前置
* AMD
```
// require.js 例子中的 main.js
// 依赖必须一开始就写好
require(['./add', './square'], function(addModule, squareModule) {
    console.log(addModule.add(1, 1))
    console.log(squareModule.square(3))
});
```
* CMD
```
// sea.js 例子中的 main.js
define(function(require, exports, module) {
    var addModule = require('./add');
    console.log(addModule.add(1, 1))

    // 依赖可以就近书写
    var squareModule = require('./square');
    console.log(squareModule.square(3))
});
```

#### [CommonJS](https://github.com/Hanqing1996/node-notes#nodejs-%E7%9A%84%E6%A8%A1%E5%9D%97%E6%9C%BA%E5%88%B6)
> 是 Node.js 模块遵循的规范
* 与CMD一样，在需要用到模块的时候才去加载模块文件，加载完再接着执行。

#### CommonJS 与 AMD
> CommonJS 规范加载模块是同步的，也就是说，只有加载完成，才能执行后面的操作。

> AMD规范则是非同步加载模块，允许指定回调函数。

> 由于 Node.js 主要用于服务器编程，模块文件一般都已经存在于本地硬盘，所以加载起来比较快，不用考虑非同步加载的方式，所以 CommonJS 规范比较适用。

> 但是，如果是浏览器环境，要从服务器端加载模块，这时就必须采用非同步模式，因此浏览器端一般采用 AMD 规范。

#### ES6 新的模块加载方案
* 与AMD一样，先执行模块代码
* 优势
1. 死代码检测和排除（tree-shaking）：我们可以用静态分析工具检测出哪些模块没有被调用过。比如，在引入工具类库时，工程中往往只用到了其中一部分组件或接口，但有可能会将其代码完整地加载进来。未被调用到的模块代码永远不会被执行，也就成为了死代码。通过静态分析可以在打包时去掉这些未曾使用过的模块，以减小打包资源体积。
2. 模块变量类型检查：JavaScript属于动态类型语言，不会在代码执行前检查类型错误（比如对一个字符串类型的值进行函数调用）。ES6 Module的静态模块结构有助于确保模块之间传递的值或接口类型是正确的。
3. 编译器优化：在CommonJS等动态模块系统中，无论采用哪种方式，本质上导入的都是一个对象，而ES6 Module支持直接导入变量，减少了引用层级，程序效率更高。

#### ES6与Common.js
* 它们有两个重大差异。
1. CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
> 原因：CommonJS 模块输出的是值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。ES6 模块的运行机制与 CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令 import，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。换句话说，ES6 的 import 有点像 Unix 系统的“符号连接”，原始值变了，import 加载的值也会跟着变。因此，ES6 模块是动态引用，并且不会缓存值，模块里面的变量绑定其所在的模块。
2. CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
> 原因 CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。
---
#### No.27 全局作用域中，用 const 和 let 声明的变量不在 window 上，那到底在哪里？如何去获取？
---
#### No.33 下面的代码打印什么内容，为什么？
```
var b = 10;
(function b(){
    b = 20;
    console.log(b); 
})();
```
* 考点：在非匿名自执行函数中，函数变量为只读状态无法修改；
* 解析
```
var b = 10;
(function b() {
    // 内部作用域，会先去查找是有已有变量b的声明，有就直接赋值20，确实有了呀。发现了具名函数 function b(){}，拿此b做赋值；
    // IIFE的函数无法进行赋值（内部机制，非匿名自执行函数类似const定义的常量），所以无效。
    // （这里说的“内部机制”，想搞清楚，需要去查阅一些资料，弄明白IIFE在JS引擎的工作方式，堆栈存储IIFE的方式等）
    b = 20;
    console.log(b); // [Function b]
    console.log(window.b); // 10，不是20
})();
```
稍微修改下就不一样了
```
(function A() {
    console.log(A); // undefined
    var A = 1;
    console.log(window.A); // undefined
    console.log(A); // 1
}())
```
> var语句被hoist到函数顶端，函数内定义了变量A但是没有赋值，所以第一个log是undefined，因为有var，并没有向global添加属性，因此window.A也是undefined。
---
#### No.46 输出以下代码执行的结果并解释为什么
```
var obj = {
    '2': 3,
    '3': 4,
    'length': 2,
    'splice': Array.prototype.splice,
    'push': Array.prototype.push
}
obj.push(1)
obj.push(2)
console.log(obj)
```
答案
```
var obj = {
    '2': 3,
    '3': 4,
    'length': 2,
    'splice': Array.prototype.splice,
    'push': Array.prototype.push
}
obj.push(1)
obj.push(2)
console.log(obj)
```
* 解析:MDN 对 push 方法的描述
> push 方法具有通用性。该方法和 call() 或 apply() 一起使用时，可应用在类似数组的对象上。push 方法根据 length 属性来决定从哪里开始插入给定的值。如果 length 不能被转成一个数值，则插入的元素索引为 0，包括 length 不存在时。当 length 不存在时，将会创建它。

> 当调用该方法时，新的 length 属性值将被返回。
---
#### No.48 call 和 apply 的区别是什么，哪个性能更好一些?
* Function.prototype.apply和Function.prototype.call 的作用是一样的，区别在于传入参数的不同；
1. 第一个参数都是，指定函数体内this的指向；
2. 第二个参数开始不同，apply是传入带下标的集合，数组或者类数组，apply把它传给函数作为参数，call从第二个开始传入的参数是不固定的，都会传给函数作为参数。
> call比apply的性能要好，平常可以多用call, call传入参数的格式正是内部所需要的格式，
---
#### No.53 输出以下代码的执行结果并解释为什么
```
var a = {n: 1};
var b = a;
a.x = a = {n: 2};

console.log(a.x) 	
console.log(b.x)
```
* 答案
```
undefined
{ n: 2 }
```
* 解析
![dSAesO.png](https://s1.ax1x.com/2020/08/13/dSAesO.png)
---
#### No.58 箭头函数与普通函数（function）的区别是什么？构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么？
* 箭头函数是普通函数的简写，可以更优雅的定义一个函数，和普通函数相比，有以下几点差异：

1、函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象。

2、不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

3、不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。

4、不可以使用 new 命令，因为：

> 没有自己的 this，无法调用 call，apply。
> 没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 __proto__（见上面：原型）
* new 过程大致是这样的：
```
function newFunc(father, ...rest) {
  var result = {};
  result.__proto__ = father.prototype;
  var result2 = father.apply(result, rest); // father 为箭头函数时，无法绑定 this,所以 apply 失败
  if (
    (typeof result2 === 'object' || typeof result2 === 'function') &&
    result2 !== null
  ) {
    return result2;
  }
  return result;
}
```
