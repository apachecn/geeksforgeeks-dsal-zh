# 检查一个数是否可以表示为两个连续完美立方体的和

> 原文:[https://www . geesforgeks . org/check-如果一个数字可以表示为两个连续完美立方体的总和/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-sum-of-two-consecutive-perfect-cubes/)

给定一个整数 **N** ，任务是检查这个数是否可以表示为两个连续的[完美立方体](https://www.geeksforgeeks.org/tag/maths-perfect-cube/)的和。

**示例:**

> **输入:** N = 35
> **输出:**是
> **说明:**
> 既然，35 = 2 <sup>3</sup> + 3 <sup>3</sup> ，那么要求的答案是肯定的。
> 
> **输入:**N = 14
> T3】输出:否

**天真法:**解决问题最简单的方法是从 1 迭代到**N**T5】的[立方根，检查任意两个连续数的完美立方之和是否等于 **N** 。如果发现是真的，打印“是”。否则，打印“否”。](https://www.geeksforgeeks.org/find-cubic-root-of-a-number/)

下面是上述方法的实现:

## C++

```
// C++ Program of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// can be expressed as the sum of
// cubes of two consecutive numbers
bool isCubeSum(int n)
{
    for (int i = 1; i * i * i <= n; i++) {
        if (i * i * i
                + (i + 1) * (i + 1) * (i + 1)
            == n)
            return true;
    }
    return false;
}

// Driver Code
int main()
{
    int n = 35;

    if (isCubeSum(n))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;

class GFG{

// Function to check if a number
// can be expressed as the sum of
// cubes of two consecutive numbers
static boolean isCubeSum(int n)
{
    for(int i = 1; i * i * i <= n; i++)
    {
        if (i * i * i + (i + 1) *
              (i + 1) * (i + 1) == n)
            return true;
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int n = 35;

    if (isCubeSum(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

# Function to check if a number
# can be expressed as the sum of
# cubes of two consecutive numbers
def isCubeSum(n):

    for i in range(1, int(pow(n, 1 / 3)) + 1):
        if (i * i * i + (i + 1) *
              (i + 1) * (i + 1) == n):
            return True;

    return False;

# Driver Code
if __name__ == '__main__':

    n = 35;

    if (isCubeSum(n)):
        print("Yes");
    else:
        print("No");

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program of the
// above approach
using System;

class GFG{

// Function to check if a number
// can be expressed as the sum of
// cubes of two consecutive numbers
static bool isCubeSum(int n)
{
    for(int i = 1; i * i * i <= n; i++)
    {
        if (i * i * i + (i + 1) *
              (i + 1) * (i + 1) == n)
            return true;
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 35;

    if (isCubeSum(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript Program of the
// above approach

// Function to check if a number
// can be expressed as the sum of
// cubes of two consecutive numbers
function isCubeSum(n)
{
    for (var i = 1; i * i * i <= n; i++) {
        if (i * i * i
                + (i + 1) * (i + 1) * (i + 1)
            == n)
            return true;
    }
    return false;
}

// Driver Code
var n = 35;
if (isCubeSum(n))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

**高效方法:**上述方法可以基于以下观察进行优化:

*   如果两个连续数的立方根之和等于 **N** ，则一个数可以表示为两个连续数的完美立方之和。
*   这可以通过公式来检查:

> ![\lfloor \sqrt[3]{N} - 1 \rfloor ^3 + \lfloor \sqrt[3]{N} \rfloor^3](img/5099047ed84a4888c1a272daf37c567c.png "Rendered by QuickLaTeX.com")

*   例如，如果 **N = 35** ，那么检查下面的等式是否等于 **N** :

> ![\lfloor \sqrt[3]{35} - 1 \rfloor ^3 + \lfloor \sqrt[3]{35} \rfloor^3      ](img/186de6e093dd94ae0627bef531980e94.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ Program to
// implement above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check that a number
// is the sum of cubes of 2
// consecutive numbers or not
bool isSumCube(int N)
{
    int a = cbrt(N);
    int b = a - 1;

    // Condition to check if a
    // number is the sum of cubes of 2
    // consecutive numbers or not
    return ((a * a * a + b * b * b) == N);
}

// Driver Code
int main()
{
    int i = 35;
    // Function call
    if (isSumCube(i)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// above approach
class GFG{

// Function to check that a number
// is the sum of cubes of 2
// consecutive numbers or not
static boolean isSumCube(int N)
{
    int a = (int)Math.cbrt(N);
    int b = a - 1;

    // Condition to check if a
    // number is the sum of cubes of 2
    // consecutive numbers or not
    return ((a * a * a + b * b * b) == N);
}

// Driver Code
public static void main(String[] args)
{
    int i = 35;

    // Function call
    if (isSumCube(i))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to
# implement above approach

# Function to check that a number
# is the sum of cubes of 2
# consecutive numbers or not
def isSumCube(N):

    a = int(pow(N, 1 / 3))
    b = a - 1

    # Condition to check if a
    # number is the sum of cubes of 2
    # consecutive numbers or not
    ans = ((a * a * a + b * b * b) == N)

    return ans

# Driver Code
i = 35

# Function call
if(isSumCube(i)):
    print("Yes")
else:
    print("No")

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// above approach
using System;
class GFG{

// Function to check that a number
// is the sum of cubes of 2
// consecutive numbers or not
static bool isSumCube(int N)
{
  int a = (int)Math.Pow(N, (double) 1 / 3);
  int b = a - 1;

  // Condition to check if a
  // number is the sum of cubes of 2
  // consecutive numbers or not
  return ((a * a * a + b * b * b) == N);
}

// Driver Code
public static void Main(String[] args)
{
  int i = 35;

  // Function call
  if (isSumCube(i))
  {
    Console.Write("Yes");
  }
  else
  {
    Console.Write("No");
  }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// above approach   

// Function to check that a number
// is the sum of cubes of 2
// consecutive numbers or not
function isSumCube(N)
{
    var a = parseInt(Math.cbrt(N));
    var b = a - 1;

    // Condition to check if a
    // number is the sum of cubes of 2
    // consecutive numbers or not
    return ((a * a * a + b * b * b) == N);
}

// Driver Code
var i = 35;

// Function call
if (isSumCube(i))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)