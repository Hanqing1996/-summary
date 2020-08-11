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
#### No.7 ES5/ES6 的继承除了写法以外还有什么区别？

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


#### ES5 是怎么实现继承的？
> 构造函数 A 与 构造函数 B 并没有继承关系，即构造函数 B 没有继承构造函数 A 上面的属性
```
function A() {
  this.a = 'hello';
}

function B() {
  A.call(this);
  this.b = 'world';
}

B.prototype.__proto__ =A.prototype

let b = new B();
```
[![aL2yZD.png](https://s1.ax1x.com/2020/08/11/aL2yZD.png)](https://imgchr.com/i/aL2yZD)

#### ES6











