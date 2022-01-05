# 计算给定边范围内可能的三角形数量

> 原文:[https://www . geeksforgeeks . org/count-给定边的可能三角形数-范围/](https://www.geeksforgeeks.org/count-number-of-triangles-possible-for-the-given-sides-range/)

给定四个整数 **A** 、 **B** 、 **C** 和 **D** ，任务是找出不同集合(X、Y 和 Z)的数量，其中 X、Y 和 Z 表示形成有效三角形的边的长度。A ≤ X ≤ B、B ≤ Y ≤ C、C≤Z≤d
**例:**

> **输入:** A = 2，B = 3，C = 4，D = 5
> **输出:** 7
> **解释:**
> 三角形边的可能长度为–
> {(2，3，4)，(2，4，4)，(2，4，5)，(3，3，4)，(3，3，5)，(3，4，4)和(3，4，5)}
> **输入:** A = 1，B = 1

**天真法:**问题中的关键观察是，如果 X，Y，Z 是三角形的有效边，X ≤ Y ≤ Z，那么这些边形成有效三角形的充分条件将是 **X+Y > Z** 。
最后，给定 X 和 Y 的可能 Z 值的计数可以计算为–

1.  如果 X+Y 大于 D，在这种情况下，Z 可以从[C，D]中选择，Z 的总可能值将是(D-C+1)。
2.  如果 X+Y 小于 D 大于 C，那么 Z 可以从[C，X+Y-1]中选择。
3.  如果 X+Y 小于或等于 C，那么我们不能选择 Z，因为这些边不会形成一个有效的三角形。

**时间复杂度:** ![O(B * C) ](img/67f50bf2e964df6952f0ce1e08bc7337.png "Rendered by QuickLaTeX.com")

**有效方法:**想法是迭代 A 的所有可能值，然后使用数学计算计算给定 X 的可能 Y 和 Z 值的数量。
对于给定的 X，X+Y 的值将在![[X+B, X+C]   ](img/0b58e1841d23bf78091ea2808980781f.png "Rendered by QuickLaTeX.com")的范围内。如果我们计算大于 D 的可能值的数量，那么 Y 和 Z 的可能值的总数将是–

```
// Number of possible values of Y and Z
// If num_greater is the number of possible
// Y values which is greater than D

```

同样，设 R 和 L 是 C 和 d 范围内 X+Y 值的上界和下界，那么 Y 和 Z 的总组合将是–

以下是上述方法的实现:

## C++

```
// C++ implementation to count the
// number of possible triangles
// for the given sides ranges

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// possible triangles for the given
// sides ranges
int count_triangles(int a, int b,
                    int c, int d)
{

    int ans = 0;

    // Iterate for every possible of x
    for (int x = a; x <= b; ++x) {

        // Range of y is [b, c]
        // From this range First
        // we will find the number
        // of x + y greater than d
        int num_greater_than_d = max(d, c + x) - max(d, b + x - 1);

        // For x+y greater than d
        // we can choose all z from [c, d]
        // Total permutation will be
        ans += num_greater_than_d * (d - c + 1);

        // Now we will find the number
        // of x+y in between the [c, d]
        int r = min(max(c, c + x), d) - c;
        int l = min(max(c, b + x - 1), d) - c;

        // [l, r] will be the range
        // from total [c, d] x+y belongs
        // For any r such that r = x+y
        // We can choose z, in the range
        // [c, d] only less than r,
        // Thus total permutation be
        int x1 = (r * (r + 1)) / 2;
        int x2 = (l * (l + 1)) / 2;

        ans += x1 - x2;
    }

    return ans;
}

// Driver Code
int main()
{
    int a = 2, b = 3, c = 4, d = 5;

    cout << count_triangles(a, b, c, d)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of possible triangles
// for the given sides ranges
import java.util.Scanner;
import java.util.Arrays;

class GFG{

// Function to count the number of
// possible triangles for the given
// sides ranges
public static int count_triangles(int a, int b,
                                  int c, int d)
{
    int ans = 0;

    // Iterate for every possible of x
    for(int x = a; x <= b; ++x)
    {

        // Range of y is [b, c]
        // From this range First
        // we will find the number
        // of x + y greater than d
        int num_greater_than_d = Math.max(d, c + x) -
                                 Math.max(d, b + x - 1);

        // For x+y greater than d
        // we can choose all z from [c, d]
        // Total permutation will be
        ans += num_greater_than_d * (d - c + 1);

        // Now we will find the number
        // of x+y in between the [c, d]
        int r = Math.min(Math.max(c, c + x), d) - c;
        int l = Math.min(Math.max(c, b + x - 1), d) - c;

        // [l, r] will be the range
        // from total [c, d] x+y belongs
        // For any r such that r = x+y
        // We can choose z, in the range
        // [c, d] only less than r,
        // Thus total permutation be
        int x1 = (r * (r + 1)) / 2;
        int x2 = (l * (l + 1)) / 2;

        ans += x1 - x2;
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int a = 2, b = 3, c = 4, d = 5;

    System.out.println(count_triangles(a, b, c, d));
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 implementation to count 
# the number of possible triangles
# for the given sides ranges

# Function to count the number of
# possible triangles for the given
# sides ranges
def count_triangles(a, b, c, d):

    ans = 0

    # Iterate for every possible of x
    for x in range(a, b + 1):

        # Range of y is [b, c]
        # From this range First
        # we will find the number
        # of x + y greater than d
        num_greater_than_d = (max(d, c + x) -
                              max(d, b + x - 1))

        # For x+y greater than d we
        # can choose all z from [c, d]
        # Total permutation will be
        ans = (ans + num_greater_than_d *
                             (d - c + 1))

        # Now we will find the number
        # of x+y in between the [c, d]
        r = min(max(c, c + x), d) - c;
        l = min(max(c, b + x - 1), d) - c;

        # [l, r] will be the range
        # from total [c, d] x+y belongs
        # For any r such that r = x+y
        # We can choose z, in the range
        # [c, d] only less than r,
        # Thus total permutation be
        x1 = int((r * (r + 1)) / 2)
        x2 = int((l * (l + 1)) / 2)

        ans = ans + (x1 - x2)

    return ans

# Driver Code
a = 2
b = 3
c = 4
d = 5

print (count_triangles(a, b, c, d), end = '\n')

# This code is contributed by PratikBasu    
```

## C#

```
// C# implementation to count the
// number of possible triangles
// for the given sides ranges
using System;

class GFG{

// Function to count the number of
// possible triangles for the given
// sides ranges
public static int count_triangles(int a, int b,
                                  int c, int d)
{
    int ans = 0;

    // Iterate for every possible of x
    for(int x = a; x <= b; ++x)
    {

        // Range of y is [b, c]
        // From this range First
        // we will find the number
        // of x + y greater than d
        int num_greater_than_d = Math.Max(d, c + x) -
                                 Math.Max(d, b + x - 1);

        // For x+y greater than d
        // we can choose all z from [c, d]
        // Total permutation will be
        ans += num_greater_than_d * (d - c + 1);

        // Now we will find the number
        // of x+y in between the [c, d]
        int r = Math.Min(Math.Max(c, c + x), d) - c;
        int l = Math.Min(Math.Max(c, b + x - 1), d) - c;

        // [l, r] will be the range
        // from total [c, d] x+y belongs
        // For any r such that r = x+y
        // We can choose z, in the range
        // [c, d] only less than r,
        // Thus total permutation be
        int x1 = (r * (r + 1)) / 2;
        int x2 = (l * (l + 1)) / 2;

        ans += x1 - x2;
    }
    return ans;
}

// Driver Code
public static void Main(String []args)
{
    int a = 2, b = 3, c = 4, d = 5;

    Console.WriteLine(count_triangles(a, b, c, d));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript implementation to count the
// number of possible triangles
// for the given sides ranges

// Function to count the number of
// possible triangles for the given
// sides ranges
function count_triangles(a , b, c , d)
{
    var ans = 0;

    // Iterate for every possible of x
    for(x = a; x <= b; ++x)
    {

        // Range of y is [b, c]
        // From this range First
        // we will find the number
        // of x + y greater than d
        var num_greater_than_d = Math.max(d, c + x) -
                                 Math.max(d, b + x - 1);

        // For x+y greater than d
        // we can choose all z from [c, d]
        // Total permutation will be
        ans += num_greater_than_d * (d - c + 1);

        // Now we will find the number
        // of x+y in between the [c, d]
        var r = Math.min(Math.max(c, c + x), d) - c;
        var l = Math.min(Math.max(c, b + x - 1), d) - c;

        // [l, r] will be the range
        // from total [c, d] x+y belongs
        // For any r such that r = x+y
        // We can choose z, in the range
        // [c, d] only less than r,
        // Thus total permutation be
        var x1 = (r * (r + 1)) / 2;
        var x2 = (l * (l + 1)) / 2;

        ans += x1 - x2;
    }
    return ans;
}

// Driver Code

var a = 2, b = 3, c = 4, d = 5;

document.write(count_triangles(a, b, c, d));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
7
```