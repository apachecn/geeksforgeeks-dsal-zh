# 计数没有连续 1 的二进制字符串数:设置 2

> 原文:[https://www . geeksforgeeks . org/count-无连续 1 的二进制字符串数-set-2/](https://www.geeksforgeeks.org/count-number-of-binary-strings-without-consecutive-1s-set-2/)

给定一个正整数 **N** ，任务是计算长度为 N 的所有可能的不同的[二进制字符串，使得没有连续的 1](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)

**示例:**

> **输入:** N = 5
> **输出:** 5
> **说明:**
> 非负整数< = 5 及其对应的二进制表示为:
> 0:0
> 1:1
> 2:10
> 3:11
> 4:100
> 5:101
> 其中，只有 3 有两个连续的 1，因此所需计数= 5
> 
> **输入:**N = 12
> T3】输出: 8

[**动态规划方法:**](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/) A [动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法已经在[这篇文章](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/)中讨论过了。

**方法:**本文讨论了一种使用[数字-dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 概念的方法。

*   类似于数字 dp 问题，这里创建了一个**三维表格**来存储计算值。假设 N<2<sup>31</sup>–1，每个数字的范围只有 2(0 或 1)。因此，表的尺寸取为**32×2×2**。
*   构建表后，[给定的数字被转换成二进制字符串](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)。
*   然后，迭代该数字。对于每次迭代:
    1.  检查前一个数字是 0 还是 1。
    2.  如果是 0，那么现在的数字可以是 0 或 1。
    3.  但是如果前一个数是 1，那么现在的数必须是 0，因为在二进制表示中我们不能有两个连续的 1。
*   现在，表格完全按照[数字 dp 问题](https://www.geeksforgeeks.org/digit-dp-introduction/)填写。

下面是上述方法的实现

## C++

```
// C++ program to count number of
// binary strings without consecutive 1’s

#include <bits/stdc++.h>
using namespace std;

// Table to store the solution of
// every sub problem
int memo[32][2][2];

// Function to fill the table
/* Here,
   pos: keeps track of current position.
   f1: is the flag to check if current
         number is less than N or not.
   pr: represents the previous digit
*/
int dp(int pos, int fl, int pr, string& bin)
{
    // Base case
    if (pos == bin.length())
        return 1;

    // Check if this subproblem
    // has already been solved
    if (memo[pos][fl][pr] != -1)
        return memo[pos][fl][pr];

    int val = 0;

    // Placing 0 at the current position
    // as it does not violate the condition
    if (bin[pos] == '0')
        val = val + dp(pos + 1, fl, 0, bin);

    // Here flag will be 1 for the
    // next recursive call
    else if (bin[pos] == '1')
        val = val + dp(pos + 1, 1, 0, bin);

    // Placing 1 at this position only if
    // the previously inserted number is 0
    if (pr == 0) {

        // If the number is smaller than N
        if (fl == 1) {
            val += dp(pos + 1, fl, 1, bin);
        }

        // If the digit at current position is 1
        else if (bin[pos] == '1') {
            val += dp(pos + 1, fl, 1, bin);
        }
    }

    // Storing the solution to this subproblem
    return memo[pos][fl][pr] = val;
}

// Function to find the number of integers
// less than or equal to N with no
// consecutive 1’s in binary representation
int findIntegers(int num)
{
    // Convert N to binary form
    string bin;

    // Loop to convert N
    // from Decimal to binary
    while (num > 0) {
        if (num % 2)
            bin += "1";
        else
            bin += "0";
        num /= 2;
    }
    reverse(bin.begin(), bin.end());

    // Initialising the table with -1.
    memset(memo, -1, sizeof(memo));

    // Calling the function
    return dp(0, 0, 0, bin);
}

// Driver code
int main()
{
    int N = 12;
    cout << findIntegers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// binary Strings without consecutive 1’s
class GFG{

// Table to store the solution of
// every sub problem
static int [][][]memo = new int[32][2][2];

// Function to fill the table
/* Here,
   pos: keeps track of current position.
   f1: is the flag to check if current
         number is less than N or not.
   pr: represents the previous digit
*/
static int dp(int pos, int fl, int pr, String bin)
{
    // Base case
    if (pos == bin.length())
        return 1;

    // Check if this subproblem
    // has already been solved
    if (memo[pos][fl][pr] != -1)
        return memo[pos][fl][pr];

    int val = 0;

    // Placing 0 at the current position
    // as it does not violate the condition
    if (bin.charAt(pos) == '0')
        val = val + dp(pos + 1, fl, 0, bin);

    // Here flag will be 1 for the
    // next recursive call
    else if (bin.charAt(pos) == '1')
        val = val + dp(pos + 1, 1, 0, bin);

    // Placing 1 at this position only if
    // the previously inserted number is 0
    if (pr == 0) {

        // If the number is smaller than N
        if (fl == 1) {
            val += dp(pos + 1, fl, 1, bin);
        }

        // If the digit at current position is 1
        else if (bin.charAt(pos) == '1') {
            val += dp(pos + 1, fl, 1, bin);
        }
    }

    // Storing the solution to this subproblem
    return memo[pos][fl][pr] = val;
}

// Function to find the number of integers
// less than or equal to N with no
// consecutive 1’s in binary representation
static int findIntegers(int num)
{
    // Convert N to binary form
    String bin = "";

    // Loop to convert N
    // from Decimal to binary
    while (num > 0) {
        if (num % 2 == 1)
            bin += "1";
        else
            bin += "0";
        num /= 2;
    }
    bin = reverse(bin);

    // Initialising the table with -1.
    for(int i = 0; i < 32; i++){
        for(int j = 0; j < 2; j++){
            for(int l = 0; l < 2; l++)
                memo[i][j][l] = -1;
        }
    }

    // Calling the function
    return dp(0, 0, 0, bin);
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver code
public static void main(String[] args)
{
    int N = 12;
    System.out.print(findIntegers(N));

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python program to count number of
# binary strings without consecutive 1’s

# Table to store the solution of
# every sub problem
memo=[[[-1 for i in range(2)] for j in range(2)] for k in range(32)]

# Function to fill the table
''' Here,
pos: keeps track of current position.
f1: is the flag to check if current
        number is less than N or not.
pr: represents the previous digit
'''
def dp(pos,fl,pr,bin):
    # Base case
    if (pos == len(bin)):
        return 1;

    # Check if this subproblem
    # has already been solved
    if (memo[pos][fl][pr] != -1):
        return memo[pos][fl][pr];

    val = 0

    # Placing 0 at the current position
    # as it does not violate the condition
    if (bin[pos] == '0'):
        val = val + dp(pos + 1, fl, 0, bin)

    # Here flag will be 1 for the
    # next recursive call
    elif (bin[pos] == '1'):
        val = val + dp(pos + 1, 1, 0, bin)

    # Placing 1 at this position only if
    # the previously inserted number is 0
    if (pr == 0):

        # If the number is smaller than N
        if (fl == 1):
            val += dp(pos + 1, fl, 1, bin)

        # If the digit at current position is 1
        elif (bin[pos] == '1'):
            val += dp(pos + 1, fl, 1, bin)

    # Storing the solution to this subproblem
    memo[pos][fl][pr] = val
    return val

# Function to find the number of integers
# less than or equal to N with no
# consecutive 1’s in binary representation
def findIntegers(num):
    # Convert N to binary form
    bin=""

    # Loop to convert N
    # from Decimal to binary
    while (num > 0):
        if (num % 2):
            bin += "1"
        else:
            bin += "0"
        num //= 2

    bin=bin[::-1];

    # Calling the function
    return dp(0, 0, 0, bin)

# Driver code
if __name__ == "__main__":

    N = 12
    print(findIntegers(N))
```

## C#

```
// C# program to count number of
// binary Strings without consecutive 1’s
using System;

public class GFG{

// Table to store the solution of
// every sub problem
static int [,,]memo = new int[32,2,2];

// Function to fill the table
/* Here,
   pos: keeps track of current position.
   f1: is the flag to check if current
         number is less than N or not.
   pr: represents the previous digit
*/
static int dp(int pos, int fl, int pr, String bin)
{
    // Base case
    if (pos == bin.Length)
        return 1;

    // Check if this subproblem
    // has already been solved
    if (memo[pos,fl,pr] != -1)
        return memo[pos,fl,pr];

    int val = 0;

    // Placing 0 at the current position
    // as it does not violate the condition
    if (bin[pos] == '0')
        val = val + dp(pos + 1, fl, 0, bin);

    // Here flag will be 1 for the
    // next recursive call
    else if (bin[pos] == '1')
        val = val + dp(pos + 1, 1, 0, bin);

    // Placing 1 at this position only if
    // the previously inserted number is 0
    if (pr == 0) {

        // If the number is smaller than N
        if (fl == 1) {
            val += dp(pos + 1, fl, 1, bin);
        }

        // If the digit at current position is 1
        else if (bin[pos] == '1') {
            val += dp(pos + 1, fl, 1, bin);
        }
    }

    // Storing the solution to this subproblem
    return memo[pos,fl,pr] = val;
}

// Function to find the number of integers
// less than or equal to N with no
// consecutive 1’s in binary representation
static int findints(int num)
{
    // Convert N to binary form
    String bin = "";

    // Loop to convert N
    // from Decimal to binary
    while (num > 0) {
        if (num % 2 == 1)
            bin += "1";
        else
            bin += "0";
        num /= 2;
    }
    bin = reverse(bin);

    // Initialising the table with -1.
    for(int i = 0; i < 32; i++){
        for(int j = 0; j < 2; j++){
            for(int l = 0; l < 2; l++)
                memo[i,j,l] = -1;
        }
    }

    // Calling the function
    return dp(0, 0, 0, bin);
}
static String reverse(String input) {
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver code
public static void Main(String[] args)
{
    int N = 12;
    Console.Write(findints(N));

}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to count number of
// binary strings without consecutive 1’s

// Table to store the solution of
// every sub problem
var memo = Array.from(Array(32), ()=>Array(2));

for(var i =0;i<32;i++)
{
    for(var j =0; j<2; j++)
    {
        memo[i][j] = new Array(2).fill(-1);
    }
}

// Function to fill the table
/* Here,
   pos: keeps track of current position.
   f1: is the flag to check if current
         number is less than N or not.
   pr: represents the previous digit
*/
function dp(pos, fl, pr, bin)
{
    // Base case
    if (pos == bin.length)
        return 1;

    // Check if this subproblem
    // has already been solved
    if (memo[pos][fl][pr] != -1)
        return memo[pos][fl][pr];

    var val = 0;

    // Placing 0 at the current position
    // as it does not violate the condition
    if (bin[pos] == '0')
        val = val + dp(pos + 1, fl, 0, bin);

    // Here flag will be 1 for the
    // next recursive call
    else if (bin[pos] == '1')
        val = val + dp(pos + 1, 1, 0, bin);

    // Placing 1 at this position only if
    // the previously inserted number is 0
    if (pr == 0) {

        // If the number is smaller than N
        if (fl == 1) {
            val += dp(pos + 1, fl, 1, bin);
        }

        // If the digit at current position is 1
        else if (bin[pos] == '1') {
            val += dp(pos + 1, fl, 1, bin);
        }
    }

    // Storing the solution to this subproblem
    return memo[pos][fl][pr] = val;
}

// Function to find the number of integers
// less than or equal to N with no
// consecutive 1’s in binary representation
function findIntegers(num)
{
    // Convert N to binary form
    var bin = "";

    // Loop to convert N
    // from Decimal to binary
    while (num > 0) {
        if (num % 2)
            bin += "1";
        else
            bin += "0";
        num =parseInt(num/2);
    }

    bin = bin.split('').reverse().join('')

    // Calling the function
    return dp(0, 0, 0, bin);
}

// Driver code
var N = 12;
document.write( findIntegers(N));

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(L * log(N))

*   O(log(N))将数字从十进制转换为二进制。
*   O(L)填充表格，其中 L 是二进制形式的长度。

**辅助空间:** O(32 * 2 * 2)