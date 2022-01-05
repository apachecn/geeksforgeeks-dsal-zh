# 找出正好有 4 个除数的第 n 个最小数

> 原文:[https://www . geeksforgeeks . org/find-n-最小数-正好有-4 个除数/](https://www.geeksforgeeks.org/find-nth-smallest-number-having-exactly-4-divisors/)

给定一个正整数 **N** ，任务是找到序列中第 **N** 个最小的数，这个数正好有**4**T6】个除数。

**示例:**

> **输入:** 4
> **输出:** 14
> **说明:**序列中有 4 个除数的数是 6，8，10，14，…，序列中的第四个数是 14。
> 
> **输入:**24
> T3】输出: 94

**逼近:**这个问题可以通过观察 **i** 对**P1<sup>a1</sup>* p2<sup>a2</sup>* P3<sup>a3</sup>…PK<sup>AK</sup>**那么[的**I**T19】的除数为 **(a1+1)(a2+1)…(ak**所以对于 **i** 来说，正好有 **4 个除数**，应该等于两个截然不同的素数](https://www.geeksforgeeks.org/total-number-divisors-given-number/)的[积，或者是某个素数的幂 **3** 。按照以下步骤解决问题:](https://www.geeksforgeeks.org/find-two-distinct-prime-numbers-with-given-product/)

*   初始化[数组](https://www.geeksforgeeks.org/array-data-structure/)**div【】**和**vis【】**以存储任意数的除数，并分别检查给定数是否被考虑。
*   将变量 **cnt** 初始化为 **0** ，以存储正好具有 **4** 除数的元素数。
*   现在，使用厄拉多塞算法的[筛。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   [迭代当](https://www.geeksforgeeks.org/java-while-loop-with-examples/)T2 小于 **n 时，使用变量 **i** 从 **2** 开始:**
    *   如果**我**是[质数](https://www.geeksforgeeks.org/tag/prime-number/):
        *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2 * I，1000000】**中迭代，增量为 **i** :
            *   如果已经考虑了数字 **j** ，那么**继续**。
            *   将**vis【j】**更新为 **true** ，将变量**currenum**初始化为**j****并将**计为 **0。**
            *   将**currenum**除以 **i** [而](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)**currenum % I**等于 **0，**递增**div【j】**和**计数**除以 **1。**
            *   如果**currenum**等于 **1，计数**等于 **3** ，**div【j】**等于 **3、**，则以 **1 递增 **cnt** 。**
            *   否则，如果**currenum**不等于 **1，则计数**等于 **1，div[j]**等于 **1，div[currenum]**等于 **0，**然后将 **cnt** 增加 **1。**
            *   如果 **cnt** 等于 **N，**则打印 **j** 并返回**。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the nth number which
// has exactly 4 divisors
int nthNumber(int n)
{

    // The divs[] array to store number of
    // divisors of every element
    int divs[1000000];

    // The vis[] array to check if given number
    // is considered or not
    bool vis[1000000];

    // The cnt stores number of elements having
    // exactly 4 divisors
    int cnt = 0;

    // Iterate while cnt less than n
    for (int i = 2; cnt < n; i++) {

        // If i is a prime
        if (divs[i] == 0) {

            // Iterate in the range [2*i, 1000000] with
            // increment of i
            for (int j = 2 * i; j < 1000000; j += i) {

                // If the number j is already considered
                if (vis[j]) {
                    continue;
                }

                vis[j] = 1;

                int currNum = j;
                int count = 0;

                // Dividing currNum by i until currNum % i is
                // equal to 0
                while (currNum % i == 0) {
                    divs[j]++;
                    currNum = currNum / i;
                    count++;
                }

                // Case a single prime in its factorization
                if (currNum == 1 && count == 3 && divs[j] == 3) {
                    cnt++;
                }

                else if (currNum != 1
                         && divs[currNum] == 0
                         && count == 1
                         && divs[j] == 1) {
                    // Case of two distinct primes which
                    // divides j exactly once each
                    cnt++;
                }

                if (cnt == n) {
                    return j;
                }
            }
        }
    }

    return -1;
}

// Driver Code
int main()
{
    // Given Input
    int N = 24;

    // Function Call
    cout << nthNumber(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find the nth number which
    // has exactly 4 divisors
    static int nthNumber(int n)
    {

        // The divs[] array to store number of
        // divisors of every element
        int divs[] = new int[1000000];

        // The vis[] array to check if given number
        // is considered or not
        boolean vis[] = new boolean[1000000];

        // The cnt stores number of elements having
        // exactly 4 divisors
        int cnt = 0;

        // Iterate while cnt less than n
        for (int i = 2; cnt < n; i++) {

            // If i is a prime
            if (divs[i] == 0) {

                // Iterate in the range [2*i, 1000000] with
                // increment of i
                for (int j = 2 * i; j < 1000000; j += i) {

                    // If the number j is already considered
                    if (vis[j]) {
                        continue;
                    }

                    vis[j] = true;

                    int currNum = j;
                    int count = 0;

                    // Dividing currNum by i until currNum %
                    // i is equal to 0
                    while (currNum % i == 0) {
                        divs[j]++;
                        currNum = currNum / i;
                        count++;
                    }

                    // Case a single prime in its
                    // factorization
                    if (currNum == 1 && count == 3
                        && divs[j] == 3) {
                        cnt++;
                    }

                    else if (currNum != 1
                             && divs[currNum] == 0
                             && count == 1
                             && divs[j] == 1) {
                        // Case of two distinct primes which
                        // divides j exactly once each
                        cnt++;
                    }

                    if (cnt == n) {
                        return j;
                    }
                }
            }
        }

        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int N = 24;

        // Function Call
        System.out.println(nthNumber(N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the nth number which
# has exactly 4 divisors
def nthNumber(n):

    # The divs[] array to store number of
    # divisors of every element
    divs = [0 for i in range(1000000)];

    # The vis[] array to check if given number
    # is considered or not
    vis = [0 for i in range(1000000)];

    # The cnt stores number of elements having
    # exactly 4 divisors
    cnt = 0;

    # Iterate while cnt less than n
    for i in range(2, n):

        # If i is a prime
        if (divs[i] == 0):

            # Iterate in the range [2*i, 1000000] with
            # increment of i
            for j in range(2 * i, 1000000):

                # If the number j is already considered
                if (vis[j]):
                    continue;

                vis[j] = 1;

                currNum = j;
                count = 0;

                # Dividing currNum by i until currNum % i is
                # equal to 0
                while (currNum % i == 0):
                    divs[j] += 1;
                    currNum = currNum // i;
                    count += 1;

                # Case a single prime in its factorization
                if (currNum == 1 and count == 3 and divs[j] == 3):
                    cnt += 1
                elif (currNum != 1
                    and divs[currNum] == 0
                    and count == 1
                    and divs[j] == 1):

                    # Case of two distinct primes which
                    # divides j exactly once each
                    cnt += 1

                if (cnt == n):
                    return j;

    return -1;

# Driver Code

# Given Input
N = 24;

# Function Call
print(nthNumber(N));

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;

// Function to find minimum number of
// elements required to obtain sum K
class GFG{

// Function to find the nth number which
// has exactly 4 divisors
static int nthNumber(int n)
{

    // The divs[] array to store number of
    // divisors of every element
    int[] divs = new int[1000000];

    // The vis[] array to check if given number
    // is considered or not
    int[] vis  = new int[1000000];

    // The cnt stores number of elements having
    // exactly 4 divisors
    int cnt = 0;

    // Iterate while cnt less than n
    for(int i = 2; cnt < n; i++)
    {

        // If i is a prime
        if (divs[i] == 0)
        {

            // Iterate in the range [2*i, 1000000] with
            // increment of i
            for(int j = 2 * i; j < 1000000; j += i)
            {

                // If the number j is already considered
                if (vis[j] != 0)
                {
                    continue;
                }

                vis[j] = 1;

                int currNum = j;
                int count = 0;

                // Dividing currNum by i until currNum % i is
                // equal to 0
                while (currNum % i == 0)
                {
                    divs[j]++;
                    currNum = currNum / i;
                    count++;
                }

                // Case a single prime in its factorization
                if (currNum == 1 && count == 3 && divs[j] == 3)
                {
                    cnt++;
                }

                else if (currNum != 1 && divs[currNum] == 0 &&
                           count == 1 && divs[j] == 1)
                {

                    // Case of two distinct primes which
                    // divides j exactly once each
                    cnt++;
                }

                if (cnt == n)
                {
                    return j;
                }
            }
        }
    }
    return -1;
}

// Driver Code
static public void Main ()
{

    // Given Input
    int N = 24;

    // Function Call
    Console.Write(nthNumber(N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the nth number which
// has exactly 4 divisors
function nthNumber(n)
{

    // The divs[] array to store number of
    // divisors of every element
    let divs = new Array(1000000);
    for(var i = 0; i < divs.length; i++)
    {
        divs[i] = 0;
    }

    // The vis[] array to check if given number
    // is considered or not
    let vis = new Array(1000000);
    for(var i = 0; i < vis.length; i++)
    {
        vis[i] = 0;
    }

    // The cnt stores number of elements having
    // exactly 4 divisors
    let cnt = 0;

    // Iterate while cnt less than n
    for(let i = 2; cnt < n; i++)
    {

        // If i is a prime
        if (divs[i] == 0)
        {

            // Iterate in the range [2*i, 1000000] with
            // increment of i
            for(let j = 2 * i; j < 1000000; j += i)
            {

                // If the number j is already considered
                if (vis[j])
                {
                    continue;
                }

                vis[j] = true;

                let currNum = j;
                let count = 0;

                // Dividing currNum by i until currNum %
                // i is equal to 0
                while (currNum % i == 0)
                {
                    divs[j]++;
                    currNum = Math.floor(currNum / i);
                    count++;
                }

                // Case a single prime in its
                // factorization
                if (currNum == 1 && count == 3 &&
                    divs[j] == 3)
                {
                    cnt++;
                }

                else if (currNum != 1 && divs[currNum] == 0 &&
                           count == 1 && divs[j] == 1)
                {

                    // Case of two distinct primes which
                    // divides j exactly once each
                    cnt++;
                }

                if (cnt == n)
                {
                    return j;
                }
            }
        }
    }
    return -1;
}

// Driver Code

// Given Input
let N = 24;

// Function Call
document.write(nthNumber(N));

// This code is contributed by code_hunt

</script>
```

**Output**

```
94
```

***时间复杂度:** O(Nlog(log(N))，其中 **N** 为 **1000000** 。*
***辅助空间:** O(N)*