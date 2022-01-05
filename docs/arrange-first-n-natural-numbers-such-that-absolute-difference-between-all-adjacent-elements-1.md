# 排列前 N 个自然数，使得所有相邻元素之间的绝对差值> 1

> 原文:[https://www . geeksforgeeks . org/array-first-n-自然数-所有相邻元素之间的绝对差-1/](https://www.geeksforgeeks.org/arrange-first-n-natural-numbers-such-that-absolute-difference-between-all-adjacent-elements-1/)

给定一个整数 **N** 。任务是找到第一个 **N** 自然数的排列，使得任意两个连续数**T8】1**之间的绝对差。如果没有这样的排列，则打印 **-1** 。

**示例:**

> **输入:**N = 5
> T3】输出: 5 3 1 4 2
> 
> **输入:** N = 3
> **输出:** -1

**方法:**可能有许多这样的排列方式，但最常见和最贪婪的方法之一是以递减(或递增)顺序排列所有奇数，然后以递减(或递增)顺序排列所有偶数。**注意**如果 **N = 3** 或 **N = 2** 则不可能有这样的安排，如果 **N = 1** 则序列将由单个元素组成，即 **1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required permutation
void arrange(int N)
{

    if (N == 1) {
        cout << "1";
        return;
    }

    // No permutation is possible
    // satisfying the given condition
    if (N == 2 || N == 3) {
        cout << "-1";
        return;
    }

    // Maximum even and odd elements < N
    int even = -1, odd = -1;
    if (N % 2 == 0) {
        even = N;
        odd = N - 1;
    }
    else {
        odd = N;
        even = N - 1;
    }

    // Print all odd elements in decreasing order
    while (odd >= 1) {
        cout << odd << " ";

        // Next element must be odd
        odd = odd - 2;
    }

    // Print all even elements in decreasing order
    while (even >= 2) {
        cout << even << " ";

        // Next element must be even
        even = even - 2;
    }
}

// Driver code
int main()
{
    int N = 5;
    arrange(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print the required
// permutation
static void arrange(int N)
{
    if (N == 1)
    {
        System.out.println("1");
        return;
    }

    // No permutation is possible
    // satisfying the given condition
    if (N == 2 || N == 3)
    {
        System.out.println("-1");
        return;
    }

    // Maximum even and odd elements < N
    int even = -1, odd = -1;
    if (N % 2 == 0)
    {
        even = N;
        odd = N - 1;
    }
    else
    {
        odd = N;
        even = N - 1;
    }

    // Print all odd elements in
    // decreasing order
    while (odd >= 1)
    {
        System.out.print(odd);
        System.out.print(" ");

        // Next element must be odd
        odd = odd - 2;
    }

    // Print all even elements in
    // decreasing order
    while (even >= 2)
    {
        System.out.print(even);
        System.out.print(" ");

        // Next element must be even
        even = even - 2;
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 5;
    arrange(N);
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the required permutation
def arrange(N):

    if (N == 1) :
        print("1")
        return

    # No permutation is possible
    # satisfying the given condition
    if (N == 2 or N == 3) :
        print("-1")
        return

    # Maximum even and odd elements < N
    even = -1
    odd = -1
    if (N % 2 == 0):
        even = N
        odd = N - 1
    else :
        odd = N
        even = N - 1

    # Print all odd elements in
    # decreasing order
    while (odd >= 1):
        print(odd, end = " ")

        # Next element must be odd
        odd = odd - 2

    # Print all even elements in
    # decreasing order
    while (even >= 2):
        print(even, end = " ")

        # Next element must be even
        even = even - 2

# Driver code
if __name__ == "__main__":

    N = 5
    arrange(N)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the required
// permutation
static void arrange(int N)
{
    if (N == 1)
    {
        Console.WriteLine("1");
        return;
    }

    // No permutation is possible
    // satisfying the given condition
    if (N == 2 || N == 3)
    {
        Console.WriteLine("-1");
        return;
    }

    // Maximum even and odd elements < N
    int even = -1, odd = -1;
    if (N % 2 == 0)
    {
        even = N;
        odd = N - 1;
    }
    else
    {
        odd = N;
        even = N - 1;
    }

    // Print all odd elements in
    // decreasing order
    while (odd >= 1)
    {
        Console.Write(odd);
        Console.Write(" ");

        // Next element must be odd
        odd = odd - 2;
    }

    // Print all even elements in
    // decreasing order
    while (even >= 2)
    {
        Console.Write(even);
        Console.Write(" ");

        // Next element must be even
        even = even - 2;
    }
}

// Driver code
public static void Main()
{
    int N = 5;
    arrange(N);
}
}

// This code is contributed
// by Shivi_Aggarwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the required
// permutation
function arrange($N)
{
    if ($N == 1)
    {
        echo "1";
        return;
    }

    // No permutation is possible
    // satisfying the given condition
    if ($N == 2 || $N == 3)
    {
        echo "-1";
        return;
    }

    // Maximum even and odd elements < N
    $even = -1 ;
    $odd = -1;

    if ($N % 2 == 0)
    {
        $even = $N;
        $odd = $N - 1;
    }
    else
    {
        $odd = $N;
        $even = $N - 1;
    }

    // Print all odd elements in
    // decreasing order
    while ($odd >= 1)
    {
        echo $odd, " ";

        // Next element must be odd
        $odd = $odd - 2;
    }

    // Print all even elements in
    // decreasing order
    while ($even >= 2)
    {
        echo $even, " ";

        // Next element must be even
        $even = $even - 2;
    }
}

// Driver code
$N = 5;
arrange($N);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print var the required
// permutation
function arrange(N)
{
    if (N == 1)
    {
        document.write("1");
        return;
    }

    // No permutation is possible
    // satisfying the given condition
    if (N == 2 || N == 3)
    {
        document.write("-1");
        return;
    }

    // Maximum even and odd elements < N
    var even = -1, odd = -1;
    if (N % 2 == 0)
    {
        even = N;
        odd = N - 1;
    }
    else
    {
        odd = N;
        even = N - 1;
    }

    // Print var all odd elements in
    // decreasing order
    while (odd >= 1)
    {
        document.write(odd);
        document.write(" ");

        // Next element must be odd
        odd = odd - 2;
    }

    // Print var all even elements in
    // decreasing order
    while (even >= 2)
    {
        document.write(even);
        document.write(" ");

        // Next element must be even
        even = even - 2;
    }
}

// Driver code
var N = 5;

arrange(N);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
5 3 1 4 2
```