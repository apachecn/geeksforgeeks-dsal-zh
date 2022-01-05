# 用文字打印给定数字的程序

> 原文:[https://www . geesforgeks . org/program-to-print-给定的数字输入单词/](https://www.geeksforgeeks.org/program-to-print-the-given-digit-in-words/)

给定一个数字 **N** ，任务是将数字的每个数字转换成单词。
**例:**

> **输入:** N = 1234
> **输出:**一二三四
> **说明:**
> 给定数字的每一位数字都转换成了对应的字。
> **输入:** N = 567
> **输出:**五六七

**方法:**思路是遍历数字的每个[位，使用](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)[开关盒](https://www.geeksforgeeks.org/switch-statement-cc/)。由于数字只有十个可能的值，因此在一个开关块中可以定义十种情况。对于每个数字，将执行其对应的大小写块，并将该数字打印成文字。
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to return the word
// of the corresponding digit
void printValue(char digit)
{

    // Switch block to check for each digit c
    switch (digit) {

    // For digit 0
    case '0':
        cout << "Zero ";
        break;

    // For digit 1
    case '1':
        cout << "One ";
        break;

    // For digit 2
    case '2':
        cout << "Two ";
        break;

    // For digit 3
    case '3':
        cout << "Three ";
        break;

    // For digit 4
    case '4':
        cout << "Four ";
        break;

    // For digit 5
    case '5':
        cout << "Five ";
        break;

    // For digit 6
    case '6':
        cout << "Six ";
        break;

    // For digit 7
    case '7':
        cout << "Seven ";
        break;

    // For digit 8
    case '8':
        cout << "Eight ";
        break;

    // For digit 9
    case '9':
        cout << "Nine ";
        break;
    }
}

// Function to iterate through every
// digit in the given number
void printWord(string N)
{
    int i, length = N.length();

    // Finding each digit of the number
    for (i = 0; i < length; i++) {

        // Print the digit in words
        printValue(N[i]);
    }
}

// Driver code
int main()
{
    string N = "123";
    printWord(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to return the word
// of the corresponding digit
static void printValue(char digit)
{

    // Switch block to check for each digit c
    switch (digit)
    {

    // For digit 0
    case '0':
        System.out.print("Zero ");
        break;

    // For digit 1
    case '1':
        System.out.print("One ");
        break;

    // For digit 2
    case '2':
        System.out.print("Two ");
        break;

    // For digit 3
    case '3':
        System.out.print("Three ");
        break;

    // For digit 4
    case '4':
        System.out.print("Four ");
        break;

    // For digit 5
    case '5':
        System.out.print("Five ");
        break;

    // For digit 6
    case '6':
        System.out.print("Six ");
        break;

    // For digit 7
    case '7':
        System.out.print("Seven ");
        break;

    // For digit 8
    case '8':
        System.out.print("Eight ");
        break;

    // For digit 9
    case '9':
        System.out.print("Nine ");
        break;
    }
}

// Function to iterate through every
// digit in the given number
static void printWord(String N)
{
    int i, length = N.length();

    // Finding each digit of the number
    for (i = 0; i < length; i++)
    {

        // Print the digit in words
        printValue(N.charAt(i));
    }
}

// Driver code
public static void main(String[] args)
{
    String N = "123";
    printWord(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the word
# of the corresponding digit
def printValue(digit):

    # Switch block to check for each digit c

    # For digit 0
    if digit == '0':
        print("Zero ", end = " ")

    # For digit 1
    elif digit == '1':
        print("One ", end = " ")

    # For digit 2
    elif digit == '2':
        print("Two ", end = " ")

    #For digit 3
    elif digit=='3':
        print("Three",end=" ")

    # For digit 4
    elif digit == '4':
        print("Four ", end = " ")

    # For digit 5
    elif digit == '5':
        print("Five ", end = " ")

    # For digit 6
    elif digit == '6':
        print("Six ", end = " ")

    # For digit 7
    elif digit == '7':
        print("Seven", end = " ")

    # For digit 8
    elif digit == '8':
        print("Eight", end = " ")

    # For digit 9
    elif digit == '9':
        print("Nine ", end = " ")

# Function to iterate through every
# digit in the given number
def printWord(N):
    i = 0
    length = len(N)

    # Finding each digit of the number
    while i < length:

        # Print the digit in words
        printValue(N[i])
        i += 1

# Driver code
N = "123"
printWord(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the word
    // of the corresponding digit
    static void printValue(char digit)
    {

        // Switch block to check for each digit c
        switch (digit)
        {

        // For digit 0
        case '0':
            Console.Write("Zero ");
            break;

        // For digit 1
        case '1':
            Console.Write("One ");
            break;

        // For digit 2
        case '2':
            Console.Write("Two ");
            break;

        // For digit 3
        case '3':
            Console.Write("Three ");
            break;

        // For digit 4
        case '4':
            Console.Write("Four ");
            break;

        // For digit 5
        case '5':
            Console.Write("Five ");
            break;

        // For digit 6
        case '6':
            Console.Write("Six ");
            break;

        // For digit 7
        case '7':
            Console.Write("Seven ");
            break;

        // For digit 8
        case '8':
            Console.Write("Eight ");
            break;

        // For digit 9
        case '9':
            Console.Write("Nine ");
            break;
        }
    }

    // Function to iterate through every
    // digit in the given number
    static void printWord(string N)
    {
        int i, length = N.Length;

        // Finding each digit of the number
        for (i = 0; i < length; i++)
        {

            // Print the digit in words
            printValue(N[i]);
        }
    }

    // Driver code
    public static void Main()
    {
        string N = "123";
        printWord(N);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

      // JavaScript implementation of
      // the above approach

      // Function to return the word
      // of the corresponding digit
      function printValue(digit) {
        // Switch block to check for
        // each digit c
        switch (digit) {
          // For digit 0
          case "0":
            document.write("Zero ");
            break;

          // For digit 1
          case "1":
            document.write("One ");
            break;

          // For digit 2
          case "2":
            document.write("Two ");
            break;

          // For digit 3
          case "3":
            document.write("Three ");
            break;

          // For digit 4
          case "4":
            document.write("Four ");
            break;

          // For digit 5
          case "5":
            document.write("Five ");
            break;

          // For digit 6
          case "6":
            document.write("Six ");
            break;

          // For digit 7
          case "7":
            document.write("Seven ");
            break;

          // For digit 8
          case "8":
            document.write("Eight ");
            break;

          // For digit 9
          case "9":
            document.write("Nine ");
            break;
        }
      }

      // Function to iterate through every
      // digit in the given number
      function printWord(N) {
        var i,
          length = N.length;

        // Finding each digit of the number
        for (i = 0; i < length; i++) {
          // Print the digit in words
          printValue(N[i]);
        }
      }

      // Driver code
      var N = "123";
      printWord(N);

</script>
```

**Output:** 

```
One Two Three
```

**相关文章:** [不使用 if 或 switch 将个别数字打印为文字](https://www.geeksforgeeks.org/print-individual-digits-as-words-without-using-if-or-switch/)