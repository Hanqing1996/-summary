#### No.6【TODO】 请分别用深度优先思想和广度优先思想实现一个拷贝函数？


#### No.14 如何实现一个 new？
参考[这里](https://github.com/Hanqing1996/JavaScript-advance/blob/master/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/README.md#%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA-new)


---
#### No.11 算法手写题                               
                                            
已知如下数组：                                     
```                                         
var arr = [ [1, 2, 2], [3, 4, 5, 5], [6, 7, 
```                                         
编写一个程序将数组扁平化去并除其中重复部分数据，最终得到一个升序且不重复的数组     

* [数组的 toString 方法将每个数组元素转换成一个字符串，并在元素之间添加逗号后合并成结果字符串](https://github.com/Hanqing1996/JavaScript-advance/tree/master/%E5%85%B6%E5%AE%831#%E5%AF%B9%E8%B1%A1%E7%9A%84-tostring-%E6%96%B9%E6%B3%95)
```
var arr = [ [1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10]

Array.from(new Set(arr.toString().split(','))).sort((a,b)=>{ return a-b}).map(Number) 
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```
#### No.31 改造下面的代码，使之输出0 - 9，写出你能想到的所有解法。                             
```javascript                                                      
for (var i = 0; i< 10; i++){                                       
	setTimeout(() => {                                             
		console.log(i);                                            
    }, 1000)                                                       
}                                                                  
```   
* 方法1：let,参考[这里](https://github.com/Hanqing1996/JavaScript-advance/tree/master/%E5%85%B6%E5%AE%831#%E9%9D%A2%E8%AF%95%E4%B8%8B%E9%9D%A2%E4%BB%A3%E7%A0%81%E7%9A%84%E8%BE%93%E5%87%BA%E6%98%AF%E4%BB%80%E4%B9%88%E4%B8%BA%E4%BB%80%E4%B9%88)
```javascript
for (let i = 0; i< 10; i++){  
	setTimeout(() => {        
		console.log(i);       
    }, 1000)                  
}       
```        
* 方法2：利用 setTimeout 函数的第三个参数，会作为回调函数的第一个参数传入     
```javascript
for (var i = 0; i < 10; i++) {

    // i 作为 setTimeout 的第三个参数传入，这样实际上就在 setTimeout 内部声明了10个不同的变量，10个回调函数可以分别访问它们。
    setTimeout(i => {
      console.log(i);
    }, 1000, i)
  }
```                                        
---
#### No.36 使用迭代的方式实现 flatten 函数
[参考](https://github.com/Hanqing1996/JavaScript-advance/blob/master/%E6%95%B0%E7%BB%84%E6%93%8D%E4%BD%9C/README.md#%E6%A8%A1%E6%8B%9F%E5%AE%9E%E7%8E%B0-flat-%E5%87%BD%E6%95%B0)
---
#### No.38 下面代码中 a 在什么情况下会打印 1？
> 这题考察的应该是类型的隐式转换
 ```javascript
 if(a == 1 && a == 2 && a == 3){
    console.log(1);               
 }                  
 ```
* 方法1:
```javascript
let a = [1,2,3];
a.valueOf = a.shift;
// 数组和数字比较，会调用 ToPrimitive(数组)，继而调用 valueOf(数组)
if( a == 1 && a == 2 && a == 3 ) {
  console.log(1);
}
```
* 方法2:同上理
```javascript
let a = {num:0};
a.valueOf = function(){
  return ++a.num
}
if(a == 1 && a == 2 && a == 3){
	console.log(1);
}
```
---
#### No.42 实现一个 sleep 函数
比如 sleep(1000) 意味着等待1000毫秒，可从 Promise、Generator、Async/Await 等角度实现