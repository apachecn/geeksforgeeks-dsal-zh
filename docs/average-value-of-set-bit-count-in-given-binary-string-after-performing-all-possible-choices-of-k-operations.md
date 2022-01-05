# 在执行所有可能的 K 操作选择后，给定二进制串中设置的比特计数的平均值

> 原文:[https://www . geesforgeks . org/执行所有可能的 k 选择操作后给定二进制字符串中的集合位计数平均值/](https://www.geeksforgeeks.org/average-value-of-set-bit-count-in-given-binary-string-after-performing-all-possible-choices-of-k-operations/)

给定一个正整数 **N** 和一个由 **K** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，并考虑一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)(比如说 **S** )具有 **N** 个设定位， 任务是在对字符串 **S** 执行完所有可能的 **K** 操作选择后，找到[设定比特数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)的[平均值](https://www.geeksforgeeks.org/mean/)，从而在**I<sup>th</sup>T25】操作中，可以翻转 **N** 比特中的任意**arr【I】**比特。**

**示例:**

> **输入:** N = 3，arr[] = {2，2}
> **输出:** 1.6667
> **解释:**给定的二进制字符串有 N 个设置位，假设 S = ' **111** 。所有可能的移动顺序如下:
> 
> *   在第一次移动中，翻转位[0]和[1]。字符串将是“ **001**
>     *   在第二次移动中，翻转位[0]和[1]。字符串将为**‘111’**。
>     *   在第二次移动中，翻转位[1]和[2]。字符串将是“ **010** ”。
>     *   在第二次移动中，翻转位[0]和[2]。字符串将为“ **100** ”。
> *   在第一次移动中，翻转位[1]和[2]。字符串将为“ **100** ”。
>     *   在第二次移动中，翻转位[0]和[1]。字符串将是“ **010** ”。
>     *   在第二次移动中，翻转位[1]和[2]。字符串将为'**111′**。
>     *   在第二次移动中，翻转位[0]和[2]。字符串将是“ **001** ”。
> *   在第一次移动中，翻转位[0]和[2]。字符串将是“ **010** ”。
>     *   在第二次移动中，翻转位[0]和[1]。字符串将为“ **100** ”。
>     *   在第二次移动中，翻转位[1]和[2]。字符串将是“ **001** ”。
>     *   在第二次移动中，翻转位[0]和[2]。字符串将是“ **111** ”。
> 
> 因此，可能的不同操作的总数是 9，并且在所有情况下操作之后的设置位的计数是 15。所以，平均值将是 15/9 = 1.6667。
> 
> **输入:** N = 5，arr[] = {1，2，3 }
> T3】输出: 2.44

**方法:**利用[概率](https://www.geeksforgeeks.org/mathematics-probability/)的一些基本原理可以解决给定的问题。假设在**(I–1)<sup>第</sup>** 次操作后，平均设定位数的值为 **p** ，平均关闭位数的值为 **q** 。可以观察到 **p** 在 **i <sup>第</sup>** 次运算后的值将变为 p = p +翻转为设置位的平均关断位数–翻转为关断位的平均设置位数。由于选择字符串中位的概率是一样的，因此 **p** 的值可以计算为**p<sub>I</sub>= p<sub>I-1</sub>+q<sub>(I–1)</sub>*(arr[I]/N)–p<sub>(I–1)</sub>*(arr[I]/N)**。按照以下步骤解决给定的问题:

*   初始化两个变量，比如说 **p** 和 **q** ，最初， **p = N** 和 **q = 0** ，因为所有的位最初都是字符串中的设置位。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，并更新 **p** 和 **q** 的值，如下所示:
    *   **p =****p+q *(arr[I]/N)–p *(arr[I]/N)**的值。
    *   类似地，**q =****q+p *(arr[I/N)–q *(arr[I/N)**的值。
*   存储在 **p** 中的值是要求的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the average number
// of Set bits after after given operations
double averageSetBits(int N, int K, int arr[])
{
    // Stores the average number of set
    // bits after current operation
    double p = N;

    // Stores the average number of set
    // bits after current operation
    double q = 0;

    // Iterate through the array arr[] and
    // update the values of p and q

    for (int i = 0; i < K; i++) {

        // Store the value of p and q of the
        // previous state before their updation
        double _p = p, _q = q;

        // Update average number of set bits
        // after performing the ith operation
        p = _p - _p * arr[i] / N + _q * arr[i] / N;

        // Update average number of off bits
        // after performing the ith operation
        q = _q - _q * arr[i] / N + _p * arr[i] / N;
    }

    // Return Answer
    return p;
}

// Driver Code
int main()
{
    int N = 5;
    int arr[] = { 1, 2, 3 };
    int K = sizeof(arr) / sizeof(arr[0]);

    cout << setprecision(10)
         << averageSetBits(N, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to calculate the average number
    // of Set bits after after given operations
    static double averageSetBits(int N, int K, int arr[])
    {
        // Stores the average number of set
        // bits after current operation
        double p = N;

        // Stores the average number of set
        // bits after current operation
        double q = 0;

        // Iterate through the array arr[] and
        // update the values of p and q

        for (int i = 0; i < K; i++) {

            // Store the value of p and q of the
            // previous state before their updation
            double _p = p, _q = q;

            // Update average number of set bits
            // after performing the ith operation
            p = _p - _p * arr[i] / N + _q * arr[i] / N;

            // Update average number of off bits
            // after performing the ith operation
            q = _q - _q * arr[i] / N + _p * arr[i] / N;
        }

        // Return Answer
        return p;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;
        int arr[] = { 1, 2, 3 };
        int K = arr.length;

        System.out.println(String.format(
            "%.10f", averageSetBits(N, K, arr)));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate the average number
# of Set bits after after given operations
def averageSetBits(N, K, arr):

    # Stores the average number of set
    # bits after current operation
    p = N

    # Stores the average number of set
    # bits after current operation
    q = 0

    # Iterate through the array arr[] and
    # update the values of p and q

    for i in range(K):

        # Store the value of p and q of the
        # previous state before their updation
        _p = p
        _q = q

        # Update average number of set bits
        # after performing the ith operation
        p = _p - _p * arr[i] / N + _q * arr[i] / N

        # Update average number of off bits
        # after performing the ith operation
        q = _q - _q * arr[i] / N + _p * arr[i] / N

    # Return Answer
    return p

# Driver Code
if __name__ == "__main__":

    N = 5
    arr = [1, 2, 3]
    K = len(arr)

    print("%.2f" % averageSetBits(N, K, arr))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to calculate the average number
    // of Set bits after after given operations
    static double averageSetBits(int N, int K, int []arr)
    {

        // Stores the average number of set
        // bits after current operation
        double p = N;

        // Stores the average number of set
        // bits after current operation
        double q = 0;

        // Iterate through the array []arr and
        // update the values of p and q

        for (int i = 0; i < K; i++) {

            // Store the value of p and q of the
            // previous state before their updation
            double _p = p, _q = q;

            // Update average number of set bits
            // after performing the ith operation
            p = _p - _p * arr[i] / N + _q * arr[i] / N;

            // Update average number of off bits
            // after performing the ith operation
            q = _q - _q * arr[i] / N + _p * arr[i] / N;
        }

        // Return Answer
        return p;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 5;
        int []arr = { 1, 2, 3 };
        int K = arr.Length;

        Console.WriteLine(String.Format(
            "{0:F10}", averageSetBits(N, K, arr)));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to calculate the average number
       // of Set bits after after given operations
       function averageSetBits(N, K, arr)
       {

           // Stores the average number of set
           // bits after current operation
           let p = N;

           // Stores the average number of set
           // bits after current operation
           let q = 0;

           // Iterate through the array arr[] and
           // update the values of p and q

           for (let i = 0; i < K; i++) {

               // Store the value of p and q of the
               // previous state before their updation
               let _p = p, _q = q;

               // Update average number of set bits
               // after performing the ith operation
               p = _p - _p * arr[i] / N + _q * arr[i] / N;

               // Update average number of off bits
               // after performing the ith operation
               q = _q - _q * arr[i] / N + _p * arr[i] / N;
           }

           // Return Answer
           return p;
       }

       // Driver Code
       let N = 5;
       let arr = [1, 2, 3];
       let K = arr.length;

       document.write(averageSetBits(N, K, arr).toPrecision(3));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
2.44
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*