# 将输入整数

中的所有“0”替换为“5”

> 原文:[https://www.geeksforgeeks.org/replace-0-5-input-integer/](https://www.geeksforgeeks.org/replace-0-5-input-integer/)

给定一个整数作为输入，并将整数中的所有“0”替换为“5”。

**示例:**

```
Input: 102 
Output: 152
Explanation: All the digits which are '0' is replaced by '5' 

Input: 1020 
Output: 1525
Explanation: All the digits which are '0' is replaced by '5'
```

不允许使用数组存储所有数字。

**<u>迭代方法-1</u>** :通过观察测试用例，很明显所有的 0 位数字都被 5 代替了。例如，对于输入= 1020，输出= 1525。思路很简单，我们给变量‘temp’赋值为 0，我们用 mod 运算符“%”得到最后一位数字。如果数字是 0，我们就用 5 代替，否则就保持原样。然后我们将“temp”乘以 10，再加上 mod 运算得到的数字。之后，我们将原始数字除以 10，得到其他数字。这样，我们将有一个数字，其中所有的“0”都被分配了“5”。如果我们反转这个数字，我们将得到期望的答案。

**<u>算法</u>** :

1.  如果数字为 0，直接返回 5。
2.  否则，执行以下步骤。
3.  创建一个变量 temp= 0 来存储将所有“0”赋给“5”的反转数字。
4.  使用 mod 运算符“%”查找最后一位数字。如果数字是“0”，那么将最后一个数字设为“5”。
5.  将 temp 乘以 10，然后加上最后一位数字。
6.  将数字除以 10，通过模运算得到更多的数字。
7.  然后用下面的方法反转这个数字。
8.  [https://www . geesforgeks . org/write-a-program-to-reverse-digits-of-a-number/](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)
9.  返回反转的数字。

## C++

```
// C++ program to replace all ‘0’
// with ‘5’ in an input Integer
#include <iostream>
using namespace std;

// A iterative function to reverse a number
int reverseTheNumber(int temp)
{
    int ans = 0;
    while (temp > 0) {
        int rem = temp % 10;
        ans = ans * 10 + rem;
        temp = temp / 10;
    }
    return ans;
}

int convert0To5(int num)
{
    // if num is 0 return 5
    if (num == 0)
        return 5;

    // Extract the last digit and
    // change it if needed
    else {
        int temp = 0;

        while (num > 0) {
            int digit = num % 10;
            //if digit is 0, make it 5
            if (digit == 0)
                digit = 5;

            temp = temp * 10 + digit;
            num = num / 10;
        }
        // call the function reverseTheNumber by passing
        // temp
        return reverseTheNumber(temp);
    }
}

// Driver code
int main()
{
    int num = 10120;
    cout << convert0To5(num);
    return 0;
}

// This code is contributed by Vrashank Rao M.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// A iterative function to reverse a number
static int reverseTheNumber(int temp)
{
    int ans = 0;
    while (temp > 0) {
        int rem = temp % 10;
        ans = ans * 10 + rem;
        temp = temp / 10;
    }
    return ans;
}

static int convert0To5(int num)
{
    // if num is 0 return 5
    if (num == 0)
        return 5;

    // Extract the last digit and
    // change it if needed
    else {
        int temp = 0;

        while (num > 0) {
            int digit = num % 10;

            //if digit is 0, make it 5
            if (digit == 0)
                digit = 5;

            temp = temp * 10 + digit;
            num = num / 10;
        }

        // call the function reverseTheNumber by passing
        // temp
        return reverseTheNumber(temp);
    }
}

    // Driver prorgram
    public static void main(String args[])
    {
        int num = 10120;
        System.out.println(convert0To5(num));
    }
}

// This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

// A iterative function to reverse a number
static int reverseTheNumber(int temp)
{
    int ans = 0;
    while (temp > 0) {
        int rem = temp % 10;
        ans = ans * 10 + rem;
        temp = temp / 10;
    }
    return ans;
}

static int convert0To5(int num)
{
    // if num is 0 return 5
    if (num == 0)
        return 5;

    // Extract the last digit and
    // change it if needed
    else {
        int temp = 0;

        while (num > 0) {
            int digit = num % 10;
            //if digit is 0, make it 5
            if (digit == 0)
                digit = 5;

            temp = temp * 10 + digit;
            num = num / 10;
        }

        // call the function reverseTheNumber by passing
        // temp
        return reverseTheNumber(temp);
    }
}

    // Driver Code
    public static void Main (string[] args) {
        int num = 10120;
        Console.Write(convert0To5(num));

    }
}

// This code is contributed by splevel62.
```

**Output**

```
15125
```

**复杂度分析**:

*   **时间复杂度** : O(2n)，其中 n 是数字中的位数，用 O(n)做数字中的 0s int 5s，再加一个 O(n)反转数字
*   **空间复杂度** : O(1)，不需要额外空间。

**<u>迭代方法-2:</u>** 通过观察测试用例，很明显所有的 0 数字都被 5 代替了。例如，对于输入= 1020，输出= 1525，可以写成 1020 + 505，还可以写成 1020 + 5*(10^2) + 5*(10^0).所以解可以以迭代的方式形成，如果遇到一个‘0’数字，找到那个数字的位置值，与 5 相乘，找到数字中所有 0 的和。将该总和与输入数相加，得到输出数。

**算法:**

1.  创建变量 *sum = 0* 存储总和， *place = 1* 存储当前数字的位置值，并创建输入变量的副本
2.  如果数字为零，返回 5
3.  当输入变量大于 0 时，重复下一步
4.  提取最后一位数字 *(n%10)* ，如果该数字为零，则更新 *sum = sum + place*5* ，从数字 *n = n/10* 中删除最后一位数字，并更新 *place = place * 10*
5.  返回总和。

## C++

```
#include<bits/stdc++.h>
using namespace std;

// Returns the number to be added to the
// input to replace all zeroes with five
int calculateAddedValue(int number)
{

    // Amount to be added
    int result = 0;

    // Unit decimal place
    int decimalPlace = 1;

    if (number == 0)
    {
        result += (5 * decimalPlace);
    }

    while (number > 0)
    {
        if (number % 10 == 0)
        {

            // A number divisible by 10, then
            // this is a zero occurrence in
            // the input
            result += (5 * decimalPlace);

        }

        // Move one decimal place
        number /= 10;
        decimalPlace *= 10;
    }
    return result;
}

int replace0with5(int number)
{
    return number += calculateAddedValue(number);
}

// Driver code
int main()
{
    cout << replace0with5(1020);
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class ReplaceDigits {
    static int replace0with5(int number)
    {
        return number += calculateAddedValue(number);
    }

    // returns the number to be added to the
    // input to replace all zeroes with five
    private static int calculateAddedValue(int number)
    {

        // amount to be added
        int result = 0;

        // unit decimal place
        int decimalPlace = 1;

        if (number == 0) {
            result += (5 * decimalPlace);
        }

        while (number > 0) {
            if (number % 10 == 0)
                // a number divisible by 10, then
                // this is a zero occurrence in the input
                result += (5 * decimalPlace);

            // move one decimal place
            number /= 10;
            decimalPlace *= 10;
        }
        return result;
    }

    public static void main(String[] args)
    {
        System.out.print(replace0with5(1020));
    }
}
```

## 蟒蛇 3

```
def replace0with5(number):
    number += calculateAddedValue(number)
    return number

# returns the number to be added to the
# input to replace all zeroes with five
def calculateAddedValue(number):

    # amount to be added
    result = 0

    # unit decimal place
    decimalPlace = 1

    if (number == 0):
        result += (5 * decimalPlace)

    while (number > 0):
        if (number % 10 == 0):

            # a number divisible by 10, then
            # this is a zero occurrence in the input
            result += (5 * decimalPlace)

        # move one decimal place
        number //= 10
        decimalPlace *= 10

    return result

# Driver code
print(replace0with5(1020))

# This code is contributed by shubhmasingh10
```

## C#

```
using System;

class GFG{

static int replace0with5(int number)
{
    return number += calculateAddedValue(number);
}

// Returns the number to be added to the
// input to replace all zeroes with five
static int calculateAddedValue(int number)
{

    // Amount to be added
    int result = 0;

    // Unit decimal place
    int decimalPlace = 1;

    if (number == 0)
    {
        result += (5 * decimalPlace);
    }

    while (number > 0)
    {
        if (number % 10 == 0)

            // A number divisible by 10, then
            // this is a zero occurrence in the input
            result += (5 * decimalPlace);

        // Move one decimal place
        number /= 10;
        decimalPlace *= 10;
    }
    return result;
}

// Driver Code
static public void Main()
{
    Console.WriteLine(replace0with5(1020));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Returns the number to be added to the
// input to replace all zeroes with five
function calculateAddedValue(number){
    // Amount to be added
    let result = 0;
    // Unit decimal place
    let decimalPlace = 1;

    if (number == 0) {
        result += (5 * decimalPlace);
    }

    while (number > 0){
        if (number % 10 == 0){
            // A number divisible by 10, then
            // this is a zero occurrence in
            // the input
            result += (5 * decimalPlace);
        }
        // Move one decimal place
        number = Math.floor(number/10);
        decimalPlace *= 10;
    }
    return result;
}

function replace0with5(number){
    return number += calculateAddedValue(number);
}

// Driver code
document.write(replace0with5(1020));

</script>
```

**输出:**

```
1525
```

**复杂度分析:**

*   **时间复杂度:** O(k)，循环只运行 k 次，其中 k 是数字的位数。
*   **空间复杂度:** O(1)，不需要额外空间。

**<u>递归方法:</u>** 思路很简单，我们用 mod 运算符“%”得到最后一位数字。如果数字是 0，我们就用 5 代替，否则就保持原样。然后我们重复剩下的数字。方法保持不变，基本区别是循环被递归函数代替。

**算法:**

1.  当数字为 0 时检查基本情况返回 5，对于所有其他情况形成递归函数。
2.  函数(*求解(int n)* )可以定义如下，如果传递的数字为 0，则返回 0，否则提取最后一位数字，即 *n = n/10* 并删除最后一位数字。如果最后一位是零，就给它赋值 5。
3.  现在通过调用 n 的递归函数返回值，即*返回 solve(n)*10 +数字*。
4.  打印答案。

## C++

```
// C++ program to replace all ‘0’
// with ‘5’ in an input Integer
#include <bits/stdc++.h>
using namespace std;

// A recursive function to replace all 0s
// with 5s in an input number It doesn't
// work if input number itself is 0.
int convert0To5Rec(int num)
{
    // Base case for recursion termination
    if (num == 0)
        return 0;

    // Extraxt the last digit and
    // change it if needed
    int digit = num % 10;
    if (digit == 0)
        digit = 5;

    // Convert remaining digits and
    // append the last digit
    return convert0To5Rec(num / 10) * 10 + digit;
}

// It handles 0 and calls convert0To5Rec()
// for other numbers
int convert0To5(int num)
{
    if (num == 0)
        return 5;
    else
        return convert0To5Rec(num);
}

// Driver code
int main()
{
    int num = 10120;
    cout << convert0To5(num);
    return 0;
}

// This code is contributed by Code_Mech.
```

## C

```
// C program to replace all ‘0’
// with ‘5’ in an input Integer
#include <stdio.h>

// A recursive function to replace
// all 0s with 5s in an input number
// It doesn't work if input number itself is 0.
int convert0To5Rec(int num)
{
    // Base case for recursion termination
    if (num == 0)
        return 0;

    // Extract the last digit and change it if needed
    int digit = num % 10;
    if (digit == 0)
        digit = 5;

    // Convert remaining digits
    // and append the last digit
    return convert0To5Rec(num / 10) * 10 + digit;
}

// It handles 0 and calls
// convert0To5Rec() for other numbers
int convert0To5(int num)
{
    if (num == 0)
        return 5;
    else
        return convert0To5Rec(num);
}

// Driver program to test above function
int main()
{
    int num = 10120;
    printf("%d", convert0To5(num));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Replace all 0 with
// 5 in an input Integer
class GFG {

    // A recursive function to replace all 0s with 5s in
    // an input number. It doesn't work if input number
    // itself is 0.
    static int convert0To5Rec(int num)
    {
        // Base case
        if (num == 0)
            return 0;

        // Extraxt the last digit and change it if needed
        int digit = num % 10;
        if (digit == 0)
            digit = 5;

        // Convert remaining digits and append the
        // last digit
        return convert0To5Rec(num / 10) * 10 + digit;
    }

    // It handles 0 and calls convert0To5Rec() for
    // other numbers
    static int convert0To5(int num)
    {
        if (num == 0)
            return 5;
        else
            return convert0To5Rec(num);
    }

    // Driver function
    public static void main(String[] args)
    {
        System.out.println(convert0To5(10120));
    }
}

// This code is contributed by Kamal Rawal
```

## 计算机编程语言

```
# Python program to replace all
# 0 with 5 in given integer

# A recursive function to replace all 0s
# with 5s in an integer
# Does'nt work if the given number is 0 itself
def convert0to5rec(num):

    # Base case for recurssion termination
    if num == 0:
        return 0

    # Extract the last digit and change it if needed
    digit = num % 10

    if digit == 0:
        digit = 5

    # Convert remaining digits and append the last digit
    return convert0to5rec(num / 10) * 10 + digit

# It handles 0 to 5 calls convert0to5rec()
# for other numbers
def convert0to5(num):
    if num == 0:
        return 5
    else:
        return convert0to5rec(num)

# Driver Program
num = 10120
print convert0to5(num)

# Contributed by Harshit Agrawal
```

## C#

```
// C# code for Replace all 0
// with 5 in an input Integer
using System;

class GFG {

    // A recursive function to replace
    // all 0s with 5s in an input number.
    // It doesn't work if input number
    // itself is 0.
    static int convert0To5Rec(int num)
    {
        // Base case
        if (num == 0)
            return 0;

        // Extraxt the last digit and
        // change it if needed
        int digit = num % 10;
        if (digit == 0)
            digit = 5;

        // Convert remaining digits
        // and append the last digit
        return convert0To5Rec(num / 10) * 10 + digit;
    }

    // It handles 0 and calls
    // convert0To5Rec() for other numbers
    static int convert0To5(int num)
    {
        if (num == 0)
            return 5;
        else
            return convert0To5Rec(num);
    }

    // Driver Code
    static public void Main()
    {
        Console.Write(convert0To5(10120));
    }
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace all 0 with 5
// in given integer

// A recursive function to replace all 0s
// with 5s in an integer. Does'nt work if
// the given number is 0 itself
function convert0to5rec($num)
{

    // Base case for recurssion termination
    if ($num == 0)
        return 0;

    // Extract the last digit and
    // change it if needed
    $digit = ($num % 10);

    if ($digit == 0)
        $digit = 5;

    // Convert remaining digits and append
    // the last digit
    return convert0to5rec((int)($num / 10)) *
                                10 + $digit;
}

// It handles 0 to 5 calls convert0to5rec()
// for other numbers
function convert0to5($num)
{
    if ($num == 0)
        return 5;
    else
        return convert0to5rec($num);
}

// Driver Code
$num = 10120;
print(convert0to5($num));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript code for Replace all 0 with
// 5 in an input Integer   
// A recursive function to replace all 0s with 5s in
    // an input number. It doesn't work if input number
    // itself is 0.
    function convert0To5Rec(num) {
        // Base case
        if (num == 0)
            return 0;

        // Extraxt the last digit and change it if needed
        var digit = num % 10;
        if (digit == 0)
            digit = 5;

        // Convert remaining digits and append the
        // last digit
        return convert0To5Rec(parseInt(num / 10)) * 10 + digit;
    }

    // It handles 0 and calls convert0To5Rec() for
    // other numbers
    function convert0To5(num) {
        if (num == 0)
            return 5;
        else
            return convert0To5Rec(num);
    }

    // Driver function

        document.write(convert0To5(10120));

// This code contributed by gauravrajput1
</script>
```

**Output**

```
15125
```

**输出:**

```
15125
```

**复杂度分析:**

*   **时间复杂度:** O(k)，递归函数只调用 k 次，其中 k 是数字的位数
*   **空间复杂度:** O(1)，不需要额外空间。

本文由**赛基兰**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。