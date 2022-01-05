# 最小的 N 位数，没有一个数字作为除数

> 原文:[https://www . geeksforgeeks . org/最小 n 位数字，没有任何数字作为除数/](https://www.geeksforgeeks.org/smallest-n-digit-number-with-none-of-its-digits-as-its-divisor/)

给定一个整数 **N** 。任务是找到最小的 N 位数 **S** ，这样 **S** 就不能被它的任何一位数字整除。如果没有这样的数字，请打印-1。
**示例:**

> **输入:** N = 2
> **输出:** 23
> **说明:** 23 是最小的两位数，不能被其任何一位数字整除。
> **输入:** N = 1
> **输出:** -1
> **说明:**每个单位数都可以被自己整除。
> **输入:** N = 4
> **输出:** 2227
> **说明:** 2227 是最小的四位数，不能被其任何一位数字整除。

**进场:**

*   方法是找到最小和最大可能的 N 位数，比如说这些数字分别是 **L** 和 **R** 。
*   迭代范围**【L，R】**。
*   对于该范围内的每个数字，提取该数字的每个数字，并检查该数字是否可被该数字整除。
*   如果该数字中至少有一个数字被除，则丢弃该数字并迭代检查下一个数字。
*   如果那个数字没有一个数字除它，那么打印那个数字并且打破循环。这样找到的这个数是最小的数。

以下是上述方法的实现:

## C++

```
// C++ Program for the given problem
#include <bits/stdc++.h>
using namespace std;

// Function to calculate power
int power(int a, int b)
{
    if (b == 0)
        return 1;
    if (b == 1)
        return a;

    int tmp = power(a, b / 2);

    int result = tmp * tmp;

    if (b % 2 == 1)
        result *= a;

    return result;
}

// Function to check if the
// N-digit number satisfies the
// given condition or not
bool check(int n)
{
    int temp = n;
    while (temp > 0) {

        // Getting the last digit
        int last_digit = temp % 10;

        // Every number is divisible
        // by 1 and dividing a number
        // by 0 isn't possible. Thus
        // numbers with 0 as a digit
        // must be discarded.
        if (last_digit == 0
            || last_digit == 1)
            return false;

        // If any digit divides the
        // number, return false
        if (n % last_digit == 0)
            return false;
        temp = temp / 10;
    }

    // If no digit divides the
    // number, return true;
    return true;
}

// Function to find the smallest
// number not divisible by any
// of its digits.
void solve(int n)
{
    // Get the lower range of n
    // digit number
    int L = power(10, n - 1);

    // Get the high range of n
    // digit number
    int R = power(10, n) - 1;

    int flag = 0;

    // check all the N-digit numbers
    for (int i = L; i <= R; i++) {

        bool answer = check(i);

        // If the first number to satisfy
        // the constraints is found
        // print it, set the flag value
        // and break out of the loop.
        if (answer == true) {

            cout << i << endl;
            flag++;
            break;
        }
    }

    // If no such digit found,
    // return -1 as per problem statement
    if (flag == 0)
        cout << -1 << endl;
}

// Driver Code
int main()
{
    int N = 4;
    solve(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the given problem
import java.util.*;

class GFG{

// Function to calculate power
static int power(int a, int b)
{
    if (b == 0)
        return 1;
    if (b == 1)
        return a;

    int tmp = power(a, b / 2);
    int result = tmp * tmp;

    if (b % 2 == 1)
        result *= a;

    return result;
}

// Function to check if the
// N-digit number satisfies the
// given condition or not
static boolean check(int n)
{
    int temp = n;
    while (temp > 0)
    {

        // Getting the last digit
        int last_digit = temp % 10;

        // Every number is divisible
        // by 1 and dividing a number
        // by 0 isn't possible. Thus
        // numbers with 0 as a digit
        // must be discarded.
        if (last_digit == 0 ||
            last_digit == 1)
            return false;

        // If any digit divides the
        // number, return false
        if (n % last_digit == 0)
            return false;
        temp = temp / 10;
    }

    // If no digit divides the
    // number, return true;
    return true;
}

// Function to find the smallest
// number not divisible by any
// of its digits.
static void solve(int n)
{

    // Get the lower range of n
    // digit number
    int L = power(10, n - 1);

    // Get the high range of n
    // digit number
    int R = power(10, n) - 1;

    int flag = 0;

    // Check all the N-digit numbers
    for(int i = L; i <= R; i++)
    {
        boolean answer = check(i);

        // If the first number to satisfy
        // the constraints is found
        // print it, set the flag value
        // and break out of the loop.
        if (answer == true)
        {
            System.out.println(i);
            flag++;
            break;
        }
    }

    // If no such digit found,
    // return -1 as per problem statement
    if (flag == 0)
    System.out.println("-1");
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    solve(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 Program for the
# given problem

# Function to calculate
# power
def power(a, b):

    if (b == 0):
        return 1;
    if (b == 1):
        return a;

    tmp = power(a, b // 2); 
    result = tmp * tmp;

    if (b % 2 == 1):
        result *= a;

    return result;

# Function to check if the
# N-digit number satisfies the
# given condition or not
def check(n):

    temp = n;
    while (temp > 0):

        # Getting the last digit
        last_digit = temp % 10;

        # Every number is divisible
        # by 1 and dividing a number
        # by 0 isn't possible. Thus
        # numbers with 0 as a digit
        # must be discarded.
        if (last_digit == 0 or
            last_digit == 1):
            return False;

        # If any digit divides the
        # number, return false
        if (n % last_digit == 0):
            return False;

        temp = temp // 10;    

    # If no digit divides the
    # number, return true;
    return True;

# Function to find the smallest
# number not divisible by any
# of its digits.
def solve(n):

    # Get the lower range of n
    # digit number
    L = power(10, n - 1);

    # Get the high range of n
    # digit number
    R = power(10, n) - 1;

    flag = 0;

    # check all the N-digit
    # numbers
    for i in range(L, R + 1):
        answer = check(i);

        # If the first number to satisfy
        # the constraints is found
        # print it, set the flag value
        # and break out of the loop.
        if (answer):           
            print(i)
            flag += 1;
            break;

    # If no such digit found,
    # return -1 as per problem
    # statement
    if (flag == 0):
        print(-1)

# Driver code
if __name__ == "__main__":

    N = 4;
    solve(N);

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the given problem
using System;

class GFG{

// Function to calculate power
static int power(int a, int b)
{
    if (b == 0)
        return 1;
    if (b == 1)
        return a;

    int tmp = power(a, b / 2);
    int result = tmp * tmp;

    if (b % 2 == 1)
        result *= a;

    return result;
}

// Function to check if the
// N-digit number satisfies the
// given condition or not
static bool check(int n)
{
    int temp = n;
    while (temp > 0)
    {

        // Getting the last digit
        int last_digit = temp % 10;

        // Every number is divisible
        // by 1 and dividing a number
        // by 0 isn't possible. Thus
        // numbers with 0 as a digit
        // must be discarded.
        if (last_digit == 0 ||
            last_digit == 1)
            return false;

        // If any digit divides the
        // number, return false
        if (n % last_digit == 0)
            return false;
        temp = temp / 10;
    }

    // If no digit divides the
    // number, return true;
    return true;
}

// Function to find the smallest
// number not divisible by any
// of its digits.
static void solve(int n)
{

    // Get the lower range of n
    // digit number
    int L = power(10, n - 1);

    // Get the high range of n
    // digit number
    int R = power(10, n) - 1;

    int flag = 0;

    // Check all the N-digit numbers
    for(int i = L; i <= R; i++)
    {
        bool answer = check(i);

        // If the first number to satisfy
        // the constraints is found
        // print it, set the flag value
        // and break out of the loop.
        if (answer == true)
        {
            Console.WriteLine(i);
            flag++;
            break;
        }
    }

    // If no such digit found,
    // return -1 as per problem statement
    if (flag == 0)
    Console.WriteLine("-1");
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;

    solve(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaSCript Program for the given problem

// Function to calculate power
function power(a, b)
{
    if (b == 0)
        return 1;
    if (b == 1)
        return a;

    let tmp = power(a, Math.floor(b / 2));

    let result = tmp * tmp;

    if (b % 2 == 1)
        result *= a;

    return result;
}

// Function to check if the
// N-digit number satisfies the
// given condition or not
function check(n)
{
    let temp = n;
    while (temp > 0) {

        // Getting the last digit
        let last_digit = temp % 10;

        // Every number is divisible
        // by 1 and dividing a number
        // by 0 isn't possible. Thus
        // numbers with 0 as a digit
        // must be discarded.
        if (last_digit == 0
            || last_digit == 1)
            return false;

        // If any digit divides the
        // number, return false
        if (n % last_digit == 0)
            return false;
        temp = Math.floor(temp / 10);
    }

    // If no digit divides the
    // number, return true;
    return true;
}

// Function to find the smallest
// number not divisible by any
// of its digits.
function solve(n)
{
    // Get the lower range of n
    // digit number
    let L = power(10, n - 1);

    // Get the high range of n
    // digit number
    let R = power(10, n) - 1;

    let flag = 0;

    // check all the N-digit numbers
    for (let i = L; i <= R; i++) {

        let answer = check(i);

        // If the first number to satisfy
        // the constraints is found
        // print it, set the flag value
        // and break out of the loop.
        if (answer === true) {

            document.write(i + "<br>");
            flag++;
            break;
        }
    }

    // If no such digit found,
    // return -1 as per problem statement
    if (flag === 0)
        document.write("-1" + "<br>");
}

// Driver Code

    let N = 4;
    solve(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2227
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*