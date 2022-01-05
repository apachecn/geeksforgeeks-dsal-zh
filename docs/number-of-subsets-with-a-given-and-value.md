# 给定“与”值的子集数量

> 原文:[https://www . geesforgeks . org/给定值子集数/](https://www.geeksforgeeks.org/number-of-subsets-with-a-given-and-value/)

给定一个长度为 **N** 的数组**和一个整数 **X** ，任务是找出**和**值为 **X** 的子集的数量。
**举例:**** 

> **输入:** arr[] = {2，3，2} X = 2
> **输出:** 6
> 所有可能的子集，并且有 and 值:
> { 2 } =**2**T9】{ 3 } = 3
> { 2 } =**2**
> { 2，3} = **2 & 3 = 2**
> {3，2} = **3 【T33 2 } =**2&3&2 = 2**
> **输入:** arr[] = {0，0，0}，X = 0
> **输出:** 7**

**方法:**一个简单的方法是通过生成所有可能的子集，然后用给定的 and 值计算子集的数量来解决问题。但是，对于较小的数组元素值，可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决。
我们先看递归关系。

> DP[I][curr _ and]= DP[I+1][curr _ and]+DP[I+1][curr _ and & arr[I]]

上述递归关系可以定义为子阵列**arr【I…N-1】**的子集数量，这样用 **curr_and** 对它们进行 and 运算将产生所需的 AND 值。
递归关系是合理的，因为只有路径。要么取当前元素，用**curr _ AND**AND，要么忽略，继续前进。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define maxN 20
#define maxM 64

// To store states of DP
int dp1[maxN][maxM];
bool v1[maxN][maxM];

// Function to return the required count
int findCnt(int* arr, int i, int curr, int n, int m)
{
    // Base case
    if (i == n) {
        return (curr == m);
    }

    // If the state has been solved before
    // return the value of the state
    if (v1[i][curr])
        return dp1[i][curr];

    // Setting the state as solved
    v1[i][curr] = 1;

    // Recurrence relation
    dp1[i][curr]
        = findCnt(arr, i + 1, curr, n, m)
          + findCnt(arr, i + 1, (curr & arr[i]), n, m);

    return dp1[i][curr];
}

// Driver code
int main()
{
    int arr[] = { 0, 0, 0 };
    int n = sizeof(arr) / sizeof(int);
    int m = 0;

    cout << findCnt(arr, 0, ((1 << 6) - 1), n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int maxN = 20;
static int maxM = 64;

// To store states of DP
static int [][]dp1 = new int[maxN][maxM];
static boolean [][]v1 = new boolean[maxN][maxM];

// Function to return the required count
static int findCnt(int []arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        return (curr == m ? 1 : 0);
    }

    // If the state has been solved before
    // return the value of the state
    if (v1[i][curr])
        return dp1[i][curr];

    // Setting the state as solved
    v1[i][curr] = true;

    // Recurrence relation
    dp1[i][curr] = findCnt(arr, i + 1, curr, n, m) +
                   findCnt(arr, i + 1, (curr & arr[i]), n, m);

    return dp1[i][curr];
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 0, 0, 0 };
    int n = arr.length;
    int m = 0;

    System.out.println(findCnt(arr, 0, ((1 << 6) - 1), n, m));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

maxN = 20
maxM = 64

# To store states of DP
dp1 = np.zeros((maxN, maxM));
v1 = np.zeros((maxN, maxM));

# Function to return the required count
def findCnt(arr, i, curr, n, m) :

    # Base case
    if (i == n) :
        return (curr == m);

    # If the state has been solved before
    # return the value of the state
    if (v1[i][curr]) :
        return dp1[i][curr];

    # Setting the state as solved
    v1[i][curr] = 1;

    # Recurrence relation
    dp1[i][curr] = findCnt(arr, i + 1, curr, n, m) + \
                   findCnt(arr, i + 1, (curr & arr[i]), n, m);

    return dp1[i][curr];

# Driver code
if __name__ == "__main__" :

    arr = [ 0, 0, 0 ];
    n = len(arr);
    m = 0;

    print(findCnt(arr, 0, ((1 << 6) - 1), n, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int maxN = 20;
static int maxM = 64;

// To store states of DP
static int [,]dp1 = new int[maxN, maxM];
static bool [,]v1 = new bool[maxN, maxM];

// Function to return the required count
static int findCnt(int []arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        return (curr == m ? 1 : 0);
    }

    // If the state has been solved before
    // return the value of the state
    if (v1[i, curr])
        return dp1[i, curr];

    // Setting the state as solved
    v1[i, curr] = true;

    // Recurrence relation
    dp1[i, curr] = findCnt(arr, i + 1, curr, n, m) +
                   findCnt(arr, i + 1, (curr & arr[i]), n, m);

    return dp1[i, curr];
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 0, 0, 0 };
    int n = arr.Length;
    int m = 0;

    Console.WriteLine(findCnt(arr, 0, ((1 << 6) - 1), n, m));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var maxN = 20;
var maxM =  64;

// To store states of DP
var dp1 = Array.from(Array(maxN), ()=> Array(maxM));
var v1 = Array.from(Array(maxN), ()=> Array(maxM));

// Function to return the required count
function findCnt(arr, i, curr, n, m)
{
    // Base case
    if (i == n) {
        return (curr == m);
    }

    // If the state has been solved before
    // return the value of the state
    if (v1[i][curr])
        return dp1[i][curr];

    // Setting the state as solved
    v1[i][curr] = 1;

    // Recurrence relation
    dp1[i][curr]
        = findCnt(arr, i + 1, curr, n, m)
          + findCnt(arr, i + 1, (curr & arr[i]), n, m);

    return dp1[i][curr];
}

// Driver code
var arr = [0, 0, 0];
var n = arr.length;
var m = 0;
document.write( findCnt(arr, 0, ((1 << 6) - 1), n, m));

</script>
```

**Output:** 

```
7
```