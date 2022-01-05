# 仅用 D 形成的可被 K 整除的最小长度的数

> 原文:[https://www . geeksforgeeks . org/最小长度的仅可被 d 整除的数字/](https://www.geeksforgeeks.org/smallest-length-of-number-divisible-by-k-formed-by-using-d-only/)

给定 2 个整数 **D** 和 **K，**的任务是找到重复 **D** 形成的一个数的最小长度，该数将被 **K** 整除。如果没有，打印 **-1** 。

**示例:**

> **输入:** D = 1，K = 37
> **输出:** 3
> **说明:**重复 1 形成的可被 37 整除的最小数是 111
> 
> **输入:** D = 2，K = 36
> **输出:** -1

**天真方法:**想法是不断形成数，直到它被 **K** 整除或超出范围。

***时间复杂度:** O(10^18)*
***辅助空间:** O(1)*

**高效方法:**想法是通过用 **K** 除数并把余数存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)中来存储产生的余数。当同样的余数再次出现时，可以断定不存在这样的数。按照以下步骤解决问题:

*   将变量 **cnt** 初始化为 **0** 存储答案， **m** 存储号码。
*   [初始化大小为 **K** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **v[]** 以存储余数，并将 **v[m]** 的值设置为 **1。**
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)并执行以下步骤
    *   如果 **m** 等于 **0，**则返回 **cnt** 的值作为答案。
    *   将 **m** 的值设置为**((m *(10% k))% k)+(d % k))% k .**
    *   如果**v【m】**等于 **1，**则返回 **-1** ，因为不可能有这样的数字。
    *   将**v【m】**的值设置为 **1** ，将 **cnt** 的值增加 **1。**
*   执行上述步骤后，返回 **-1 的值。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to form the smallest number
// possible
int smallest(int k, int d)
{
    int cnt = 1;
    int m = d % k;

    // Array to mark the remainders
    // counted already
    vector<int> v(k, 0);
    v[m] = 1;

    // Iterate over the range
    while (1) {
        if (m == 0)
            return cnt;
        m = (((m * (10 % k)) % k) + (d % k)) % k;

        // If that remainder is already found,
        // return -1
        if (v[m] == 1)
            return -1;
        v[m] = 1;
        cnt++;
    }
    return -1;
}

// Driver Code
int main()
{

    int d = 1;
    int k = 41;
    cout << smallest(k, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to form the smallest number
// possible
static int smallest(int k, int d)
{
    int cnt = 1;
    int m = d % k;

    // Array to mark the remainders
    // counted already
    int[] v = new int[k];
    Arrays.fill(v, 0);
    v[m] = 1;

    // Iterate over the range
    while (1 != 0)
    {
        if (m == 0)
            return cnt;

        m = (((m * (10 % k)) % k) + (d % k)) % k;

        // If that remainder is already found,
        // return -1
        if (v[m] == 1)
            return -1;

        v[m] = 1;
        cnt++;
    }
}

// Driver Code
public static void main(String[] args)
{
    int d = 1;
    int k = 41;

    System.out.println(smallest(k, d));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach;

# Function to form the smallest number
# possible
def smallest(k, d):
    cnt = 1
    m = d % k

    # Array to mark the remainders
    # counted already
    v = [0 for i in range(k)];
    v[m] = 1

    # Iterate over the range
    while (1):
        if (m == 0):
            return cnt
        m = (((m * (10 % k)) % k) + (d % k)) % k

        # If that remainder is already found,
        # return -1
        if (v[m] == 1):
            return -1
        v[m] = 1
        cnt += 1

    return -1

# Driver Code
d = 1
k = 41
print(smallest(k, d))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to form the smallest number
// possible
static int smallest(int k, int d)
{
    int cnt = 1;
    int m = d % k;

    // Array to mark the remainders
    // counted already
    int [] v = new int[k];
    for(int i=0;i<k;i++)
        v[i] = 0;
    v[m] = 1;

    // Iterate over the range
    while (true) {
        if (m == 0)
            return cnt;
        m = (((m * (10 % k)) % k) + (d % k)) % k;

        // If that remainder is already found,
        // return -1
        if ( v[m] == 1)
            return -1;

        v[m] = 1;
        cnt++;
    }
   // return -1;
}

// Driver Code
public static void Main()
{

    int d = 1;
    int k = 41;
    Console.Write(smallest(k, d));
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach;

        // Function to form the smallest number
        // possible
        function smallest(k, d) {
            let cnt = 1;
            let m = d % k;

            // Array to mark the remainders
            // counted already
            let v = new Array(k).fill(0);
            v[m] = 1;

            // Iterate over the range
            while (1) {
                if (m == 0)
                    return cnt;
                m = (((m * (10 % k)) % k) + (d % k)) % k;

                // If that remainder is already found,
                // return -1
                if (v[m] == 1)
                    return -1;
                v[m] = 1;
                cnt++;
            }
            return -1;
        }

        // Driver Code
        let d = 1;
        let k = 41;
        document.write(smallest(k, d));

   // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
5
```

***时间复杂度:**O(K)*
T5**辅助空间:** O(K)