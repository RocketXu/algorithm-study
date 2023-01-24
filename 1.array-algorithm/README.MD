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

## 二、双指针(滑动窗口)
### 2.1 同向双指针
>通过两个指针同时指向头节点或者尾节点，然后往一个方向去迭代遍历

### 2.2 不同向双指针
>通过两个指针一个指向头部一个指向尾部，然后按照条件共同向中间遍历

### 2.3 对于排完序之后的双指针有一个使用的小技巧
>以升序为例子：当目标值>两个指针相加时的和，那么就右指针向左移动；反之左指针向右移动


## 三、排序
>常见的几种排序算法还是需要总结的<font color="red">待总结</font>


## 四、子数组
### 4.1 滑动窗口
使用滑动窗口的解读
1. 滑动窗口其实和<font color="red">双指针</font>有异曲同工之妙
   1. 使用两个指针来控制有效窗口内的值，然后根据题意来判断条件
   2. 当快指针到**符合条件**对应的位置时，让慢指针不断的**靠近快指针**来期望获得最优解（这个过程就是缩小滑动窗口的过程）
![](./img/2023-01-02-15-42-23.png)
2. 滑动窗口模板：以[leetCode209.长度最小的子数组](./problem/leetCode209.长度最小的子数组.md)为例子，看好<font color="red">for/while</font>两个循环的意义
```java
class Solution {
    /**
        滑动窗口，变相的双指针玩法
     */
    public int minSubArrayLen(int target, int[] nums) {
        // 答案值
        int ans = Integer.MAX_VALUE;
        // 左边界
        int left = 0;
        // 总和
        int sum = 0;
        // 重点一：使用for循环控制右边界【快指针】
        for(int i = 0; i <= nums.length- 1; i++){
            sum += nums[i];
            // 重点二：while 控制左边界，不断的来试探最优解法（题意满足大于等于）【慢指针】
            while(left <= i && sum >= target){
                // 结果值取最小值
                ans = Math.min(ans, i - left + 1);
                // 左指针过来就是减去总和
                sum -= nums[left];
                left ++;
            }
        }
        return ans == Integer.MAX_VALUE ? 0:ans;
    }
}
```


### 4.2 前缀和

>这其实是一道极为简单的数学问题，就是【1，2，3】
>这里的总和 = 6 就是等价于（1+2）+3=6【这里确实很傻，但是（1+2）就是称为前缀和】 

这里有一个比较好的题目就是[leetCode560.和为k的子数组](sub-array/problem/leetCode325.%20和等于%20k%20的最长子数组长度.md)

- 前缀和模板如下（主要还是通过map来缓存对应值）
```java
// val-出现的次数
Map<Integer,Integer> preSumToCountMap = new HashMap<>();
// 有的时候原始数组前面就是0，所以一开始将前缀数组进行赋值0，出现次数1次
preSumToCountMap.put(0, 1);
for(int i = 0; i <= nums.length - 1; i++){
            preSum += nums[i];
            // 相减的问题
            if(preSumToCountMap.containsKey(preSum- k)){
                Integer count = preSumToCountMap.get(preSum- k);
                ans = ans + count;
            }
            preSumToCountMap.put(preSum, preSumToCountMap.getOrDefault(preSum,0) + 1);
}
```

