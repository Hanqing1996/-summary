#### No.9 Async/Await 如何通过同步的方式实现异步
参考 [这里](https://github.com/Hanqing1996/js-you-don-t-know#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%AF%B4-asyncawait-%E6%98%AF-generator-%E7%9A%84%E8%AF%AD%E6%B3%95%E7%B3%96)

#### No.10 异步笔试题，请写出下面代码的运行结果
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
#### No.64 模拟实现一个 Promise.finally
```
Promise.prototype.finally = function (callback) {
  let P = this.constructor; // 获取当前实例构造函数的引用
  return this.then(
    value  => P.resolve(callback()).then(() => value), // 我也不知道为什么这里不是 callback 
    reason => P.resolve(callback()).then(() => { throw reason })
  );
};
``` 
#### No.65 介绍下 Promise.all 使用、原理实现及错误处理
* 使用
```
const p=Promise.all(p1,p2,p3)
```
接受多个 Promise 实例作为参数，如果有某个参数 reject,则 p 的状态直接确定为 rejected,否则等到所有参数都 resolve,p 状态才确定为 resolved 
* 原理实现
```
var p1 =new Promise(function(resolve,reject){
    setTimeout(function(){
        resolve(1);
    },0)
});
var p2 = new Promise(function(resolve,reject){
        setTimeout(function(){
            resolve(2);
        },200)
 });
 var p3 = new Promise(function(resolve,reject){
        setTimeout(function(){
            try{
            console.log(XX.BBB);
            }
            catch(exp){
                resolve("error");
            }
        },100)
});
Promise.all([p1, p2, p3]).then(function (results) {
    console.log("success")
     console.log(results);
}).catch(function(r){
    console.log("err");
    console.log(r);
});
```
* 错误处理
如果作为 all 参数的 Promise 实例，自己定义了`catch`方法，那么它一旦被`rejected`，并不会触发`Promise.all()`的`catch`方法。
---
#### No.89 设计并实现 Promise.race()
注意 race 的特点，只要有一个参数的状态确定下来，调用 race 的实例状态就会确定下来，参考[这里](https://github.com/Hanqing1996/JavaScript-advance/blob/master/%E5%BC%82%E6%AD%A5/README.md#promiserace)
```
Promise._race = promises => new Promise((resolve, reject) => {
	promises.forEach(promise => {
		promise.then(resolve, reject)
	})
})
```






