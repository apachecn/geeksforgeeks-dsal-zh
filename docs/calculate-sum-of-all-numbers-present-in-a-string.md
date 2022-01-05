# 计算字符串中所有数字的总和

> 原文:[https://www . geesforgeks . org/calculate-sum-all-numbers-in-present-in-string/](https://www.geeksforgeeks.org/calculate-sum-of-all-numbers-present-in-a-string/)

给定包含字母数字字符的字符串，计算该字符串中所有数字的总和。

**示例:**

```
Input:  1abc23
Output: 24

Input:  geeks4geeks
Output: 4

Input:  1abc2x30yz67
Output: 100

Input:  123abc
Output: 123
```

**难度等级:**菜鸟

这个问题中唯一棘手的部分是多个连续的数字被认为是一个数字。
想法很简单。我们扫描输入字符串的每个字符，如果一个数字是由字符串的连续字符组成的，我们将结果增加这个数量。

下面是上述想法的实现:

## C++

```
// C++ program to calculate sum of all numbers present
// in a string containing alphanumeric characters
#include <iostream>
using namespace std;

// Function to calculate sum of all numbers present
// in a string containing alphanumeric characters
int findSum(string str)
{
    // A temporary string
    string temp = "";

    // holds sum of all numbers present in the string
    int sum = 0;

    // read each character in input string
    for (char ch : str) {
        // if current character is a digit
        if (isdigit(ch))
            temp += ch;

        // if current character is an alphabet
        else {
            // increment sum by number found earlier
            // (if any)
            sum += atoi(temp.c_str());

            // reset temporary string to empty
            temp = "";
        }
    }

    // atoi(temp.c_str()) takes care of trailing
    // numbers
    return sum + atoi(temp.c_str());
}

// Driver code
int main()
{
    // input alphanumeric string
    string str = "12abc20yz68";

    // Function call
    cout << findSum(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate sum of all numbers present
// in a string containing alphanumeric characters
class GFG {

    // Function to calculate sum of all numbers present
    // in a string containing alphanumeric characters
    static int findSum(String str)
    {
        // A temporary string
        String temp = "0";

        // holds sum of all numbers present in the string
        int sum = 0;

        // read each character in input string
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);

            // if current character is a digit
            if (Character.isDigit(ch))
                temp += ch;

            // if current character is an alphabet
            else {
                // increment sum by number found earlier
                // (if any)
                sum += Integer.parseInt(temp);

                // reset temporary string to empty
                temp = "0";
            }
        }

        // atoi(temp.c_str()) takes care of trailing
        // numbers
        return sum + Integer.parseInt(temp);
    }

    // Driver code
    public static void main(String[] args)
    {

        // input alphanumeric string
        String str = "12abc20yz68";

        // Function call
        System.out.println(findSum(str));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to calculate sum of
# all numbers present in a str1ing
# containing alphanumeric characters

# Function to calculate sum of all
# numbers present in a str1ing
# containing alphanumeric characters

def findSum(str1):

    # A temporary str1ing
    temp = "0"

    # holds sum of all numbers
    # present in the str1ing
    Sum = 0

    # read each character in input string
    for ch in str1:

        # if current character is a digit
        if (ch.isdigit()):
            temp += ch

        # if current character is an alphabet
        else:

            # increment Sum by number found
            # earlier(if any)
            Sum += int(temp)

            # reset temporary str1ing to empty
            temp = "0"

    # atoi(temp.c_str1()) takes care
    # of trailing numbers
    return Sum + int(temp)

# Driver code

# input alphanumeric str1ing
str1 = "12abc20yz68"

# Function call
print(findSum(str1))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to calculate sum of
// all numbers present in a string
// containing alphanumeric characters
using System;

class GFG {

    // Function to calculate sum of
    // all numbers present in a string
    // containing alphanumeric characters
    static int findSum(String str)
    {
        // A temporary string
        String temp = "0";

        // holds sum of all numbers
        // present in the string
        int sum = 0;

        // read each character in input string
        for (int i = 0; i < str.Length; i++) {
            char ch = str[i];

            // if current character is a digit
            if (char.IsDigit(ch))
                temp += ch;

            // if current character is an alphabet
            else {

                // increment sum by number found earlier
                // (if any)
                sum += int.Parse(temp);

                // reset temporary string to empty
                temp = "0";
            }
        }

        // atoi(temp.c_str()) takes care of trailing
        // numbers
        return sum + int.Parse(temp);
    }

    // Driver code
    public static void Main(String[] args)
    {

        // input alphanumeric string
        String str = "12abc20yz68";

        // Function call
        Console.WriteLine(findSum(str));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to calculate
// sum of all numbers present
// in a string containing
// alphanumeric characters

    // Function to calculate sum
    // of all numbers present
    // in a string containing
    // alphanumeric characters
    function findSum(str)
    {
        // A temporary string
        let temp = "0";

        // holds sum of all numbers
        // present in the string
        let sum = 0;

        // read each character in input string
        for (let i = 0; i < str.length; i++) {
            let ch = str[i];

            // if current character is a digit
            if (!isNaN(String(ch) * 1))
                temp += ch;

            // if current character is an alphabet
            else {
                // increment sum by number found earlier
                // (if any)
                sum += parseInt(temp);

                // reset temporary string to empty
                temp = "0";
            }
        }

        // atoi(temp.c_str()) takes care of trailing
        // numbers
        return sum + parseInt(temp);
    }

    // Driver code
    // input alphanumeric string
    let str = "12abc20yz68";

    // Function call
    document.write(findSum(str));

// This code is contributed by unknown2108

</script>
```

**Output**

```
100
```

**时间复杂度:** O(n)，其中 n 为字符串长度。

实现 Regex 的更好的解决方案。

## 蟒蛇 3

```
# Python3 program to calculate sum of
# all numbers present in a str1ing
# containing alphanumeric characters

# Function to calculate sum of all
# numbers present in a str1ing
# containing alphanumeric characters
import re

def find_sum(str1):
    # Regular Expression that matches
    # digits in between a string
    return sum(map(int, re.findall('\d+', str1)))

# Driver code
# input alphanumeric str1ing
str1 = "12abc20yz68"

# Function call
print(find_sum(str1))

# This code is contributed
# by Venkata Ramana B
```

**Output**

```
100
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。