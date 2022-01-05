# 将数组 A[]拆分为具有相等和且大小等于数组 B[]元素的子集

> 原文:[https://www . geeksforgeeks . org/将数组 a 拆分为具有等于数组 b 元素的和和大小的子集/](https://www.geeksforgeeks.org/split-an-array-a-into-subsets-having-equal-sum-and-sizes-equal-to-elements-of-array-b/)

给定一个由 **N** 个整数组成的数组 **A[]** ，任务是将数组 **A[]** 分割成与数组 **B[]** 中的元素具有相等和且长度相等的子集。

**示例:**

> **输入:** A[] = {17，13，21，20，50，29}，B[] = {2，3，1}
> **输出:**
> 21 29
> 17 13 20
> 50
> 
> **输入:** A[] = { 1，2，3，4，5，6}，B[] = { 2，2，2 }
> T3】输出:T5】1 6
> 2 5
> 3 4

**方法:**按照以下步骤解决问题:

*   由于已经给出了子集的计数，所以计算每个子集的总和。
*   遍历数组 B[]的每个元素，找到长度 B[i]的每个可能的组合，并检查组合的总和是否等于所需的总和。
*   对每个数组元素 B[i]重复上述步骤，并打印最终答案

下面是上述方法的实现:

## 计算机编程语言

```
# Python Program to implement
# the above approach
from itertools import combinations

# Function to split elements of first
# array into subsets of size given as
# elements in the second array
def main(A, B):

    # Required sum of subsets
    req_sum = sum(A) // len(B)

    # Stores the subsets
    final = []

    # Iterate the array B[]
    for i in B:

        # Generate all possible
        # combination of length B[i]
        temp = list(combinations(A, i))

    # Iterate over all the combinations
        for j in temp:

            # If the sum is equal to the 
            # required sum of subsets
            if(sum(j) == req_sum):

                # Store the subset
                temp = list(j)
                final.append(temp)

                for k in temp:

                    # Removing the subset
                    # from the array
                    A.remove(k)
                break

    # Printing the final result
    print(final)

# Driver Code
if __name__ == '__main__':
    # Value of array A and B
    A = [1, 2, 3, 4, 5, 6]
    B = [2, 2, 2]

    # Function call
    main(A, B)
```

**Output:**

```
[[1, 6], [2, 5], [3, 4]]

```

**时间复杂度:**O(N<sup>3</sup>)
T5】辅助空间: O(2 <sup>maxm</sup> ，其中 *maxm* 是数组 B[]中的最大元素