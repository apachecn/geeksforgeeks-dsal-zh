# 由数字总和为 N 的非重复数字组成的最小正数

> 原文:[https://www . geesforgeks . org/最小正数-由非重复数字组成-其数字总和为-n/](https://www.geeksforgeeks.org/smallest-positive-number-made-up-of-non-repeating-digits-whose-sum-of-digits-is-n/)

给定一个正整数 **N** ，任务是找出由不同数字组成的最小正数，这些数字的[和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)等于 **N** 。如果没有，打印**-1”**。

**示例:**

> **输入:** N = 11
> **输出:** 29
> **说明:**位数之和= 2 + 9 = 11 ( = N)。
> 
> **输入:** N = 46
> **输出:** -1

**方法:**该想法基于以下观察:

*   **如果 N < 10:** 必选答案为 **N** 本身。
*   **如果 N > 45:** 必选答案为 **-1** 因为可以用不重复数字做的最小数字是 123456789，其数字之和为 45。
*   **否则:**可根据以下模式得出答案。

> 考虑下面的例子，为了理解这个模式，
> 
> 对于 N = 10:输出为 19。
> 对于 N = 11:输出为 29。
> 对于 N = 12:输出为 39。
> N = 13:输出为 49。
> ……
> N = 21:输出 489。
> 对于 N = 22:输出为 589。
> 对于 N = 23:输出为 689。
> 
> 观察上述结果，很明显，答案包含从一个数字开始直到数字和小于 n 的递减顺序的数字，其差值为 1

按照以下步骤解决问题:

*   如果给定的数字小于 10，则打印数字本身。
*   如果给定数值大于 45，则打印**-1”**。
*   否则，请执行以下步骤:
    *   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **res** 来存储需要的答案并初始化一个变量，比如说**数字**，作为 **9** 。
    *   [循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)直到 **N ≤数字**并执行以下步骤:
        *   [在**RES**T5 开始时按下**数字**。](https://www.geeksforgeeks.org/stdstringinsert-in-c/)
        *   将 **N** 减少**位**。
        *   用 **1** 减少**位**。
    *   如果发现 **N** 的值大于 **0** ，则在 **res** 的起始处推字符。
    *   完成以上步骤后，打印 **res** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find smallest positive
// number made up of non-repeating digits
// whose sum of its digits is equal to n
void result(int n)
{
    if (n > 45) {

        // No such number exists
        cout << -1;
        return;
    }

    // Stores the required answer
    string res;

    // Store the digit at unit's place
    int digit = 9;

    // Iterate until n > digit
    while (n > digit) {

        // Push digit at the start of res
        res = char('0' + digit) + res;

        // Decrement n by digit
        n -= digit;

        // Decrement digit by 1
        digit -= 1;
    }

    if (n > 0) {

        // Push the remaining number
        // as the starting digit
        res = char('0' + n) + res;
    }

    // Print the required number
    cout << res;
}

// Driver Code
int main()
{
    int N = 19;

    // Function Call
    result(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find smallest positive
// number made up of non-repeating digits
// whose sum of its digits is equal to n
static void result(int n)
{
    if (n > 45)
    {

        // No such number exists
        System.out.print(-1);
        return;
    }

    // Stores the required answer
    String res="";

    // Store the digit at unit's place
    int digit = 9;

    // Iterate until n > digit
    while (n > digit)
    {

        // Push digit at the start of res
        res = (char)('0' + digit) + res;

        // Decrement n by digit
        n -= digit;

        // Decrement digit by 1
        digit -= 1;
    }

    if (n > 0)
    {

        // Push the remaining number
        // as the starting digit
        res = (char)('0' + n) + res;
    }

    // Print the required number
    System.out.print(res);
}

// Driver Code
public static void main(String[] args)
{
    int N = 19;

    // Function Call
    result(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find smallest positive
# number made up of non-repeating digits
# whose sum of its digits is equal to n
def result(n):

    if (n > 45):

        # No such number exists
        print(-1, end = "")
        return

    # Stores the required answer
    res = ""

    # Store the digit at unit's place
    digit = 9

    # Iterate until n > digit
    while (n > digit):

        # Push digit at the start of res
        res = str(digit) + res

        # Decrement n by digit
        n -= digit

        # Decrement digit by 1
        digit -= 1

    if (n > 0):

        # Push the remaining number
        # as the starting digit
        res = str(n) + res

    # Print the required number
    print(res)

# Driver Code
if __name__ == '__main__':

    N = 19

    # Function Call
    result(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find smallest positive
// number made up of non-repeating digits
// whose sum of its digits is equal to n
static void result(int n)
{
    if (n > 45)
    {

        // No such number exists
        Console.Write(-1);
        return;
    }

    // Stores the required answer
    string res = "";

    // Store the digit at unit's place
    int digit = 9;

    // Iterate until n > digit
    while (n > digit)
    {

        // Push digit at the start of res
        res = (char)('0' + digit) + res;

        // Decrement n by digit
        n -= digit;

        // Decrement digit by 1
        digit -= 1;
    }

    if (n > 0)
    {

        // Push the remaining number
        // as the starting digit
        res = (char)('0' + n) + res;
    }

    // Print the required number
    Console.Write(res);
}

// Driver Code
public static void Main()
{
    int N = 19;

    // Function Call
    result(N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find smallest positive
// number made up of non-repeating digits
// whose sum of its digits is equal to n
function result(n)
{
    if (n > 45) {

        // No such number exists
        document.write(-1);
    }

    // Stores the required answer
    var res = "";

    // Store the digit at unit's place
    var digit = 9;

    // Iterate until n > digit
    while (n > digit) {

        // Push digit at the start of res
        res = String.fromCharCode(48 + digit) + res;

        // Decrement n by digit
        n -= digit;

        // Decrement digit by 1
        digit -= 1;
    }

    if (n > 0) {

        // Push the remaining number
        // as the starting digit
        res = String.fromCharCode(48 + n) + res;
    }

    // Print the required number
    document.write(res);
}

// Driver Code
var N = 19;

// Function Call
result(N);

</script>
```

**Output:** 

```
289
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)