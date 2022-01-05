# 从它们的和与或中找出两个数字

> 原文:[https://www . geesforgeks . org/find-two-numbers-from-sum-and-or/](https://www.geeksforgeeks.org/find-two-numbers-from-their-sum-and-or/)

给定两个整数 **X** 和 **Y** ，任务是找出两个数字，它们的[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 是 **X** ，它们的和是 **Y** 。如果不存在这样的整数，则打印**-1”**。

**示例:**

> **输入:** X = 7，Y = 11
> **输出:** 4 7
> **说明:**
> 4 和 7 的按位 OR 为 7，两个整数之和为 4 + 7 = 11，满足给定条件。
> 
> **输入:** X = 11，Y = 7
> **输出:** -1

**天真方法:**解决给定问题的最简单方法是生成数组的所有可能对，如果存在满足给定条件的对，则打印该对。否则，打印**-1”**。

***时间复杂度:** O(Y)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用[逐位运算符](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/)的属性进行优化。考虑任意两个整数 **A** 和 **B** ，那么两个整数之和可以表示为 **A + B = (A & B) + (A | B)** 。现在，放置变量 **X** 和 **Y** ，并将等式更改为:

> = >**Y =(A&B)+X**
> =>**(A&B)= Y–X**
> 因此可以用这个方程推导出上面的观测值。

按照以下步骤解决给定的问题:

*   如果 **Y** 的值小于 **X** ，则不会有解，因为 [**按位 AND**](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/) 运算总是非负的。
*   现在对于 **X** 和 **Y** 的逐位表示中的 **K <sup>第</sup>位**位，如果该位在 **(A & B)** 中为 **'1'** ，在 **(A | B)** 中为**“0”**，则没有可能的解决方案。这是因为如果两个数的位“与”是 **1** ，那么位“或”也应该是 **1** 。
*   否则总是可以选择两个整数 **A** 和 **B** ，可以计算为**A = Y–X**和 **B = X** 。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define MaxBit 32
using namespace std;

// Function to find the two integers from
// the given sum and Bitwise OR value
int possiblePair(int X, int Y)
{
    int Z = Y - X;

    // Check if Z is non negative
    if (Z < 0) {
        cout << "-1";
        return 0;
    }

    // Iterate through all the bits
    for (int k = 0; k < MaxBit; k++) {

        // Find the kth bit of A & B
        int bit1 = (Z >> k) & 1;

        // Find the kth bit of A | B
        int bit2 = (Z >> k) & 1;

        // If bit1 = 1 and bit2 = 0, then
        // there will be no possible pairs
        if (bit1 && !bit2) {
            cout << "-1";
            return 0;
        }
    }

    // Print the possible pairs
    cout << Z << ' ' << X;

    return 0;
}

// Driver Code
int main()
{
    int X = 7, Y = 11;
    possiblePair(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

static int MaxBit = 32;

// Function to find the two integers from
// the given sum and Bitwise OR value
static void possiblePair(int X, int Y)
{
    int Z = Y - X;

    // Check if Z is non negative
    if (Z < 0) {
        System.out.print("-1");
    }

    // Iterate through all the bits
    for (int k = 0; k < MaxBit; k++) {

        // Find the kth bit of A & B
        int bit1 = (Z >> k) & 1;

        // Find the kth bit of A | B
        int bit2 = (Z >> k) & 1;

        // If bit1 = 1 and bit2 = 0, then
        // there will be no possible pairs
        if (bit1 != 0 && bit2 == 0) {
            System.out.print("-1");
        }
    }

    // Print the possible pairs
    System.out.print( Z + " " + X);

}

// Driver Code
public static void main(String[] args)

{
    int X = 7, Y = 11;
    possiblePair(X, Y);
}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
MaxBit = 32

# Function to find the two integers from
# the given sum and Bitwise OR value
def possiblePair(X, Y):
    Z = Y - X

    # Check if Z is non negative
    if (Z < 0):
        print("-1")
        return 0

    # Iterate through all the bits
    for k in range(MaxBit):

        # Find the kth bit of A & B
        bit1 = (Z >> k) & 1

        # Find the kth bit of A | B
        bit2 = (Z >> k) & 1

        # If bit1 = 1 and bit2 = 0, then
        # there will be no possible pairs
        if (bit1 == 1 and bit2 == 0):
            print("-1")
            return 0

    # Print the possible pairs
    print(Z, X)

    return 0

# Driver Code
if __name__ == '__main__':
    X = 7
    Y = 11
    possiblePair(X, Y)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
//C# code for the above approach
using System;

public class GFG{

static int MaxBit = 32;

// Function to find the two integers from
// the given sum and Bitwise OR value
static void possiblePair(int X, int Y)
{
    int Z = Y - X;

    // Check if Z is non negative
    if (Z < 0) {
        Console.Write("-1");
    }

    // Iterate through all the bits
    for (int k = 0; k < MaxBit; k++) {

        // Find the kth bit of A & B
        int bit1 = (Z >> k) & 1;

        // Find the kth bit of A | B
        int bit2 = (Z >> k) & 1;

        // If bit1 = 1 and bit2 = 0, then
        // there will be no possible pairs
        if (bit1 != 0 && bit2 == 0) {
            Console.Write("-1");
        }
    }

    // Print the possible pairs
    Console.Write( Z + " " + X);

}

// Driver Code

    static public void Main (){

        // Code
      int X = 7, Y = 11;
    possiblePair(X, Y);
    }
}
// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>
// Javascript program for the above approach
let MaxBit = 32;

// Function to find the two integers from
// the given sum and Bitwise OR value
function possiblePair(X, Y) {
  let Z = Y - X;

  // Check if Z is non negative
  if (Z < 0) {
    document.write("-1");
    return 0;
  }

  // Iterate through all the bits
  for (let k = 0; k < MaxBit; k++) {
    // Find the kth bit of A & B
    let bit1 = (Z >> k) & 1;

    // Find the kth bit of A | B
    let bit2 = (Z >> k) & 1;

    // If bit1 = 1 and bit2 = 0, then
    // there will be no possible pairs
    if (bit1 && !bit2) {
      document.write("-1");
      return 0;
    }
  }

  // Print the possible pairs
  document.write(Z + " " + X);

  return 0;
}

// Driver Code

let X = 7,
  Y = 11;
possiblePair(X, Y);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
4 7
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)