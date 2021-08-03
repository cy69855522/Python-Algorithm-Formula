# Python-Algorithm-Formula
基于Python的算法题公式化套路总结

# 前言
- 许多算法题可以看作是（题意转化 + 常用公式）的组合，本项目旨在收录常用算法模块，由此达到触类旁通的效果
- 项目持续更新中，默认使用 python3.8+，欢迎PR⛄~
- 看完题目没有思路时，想：
- - 如果是人工解决，是怎么做的？举个例子试试
  - DP：是否有时间序列？
  - 递归：是否可以分解为子任务？
  - BFS：是否可以转换为图的搜索问题？
  - 极值：堆、单调队列
# 反射弧
- 有序数组
  - 双指针往内夹
  - 二分搜索
# 技巧
- `@lru_cache(None)`缓存装饰器可直接利用缓存的相同输入时函数的结果
- BFS、DFS题都可以使用`collections.deque`模块
  - `q = collections.deque([root])`
  - `while q`
  - `q.popleft()`
  - `q.popright()`

# 公式
## 二分查找 BS
- 题目包含“有序”俩字
- 时间复杂度包含O(logN)
- 确定查找区间为闭区间，然后构思

## 双指针
- 实际同对队列的应用
- 有的题可以用迭代器代替
- 确定快慢指针移动的条件是那个指针决定的
- 把数组看作函数看看有没有什么特殊的地方

## 链表
- 一般用虚拟头会很省事

## 数组
- 先考虑下排序是否有帮助

## 动态规划 DP
- What？
  - DP的核心在于复用结果。DP把一个问题看作一个序列中的某一步，而这一步的结果可以基于前几步的结果进行快速求解。比如计算9个1相加时，DP计算的是`8+1`而不是`1+1+1+1+1+1+1+1+1`
- When？
  - 一个问题的解答可以被视为时间序列上的某个节点
  - 算法对时间复杂度要求较为严格（因为DP可以节省时间）
- How？
  1. 将问题转化为时间序列
  2. 创建与时间序列等长的list用于保存每个时间节点
  3. 初始化时间序列的开头
  4. 理清当前节点是如何利用之前节点快速求解的
- [152. 乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)
  ```python
  class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        # ①
        dp_min, dp_max = nums.copy(), nums.copy() # ②、③
        for i in range(1, len(nums)):
            cho = (n:=nums[i], n*dp_min[i-1], n*dp_max[i-1])
            dp_min[i], dp_max[i] = min(cho), max(cho) # ④
        return max(dp_max)
  ```
  1. nums可以被视为时间序列，nums对应的结果可以基于nums[:-1]的结果快速求解
  2. 创建了两个list分别用于保存：以对应位置元素为连续子数组末端时的乘积最大值、最小值，list长度同nums
  3. 当nums只有一个数字时，最大乘积就是那个数字。所以需要保证`dp_min[0]、dp_max[0] = nums[0]`
  4. 以nums[-1]结尾的乘积最大子数组 = max(nums[-1]，nums[-1] * 以nums[-2]结尾的乘积最大值或最小值)
## 广度优先搜索 BFS

## 深度优先搜索 DFS

## 滑动窗口
- 队列、滑动窗口的最大值：递减队列
- 窗口内是什么？
- 如何移动窗口的起始位置？
- 如何移动窗口的结束位置？

## 排序
- 比较数组中的一对数字：MergeSort
  - [剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

## 递归
- 思考n和n-1的关系
- 可以考虑最后两个值的情况

## 二叉树
- 树形问题一般使用递归解决
- 中序遍历中左子树一定在根节点左边，右子树同理
- 二叉查找树问题考虑它的性质和遍历情况
