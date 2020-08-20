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

```