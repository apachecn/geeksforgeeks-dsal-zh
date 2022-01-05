# 大小为 K 的子集，乘积等于两个完美正方形的差

> 原文:[https://www . geeksforgeeks . org/大小为 k 的子集，乘积等于两个完美平方的差/](https://www.geeksforgeeks.org/subsets-of-size-k-with-product-equal-to-difference-of-two-perfect-squares/)

给定一个大小为 **N** 的不同整数数组 **arr[]** 和一个整数 **K** ，任务是计算数组大小为 **K** 的子集数量，其元素乘积可以表示为**a<sup>2</sup>–b<sup>2</sup>**。

**示例:**

> **输入:** arr[] = {1，2，3} K = 2
> **输出:** 2
> **解释:**
> 长度 2 的所有可能子集及其乘积如下:
> {1，2} = 2
> {2，3} = 6
> {1，3} = 3
> 因为，只有 3 可以表示为(2<sup>2</sup>–1<sup>2</sup>
> 
> **输入:** arr[] = {2，5，6} K = 2
> **输出:** 2
> **解释:**
> 所有可能的连续子序列及其乘积如下:
> {2，5} = 10
> {2，6} = 12
> {5，6} = 30
> 因为，只有 12 可以表示为(4<sup>2</sup>–2<sup>2</sup>

**进场:**

1.  [生成所有大小的子集 **K** 。](https://www.geeksforgeeks.org/python-program-to-get-all-subsets-of-given-size-of-a-set/)
2.  计算所有子集的[乘积。](https://www.geeksforgeeks.org/sum-products-possible-subsets/)
3.  一个[数只有当它是**奇数或可被 4** 整除时，才能表示为两个数](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-difference-of-two-squares/)的平方之差。
4.  因此，用满足这个条件的乘积计算所有子集。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 implementation of the approach

import itertools

# Function to return the
# Count of required sub-sequences
def count_seq(arr, n, k):

    # ans is Count variable
    ans = 0

    for seq in itertools.combinations(arr, k):

        # product of seq
        pro = 1 

        for ele in seq:
            pro *= ele

        # checking form of a2-b2
        if ((pro % 4) != 2): 
            ans += 1
    return ans

# Driver code
if __name__ == "__main__":
    arr = [2, 5, 6]
    n = len(arr)
    k = 2
    print(count_seq(arr, n, k))
```

**Output:**

```
1

```