# 追加两个元素，使数组满足给定条件

> 原文:[https://www . geesforgeks . org/append-两个元素组成数组-满足给定条件/](https://www.geeksforgeeks.org/append-two-elements-to-make-the-array-satisfy-the-given-condition/)

给定一个非负整数的数组 **arr[]** ，我们将 **X** 定义为所有数组元素的异或，将 **S** 定义为所有数组元素的和。任务是找到两个元素，使得当它们被附加到数组时 **S = 2 * X** 满足更新的数组。

**示例:**

> **输入:** arr[] = {1，7}
> **输出:** 6 14
> 最初 S = 8，X = 6。追加 6
> 和 14 后，S_NEW = (8 + 6 + 14) = 28
> 和 X_NEW = (6 ^ 6 ^ 14) = 14
> 显然，S_NEW = 2 * X_NEW
> **输入:** arr[] = {1，3}
> **输出:** 2 6

**天真方法:**运行从 **1** 到 **S** 的两个嵌套循环，并检查每对循环是否满足条件。这需要 **O(S <sup>2</sup> )** 时间。
**高效方法:**可以观察到，如果将 **X** 和 **S + X** 追加到数组中，那么满足给定条件的 **S_NEW = 2 * (S + X)** 和 **X_NEW = S + X** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required numbers
void findNums(int arr[], int n)
{

    // Find the sum and xor
    int S = 0, X = 0;
    for (int i = 0; i < n; i++) {
        S += arr[i];
        X ^= arr[i];
    }

    // Print the required elements
    cout << X << " " << (X + S);
}

// Driver code
int main()
{
    int arr[] = { 1, 7 };
    int n = sizeof(arr) / sizeof(int);

    findNums(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find the required numbers
    static void findNums(int arr[], int n)
    {

        // Find the sum and xor
        int S = 0, X = 0;
        for (int i = 0; i < n; i++)
        {
            S += arr[i];
            X ^= arr[i];
        }

        // Print the required elements
        System.out.println(X + " " + (X + S));
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 7 };
        int n = arr.length;

        findNums(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required numbers
def findNums(arr, n) :

    # Find the sum and xor
    S = 0; X = 0;
    for i in range(n) :
        S += arr[i];
        X ^= arr[i];

    # Print the required elements
    print(X, X + S);

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 7 ];
    n = len(arr);

    findNums(arr, n);

# This code is contributed by AnkiRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the required numbers
    static void findNums(int []arr, int n)
    {

        // Find the sum and xor
        int S = 0, X = 0;
        for (int i = 0; i < n; i++)
        {
            S += arr[i];
            X ^= arr[i];
        }

        // Print the required elements
        Console.WriteLine(X + " " + (X + S));
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 7 };
        int n = arr.Length;

        findNums(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach    
// Function to find the required numbers
    function findNums(arr , n) {

        // Find the sum and xor
        var S = 0, X = 0;
        for (i = 0; i < n; i++) {
            S += arr[i];
            X ^= arr[i];
        }

        // Prvar the required elements
        document.write(X + " " + (X + S));
    }

    // Driver code

        var arr = [ 1, 7 ];
        var n = arr.length;

        findNums(arr, n);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
6 14
```

**时间复杂度:** O(n)

**辅助空间:** O(1)