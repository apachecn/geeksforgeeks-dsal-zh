# 通过重复乘以 10 或 20 来检查 N 是否可以从 1 中得到

> 原文:[https://www . geesforgeks . org/check-if-n-can-from-1-by-reply-乘 10 或-20/](https://www.geeksforgeeks.org/check-if-n-can-be-obtained-from-1-by-repetitively-multiplying-by-10-or-20/)

给定一个整数 **N** ，任务是通过重复乘以 10 或 20 来确定是否有可能从 1 获得值 **N** 。如果可能，打印“是”，否则打印“否”。
**例:**

> **输入:** N = 200
> **输出:** YES
> **解释:**
> 1 * 10->10 * 20->200
> **输入:** N = 90
> **输出:** NO

**进场:**
按照以下步骤解决问题:

1.  计算尾随零的数量。
2.  去掉尾随零后，如果剩余的 N 不能表示为 2 的幂，则打印**否**。
3.  否则，如果记录 <sub>2</sub> N < =尾随零的计数，则打印“是”。

**以下是上述方法的实施:**

## C++

```
// C++ program to check if N
// can be obtained from 1 by
// repetitive multiplication
// by 10 or 20
#include<bits/stdc++.h>
using namespace std;

// Function to check if N can
// be obtained or not
void Is_possible(long long int N)
{
    int C = 0;
    int D = 0;

    // Count and remove trailing
    // zeroes
    while (N % 10 == 0)
    {
        N = N / 10;
        C += 1;
    }

    // Check if remaining
    // N is a power of 2
    if(pow(2, (int)log2(N)) == N)
    {
        D = (int)log2(N);

        // To check the condition
        // to print YES or NO
        if (C >= D)
            cout << "YES";
        else
            cout << "NO";
    }
    else
        cout << "NO";
}

// Driver code
int main()
{
    long long int N = 2000000000000;

    Is_possible(N);
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if N
// can be obtained from 1 by
// repetitive multiplication
// by 10 or 20
import java.util.*;

class GFG{

static void Is_possible(long N)
{
    long C = 0;
    long D = 0;

    // Count and remove trailing
    // zeroes
    while (N % 10 == 0)
    {
        N = N / 10;
        C += 1;
    }

    // Check if remaining
    // N is a power of 2
    if(Math.pow(2, (long)(Math.log(N) /
                         (Math.log(2)))) == N)
    {
        D = (long)(Math.log(N) / (Math.log(2)));

        // To check the condition
        // to prlong YES or NO
        if (C >= D)
            System.out.print("YES");
        else
            System.out.print("NO");
    }
    else
        System.out.print("NO");
}

// Driver code
public static void main(String args[])
{
    long N = 2000000000000L;
    Is_possible(N);
}
}

// This code is contributed by Stream_Cipher
```

## 计算机编程语言

```
# Python Program to check if N
# can be obtained from 1 by
# repetitive multiplication
# by 10 or 20

import math

# Function to check if N can
# be obtained or not
def Is_possible(N):

    C = 0
    D = 0

    # Count and remove trailing
    # zeroes
    while ( N % 10 == 0):
        N = N / 10
        C += 1

    # Check if remaining
    # N is a power of 2
    if ( math.log(N, 2)
    - int(math.log(N, 2)) == 0):

        D = int(math.log(N, 2))

        # To check the condition
        # to print YES or NO
        if (C >= D):
            print("YES")

        else:
            print("NO")

    else:
        print("NO")

# Driver Program
N = 2000000000000
Is_possible(N)
```

## C#

```
// C# program to check if N
// can be obtained from 1 by
// repetitive multiplication
// by 10 or 20
using System;

class GFG{

static void Is_possible(long N)
{
    long C = 0;
    long D = 0;

    // Count and remove trailing
    // zeroes
    while (N % 10 == 0)
    {
        N = N / 10;
        C += 1;
    }

    // Check if remaining
    // N is a power of 2
    if(Math.Pow(2, (long)(Math.Log(N) /
                         (Math.Log(2)))) == N)
    {
        D = (long)(Math.Log(N) / (Math.Log(2)));

        // To check the condition
        // to prlong YES or NO
        if (C >= D)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
    else
        Console.WriteLine("NO");
}

// Driver Code
public static void Main()
{
    long N = 2000000000000L;

    Is_possible(N);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
// Java  script program to check if N
// can be obtained from 1 by
// repetitive multiplication
// by 10 or 20

function Is_possible( N)
{
    let  C = 0;
    let  D = 0;

    // Count and remove trailing
    // zeroes
    while (N % 10 == 0)
    {
        N = N / 10;
        C += 1;
    }

    // Check if remaining
    // N is a power of 2
    if(Math.pow(2, (Math.log(N) /
                        (Math.log(2)))) == N)
    {
        D = (Math.log(N) / (Math.log(2)));

        // To check the condition
        // to prlong YES or NO
        if (C >= D)
            document.write("YES");
        else
            document.write("NO");
    }
    else
        document.write("NO");
}

// Driver code

    let  N = 2000000000000;
    Is_possible(N);

//this code is contributed by sravan kumar
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(log<sub>10</sub>(N))*
***辅助空间:** O(1)*