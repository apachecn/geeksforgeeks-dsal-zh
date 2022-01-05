# 数组中的总对，其中 LSB 的按位“与”、按位“或”和按位“异或”为 1

> 原文:[https://www . geesforgeks . org/total-pairs-in-a-array-so-LSB 的逐位或逐位异或-is-1/](https://www.geeksforgeeks.org/total-pairs-in-an-array-such-that-the-bitwise-and-bitwise-or-and-bitwise-xor-of-lsb-is-1/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找到配对的数量 **(arr[i]，arr[j])** 为**CNT 和**， **cntOR** 和 **cntXOR** ，这样:

1.  **cntAND:** 最低有效位按位“与”为 1 的对的计数。
2.  **cntOR:** 最低有效位按位“或”为 1 的对的计数。
3.  **cntXOR:** 最低有效位按位异或为 1 的对的计数。

**例:**

> **输入:** arr[] = {1，2，3}
> **输出:**
> cntXOR = 2
> cntAND = 1
> cntOR = 3
> 二进制数组元素为{01，10，11}
> 总计 XOR 对:2 即(1，2)和(2，3)
> 总计 AND 对:1 即(1，3)
> 总计 OR 对:3 即(T0)

**进场:**

1.  要得到数组元素的 **LSB** ，首先我们计算全部的偶、奇元素。偶数元素的 LSB 为 0，奇数元素的 LSB 为 1。
2.  为了
    *   **异或为 1** ，两个元素的 LSB 必须不同。
    *   **AND 为 1** ，两个元素的 LSB 都必须为 1。
    *   **OR 为 1** ，至少有一个元素的 LSB 应该为 1。
3.  因此，所需对的总数
    *   **表示 xorg:**CNT xor = CNT odd * CNT even
    *   **用于 AND:**cntAND = cntOdd *(cntOdd–1)/2
    *   **表示 or:**CNT =(CNT odd * CNT even)+CNT odd *(CNT odd–1)/2

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of required pairs
void CalculatePairs(int a[], int n)
{

    // To store the count of elements which
    // give remainder 0 i.e. even values
    int cnt_zero = 0;

    // To store the count of elements which
    // give remainder 1 i.e. odd values
    int cnt_one = 0;

    for (int i = 0; i < n; i++) {

        if (a[i] % 2 == 0)
            cnt_zero += 1;
        else
            cnt_one += 1;
    }

    long int total_XOR_pairs = cnt_zero * cnt_one;
    long int total_AND_pairs = (cnt_one) * (cnt_one - 1) / 2;
    long int total_OR_pairs = cnt_zero * cnt_one
                              + (cnt_one) * (cnt_one - 1) / 2;

    cout << "cntXOR = " << total_XOR_pairs << endl;
    cout << "cntAND = " << total_AND_pairs << endl;
    cout << "cntOR = " << total_OR_pairs << endl;
}

// Driver code
int main()
{
    int a[] = { 1, 3, 4, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    CalculatePairs(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to find the count of required pairs
    static void CalculatePairs(int a[], int n)
    {

        // To store the count of elements which
        // give remainder 0 i.e. even values
        int cnt_zero = 0;

        // To store the count of elements which
        // give remainder 1 i.e. odd values
        int cnt_one = 0;

        for (int i = 0; i < n; i++) {

            if (a[i] % 2 == 0)
                cnt_zero += 1;
            else
                cnt_one += 1;
        }

        int total_XOR_pairs = cnt_zero * cnt_one;
        int total_AND_pairs = (cnt_one) * (cnt_one - 1) / 2;
        int total_OR_pairs = cnt_zero * cnt_one
                             + (cnt_one) * (cnt_one - 1) / 2;

        System.out.println("cntXOR = " + total_XOR_pairs);
        System.out.println("cntAND = " + total_AND_pairs);
        System.out.println("cntOR = " + total_OR_pairs);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 1, 3, 4, 2 };
        int n = a.length;

        CalculatePairs(a, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find number of pairs

# Function to find the count of required pairs
def CalculatePairs(a, n):

    # To store the count of elements which
    # give remainder 0 i.e. even values
    cnt_zero = 0

    # To store the count of elements which
    # give remainder 1 i.e. odd values
    cnt_one = 0

    for i in range(0, n):
        if (a[i] % 2 == 0):
            cnt_zero += 1
        else:
            cnt_one += 1

    total_XOR_pairs = cnt_zero * cnt_one
    total_AND_pairs = (cnt_one) * (cnt_one - 1) / 2
    total_OR_pairs = cnt_zero * cnt_one + (cnt_one) * (cnt_one - 1) / 2

    print("cntXOR = ", int(total_XOR_pairs))
    print("cntAND = ", int(total_AND_pairs))
    print("cntOR = ", int(total_OR_pairs))

# Driver code
if __name__ == '__main__':

    a = [1, 3, 4, 2]
    n = len(a)

    # Print the count
    CalculatePairs(a, n)
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to find the count of required pairs
    static void CalculatePairs(int[] a, int n)
    {

        // To store the count of elements which
        // give remainder 0 i.e. even values
        int cnt_zero = 0;

        // To store the count of elements which
        // give remainder 1 i.e. odd values
        int cnt_one = 0;

        for (int i = 0; i < n; i++) {

            if (a[i] % 2 == 0)
                cnt_zero += 1;
            else
                cnt_one += 1;
        }

        int total_XOR_pairs = cnt_zero * cnt_one;
        int total_AND_pairs = (cnt_one) * (cnt_one - 1) / 2;
        int total_OR_pairs = cnt_zero * cnt_one
                             + (cnt_one) * (cnt_one - 1) / 2;

        Console.WriteLine("cntXOR = " + total_XOR_pairs);
        Console.WriteLine("cntAND = " + total_AND_pairs);
        Console.WriteLine("cntOR = " + total_OR_pairs);
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 1, 3, 4, 2 };
        int n = a.Length;

        // Print the count
        CalculatePairs(a, n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find the count of required pairs
function CalculatePairs($a, $n)
{

    // To store the count of elements which
    // give remainder 0 i.e. even values
    $cnt_zero = 0;

    // To store the count of elements which
    // give remainder 1 i.e. odd values
    $cnt_one = 0;

    for ($i = 0; $i < $n; $i++) {

        if ($a[$i] % 2 == 0)
            $cnt_zero += 1;
        else
            $cnt_one += 1;
    }

    $total_XOR_pairs = $cnt_zero * $cnt_one;
    $total_AND_pairs = ($cnt_one) * ($cnt_one - 1) / 2;
    $total_OR_pairs = $cnt_zero * $cnt_one
+ ($cnt_one) * ($cnt_one - 1) / 2;

    echo("cntXOR = $total_XOR_pairs\n");
    echo("cntAND = $total_AND_pairs\n");
    echo("cntOR = $total_OR_pairs\n");
}

// Driver code
$a = array(1, 3, 4, 2);
$n = count($a);

// Print the count
CalculatePairs($a, $n);
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find the count of required pairs
function CalculatePairs(a, n)
{

    // To store the count of elements which
    // give remainder 0 i.e. even values
    let cnt_zero = 0;

    // To store the count of elements which
    // give remainder 1 i.e. odd values
    let cnt_one = 0;

    for (let i = 0; i < n; i++) {

        if (a[i] % 2 == 0)
            cnt_zero += 1;
        else
            cnt_one += 1;
    }

    let total_XOR_pairs = cnt_zero * cnt_one;
    let total_AND_pairs = (cnt_one) * (cnt_one - 1) / 2;
    let total_OR_pairs = cnt_zero * cnt_one
                            + (cnt_one) * (cnt_one - 1) / 2;

    document.write("cntXOR = " + total_XOR_pairs + "<br>");
    document.write("cntAND = " + total_AND_pairs + "<br>");
    document.write("cntOR = " + total_OR_pairs + "<br>");
}

// Driver code

    let a = [ 1, 3, 4, 2 ];
    let n = a.length;

    CalculatePairs(a, n);

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
cntXOR = 4
cntAND = 1
cntOR = 5
```

**时间复杂度:** O(N)