### 剑指 Offer 66. 构建乘积数组


##### 1.题目
给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。


##### 2.示例
示例1:
```
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

##### 3.思路
- 1.第一次循环得到每一个数前面几个数字的乘积；
- 2.第二次循环得到后面部分的乘积，然后与前面的之前乘积相乘。

##### 4.代码
```javascript
/**
 * @param {number[]} a
 * @return {number[]}
 */
var constructArr = function(a) {
    let res = [], temp = 1
    for(let i = 0; i < a.length; i++) {
        res[i]= temp
        temp = temp * a[i]
    }
    temp = 1
    for(let i = a.length - 1; i >= 0; i--) {
        res[i] *= temp
        temp = temp * a[i]
            
    }
    return res
};
```