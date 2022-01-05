# 打印给定字符串的所有子字符串的程序

> 原文:[https://www . geesforgeks . org/program-print-substrings-given-string/](https://www.geeksforgeeks.org/program-print-substrings-given-string/)

给定一个字符串作为输入。我们需要编写一个程序，打印给定字符串的所有非空子字符串。

**例:**

```
Input :  abcd
Output :  a 
          b
          c
          d
          ab
          bc
          cd
          abc
          bcd
          abcd
```

我们可以运行三个嵌套循环，最外面的循环选择一个起始字符，中间的循环将所选字符右边的所有字符视为子串的结束字符。最里面的循环打印从当前拾取的起点到拾取的终点的字符。

## c++

```
// C++ program to print all possible
// substrings of a given string

#include<bits/stdc++.h>
using namespace std;

// Function to print all sub strings
void subString(char str[], int n)
{
    // Pick starting point
    for (int len = 1; len <= n; len++)
    {   
        // Pick ending point
        for (int i = 0; i <= n - len; i++)
        {
            //  Print characters from current
            // starting point to current ending
            // point. 
            int j = i + len - 1;           
            for (int k = i; k <= j; k++)
                cout << str[k];

            cout << endl;
        }
    }
}

// Driver program to test above function
int main()
{
    char str[] = "abc";
    subString(str, strlen(str));
    return 0;
}
```

## Java

```
//Java program to print all possible
// substrings of a given string

class GFG {

// Function to print all sub strings
    static void subString(char str[], int n) {
        // Pick starting point
        for (int len = 1; len <= n; len++) {
            // Pick ending point
            for (int i = 0; i <= n - len; i++) {
                //  Print characters from current
                // starting point to current ending
                // point. 
                int j = i + len - 1;
                for (int k = i; k <= j; k++) {
                    System.out.print(str[k]);
                }

                System.out.println();
            }
        }
    }

// Driver program to test above function
    public static void main(String[] args) {
        char str[] = {'a', 'b', 'c'};
        subString(str, str.length);

    }
}
// This code is contributed by PrinciRaj1992
```

## Python

```
# Python3 program to print all possible
# substrings of a given string

# Function to print all sub strings
def subString(Str,n):

    # Pick starting point
    for Len in range(1,n + 1):

        # Pick ending point
        for i in range(n - Len + 1):

            # Print characters from current
            # starting point to current ending
            # point.
            j = i + Len - 1

            for k in range(i,j + 1):
                print(Str[k],end="")
            print()

# Driver program to test above function
Str = "abc"
subString(Str,len(Str))

# This code is contributed by mohit kumar
```

## c#

```
// C# program to print all possible
// substrings of a given string
using System;

public class GFG {

    // Function to print all sub
    // strings
    static void subString(string str,
                               int n)
    {

        // Pick starting point
        for (int len = 1; len <= n;
                               len++)
        {
            // Pick ending point
            for (int i = 0;
                    i <= n - len; i++)
            {
                // Print characters
                // from current
                // starting point to
                // current ending
                // point.
                int j = i + len - 1;

                for (int k = i; k <= j;
                                    k++)
                    Console.Write(str[k]);

                Console.WriteLine();
            }
        }
    }

    // Driver program to test
    // above function
    static public void Main ()
    {
        string str = "abc";
        subString(str, str.Length);
    }
}

// This code is contributed by anuj_67.
```

## PHP

T4

## Javascript

```
<script>
//Javascript program to print all possible
// substrings of a given string

    // Function to print all sub strings
    function subString(str,n)
    {
        // Pick starting point
        for (let len = 1; len <= n; len++) {
            // Pick ending point
            for (let i = 0; i <= n - len; i++) {
                //  Print characters from current
                // starting point to current ending
                // point.
                let j = i + len - 1;
                for (let k = i; k <= j; k++) {
                    document.write(str[k]);
                }

                document.write("<br>");
            }
        }
    }
    // Driver program to test above function
    let str=['a', 'b', 'c'];
    subString(str, str.length);

// This code is contributed by patel2127
</script>
```

**输出**

```
a
b
c
ab
bc
abc
```