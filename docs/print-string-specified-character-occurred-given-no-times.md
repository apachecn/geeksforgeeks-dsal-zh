# 在指定字符出现给定次数后打印字符串

> 原文:[https://www . geesforgeks . org/print-string-specified-character-excepted-给定-no-times/](https://www.geeksforgeeks.org/print-string-specified-character-occurred-given-no-times/)

给定一个字符串、一个字符和一个计数，任务是在指定的字符出现计数次数后打印该字符串。如果出现任何不满意的情况，请打印“空字符串”。(给定字符不存在，或存在但少于给定计数，或给定计数在最后一次索引时完成)。如果给定的计数是 0，那么给定的字符不重要，只需打印整个字符串。
**例:**

```
Input  :  str = "This is demo string" 
          char = i,    
          count = 3
Output :  ng

Input :  str = "geeksforgeeks"
         char = e, 
         count = 2
Output : ksforgeeks
```

问于:[甲骨文](https://www.geeksforgeeks.org/oracle-interview-set-8-campus-application-developer-2/)T2】

**实现:**
1-开始遍历字符串。

*   如果当前字符等于给定字符，则增加 occ_count。
*   如果 occ_count 等于给定计数，则退出循环。

2-在索引后打印字符串，直到字符串在循环中被遍历。
3-如果索引已经到达最后，则打印“空字符串”。

## C++

```
// C++ program for above implementation
#include <iostream>
using namespace std;

// Function to print the string
void printString(string str, char ch, int count)
{
    int occ = 0, i;

    // If given count is 0
    // print the given string and return
    if (count == 0) {
        cout << str;
        return;
    }

    // Start traversing the string
    for (i = 0; i < str.length(); i++) {

        // Increment occ if current char is equal
        // to given character
        if (str[i] == ch)
            occ++;

        // Break the loop if given character has
        // been occurred given no. of times
        if (occ == count)
            break;
    }

    // Print the string after the occurrence
    // of given character given no. of times
    if (i < str.length() - 1)
        cout << str.substr(i + 1, str.length() - (i + 1));

    // Otherwise string is empty
    else
        cout << "Empty string";
}

// Drivers code
int main()
{
    string str = "geeks for geeks";
    printString(str, 'e', 2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation

public class GFG
{
    // Method to print the string
    static void printString(String str, char ch, int count)
    {
        int occ = 0, i;

        // If given count is 0
        // print the given string and return
        if (count == 0) {
            System.out.println(str);
            return;
        }

        // Start traversing the string
        for (i = 0; i < str.length(); i++) {

            // Increment occ if current char is equal
            // to given character
            if (str.charAt(i) == ch)
                occ++;

            // Break the loop if given character has
            // been occurred given no. of times
            if (occ == count)
                break;
        }

        // Print the string after the occurrence
        // of given character given no. of times
        if (i < str.length() - 1)
            System.out.println(str.substring(i + 1));

        // Otherwise string is empty
        else
            System.out.println("Empty string");
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "geeks for geeks";
        printString(str, 'e', 2);
    }
}
```

## 蟒蛇 3

```
# Python3 program for above implementation

# Function to print the string
def printString(str, ch, count):
    occ, i = 0, 0

    # If given count is 0
    # print the given string and return
    if (count == 0):
        print(str)

    # Start traversing the string
    for i in range(len(str)):

        # Increment occ if current char
        # is equal to given character
        if (str[i] == ch):
            occ += 1

        # Break the loop if given character has
        # been occurred given no. of times
        if (occ == count):
            break

    # Print the string after the occurrence
    # of given character given no. of times
    if (i < len(str)- 1):
        print(str[i + 1: len(str) - i + 2])

    # Otherwise string is empty
    else:
        print("Empty string")

# Driver code
if __name__ == '__main__':
    str = "geeks for geeks"
    printString(str, 'e', 2)

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# program for above implementation
using System;

public class GFG {

    // Method to print the string
    static public void printString(string str,
                           char ch, int count)
    {
        int occ = 0, i;

        // If given count is 0
        // print the given string
        // and return
        if (count == 0) {
            Console.WriteLine(str);
            return;
        }

        // Start traversing the string
        for (i = 0; i < str.Length; i++)
        {

            // Increment occ if current
            // char is equal to given
            // character
            if (str[i] == ch)
                occ++;

            // Break the loop if given
            // character has been occurred
            // given no. of times
            if (occ == count)
                break;
        }

        // Print the string after the
        // occurrence of given character
        // given no. of times
        if (i < str.Length - 1)
            Console.WriteLine(str.Substring(i + 1));

        // Otherwise string is empty
        else
            Console.WriteLine("Empty string");
    }

    // Driver Method
    static public void Main()
    {
        string str = "geeks for geeks";
        printString(str, 'e', 2);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program for above implementation

// Method to print the string
function printString(str, ch , count)
{
    var occ = 0, i;

    // If given count is 0
    // print the given string and return
    if (count == 0) {
        document.write(str);
        return;
    }

    // Start traversing the string
    for (i = 0; i < str.length; i++) {

        // Increment occ if current char is equal
        // to given character
        if (str.charAt(i) == ch)
            occ++;

        // Break the loop if given character has
        // been occurred given no. of times
        if (occ == count)
            break;
    }

    // Print the string after the occurrence
    // of given character given no. of times
    if (i < str.length - 1)
        document.write(str.substring(i + 1));

    // Otherwise string is empty
    else
        document.write("Empty string");
}

// Driver Method
var str = "geeks for geeks";
printString(str, 'e', 2);

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
ks for geeks
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。