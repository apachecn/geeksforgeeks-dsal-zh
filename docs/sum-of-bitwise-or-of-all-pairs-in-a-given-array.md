# 给定数组中所有对的位或之和

> 原文:[https://www . geesforgeks . org/给定数组中所有对的按位或和/](https://www.geeksforgeeks.org/sum-of-bitwise-or-of-all-pairs-in-a-given-array/)

给定数组“arr[0..整数的 n-1 "]。任务是计算所有对的按位或之和，即计算给定数组中所有对的“ **arr[i] | arr[j]** ”之和，其中 i < j .这里**“|”**是按位或运算符。预期时间复杂度为 0(n)。
**例:**

```
Input:  arr[] = {5, 10, 15}
Output: 15
Required Value = (5  |  10) + (5  |  15) + (10  |  15) 
               = 15 + 15 + 15 
               = 45

Input: arr[] = {1, 2, 3, 4}
Output: 3
Required Value = (1  |  2) + (1  |  3) + (1  |  4) + 
                 (2  |  3) + (2  |  4) + (3  |  4) 
               = 3 + 3 + 5 + 3 + 6 + 7
               = 27
```

一种**蛮力**方法是运行两个循环，时间复杂度为 0(n<sup>2</sup>)。

## C++

```
// A Simple C++ program to compute sum of bitwise OR
// of all pairs
#include <bits/stdc++.h>
using namespace std;

// Returns value of "arr[0]  | arr[1] + arr[0] | arr[2] +
// ... arr[i] | arr[j] + ..... arr[n-2] |  arr[n-1]"
int pairORSum(int arr[], int n)
{
    int ans = 0; // Initialize result

    // Consider all pairs (arr[i], arr[j) such that
    // i < j
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            ans += arr[i] | arr[j];

    return ans;
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << pairORSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program to compute
// sum of bitwise OR of all pairs
import java.io.*;

class GFG {

    // Returns value of "arr[0] | arr[1] +
    // arr[0] | arr[2] + ... arr[i] | arr[j] +
    // ..... arr[n-2] | arr[n-1]"
    static int pairORSum(int arr[], int n)
    {
        int ans = 0; // Initialize result

        // Consider all pairs (arr[i], arr[j)
        // such that i < j
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                ans += arr[i] | arr[j];

        return ans;
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4 };
        int n = arr.length;
        System.out.println(pairORSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# A Simple Python 3 program to compute
# sum of bitwise OR of all pairs

# Returns value of "arr[0] | arr[1] +
# arr[0] | arr[2] + ... arr[i] | arr[j] +
# ..... arr[n-2] | arr[n-1]"
def pairORSum(arr, n) :
    ans = 0 # Initialize result

    # Consider all pairs (arr[i], arr[j)
    # such that i < j
    for i in range(0, n) :
        for j in range((i + 1), n) :
            ans = ans + arr[i] | arr[j]

    return ans

# Driver program to test above function
arr = [1, 2, 3, 4]
n = len(arr)
print(pairORSum(arr, n))
```

## C#

```
// A Simple C# program to compute
// sum of bitwise OR of all pairs
using System;

class GFG {

    // Returns value of "arr[0] | arr[1] +
    // arr[0] | arr[2] + ... arr[i] | arr[j] +
    // ..... arr[n-2] | arr[n-1]"
    static int pairORSum(int[] arr, int n)
    {

        int ans = 0; // Initialize result

        // Consider all pairs (arr[i], arr[j)
        // such that i < j
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                ans += arr[i] | arr[j];

        return ans;
    }

    // Driver program to test above function
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4 };
        int n = arr.Length;
        Console.Write(pairORSum(arr, n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple PHP program to
// compute sum of bitwise
// OR of all pairs

// Returns value of "arr[0] |
// arr[1] + arr[0] | arr[2] +
// ... arr[i] | arr[j] + .....
// arr[n-2] | arr[n-1]"

function pairORSum($arr, $n)
{
    // Initialize result
    $ans = 0;

    // Consider all pairs (arr[i],
    // arr[j) such that i < j
    for ($i = 0; $i < $n; $i++)
        for ( $j = $i + 1; $j < $n; $j++)
        $ans += $arr[$i] | $arr[$j];

    return $ans;
}

// Driver Code
$arr = array(1, 2, 3, 4);
$n = sizeof($arr) ;
echo pairORSum($arr, $n), "\n";

?>
```

## java 描述语言

```
<script>

// A Simple Javascript program to compute sum of bitwise OR
// of all pairs

// Returns value of "arr[0]  | arr[1] + arr[0] | arr[2] +
// ... arr[i] | arr[j] + ..... arr[n-2] |  arr[n-1]"
function pairORSum(arr, n)
{
    var ans = 0; // Initialize result

    // Consider all pairs (arr[i], arr[j) such that
    // i < j
    for (var i = 0; i < n; i++)
        for (var j = i + 1; j < n; j++)
            ans += arr[i] | arr[j];

    return ans;
}

// Driver program to test above function
var arr = [1, 2, 3, 4];
var n = arr.length;
document.write( pairORSum(arr, n));

</script>
```

**输出:**

```
27
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:0(1)

一个**高效解**可以在 O(n)时间内解决这个问题。这里的假设是整数用 32 位表示。
其思想是在每第 I 个位置(i > =0 & & i < =31)计数设定位数。如果两个数中对应的位都等于 1，则两个数的“与”的任意第 I 位都是 1。
设 **k1** 为第 I 个位置的设定位数。具有第 I 个设置位的总对数将是<sup>k1</sup>C<sub>2</sub>= k1 *(k1-1)/2(计数 k1 意味着有 k1 个数具有第 I 个设置位)。每对加 2 <sup>i</sup> 到总和。类似地，总 k0 值在第 I 个位置没有设置位。现在每个元素(没有在第 I 个位置设置位)可以与 k1 个元素配对(即。在第 I 个位置设置了位的那些元素)，所以总共有 k1 * k0 对，并且每个这样的对还将 2 <sup>i</sup> 加到总和中。
**sum = sum+(1<<I)*(k1 *(k1-1)/2)+(1<<I)*(k1 * k0)**
这个思路类似于求所有对之间的位差之和[。
以下是上述办法的实施:](https://www.geeksforgeeks.org/sum-of-bit-differences-among-all-pairs/) 

## C++

```
// An efficient C++ program to compute sum of bitwise OR
// of all pairs
#include <bits/stdc++.h>
using namespace std;
typedef long long int LLI;

// Returns value of "arr[0] | arr[1] + arr[0] | arr[2] +
// ... arr[i] | arr[j] + ..... arr[n-2] | arr[n-1]"

LLI pairORSum(LLI arr[], LLI n)
{

    LLI ans = 0; // Initialize result
    // Traverse over all bits
    for (LLI i = 0; i < 32; i++) {
        // Count number of elements with the i'th bit set(ie., 1)
        LLI k1 = 0; // Initialize the count

        // Count number of elements with i’th bit not-set(ie., 0) `
        LLI k0 = 0; // Initialize the count

        for (LLI j = 0; j < n; j++) {

            if ((arr[j] & (1 << i))) // if i'th bit is set
                k1++;
            else
                k0++;
        }
        // There are k1 set bits, means k1(k1-1)/2 pairs. k1C2
        // There are k0 not-set bits and k1 set bits so total pairs will be k1*k0.

        // Every pair adds 2^i to the answer. Therefore,

        ans = ans + (1 << i) * (k1 * (k1 - 1) / 2) + (1 << i) * (k1 * k0);
    }

    return ans;
}

// Driver program to test the above function

int main()

{

    LLI arr[] = { 1, 2, 3, 4 };

    LLI n = sizeof(arr) / sizeof(arr[0]);

    cout << pairORSum(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to compute
// sum of bitwise OR of all pairs
import java.io.*;

class GFG {

    // Returns value of "arr[0] | arr[1] + arr[0] | arr[2] +
    // ... arr[i] | arr[j] + ..... arr[n-2] | arr[n-1]"
    static int pairORSum(int arr[], int n)
    {
        int ans = 0; // Initialize result
        // Traverse over all bits
        for (int i = 0; i < 32; i++) {
            // Count number of elements with the ith bit set(ie., 1)
            int k1 = 0; // Initialize the count

            // Count number of elements with ith bit not-set(ie., 0) `
            int k0 = 0; // Initialize the count

            for (int j = 0; j < n; j++) {

                if ((arr[j] & (1 << i)) != 0) // if i'th bit is set
                    k1++;
                else
                    k0++;
            }
            // There are k1 set bits, means k1(k1-1)/2 pairs. k1C2
            // There are k0 not-set bits and k1 set bits so total pairs will be k1*k0.
            // Every pair adds 2^i to the answer. Therefore,

            ans = ans + (1 << i) * (k1 * (k1 - 1) / 2) + (1 << i) * (k1 * k0);
        }

        return ans;
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4 };
        int n = arr.length;
        System.out.println(pairORSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# An efficient Python 3 program to
# compute the sum of bitwise OR of all pairs

# Returns value of "arr[0] | arr[1] + arr[0] | arr[2] +
# ... arr[i] | arr[j] + ..... arr[n-2] | arr[n-1]"

def pairORSum(arr, n) :
    # Initialize result
    ans = 0
    # Traverse over all bits
    for i in range(0, 32) :
        # Count number of elements with the i'th bit set(ie., 1)
        k1 = 0

        # Count number of elements with i’th bit not-set(ie., 0) `
        k0 = 0

        for j in range(0, n) :

            if( (arr[j] & (1<<i)) ):   # if i'th bit is set
                k1 = k1 + 1

            else :
                k0 = k0 + 1
        # There are k1 set bits, means k1(k1-1)/2 pairs. k1C2
        # There are k0 not-set bits and k1 set bits so total pairs will be k1 * k0.

        # Every pair adds 2 ^ i to the answer. Therefore,

        ans = ans + (1<<i) * (k1*(k1-1)//2) + (1<<i) * (k1 * k0)

    return ans

# Driver program to test above function
arr = [1, 2, 3, 4]
n = len(arr)
print(pairORSum(arr, n))
```

## C#

```
// An efficient C# program to compute
// sum of bitwise OR of all pairs
using System;

class GFG {

    // Returns value of "arr[0] | arr[1] + arr[0] | arr[2] +
    // ... arr[i] | arr[j] + ..... arr[n-2] | arr[n-1]"
    static int pairORSum(int[] arr, int n)
    {
        int ans = 0; // Initialize result
        // Traverse over all bits
        for (int i = 0; i < 32; i++) {
            // Count number of elements with the ith bit set(ie., 1)
            int k1 = 0; // Initialize the count

            // Count number of elements with ith bit not-set(ie., 0) `
            int k0 = 0; // Initialize the count

            for (int j = 0; j < n; j++) {
                // if i'th bit is set
                if ((arr[j] & (1 << i)) != 0)
                    k1++;
                else
                    k0++;
            }
            // There are k1 set bits, means k1(k1-1)/2 pairs. k1C2
            // There are k0 not-set bits and k1 set bits so total pairs will be k1*k0.
            // Every pair adds 2^i to the answer. Therefore,

            ans = ans + (1 << i) * (k1 * (k1 - 1) / 2) + (1 << i) * (k1 * k0);
        }

        return ans;
    }

    // Driver program to test above function
    public static void Main()
    {
        int[] arr = new int[] { 1, 2, 3, 4 };
        int n = arr.Length;

        Console.Write(pairORSum(arr, n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program to compute
// sum of bitwise OR of all pairs

// Returns value of "arr[0] | arr[1] + arr[0] | arr[2] +
// ... arr[i] | arr[j] + ..... arr[n-2] | arr[n-1]"

function pairORSum($arr, $n)
{
    $ans = 0; // Initialize result
    // Traverse over all bits
    for ( $i = 0; $i < 32; $i++){
        // Count number of elements with the ith bit set(ie., 1)
        $k1 = 0; // Initialize the count

        // Count number of elements with ith bit not-set(ie., 0) `
        $k0 = 0; // Initialize the count

        for ( $j = 0; $j < $n; $j++){

            if ( ($arr[$j] & (1 << $i)))  // if i'th bit is set
                $k1++;
            else
                $k0++;
    }
    // There are k1 set bits, means k1(k1-1)/2 pairs. k1C2
    // There are k0 not-set bits and k1 set bits so total pairs will be k1*k0.
    // Every pair adds 2^i to the answer. Therefore,

    $ans = $ans + (1<<$i) * ($k1*($k1-1)/2) + (1<<$i) * ($k1*$k0) ;

}

return $ans;

}

    // Driver Code
    $arr = array(1, 2, 3, 4);
    $n = sizeof($arr);
    echo pairORSum($arr, $n) ;

?>
```

## java 描述语言

```
<script>

// An efficient Javascript program
// to compute sum of bitwise OR
// of all pairs

// Returns value of "arr[0] | arr[1] + arr[0] | arr[2] +
// ... arr[i] | arr[j] + ..... arr[n-2] | arr[n-1]"

function pairORSum( arr, n)
{

    var ans = 0; // Initialize result
    // Traverse over all bits
    for (var i = 0; i < 32; i++) {
        // Count number of elements
        // with the i'th bit set(ie., 1)
        var k1 = 0; // Initialize the count

        // Count number of elements with
        // i’th bit not-set(ie., 0) `
        var k0 = 0; // Initialize the count

        for (var j = 0; j < n; j++) {

            if ((arr[j] & (1 << i))) // if i'th bit is set
                k1++;
            else
                k0++;
        }
        // There are k1 set bits,
        // means k1(k1-1)/2 pairs. k1C2
        // There are k0 not-set bits and
        // k1 set bits so total pairs will be k1*k0.

        // Every pair adds 2^i to the answer. Therefore,

        ans = ans + (1 << i) * (k1 * (k1 - 1) / 2) +
        (1 << i) * (k1 * k0);
    }

    return ans;
}

// Driver program to test the above function
var arr = [1, 2, 3, 4];
var n = arr.length;
document.write( pairORSum(arr, n));

</script>
```

**输出**:

```
27
```

时间复杂度:0(n * 32)

辅助空间:0(1)