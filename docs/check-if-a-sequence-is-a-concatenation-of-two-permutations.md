# 检查一个序列是否是两个排列的连接

> 原文:[https://www . geesforgeks . org/check-if-a-sequence-is-concation-of-two-排列/](https://www.geeksforgeeks.org/check-if-a-sequence-is-a-concatenation-of-two-permutations/)

给定一个包含正整数的数组 **arr** ，任务是检查给定的数组 **arr** 是否是两个排列的串联。一个 M 个整数的序列，如果它包含从 1 到 M 的所有整数恰好一次，就叫做置换。
**例:**

> **输入:** arr[] = {1，2，5，3，4，1，1}
> **输出:**否
> **说明:**
> 给定数组包含 1 三次。前 5 个元素形成长度为 5 的排列，但其余 2 个元素不形成排列。
> **输入:** arr[] = {1，2，5，3，4，1，2}
> **输出:** Yes
> **解释:**
> 给定数组 arr[] = {1，2，5，3，4} + {1，2}
> 前 5 个元素组成长度为 5 的排列，其余 2 个元素组成长度为 2 的排列。

**进场:**

1.  [遍历给定的数组](https://www.geeksforgeeks.org/iterating-arrays-java/)和[计算所有元素的总和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。
2.  形成包含[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的前缀数组。
3.  现在，对于范围[1，N]中的每个索引
    *   使用以下条件，检查从开始到当前索引的元素是否形成排列:

```
Sum of K elements = Sum of K natural numbers

where K is the current index
```

*   然后检查剩余的元素形成排列。
*   如果是，那么我们打印/返回是。

以下是上述方法的实现:

## C++

```
// C++ program to check if a given sequence
// is a concatenation of two permutations or not

#include <bits/stdc++.h>
using namespace std;

// Function to Check if a given sequence
// is a concatenation of two permutations or not
bool checkPermutation(int arr[], int n)
{
    // Computing the sum of all the
    // elements in the array
    long long sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    long long prefix[n + 1] = { 0 };
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (int i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        long long lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        long long rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        long long l_len = i + 1,
                  r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
             == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 5, 3, 4, 1, 2 };
    int n = sizeof(arr) / sizeof(int);

    if (checkPermutation(arr, n))
        cout << "Yes\n";
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given sequence
// is a concatenation of two permutations or not
import java.util.*;

class GFG{

// Function to Check if a given sequence
// is a concatenation of two permutations or not
static boolean checkPermutation(int []arr, int n)
{
    // Computing the sum of all the
    // elements in the array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    int []prefix = new int[n + 1];
    Arrays.fill(prefix,0);
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (int i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        int lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        int rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        int l_len = i + 1,
                r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
            == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Driver code
public static void main(String args[])
{
    int []arr = { 1, 2, 5, 3, 4, 1, 2 };
    int n = arr.length;

    if (checkPermutation(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");

}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python program to check if a given sequence
# is a concatenation of two permutations or not

# Function to Check if a given sequence
# is a concatenation of two permutations or not
def checkPermutation(arr, n):

    # Computing the sum of all the
    # elements in the array
    sum = 0;
    for i in range(n):
        sum += arr[i];

    # Computing the prefix sum
    # for all the elements in the array
    prefix = [0]*(n + 1);
    prefix[0] = arr[0];
    for i in range(n):
        prefix[i] = prefix[i - 1] + arr[i];

    # Iterating through the i
    # from lengths 1 to n-1
    for i in range(n - 1):

        # Sum of first i+1 elements
        lsum = prefix[i];

        # Sum of remaining n-i-1 elements
        rsum = sum - prefix[i];

        # Lengths of the 2 permutations
        l_len = i + 1
        r_len = n - i - 1;

        # Checking if the sums
        # satisfy the formula or not
        if (((2 * lsum)== (l_len * (l_len + 1))) and
            ((2 * rsum)== (r_len * (r_len + 1)))):
            return True;

    return False;

# Driver code
if __name__=='__main__':

    arr = [ 1, 2, 5, 3, 4, 1, 2 ]
    n = len(arr)

    if (checkPermutation(arr, n)):
        print("Yes");
    else:
        print("No");

# This code is contributed by Princi Singh
```

## C#

```
// C# program to check if a given sequence
// is a concatenation of two permutations or not
using System;

class GFG{

// Function to Check if a given sequence
// is a concatenation of two permutations or not
static bool checkPermutation(int []arr, int n)
{
    // Computing the sum of all the
    // elements in the array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    int []prefix = new int[n + 1];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (int i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        int lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        int rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        int l_len = i + 1,
                r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
            == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 5, 3, 4, 1, 2 };
    int n = arr.Length;

    if (checkPermutation(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to check if a given sequence
// is a concatenation of two permutations or not

// Function to Check if a given sequence
// is a concatenation of two permutations or not
function checkPermutation(arr, n)
{
    // Computing the sum of all the
    // elements in the array
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // Computing the prefix sum
    // for all the elements in the array
    let prefix = Array.from({length: n+1}, (_, i) => 0);
    prefix[0] = arr[0];
    for (let i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    // Iterating through the i
    // from lengths 1 to n-1
    for (let i = 0; i < n - 1; i++) {

        // Sum of first i+1 elements
        let lsum = prefix[i];

        // Sum of remaining n-i-1 elements
        let rsum = sum - prefix[i];

        // Lengths of the 2 permutations
        let l_len = i + 1,
                r_len = n - i - 1;

        // Checking if the sums
        // satisfy the formula or not
        if (((2 * lsum)
            == (l_len * (l_len + 1)))
            && ((2 * rsum)
                == (r_len * (r_len + 1))))
            return true;
    }

    return false;
}

// Driver Code

        let arr = [ 1, 2, 5, 3, 4, 1, 2 ];
    let n = arr.length;

    if (checkPermutation(arr, n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

时间复杂度:0(n)

辅助空间:O(n)