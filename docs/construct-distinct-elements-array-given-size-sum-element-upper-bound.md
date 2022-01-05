# 构造一个给定大小、和和元素上限的不同元素数组

> 原文:[https://www . geesforgeks . org/construct-distinct-elements-array-size-sum-element-upper-bound/](https://www.geeksforgeeks.org/construct-distinct-elements-array-given-size-sum-element-upper-bound/)

给定原始数组的 **N** 大小、 **SUM** 数组中所有元素的总和以及 **K** 使得数组中没有元素大于 K，构造数组中所有元素唯一的原始数组。如果没有解决方案，打印“不可能”。
注意:所有元素应为正。
**示例:**

```
Input : N = 3, SUM = 15, K = 8  
Output: array[] = {1, 6, 8} 
The constructed array has size 3, sum
15 and all elements are smaller than
or equal to 8.

Input : N = 2,  SUM = 9, K = 10  
Output: array[]={1, 8} 

Input  : N = 3, SUM = 23, K = 8  
Output : Not Possible
```

我们必须选择 N 个元素，所有元素必须是正的，任何元素都不能大于 k。由于元素是正的和不同的，最小可能和等于前 N 个自然数的和，即 N * (N + 1)/2。
由于所有元素应小于或等于 K，最大可能和为 K + (K-1) + (K-2) + …..+ (K-N+1) = (N*K)- (N*(N-1))/2。
所以如果给定的和在最小和最大可能和之间，那么只能形成数组，否则我们必须打印-1。
下面是完整的算法，如果构建阵列是可行的。
1。创建一个大小为 N 的数组，并用前 N 个数字填充它。所以数组的总和将是最小的可能总和。
2。找到数组中最大的元素，但是由于数组是排序的，所以数组[N]将是最大的。

*   如果最大元素小于 K，我们用 K 替换它，并检查数组的新和。
    *   如果它小于给定的 SUM，我们移动到数组中的 N-1 位置，因为数组[N]不能进一步递增，为了保持唯一性，我们将 K 减少 1。
    *   如果它大于给定的和，我们替换一个元素，这样和将被给定和，并且将脱离循环。
*   如果最大的元素等于 K，我们移动到数组中的 N-1 位置，因为数组[N]不能进一步递增，为了保持唯一性，我们将 K 减少 1。

3.打印数组。

## C++

```
// CPP program to construct a distinct element
// array with given size, sum, element upper
// bound and all elements positive
#include <bits/stdc++.h>
using namespace std;

void printArray(int N, int SUM, int K)
{
    // smallest possible sum
    int minSum = (N * (N + 1)) / 2;

    // largest possible sum
    int maxSum = (N * K) - (N * (N - 1)) / 2;

    if (minSum > SUM || maxSum < SUM) {
        printf("Not Possible");
        return;
    }

    // Creating array with minimum possible
    // sum.
    int arr[N + 1];
    for (int i = 1; i <= N; i++)
        arr[i] = i;
    int sum = minSum;

    // running the loop from last because the
    // array is sorted and running from last
    // will give largest numbers
    for (int i = N; i >= 1; i--) {

        // replacing i with K, Note arr[i] = i
        int x = sum + (K - i);
        if (x < SUM) {
            sum = sum + (K - i);
            arr[i] = K; // can't be incremented further
            K--; // to maintain uniqueness
        }

        else {

            // directly replacing with a suitable
            // element to make sum as given sum
            arr[i] += (SUM - sum);
            sum = SUM;
            break;
        }
    }

    for (int i = 1; i <= N; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int N = 3, SUM = 15, K = 8;
    printArray(N, SUM, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct a distinct element
// array with given size, sum, element upper
// bound and all elements positive

import java.io.*;

class GFG {
    static void printArray(int N, int SUM, int K)
    {
        // smallest possible sum
        int minSum = (N * (N + 1)) / 2;

        // largest possible sum
        int maxSum = (N * K) - (N * (N - 1)) / 2;

        if (minSum > SUM || maxSum < SUM) {
            System.out.println("Not Possible");
            return;
        }

        // Creating array with
        // minimum possible sum.
        int arr[] = new int[N + 1];
        for (int i = 1; i <= N; i++)
            arr[i] = i;

        int sum = minSum;

        // running the loop from last because the
        // array is sorted and running from last
        // will give largest numbers
        for (int i = N; i >= 1; i--) {

            // replacing i with K, Note arr[i] = i
            int x = sum + (K - i);
            if (x < SUM) {
                sum = sum + (K - i);

                // can't be incremented further
                arr[i] = K;

                // to maintain uniqueness
                K--;
            }

            else {

                // directly replacing with a suitable
                // element to make sum as given sum
                arr[i] += (SUM - sum);
                sum = SUM;
                break;
            }
        }

        for (int i = 1; i <= N; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 3, SUM = 15, K = 8;
        printArray(N, SUM, K);
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to construct a distinct
# element array with given size, sum,
# element upper bound and all elements
# positive
def printArray(N, SUM, K):

    # smallest possible sum
    minSum = (N * (N + 1)) / 2

    # largest possible sum
    maxSum = (N * K) - (N * (N - 1)) / 2

    if (minSum > SUM or maxSum < SUM):
        print("Not Possible")
        return

    # Creating array with minimum
    # possible sum.
    arr = [0 for i in range(N + 1)]
    for i in range(1, N + 1, 1):
        arr[i] = i
    sum = minSum

    # running the loop from last because
    # the array is sorted and running
    # from last will give largest numbers
    i = N
    while(i >= 1):

        # replacing i with K, Note arr[i] = i
        x = sum + (K - i)
        if (x < SUM):
            sum = sum + (K - i)
            arr[i] = K

            # can't be incremented further
            K -= 1

            # to maintain uniqueness
        else:

            # directly replacing with a suitable
            # element to make sum as given sum
            arr[i] += (SUM - sum)
            sum = SUM
            break
        i -= 1

    for i in range(1, N + 1, 1):
        print(int(arr[i]), end = " ")

# Driver code
if __name__ == '__main__':
    N = 3
    SUM = 15
    K = 8
    printArray(N, SUM, K)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to construct a distinct element
// array with given size, sum, element upper
// bound and all elements positive
using System;

class GFG {

    static void printArray(int N, int SUM, int K)
    {

        // smallest possible sum
        int minSum = (N * (N + 1)) / 2;

        // largest possible sum
        int maxSum = (N * K) - (N * (N - 1)) / 2;

        if (minSum > SUM || maxSum < SUM) {
            Console.WriteLine("Not Possible");
            return;
        }

        // Creating array with
        // minimum possible sum.
        int[] arr = new int[N + 1];
        for (int i = 1; i <= N; i++)
            arr[i] = i;

        int sum = minSum;

        // running the loop from last because the
        // array is sorted and running from last
        // will give largest numbers
        for (int i = N; i >= 1; i--) {

            // replacing i with K, Note arr[i] = i
            int x = sum + (K - i);

            if (x < SUM) {
                sum = sum + (K - i);

                // can't be incremented further
                arr[i] = K;

                // to maintain uniqueness
                K--;
            }

            else {

                // directly replacing with a suitable
                // element to make sum as given sum
                arr[i] += (SUM - sum);
                sum = SUM;
                break;
            }
        }

        for (int i = 1; i <= N; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main()
    {

        int N = 3, SUM = 15, K = 8;

        printArray(N, SUM, K);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to construct a distinct element
// array with given size, sum, element upper
// bound and all elements positive

function printArray($N, $SUM, $K)
{
    // smallest possible sum
    $minSum = ($N * ($N + 1)) / 2;

    // largest possible sum
    $maxSum = ($N * $K) - ($N * ($N - 1)) / 2;

    if ($minSum > $SUM || $maxSum < $SUM) {
        echo"Not Possible";
        return;
    }

    // Creating array with minimum possible
    // sum.
     $arr = array();
    for ($i = 1; $i <= $N; $i++)
        $arr[$i] = $i;
      $sum = $minSum;

    // running the loop from last because the
    // array is sorted and running from last
    // will give largest numbers
    for ($i = $N; $i >= 1; $i--) {

        // replacing i with K, Note arr[i] = i
        $x = $sum + ($K - $i);
        if ($x <$SUM) {
            $sum = $sum + ($K - $i);
            $arr[$i] =$K; // can't be incremented further
            $K--; // to maintain uniqueness
        }

        else {

            // directly replacing with a suitable
            // element to make sum as given sum
            $arr[$i] += ($SUM - $sum);
            $sum = $SUM;
            break;
        }
    }

    for ($i = 1; $i <= $N; $i++)
        echo $arr[$i] , " ";
}

// Driver code
    $N = 3; $SUM = 15;$K = 8;
    printArray($N, $SUM, $K);
// This code is contributed by inder_verma..

?>
```

## java 描述语言

```
<script>
// JavaScript program to construct a distinct element
// array with given size, sum, element upper
// bound and all elements positive

function printArray(N, SUM, K)
{
    // smallest possible sum
    let minSum = Math.floor((N * (N + 1)) / 2);

    // largest possible sum
    let maxSum = (N * K) - Math.floor((N * (N - 1)) / 2);

    if (minSum > SUM || maxSum < SUM) {
        document.write("Not Possible");
        return;
    }

    // Creating array with minimum possible
    // sum.
    let arr = new Array(N + 1);
    for (let i = 1; i <= N; i++)
        arr[i] = i;
    let sum = minSum;

    // running the loop from last because the
    // array is sorted and running from last
    // will give largest numbers
    for (let i = N; i >= 1; i--) {

        // replacing i with K, Note arr[i] = i
        let x = sum + (K - i);
        if (x < SUM) {
            sum = sum + (K - i);
            arr[i] = K; // can't be incremented further
            K--; // to maintain uniqueness
        }

        else {

            // directly replacing with a suitable
            // element to make sum as given sum
            arr[i] += (SUM - sum);
            sum = SUM;
            break;
        }
    }

    for (let i = 1; i <= N; i++)
        document.write(arr[i] + " ");
}

// Driver code
    let N = 3, SUM = 15, K = 8;
    printArray(N, SUM, K);

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
1 6 8
```

**时间复杂度:** O(N)