# 删除两个零之间的元素

> 原文:[https://www.geeksforgeeks.org/removing-elements-two-zeros/](https://www.geeksforgeeks.org/removing-elements-two-zeros/)

给定一个显示字符串大小的整数 N，在下一行中给定一个字符串**，它包含一个只有 0 和 1 的字符串**。任务是每次删除两个零字符之间的单个字符。

**在每一回合中，只有满足以下条件的字符串中的一个字符将被删除:**

*   It must be surrounded by zeros on both sides.

**例:**

```
Input  : str = "1001
Output : str = "1001"

Input  : str = "10101
Output : str = "1001"

```

使用从 1 到 N–1 的循环，检查是否有任何元素位于两个零之间，例如 s[I–1]= ' 0 '和 s[i + 1] = '0 '。如果条件满足，则删除该位置的字符，并再次开始搜索模式。

## c++

```
// C++ program to delete elements between zeros
#include <bits/stdc++.h>
using namespace std;

// Function to find the string 
// after operation
string findstring(string s)
{
    int n = s.length();

    // Travesing through string 
    for (int i = 1; i < n - 1; i++)
    {
        // Checking for character 
        // Between two zeros
        if ((s.at(i - 1) == '0' && 
            s.at(i + 1) == '0'))
        {

            // deleting the character 
            // At specific position
            s.erase(i, 1);

            i--;
            if (i > 0 && s.at(i - 1) == '0')
                 i--;

            // updating the length 
            // of the string
            n = s.length();
        }
    }

    return s;
}

// Drivers code
int main() {

    cout << findstring("100100");
    return 0;
}
```

## Java

```
// Java program to delete elements between zeros
import java.util.*;

public class GFG 
{
    // Function to find the string 
    // after operation
    static String findstring(String s)
    {
        int n = s.length();

        // use for loop to remove the
        // character between two zeros
        for (int i = 1; i < n - 1; i++)
        { 
            // Checking for character 
            // Between two zeros
            if ((s.charAt(i - 1) == '0' && 
                 s.charAt(i + 1) == '0'))
            {

                // deleting the character 
                // At specific position
                s = s.substring(0, i) + s.substring(i + 1);

                i--;
                if (i > 0 && s.charAt(i - 1) == '0')
                    i--;

                // updating the length 
                // of the string
                n = s.length();
            }
        }

        return s;
    }

    // Driver code
    public static void main(String[] args)
    {
       String s="100100";
       System.out.println(findstring(s));
    }
}
```

## python 3

```
# Python3 program to delete elements
# between zeros

# Function to find the string
# after operation
def findstring(s):

    n = len(s)
    s = list(s)
    i = 1

    # Travesing through string
    while i < n - 1:

        # Checking for character
        # Between two zeros
        if (s[i - 1] == '0' and 
            s[i + 1] == '0'):

            # Deleting the character
            # At specific position
            s.pop(i)

            i -= 1
            if i > 0 and s[i - 1] == '0':
                i -= 1

            # Updating the length
            # of the string
            n = len(s)
        i += 1

    return ''.join(s)

# Driver code
if __name__ == '__main__':

    print (findstring('100100'))

# This code is contributed by rutvik_56
```

## c#

```
// C# program to delete 
// elements between zeros
using System;

class GFG
{
    // Function to find the 
    // string after operation
    static string findstring(string s)
    {
        int n = s.Length;
        string st = "";

        // Travesing through string 
        for (int i = 1; i < n - 1; i++)
        {
            // Checking for character 
            // Between two zeros
            if ((s[i - 1] == '0' && 
                 s[i + 1] == '0'))
            {

                // deleting the character 
                // At specific position
                st = s.Remove(i, 1);
                s = st;

                i--;
                if (i > 0 && 
                    s[i - 1] == '0')
                    i--;

                // updating the length 
                // of the string
                n = s.Length;
            }
        }                 
        return s;
    }

    // Driver code
    static void Main()
    {
        Console.Write(findstring("100100"));
    }
}

// This code is contributed by 
// Manish Shaw(manishshaw1)
```

**输出:**

```
100

```

**时间复杂度:** O(N)，其中 N 为输入字符串的大小。