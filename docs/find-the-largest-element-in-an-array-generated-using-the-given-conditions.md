# 找到使用给定条件生成的数组中最大的元素

> 原文:[https://www . geeksforgeeks . org/find-使用给定条件生成的数组中最大的元素/](https://www.geeksforgeeks.org/find-the-largest-element-in-an-array-generated-using-the-given-conditions/)

给定一个整数 **N** *(2 ≤ N ≤ 1e6)* ，任务是找到基于以下步骤生成的大小为 **N + 1** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中存在的最大元素:

*   arr[0] = 0
*   arr[1] = 1
*   arr[2 * i] = arr[i]，当 2 ≤ 2 * i ≤ N 时
*   疤痕[2 * i + 1] = 疤痕[i] + 疤痕[i + 1]当 2≤2 * i + 1≤N

**示例:**

> **输入:** N = 7
> **输出:** 3
> **解释:**根据给定规则构建数组:
> 
> *   Arr[0] = 0
> *   Arr[1] = 1
> *   Arr[(1 * 2) = 2] = Arr[1] = 1
> *   Arr[(1 * 2)+1 = 3]= Arr[1]+Arr[2]= 1+1 = 2
> *   Arr[(2 * 2) = 4] = Arr[2] = 1
> *   Arr[(2 * 2)+1 = 5]= Arr[2]+Arr[3]= 1+2 = 3
> *   Arr[(3 * 2) = 6] = Arr[3] = 2
> *   Arr[(3 * 2)+1 = 7]= Arr[3]+Arr[4]= 2+1 = 3
> 
> 因此，构造的数组是{0，1，1，2，1，3，2，3}。数组中存在的最大元素是 3。
> 
> **输入:** N = 2
> **输出:** 1
> **说明:**根据给定规则，Arr[0]、Arr[1]、Arr[2]中最大值为 1。

**方法:**解决问题的思路是基于给定的一组规则生成所有的数组元素，然后，找到其中的最大值。使用以下步骤迭代查找每个数组元素:

> **如果我是偶数:** Arr[i] = Arr[i/2]
> **否则，如果我是奇数:**Arr[I]= Arr[(I–1)/2]+Arr[(I–1)/2+1]

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate the
// required array
vector<int> findArray(int n)
{
    // Stores the array
    vector<int> Arr(n + 1);

    // Base case
    Arr[0] = 0;
    Arr[1] = 1;

    // Iterate over the indices
    for (int i = 2; i <= n; i++) {

        // If current index is even
        if (i % 2 == 0) {

            Arr[i] = Arr[i / 2];
        }
        // Otherwise
        else {

            Arr[i]
                = Arr[(i - 1) / 2]
                  + Arr[(i - 1) / 2 + 1];
        }
    }

    return Arr;
}

// Function to find and return
// the maximum array element
int maxElement(int n)
{
    // If n is 0
    if (n == 0)
        return 0;

    // If n is 1
    if (n == 1)
        return 1;

    // Generates the required array
    vector<int> Arr = findArray(n);

    // Return maximum element of Arr
    return *max_element(
        Arr.begin(), Arr.end());
}

// Driver Code
int main()
{
    int N = 7;
    cout << maxElement(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
import java.util.Arrays;

class GFG{

// Function to generate the
// required array and to find
// and return the maximum array
// element
static int[] findArray(int n)
{

    // Stores the array
    int Arr[] = new int[n + 1];

    // Base case
    Arr[0] = 0;
    Arr[1] = 1;

    // Iterate over the indices
    for(int i = 2; i <= n; i++)
    {

        // If current index is even
        if (i % 2 == 0)
        {
            Arr[i] = Arr[i / 2];
        }

        // Otherwise
        else
        {
            Arr[i] = Arr[(i - 1) / 2] +
                     Arr[(i - 1) / 2 + 1];
        }
    }
    return Arr;
}

// Function to find and return
// the maximum array element
static int maxElement(int n)
{

    // If n is 0
    if (n == 0)
        return 0;

    // If n is 1
    if (n == 1)
        return 1;

    // Generates the required array
    int[] Arr = findArray(n);

    // Return maximum element of Arr
    int ans = Integer.MIN_VALUE;
    for(int i = 0; i < n; i++)
    {
        ans = Math.max(ans, Arr[i]);
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int N = 7;

    System.out.println(maxElement(N));
}
}

// This code is contributed by ananyadixit8
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to generate the
# required array
def findArray(n):

    # Stores the array
    Arr = [0] * (n + 1)

    # Base case
    Arr[1] = 1

    # Iterate over the indices
    for i in range(2, n + 1):

        # If current index is even
        if (i % 2 == 0):
            Arr[i] = Arr[i // 2]

        # Otherwise
        else:
            Arr[i] = (Arr[(i - 1) // 2] +
                      Arr[(i - 1) // 2 + 1])

    return Arr

# Function to find and return
# the maximum array element
def maxElement(n):

    # If n is 0
    if (n == 0):
        return 0

    # If n is 1
    if (n == 1):
        return 1

    # Generates the required array
    Arr = findArray(n)

    # Return maximum element of Arr
    return max(Arr)

# Driver Code
if __name__ == "__main__" :

    N = 7

    print(maxElement(N))

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to generate the
// required array and to find
// and return the maximum array
// element
static int[] findArray(int n)
{

    // Stores the array
    int []Arr = new int[n + 1];

    // Base case
    Arr[0] = 0;
    Arr[1] = 1;

    // Iterate over the indices
    for(int i = 2; i <= n; i++)
    {

        // If current index is even
        if (i % 2 == 0)
        {
            Arr[i] = Arr[i / 2];
        }

        // Otherwise
        else
        {
            Arr[i] = Arr[(i - 1) / 2] +
                     Arr[(i - 1) / 2 + 1];
        }
    }
    return Arr;
}

// Function to find and return
// the maximum array element
static int maxElement(int n)
{

    // If n is 0
    if (n == 0)
        return 0;

    // If n is 1
    if (n == 1)
        return 1;

    // Generates the required array
    int[] Arr = findArray(n);

    // Return maximum element of Arr
    int ans = int.MinValue;
    for(int i = 0; i < n; i++)
    {
        ans = Math.Max(ans, Arr[i]);
    }
    return ans;
}

// Driver Code
public static void Main(String []args)
{
    int N = 7;   
    Console.WriteLine(maxElement(N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to generate the
// required array and to find
// and return the maximum array
// element
function findArray(n)
{

    // Stores the array
    let Arr = Array.from({length: n+1}, (_, i) => 0);

    // Base case
    Arr[0] = 0;
    Arr[1] = 1;

    // Iterate over the indices
    for(let i = 2; i <= n; i++)
    {

        // If current index is even
        if (i % 2 == 0)
        {
            Arr[i] = Arr[i / 2];
        }

        // Otherwise
        else
        {
            Arr[i] = Arr[(i - 1) / 2] +
                     Arr[(i - 1) / 2 + 1];
        }
    }
    return Arr;
}

// Function to find and return
// the maximum array element
function maxElement(n)
{

    // If n is 0
    if (n == 0)
        return 0;

    // If n is 1
    if (n == 1)
        return 1;

    // Generates the required array
    let Arr = findArray(n);

    // Return maximum element of Arr
    let ans = Number.MIN_VALUE;
    for(let i = 0; i < n; i++)
    {
        ans = Math.max(ans, Arr[i]);
    }
    return ans;
}

// Driver Code
    let N = 7;
    document.write(maxElement(N));

   // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)