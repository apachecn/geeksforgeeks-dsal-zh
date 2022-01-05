# 检查给定坐标

能否形成直角三角形

> 原文:[https://www . geeksforgeeks . org/check-if-a-直角三角形-可由给定坐标形成/](https://www.geeksforgeeks.org/check-if-a-right-angled-triangle-can-be-formed-by-the-given-coordinates/)

给定三个笛卡尔坐标，任务是检查给定的坐标是否可以形成直角三角形。如果可以创建一个[直角三角形](https://www.geeksforgeeks.org/find-sides-right-angled-triangle-given-hypotenuse-area/)，打印**是**。否则，打印**否**。
**举例:**

> **输入:** X1=0，Y1=5，X2=19，Y2=5，X3=0，Y3=0
> **输出:**是
> **说明:**
> 侧连接点(X1，Y1)和(X2，Y2)的长度为 12。
> 侧连接点(X2，Y2)和(X3，Y3)的长度为 15。
> 侧连接点(X1，Y1)和(X3，Y3)的长度为 9。
> 12<sup>2</sup>+9<sup>2</sup>= 15<sup>2</sup>。
> 因此可以做成直角三角形。
> 
> **输入:** X1=5，Y1=14，X2=6，Y2=13，X3=8，Y3 = 7
> T3】输出:否

**方法:**
想法是用[毕达哥拉斯定理](https://en.wikipedia.org/wiki/Pythagorean_theorem)检查直角三角形是否可能。通过连接给定的坐标计算三角形三条边的长度。让边为 ***A，B*** ，和 ***C.*** 给定的三角形是直角的当且仅当***A<sup>2</sup>+B<sup>2</sup>= C<sup>2</sup>。*** 如果条件成立，打印*是*。否则，打印*号*

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if right-angled
// triangle can be formed by the
// given coordinates
void checkRightAngled(int X1, int Y1,
                      int X2, int Y2,
                      int X3, int Y3)
{
    // Calculate the sides
    int A = (int)pow((X2 - X1), 2)
            + (int)pow((Y2 - Y1), 2);

    int B = (int)pow((X3 - X2), 2)
            + (int)pow((Y3 - Y2), 2);

    int C = (int)pow((X3 - X1), 2)
            + (int)pow((Y3 - Y1), 2);

    // Check Pythagoras Formula
    if ((A > 0 and B > 0 and C > 0)
        and (A == (B + C) or B == (A + C)
             or C == (A + B)))
        cout << "Yes";

    else
        cout << "No";
}

// Driver Code
int main()
{
    int X1 = 0, Y1 = 2;
    int X2 = 0, Y2 = 14;
    int X3 = 9, Y3 = 2;

    checkRightAngled(X1, Y1, X2,
                     Y2, X3, Y3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if right-angled
// triangle can be formed by the
// given coordinates
static void checkRightAngled(int X1, int Y1,
                             int X2, int Y2,
                             int X3, int Y3)
{

    // Calculate the sides
    int A = (int)Math.pow((X2 - X1), 2) +
            (int)Math.pow((Y2 - Y1), 2);

    int B = (int)Math.pow((X3 - X2), 2) +
            (int)Math.pow((Y3 - Y2), 2);

    int C = (int)Math.pow((X3 - X1), 2) +
            (int)Math.pow((Y3 - Y1), 2);

    // Check Pythagoras Formula
    if ((A > 0 && B > 0 && C > 0) &&
        (A == (B + C) || B == (A + C) ||
         C == (A + B)))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String s[])
{
    int X1 = 0, Y1 = 2;
    int X2 = 0, Y2 = 14;
    int X3 = 9, Y3 = 2;

    checkRightAngled(X1, Y1, X2, Y2, X3, Y3);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check if right-angled
# triangle can be formed by the
# given coordinates
def checkRightAngled(X1, Y1, X2,
                     Y2, X3, Y3):

    # Calculate the sides
    A = (int(pow((X2 - X1), 2)) +
         int(pow((Y2 - Y1), 2)))
    B = (int(pow((X3 - X2), 2)) +
         int(pow((Y3 - Y2), 2)))
    C = (int(pow((X3 - X1), 2)) +
         int(pow((Y3 - Y1), 2)))

    # Check Pythagoras Formula
    if ((A > 0 and B > 0 and C > 0) and
        (A == (B + C) or B == (A + C) or
         C == (A + B))):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__=='__main__':

    X1 = 0; X2 = 0; X3 = 9;
    Y1 = 2; Y2 = 14; Y3 = 2;

    checkRightAngled(X1, Y1, X2,
                     Y2, X3, Y3)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if right-angled
// triangle can be formed by the
// given coordinates
static void checkRightAngled(int X1, int Y1,
                             int X2, int Y2,
                             int X3, int Y3)
{

    // Calculate the sides
    int A = (int)Math.Pow((X2 - X1), 2) +
            (int)Math.Pow((Y2 - Y1), 2);

    int B = (int)Math.Pow((X3 - X2), 2) +
            (int)Math.Pow((Y3 - Y2), 2);

    int C = (int)Math.Pow((X3 - X1), 2) +
            (int)Math.Pow((Y3 - Y1), 2);

    // Check Pythagoras Formula
    if ((A > 0 && B > 0 && C > 0) &&
        (A == (B + C) || B == (A + C) ||
         C == (A + B)))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main(String []s)
{
    int X1 = 0, Y1 = 2;
    int X2 = 0, Y2 = 14;
    int X3 = 9, Y3 = 2;

    checkRightAngled(X1, Y1, X2, Y2, X3, Y3);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach
      // Function to check if right-angled
      // triangle can be formed by the
      // given coordinates
      function checkRightAngled
      (X1, Y1, X2, Y2, X3, Y3)
      {
        // Calculate the sides
        var A = Math.pow(X2 - X1, 2) +
        Math.pow(Y2 - Y1, 2);

        var B = Math.pow(X3 - X2, 2) +
        Math.pow(Y3 - Y2, 2);

        var C = Math.pow(X3 - X1, 2) +
        Math.pow(Y3 - Y1, 2);

        // Check Pythagoras Formula
        if (
          A > 0 &&
          B > 0 &&
          C > 0 &&
          (A === B + C || B === A + C ||
          C === A + B)
        )
          document.write("Yes");
        else document.write("No");
      }

      // Driver Code
      var X1 = 0,
        Y1 = 2;
      var X2 = 0,
        Y2 = 14;
      var X3 = 9,
        Y3 = 2;
      checkRightAngled(X1, Y1, X2, Y2, X3, Y3);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*