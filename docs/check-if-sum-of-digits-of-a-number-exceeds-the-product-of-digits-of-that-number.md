# 检查一个数字的位数总和是否超过该数字位数的乘积

> 原文:[https://www . geesforgeks . org/检查数字总和是否超过该数字的乘积/](https://www.geeksforgeeks.org/check-if-sum-of-digits-of-a-number-exceeds-the-product-of-digits-of-that-number/)

给定一个正整数 **N** ，任务是检查[的**N**T5 的位数之和是否严格大于](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)[的**N**T9 的位数之积。如果发现**为真**，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)

**示例:**

> **输入:** N = 1234
> **输出:**否
> **说明:**
> N(= 1234)位数之和为= 1 + 2 + 3 + 4 = 10。
> N(= 1234)位数的乘积是 1*2*3*4 = 24。
> 由于位数之和小于数组的乘积。因此，打印编号。
> 
> **输入:**N = 1024
> T3】输出:是

**方法:**按照以下步骤解决给定问题:

*   初始化两个变量，将**sumofdigt**表示为 **0** ，将**prodofdigt**表示为 **1** ，存储 **N** 位数的和与积。
*   [迭代直到](https://www.geeksforgeeks.org/python-while-loops/) **N** 大于 **0** 并执行以下步骤:
    *   找到 **N** 的最后一位数字，并将其存储在一个变量中，比如**雷姆**。
    *   将**sumofdigt**的值增加 **rem** 。
    *   将**生产 git** 的值更新为**生产 git*rem** 。
*   完成上述步骤后，如果**sumofdigt**的值大于**prodofdigt**，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if the sum of the
// digits of N is strictly greater than
// the product of the digits of N or not
void check(int n)
{
    // Stores the sum and the product of
    // the digits of N
    int sumOfDigit = 0;
    int prodOfDigit = 1;

    while (n > 0) {

        // Stores the last digit if N
        int rem;
        rem = n % 10;

        // Increment the value of
        // sumOfDigits
        sumOfDigit += rem;

        // Update the prodOfDigit
        prodOfDigit *= rem;

        // Divide N by 10
        n /= 10;
    }

    // Print the result
    if (sumOfDigit > prodOfDigit)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    int N = 1234;
    check(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the sum of the
// digits of N is strictly greater than
// the product of the digits of N or not
static void check(int n)
{

    // Stores the sum and the product of
    // the digits of N
    int sumOfDigit = 0;
    int prodOfDigit = 1;

    while (n > 0)
    {

        // Stores the last digit if N
        int rem;
        rem = n % 10;

        // Increment the value of
        // sumOfDigits
        sumOfDigit += rem;

        // Update the prodOfDigit
        prodOfDigit *= rem;

        // Divide N by 10
        n /= 10;
    }

    // Print the result
    if (sumOfDigit > prodOfDigit)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int N = 1234;

    check(N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the sum of the
# digits of N is strictly greater than
# the product of the digits of N or not
def check(n):

    # Stores the sum and the product of
    # the digits of N
    sumOfDigit = 0
    prodOfDigit = 1

    while n > 0:

        # Stores the last digit if N
        rem = n % 10

        # Increment the value of
        # sumOfDigits
        sumOfDigit += rem

        # Update the prodOfDigit
        prodOfDigit *= rem

        # Divide N by 10
        n = n // 10

    # Print the result
    if sumOfDigit > prodOfDigit:
        print("Yes")
    else:
        print("No")

# Driver Code
N = 1234

check(N)

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the sum of the
// digits of N is strictly greater than
// the product of the digits of N or not
static void check(int n)
{

    // Stores the sum and the product of
    // the digits of N
    int sumOfDigit = 0;
    int prodOfDigit = 1;

    while (n > 0)
    {

        // Stores the last digit if N
        int rem;
        rem = n % 10;

        // Increment the value of
        // sumOfDigits
        sumOfDigit += rem;

        // Update the prodOfDigit
        prodOfDigit *= rem;

        // Divide N by 10
        n /= 10;
    }

    // Print the result
    if (sumOfDigit > prodOfDigit)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main()
{
    int N = 1234;

    check(N);

}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the sum of the
// digits of N is strictly greater than
// the product of the digits of N or not
function check(n)
{

    // Stores the sum and the product of
    // the digits of N
    let sumOfDigit = 0;
    let prodOfDigit = 1;

    while (n > 0)
    {

        // Stores the last digit if N
        let rem;
        rem = n % 10;

        // Increment the value of
        // sumOfDigits
        sumOfDigit += rem;

        // Update the prodOfDigit
        prodOfDigit *= rem;

        // Divide N by 10
        n = Math.floor(n / 10);
    }

    // Prlet the result
    if (sumOfDigit > prodOfDigit)
        document.write("Yes");
    else
        document.write("No");
}

// Driver Code

    let N = 1234;

    check(N);   

</script>
```

**Output:** 

```
No
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*