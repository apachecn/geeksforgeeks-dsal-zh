# 所有 N 位阿姆斯特朗数的异或和或

> 原文:[https://www . geeksforgeeks . org/xor-and-or-of-all-n-digits-Armstrong-numbers/](https://www.geeksforgeeks.org/xor-and-or-of-all-n-digit-armstrong-numbers/)

给定一个整数 **N** ，任务是找出所有 **N 位** [阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)的**异或**和**或**值。

**示例**

> **输入:** N = 3
> **输出:** XOR = 271，OR = 511
> 153，370，371，407 是三位数的阿姆斯特朗数
> 
> **输入:** N = 4
> **输出:** XOR = 880，OR = 10098

**进场:**

*   通过以下方式找到 N 位阿姆斯特朗号码的起始号码和结束号码:

```
Starting N-digit Armstrong number = pow(10, n - 1)
Ending N-digit Armstrong number   = pow(10, n) - 1
```

*   从起始数字到结束数字，反复检查 N 位阿姆斯特朗数字，并检查该数字是否为阿姆斯特朗。
*   如果这个数是阿姆斯特朗，那么分别取这个数的异或和或。
*   否则继续进行下一次迭代，并在所有迭代后打印异或和或的值。

下面是上述方法的实现:

## C++14

```
// C++ program to find the XOR
// and OR of all Armstrong numbers
// of N digits
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is Armstrong or not
bool isArmstrong(int x, int n)
{
    int sum1 = 0;
    int temp = x;
    while (temp > 0) {
        int digit = temp % 10;
        sum1 += (int)pow(digit, n);
        temp /= 10;
    }
    return sum1 == x;
}

// Function to find XOR of all
// N-digits Armstrong number
void CalculateXORandOR(int n)
{

    // To store the XOR and OR of all
    // Armstrong number
    int CalculateXOR = 0;
    int CalculateOR = 0;

    // Starting N-digit
    // Armstrong number
    int start = (int)pow(10, n - 1);

    // Ending N-digit
    // Armstrong number
    int end = (int)pow(10, n) - 1;

    // Iterate over starting and
    // ending number
    for (int i = start; i < end + 1; i++)
    {

        // To check if i is
        // Armstrong or not
        if (isArmstrong(i, n)) {
            CalculateXOR = CalculateXOR ^ i;
            CalculateOR = CalculateOR | i;
        }
    }

    // Print the XOR and OR of all
    // Armstrong number
    cout << "XOR = " << CalculateXOR << endl;
    cout << "OR = " << CalculateOR << endl;
}

// Driver Code
int main()
{

    int n = 4;
    CalculateXORandOR(n);
}

// This code is contributed by shivanisinghss2110
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the XOR
// and OR of all Armstrong numbers
// of N digits
class GFG
{

    // Function to check if a number
    // is Armstrong or not
    static boolean isArmstrong(int x, int n) {
        int sum1 = 0;
        int temp = x;
        while (temp > 0) {
            int digit = temp % 10;
            sum1 += Math.pow(digit, n);
            temp /= 10;
        }
        return sum1 == x;
    }

    // Function to find XOR of all
    // N-digits Armstrong number
    static void CalculateXORandOR(int n) {

        // To store the XOR and OR of all
        // Armstrong number
        int CalculateXOR = 0;
        int CalculateOR = 0;

        // Starting N-digit
        // Armstrong number
        int start = (int) Math.pow(10, n - 1);

        // Ending N-digit
        // Armstrong number
        int end = (int) (Math.pow(10, n)) - 1;

        // Iterate over starting and
        // ending number
        for (int i = start; i < end + 1; i++) {

            // To check if i is
            // Armstrong or not
            if (isArmstrong(i, n)) {
                CalculateXOR = CalculateXOR ^ i;
                CalculateOR = CalculateOR | i;
            }
        }

        // Print the XOR and OR of all
        // Armstrong number
        System.out.println("XOR = " + CalculateXOR);
        System.out.println("OR = " + CalculateOR);
    }

    // Driver Code
    public static void main(String[] args) {

        int n = 4;
        CalculateXORandOR(n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the XOR
# and OR of all Armstrong numbers
# of N digits

# Function to check if a number
# is Armstrong or not
def isArmstrong (x, n):
    sum1 = 0 
    temp = x 
    while temp > 0:
        digit = temp % 10
        sum1 += digit **n
        temp //= 10
    return sum1 == x

# Function to find XOR of all
# N-digits Armstrong number
def CalculateXORandOR(n) :

    # To store the XOR and OR of all
    # Armstrong number
    CalculateXOR = 0
    CalculateOR = 0

    # Starting N-digit
    # Armstrong number
    start = 10 ** (n - 1)

    # Ending N-digit
    # Armstrong number
    end = (10**n) - 1
    # Iterate over starting and
    # ending number
    for i in range( start, end + 1) :

        # To check if i is
        # Armstrong or not
        if (isArmstrong(i, n)) :
            CalculateXOR = CalculateXOR ^ i
            CalculateOR = CalculateOR | i

    # Print the XOR and OR of all
    # Armstrong number
    print("XOR = ", CalculateXOR)
    print("OR = ", CalculateOR)

# Driver Code
if __name__ == "__main__" :

    n = 4;
    CalculateXORandOR(n);
```

## C#

```
// C# program to find the XOR
// and OR of all Armstrong numbers
// of N digits
using System;

class GFG
{

    // Function to check if a number
    // is Armstrong or not
    static bool isArmstrong(int x, int n) {
        int sum1 = 0;
        int temp = x;
        while (temp > 0) {
            int digit = temp % 10;
            sum1 += (int)Math.Pow(digit, n);
            temp /= 10;
        }
        return sum1 == x;
    }

    // Function to find XOR of all
    // N-digits Armstrong number
    static void CalculateXORandOR(int n) {

        // To store the XOR and OR of all
        // Armstrong number
        int CalculateXOR = 0;
        int CalculateOR = 0;

        // Starting N-digit
        // Armstrong number
        int start = (int) Math.Pow(10, n - 1);

        // Ending N-digit
        // Armstrong number
        int end = (int) (Math.Pow(10, n)) - 1;

        // Iterate over starting and
        // ending number
        for (int i = start; i < end + 1; i++) {

            // To check if i is
            // Armstrong or not
            if (isArmstrong(i, n)) {
                CalculateXOR = CalculateXOR ^ i;
                CalculateOR = CalculateOR | i;
            }
        }

        // Print the XOR and OR of all
        // Armstrong number
        Console.WriteLine("XOR = " + CalculateXOR);
        Console.WriteLine("OR = " + CalculateOR);
    }

    // Driver Code
    public static void Main(String[] args) {

        int n = 4;
        CalculateXORandOR(n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the XOR
// and OR of all Armstrong numbers
// of N digits

// Function to check if a number
// is Armstrong or not
function isArmstrong(x, n)
{
    let sum1 = 0;
    let temp = x;

    while (temp > 0)
    {
        let digit = temp % 10;
        sum1 += Math.pow(digit, n);
        temp = parseInt(temp / 10, 10);
    }
    return (sum1 == x);
}

// Function to find XOR of all
// N-digits Armstrong number
function CalculateXORandOR(n)
{

    // To store the XOR and OR of all
    // Armstrong number
    let CalculateXOR = 0;
    let CalculateOR = 0;

    // Starting N-digit
    // Armstrong number
    let start = Math.pow(10, n - 1);

    // Ending N-digit
    // Armstrong number
    let end = (Math.pow(10, n)) - 1;

    // Iterate over starting and
    // ending number
    for(let i = start; i < end + 1; i++)
    {

        // To check if i is
        // Armstrong or not
        if (isArmstrong(i, n))
        {
            CalculateXOR = CalculateXOR ^ i;
            CalculateOR = CalculateOR | i;
        }
    }

    // Print the XOR and OR of all
    // Armstrong number
    document.write("XOR = " + CalculateXOR + "</br>");
    document.write("OR = " + CalculateOR + "</br>");
}

// Driver code
let n = 4;
CalculateXORandOR(n);

// This code is contributed by divyeshrabadiya07  

</script>
```

**Output:** 

```
XOR =  880
OR =  10098
```

时间复杂度:O((10<sup>n</sup>–10<sup>n-1</sup>)* log<sub>10</sub>n)

辅助空间:0(1)