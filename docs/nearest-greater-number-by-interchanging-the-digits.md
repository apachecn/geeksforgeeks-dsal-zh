# 通过互换数字

最接近较大的数字

> 原文:[https://www . geeksforgeeks . org/通过数字互换获得最近的更大数字/](https://www.geeksforgeeks.org/nearest-greater-number-by-interchanging-the-digits/)

给定两个整数 **A** 和 **B** 。任务是通过互换 **A** 的数字找到与 **B** 最近的较大值。如果没有这样的可能，那么打印-1。
**举例:**

> **输入:** A = 459，B = 500
> **输出:** 549
> 549 是最近的较大者。
> **输入:** A = 321，B = 567
> **输出:** -1
> **输入:** A = 231，B = 125
> **输出:** 132

**先决条件:** [一串的所有排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)
**方法:**

*   使用整数设置 min1 的最小值。最大值
*   用上述置换方法交换 A 的数字。
*   检查 A 的介电常数是否小于 min1。如果小于，则将 min1 更新为 a。
*   对 A 的所有置换重复此操作，找到最小的较大值

以下是上述方法的实现:

## C++

```
// C++ program to find nearest greater value
#include <bits/stdc++.h>
using namespace std;

int min1 = INT_MAX;
int _count = 0;

// Find all the possible permutation of Value A.
int permutation(string str1, int i, int n, int p)
{
    if (i == n)
    {
        // Convert into Integer
        int q = stoi(str1);

        // Find the minimum value of A by interchanging
        // the digit of A and store min1.
        if (q - p > 0 && q < min1)
        {
            min1 = q;
            _count = 1;
        }
    }
    else
    {
        for (int j = i; j <= n; j++)
        {
            // Swap two string character
            swap(str1[i], str1[j]);
            permutation(str1, i + 1, n, p);
            swap(str1[i], str1[j]);
        }
    }
    return min1;
}

// Driver code
int main()
{
    int A = 213;
    int B = 111;

    // Convert integer value into string to
    // find all the permutation of the number
    string str1 = to_string(A);
    int len = str1.length();
    int h = permutation(str1, 0, len - 1, B);

    // count=1 means number greater than B exists
    _count ? cout << h << endl : cout << -1 << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find nearest greater value
import java.io.*;
import java.util.*;

class GFG {
    static int min1 = Integer.MAX_VALUE;
    static int count = 0;

    // Find all the possible permutation of Value A.
    public int permutation(String str1, int i, int n, int p)
    {

        if (i == n) {

            // Convert into Integer
            int q = Integer.parseInt(str1);

            // Find the minimum value of A by interchanging
            // the digit of A and store min1.
            if (q - p > 0 && q < min1) {
                min1 = q;
                count = 1;
            }
        }

        else {
            for (int j = i; j <= n; j++) {
                str1 = swap(str1, i, j);
                permutation(str1, i + 1, n, p);
                str1 = swap(str1, i, j);
            }
        }
        return min1;
    }

    // Swap two string character
    public String swap(String str, int i, int j)
    {
        char ch[] = str.toCharArray();
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        // Return the string after
        // swapping between two character.
        return String.valueOf(ch);
    }

    // Driver code
    public static void main(String[] args)
    {

        int A = 213;
        int B = 111;

        GFG gfg = new GFG();

        // Convert integer value into string to
        // find all the permutation of the number
        String str1 = Integer.toString(A);
        int len = str1.length();
        int h = gfg.permutation(str1, 0, len - 1, B);

        // count=1 means number greater than B exists
        if (count == 1)
            System.out.println(h);
        else
            System.out.println(-1);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find nearest greater value
min1 = 10**9
_count = 0

# Find all the possible permutation of Value A.
def permutation(str1, i, n, p):
    global min1, _count
    if (i == n):

        # Convert into Integer
        str1 = "".join(str1)
        q = int(str1)

        # Find the minimum value of A
        # by interchanging the digits
        # of A and store min1.
        if (q - p > 0 and q < min1):
            min1 = q
            _count = 1
    else:
        for j in range(i, n + 1):

            # Swap two character)
            str1[i], str1[j] = str1[j], str1[i]
            permutation(str1, i + 1, n, p)
            str1[i], str1[j] = str1[j], str1[i]

    return min1

# Driver code
A = 213
B = 111

# Convert integer value into to
# find all the permutation of the number
str2 = str(A)
str1 = [i for i in str2]
le = len(str1)

h = permutation(str1, 0, le - 1, B)

# count=1 means number greater than B exists
if _count == 1:
    print(h)
else:
    print(-1)

# This code is contributed by
# mohit
```

## C#

```
// C# program to find nearest greater value
using System;

class GFG
{
    static int min1 = int.MaxValue;
    static int count = 0;

    // Find all the possible permutation of Value A.
    public int permutation(String str1, int i,
                                 int n, int p)
    {
        if (i == n)
        {

            // Convert into Integer
            int q = int.Parse(str1);

            // Find the minimum value of A by interchanging
            // the digit of A and store min1.
            if (q - p > 0 && q < min1)
            {
                min1 = q;
                count = 1;
            }
        }

        else
        {
            for (int j = i; j <= n; j++)
            {
                str1 = swap(str1, i, j);
                permutation(str1, i + 1, n, p);
                str1 = swap(str1, i, j);
            }
        }
        return min1;
    }

    // Swap two string character
    public String swap(String str, int i, int j)
    {
        char []ch = str.ToCharArray();
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;

        // Return the string after
        // swapping between two character.
        return String.Join("", ch);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int A = 213;
        int B = 111;

        GFG gfg = new GFG();

        // Convert integer value into string to
        // find all the permutation of the number
        String str1 = A.ToString();
        int len = str1.Length;
        int h = gfg.permutation(str1, 0, len - 1, B);

        // count=1 means number greater than B exists
        if (count == 1)
            Console.WriteLine(h);
        else
            Console.WriteLine(-1);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// JAVAscript program to find nearest greater value

let min1 = Number.MAX_VALUE;
let count = 0;

// Find all the possible permutation of Value A.
function permutation(str1,i,n,p)
{
    if (i == n) {

            // Convert into Integer
            let q = parseInt(str1);

            // Find the minimum value of A by interchanging
            // the digit of A and store min1.
            if (q - p > 0 && q < min1) {
                min1 = q;
                count = 1;
            }
        }

        else {
            for (let j = i; j <= n; j++) {
                str1 = swap(str1, i, j);
                permutation(str1, i + 1, n, p);
                str1 = swap(str1, i, j);
            }
        }
        return min1;
}

 // Swap two string character
function swap(str,i,j)
{
    let ch = str.split("");
        let temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        // Return the string after
        // swapping between two character.
        return (ch).join("");
}

// Driver code
let A = 213;
        let B = 111;

        // Convert integer value into string to
        // find all the permutation of the number
        let str1 = A.toString();
        let len = str1.length;
        let h = permutation(str1, 0, len - 1, B);

        // count=1 means number greater than B exists
        if (count == 1)
            document.write(h);
        else
            document.write(-1);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
123
```