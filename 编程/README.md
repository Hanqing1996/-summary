#### No.6【TODO】 请分别用深度优先思想和广度优先思想实现一个拷贝函数？


#### No.14 如何实现一个 new？
参考[这里](https://github.com/Hanqing1996/JavaScript-advance/blob/master/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/README.md#%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA-new)



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