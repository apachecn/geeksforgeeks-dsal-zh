# 将一个数组分成 3 组，这样 X3 可以被 X2 整除，X2 可以被 X1 整除

> 原文:[https://www . geeksforgeeks . org/将数组拆分为 3 个这样的组，x3 可被 x2 整除，x2 可被 x1 整除/](https://www.geeksforgeeks.org/split-an-array-into-groups-of-3-such-that-x3-is-divisible-by-x2-and-x2-is-divisible-by-x1/)

给定一个包含 **N** 元素的数组**A**(**N**可被 **3** 整除)，任务是将数字拆分为 3 个一组，让该组有 3 个元素 X1、X2 和 X3，该组应该满足以下条件:

*   X1、X2 和 X3 是成对不同的
*   X3 可以被 X2 分割
*   X2 可以被 X1 整除

如果无法将数组拆分成 **N/3** 这样的组，打印-1。
**注意:**数组的元素将位于 1 到 6(包括 1 和 6)的范围内。
**例:**

```
Input : N = 6, A[] = {2, 2, 1, 1, 4, 6}
Output : 1 2 4
         1 2 6
Explanation: 
*Group 1*: Pairs = {(1,2), (2,4), (1,4)}
All pairs are distinct, 
4 is divisible by 2 and 2 by 1.
*Group 2*: Pairs = {(1,2), (2,6), (1,6)}
All pairs are distinct, 
6 is divisible by 2 and 2 by 1.

Input : N = 6, A[] = {1, 1, 1, 6, 6, 3}
Output : -1
```

**方法:**
由于数组的值在 1 到 6 之间，只能组成以下几种组:

*   1 2 4
*   1 2 6
*   1 3 6

从计算每个元素的频率开始。由于 1 在所有组中都很常见，因此它必须恰好出现 **N/3** 次。4 只能放入第一种组，它总是包含 2。所以 2 的计数应该大于 4 的计数。剩下的 2 个只能放在第二类组里。现在，剩下的数字必须放在第三类组中。如果在任何时候计数少于要求，答案将是-1。
以下是上述办法的实施情况:

## C++

```
// C++ program to split array in groups of 3

#include <bits/stdc++.h>
using namespace std;

// Function to print the groups after
// splitting array in groups of 3
void printGroups(int n, int a[])
{
    int ct[7] = { 0 }, grps = n / 3, i;

    // Count occurrence of each element
    for (i = 0; i < n; i++)
        ct[a[i]]++;

    // Check if it is possible to form the groups
    if (ct[1] != grps || (ct[4] + ct[6]) != grps
              || (ct[2] + ct[3]) != grps || ct[4] > ct[2])
    {
        cout << -1;
        return;
    }

    // Print groups that end at 4
    for (i = 0; i < ct[4]; i++)
        cout << "1 2 4\n";

    // Print groups that end at 6, with 2
    // in the middle
    for (i = 0; i < ct[2] - ct[4]; i++)
        cout << "1 2 6\n";

    // Print groups that have a 3 in the middle
    for (i = 0; i < ct[3]; i++)
        cout << "1 3 6\n";
}

// Driver Code
int main()
{
    int n = 6;
    int a[n] = { 2, 2, 1, 1, 4, 6 };

    printGroups(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split array in groups of 3
class GFG
{

    // Function to print the groups after
    // splitting array in groups of 3
    static void printGroups(int n, int a[])
    {
        int ct[] = new int[7], grps = n / 3, i;

        // Count occurrence of each element
        for (i = 0; i < n; i++)
        {
            ct[a[i]]++;
        }

        // Check if it is possible to form the groups
        if (ct[1] != grps || (ct[4] + ct[6]) != grps
            || (ct[2] + ct[3]) != grps || ct[4] > ct[2])
        {
            System.out.print(-1);
            return;
        }

        // Print groups that end at 4
        for (i = 0; i < ct[4]; i++)
        {
            System.out.print("1 2 4\n");
        }

        // Print groups that end at 6, with 2
        // in the middle
        for (i = 0; i < ct[2] - ct[4]; i++)
        {
            System.out.print("1 2 6\n");
        }

        // Print groups that have a 3 in the middle
        for (i = 0; i < ct[3]; i++)
        {
            System.out.print("1 3 6\n");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 6;
        int a[] = {2, 2, 1, 1, 4, 6};

        printGroups(n, a);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to split array in
# groups of 3

# Function to print the groups after
# splitting array in groups of 3
def printGroups(n, a):

    ct = [0 for i in range(7)]
    grps = n // 3
    i = 0

    # Count occurrence of each element
    for i in range(n):
        ct[a[i]] += 1

    # Check if it is possible to
    # form the groups
    if (ct[1] != grps or (ct[4] + ct[6]) != grps or
       (ct[2] + ct[3]) != grps or ct[4] > ct[2]):
        print(-1)
        return

    # Print groups that end at 4
    for i in range(ct[4]):
        print("1 2 4")

    # Print groups that end at 6, with 2
    # in the middle
    for i in range(ct[2] - ct[4]):
        print("1 2 6")

    # Print groups that have a 3 in the middle
    for i in range(ct[3]):
        print("1 3 6")

# Driver Code
n = 6
a = [2, 2, 1, 1, 4, 6 ]

printGroups(n, a)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to split array in groups of 3
using System;

class GFG
{

    // Function to print the groups after
    // splitting array in groups of 3
    static void printGroups(int n, int []a)
    {
        int []ct = new int[7];
        int grps = n / 3, i;

        // Count occurrence of each element
        for (i = 0; i < n; i++)
        {
            ct[a[i]]++;
        }

        // Check if it is possible to form the groups
        if (ct[1] != grps || (ct[4] + ct[6]) != grps ||
           (ct[2] + ct[3]) != grps || ct[4] > ct[2])
        {
            Console.Write(-1);
            return;
        }

        // Print groups that end at 4
        for (i = 0; i < ct[4]; i++)
        {
            Console.Write("1 2 4\n");
        }

        // Print groups that end at 6, with 2
        // in the middle
        for (i = 0; i < ct[2] - ct[4]; i++)
        {
            Console.Write("1 2 6\n");
        }

        // Print groups that have a 3 in the middle
        for (i = 0; i < ct[3]; i++)
        {
            Console.Write("1 3 6\n");
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 6;
        int []a = {2, 2, 1, 1, 4, 6};

        printGroups(n, a);
    }
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to split array in groups of 3

// Function to print the groups after
// splitting array in groups of 3
function printGroups($n, $a)
{
    $ct = array(); $grps = $n / 3;

    // Count occurrence of each element
    for ($i = 0; $i < $n; $i++)
        $ct[$a[$i]]++;

    // Check if it is possible to form the groups
    if ($ct[1] != $grps || ($ct[4] + $ct[6]) != $grps ||
       ($ct[2] + $ct[3]) != $grps || $ct[4] > $ct[2])
    {
        echo -1;
        return;
    }

    // Print groups that end at 4
    for ($i = 0; $i < $ct[4]; $i++)
        echo "1 2 4\n";

    // Print groups that end at 6, with 2
    // in the middle
    for ($i = 0; $i < $ct[2] - $ct[4]; $i++)
        echo "1 2 6\n";

    // Print groups that have a 3 in the middle
    for ($i = 0; $i < $ct[3]; $i++)
        echo "1 3 6\n";
}

// Driver Code
$n = 6;
$a = array(2, 2, 1, 1, 4, 6);

printGroups($n, $a);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to split array in groups of 3

// Function to print the groups after
// splitting array in groups of 3
function printGroups(n, a)
{
    let ct = new Array(7).fill(0), grps = parseInt(n / 3), i;

    // Count occurrence of each element
    for (i = 0; i < n; i++)
        ct[a[i]]++;

    // Check if it is possible to form the groups
    if (ct[1] != grps || (ct[4] + ct[6]) != grps
              || (ct[2] + ct[3]) != grps || ct[4] > ct[2])
    {
        document.write(-1);
        return;
    }

    // Print groups that end at 4
    for (i = 0; i < ct[4]; i++)
        document.write("1 2 4<br>");

    // Print groups that end at 6, with 2
    // in the middle
    for (i = 0; i < ct[2] - ct[4]; i++)
        document.write("1 2 6<br>");

    // Print groups that have a 3 in the middle
    for (i = 0; i < ct[3]; i++)
        document.write("1 3 6<br>");
}

// Driver Code
    let n = 6;
    let a = [ 2, 2, 1, 1, 4, 6 ];

    printGroups(n, a);

</script>
```

**Output:** 

```
1 2 4
1 2 6
```

**时间复杂度:** O(N)