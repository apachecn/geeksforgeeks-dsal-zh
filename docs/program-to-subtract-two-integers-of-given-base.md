# 给定基数减去两个整数的程序

> 原文:[https://www . geeksforgeeks . org/给定基数的减二整数程序/](https://www.geeksforgeeks.org/program-to-subtract-two-integers-of-given-base/)

给定三个正整数 **X** 、 **Y** 和 **B** ，其中 **X** 和 **Y** 为 **Base-B** 整数，任务是求**X–Y**的值，使得 **X > = Y** 。

**示例:**

> **输入:** X = 1212，Y = 256，B = 8
> **输出:** 0734
> **说明:**8 进制 1212–256 的值为 734 **。**
> 
> **输入:** X = 546，Y = 248，B = 9
> T3】输出: 287

**方法:**给定的问题可以用基础数学减法求解。按照以下步骤解决给定的问题:

*   初始化两个变量**功率= 1** 、**进位= 0** ，分别记录当前功率和减法时产生的进位。
*   初始化一个变量，比如 **finalVal = 0** ，以存储**X–Y**的结果值。
*   [循环](https://www.geeksforgeeks.org/range-based-loop-c/)直到 **X > 0** 并执行以下步骤:
    *   将 **X** 和 **Y** 当前值的最后几个数字存储在两个变量中，分别表示 **n1 = X % 10** 和 **n2 = Y % 10** 。
    *   通过更新 **X = X / 10** 和 **Y = Y / 10** ，删除 **X** 和 **Y** 的最后一位数字。
    *   初始化**温度= n1–N2+进位**。
    *   如果**温度<为 0** ，则在 **N** 上加上基数 **B** ，即 **N = N + B** ，设置**进位= -1** ，作为借项。否则，设置**进位= 0** 。
    *   将当前 **temp * power** 加到 finalVal，即**final val = final val+temp * power**，设置 **power = power * 10** 。
*   完成上述步骤后，打印**最终值**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find X - Y in base B
int getDifference(int B, int X, int Y)
{

    // To store final answer
    int finalVal = 0;

    // To store carry generated
    int carry = 0;

    // To keep track of power
    int power = 1;

    while (X > 0) {

        // Store last digits of current
        // value of X and Y in n1 and
        // n2 respectively
        int n1 = X % 10;
        int n2 = Y % 10;

        // Remove last digits from
        // X and Y
        X = X / 10;
        Y = Y / 10;

        int temp = n1 - n2 + carry;

        if (temp < 0) {

            // Carry = -1 will act
            // as borrow
            carry = -1;
            temp += B;
        }

        else {
            carry = 0;
        }

        // Add in final result
        finalVal += temp * power;
        power = power * 10;
    }

    // Return final result
    return finalVal;
}

// Driver Code
int main()
{
    int X = 1212;
    int Y = 256;
    int B = 8;

    cout << (getDifference(B, X, Y));

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find X - Y in base B
    public static int getDifference(
        int B, int X, int Y)
    {

        // To store final answer
        int finalVal = 0;

        // To store carry generated
        int carry = 0;

        // To keep track of power
        int power = 1;

        while (X > 0) {

            // Store last digits of current
            // value of X and Y in n1 and
            // n2 respectively
            int n1 = X % 10;
            int n2 = Y % 10;

            // Remove last digits from
            // X and Y
            X = X / 10;
            Y = Y / 10;

            int temp = n1 - n2 + carry;

            if (temp < 0) {

                // Carry = -1 will act
                // as borrow
                carry = -1;
                temp += B;
            }

            else {
                carry = 0;
            }

            // Add in final result
            finalVal += temp * power;
            power = power * 10;
        }

        // Return final result
        return finalVal;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int X = 1212;
        int Y = 256;
        int B = 8;

        System.out.println(
            getDifference(B, X, Y));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find X - Y in base B
def getDifference(B, X, Y) :

    # To store final answer
    finalVal = 0;

    # To store carry generated
    carry = 0;

    # To keep track of power
    power = 1;

    while (X > 0) :

        # Store last digits of current
        # value of X and Y in n1 and
        # n2 respectively
        n1 = X % 10;
        n2 = Y % 10;

        # Remove last digits from
        # X and Y
        X = X // 10;
        Y = Y // 10;

        temp = n1 - n2 + carry;

        if (temp < 0) :

            # Carry = -1 will act
            # as borrow
            carry = -1;
            temp += B;

        else :
            carry = 0;

        # Add in final result
        finalVal += temp * power;
        power = power * 10;

    # Return final result
    return finalVal;

# Driver Code
if __name__ == "__main__" :

    X = 1212;
    Y = 256;
    B = 8;

    print(getDifference(B, X, Y));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to find X - Y in base B
    public static int getDifference(int B, int X, int Y)
    {

        // To store final answer
        int finalVal = 0;

        // To store carry generated
        int carry = 0;

        // To keep track of power
        int power = 1;

        while (X > 0) {

            // Store last digits of current
            // value of X and Y in n1 and
            // n2 respectively
            int n1 = X % 10;
            int n2 = Y % 10;

            // Remove last digits from
            // X and Y
            X = X / 10;
            Y = Y / 10;

            int temp = n1 - n2 + carry;

            if (temp < 0) {

                // Carry = -1 will act
                // as borrow
                carry = -1;
                temp += B;
            }

            else {
                carry = 0;
            }

            // Add in final result
            finalVal += temp * power;
            power = power * 10;
        }

        // Return final result
        return finalVal;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int X = 1212;
        int Y = 256;
        int B = 8;

        Console.WriteLine(getDifference(B, X, Y));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find X - Y in base B
function getDifference(B, X, Y) {
  // To store final answer
  let finalVal = 0;

  // To store carry generated
  let carry = 0;

  // To keep track of power
  let power = 1;

  while (X > 0) {
    // Store last digits of current
    // value of X and Y in n1 and
    // n2 respectively
    let n1 = X % 10;
    let n2 = Y % 10;

    // Remove last digits from
    // X and Y
    X = Math.floor(X / 10);
    Y = Math.floor(Y / 10);

    let temp = n1 - n2 + carry;

    if (temp < 0) {
      // Carry = -1 will act
      // as borrow
      carry = -1;
      temp += B;
    } else {
      carry = 0;
    }

    // Add in final result
    finalVal += temp * power;
    power = power * 10;
  }

  // Return final result
  return finalVal;
}

// Driver Code

let X = 1212;
let Y = 256;
let B = 8;

document.write(getDifference(B, X, Y));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
734
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*