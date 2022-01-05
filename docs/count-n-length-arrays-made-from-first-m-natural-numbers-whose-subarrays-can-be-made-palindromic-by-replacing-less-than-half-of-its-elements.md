# 计算由前 M 个自然数组成的 N 长度数组，通过替换其少于一半的元素可以使其子数组成为回文

> 原文:[https://www . geeksforgeeks . org/count-n-length-arrays-first-m-natural-numbers-通过替换少于其一半的元素可以制作谁的子数组-回文/](https://www.geeksforgeeks.org/count-n-length-arrays-made-from-first-m-natural-numbers-whose-subarrays-can-be-made-palindromic-by-replacing-less-than-half-of-its-elements/)

给定两个整数 **N** 和 **M** ，任务是用范围**【1，M】**中的元素找到尺寸 **N** 的[数组的计数，其中长度大于 **1** 的所有](https://www.geeksforgeeks.org/array-data-structure/)[子数组都可以通过替换其元素](https://www.geeksforgeeks.org/check-if-any-subarray-can-be-made-palindromic-by-replacing-less-than-half-of-its-elements/)的不到一半，即**地板(长度/2)** 来进行回文。

**示例:**

> **输入:** N = 2，M = 3
> **输出:** 6
> **解释:**
> 使用值 1 到 3，即[1，1]，[1，2]，[1，3]，[2，1][2，2]，[2，3]，[3，1]，[3，2]，[3，3]，有 9 个长度为 2 的可能数组。
> 除了[1，1]，[2，2]和[3，3]之外，所有这些阵列都具有长度大于 1 的子阵列，这需要 1 次操作才能使它们成为回文。所以要求的答案是 9–3 = 6。
> 
> **输入:** N = 5，M = 10
> T3】输出: 30240

**方法:**根据以下观察结果可以解决问题:

*   使数组成为[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)所需的最大允许操作数可能是**楼(大小(数组)/2)** 。
*   可以观察到，通过选择一个子阵，以相同的值开始和结束，使其成为回文所需的运算次数将小于**层(子阵的大小)/2** 。
*   因此，任务简化为使用不包含任何重复元素的范围**【1，M】**中的整数值来查找大小为 **N** 的数组数量，这可以通过查找 **M** 与**N**T9】的[排列来轻松完成，即 **Mp <sub>N</sub>** ，其等于**M *(M–1)*(M–2)*…*(M–3)**](https://www.geeksforgeeks.org/permutation-coefficient/)

按照以下步骤解决问题:

1.  初始化一个整数变量，比如 **ans = 1** 。
2.  从 **i = 0 到 N–1**遍历并将 **ans** 更新为 **ans = ans * (M-i)**
3.  打印 **ans** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// Function to find the number of arrays
// following the given condition
void noOfArraysPossible(ll N, ll M)
{
    // Initialize answer
    ll ans = 1;

    // Calculate nPm
    for (ll i = 0; i < N; ++i) {
        ans = ans * (M - i);
    }

    // Print ans
    cout << ans;
}

// Driver Code
int main()
{

    // Given N and M
    ll N = 2, M = 3;

    // Function Call
    noOfArraysPossible(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the number of arrays
// following the given condition
static void noOfArraysPossible(int N, int M)
{
    // Initialize answer
    int ans = 1;

    // Calculate nPm
    for (int i = 0; i < N; ++i)
    {
        ans = ans * (M - i);
    }

    // Print ans
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given N and M
    int N = 2, M = 3;

    // Function Call
    noOfArraysPossible(N, M);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of arrays
# following the given condition
def noOfArraysPossible(N, M):

    # Initialize answer
    ans = 1

    # Calculate nPm
    for i in range(N):
        ans = ans * (M - i)

    # Print ans
    print(ans)

# Driver Code
if __name__ == "__main__" :

    # Given N and M
    N = 2
    M = 3

    # Function Call
    noOfArraysPossible(N, M)

# This code is contributed by jana_sayantan
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the number of arrays
// following the given condition
static void noOfArraysPossible(int N, int M)
{
    // Initialize answer
    int ans = 1;

    // Calculate nPm
    for (int i = 0; i < N; ++i)
    {
        ans = ans * (M - i);
    }

    // Print ans
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    // Given N and M
    int N = 2, M = 3;

    // Function Call
    noOfArraysPossible(N, M);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to find the number of arrays

    // following the given condition
    function noOfArraysPossible(N , M)
    {

        // Initialize answer
        var ans = 1;

        // Calculate nPm
        for (i = 0; i < N; ++i) {
            ans = ans * (M - i);
        }

        // Print ans
        document.write(ans);
    }

    // Driver Code

        // Given N and M
        var N = 2, M = 3;

        // Function Call
        noOfArraysPossible(N, M);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)