# 打印一个字符串的所有子序列

> 原文:[https://www.geeksforgeeks.org/print-subsequences-string/](https://www.geeksforgeeks.org/print-subsequences-string/)

给定一个字符串，我们必须找出它的所有子序列。字符串是给定字符串的子序列，它是通过删除给定字符串的某些字符而不改变其顺序来生成的。

示例:

```
Input : abc
Output : a, b, c, ab, bc, ac, abc

Input : aaa
Output : a, aa, aaa
```

**方法 1(挑与不挑概念)**

## c++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Find all subsequences
void printSubsequence(string input, string output)
{
    // Base Case
    // if the input is empty print the output string
    if (input.empty()) {
        cout << output << endl;
        return;
    }

    // output is passed with including
    // the Ist character of
    // Input string
    printSubsequence(input.substr(1), output + input[0]);

    // output is passed without
    // including the Ist character
    // of Input string
    printSubsequence(input.substr(1), output);
}

// Driver code
int main()
{
    // output is set to null before passing in as a
    // parameter
    string output = "";
    string input = "abcd";

    printSubsequence(input, output);

    return 0;
}
```

## Java

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Declare a global list
    static List<String> al = new ArrayList<>();

    // Creating a public static Arraylist such that
    // we can store values
    // IF there is any question of returning the
    // we can directly return too// public static
    // ArrayList<String> al = new ArrayList<String>();
    public static void main(String[] args)
    {
        String s = "abcd";
        findsubsequences(s, ""); // Calling a function
        System.out.println(al);
    }

    private static void findsubsequences(String s,
                                         String ans)
    {
        if (s.length() == 0) {
            al.add(ans);
            return;
        }

        // We add adding 1st character in string
        findsubsequences(s.substring(1), ans + s.charAt(0));

        // Not adding first character of the string
        // because the concept of subsequence either
        // character will present or not
        findsubsequences(s.substring(1), ans);
    }
}
```

## python 3

```
# Below is the implementation of the above approach
def printSubsequence(input, output):

    # Base Case
    # if the input is empty print the output string
    if len(input) == 0:
        print(output, end=' ')
        return

    # output is passed with including the
    # 1st character of input string
    printSubsequence(input[1:], output+input[0])

    # output is passed without including the
    # 1st character of input string
    printSubsequence(input[1:], output)

# Driver code
# output is set to null before passing in
# as a parameter
output = ""
input = "abcd"

printSubsequence(input, output)

# This code is contributed by Tharun Reddy
```

## c#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static void printSubsequence(string input,
                             string output)
{

    // Base Case
    // If the input is empty print the output string
    if (input.Length == 0)
    {
        Console.WriteLine(output);
        return;
    }

    // Output is passed with including
    // the Ist character of
    // Input string
    printSubsequence(input.Substring(1),
                     output + input[0]);

    // Output is passed without
    // including the Ist character
    // of Input string
    printSubsequence(input.Substring(1),
                     output);
}

// Driver code
static void Main()
{

    // output is set to null before passing
    // in as a parameter
    string output = "";
    string input = "abcd";

    printSubsequence(input, output);
}
}

// This code is contributed by SoumikMondal
```

## Javascript

```
<script>

// JavaScript program for the above approach

// Find all subsequences
function printSubsequence(input, output)
{
    // Base Case
    // if the input is empty print the output string
    if (input.length==0) {
        document.write( output + "<br>");
        return;
    }

    // output is passed with including
    // the Ist character of
    // Input string
    printSubsequence(input.substring(1), output + input[0]);

    // output is passed without
    // including the Ist character
    // of Input string
    printSubsequence(input.substring(1), output);
}

// Driver code
// output is set to null before passing in as a
// parameter
var output = "";
var input = "abcd";
printSubsequence(input, output);

</script>
```

**输出**

```
abcd
abc
abd
ab
acd
ac
ad
a
bcd
bc
bd
b
cd
c
d
```