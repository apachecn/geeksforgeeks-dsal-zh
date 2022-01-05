# 给定两个算术序列中最不常见的元素

> 原文:[https://www . geesforgeks . org/给定两个算术序列中最不常见的元素/](https://www.geeksforgeeks.org/least-common-element-in-given-two-arithmetic-sequences/)

给定四个正数 **A、B、C、D** ，使得 A 和 B 分别是第一算术序列的第一项和公共差，而 C 和 D 分别表示第二算术序列的相同，如下所示:

> 第一算术序列: **A，A + B，A + 2B，A + 3B，…。**
> 第二等差数列: **C，C + D，C + 2D，C + 3D，…。**

任务是从上面的 [AP](https://www.geeksforgeeks.org/progressions-ap-gp-hp/) 序列中找到最不常见的元素。如果没有，则打印 **-1** 。

**示例:**

> **输入:** A = 2，B = 20，C = 19，D = 9
> **输出:** 82
> **解释:**
> 序列 1: {2，2 + 20，2 + 2(20)，2 + 3(20)，2+4(20)……..} = {2，22，42，62， **82** ，…..}
> 序列 2: {19，19 + 9，19 + 2(9)，19 + 3(9)，19 + 4(9)，19 + 5(9)，19 + 6(9)，19 + 7(9) …..} = {19，28，37，46，55，64，73， **82** ，…..}
> 因此，82 是最小的公共元素。
> 
> **输入:** A = 2，B = 18，C = 19，D = 9
> **输出:** -1

**进场:**

由于给定的两个序列的任意项都可以表示为 **A + x*B** 和 **C + y*D** ，因此，为了解决这个问题，我们需要找到两项相等的 x 和 y 的最小值。
按照以下步骤解决问题:

*   为了找到在两个 [AP 序列](https://www.geeksforgeeks.org/progressions-ap-gp-hp/)中共同的最小值，想法是找到满足以下等式的 x 和 y 的最小整数值:

> A + x*B = C + y*D
> 
> = >以上方程可以重新排列为
> x * B = C–A+y * D
> =>以上方程可以进一步重新排列为
> x =(C–A+y * D)/B

*   检查是否存在**(C–A+y * D)% B**为 **0** 的整数值 **y** 。如果存在，那么最小的数字是 **(C + y*D)** 。
*   检查 **(C + y*D)** 是否为答案，其中 **y** 会在一个范围内 **(0，B)** 因为从 **i = B，B+1，** …。剩余值将被重复。
*   如果以上步骤没有得到这样的数字，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest element
// common in both the subsequences
long smallestCommon(long a, long b,
                    long c, long d)
{
    // If a is equal to c
    if (a == c)
        return a;

    // If a exceeds c
    if (a > c) {
        swap(a, c);
        swap(b, d);
    }

    long first_term_diff = (c - a);
    long possible_y;

    // Check for the satisfying
    // equation
    for (possible_y = 0; possible_y < b; possible_y++) {

        // Least value of possible_y
        // satisfying the given equation
        // will yield true in the below if
        // and break the loop
        if ((first_term_diff % b
             + possible_y * d)
                % b
            == 0) {
            break;
        }
    }

    // If the value of possible_y
    // satisfying the given equation
    // lies in range [0, b]
    if (possible_y != b) {
        return c + possible_y * d;
    }

    // If no value of possible_y
    // satisfies the given equation
    return -1;
}

// Driver Code
int main()
{
    long A = 2, B = 20, C = 19, D = 9;
    cout << smallestCommon(A, B, C, D);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the smallest element
// common in both the subsequences
static int smallestCommon(int a, int b,
                          int c, int d)
{
    // If a is equal to c
    if (a == c)
        return a;

    // If a exceeds c
    if (a > c)
    {
        swap(a, c);
        swap(b, d);
    }

    int first_term_diff = (c - a);
    int possible_y;

    // Check for the satisfying
    // equation
    for (possible_y = 0;
         possible_y < b; possible_y++)
    {

        // Least value of possible_y
        // satisfying the given equation
        // will yield true in the below if
        // and break the loop
        if ((first_term_diff % b +
             possible_y * d) % b == 0)
        {
            break;
        }
    }

    // If the value of possible_y
    // satisfying the given equation
    // lies in range [0, b]
    if (possible_y != b)
    {
        return c + possible_y * d;
    }

    // If no value of possible_y
    // satisfies the given equation
    return -1;
}

static void swap(int x, int y)
{
      int temp = x;
      x = y;
      y = temp;
}

// Driver Code
public static void main(String[] args)
{
    int A = 2, B = 20, C = 19, D = 9;
    System.out.print(smallestCommon(A, B, C, D));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the smallest element
# common in both the subsequences
def smallestCommon(a, b, c, d):

    # If a is equal to c
    if (a == c):
        return a;

    # If a exceeds c
    if (a > c):
        swap(a, c);
        swap(b, d);

    first_term_diff = (c - a);
    possible_y = 0;

    # Check for the satisfying
    # equation
    for possible_y in range(b):

        # Least value of possible_y
        # satisfying the given equation
        # will yield True in the below if
        # and break the loop
        if ((first_term_diff % b +
             possible_y * d) % b == 0):
            break;

    # If the value of possible_y
    # satisfying the given equation
    # lies in range [0, b]
    if (possible_y != b):
        return c + possible_y * d;

    # If no value of possible_y
    # satisfies the given equation
    return -1;

def swap(x, y):
    temp = x;
    x = y;
    y = temp;

# Driver Code
if __name__ == '__main__':
    A = 2; B = 20; C = 19; D = 9;
    print(smallestCommon(A, B, C, D));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the smallest element
// common in both the subsequences
static int smallestCommon(int a, int b,
                          int c, int d)
{
    // If a is equal to c
    if (a == c)
        return a;

    // If a exceeds c
    if (a > c)
    {
        swap(a, c);
        swap(b, d);
    }

    int first_term_diff = (c - a);
    int possible_y;

    // Check for the satisfying
    // equation
    for (possible_y = 0;
         possible_y < b; possible_y++)
    {

        // Least value of possible_y
        // satisfying the given equation
        // will yield true in the below if
        // and break the loop
        if ((first_term_diff % b +
             possible_y * d) % b == 0)
        {
            break;
        }
    }

    // If the value of possible_y
    // satisfying the given equation
    // lies in range [0, b]
    if (possible_y != b)
    {
        return c + possible_y * d;
    }

    // If no value of possible_y
    // satisfies the given equation
    return -1;
}

static void swap(int x, int y)
{
      int temp = x;
      x = y;
      y = temp;
}

// Driver Code
public static void Main(String[] args)
{
    int A = 2, B = 20, C = 19, D = 9;
    Console.Write(smallestCommon(A, B, C, D));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program for the
// above approach

// Function to find the smallest element
// common in both the subsequences
function smallestCommon(a, b, c, d)
{
    // If a is equal to c
    if (a == c)
        return a;

    // If a exceeds c
    if (a > c)
    {
        swap(a, c);
        swap(b, d);
    }

    let first_term_diff = (c - a);
    let possible_y;

    // Check for the satisfying
    // equation
    for (possible_y = 0;
         possible_y < b; possible_y++)
    {

        // Least value of possible_y
        // satisfying the given equation
        // will yield true in the below if
        // and break the loop
        if ((first_term_diff % b +
             possible_y * d) % b == 0)
        {
            break;
        }
    }

    // If the value of possible_y
    // satisfying the given equation
    // lies in range [0, b]
    if (possible_y != b)
    {
        return c + possible_y * d;
    }

    // If no value of possible_y
    // satisfies the given equation
    return -1;
}

function swap(x, y)
{
      let temp = x;
      x = y;
      y = temp;
}

// Driver Code

    let A = 2, B = 20, C = 19, D = 9;
    document.write(smallestCommon(A, B, C, D));

</script>
```

**Output:** 

```
82
```

***时间复杂度:** O(B)*
***辅助空间:** O(1)*