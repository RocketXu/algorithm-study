# 数组题型总结
## 一、二分查找
> 二分查询经典模板：我们使用的不能过于片面有的时候我们要用左边右闭的方法进行解题，但是有的时候我们也需要使用别的模板进行解题【这一切的前提都是排好序的】
> 如 [leetcode34.在排序数组中查找元素的第一个和最后一个位置](./binary-search/problem/leetcode34.%20在排序数组中查找元素的第一个和最后一个位置.md)



- 使用左闭右闭的方式【意思就是一开始指针都正好指向头和尾，这个时候循环的条件就是<font color="red"><=</font>】
  

```java
int left = 0；
int right = num[].length - 1;
// 终止条件是当左指针跑到右边结束
while(left <= right){
    // 这种方式可能会溢出，使用下面一种方式
    // int mid = (left + right) / 2;
    int mid = left + (right - left) / 2;
    if(num[mid] > target){
        // 在左边
        right = mid - 1;
    }else if(num[mid] < target){
        // 在右边
        left = mid + 1;
    }else{
        // 找到目标值
        return mid;
    }   
}
```

## 二、指针



## 三、排序


## 四、子数组



