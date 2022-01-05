# 从最后一个

开始，在交替的索引上按顺序添加自然数，找到下一个数字

> 原文:[https://www . geeksforgeeks . org/通过从最后一个索引开始交替添加自然数来查找下一个数字/](https://www.geeksforgeeks.org/find-the-next-number-by-adding-natural-numbers-in-order-on-alternating-indices-from-last/)

给定一个大小为 **N** 的数字串**S**，任务是找到给定数字串 **S** 的每一个备选数字加上数字 **1** 、 **2** 、 **3** 、… **直到无穷大**所形成的数字。在任何时候，如果加法结果不是一个数字，执行 r [的数字加法，直到结果是一个数字](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)。

**示例:**

> **输入:** S = "1345"
> **输出:** 1546
> **解释:**
> 最后一位加 1，即 5 变成 6，将字符串修改为“1346”。
> 在倒数第二个数字上加 2，即 3 将变成 5，从而将字符串修改为“1546”。
> 经过以上步骤，形成的结果字符串为“1546”。
> 
> **输入:**S = " 789 "
> T3】输出: 981

**方法:**解决这个问题的思路在于重复加法的部分。实际上没有必要重复执行加法，直到有一个数字。相反，执行**数字% 9** 。如果**数字% 9** 等于 **9** ，那么 [**位数之和**](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/) 等于 9，否则位数之和等于**数字% 9** 。按照以下步骤解决问题:

*   将变量 **temp** 和**add _ number**初始化为 **0** ，以存储要更改的位置和要添加的编号。
*   [将字符串变量**结果**初始化为空字符串](https://www.geeksforgeeks.org/strings-in-c-and-how-to-create-them/)来存储结果。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【len-1，0】**，其中 **len** 是字符串的长度，并执行以下步骤:
    *   将变量**数字**初始化为字符串中当前位置的数字。
    *   如果**温度%2** 等于 **0** ，那么将**相加 _ 编号**的值增加 **1** ，并将其加到变量**数字上。**
    *   如果**数字**大于等于 **10** ，则将**数字**的值设置为**数字%9** ，如果仍然如此，**数字**等于 **0** ，则将其值设置为 9。
    *   将变量**数字**加到变量**结果**的开头。
*   执行上述步骤后，打印**结果**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate the resultant
// number using the given criteria
string generateNumber(string number)
{
    int temp = 0, adding_number = 0;

    // Storing end result
    string result = "";

    // Find the length of numeric string
    int len = number.size();

    // Traverse the string
    for (int i = len - 1; i >= 0; i--) {

        // Storing digit at ith position
        int digit = number[i] - '0';

        // Checking that the number would
        // be added or not
        if (temp % 2 == 0) {

            adding_number += 1;
            digit += adding_number;

            // Logic for summing the digits
            // if the digit is greater than 10
            if (digit >= 10) {
                digit %= 9;
                if (digit == 0)
                    digit = 9;
            }
        }

        // Storing the result
        result = to_string(digit) + result;
        temp += 1;
    }

    // Returning the result
    return result;
}

// Driver Code
int main()
{
    string S = "1345";
    cout << generateNumber(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to generate the resultant
    // number using the given criteria
    public static String generateNumber(String number) {
        int temp = 0, adding_number = 0;

        // Storing end result
        String result = "";

        // Find the length of numeric string
        int len = number.length();

        // Traverse the string
        for (int i = len - 1; i >= 0; i--) {

            // Storing digit at ith position
            int digit = (int) number.charAt(i) - (int) '0';

            // Checking that the number would
            // be added or not
            if (temp % 2 == 0) {

                adding_number += 1;
                digit += adding_number;

                // Logic for summing the digits
                // if the digit is greater than 10
                if (digit >= 10) {
                    digit %= 9;
                    if (digit == 0)
                        digit = 9;
                }
            }

            // Storing the result
            result = digit + result;
            temp += 1;
        }

        // Returning the result
        return result;
    }

    // Driver Code
    public static void main(String args[]) {
        String S = "1345";
        System.out.println(generateNumber(S));
    }

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to generate the resultant
# number using the given criteria
def generateNumber(number) :

    temp = 0; adding_number = 0;

    # Storing end result
    result = "";

    # Find the length of numeric string
    l = len(number);

    # Traverse the string
    for i in range(l - 1, -1, -1) :

        # Storing digit at ith position
        digit = ord(number[i]) - ord('0');

        # Checking that the number would
        # be added or not
        if (temp % 2 == 0) :

            adding_number += 1;
            digit += adding_number;

            # Logic for summing the digits
            # if the digit is greater than 10
            if (digit >= 10) :
                digit %= 9;
                if (digit == 0) :
                    digit = 9;

        # Storing the result
        result = str(digit) + result;
        temp += 1;

    # Returning the result
    return result;

# Driver Code
if __name__ ==  "__main__" :

    S = "1345";
    print(generateNumber(S));

    # This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to generate the resultant
        // number using the given criteria
        function generateNumber(number) {
            let temp = 0, adding_number = 0;

            // Storing end result
            let result = "";

            // Find the length of numeric string
            let len = number.length;

            // Traverse the string
            for (let i = len - 1; i >= 0; i--) {

                // Storing digit at ith position
                let digit = parseInt(number[i]);

                // Checking that the number would
                // be added or not
                if (temp % 2 == 0) {

                    adding_number += 1;
                    digit += adding_number;

                    // Logic for summing the digits
                    // if the digit is greater than 10
                    if (digit >= 10) {
                        digit %= 9;
                        if (digit == 0)
                            digit = 9;
                    }
                }

                // Storing the result
                result = (digit).toString() + result;
                temp += 1;
            }

            // Returning the result
            return result;
        }

        // Driver Code

        let S = "1345";
        document.write(generateNumber(S));

// This code is contributed by Potta Lokesh
    </script>
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to generate the resultant
    // number using the given criteria
    public static String generateNumber(string number) {
        int temp = 0, adding_number = 0;

        // Storing end result
        string result = "";

        // Find the length of numeric string
        int len = number.Length;

        // Traverse the string
        for (int i = len - 1; i >= 0; i--) {

            // Storing digit at ith position
            int digit = (int)number[i] - (int)'0';

            // Checking that the number would
            // be added or not
            if (temp % 2 == 0) {

                adding_number += 1;
                digit += adding_number;

                // Logic for summing the digits
                // if the digit is greater than 10
                if (digit >= 10) {
                    digit %= 9;
                    if (digit == 0)
                        digit = 9;
                }
            }

            // Storing the result
            result = digit + result;
            temp += 1;
        }

        // Returning the result
        return result;
    }

    // Driver Code
    public static void Main(string []args) {
        string S = "1345";
        Console.WriteLine(generateNumber(S));
    }

}

// This code is contributed by AnkThon
```

**Output:** 

```
1546
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)