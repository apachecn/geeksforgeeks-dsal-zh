# 检查数组是否是从 1 到 N 的数字排列:集合 2

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-a-numbers-array-从-1 到-n-set-2/](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n-set-2/)

给定一个包含正整数 **N** 的数组 **arr** ，任务是检查给定的数组 arr 是否代表一个排列。

> 一个 N 个整数的序列，如果它包含从 1 到 N 的所有整数恰好一次，就叫做置换。

**例:**

> **输入:** arr[] = {1，2，5，3，2}
> **输出:**否
> **说明:**
> 给定数组包含 2 两次，数组缺少 4 表示长度为 5 的排列。
> **输入:** arr[] = {1，2，5，3，4}
> **输出:**是
> **说明:**
> 给定数组包含 1 到 5 的所有整数正好一次。因此，它代表长度为 5 的排列。

**天真的做法:** ***在 O(N)<sup>2</sup>时间***
这种做法在这里被提到
**另一种做法:** ***在 O(N)时间和 O(N)空间***
这种做法在这里被提到。
**高效方法:** ***使用哈希表***

1.  创建一个 N 大小的[哈希表](https://www.geeksforgeeks.org/hashtable-in-java/)，存储从 1 到 N 的每个数字的频率计数
2.  遍历给定数组，将每个数字的[频率存储在哈希表中。](https://www.geeksforgeeks.org/find-frequency-number-array/)
3.  然后遍历哈希表，检查从 1 到 N 的所有数字是否都有 1 的频率。
4.  如果上述条件为真，则打印“是”，否则打印“否”。

**以下是上述方法的实施:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to decide if an array
// represents a permutation or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if an
// array represents a permutation or not
string permutation(int arr[], int N)
{

    int hash[N + 1] = { 0 };

    // Counting the frequency
    for (int i = 0; i < N; i++) {
        hash[arr[i]]++;
    }

    // Check if each frequency is 1 only
    for (int i = 1; i <= N; i++) {
        if (hash[i] != 1)
            return "No";
    }

    return "Yes";
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 5, 5, 3 };
    int n = sizeof(arr) / sizeof(int);
    cout << permutation(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to decide if an array
// represents a permutation or not
class GFG{

// Function to check if an
// array represents a permutation or not
static String permutation(int arr[], int N)
{

    int []hash = new int[N + 1];

    // Counting the frequency
    for (int i = 0; i < N; i++) {
        hash[arr[i]]++;
    }

    // Check if each frequency is 1 only
    for (int i = 1; i <= N; i++) {
        if (hash[i] != 1)
            return "No";
    }

    return "Yes";
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 5, 5, 3 };
    int n = arr.length;
    System.out.print(permutation(arr, n) +"\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to decide if an array
# represents a permutation or not

# Function to check if an
# array represents a permutation or not
def permutation(arr,  N) :

    hash = [0]*(N + 1);

    # Counting the frequency
    for i in range(N) :
        hash[arr[i]] += 1;

    # Check if each frequency is 1 only
    for i in range(1, N + 1) :
        if (hash[i] != 1) :
            return "No";

    return "Yes";

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 5, 5, 3 ];
    n = len(arr);
    print(permutation(arr, n));

    # This code is contributed by Yash_R
```

## C#

```
// C# program to decide if an array
// represents a permutation or not
using System;

class GFG{

    // Function to check if an
    // array represents a permutation or not
    static string permutation(int []arr, int N)
    {

        int []hash = new int[N + 1];

        // Counting the frequency
        for (int i = 0; i < N; i++) {
            hash[arr[i]]++;
        }

        // Check if each frequency is 1 only
        for (int i = 1; i <= N; i++) {
            if (hash[i] != 1)
                return "No";
        }

        return "Yes";
    }

    // Driver code
    public static void Main(string[] args)
    {
        int []arr = { 1, 1, 5, 5, 3 };
        int n = arr.Length;
        Console.Write(permutation(arr, n) +"\n");
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// JavaScript program to decide if an array
// represents a permutation or not

// Function to check if an
// array represents a permutation or not
function permutation(arr, N)
{

    var hash = Array(N+1).fill(0);

    // Counting the frequency
    for (var i = 0; i < N; i++) {
        hash[arr[i]]++;
    }

    // Check if each frequency is 1 only
    for (var i = 1; i <= N; i++) {
        if (hash[i] != 1)
            return "No";
    }

    return "Yes";
}

// Driver code
var arr = [1, 1, 5, 5, 3];
var n = arr.length;
document.write( permutation(arr, n));

</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(N)*