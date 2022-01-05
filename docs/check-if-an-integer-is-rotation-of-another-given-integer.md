# 检查一个整数是否是另一个给定整数的旋转

> 原文:[https://www . geeksforgeeks . org/check-如果一个整数是另一个给定整数的旋转/](https://www.geeksforgeeks.org/check-if-an-integer-is-rotation-of-another-given-integer/)

给定两个整数 **A** 和 **B** ，任务是检查整数 **A** 是否是整数 **B** 的数字旋转。如果发现属实，则打印**“是”**。否则打印**“否”**。

**例:**

> **输入:** A= 976，B = 679
> T3】输出:是
> 
> **输入:** A= 974，B = 2345
> T3】输出:否

**方法:**按照以下步骤解决问题:

*   如果 **A == B** ，则打印**“是”**。
*   计算变量中整数 **A** 和 **B** 的位数，比如**数字 1** 和**数字 2** 。
*   如果 **dig1！= dig2** 被发现为真，则打印**“否”**。
*   初始化一个变量，比如**温度**。分配**温度= A** 。
*   现在，迭代并执行以下操作:
    *   [如果 **A** 等于 **B** 和](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)断开，则打印**“是”**。
    *   检查 **(A==温度)**即 **A** 是否等于原始整数**温度**。如果发现是真的，则打印**“否”**并断开。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the integer
// A is a rotation of the integer B
int check(int A, int B)
{

    if (A == B) {
        return 1;
    }

    // Stores the count of digits in A
    int dig1 = floor(log10(A) + 1);

    // Stores the count of digits in B
    int dig2 = floor(log10(B) + 1);

    // If dig1 not equal to dig2
    if (dig1 != dig2) {
        return 0;
    }

    int temp = A;

    while (1) {

        // Stores position of first digit
        int power = pow(10, dig1 - 1);

        // Stores the first digit
        int firstdigit = A / power;

        // Rotate the digits of the integer
        A = A - firstdigit * power;
        A = A * 10 + firstdigit;

        // If A is equal to B
        if (A == B) {
            return 1;
        }
        // If A is equal to the initial
// value of integer A
        if (A == temp) {
            return 0;
        }
    }
}

// Driver Code
int main()
{
    int A = 967, B = 679;

    if (check(A, B))
        cout << "Yes";
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
class GFG {

    // Function to check if the integer
    // A is a rotation of the integer B
    static int check(int A, int B)
    {

        if (A == B) {
            return 1;
        }

        // Stores the count of digits in A
        int dig1 = (int)Math.floor(Math.log10(A) + 1);

        // Stores the count of digits in B
        int dig2 = (int)Math.floor(Math.log10(B) + 1);

        // If dig1 not equal to dig2
        if (dig1 != dig2) {
            return 0;
        }

        int temp = A;

        while (true) {

            // Stores position of first digit
            int power = (int)Math.pow(10, dig1 - 1);

            // Stores the first digit
            int firstdigit = A / power;

            // Rotate the digits of the integer
            A = A - firstdigit * power;
            A = A * 10 + firstdigit;

            // If A is equal to B
            if (A == B) {
                return 1;
            }
            // If A is equal to the initial
            // value of integer A
            if (A == temp) {
                return 0;
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A = 967, B = 679;

        if (check(A, B) == 1)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to check if the integer
# A is a rotation of the integer B
def check(A, B) :

    if (A == B) :
        return 1

    # Stores the count of digits in A
    dig1 = math.floor(math.log10(A) + 1)

    # Stores the count of digits in B
    dig2 = math.floor(math.log10(B) + 1)

    # If dig1 not equal to dig2
    if (dig1 != dig2) :
        return 0

    temp = A

    while (True) :

        # Stores position of first digit
        power = pow(10, dig1 - 1)

        # Stores the first digit
        firstdigit = A // power

        # Rotate the digits of the integer
        A = A - firstdigit * power
        A = A * 10 + firstdigit

        # If A is equal to B
        if (A == B) :
            return 1

        # If A is equal to the initial value of integer A
        if (A == temp) :
            return 0

          # Driver code
A, B = 967, 679

if (check(A, B)) :
    print("Yes")
else :
    print("No")

    # This code is contributed by divyesh072019.
```

## C#

```
// C# implementation of the approach
using System;
public class GFG
{

    // Function to check if the integer
    // A is a rotation of the integer B
    static int check(int A, int B)
    {
        if (A == B)
        {
            return 1;
        }

        // Stores the count of digits in A
        int dig1 = (int)Math.Floor(Math.Log10(A) + 1);

        // Stores the count of digits in B
        int dig2 = (int)Math.Floor(Math.Log10(B) + 1);

        // If dig1 not equal to dig2
        if (dig1 != dig2)
        {
            return 0;
        }
        int temp = A;
        while (true)
        {

            // Stores position of first digit
            int power = (int)Math.Pow(10, dig1 - 1);

            // Stores the first digit
            int firstdigit = A / power;

            // Rotate the digits of the integer
            A = A - firstdigit * power;
            A = A * 10 + firstdigit;

            // If A is equal to B
            if (A == B)
            {
                return 1;
            }

            // If A is equal to the initial
            // value of integer A
            if (A == temp)
            {
                return 0;
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int A = 967, B = 679;
        if (check(A, B) == 1)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to check if the integer
    // A is a rotation of the integer B
    function check(A, B)
    {
        if (A == B)
        {
            return 1;
        }

        // Stores the count of digits in A
        let dig1 = Math.floor(Math.log10(A) + 1);

        // Stores the count of digits in B
        let dig2 = Math.floor(Math.log10(B) + 1);

        // If dig1 not equal to dig2
        if (dig1 != dig2)
        {
            return 0;
        }
        let temp = A;
        while (true)
        {

            // Stores position of first digit
            let power = Math.pow(10, dig1 - 1);

            // Stores the first digit
            let firstdigit = parseInt(A / power, 10);

            // Rotate the digits of the integer
            A = A - firstdigit * power;
            A = A * 10 + firstdigit;

            // If A is equal to B
            if (A == B)
            {
                return 1;
            }

            // If A is equal to the initial
            // value of integer A
            if (A == temp)
            {
                return 0;
            }
        }
    }

    let A = 967, B = 679;
    if (check(A, B) == 1)
      document.write("Yes");
    else
      document.write("No");

  // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(数字(N))*
***辅助空间:** O(1)*