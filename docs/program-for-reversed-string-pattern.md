# 反串模式程序

> 原文:[https://www . geesforgeks . org/program-for-reversed-string-pattern/](https://www.geeksforgeeks.org/program-for-reversed-string-pattern/)

给定字符串**字符串**作为输入。任务是打印模式，如示例所示。

**示例:**

> **输入:** str = "geeks"
> **输出:**
> g
> e
> * s k
> **说明:**
> 在第一行，打印字符串中的第一个字符。
> 在第二行，以相反的顺序打印下两个字符。
> 第三行字符不够打印，追加*s，倒序打印。
> 
> **输入:** str = "orange"
> **输出:**
> o
> a r
> e g n

**进场:**

*   用值 **1** 初始化一个空列表和一个变量 **x** 。
*   遍历输入字符串**字符串**，并将字符添加到列表中。
*   如果列表的长度等于 **x** 的值，那么
    1.  以相反的顺序打印列表中的字符。
    2.  将 x 的值增加 1。
    3.  清空列表
*   如果最后一个打印字符的长度不是 **0** 并且小于 **x** 的值，则追加 **x-length(x) *s** 并以相反的顺序打印。

## C++

```
#include<bits/stdc++.h>
using namespace std;

// method declared to print the pattern of
// the string passed as argument
void reverseString(string str)
    {
        // a temporary string to store the
        // value of each row of pattern
        string r = "";
        int x = 1;
        for (int i = 0 ; i < str.length(); i++)
        {
            // extracting each character and
            // adding it to the string r
            r = r + str[i];
            if (r.length() == x)
            {
                // loop to print the string r in reverse order
                for(int j = r.length() - 1; j >= 0; j--)
                    cout<<r.at(j) << " ";
                x += 1;
                r = "";
                cout<<endl;
            }
        }

        // condition checking to add the "*" if required
        if (r.length() < x && r.length() != 0)
        {
            // adding the number of "*" required in r
            for(int k = 1; k <= x - r.length(); k++)
                r = r + "*";

            // printing r in reverse order
            for(int j = r.length() - 1; j >= 0; j--)
                    cout << r.at(j) << " ";
        }
    }

// Driver Code
int main()
{
    // sample string to check the code
    string str = "geeks";

    // method calling
    reverseString(str);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
    // method declared to print the pattern of
    // the string passed as argument
    public static void reverseString(String str)
    {
        // a temporary string to store the
        // value of each row of pattern
        String r = "";
        int x = 1;
        for (int i = 0 ; i < str.length(); i++)
        {
            // extracting each character and
            // adding it to the string r
            r = r + str.charAt(i);
            if (r.length() == x)
            {
                // loop to print the string r in reverse order
                for(int j = r.length() - 1; j >= 0; j--)
                    System.out.print(r.charAt(j) + " ");
                x += 1;
                r = "";
                System.out.println();
            }
        }

        // condition checking to add the "*" if required
        if (r.length() < x && r.length() != 0)
        {
            // adding the number of "*" required in r
            for(int k = 1; k <= x - r.length(); k++)
                r = r + "*";

            // printing r in reverse order
            for(int j = r.length() - 1; j >= 0; j--)
                    System.out.print(r.charAt(j) + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // sample string to check the code
        String str = "geeks";

        // method calling
        reverseString(str);
    }
}

// This code is contributed by Animesh_Gupta
```

## 蟒蛇 3

```
# function to print the pattern
def reverseString(str):

    # initialize an empty list
    r = []

    # initialize the value of x as 1
    x = 1

    # traverse through all the characters of x
    for i in str:

        # append all the characters to the list
        r.append(i)

        # if the length of the list is x
        if len(r)== x:

            # print the list in reverse order
            print(*reversed(r))

            # increment the value of x
            x+= 1
            # empty the list
            r = []

    # if the list is not empty
    # length of the list is less than x
    if len(r)<x and len(r)!= 0:

        # print x-len(r) *s and the reversed list
        print('* ' * (x-len(r)), *reversed(r))

# get the input string
str = "geeks"

# calling the function to print the pattern
reverseString(str)
```

## C#

```
using System;

class GFG
{
    // method declared to print the pattern of
    // the string passed as argument
    public static void reverseString(String str)
    {
        // a temporary string to store the
        // value of each row of pattern
        String r = "";
        int x = 1;
        for (int i = 0 ; i < str.Length; i++)
        {
            // extracting each character and
            // adding it to the string r
            r = r + str[i];
            if (r.Length == x)
            {
                // loop to print the string r in reverse order
                for(int j = r.Length - 1; j >= 0; j--)
                    Console.Write(r[j] + " ");
                x += 1;
                r = "";
                Console.WriteLine();
            }
        }

        // condition checking to add the "*" if required
        if (r.Length < x && r.Length != 0)
        {
            // adding the number of "*" required in r
            for(int k = 1; k <= x - r.Length; k++)
                r = r + "*";

            // printing r in reverse order
            for(int j = r.Length - 1; j >= 0; j--)
                    Console.Write(r[j] + " ");
        }
    }

    // Driver Code
    public static void Main(String []args)
    {
        // sample string to check the code
        String str = "geeks";

        // method calling
        reverseString(str);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// method declared to print the pattern of
// the string passed as argument
function reverseString(str) {
        // a temporary string to store the
        // value of each row of pattern
        var r = "";
        var x = 1;
        for (var i = 0 ; i < str.length; i++)
        {
            // extracting each character and
            // adding it to the string r
            r = r + str[i];
            if (r.length == x)
            {
                // loop to print the string r in reverse order
                for(var j = r.length - 1; j >= 0; j--)
                    document.write( r[j] + " ");
                x += 1;
                r = "";
                document.write("<br>");
            }
        }

        // condition checking to add the "*" if required
        if (r.length < x && r.length != 0)
        {
            // adding the number of "*" required in r
            for(var k = 1; k <= x - r.length; k++)
                r = r + "*";

            // printing r in reverse order
            for(var j = r.length - 1; j >= 0; j--)
                    document.write( r[j] + " ");
        }
    }

// Driver Code
// sample string to check the code
var str = "geeks";

// method calling
reverseString(str);

</script>
```

**Output:** 

```
g
e e
* s k
```