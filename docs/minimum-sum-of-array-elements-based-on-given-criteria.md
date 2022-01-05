# 基于给定标准的阵列元素的最小和

> 原文:[https://www . geesforgeks . org/基于给定标准的数组元素最小和/](https://www.geeksforgeeks.org/minimum-sum-of-array-elements-based-on-given-criteria/)

给定一个大小为 **N** 的数组 **A[]** ，其中一些条目是整数，一些条目是-1。任务是用满足以下标准的数字替换-1。

1.  要替换的数字的二进制表示应该只有奇数位的 0，并且数字必须是偶数。
2.  The array entries A[i] with which -1’s are replaced with are in such a way that **A[i]>=A[i-1]** and also for the given array **A[0]!=-1**.

    完成上述操作后，找到可能的最小数组条目总和。

**示例:**

> **输入:** A[] = {1，5，-1，25，-1，7，35， -1}
> **输出:** 153
> 指标 2:用 8 代替-1 作为其二进制表示为 1000，其奇数位为 0
> ，8 为偶数，8 为 8 > =5
> 指标 4:用 32 代替-1 作为其二进制表示为 100000，其奇数位为 0
> ，32 为偶数，32 > =25
> 指标 7:用 40 代替-1 作为其二进制表示为 1000
> 
> **输入:** A[] = {4，8，12，-1，3，0，15，-1，34，-1 }
> T3】输出: 142

**进场:**

*   使用线性搜索迭代数组以识别所有的-1。
*   只要有-1，就从索引比当前索引小 1 的数字开始生成另一个 while 循环。
*   检查级数中所有项的二进制表示的奇数位置，如果它如预期的那样只包含零，则脱离循环，否则将迭代器递增 1，直到我们达到所需的数字。
*   当满足要求的数字时，给定索引处的对应元素被替换为满足所有条件的新数字。
*   在所有-1 被替换后，计算数组条目的总和。

下面是上述方法的实现:

```
# Find the minimum sum of array 
# entries following given criteria.
def Bit_Even_Arrays(arr):

    # Iterating through the 
    # array to find -1's
    for k, v in enumerate(arr):
        z = 0
        if v == -1:

            # Starting from the entry
            # with index 1 less than -1
            # as A[i]>= A[i-1]
            y = k - 1
            z = arr[y]

            # Initiating the infinite series
            # that satisfies given criteria 
            # and breaking out of the loop
            # once it satisfies
            while True:
                S = bin(z)[2:][1::2]
                if (z % 2 == 0) \
                          &(len(set(S))== 1)\
                            & ('0' in set(S)):
                    break
                else:

                    # incrementing the entry
                    # until the required 
                    # entry is met
                    z += 1 
            arr[k]= z
    return (sum(arr)) 

# Driver code
if __name__ == '__main__':
      arr = [1, 5, -1, 25, -1, 7, 35, -1]
      print (Bit_Even_Arrays(arr))
```

**Output:**

```
153

```