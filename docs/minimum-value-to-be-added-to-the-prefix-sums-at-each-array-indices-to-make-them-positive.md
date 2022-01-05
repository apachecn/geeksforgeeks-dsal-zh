# 在每个数组索引处加到前缀和上的最小值，使它们为正

> 原文:[https://www . geeksforgeeks . org/每个数组索引的前缀加和的最小值使它们为正数/](https://www.geeksforgeeks.org/minimum-value-to-be-added-to-the-prefix-sums-at-each-array-indices-to-make-them-positive/)

给定一个由整数的 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) arr **[]** ，任务是找到需要添加的最小正值 **S** ，使得在添加 **S** 之后给定数组的每个索引处的[前缀和总是正的。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)

**示例:**

> **输入:** arr[] = {-3，2，-3，4，2}
> **输出:** 5
> **解释:**
> 对于 S = 5，每个数组索引处的前缀和如下:
> 在索引 1 处:(5–3)= 2
> 在索引 2 处:(2 + 2) = 4
> 在索引 3 处:(4–3)= 1
> 在索引 4 处:(1 + 4) = 5
> 在索引 5 处:(T0)
> 
> **输入:** arr[] = {1，2 }
> T3】输出: 1

**天真方法:**最简单的方法是从 **1** 开始迭代 **S** 的所有可能值，并将 **S** 添加到每个数组索引处的前缀和中，并检查其是否大于 **0** 。打印 **S** 的值，对于该值，所有前缀和都为正。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，请执行以下步骤:

*   用 **0** 初始化一个变量**最小值**来存储最小前缀和。
*   初始化一个变量**和**来存储每个索引处的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   使用变量 **i** 在范围**【0，N–1】**内遍历数组**【arr】**。
    *   更新**总和**并将**arr【I】**添加到**总和**中。
    *   如果**总和**小于**最小值**，则将**最小值**设置为**总和**。
*   初始化一个变量**开始值**以存储所需结果，并将**开始值**设置为等于**(1–最小值)**。
*   完成上述步骤后，将**开始值**的值打印为 **S** 的最小可能值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum startValue
// for positive prefix sum at each index
int minStartValue(vector<int>& nums)
{
    // Store the minimum prefix sum
    int minValue = 0;

    // Stores prefix sum at each index
    int sum = 0;

    // Traverse over the array
    for (auto n : nums) {

        // Update the prefix sum
        sum += n;

        // Update the minValue
        minValue = min(minValue, sum);
    }

    int startValue = 1 - minValue;

    // Return the positive start value
    return startValue;
}

// Driver Code
int main()
{
    vector<int> nums = { -3, 2, -3, 4, 2 };

    // Function Call
    cout << minStartValue(nums);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// Function to find minimum startValue
// for positive prefix sum at each index
static int minStartValue(int[] nums)
{

    // Store the minimum prefix sum
    int minValue = 0;

    // Stores prefix sum at each index
    int sum = 0;

    // Traverse over the array
    for(int n : nums)
    {

        // Update the prefix sum
        sum += n;

        // Update the minValue
        minValue = Math.min(minValue, sum);
    }

    int startValue = 1 - minValue;

    // Return the positive start value
    return startValue;
}

// Driver Code
public static void main(String[] args)
{
    int[] nums = { -3, 2, -3, 4, 2 };

    // Function Call
    System.out.println(minStartValue(nums));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find minimum startValue
# for positive prefix sum at each index
def minStartValue(nums):

    # Store the minimum prefix sum
    minValue = 0

    # Stores prefix sum at each index
    sum = 0

    # Traverse over the array
    for i in range(len(nums)):

        # Update the prefix sum
        sum += nums[i]

        # Update the minValue
        minValue = min(minValue, sum)

    startValue = 1 - minValue

    # Return the positive start value
    return startValue

# Driver Code
if __name__ == '__main__':

    nums = [ -3, 2, -3, 4, 2 ]

    # Function Call
    print(minStartValue(nums))

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum startValue
// for positive prefix sum at each index
static int minStartValue(int[] nums)
{

    // Store the minimum prefix sum
    int minValue = 0;

    // Stores prefix sum at each index
    int sum = 0;

    // Traverse over the array
    foreach(int n in nums)
    {

        // Update the prefix sum
        sum += n;

        // Update the minValue
        minValue = Math.Min(minValue, sum);
    }

    int startValue = 1 - minValue;

    // Return the positive start value
    return startValue;
}

// Driver Code
public static void Main()
{
    int[] nums = { -3, 2, -3, 4, 2 };

    // Function Call
    Console.WriteLine(minStartValue(nums));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find minimum startValue
// for positive prefix sum at each index
function minStartValue(nums)
{

    // Store the minimum prefix sum
    let minValue = 0;

    // Stores prefix sum at each index
    let sum = 0;

    // Traverse over the array
    for (let n = 0; n < nums.length; n++) {

        // Update the prefix sum
        sum += nums[n];

        // Update the minValue
        minValue = Math.min(minValue, sum);
    }
    let startValue = 1 - minValue;

    // Return the positive start value
    return startValue;
}

// Driver Code
    let nums = [ -3, 2, -3, 4, 2 ];

    // Function Call
    document.write(minStartValue(nums));

    // This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)