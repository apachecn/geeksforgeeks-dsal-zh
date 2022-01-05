# 找出两个复合数，这样就有了 N 个不同

> 原文:[https://www . geesforgeks . org/find-two-composite-numbers-so-difference-is-n/](https://www.geeksforgeeks.org/find-two-composite-numbers-such-that-there-difference-is-n/)

给定一个数字 **N** ，任务是找到两个复合数字 **X** 和 **Y** ，使得它们之间的差值等于 **N** 。请注意，此任务可以有多个答案。打印其中任何一个。
**举例:**

```
Input: N = 4
Output: X = 36, Y = 32

Input: N = 1
Output: X = 9, Y = 8
```

**接近** :

*   我们必须找到**X–Y = N**。

*   我们知道 **N** 的最小值可以是 **0** 或者 **1** 。如果是 **0** ，那么我们可以打印任意一个合成号码两次。

*   如果 **N = 0** ，那么我们可以打印 **9*N** 和 **8 * N** ，因为这些合成数字之间的差异最小，即 **1** 。

*   我们也可以打印 **15 * N** 和 **16 * N** ，但是我们必须打印任意两个复合数字，所以这些都是可能的。

下面是
的实现

## C++

```
#include <bits/stdc++.h>
using namespace std;
// C++ code to Find two Composite Numbers
// such that there difference is N

// Function to find the two composite numbers
void find_composite_nos(int n)
{
    cout << 9 * n << " " << 8 * n;
}

// Driver code
int main()
{
    int n = 4;

    find_composite_nos(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Find two Composite Numbers
// such that there difference is N
class GFG
{

    // Function to find the two composite numbers
    static void find_composite_nos(int n)
    {
        System.out.println(9 * n + " " + 8 * n);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 4;

        find_composite_nos(n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 code to Find two Composite Numbers
# such that their difference is N

# Function to find the two composite numbers
def find_composite_nos(n) :

    print(9 * n, 8 * n);

# Driver code
if __name__ == "__main__" :

    n = 4;

    find_composite_nos(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# code to Find two Composite Numbers
// such that there difference is N
using System;

class GFG
{

    // Function to find the two composite numbers
    static void find_composite_nos(int n)
    {
        Console.WriteLine(9 * n + " " + 8 * n);
    }

    // Driver code
    public static void Main()
    {
        int n = 4;

        find_composite_nos(n);
    }
}

// This code is contributed by AnkitRai01 
```

## java 描述语言

```
<script>

// javascript code to Find two Composite Numbers
// such that there difference is N

// Function to find the two composite numbers
function find_composite_nos(n)
{
    document.write(9 * n + " " + 8 * n);
}

// Driver code

var n = 4;

find_composite_nos(n);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
36 32
```