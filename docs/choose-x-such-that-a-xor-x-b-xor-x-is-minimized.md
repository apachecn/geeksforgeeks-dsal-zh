# 选择 X，使得(A 异或 X) + (B 异或 X)最小化

> 原文:[https://www . geesforgeks . org/choose-x-so-a-xor-x-B- xor-x-is-minimum/](https://www.geeksforgeeks.org/choose-x-such-that-a-xor-x-b-xor-x-is-minimized/)

给定两个整数 **A** 和 **B** 。任务是选择一个整数 **X** ，使得 **(A xor X) + (B xor X)** 为最小可能。

**示例:**

> **输入:** A = 2，B = 3
> T3】输出: X = 2，和= 1
> 
> **输入:** A = 7，B = 8
> T3】输出: X = 0，Sum = 15

一个**简单的解决方案**是将 **A** 和 **B** 与 **X ≤ min(A，B)** 的所有可能值进行异或运算，生成所有可能的和。要生成所有可能的和，需要 **O(N)** 时间，其中 **N = min(A，B)** 。

一个**有效的解决方案**是基于这样的事实，即数字 **X** 将只包含该索引处的设置位，其中 **A** 和 **B** 都包含一个设置位，从而在与 **X** 进行异或运算后，该位将被取消设置。这将只需要**0(对数 N)** 时间。
**其他情况:**如果在特定索引处，一个或两个数字包含 **0** (未设置位)，而数字 **X** 包含 **1** (设置位)，那么 **0** 将在与 **A** 和 **B** 中的 **X** 进行异或运算后进行设置，则总和无法最小化。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the integer X such that
// (A xor X) + (B ^ X) is minimized
int findX(int A, int B)
{
    int j = 0, x = 0;

    // While either A or B is non-zero
    while (A || B) {

        // Position at which both A and B
        // have a set bit
        if ((A & 1) && (B & 1)) {

            // Inserting a set bit in x
            x += (1 << j);
        }

        // Right shifting both numbers to
        // traverse all the bits
        A >>= 1;
        B >>= 1;
        j += 1;
    }
    return x;
}

// Driver code
int main()
{
    int A = 2, B = 3;
    int X = findX(A, B);

    cout << "X = " << X << ", Sum = " << (A ^ X) + (B ^ X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the integer X such that
    // (A xor X) + (B ^ X) is minimized
    static int findX(int A, int B)
    {
        int j = 0, x = 0;

        // While either A or B is non-zero
        while (A != 0 || B != 0) {

            // Position at which both A and B
            // have a set bit
            if ((A % 2 == 1) && (B % 2 == 1)) {

                // Inserting a set bit in x
                x += (1 << j);
            }

            // Right shifting both numbers to
            // traverse all the bits
            A >>= 1;
            B >>= 1;
            j += 1;
        }
        return x;
    }

    // Driver code
    public static void main(String[] args)
    {
        int A = 2, B = 3;
        int X = findX(A, B);

        System.out.println(
            "X = " + X + ", Sum = " + ((A ^ X) + (B ^ X)));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the integer X such that
# (A xor X) + (B ^ X) is minimized

def findX(A, B):
    j = 0
    x = 0

    # While either A or B is non-zero
    while (A or B):

        # Position at which both A and B
        # have a set bit
        if ((A & 1) and (B & 1)):

            # Inserting a set bit in x
            x += (1 << j)

        # Right shifting both numbers to
        # traverse all the bits
        A >>= 1
        B >>= 1
        j += 1
    return x

# Driver code
if __name__ == '__main__':
    A = 2
    B = 3
    X = findX(A, B)

    print("X =", X, ", Sum =", (A ^ X) + (B ^ X))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the integer X such that
    // (A xor X) + (B ^ X) is minimized
    static int findX(int A, int B)
    {
        int j = 0, x = 0;

        // While either A or B is non-zero
        while (A != 0 || B != 0) {

            // Position at which both A and B
            // have a set bit
            if ((A % 2 == 1) && (B % 2 == 1)) {

                // Inserting a set bit in x
                x += (1 << j);
            }

            // Right shifting both numbers to
            // traverse all the bits
            A >>= 1;
            B >>= 1;
            j += 1;
        }
        return x;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int A = 2, B = 3;
        int X = findX(A, B);

        Console.WriteLine(
            "X = " + X + ", Sum = " + ((A ^ X) + (B ^ X)));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the integer X such that
// (A xor X) + (B ^ X) is minimized
function findX($A, $B)
{
    $j = 0;
    $x = 0;

    // While either A or B is non-zero
    while ($A || $B) {

        // Position at which both A and B
        // have a set bit
        if (($A & 1) && ($B & 1))
        {

            // Inserting a set bit in x
            $x += (1 << $j);
        }

        // Right shifting both numbers to
        // traverse all the bits
        $A >>= 1;
        $B >>= 1;
        $j += 1;
    }
    return $x;
}

// Driver code
    $A = 2;
    $B = 3;
    $X = findX($A, $B);

    echo "X = " , $X , ", Sum = ",
        ($A ^ $X) + ($B ^ $X);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the integer X such that
    // (A xor X) + (B ^ X) is minimized
    function findX(A, B)
    {
        let j = 0, x = 0;

        // While either A or B is non-zero
        while (A != 0 || B != 0) {

            // Position at which both A and B
            // have a set bit
            if ((A % 2 == 1) && (B % 2 == 1)) {

                // Inserting a set bit in x
                x += (1 << j);
            }

            // Right shifting both numbers to
            // traverse all the bits
            A >>= 1;
            B >>= 1;
            j += 1;
        }
        return x;
    }

    let A = 2, B = 3;
    let X = findX(A, B);

    document.write("X = " + X + ", Sum = " + ((A ^ X) + (B ^ X)));

        // This code is contributed by suresh07.
</script>
```

**Output**

```
X = 2, Sum = 1
```

时间复杂度:0(对数(最大值(A，B))

辅助空间:0(1)

**最有效的方法:**

利用 **X** 将只包含设定位为 A 和 B 的思想， **X = A & B** 。替换 x 时，上述等式变为**(a ^(a&b))+(b ^(a&b))**，这进一步等同于 **A^B** 。

```
Proof:
Given (A ^ X) + (B ^ X)
Taking X = (A & B), we have 
(A ^ (A & B)) + (B ^ (A & B))
 (using x ^ y = x'y + y'x )
= (A'(A & B) + A(A & B)') + (B'(A & B) + B(A & B)')
   (using (x & y)' = x' + y')
= (A'(A & B) + A(A' + B')) + (B'(A & B) + B(A' + B'))
  (A'(A & B) = A'A & A'B = 0, B'(A & B) 
 = B'A & B'B = 0)
= (A(A' + B')) + (B(A' + B'))                               
= (AA' + AB') + (BA' + BB')
  (using xx' = x'x = 0)                                   
= (AB') + (BA')                                             
= (A ^ B)
```

点击此处了解更多布尔属性。

下面是上述方法的实现:

## C++

```
// c++ implementation of above approach
#include <iostream>
using namespace std;

// finding X
int findX(int A, int B) {
  return A & B;
}

// finding Sum
int findSum(int A, int B) {
  return A ^ B;
}

// Driver code
int main()
{
    int A = 2, B = 3;
    cout << "X = " << findX(A, B)
         << ", Sum = " << findSum(A, B);
    return 0;
}

// This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{
    // finding X
    public static int findX(int A, int B)
    {
      return A & B;
    }

    // finding Sum
    public static int findSum(int A, int B)
    {
        return A ^ B;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A = 2, B = 3;
        System.out.print("X = " + findX(A, B)
                         + ", Sum = " + findSum(A, B));
    }
}
// This code is contributed by yashbeersingh42
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# finding X
def findX(A, B):
    return A & B

# finding Sum
def findSum(A, B):
    return A ^ B

# Driver code
A, B = 2, 3
print("X =", findX(A, B) , ", Sum =" , findSum(A, B))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation of above approach
using System;

class GFG{

// Finding X
public static int findX(int A, int B)
{
    return A & B;
}

// Finding Sum
public static int findSum(int A, int B)
{
    return A ^ B;
}

// Driver Code
public static void Main(String[] args)
{
    int A = 2, B = 3;

    Console.Write("X = " + findX(A, B) +
                  ", Sum = " + findSum(A, B));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // finding X
    function findX(A, B) {
      return A & B;
    }

    // finding Sum
    function findSum(A, B) {
      return A ^ B;
    }

    let A = 2, B = 3;
    document.write("X = " + findX(A, B) + ", Sum = " + findSum(A, B));

</script>
```

**Output**

```
X = 2, Sum = 1
```

时间复杂度:0(1)

辅助空间:0(1)