# 1.题目描述：

给定一个整数数组nums,找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和；

![img](https://img-blog.csdnimg.cn/20200528175852903.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 2.来源：

https://leetcode-cn.com/problems/maximum-subarray/

# 3.编吧：

## 动态规划

**核心思想**：若当前元素之前的和小于0(presum<0)，则丢弃当前元素之前的数列；

**步骤**：初始值:maxsum = nums[0] = -2;presum = 0

（1）num = -2;

presum = max(presum+num,num) = max(0-2,-2) = -2;

maxsum = max(maxsum,presum) = max(-2,-2) = -2;

（此时子数组从第一个元素-2开始）

（2）num = 1;

presum = max(presum+num,num) = max(-2+1,1) = 1;

maxsum = max(maxsum,presum) = max(-2,1) = 1;

(由于上一步骤计算出的presum<0;所以丢弃前面的数列，子数组从第二个元素1开始)

（3）num = -3,

presum = max(presum+num,num) = max(1-3,-3) = -2;

maxsum = max(maxsum,presum) = max(1,-2) = 1;

（4）num = 4,

presum = max(presum+num,num) = max(-2+4，4) = 4;

maxsum = max(maxsum,presum) = max(1,2) = 4;

(由于上一步骤计算出的presum<0;所以丢弃前面的数列，子数组从第四个元素4开始)

（5）num = -1;

presum = max(presum+num,num) = max(4-1，-1) = 3;

maxsum = max(maxsum,presum) = max(4，3) = 4;

（6）num = 2;

presum = max(presum+num,num) = max(3+2，2) = 5;

maxsum = max(maxsum,presum) = max(4,5) = 5;

（7）num = 1;

presum = max(presum+num,num) = max(5+1，1) = 6;

maxsum = max(maxsum,presum) = max(5,6) = 6;

（8）num = -5;

presum = max(presum+num,num) = max(6-5,-5) = 1;

maxsum = max(maxsum,presum) = max(6,1) = 6;

（9）num = 4;

presum = max(presum+num,num) = max(1+4,4) = 5;

maxsum = max(maxsum,presum) = max(6,5) = 6;

总结：从第（7）步骤开始max的值始终为6；并且子数组从第四个元素4开始，到第七个元素1结束，即数组[4,-1,2,1]为nums数组中具有最大和的连续子数组；

# 4.Code Show

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = nums[0];
        int before = 0;
        for(int num:nums){
            before = Math.max(before+num,num);
            max = Math.max(max,before);
        }
        return max;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 5.复杂度分析

- 时间复杂度：O(n)，其中n为nums数组的长度，只需要遍历一遍数组即可求得答案；

- 空间复杂度：O(1)，只需要常数空间存放若干变量；

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)