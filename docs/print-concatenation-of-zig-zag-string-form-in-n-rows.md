# 打印 n 行之字形字符串的连接

> 原文:[https://www . geesforgeks . org/print-concation-of-zig-zag-string-form-in-row/](https://www.geeksforgeeks.org/print-concatenation-of-zig-zag-string-form-in-n-rows/)

给定一个字符串和行数“n”。当输入字符串以之字形逐行写入时，打印由 n 行连接而成的字符串。

**示例:**

```
Input: str = "ABCDEFGH"
       n = 2
Output: "ACEGBDFH"
Explanation: Let us write input string in Zig-Zag fashion
             in 2 rows.
A   C   E   G   
  B   D   F   H
Now concatenate the two rows and ignore spaces 
in every row. We get "ACEGBDFH"

Input: str = "GEEKSFORGEEKS"
       n = 3
Output: GSGSEKFREKEOE
Explanation: Let us write input string in Zig-Zag fashion
             in 3 rows.
G       S       G       S
  E   K   F   R   E   K
    E       O       E
Now concatenate the two rows and ignore spaces 
in every row. We get "GSGSEKFREKEOE"
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/concatenation-of-zig-zag-string-in-n-rows0308/1)

想法是遍历输入字符串。每个角色都必须到其中一行。逐个将所有字符添加到不同的行中。下面是算法:

```
1) Create an array of n strings, arr[n]
2) Initialize direction as "down" and row as 0\. The 
   direction indicates whether we need to move up or 
   down in rows. 
3) Traverse the input string, do following for every
   character.
   a) Append current character to string of current row.
   b) If row number is n-1, then change direction to 'up'
   c) If row number is 0, then change direction to 'down'
   d) If direction is 'down', do row++.  Else do row--.
4) One by one print all strings of arr[]. 
```

以下是上述想法的实现。

## C++

```
// C++ program to print string obtained by concatenation
// of different rows of Zig-Zag fashion

#include<bits/stdc++.h>
using namespace std;

// Prints concatenation of all rows of str's Zig-Zag fashion
void printZigZagConcat(string str, int n)
{
    // Corner Case (Only one row)
    if (n == 1)
    {
        cout << str;     
        return;
    }  

    // Find length of string
    int len = str.length();

    // Create an array of strings for all n rows
    string arr[n];

    // Initialize index for array of strings arr[]
    int row = 0;
    bool down; // True if we are moving down in rows,
               // else false

    // Traverse through given string
    for (int i = 0; i < len; ++i)
    {
        // append current character to current row
        arr[row].push_back(str[i]);

        // If last row is reached, change direction to 'up'
        if (row == n-1)
          down = false;

        // If 1st row is reached, change direction to 'down'
        else if (row == 0)
          down = true;

        // If direction is down, increment, else decrement
        (down)? (row++): (row--);
    }

    // Print concatenation of all rows
    for (int i = 0; i < n; ++i)
        cout << arr[i];
}

