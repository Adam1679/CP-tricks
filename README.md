# CP-tricks
刷题心得

# 刷题技巧总结
## 单调栈
- 注意在向前的单调栈合向后的单调栈，分开使用<=和<来避免计算的重复
(leetcode ) https://leetcode.com/problems/sum-of-subarray-minimums/submissions/

- 单调增的单调栈: 不允许重复值，while(!q.empty() && a[i] > a[q.top()] ) q.pop(); 或者 允许重复值，while(!q.empty() && a[i] >= a[q.top()] ) q.pop();
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

## 模板，区间合并和最多不相交的区间
253. Meeting Rooms II 或者[区间分组](https://www.acwing.com/solution/content/5898/) : 排序，从前往后枚举每个区间，判断能否将其放到某个现有的组中，即是否存在当前区间的的左端点L > 任意组中右端点的最小值的组。可用堆来优化。

1520. Maximum Number of Non-Overlapping Substrings

[区间选点](https://www.acwing.com/solution/content/5887/): 选点从而覆盖所有区间。排序，贪心选右边区间。

[最大不相交区间](https://www.acwing.com/solution/content/4276/): 排序，然后贪心的判断当前的左端点和当前区间的最小的右端点。
## Divisible问题转化为余数问题
(Check If Array Pairs Are Divisible by k)[https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k/]

## 动态规划
[背包九讲](https://www.acwing.com/blog/content/852/)
- 01背包
- 完全背包
- 多重背包
- 混合背包 -> 各司其职
- 有依赖的背包->多重背包
- 二维费用背包
- 组内互斥背包->多重背包


# Data Strucutre Question
1. Binary Tree Traversal
[二叉树非递归遍历，Morris遍历，层次遍历，DFS遍历模板大全](https://www.acwing.com/blog/content/414/)

2. LRU
双向链表 + Hash

3.堆
```
// 递归的下沉一个数，使用完全二叉树来存储。
void down(int u)
{
    int t = u;
    if(u*2 <= size && h[u*2] < h[t]) t = u*2;
    if(u*2 + 1 <= size && h[u*2 + 1] < h[t]) t = u*2 + 1;
    if(u != t)
    {
        swap(h[u],h[t]);
        down(t);
    }
}
// 上移动
void up(int u)
{
    while(u/2 && h[u/2] > h[u])
    {
        swap(h[u/2],h[u]);
        u /= 2;
    }
}
```

# 文章

[动态规划—各种 DP 优化](https://www.acwing.com/blog/content/630/)

[排序算法详细总结](https://www.acwing.com/blog/content/541/)


