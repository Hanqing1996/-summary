#### js基础
* No2：['1', '2', '3'].map(parseInt) what & why ?
* No.4 介绍下 Set、Map、WeakSet 和 WeakMap 的区别？
* No.7【TODO】 ES5/ES6 的继承除了写法以外还有什么区别？
* No.26 介绍模块化发展历程
* No.33 下面的代码打印什么内容，为什么？
```
var b = 10;
(function b(){
    b = 20;
    console.log(b); 
})();
```
* No.48 call 和 apply 的区别是什么，哪个性能更好一些?
* No.58 箭头函数与普通函数（function）的区别是什么？构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么？
* No.65 a.b.c.d 和 a['b']['c']['d']，哪个性能更高?
* No.66 ES6 代码转成 ES5 代码的实现思路是什么?
* No.72 为什么普通 for 循环的性能远远高于 forEach 的性能，请解释其中的原因。
* No.75 数组里面有10万个数据，取第一个元素和第10万个元素的时间相差多少
* ❌ No.76 输出以下代码运行结果
```
// example 1
var a={}, b='123', c=123;  
a[b]='b';
a[c]='c';  
console.log(a[b]);

---------------------
// example 2
var a={}, b=Symbol('123'), c=Symbol('123');  
a[b]='b';
a[c]='c';  
console.log(a[b]);

---------------------
// example 3
var a={}, b={key:'123'}, c={key:'456'};  
a[b]='b';
a[c]='c';  
console.log(a[b]);
```
* No.79 input 搜索如何防抖，如何处理中文输入
* No.83 var、let 和 const 区别的实现原理是什么?
* No.96 介绍下前端加密的常见场景和方法
* No.98 写出如下代码的打印结果
```
function changeObjProperty(o) {
    o.siteUrl = "http://www.baidu.com"
    o = new Object()
    o.siteUrl = "http://www.google.com"
  } 
  let webSite = new Object();
  changeObjProperty(webSite);
  console.log(webSite.siteUrl);
```
* No.100 请写出如下代码的打印结果
```
function Foo() {
Foo.a = function() {
console.log(1)
}
this.a = function() {
console.log(2)
}
}
Foo.prototype.a = function() {
console.log(3)
}
Foo.a = function() {
console.log(4)
}
Foo.a();
let obj = new Foo();
obj.a();
Foo.a();
```
* No.106 分别写出如下代码的返回值
```
String('11') == new String('11');
String('11') === new String('11');
```
* No.108 请写出如下代码的打印结果
```
var name = 'Tom';
(function() {
if (typeof name == 'undefined') {
  var name = 'Jack';
  console.log('Goodbye ' + name);
} else {
  console.log('Hello ' + name);
}
})();
```
* No.116 请写出如下代码的打印结果
```
1 + "1"

2 * "2"

[1, 2] + [2, 1]

"a" + + "b"
```
* ❌ No.129 输出以下代码执行结果
```
function wait() {
  return new Promise(resolve =>
    setTimeout(resolve, 10 * 1000)
  )
}

async function main() {
  const x = wait();
  const y = wait();
  const z = wait();
  await x;
  await y;
  await z;
  console.timeEnd();
}
main();
```
* ❌ No.130 第 130 题：输出以下代码执行结果
```
function wait() {
  return new Promise(resolve =>
    setTimeout(resolve, 10 * 1000)
  )
}

async function main() {
  console.time();
  await wait();
  await wait();
  await wait();
  console.timeEnd();
}
main();
```
---

#### 异步
* No.9 Async/Await 如何通过同步的方式实现异步？
* ❌ No.10 异步笔试题，请写出下面代码的运行结果
```
async function async1() {
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2() {
    console.log('async2');
}
console.log('script start');
setTimeout(function() {
    console.log('setTimeout');
}, 0)
async1();
new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    console.log('promise2');
});
console.log('script end');
```
* ❌ No.64 模拟实现一个 Promise.finally
* ❌ No.65 介绍下 Promise.all 使用、原理实现及错误处理
* ❌ No.89 设计并实现 Promise.race()
---
#### 编程
* ❌ No.6【TODO】 请分别用深度优先思想和广度优先思想实现一个拷贝函数？
* No.11 算法手写题

已知如下数组：
```
var arr = [ [1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10];
```
编写一个程序将数组扁平化去并除其中重复部分数据，最终得到一个升序且不重复的数组































#### 框架
* ❌ No.1 写 React / Vue 项目时为什么要在列表组件中写 key，其作用是什么？




```

a:1
b:123
c:'hi'

```