// Driver program
int main()
{
    string str = "GEEKSFORGEEKS";
    int n = 3;
    printZigZagConcat(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print string
// obtained by concatenation
// of different rows of
// Zig-Zag fashion
import java.util.Arrays;

class GFG {

    // Prints concatenation
    // of all rows of str's
    // Zig-Zag fashion
    static void printZigZagConcat(String str,
            int n)
    {

        // Corner Case (Only one row)
        if (n == 1)
        {
            System.out.print(str);
            return;
        }
        char[] str1 = str.toCharArray();

        // Find length of string
        int len = str.length();

        // Create an array of
        // strings for all n rows
        String[] arr = new String[n];
        Arrays.fill(arr, "");

        // Initialize index for
        // array of strings arr[]
        int row = 0;
        boolean down = true; // True if we are moving
        // down in rows, else false

        // Traverse through
        // given string
        for (int i = 0; i < len; ++i)
        {
            // append current character
            // to current row
            arr[row] += (str1[i]);

            // If last row is reached,
            // change direction to 'up'
            if (row == n - 1)
            {
                down = false;
            }

            // If 1st row is reached,
            // change direction to 'down'
            else if (row == 0)
            {
                down = true;
            }

            // If direction is down,
            // increment, else decrement
            if (down)
            {
                row++;
            }
            else
            {
                row--;
            }
        }

        // Print concatenation
        // of all rows
        for (int i = 0; i < n; ++i)
        {
            System.out.print(arr[i]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "GEEKSFORGEEKS";
        int n = 3;
        printZigZagConcat(str, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to print
# string obtained by
# concatenation of different
# rows of Zig-Zag fashion

# Prints concatenation of all
# rows of str's Zig-Zag fashion
def printZigZagConcat(str, n):

    # Corner Case (Only one row)
    if n == 1:
        print(str)    
        return

    # Find length of string
    l = len(str)

    # Create an array of
    # strings for all n rows
    arr=["" for x in range(l)]

    # Initialize index for
    # array of strings arr[]
    row = 0

    # Traverse through
    # given string
    for i in range(l):

        # append current character
        # to current row
        arr[row] += str[i]

        # If last row is reached,
        # change direction to 'up'
        if row == n - 1:
            down = False

        # If 1st row is reached,
        # change direction to 'down'
        elif row == 0:
            down = True

        # If direction is down,
        # increment, else decrement
        if down:
            row += 1
        else:
            row -= 1

    # Print concatenation
    # of all rows
    for i in range(n):
        print(arr[i], end = "")

# Driver Code
str = "GEEKSFORGEEKS"
n = 3
printZigZagConcat(str, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print string
// obtained by concatenation
// of different rows of
// Zig-Zag fashion
using System;

class GFG
{

    // Prints concatenation
    // of all rows of str's
    // Zig-Zag fashion
    static void printZigZagConcat(string str,
                                  int n)
    {

    // Corner Case (Only one row)
    if (n == 1)
    {
        Console.Write(str);    
        return;
    }

    char[] str1 = str.ToCharArray();

    // Find length of string
    int len = str.Length;

    // Create an array of
    // strings for all n rows
    string []arr = new string[n];

    // Initialize index for
    // array of strings arr[]
    int row = 0;
    bool down = true; // True if we are moving
                      // down in rows, else false

    // Traverse through
    // given string
    for (int i = 0; i < len; ++i)
    {
        // append current character
        // to current row
        arr[row] += (str1[i]);

        // If last row is reached,
        // change direction to 'up'
        if (row == n - 1)
        down = false;

        // If 1st row is reached,
        // change direction to 'down'
        else if (row == 0)
        down = true;

        // If direction is down,
        // increment, else decrement
        if(down)
        row++;
        else
        row--;
    }

    // Print concatenation
    // of all rows
    for (int i = 0; i < n; ++i)
        Console.Write(arr[i]);
    }

    // Driver Code
    public static void Main()
    {
        String str = "GEEKSFORGEEKS";
        int n = 3;
        printZigZagConcat(str, n);
    }
}

// This code is contributed
// by ChitraNayal
```

## java 描述语言

```
<script>
// Javascript program to print string
// obtained by concatenation
// of different rows of
// Zig-Zag fashion

// Prints concatenation
    // of all rows of str's
    // Zig-Zag fashion
function printZigZagConcat(str,n)
{
    // Corner Case (Only one row)
        if (n == 1)
        {
            document.write(str);
            return;
        }
        let str1 = str.split("");

        // Find length of string
        let len = str.length;

        // Create an array of
        // strings for all n rows
        let arr = new Array(n);
        for(let i=0;i<n;i++)
        {
            arr[i]="";
        }

        // Initialize index for
        // array of strings arr[]
        let row = 0;
        let down = true; // True if we are moving
        // down in rows, else false

        // Traverse through
        // given string
        for (let i = 0; i < len; ++i)
        {
            // append current character
            // to current row
            arr[row] += (str1[i]);

            // If last row is reached,
            // change direction to 'up'
            if (row == n - 1)
            {
                down = false;
            }

            // If 1st row is reached,
            // change direction to 'down'
            else if (row == 0)
            {
                down = true;
            }

            // If direction is down,
            // increment, else decrement
            if (down)
            {
                row++;
            }
            else
            {
                row--;
            }
        }

        // Print concatenation
        // of all rows
        for (let i = 0; i < n; ++i)
        {
            document.write(arr[i]);
        }
}

// Driver Code
let str = "GEEKSFORGEEKS";
let n = 3;
printZigZagConcat(str, n);

// This code is contributed by ab2127
</script>
```

**Output**

```
GSGSEKFREKEOE
```

**时间复杂度:** O(len)，其中 len 为输入字符串的长度。
**辅助空间:** O(len)
感谢高拉夫·阿希瓦尔提出上述解决方案。

**另一种方法:**
如果假设我们逐个迭代行数 n 的虚矩阵，并打印第一行和最后一行的字符
，对于中间行，索引将增加 i+= 2*(n-1)
的值，如果我们向上，索引将增加 i+= 2*(n-rowNum-1)，对于向下，索引将增加 2*rowNum。下面是工作实现。在 JAVA 中

下面是上述方法的实现:

## C++

```
// C++ Program for above approach
#include<bits/stdc++.h>
using namespace std;
// Function for zig-zag Concatenation
string zigZagConcat(string s, int n)
{
    // Check is n is less
    // or equal to 1
    if (n <= 1)
    {
        return s;
    }
    string result = "";
    // Iterate rowNum from 0 to n - 1
    for (int rowNum = 0; rowNum < n; rowNum++)
    {
        int i = rowNum;
        bool up = true;
        // Iterate i till s.length() - 1
        while (i < s.length())
        {

            result += s[i];

            // Check is rowNum is 0 or n - 1
            if (rowNum == 0 || rowNum == n - 1)
            {
                i += (2 * n - 2);
            }
            else
            {
                if (up)
                {
                    i += (2 * (n - rowNum) - 2);
                }
                else
                {
                    i += rowNum * 2;
                }
                up ^= true;
            }
        }
    }
    return result;
}

// Driver Code
int main()
{
    string str = "GEEKSFORGEEKS";
    int n = 3;
    cout<< zigZagConcat(str, n);
}

// This code is contributed by Mayank Tyagi
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.lang.*;

class Solution
{

    // Function for zig-zag Concatenation
    private static String zigZagConcat(
                                String s, int n)
    {

        // Check is n is less
        // or equal to 1
        if (n <= 1)
        {
            return s;
        }

        StringBuilder result = new
                             StringBuilder();

        // Iterate rowNum from 0 to n - 1
        for (int rowNum = 0; rowNum < n; rowNum++)
        {
            int i = rowNum;
            boolean up = true;

            // Iterate i till s.length() - 1
            while (i < s.length())
            {

                result = result.append(s.charAt(i));

                // Check is rowNum is 0 or n - 1
                if (rowNum == 0 || rowNum == n - 1)
                {
                    i += (2 * n - 2);
                }
                else
                {
                    if (up)
                    {
                        i += (2 * (n - rowNum) - 2);
                    }
                    else
                    {
                        i += rowNum * 2;
                    }
                    up ^= true;
                }
            }
        }
        return result.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "GEEKSFORGEEKS";
        int n = 3;
        System.out.println(zigZagConcat(str, n));
    }
}

// This code is contributed by Sakshi Sachdeva
```

## 蟒蛇 3

```
# Python Program for above approach

# Function for zig-zag Concatenation
def zigZagConcat(s, n):

    # Check is n is less 
    # or equal to 1
    if (n <= 1):
        return s

    result = ""

    # Iterate rowNum from 0 to n - 1
    for rowNum in range(n):
        i = rowNum
        up = True

        # Iterate i till s.length() - 1
        while(i < len(s)):
            result += s[i]

            # Check is rowNum is 0 or n - 1
            if (rowNum == 0 or rowNum == n - 1):
                i += (2 * n - 2)
            else:
                if(up):
                    i += (2 * (n - rowNum) - 2)
                else:
                    i += rowNum * 2
                up ^= True

    return result

# Driver Code
str = "GEEKSFORGEEKS"
n = 3
print(zigZagConcat(str, n))

# This code is contributed by rag2127
```

## C#

```
// C# Program for above approach
using System;
public class GFG{

  // Function for zig-zag Concatenation
  static string zigZagConcat( string s, int n)
  {
    // Check is n is less 
    // or equal to 1
    if (n <= 1) 
    {
      return s;
    }
    string result="";
    // Iterate rowNum from 0 to n - 1
    for (int rowNum = 0; rowNum < n; rowNum++)
    {
      int i = rowNum;
      bool up = true;
      // Iterate i till s.length() - 1
      while (i < s.Length) 
      {

        result += s[i];

        // Check is rowNum is 0 or n - 1
        if (rowNum == 0 || rowNum == n - 1) 
        {
          i += (2 * n - 2);
        }
        else
        {
          if (up) 
          {
            i += (2 * (n - rowNum) - 2);
          }
          else
          {
            i += rowNum * 2;
          }
          up ^= true;
        }
      }
    }
    return result;
  }

  // Driver Code
  static public void Main (){
    string str = "GEEKSFORGEEKS";
    int n = 3;
    Console.WriteLine(zigZagConcat(str, n));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript Program for above approach

// Function for zig-zag Concatenation
function zigZagConcat(s,n)
{

    // Check is n is less
        // or equal to 1
        if (n <= 1)
        {
            return s;
        }

        let result = [];

        // Iterate rowNum from 0 to n - 1
        for (let rowNum = 0; rowNum < n; rowNum++)
        {
            let i = rowNum;
            let up = true;

            // Iterate i till s.length() - 1
            while (i < s.length)
            {

                result.push(s[i]);

                // Check is rowNum is 0 or n - 1
                if (rowNum == 0 || rowNum == n - 1)
                {
                    i += (2 * n - 2);
                }
                else
                {
                    if (up)
                    {
                        i += (2 * (n - rowNum) - 2);
                    }
                    else
                    {
                        i += rowNum * 2;
                    }
                    up ^= true;
                }
            }
        }
        return result.join("");
}

// Driver Code
let str = "GEEKSFORGEEKS";
let n = 3;
document.write(zigZagConcat(str, n));

// This code is contributed by unknown2108
</script>
```

**Output**

```
GSGSEKFREKEOE
```

**时间复杂度:** O(长度)

**空间复杂度:** O(1)

感谢释迦牟尼提出上述解决方案。
如果发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论