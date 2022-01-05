# 仅打印数字 0 和 1 的数字，使其总和为 N

> 原文:[https://www . geesforgeks . org/print-numbers-with-digits-0-and-1-only-this-sum-is-n/](https://www.geeksforgeeks.org/print-numbers-with-digits-0-and-1-only-such-that-their-sum-is-n/)

给定一个数字 N，任务是找到只由 0 和 1 组成的所需数字，其和等于 N。
**示例:**

```
Input: 9 
Output: 1 1 1 1 1 1 1 1 1 
Only numbers smaller than or equal to 9 with 
digits 0 and 1 only are 0 and 1 itself.
So to get 9, we have to add 1 - 9 times.

Input: 31
Output: 11 10 10
```

**进场:**

1.  将产品 p 初始化为 1，将 m 初始化为零。
2.  创建存储 0 和 1 的结果整数计数的向量。
3.  循环 N 并检查 N 是否是 10 的倍数如果是，获取小数并通过乘以 10 来更新 p，并将该值存储在向量中，并将 N 减少 m。对每个小数执行此操作，并打印向量的总大小。
4.  最后遍历向量并打印元素。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers
int findNumbers(int N)
{
    // Initialize vector array that store
    // result.
    vector<int> v;

    // Get the each decimal and find its
    // count store in vector.
    while (N) {

        int n = N, m = 0, p = 1;
        while (n) {

            // find decimal
            if (n % 10)
              m += p;

            n /= 10;
            p *= 10;
        }

        v.push_back(m);

        // Decrement N by m for each decimal
        N -= m;
    }

    // Loop for each element of vector
    // And print its content.
    for (int i = 0; i < v.size(); i++)
        cout << " " << v[i];

    return 0;
}

// Driver code
int main()
{
    int N = 31;
    findNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

public class GfG{

    // Function to count the numbers
    public static int findNumbers(int N)
    {
        // Initialize vector array that store
        // result.
        ArrayList<Integer> v = new ArrayList<Integer>();

        // Get the each decimal and find its
        // count store in vector.
        while (N > 0) {

            int n = N, m = 0, p = 1;
            while (n > 0) {

                // find decimal
                if (n % 10 != 0)
                  m += p;

                n /= 10;
                p *= 10;
            }

            v.add(m);

            // Decrement N by m for each decimal
            N -= m;
        }

        // Loop for each element of vector
        // And print its content.
        for (int i = 0; i < v.size(); i++)
            System.out.print(" " + v.get(i));

        return 0;
    }

     public static void main(String []args){

        int N = 31;
        findNumbers(N);
     }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach

# Function to count the numbers
def findNumbers(N) :

    # Initialize vector array that
    # store result.
    v = [];

    # Get the each decimal and find
    # its count store in vector.
    while (N) :

        n, m, p = N, 0, 1
        while (n) :

            # find decimal
            if (n % 10) :
                m += p

            n //= 10
            p *= 10

        v.append(m);

        # Decrement N by m for
        # each decimal
        N -= m

    # Loop for each element of vector
    # And print its content.
    for i in range(len(v)) :
        print(v[i], end = " ")

# Driver Code
if __name__ == "__main__" :

    N = 31
    findNumbers(N)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GfG
{

    // Function to count the numbers
    public static int findNumbers(int N)
    {
        // Initialize vector array that store
        // result.
        ArrayList v = new ArrayList();

        // Get the each decimal and find its
        // count store in vector.
        while (N > 0)
        {
            int n = N, m = 0, p = 1;
            while (n > 0)
            {

                // find decimal
                if (n % 10 != 0)
                    m += p;

                n /= 10;
                p *= 10;
            }
            v.Add(m);

            // Decrement N by m for each decimal
            N -= m;
        }

        // Loop for each element of vector
        // And print its content.
        for (int i = 0; i < v.Count; i++)
            Console.Write(" " + v[i]);

        return 0;
    }

    // Driver code
    public static void Main()
    {
        int N = 31;
        findNumbers(N);
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to count the numbers
function findNumbers($N)
{
    // Initialize vector array
    // that store result.
    $v = array();

    // Get the each decimal and find
    // its count store in vector.
    while ($N)
    {

        $n = $N;
        $m = 0;
        $p = 1;
        while ($n)
        {

            // find decimal
            if ($n % 10)
            $m += $p;

            $n /= 10;
            $p *= 10;
        }

        array_push($v,$m);

        // Decrement N by m for
        // each decimal
        $N -= $m;
    }

    // Loop for each element of vector
    // And print its content.
    for ($i = 0; $i < sizeof($v); $i++)
        echo " " , $v[$i];

    return 0;
}

// Driver code
$N = 31;
findNumbers($N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to count the numbers
function findNumbers(N)
{
    // Initialize vector array that store
    // result.
    let v = [];

    // Get the each decimal and find its
    // count store in vector.
    while (N) {

        let n = N, m = 0, p = 1;
        while (n) {

            // find decimal
            if (n % 10)
              m += p;

            n = parseInt(n/10);
            p *= 10;
        }

        v.push(m);

        // Decrement N by m for each decimal
        N -= m;
    }

    // Loop for each element of vector
    // And print its content.
    for (let i = 0; i < v.length; i++)
        document.write(" " + v[i]);

    return 0;
}

// Driver code
let N = 31;
findNumbers(N);

// This code is contributed by souravmahato34.
</script>
```

**Output:** 

```
11 10 10
```

***时间复杂度** : O(log(N))*
***辅助空间** : O(log(N))*