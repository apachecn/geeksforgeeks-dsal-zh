# 将数字转换为字符的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-in-number-in-characters/](https://www.geeksforgeeks.org/program-to-convert-number-in-characters/)

给定一个整数 **N** 。任务是将数字转换成字符。

**示例:**

> **输入:**N = 74254
> T3】输出:七四二五四
> 
> **输入:**N = 23
> T3】输出:二三

**一种有效的方法:**

1.  反转数字。
2.  从右到左迭代反转的数字。
3.  用**模数**提取最后一位数字，然后用**开关格**得到对应的字。
4.  迭代时将数字除以 10。

## C++

```
// C++ program to convert number in characters
#include<bits/stdc++.h>
using namespace std;
void NumbertoCharacter(int n)
{
    int rev = 0, r = 0;

    // To calculate the reverse of the number
    while (n > 0) {

        // The remainder will give the last digit of the number
        r = n % 10;
        rev = rev * 10 + r;
        n = n / 10;
    }

    while (rev > 0) {
        // Extract the first digit of the reversed number
        r = rev % 10;

        // Match it with switch case
        switch (r) {
        case 1:
            cout << "one ";
            break;
        case 2:
            cout << "two ";
            break;
        case 3:
            cout << "three ";
            break;
        case 4:
            cout << "four ";
            break;
        case 5:
            cout << "five ";
            break;
        case 6:
            cout << "six ";
            break;
        case 7:
            cout << "seven ";
            break;
        case 8:
            cout << "eight ";
            break;
        case 9:
            cout << "nine ";
            break;
        case 0:
            cout << "zero ";
            break;
        default:
            cout << "inValid ";
            break;
        }

        // Divide the number by 10 to get the next number
        rev = rev / 10;
    }
}
// Driver code
#include <iostream>
int main()
{
    int n = 12345;
    NumbertoCharacter(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert number in characters
class GFG{

static void NumbertoCharacter(int n)
{
    int rev = 0, r = 0;

    // To calculate the reverse of the number
    while (n > 0)
    {

        // The remainder will give
        // the last digit of the number
        r = n % 10;
        rev = rev * 10 + r;
        n = n / 10;
    }

    while (rev > 0)
    {

        // Extract the first digit
        // of the reversed number
        r = rev % 10;

        // Match it with switch case
        switch (r)
        {
        case 1:
            System.out.print("one ");
            break;
        case 2:
            System.out.print("two ");
            break;
        case 3:
            System.out.print("three ");
            break;
        case 4:
            System.out.print("four ");
            break;
        case 5:
            System.out.print("five ");
            break;
        case 6:
            System.out.print("six ");
            break;
        case 7:
            System.out.print("seven ");
            break;
        case 8:
            System.out.print("eight ");
            break;
        case 9:
            System.out.print("nine ");
            break;
        case 0:
            System.out.print("zero ");
            break;
        default:
            System.out.print("InValid ");
            break;
        }

        // Divide the number by 10
        // to get the next number
        rev = rev / 10;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 12345;
    NumbertoCharacter(n);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to convert
# number in characters
def NumbertoCharacter(n):
    rev = 0; r = 0;

    # To calculate the
    # reverse of the number
    while (n > 0):

        # The remainder will give
        # the last digit of the number
        r = n % 10;
        rev = rev * 10 + r;
        n = n // 10;   

    while (rev > 0):

        # Extract the first digit
        # of the reversed number
        r = rev % 10;

        # Match it with switch case
        switcher = {
                0 : "zero ",
                1 : "one ",
                2 : "two ",
                3 : "three ",
                4 : "four ",
                5 : "five ",
                6 : "six ",
                7 : "seven ",
                8 : "eight ",
                9 : "nine "
        }
        print( switcher.get(r, "InValid"),
               end = " ") ;       

        # Divide the number by 10
        # to get the next number
        rev = rev // 10;

# Driver code
if __name__ == '__main__':
    n = 12345;
    NumbertoCharacter(n);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to convert number in characters
using System;

class GFG{

static void NumbertoCharacter(int n)
{
    int rev = 0, r = 0;

    // To calculate the reverse
    // of the number
    while (n > 0)
    {

        // The remainder will give
        // the last digit of the number
        r = n % 10;
        rev = rev * 10 + r;
        n = n / 10;
    }

    while (rev > 0)
    {

        // Extract the first digit
        // of the reversed number
        r = rev % 10;

        // Match it with switch case
        switch (r)
        {
            case 1:
                Console.Write("one ");
                break;
            case 2:
                Console.Write("two ");
                break;
            case 3:
                Console.Write("three ");
                break;
            case 4:
                Console.Write("four ");
                break;
            case 5:
                Console.Write("five ");
                break;
            case 6:
                Console.Write("six ");
                break;
            case 7:
                Console.Write("seven ");
                break;
            case 8:
                Console.Write("eight ");
                break;
            case 9:
                Console.Write("nine ");
                break;
            case 0:
                Console.Write("zero ");
                break;
            default:
                Console.Write("inValid ");
                break;
        }

        // Divide the number by 10
        // to get the next number
        rev = rev / 10;
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 12345;

    NumbertoCharacter(n);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program to convert number in characters

function NumbertoCharacter(n)
{
    let rev = 0, r = 0;

    // To calculate the reverse of the number
    while (n > 0)
    {

        // The remainder will give
        // the last digit of the number
        r = n % 10;
        rev = rev * 10 + r;
        n = Math.floor(n / 10);
    }

    while (rev > 0)
    {

        // Extract the first digit
        // of the reversed number
        r = rev % 10;

        // Match it with switch case
        switch (r)
        {
        case 1:
            document.write("one ");
            break;
        case 2:
            document.write("two ");
            break;
        case 3:
            document.write("three ");
            break;
        case 4:
            document.write("four ");
            break;
        case 5:
            document.write("five ");
            break;
        case 6:
            document.write("six ");
            break;
        case 7:
            document.write("seven ");
            break;
        case 8:
            document.write("eight ");
            break;
        case 9:
            document.write("nine ");
            break;
        case 0:
            document.write("zero ");
            break;
        default:
            document.write("UnValid ");
            break;
        }

        // Divide the number by 10
        // to get the next number
        rev = Math.floor(rev / 10);
    }
}

// Driver code
let n = 12345;
NumbertoCharacter(n);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
one two three four five
```

**时间复杂度:** O(k)
k 是数字的长度。
**空间复杂度:** O(1)