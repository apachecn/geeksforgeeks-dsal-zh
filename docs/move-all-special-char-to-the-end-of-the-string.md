# 将所有特殊字符移动到字符串的末尾

> 原文:[https://www . geesforgeks . org/move-all-special-char-to-the-end-the-string/](https://www.geeksforgeeks.org/move-all-special-char-to-the-end-of-the-string/)

在本文中，我们将学习如何将所有特殊字符移动到字符串的末尾。
**例:**

> **输入:**！@$%^ & *AJAY
> **输出:** AJAY！@$%^ & *
> **输入:**极客 sf！@ orgeek @ s a # $ c%o^mputer s * * * * science p # o @ rtal fo @ r ge % eks
> **输出:**geeks forgeek 是一个面向极客的计算机科学门户网站！@@#$%^****#@@%

先决条件:[Java 中的正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)
思想是遍历输入字符串并维护两个字符串，一个字符串包含普通字符(A，A，1，' '等)，另一个字符串维护特殊字符(@，$，等)。最后，连接两个字符串并返回。
**这里是执行上述方法的**

## C++

```
// C++ program move all special char to the end of the string

#include <bits/stdc++.h>
using namespace std;

// Function return a string with all special
// chars to the end
string moveAllSC(string str)
{
    // Take length of string
    int len = str.length();

    // traverse string
    string res1 = "", res2 = "";
    for (int i = 0; i < len; i++)
    {
        char c = str.at(i);

        // check char at index i is a special char
        if (isalnum(c) || c == ' ')
            res1 += c;
        else
            res2 += c;
    }

    return res1 + res2;
}

// Driver code
int main()
{
    string str1("Geeksf!@orgeek@s A#$ c%o^mputer");
    string str2(" s****cience p#o@rtal fo@r ge%eks");
    string str = str1 + str2;
    cout << moveAllSC(str) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program move all special char to the end of the string
class GFG1 {

    // Function return a string with all special
    // chars to the end
    static String moveAllSC(String str)
    {
        // Take length of string
        int len = str.length();

        // regular expression for check char is special
        // or not.
        String regx = "[a-zA-Z0-9\\s+]";

        // traverse string
        String res1 = "", res2 = "";
        for (int i = 0; i < len; i++) {

            char c = str.charAt(i);

            // check char at index i is a special char
            if (String.valueOf(c).matches(regx))
               res1 = res1 + c;
            else
               res2 = res2 + c;
        }
        return res1 + res2;
    }

    public static void main(String args[])
    {
        String str = "Geeksf!@orgeek@s A#$ c%o^mputer"
                     + " s****cience p#o@rtal fo@r ge%eks";
        System.out.println(moveAllSC(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program move all special char
# to the end of the string

# Function return a string with all
# special chars to the end
def moveAllSC(string):

    # Take length of string
    length = len(string)

    # Traverse string
    res1, res2 = "", ""
    for i in range(0, length):

        c = string[i]

        # check char at index i is a special char
        if c.isalnum() or c == " ":
            res1 = res1 + c
        else:
            res2 = res2 + c

    return res1 + res2

# Driver Code
if __name__ == "__main__":

    string = "Geeksf!@orgeek@s A#$ c%o^mputer" \
            +" s****cience p#o@rtal fo@r ge%eks"

    print(moveAllSC(string))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program move all special char
// to the end of the string
using System;
using System.Text.RegularExpressions;

class GFG
{

    // Function return a string with all
    // special chars to the end
    static String moveAllSC(String str)
    {
        // Take length of string
        int len = str.Length;

        // regular expression to check
        // char is special or not.
        var regx = new Regex("[a-zA-Z0-9\\s+]");

        // traverse string
        String res1 = "", res2 = "";
        for (int i = 0; i < len; i++)
        {
            char c = str[i];

            // check char at index i is a special char
            if (regx.IsMatch(c.ToString()))
                res1 = res1 + c;
            else
                res2 = res2 + c;
        }
        return res1 + res2;
    }

    public static void Main(String []args)
    {
        String str = "Geeksf!@orgeek@s A#$ c%o^mputer" +
                     " s****cience p#o@rtal fo@r ge%eks";
        Console.WriteLine(moveAllSC(str));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript program move all special char
      // to the end of the string
      // Function return a string with all
      // special chars to the end
      function moveAllSC(str) {
        // Take length of string
        var len = str.length;

        // regular expression to check
        // char is special or not.
        var regx = new RegExp("[a-zA-Z0-9\\s+]");

        // traverse string
        var res1 = "",
          res2 = "";
        for (var i = 0; i < len; i++) {
          var c = str[i].toString();
          // check char at index i is a special char
          if (regx.test(c)) res1 = res1 + c;
          else res2 = res2 + c;
        }
        return res1 + res2;
      }

      var str =
        "Geeksf!@orgeek@s A#$ c%o^mputer" + " s****cience p#o@rtal fo@r ge%eks";
      document.write(moveAllSC(str));
    </script>
```

**Output:** 

```
Geeksforgeeks A computer science portal for geeks!@@#$%^****#@@%
```