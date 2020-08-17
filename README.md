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
* No.76 输出以下代码运行结果
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
* No.129 输出以下代码执行结果
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
* No.130 第 130 题：输出以下代码执行结果
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