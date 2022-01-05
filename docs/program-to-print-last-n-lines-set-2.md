# 程序打印最后 N 行| Set-2

> 原文:[https://www . geesforgeks . org/program-to-print-last-n-line-set-2/](https://www.geeksforgeeks.org/program-to-print-last-n-lines-set-2/)

给定一个字符串中的一些文本行，每行由“\n”字符分隔。打印最后 N 行。如果行数小于 N，则打印所有行。

这个问题的解决方法已经在 [Set-1](https://www.geeksforgeeks.org/print-last-10-lines-of-a-given-file/) 中讨论过，其中只打印了 10 行。在这篇文章中，讨论了打印最后 N 行的另一种方法。

**算法:**

*   使用 [strtok](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/) 将字符串分割成“\n”周围。
*   将单个字符串存储在向量中。
*   打印向量的最后 N 个字符串。

下面是上述方法的实现:

## C++

```
// C++ program to print the last N lines
#include <bits/stdc++.h>
using namespace std;

void PrintLast(string s, int t)
{
    // Vector to store individual strings.
    vector<string> v;

    // Get a pointer to string.
    char* str = &s[0];
    // Split the string around '\n'.
    char* token = strtok(str, "\n");

    // Save all strings in the vector.
    while (token) {
        v.push_back(token);
        token = strtok(NULL, "\n");
    }

    if (v.empty()) {
        cout << "ERROR: string doesn't contain '\\n' character\n";
        return;
    }

    // If the string has t lines
    if (v.size() >= t) {
        for (int i = v.size() - t; i < v.size(); i++)
            cout << v[i] << endl;
    }
    else {
        for (int i = 0; i < v.size(); i++)
            cout << v[i] << endl;
    }
}

// Driver Code
int main()
{
    string s1 = "str1\nstr2\nstr3\nstr4\nstr5\nstr6\nstr7\nstr8\nstr9"
                "\nstr10\nstr11\nstr12\nstr13\nstr14\nstr15\nstr16\nstr17"
                "\nstr18\nstr19\nstr20\nstr21\nstr22\nstr23\nstr24\nstr25";
    int n = 10;
    PrintLast(s1, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the last N lines
import java.util.*;

class GFG 
{
    static void printLast(String s, int t)
    {

        // Vector to store individual strings.
        // Save all strings in the vector.
        String[] v = s.split("\n");

        if (v.length == 0) 
        {
            System.out.println("ERROR: string doesn't " + 
                              "contain '\\n' character");
            return;
        }

        // If the string has t lines
        if (v.length >= t) 
        {
            for (int i = v.length - t; i < v.length; i++)
            {
                System.out.println(v[i]);
            }
        } 
        else 
        {
            for (int i = 0; i < v.length; i++)
            {
                System.out.println(v[i]);
            }
        }
    }

    // Driver Code
    public static void main(String[] args) 
    {
        String s1 = "str1\nstr2\nstr3\nstr4\nstr5\nstr6\nstr7" + 
                    "\nstr8\nstr9\nstr10\nstr11\nstr12\nstr13" + 
                    "\nstr14\nstr15\nstr16\nstr17\nstr18\nstr19" + 
                    "\nstr20\nstr21\nstr22\nstr23\nstr24\nstr25";
        int n = 10;
        printLast(s1, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to print the last N lines 
def PrintLast(s, t): 

    # Vector to store individual strings. 
    v = s.split('\n')

    if len(v) == 0: 
        print("ERROR: string doesn't ",
              "contain '\\n' character\n") 
        return

    # If the string has t lines 
    elif len(v) >= t: 
        for i in range(len(v) - t, len(v)): 
            print(v[i]) 

    else:
        for i in range(0, len(v)): 
            print(v[i])

# Driver Code 
if __name__ == "__main__":

    s1 = "str1\nstr2\nstr3\nstr4\nstr5\nstr6" + \
         "\nstr7\nstr8\nstr9\nstr10\nstr11" + \
         "\nstr12\nstr13\nstr14\nstr15\nstr16" + \
         "\nstr17\nstr18\nstr19\nstr20\nstr21" + \
         "\nstr22\nstr23\nstr24\nstr25"

    n = 10
    PrintLast(s1, n) 

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print the last N lines
using System;

class GFG 
{
    static void printLast(String s, int t)
    {

        // List to store individual strings.
        // Save all strings in the vector.
        String[] v = s.Split('\n');

        if (v.Length == 0) 
        {
            Console.WriteLine("ERROR: string doesn't " + 
                            "contain '\\n' character");
            return;
        }

        // If the string has t lines
        if (v.Length >= t) 
        {
            for (int i = v.Length - t; i < v.Length; i++)
            {
                Console.WriteLine(v[i]);
            }
        } 
        else
        {
            for (int i = 0; i < v.Length; i++)
            {
                Console.WriteLine(v[i]);
            }
        }
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        String s1 = "str1\nstr2\nstr3\nstr4\nstr5\nstr6\nstr7" + 
                    "\nstr8\nstr9\nstr10\nstr11\nstr12\nstr13" + 
                    "\nstr14\nstr15\nstr16\nstr17\nstr18\nstr19" + 
                    "\nstr20\nstr21\nstr22\nstr23\nstr24\nstr25";
        int n = 10;
        printLast(s1, n);
    }
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
str16
str17
str18
str19
str20
str21
str22
str23
str24
str25

```