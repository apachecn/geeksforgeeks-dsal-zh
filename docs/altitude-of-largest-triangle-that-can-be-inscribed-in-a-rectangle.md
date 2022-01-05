# 可在矩形内接的最大三角形的高度

> 原文:[https://www . geesforgeks . org/矩形内接最大三角形高度/](https://www.geeksforgeeks.org/altitude-of-largest-triangle-that-can-be-inscribed-in-a-rectangle/)

给定一个长度为 **L** 和宽度为 **B、**的矩形，任务是打印最大的[三角形](https://www.geeksforgeeks.org/c-program-print-floyds-triangle/)可能的最大整数高度，这样三角形的高度应该等于底边的一半。

**示例:**

> **输入:** L = 3，B = 4
> T3】输出: 2
> 
> **输入:** L = 8，B = 9
> T3】输出: 4
> 
> **输入:** L = 325，B = 300
> T3】输出: 162

**天真法:**最简单的方法是反向迭代**【0，min(L，B)】**的范围，如果当前值小于等于 **max(L，B) / 2** ，则打印当前值作为答案，打破循环。

***时间复杂度:** O(min(L，B))*
***辅助空间:** O(1)*

**二分搜索法法:**上述方法可以通过使用[二分搜索法技术](https://www.geeksforgeeks.org/binary-search/)并观察选择矩形最大边长边上的三角形的底边总是最优的这一事实来优化。按照以下步骤解决问题:

*   如果 **L** 大于 **B** ，则交换数值。
*   初始化三个变量，比如说，**低**为 **0，**和**高**为 **L** 在范围**【0，L】上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。**
*   另外，初始化一个变量，说 **res** 为 **0** 来存储高度的最大可能长度。
*   当**低电平**小于或等于**高电平**时迭代，并执行以下步骤:
    *   初始化一个变量，说**中间**，设置为**低+(高–低)/ 2** 。
    *   如果**中间≤ B / 2** 的值，则将**中间**分配给 **res** 和**中间+1** 到**低**。
    *   否则，将**高**设置为**中-1**。
*   最后，完成上述步骤后，打印在 **res** 中获得的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
int largestAltitude(int L, int B)
{
    // If L is greater than B
    if (L > B) {
        swap(B, L);
    }

    // Variables to perform binary
    // search
    int low = 0, high = L;

    // Stores the maximum altitude
    // possible
    int res = 0;

    // Iterate until low is less
    // than high
    while (low <= high) {

        // Stores the mid value
        int mid = low + (high - low) / 2;

        // If mide is less than
        // or equal to the B/2
        if (mid <= (B / 2)) {

            // Update res
            res = mid;

            // Update low
            low = mid + 1;
        }
        else

            // Update high
            high = mid - 1;
    }

    // Print the result
    return res;
}

// Driver Code
int main()
{
    // Given Input
    int L = 3;
    int B = 4;

    // Function call
    cout << largestAltitude(L, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
static int largestAltitude(int L, int B)
{

    // If L is greater than B
    if (L > B)
    {
        int t = L;
        L = B;
        B = t;
    }

    // Variables to perform binary
    // search
    int low = 0, high = L;

    // Stores the maximum altitude
    // possible
    int res = 0;

    // Iterate until low is less
    // than high
    while (low <= high)
    {

        // Stores the mid value
        int mid = low + (high - low) / 2;

        // If mide is less than
        // or equal to the B/2
        if (mid <= (B / 2))
        {

            // Update res
            res = mid;

            // Update low
            low = mid + 1;
        }
        else

            // Update high
            high = mid - 1;
    }

    // Print the result
    return res;
}

// Driver Code
public static void main(String[] args)
{
     // Given Input
    int L = 3;
    int B = 4;

    // Function call
    System.out.print(largestAltitude(L, B));
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the greatest
# altitude of the largest triangle
# triangle that can be inscribed
# in the rectangle
def largestAltitude(L, B):

    # If L is greater than B
    if (L > B):
        temp = B
        B = L
        L = temp

    # Variables to perform binary
    # search
    low = 0
    high = L

    # Stores the maximum altitude
    # possible
    res = 0

    # Iterate until low is less
    # than high
    while (low <= high):
        # Stores the mid value
        mid = low + (high - low) // 2

        # If mide is less than
        # or equal to the B/2
        if (mid <= (B / 2)):
            # Update res
            res = mid

            # Update low
            low = mid + 1

        else:
            # Update high
            high = mid - 1

    # Print the result
    return res

# Driver Code
if __name__ == '__main__':

    # Given Input
    L = 3
    B = 4

    # Function call
    print(largestAltitude(L, B))

    # This ode is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
static int largestAltitude(int L, int B)
{

    // If L is greater than B
    if (L > B)
    {
        int t = L;
        L = B;
        B = t;
    }

    // Variables to perform binary
    // search
    int low = 0, high = L;

    // Stores the maximum altitude
    // possible
    int res = 0;

    // Iterate until low is less
    // than high
    while (low <= high)
    {

        // Stores the mid value
        int mid = low + (high - low) / 2;

        // If mide is less than
        // or equal to the B/2
        if (mid <= (B / 2))
        {

            // Update res
            res = mid;

            // Update low
            low = mid + 1;
        }
        else

            // Update high
            high = mid - 1;
    }

    // Print the result
    return res;
}

// Driver Code
public static void Main(string[] args)
{

    // Given Input
    int L = 3;
    int B = 4;

    // Function call
    Console.Write(largestAltitude(L, B));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
function largestAltitude(L, B) {
  // If L is greater than B
  if (L > B) {
    let temp = B;
    B = L;
    L = temp;
  }

  // Variables to perform binary
  // search
  let low = 0,
    high = L;

  // Stores the maximum altitude
  // possible
  let res = 0;

  // Iterate until low is less
  // than high
  while (low <= high) {
    // Stores the mid value
    let mid = Math.floor(low + (high - low) / 2);

    // If mide is less than
    // or equal to the B/2
    if (mid <= Math.floor(B / 2)) {
      // Update res
      res = mid;

      // Update low
      low = mid + 1;
    }

    // Update high
    else high = mid - 1;
  }

  // Print the result
  return res;
}

// Driver Code

// Given Input
let L = 3;
let B = 4;

// Function call
document.write(largestAltitude(L, B));

</script>
```

**Output**

```
2
```

***时间复杂度:** O(log(min(L，B))*
***辅助空间:** O(1)*

**高效进场:**通过观察将三角形的底边放在长度的边上，**最大(L，B** )高度将等于**最小(最大(L，B)/2，最小(L，B))** ，可以进一步优化上述进场。按照以下步骤解决问题:

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
int largestAltitude(int L, int B)
{
    // If L is greater than B
    if (L > B)
        swap(L, B);
    // Stores the maximum altitude
    // value
    int res = min(B / 2, L);

    // Return res
    return res;
}

// Driver Code
int main()
{
    // Given Input
    int L = 3;
    int B = 4;

    // Function call
    cout << largestAltitude(L, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C++ program for the above approach
import java.io.*;
class GFG
{

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
static int largestAltitude(int L, int B)
{

    // If L is greater than B
    if (L > B)
        {
        int t = L;
        L = B;
        B = t;
    }

    // Stores the maximum altitude
    // value
    int res = Math.min(B / 2, L);

    // Return res
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int L = 3;
    int B = 4;

    // Function call
    System.out.print( largestAltitude(L, B));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to find the greatest
# altitude of the largest triangle
# triangle that can be inscribed
# in the rectangle
def largestAltitude( L,  B):

    # If L is greater than B
    if (L > B):
        temp = B
        B = L
        L = temp
    # Stores the maximum altitude
    # value
    res = min(B // 2, L)

    # Return res
    return res

# Driver Code
# Given Input
L = 3
B = 4

# Function call
print(largestAltitude(L, B))

# This ode is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
static int largestAltitude(int L, int B)
{

    // If L is greater than B
    if (L > B)
        {
        int t = L;
        L = B;
        B = t;
    }

    // Stores the maximum altitude
    // value
    int res = Math.Min(B / 2, L);

    // Return res
    return res;
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int L = 3;
    int B = 4;

    // Function call
    Console.Write( largestAltitude(L, B));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JAvascript. program for the above approach
// Function to find the greatest
// altitude of the largest triangle
// triangle that can be inscribed
// in the rectangle
function largestAltitude(L, B)
{

    // If L is greater than B
    if (L > B)
        {
        var t = L;
        L = B;
        B = t;
    }

    // Stores the maximum altitude
    // value
    var res = Math.min(B / 2, L);

    // Return res
    return res;
}

// Driver Code
    // Given Input
    var L = 3;
    var B = 4;

    // Function call
    document.write( largestAltitude(L, B));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)