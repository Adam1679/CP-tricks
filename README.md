# CP-tricks
刷题心得

# 刷题技巧总结
## array
[shortest word distance](https://leetcode.com/problems/shortest-word-distance/description/): 判断两个东西的距离，使用rolling的形式来判断。

[Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/discuss/76607/C%2B%2B-O(nlogn)-Time-O(n)-Space-MergeSort-Solution-with-Detail-Explanation): merge sort通常用来处理这种计算逆序的题目。

[first miss number], [Find All Duplicates in an Array]: 都可以使用一些swap来解决。对于所有都是正数的arry，加负数来代表是否存在。


[Find Peak Element](https://leetcode.com/problems/find-peak-element/): 使用二分。正确性比较难证明。
## 单调栈
- 注意在向前的单调栈合向后的单调栈，分开使用<=和<来避免计算的重复
(leetcode ) https://leetcode.com/problems/sum-of-subarray-minimums/submissions/

- 单调增的单调栈: 不允许重复值，while(!q.empty() && a[i] > a[q.top()] ) q.pop(); 或者 允许重复值，while(!q.empty() && a[i] >= a[q.top()] ) q.pop();
## 前缀和和后缀来解决一些有“除了某个点之外的所有”的性质的问题
1. [LeetCode 238. Product of Array Except Self.](https://www.acwing.com/solution/content/288/)

使用前缀积和后缀积。
Path Sum III: 使用前缀和把路径的和转化为two sum的问题。


2. Google Kickstart. [看狗](https://www.acwing.com/problem/content/836/)
枚举最后一次的操作，然后使用前缀和后缀来获得除了这个选择之外的最小值

## 动态规划结合状态压缩，状态必须存在拓扑序列，不能环形依赖. 
[拯救大兵瑞恩](https://www.acwing.com/solution/content/14096/)

[1542. Find Longest Awesome Substring](https://leetcode.com/problems/find-longest-awesome-substring/): 使用状态压缩来记录奇偶状态，从而达到判断某个子序列的状态是否是奇数/偶然。然后使用dp。[最长偶数原因的字串问题，类似](https://leetcode.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/).



## 各类子序列问题
[子序列问题](https://www.acwing.com/blog/content/823/)

子序列问题，而如果么有要求连续，那么优先考虑sort。[1498. Number of Subsequences That Satisfy the Given Sum Condition](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/)

[公共子序列]

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

[区间覆盖](https://www.acwing.com/solution/content/3752/)：最少区间来覆盖一个区间[L, R]。排序，选能覆盖当前L的右端点最大的区间。
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

## 贪心
区间问题大多贪心。

(哈夫曼树)[https://www.acwing.com/solution/content/2876/]：优先队列+贪心

## dfs
[组合数1，2，3](https://leetcode.com/problems/combination-sum-ii/discuss/16878/Combination-Sum-I-II-and-III-Java-solution-(see-the-similarities-yourself))
dfs如果有重复数字并且要求unique conbinations，那么需要while loop 去排除重复。

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


