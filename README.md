# CP-tricks
刷题心得

# 刷题技巧总结

## 前缀和和后缀来解决一些有“除了某个点之外的所有”的性质的问题

1. [LeetCode 238. Product of Array Except Self.](https://www.acwing.com/solution/content/288/)

使用前缀积和后缀积。

2. Google Kickstart. [看狗](https://www.acwing.com/problem/content/836/)
枚举最后一次的操作，然后使用前缀和后缀来获得除了这个选择之外的最小值

## 动态规划结合状态压缩，状态必须存在拓扑序列，不能环形依赖. 
[拯救大兵瑞恩](https://www.acwing.com/solution/content/14096/)

## 各类子序列问题
[子序列问题](https://www.acwing.com/blog/content/823/)

子序列问题，而如果么有要求连续，那么优先考虑sort。[1498. Number of Subsequences That Satisfy the Given Sum Condition](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/)

## 对于二维矩阵求一个字矩阵的性质的题目，可以转化为一维的问题。
(Count Submatrices With All Ones)[https://leetcode.com/problems/count-submatrices-with-all-ones/]
使用了二维转一维的思想，每列算一个像右像左的值，然后使用1维度求解。

(363. Max Sum of Rectangle No Larger Than K) 使用前缀和来降低维度

## 树状数组 + 离散化解决一下动态算小于等于某个值的数量的问题，或者某些区间问题
(Count of Smaller Numbers After Self)[https://leetcode.com/problems/count-of-smaller-numbers-after-self/]

## 环状的问题
1. 在后面接上一个相同的数组来接解决边界问题。并且限制长度。
2. 枚举结尾的点

## Divisible问题转化为余数问题
(Check If Array Pairs Are Divisible by k)[https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k/]
# 文章

[动态规划—各种 DP 优化](https://www.acwing.com/blog/content/630/)

[排序算法详细总结](https://www.acwing.com/blog/content/541/)

