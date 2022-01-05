# 查询所有子阵列的异或运算

> 原文:[https://www . geeksforgeeks . org/所有子阵列的 xor 上的查询/](https://www.geeksforgeeks.org/queries-on-xor-of-xors-of-all-subarrays/)

给定一个由 **n** 个整数组成的数组 **A** ，比如 A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，…，A <sub>n</sub> 。您将获得 **Q** 查询表单**【l，r】**。任务是找出一个数组中所有子数组的异或运算，该数组包含元素 A <sub>l</sub> ，A <sub>l+1</sub> ，…..，A <sub>r</sub> 。
**举例:**

```
Input : A[] = { 1, 2, 3, 4, 5 }, Q = 3
        q1 = { 1, 2 }
        q2 = { 1, 3 }
        q3 = { 2, 4 }
Output : 0
         2
         6
For query 1, the extracted array is [1, 2] and 
subarrays of the array is [1], [2], [1, 2]. 
So, the answer is (1) ⊕  (2) ⊕  (1 ⊕ 2) = 0.
For query 2, the extracted array is [1, 2, 3] and 
subarrays of the array is
[1], [2], [1, 2], [2, 3], [1, 2, 3]. 
So the answer is (1) ⊕  (2) ⊕  (3) ⊕ (1 ⊕  2) ⊕  
                 (2 ⊕  3) ⊕  (1 ⊕  2 ⊕  3) = 2.
For query 3, the extracted array is [2, 3, 4] and 
subarrays of the array is 
[2], [3], [4], [2, 3], [3, 4], [2, 3, 4].
So the answer is (2) ⊕ (3) ⊕  (4) ⊕  (2 ⊕  3) ⊕  
                 (3 ⊕  4) ⊕  (2 ⊕  3 ⊕  4) = 6.

Input : A[] = { 5, 8, 9, 1, 7 }, Q = 3
        query1 = { 1, 3 }
        query2 = { 3, 4 }
        query3 = { 2, 5 }
Output : 12
         0
         0
```

首先回忆一下 XOR 的性质，
1。x ⊕ x = 0
2。如果 x ⊕ y = z，那么 x = y ⊕ z
利用第一个性质，我们可以说任意数 x XORed 的偶数次将得到 0，奇数次将得到 x.
如果我们想求一个数组的所有子数组的 xor 的 XOPR，我们需要求在所有子数组中总共出现奇数次的元素。
假设我们有一个数组[1，2，3]。它的子阵列将是[1]，[2]，[3]，[1，2]，[2，3]，[1，2，3]。
1 共发生 3 次。
2 共发生 4 次。
3 共发生 3 次。
我们可以观察到，在第 i <sup>个</sup>索引处的数字将具有(I+1)x(sizeofarray–I)个频率。
如果一个数组有奇数个整数，从第一个元素开始，每个替换元素在所有子数组中总共出现奇数次。因此，所有子阵列的异或将是阵列中交替元素的异或。
如果一个数组有偶数个整数，那么每个元素在所有子数组中总共出现偶数次。因此，所有子阵列的异或将始终为 0。
为每个查询遍历数组是低效的。我们可以将 xor 的值存储到每个元素，方法是使用递归将它与替换元素进行 xor 运算
prefix _ xor[I]= a[I]⊕prefix _ xor[I–2]
对于每个查询，我们的起始索引为 l，结束索引为 r。如果(r–l+1)为奇数，答案将是 prefix _ xor[r]⊕prefix _ xor[l–2]。
以下是本办法的实施情况:

## C++

```
// CPP Program to answer queries on XOR of XORs
// of all subarray
#include <bits/stdc++.h>
#define N 100
using namespace std;

// Output for each query
void ansQueries(int prefeven[], int prefodd[],
                                 int l, int r)
{
    // If number of element is even.
    if ((r - l + 1) % 2 == 0)
        cout << "0";

    // If number of element is odd.
    else {

        // if l is even
        if (l % 2 == 0)
            cout << (prefeven[r] ^ prefeven[l - 1]);

        // if l is odd
        else
            cout << (prefodd[r] ^ prefodd[l - 1]);
    }

    cout << endl;
}

// Wrapper Function
void wrapper(int arr[], int n, int l[], int r[], int q)
{
    int prefodd[N] = { 0 }, prefeven[N] = { 0 };

    // Evaluating prefixodd and prefixeven
    for (int i = 1; i <= n; i++) {
        if ((i) % 2 == 0) {
            prefeven[i] = arr[i - 1] ^ prefeven[i - 1];
            prefodd[i] = prefodd[i - 1];
        }
        else {
            prefeven[i] = prefeven[i - 1];
            prefodd[i] = prefodd[i - 1] ^ arr[i - 1];
        }
    }

    int i = 0;
    while (i != q) {
        query(prefeven, prefodd, l[i], r[i]);
        i++;
    }
}

// Driven Program
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int l[] = { 1, 1, 2 };
    int r[] = { 2, 3, 4 };
    int q = sizeof(l) / sizeof(l[0]);

    ansQueries(arr, n, l, r, q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Queries on XOR
// of XORs of all subarrays
import java.util.*;

class GFG {

    // Output for each query
    static void ansQueries(int prefeven[],
                           int prefodd[],
                           int l, int r)
    {
        // If number of element is even.
        if ((r - l + 1) % 2 == 0)
            System.out.println("0");

        // If number of element is odd.
        else
        {
            // if l is even
            if (l % 2 == 0)
                System.out.println(prefeven[r] ^
                                prefeven[l - 1]);

            // if l is odd
            else
                System.out.println(prefodd[r] ^
                                 prefodd[l - 1]);
        }
    }

    // Wrapper Function
    static void wrapper(int arr[], int n,
                        int l[], int r[],
                                   int q)
    {
        int prefodd[] = new int[100];
        int prefeven[] = new int[100];

        // Evaluating prefixodd
        // and prefixeven
        for (int i = 1; i <= n; i++) {

            if ((i) % 2 == 0) {

                prefeven[i] = arr[i - 1] ^
                             prefeven[i - 1];

                prefodd[i] = prefodd[i - 1];
            }
            else
            {
                prefeven[i] = prefeven[i - 1];
                prefodd[i] = prefodd[i - 1] ^
                             arr[i - 1];
            }
        }

        int i = 0;

        while (i != q){

            ansQueries(prefeven, prefodd,
                             l[i], r[i]);
            i++;
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 4 , 5};
        int n = arr.length;

        int l[] = {1, 1, 2};
        int r[] = {2, 3, 4};
        int q = l.length;

        wrapper(arr, n, l, r, q);
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 Program to answer queries on
# XOR of XORs of all subarray
N = 100

# Output for each query
def ansQueries(prefeven, prefodd, l, r):

    # If number of element is even.
    if ((r - l + 1) % 2 == 0):
        print("0")

    # If number of element is odd.
    else :

        # if l is even
        if (l % 2 == 0):
            print(prefeven[r] ^
                  prefeven[l - 1])

        # if l is odd
        else:
            print(prefodd[r] ^
                  prefodd[l - 1])

# Wrapper Function
def wrapper(arr, n, l, r, q):

    prefodd = [0] * N
    prefeven = [0] * N

    # Evaluating prefixodd and prefixeven
    for i in range(1, n + 1) :
        if ((i) % 2 == 0) :
            prefeven[i] = arr[i - 1] ^ prefeven[i - 1]
            prefodd[i] = prefodd[i - 1]

        else :
            prefeven[i] = prefeven[i - 1]
            prefodd[i] = prefodd[i - 1] ^ arr[i - 1]

    i = 0
    while (i != q) :
        ansQueries(prefeven, prefodd, l[i], r[i])
        i += 1

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5 ]
    n = len(arr)

    l = [ 1, 1, 2 ]
    r = [ 2, 3, 4 ]
    q = len(l)

    wrapper(arr, n, l, r, q)

# This code is contributed by ita_c
```

## C#

```
// C# code for Queries on XOR
// of XORs of all subarrays
using System;

class GFG {

    // Output for each query
    static void ansQueries(int[] prefeven,
                           int[] prefodd,
                           int l, int r)
    {
        // If number of element is even.
        if ((r - l + 1) % 2 == 0)
            Console.WriteLine("0");

        // If number of element is odd.
        else {
            // if l is even
            if (l % 2 == 0)
                Console.WriteLine(prefeven[r] ^ prefeven[l - 1]);

            // if l is odd
            else
                Console.WriteLine(prefodd[r] ^ prefodd[l - 1]);
        }
    }

    // Wrapper Function
    static void wrapper(int[] arr, int n,
                        int[] l, int[] r,
                        int q)
    {
        int[] prefodd = new int[100];
        int[] prefeven = new int[100];

        // Evaluating prefixodd
        // and prefixeven
        for (int i = 1; i <= n; i++) {

            if ((i) % 2 == 0) {

                prefeven[i] = arr[i - 1] ^ prefeven[i - 1];

                prefodd[i] = prefodd[i - 1];
            }
            else {
                prefeven[i] = prefeven[i - 1];
                prefodd[i] = prefodd[i - 1] ^ arr[i - 1];
            }
        }

        int j = 0;

        while (j != q) {

            ansQueries(prefeven, prefodd,
                    l[j], r[j]);
            j++;
        }
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;

        int[] l = { 1, 1, 2 };
        int[] r = { 2, 3, 4 };
        int q = l.Length;

        wrapper(arr, n, l, r, q);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php Program to answer
// queries on XOR of XORs
// of all subarray
// Output for each query

function ansQueries($prefeven, $prefodd,
                                $l, $r)
{

    // If number of element is even.
    if (($r - $l + 1) % 2 == 0)
    {
        echo "0";
}

    // If number of element is odd.
    else {

        // if l is even
        if ($l % 2 == 0)
            echo ($prefeven[$r] ^
                  $prefeven[$l - 1]);

        // if l is odd
        else
            echo ($prefodd[$r] ^
                  $prefodd[$l - 1]);
    }

    echo "\n";
}

// Wrapper Function
function wrapper(array $arr, $n, array $l,
                            array $r, $q)
{
    $prefodd=array_fill(0,100,0);
    $prefeven=array_fill(0,100,0);

    // Evaluating prefixodd
    // and prefixeven
    for ($i = 1; $i <= $n; $i++)
    {
        if (($i) % 2 == 0)
        {
            $prefeven[$i] = $arr[$i - 1] ^
                        $prefeven[$i - 1];
            $prefodd[$i] = $prefodd[$i - 1];
        }
        else {
            $prefeven[$i] = $prefeven[$i - 1];
            $prefodd[$i] = $prefodd[$i - 1] ^
                                $arr[$i - 1];
        }
    }

    $i = 0;
    while ($i != $q) {
        ansQueries($prefeven, $prefodd,
                    $l[$i], $r[$i]);
        $i++;
    }
}

    // Driver code
    $arr = array ( 1, 2, 3, 4, 5 );
    $n = sizeof($arr) / sizeof($arr[0]);

    $l=array ( 1, 1, 2 );
    $r=array ( 2, 3, 4 );
    $q = sizeof($l) / sizeof($l[0]);

    wrapper($arr, $n, $l, $r, $q);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program for Queries on XOR
// of XORs of all subarrays

// Output for each query
    function ansQueries(prefeven,
                           prefodd,
                           l, r)
    {
        // If number of element is even.
        if ((r - l + 1) % 2 == 0)
            document.write("0");

        // If number of element is odd.
        else
        {
            // if l is even
            if (l % 2 == 0)
                document.write(prefeven[r] ^
                                prefeven[l - 1]) ;

            // if l is odd
            else
                document.write(prefodd[r] ^
                                 prefodd[l - 1] );
        }
        document.write( "<br/>");
    }

    // Wrapper Function
    function wrapper(arr, n,
                        l, r, q)
    {
        let prefodd = [];
        let prefeven = [];

        // Evaluating prefixodd
        // and prefixeven
        for (let i = 1; i <= n; i++) {

            if ((i) % 2 == 0) {

                prefeven[i] = arr[i - 1] ^
                             prefeven[i - 1];

                prefodd[i] = prefodd[i - 1];
            }
            else
            {
                prefeven[i] = prefeven[i - 1];
                prefodd[i] = prefodd[i - 1] ^
                             arr[i - 1];
            }
        }

        let i = 0;

        while (i != q){

            ansQueries(prefeven, prefodd,
                             l[i], r[i]);
            i++;
        }
    }

// Driver code

        let arr = [1, 2, 3, 4 , 5];
        let n = arr.length;

        let l = [1, 1, 2];
        let r = [2, 3, 4];
        let q = l.length;

        wrapper(arr, n, l, r, q);

</script>
```

**输出:**

```
0
2
6
```