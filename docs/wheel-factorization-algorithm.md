# 轮分解算法

> 原文:[https://www . geesforgeks . org/wheel-因式分解-算法/](https://www.geeksforgeeks.org/wheel-factorization-algorithm/)

给定一个数字 **N** 。任务是检查给定的数字是否是[质数](https://www.geeksforgeeks.org/prime-numbers/)。
**例:**

> **输入:** N = 987
> **输出:**不是素数
> **解释:**
> As，987 = 3*7*47。因此 987 不是质数。
> **输入:** N = 67
> **输出:**质数

**轮因式分解法:**
轮因式分解是对厄拉多塞法[筛的改进。对于轮因式分解，从一个小的数字列表开始，称为**基** —通常是前几个](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质数](https://www.geeksforgeeks.org/prime-numbers/)，然后生成与基的所有数字互质的整数的列表，称为**轮**。然后在**轮**中找到要分解的数的最小除数，在此基础上依次除以数。

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Wheel_factorization-n%3D30.svg/800px-Wheel_factorization-n%3D30.svg.png)

假设我们选择**基础**作为 **{2，3，5}** ，与基础互质的数字为 **{7，11，13，17，19，23，29，31}** 设置为**轮**。
为了更好地理解，请看上图中数字展示的图案。前三个质数的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 为 30。以 7、1 和 3 结尾且不是 2、3 和 5 的倍数的数字(小于 30)，并且总是[素数](https://www.geeksforgeeks.org/prime-numbers/)，即 **{7、11、13、17、19、23、29}** 。把 31 号加到这个列表中，然后如果我们把 **30** 的倍数加到列表中的任何一个数字上，它就会给我们一个[质数](https://www.geeksforgeeks.org/prime-numbers/)。
**车轮分解法算法:**

```
For the number N to be Prime or not:
bool isPrime(x) {
    if (x < 2) {
          return False;
    }
    for N in {2, 3, 5} {
          return False;
    }
    for p= [0, sqrt(N)] such that p = p + 30: {
          for c in [p+7, p+11, p+13, p+17, p+19, p+23, p+29, p+31] {
              if c > sqrt(N)      
                  break;
              else if N % (c+p) = 0:
                  return False;
          }
    }
}
return True;
}
```

**方法:**
以下是上述算法的方法:

1.  对于给定数 **N** 的[素性测试](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)，检查给定数是否能被 2、3、5 中的任何一个整除。
2.  如果该数不能被 2、3、5 中的任何一个整除，则检查列表[7、11、13、17、19、23、29、31]中 30 的倍数相加形成的数是否除以给定数 **N** 。如果是，那么给定的数字不是[质数](https://www.geeksforgeeks.org/prime-numbers/)，否则是[质数](https://www.geeksforgeeks.org/prime-numbers/)。

以下是上述方法的实现:

## C++

```
// C++ program to check if the
// given number is prime using
// Wheel Factorization Method
#include "bits/stdc++.h"
using namespace std;

// Function to check if a given
// number x is prime or not
void isPrime(int N)
{
    bool isPrime = true;
    // The Wheel for checking
    // prime number
    int arr[8] = { 7, 11, 13, 17,
                   19, 23, 29, 31 };

    // Base Case
    if (N < 2) {
        isPrime = false;
    }

    // Check for the number taken
    // as basis
    if (N % 2 == 0 || N % 3 == 0
        || N % 5 == 0) {
        isPrime = false;
    }

    // Check for Wheel
    // Here i, acts as the layer
    // of the wheel
    for (int i = 0; i < sqrt(N); i += 30) {

        // Check for the list of
        // Sieve in arr[]
        for (int c : arr) {

            // If number is greater
            // than sqrt(N) break
            if (c > sqrt(N)) {
                break;
            }

            // Check if N is a multiple
            // of prime number in the
            // wheel
            else {
                if (N % (c + i) == 0) {
                    isPrime = false;
                    break;
                }
            }

            // If at any iteration
            // isPrime is false,
            // break from the loop
            if (!isPrime)
                break;
        }
    }

    if (isPrime)
        cout << "Prime Number";
    else
        cout << "Not a Prime Number";
}

// Driver's Code
int main()
{
    int N = 121;

    // Function call for primality
    // check
    isPrime(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the
// given number is prime using
// Wheel Factorization Method
import java.util.*;

class GFG{

// Function to check if a given
// number x is prime or not
static void isPrime(int N)
{
    boolean isPrime = true;

        // The Wheel for checking
    // prime number
    int []arr = { 7, 11, 13, 17,19, 23, 29, 31 };

    // Base Case
    if (N < 2) {
        isPrime = false;
    }

    // Check for the number taken
    // as basis
    if (N % 2 == 0 || N % 3 == 0
        || N % 5 == 0) {
        isPrime = false;
    }

    // Check for Wheel
    // Here i, acts as the layer
    // of the wheel
    for (int i = 0; i < Math.sqrt(N); i += 30) {

        // Check for the list of
        // Sieve in arr[]
        for (int c : arr) {

            // If number is greater
            // than sqrt(N) break
            if (c > Math.sqrt(N)) {
                break;
            }

            // Check if N is a multiple
            // of prime number in the
            // wheel
            else {
                if (N % (c + i) == 0) {
                    isPrime = false;
                    break;
                }
            }

            // If at any iteration
            // isPrime is false,
            // break from the loop
            if (!isPrime)
                break;
        }
    }

    if (isPrime)
        System.out.println("Prime Number");
    else
        System.out.println("Not a Prime Number");
}

// Driver's Code
public static void main(String args[])
{
    int N = 121;

    // Function call for primality
    // check
    isPrime(N);
}
}

// This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to check if the
// given number is prime using
// Wheel Factorization Method
using System;

class GFG{

// Function to check if a given
// number x is prime or not
static void isPrime(int N)
{
    bool isPrime = true;

     // The Wheel for checking
    // prime number
    int []arr = { 7, 11, 13, 17,19, 23, 29, 31 };

    // Base Case
    if (N < 2) {
        isPrime = false;
    }

    // Check for the number taken
    // as basis
    if (N % 2 == 0 || N % 3 == 0
        || N % 5 == 0) {
        isPrime = false;
    }

    // Check for Wheel
    // Here i, acts as the layer
    // of the wheel
    for (int i = 0; i < (int)Math.Sqrt(N); i += 30) {

        // Check for the list of
        // Sieve in arr[]
        foreach (int c in arr) {

            // If number is greater
            // than sqrt(N) break
            if (c > (int)Math.Sqrt(N)) {
                break;
            }

            // Check if N is a multiple
            // of prime number in the
            // wheel
            else {
                if (N % (c + i) == 0) {
                    isPrime = false;
                    break;
                }
            }

            // If at any iteration
            // isPrime is false,
            // break from the loop
            if (!isPrime)
                break;
        }
    }

    if (isPrime)
        Console.WriteLine("Prime Number");
    else
        Console.WriteLine("Not a Prime Number");
}

// Driver's Code
public static void Main(String []args)
{
    int N = 121;

    // Function call for primality
    // check
    isPrime(N);
}
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3  program to check if the
# given number is prime using
# Wheel Factorization Method
import math

# Function to check if a given
# number x is prime or not
def isPrime( N):

    isPrime = True;
    # The Wheel for checking
    # prime number
    arr= [ 7, 11, 13, 17,
                19, 23, 29, 31 ]

    # Base Case
    if (N < 2) :
        isPrime = False

    # Check for the number taken
    # as basis
    if (N % 2 == 0 or N % 3 == 0
        or N % 5 == 0):
        isPrime = False

    # Check for Wheel
    # Here i, acts as the layer
    # of the wheel
    for i in range(0,int(math.sqrt(N)), 30) :

        # Check for the list of
        # Sieve in arr[]
        for c in  arr:

            # If number is greater
            # than sqrt(N) break
            if (c > int(math.sqrt(N))):
                break

            # Check if N is a multiple
            # of prime number in the
            # wheel
            else :
                if (N % (c + i) == 0) :
                    isPrime = False
                    break

            # If at any iteration
            # isPrime is false,
            # break from the loop
            if (not isPrime):
                break

    if (isPrime):
        print("Prime Number")
    else:
        print("Not a Prime Number")

# Driver's Code
if __name__ == "__main__":
    N = 121

    # Function call for primality
    # check
    isPrime(N)

# This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript program to check if the
// given number is prime using
// Wheel Factorization Method

// Function to check if a given
// number x is prime or not
function isPrime(N)
{
    let isPrime = true;
    // The Wheel for checking
    // prime number
    let arr = [ 7, 11, 13, 17,
                19, 23, 29, 31 ];

    // Base Case
    if (N < 2) {
        isPrime = false;
    }

    // Check for the number taken
    // as basis
    if (N % 2 == 0 || N % 3 == 0
        || N % 5 == 0) {
        isPrime = false;
    }

    // Check for Wheel
    // Here i, acts as the layer
    // of the wheel
    for (let i = 0; i < Math.sqrt(N); i += 30) {

        // Check for the list of
        // Sieve in arr[]
        for (let c of arr) {

            // If number is greater
            // than sqrt(N) break
            if (c > Math.sqrt(N)) {
                break;
            }

            // Check if N is a multiple
            // of prime number in the
            // wheel
            else {
                if (N % (c + i) == 0) {
                    isPrime = false;
                    break;
                }
            }

            // If at any iteration
            // isPrime is false,
            // break from the loop
            if (!isPrime)
                break;
        }
    }

    if (isPrime)
        document.write("Prime Number");
    else
        document.write("Not a Prime Number");
}

// Driver's Code

    let N = 121;

    // Function call for primality
    // check
    isPrime(N);

    // This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Not a Prime Number
```

时间复杂度:O(N <sup>3/2</sup> )

辅助空间:0(1)