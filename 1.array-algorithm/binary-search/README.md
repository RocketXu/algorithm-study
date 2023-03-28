# 二分查找的原理以及实现
二分查找的实现原理非常简单，首先要有一个有序的列表。但是如果没有，则该怎么办？可以使用排序算法进行排序。以升序为例子：然后进行折半查找，找到中间值，然后目标值大于中间值就是在后半段；目标值小于中间值就是在前半段。
`在做题目时也非常容易识别：找就是对于找值得相关题目`


# 经典列题

1. [二分查找基础](./problem/leetcode704：二分查找.md) =》 经典二分
2. [搜索插入位置](./problem/leetcode35.%20搜索插入位置.md) =》 二分小变式，找规律
3. [排序数组中查找元素的第一个和最后一个位置](./problem/leetcode34.%20在排序数组中查找元素的第一个和最后一个位置.md) =》 二分找左右边界
4. [平方根](./problem/leetcode69.%20x%20的平方根.md) =》二分查找




# 总结
1. 二分查找模板

>查找目标不要慌，二分查找会来帮；
左闭右闭加while，循环条件可等于；
优化速度可多移，题目不同变动移动方式。

```java
int left = 0;
int right = nums.length - 1;
while(left <= right){
    int mid = left + (right - left) / 2;
    if(nums[mid] < target){
        // 可以优化多移动一位
        left = mid + 1;
    }
    if(nums[mid] > target){
        // 可以优化多移动一位
        left = mid - 1;
    }
    if(nums[mid] == target){
        return mid;
    }
}
// 没找到
return -1;

```