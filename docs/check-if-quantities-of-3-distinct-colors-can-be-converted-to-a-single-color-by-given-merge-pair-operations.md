# 检查 3 种不同颜色的数量是否可以通过给定的合并对操作转换成单一颜色

> 原文:[https://www . geeksforgeeks . org/check-如果三种不同颜色的数量可以通过给定的合并对操作转换为单一颜色/](https://www.geeksforgeeks.org/check-if-quantities-of-3-distinct-colors-can-be-converted-to-a-single-color-by-given-merge-pair-operations/)

给定 3 个整数 **R** 、 **G** 和 **B** 分别表示红、绿、蓝 3 种颜色的计数，使得相同数量的两种不同颜色(比如 **X** )结合形成两倍于该数量的第三种颜色 **2 * X** 。任务是检查是否有可能将所有颜色转换为单一颜色。如果可能，则打印**“是”**。否则，打印“**否”**。

**示例:**

> **输入:** R = 1，G = 1，B = 1
> **输出:**是
> **说明:**
> 操作 1:将 1 单位红色和 1 单位蓝色混合，得到 2 单位绿色。
> 因此，每种颜色的计数为:R = 0，G = 3，B = 0
> 因此，所有颜色都转换为单一颜色。
> 
> **输入:** R = 1，G = 6，B = 3
> **输出:**是
> **说明:**
> 操作 1:将 1 单位红色和 1 单位绿色混合，得到 2 单位蓝色。
> 因此，每种颜色的计数为:R = 0，G = 5，B = 5
> 操作 2:将 5 单位的绿色和 5 单位的蓝色混合，得到 10 单位的红色。
> 因此，每种颜色的计数为:R = 10，G = 0，B = 0
> 因此，所有颜色都转换为单一颜色。

**方法:**将所有颜色改为相同颜色意味着任务是达到最终状态，如 **T = (0，0，R + G + B)** 或其其他两种排列中的任何一种。最初状态是 I = (R，G，B)。每次操作后，最初两种颜色的值各减少一，第三种颜色的值增加两。这个操作可以写成基于所选颜色的 **(-1，-1，+2)** 的排列。因此，形成以下等式:

> **N * op**≦**T mod 3**其中，
> T5【N】T6
> 是要执行的操作数量 **op** 是操作
> **T** 是最终状态

使用上面的等式，观察如果两个值在用 3 求模后相等，给定的颜色可以变成一种单一的颜色。因此，请按照以下步骤解决问题:

1.  计算所有给定颜色的[模](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/) 3。
2.  检查是否有相等的配对。
3.  如果发现是真的，打印“**是”**。否则，打印“**否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether it is
// possible to do the operation or not
bool isPossible(int r, int b, int g)
{

    // Calculate modulo 3
    // of all the colors
    r = r % 3;
    b = b % 3;
    g = g % 3;

    // Check for any equal pair
    if (r == b || b == g || g == r) {
        return true;
    }

    // Otherwise
    else {
        return false;
    }
}

// Driver Code
int main()
{
    // Given colors
    int R = 1, B = 3, G = 6;

    // Function Call
    if (isPossible(R, B, G)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to check whether
// it is possible to do the
// operation or not
static boolean isPossible(int r,
                          int b, int g)
{
    // Calculate modulo 3
    // of all the colors
    r = r % 3;
    b = b % 3;
    g = g % 3;

    // Check for any equal pair
    if (r == b || b == g || g == r)
    {
        return true;
    }

    // Otherwise
    else
    {
        return false;
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given colors
    int R = 1, B = 3, G = 6;

    // Function Call
    if (isPossible(R, B, G))
    {
        System.out.print("Yes" + "\n");
    }
    else
    {
        System.out.print("No" + "\n");
    }
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether it is
# possible to do the operation or not
def isPossible(r, b, g):

    # Calculate modulo 3
    # of all the colors
    r = r % 3
    b = b % 3
    g = g % 3

    # Check for any equal pair
    if(r == b or b == g or g == r):
        return True

    # Otherwise
    else:
        return False

# Driver Code

# Given colors
R = 1
B = 3
G = 6

# Function call
if(isPossible(R, B, G)):
    print("Yes")
else:
    print("No")

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to check whether
// it is possible to do the
// operation or not
static bool isPossible(int r,
                       int b, int g)
{
  // Calculate modulo 3
  // of all the colors
  r = r % 3;
  b = b % 3;
  g = g % 3;

  // Check for any equal pair
  if (r == b || b == g || g == r)
  {
    return true;
  }

  // Otherwise
  else
  {
    return false;
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given colors
  int R = 1, B = 3, G = 6;

  // Function Call
  if (isPossible(R, B, G))
  {
    Console.Write("Yes" + "\n");
  }
  else
  {
    Console.Write("No" + "\n");
  }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check whether it is
// possible to do the operation or not
function isPossible(r, b, g)
{

    // Calculate modulo 3
    // of all the colors
    r = r % 3;
    b = b % 3;
    g = g % 3;

    // Check for any equal pair
    if (r == b || b == g || g == r) {
        return true;
    }

    // Otherwise
    else {
        return false;
    }
}

// Driver Code
// Given colors
var R = 1, B = 3, G = 6;
// Function Call
if (isPossible(R, B, G)) {
    document.write( "Yes");
}
else {
    document.write( "No");
}

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)