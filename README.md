[No2：['1', '2', '3'].map(parseInt) what & why ?](# No2：['1', '2', '3'].map(parseInt) what & why ?)


# [No2：['1', '2', '3'].map(parseInt) what & why ?](https://muyiy.cn/question/js/2.html)
* [将字符串数组中的元素转为Number型，为什么不能直接用ParseInt](https://github.com/Hanqing1996/JavaScript-advance/tree/master/%E5%85%B6%E5%AE%832#%E5%B0%86%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E5%85%83%E7%B4%A0%E8%BD%AC%E4%B8%BAnumber%E5%9E%8B%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E8%83%BD%E7%9B%B4%E6%8E%A5%E7%94%A8parseint)
#### 注意点
```
parseInt(string, radix);
```
在radix为 undefined，或者radix为 0 或者没有指定的情况下，JavaScript 作如下处理（以下的基数指的就是进制）：
1. 如果字符串 string 以"0x"或者"0X"开头, 则基数是16 (16进制).
2. 如果字符串 string 以"0"开头, 基数是8（八进制）或者10（十进制），那么具体是哪个基数由实现环境决定。ECMAScript 5 规定使用10，但是并不是所有的浏览器都遵循这个规定。因此，永远都要明确给出radix参数的值。
3. 
