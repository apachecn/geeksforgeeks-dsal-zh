# 计算所有子阵列的不同位或

> 原文:[https://www . geeksforgeeks . org/count-distinct-bit-or-of-all-subarrays/](https://www.geeksforgeeks.org/count-distinct-bitwise-or-of-all-subarrays/)

给定一个非负整数的数组 **A** ，其中![0 \leq A[i] \leq 10^{9}    ](img/63af66a7da1f617c936f4c1ea3098d6a.png "Rendered by QuickLaTeX.com")。任务是计算通过对所有可能的子阵列中的所有元素进行按位“或”而获得的不同可能结果的数量。
**示例:**

```
Input: A = [1, 2]
Output: 3
Explanation: The possible subarrays are [1], [2], [1, 2].
These Bitwise OR of subarrays are 1, 2, 3.
There are 3 distinct values, so the answer is 3.

Input: A = [1, 2, 4]
Output: 6
Explanation: The possible distinct values are 1, 2, 3, 4, 6, and 7.
```

**方法:**
天真的方法是生成所有可能的子阵列，并对子阵列中的所有元素进行按位“或”运算。将每个结果存储在**设置**中，并返回设置的**长度。
**高效进场:**
我们可以把上面的进场做得更好。天真的方法是计算所有可能的结果，其中， **res(i，j) = A[i] | A[i+1] | … | A[j]** 。然而，我们可以通过注意到 **res(i，j+1) = res(i，j) | A[j+1]** 来加快速度。在 **kth** 步骤中，假设我们在某个设置 **pre** 中拥有所有的 **res(i，k)** 。然后我们可以使用 **res(i，k+1) = res(i，k) | A[k+1]** 找到下一个 **pre** set **(对于 k - > k+1)** 。
但是，该集合 **pre** 中唯一值的数量是 atmost 32，因为列表 **res(k，k)，res(k-1，k)，res(k-2，k)……**是**单调递增**，并且任何不同于前一个的后续值在其二进制表示中必须有更多的 1，该二进制表示最多可以有 **32 个 1**。
**以下是上述办法的实施情况。**** 

## 计算机编程语言

```
# Python implementation of the above approach

# function to return count of distinct bitwise OR
def subarrayBitwiseOR(A):

    # res contains distinct values
    res = set()

    pre = {0}

    for x in A:
        pre = {x | y for y in pre} | {x}
        res |= pre

    return len(res)

# Driver program
A = [1, 2, 4]

# print required answer
print(subarrayBitwiseOR(A))

# This code is written by
# Sanjit_Prasad
```

**Output**

```
6
```

**时间复杂度:** O(N*log(K))，其中 N 为 A 的长度，K 为 A 中元素的最大尺寸。

上述方法的 C++实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// function to calculate count of
// distinct bitwise OR of all
// subarrays.
int distintBitwiseOR(int arr[], int n)
{
    unordered_set<int> ans, prev;

    for (int i = 0; i < n; i++) {
        unordered_set<int> ne;

        for (auto x : prev)
            ne.insert(arr[i] | x);
        ne.insert(arr[i]);

        for (auto x : ne)
            ans.insert(x);

        prev = ne;
    }

    return ans.size();
}

// Driver Code
int main()
{
    int n = 3;
    int arr[] = { 1, 2, 4 };

    cout << distintBitwiseOR(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // function to calculate count of
// distinct bitwise OR of all
// subarrays.
 static int distintBitwiseOR(int arr[], int n)
  {

     HashSet<Integer>ans = new HashSet<>();
        HashSet<Integer>prev = new HashSet<>();
        for(int i = 0; i < n; i++)
        {
            HashSet<Integer>ne = new HashSet<>();
            ne.add(arr[i]);
            for(int x :prev)
            {
                ne.add(arr[i]|x);
            }
            for(int x :ne)
            {
              ans.add(x);
            }

            prev = ne;
        }
        return ans.size();
    }

    // Driver code
    public static void main (String[] args) {
         int n = 3;
         int arr[] = { 1, 2, 4 };
         System.out.println(distintBitwiseOR(arr, n));

    }
}

// This code is contributed by iramkhalid24.
```

**Output**

```
6
```