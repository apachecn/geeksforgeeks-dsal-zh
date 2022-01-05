# 如果 arr[i] > 2*arr[i-1]

，检查是否存在和等于 k 的子序列

> 原文:[https://www . geesforgeks . org/check-a-subserial-exists-其和等于 k-if-arri-2arri-1/](https://www.geeksforgeeks.org/check-whether-a-subsequence-exists-whose-sum-is-equal-to-k-if-arri-2arri-1/)

给定正整数的排序数组，其中 **arr[i] > 2*arr[i-1]** ，检查是否存在总和等于 k 的子序列。
**示例:**

> **输入:** arr[]={ 1，3，7，15，31}，K=18
> **输出:**True
> A[1]+A[3]= 3+15 = 18
> 我们找到了一个和为 18
> **的子序列输入:** arr[]={ 1，3，7，15，31}，K=20
> **输出:** False
> 没有子序列

**天真的解决方案**:基本的解决方案是检查所有 2^n 可能的组合，并检查是否有任何和等于 k 的子序列。这个过程不适用于更高的 n，n 值> 20。
时间复杂度:O(2^N)
**高效解**:给我们 **arr[i] > 2*arr[i-1]** 所以我们可以说**arr[I]>(arr[I-1]+arr[I-2]+…+arr[2]+arr[1]+arr[0])**。
我们假设 arr[i]<= K(arr[I-1]+arr[I-2]+…+arr[2]+arr[1]+arr[0])，所以我们必须在集合中包含 arr[I]。因此，我们必须以降序遍历数组，当我们找到 arr[i] < =k 时，我们将在集合中包含 arr[i]，并从 K 中减去 arr[i]，并继续循环，直到 K 的值等于零。
如果 K 的值为零，则有一个子序列，否则没有。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Function to check whether sum of any set
// of the array element is equal
// to k or not
bool CheckForSequence(int arr[], int n, int k)
{
    // Traverse the array from end
    // to start
    for (int i = n - 1; i >= 0; i--) {
        // if k is greater than
        // arr[i] then subtract
        // it from k
        if (k >= arr[i])
            k -= arr[i];
    }

    // If there is any subsequence
    // whose sum is equal to k
    if (k != 0)
        return false;
    else
        return true;
}

// Driver code
int main()
{
    int A[] = { 1, 3, 7, 15, 31 };
    int n = sizeof(A) / sizeof(int);
    cout << (CheckForSequence(A, n, 18)
                 ? "True": "False") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

// Function to check whether
// sum of any set of the array element
// is equal to k or not
static boolean CheckForSequence(int arr[],
                                int n, int k)
{
    // Traverse the array from end
    // to start
    for (int i = n - 1; i >= 0; i--)
    {
        // if k is greater than
        // arr[i] then subtract
        // it from k
        if (k >= arr[i])
            k -= arr[i];
    }

    // If there is any subsequence
    // whose sum is equal to k
    if (k != 0)
        return false;
    else
        return true;
}

// Driver code
public static void main (String[] args)
{

    int A[] = { 1, 3, 7, 15, 31 };
    int n = A.length;
    System.out.println(CheckForSequence(A, n, 18) ?
                                            "True": "False");
}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to check whether sum of any set
# of the array element is equal
# to k or not
def CheckForSequence(arr, n, k) :

    # Traverse the array from end
    # to start
    for i in range(n - 1, -1, -1) :
        # if k is greater than
        # arr[i] then subtract
        # it from k
        if (k >= arr[i]) :
            k -= arr[i];

    # If there is any subsequence
    # whose sum is equal to k
    if (k != 0) :
        return False;
    else :
        return True;

# Driver code
if __name__ == "__main__" :

    A = [ 1, 3, 7, 15, 31 ];
    n = len(A);

    if (CheckForSequence(A, n, 18)) :
        print(True)
    else :
        print(False)

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to check whether
// sum of any set of the array element
// is equal to k or not
static bool CheckForSequence(int []arr,
                                int n, int k)
{
    // Traverse the array from end
    // to start
    for (int i = n - 1; i >= 0; i--)
    {
        // if k is greater than
        // arr[i] then subtract
        // it from k
        if (k >= arr[i])
            k -= arr[i];
    }

    // If there is any subsequence
    // whose sum is equal to k
    if (k != 0)
        return false;
    else
        return true;
}

// Driver code
public static void Main ()
{

    int []A = { 1, 3, 7, 15, 31 };
    int n = A.Length;
    Console.WriteLine(CheckForSequence(A, n, 18) ?
                                            "True": "False");
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// Javascript program to implement the above approach

// Function to check whether sum of any set
// of the array element is equal
// to k or not
function CheckForSequence( arr,n,k)
{
   // Traverse the array from end
    // to start
    for (var i = n - 1; i >= 0; i--) {
        // if k is greater than
        // arr[i] then subtract
        // it from k
        if (k >= arr[i])
            k -= arr[i];
    }

    // If there is any subsequence
    // whose sum is equal to k
    if (k != 0)
        return false;
    else
        return true;
}

var A = [ 1, 3, 7, 15, 31 ];
var n = A.length;
document.write( (CheckForSequence(A, n, 18) ? "True": "False") +"<br>");

//This code is contributed by SoumikModnal
</script>
```

**Output:** 

```
True
```

**时间复杂度** : O(N)