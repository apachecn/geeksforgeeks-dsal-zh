# 用不同的字符替换字符串的每个字符

> 原文:[https://www . geesforgeks . org/用不同的字符替换字符串中的每个字符/](https://www.geeksforgeeks.org/replace-every-character-of-a-string-by-a-different-character/)

给定一个仅由小写字母组成的字符串**。任务是用新的字符替换每个字符。新字符属于![$a-z$   ](img/31ccc6b8d511ade3fc14a550e647dffb.png "Rendered by QuickLaTeX.com")(仅小写)str[i]的替换由:
决定**

> **字符串[i] =在字符串[i]后重复遍历 ascii(字符串[i])字符数后获得的字符。**

**示例:** 

> ****输入:** str = "geeksforgeeks"
> **输出:** fbbnddvbfbbnd
> 在上述情况下 str = " geeksforgeeks "
> 的 ASCII 值为 103，因此“g”被替换为在所需范围内从“g”移动 103 次，即 a-z.
> 因此，字符“g”被替换为“f”。
> 同样，完整的字符串“geeksforgeeks”变成了“fbbnddvbfbbnd”。
> **输入:** str = "science"
> **输出:** dxjbtxb**

****进场:**** 

1.  **遍历字符串。**
2.  **对于每个 I，找到需要用 str[i]替换的字符。**
3.  **将字符串[i]替换为该字符。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program for Replace every character of a
// string by a different character
#include <bits/stdc++.h>
using namespace std;

// Function to manipulate the string
void manipulateString(string &str)
{

    // looping through each character of string
    for (int i = 0; i < str.length(); i++) {

        // storing integer ASCII value of
        // the character in 'asc'
        int asc = str[i];

        // 'rem' contains coded value which
        // needs to be rounded to 26
        int rem = asc - (26 - (str[i] - 'a'));

        // converting 'rem' character in range
        // 0-25 and storing in 'm'
        int m = rem % 26;

        // printing character by adding ascii value of 'a'
        // so that it becomes in the desired range i.e. a-z
        str[i] = (char)(m + 'a');
    }
}

// Driver code
int main()
{

    // Declaring str as 'geeksforgeeks'
    string str = "geeksforgeeks";

    manipulateString(str);

    cout << str;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for Replace every character of a
// string by a different character
public class GFG {

    //Function to manipulate the string
    static void manipulateString(String str)
    {

        char[] str1 = str.toCharArray();

     // looping through each character of string
     for (int i = 0; i < str.length(); i++) {

         // storing integer ASCII value of
         // the character in 'asc'

         int asc = str1[i];

         // 'rem' contains coded value which
         // needs to be rounded to 26
         int rem = asc - (26 - (str1[i] - 97));

         // converting 'rem' character in range
         // 0-25 and storing in 'm'
         int m = rem % 26;

         // printing character by adding ascii value of 'a'
         // so that it becomes in the desired range i.e. a-z
         str1[i] = (char)(m + 'a');

     }

     String str2 = String.valueOf(str1);
     System.out.println(str2);

    }

    //Driver code
    public static void main(String[] args) {

        // Declaring str as 'geeksforgeeks'
         String str = "geeksforgeeks";

         manipulateString(str);

    }
}
```

## **蟒蛇 3**

```
# Python 3 program for Replace every character of a
# string by a different character

# Function to manipulate the string
def manipulateString(str) :

    # looping through each character of string
    for i in range(len(str)) :

        # storing integer ASCII value of
        # the character in 'asc'
        asc = ord(str[i])

        # 'rem' contains coded value which
        # needs to be rounded to 26
        rem = asc - (26 - (ord(str[i]) - ord('a')))

        # converting 'rem' character in range
        # 0-25 and storing in 'm'
        m  = rem % 26

        #printing character by adding ascii value of 'a'
        # so that it becomes in the desired range i
        str[i] = chr(m + ord('a'))

    # join method join all individual
    # characters to form a string
    print(''.join(str))

# Driver code    
if __name__ == "__main__" :

    str = "geeksforgeeks"

    # convert string into list of characters
    str = list(str)

    # Function calling
    manipulateString(str)

# This code is contributed by ANKITRAI1
```

## **C#**

```

// C# program for Replace every character of a
// string by a different character
using System;
public class GFG {

    //Function to manipulate the string
    static void manipulateString(String str)
    {

        char[] str1 = str.ToCharArray();

     // looping through each character of string
     for (int i = 0; i < str.Length; i++) {

         // storing integer ASCII value of
         // the character in 'asc'

         int asc = str1[i];

         // 'rem' contains coded value which
         // needs to be rounded to 26
         int rem = asc - (26 - (str1[i] - 97));

         // converting 'rem' character in range
         // 0-25 and storing in 'm'
         int m = rem % 26;

         // printing character by adding ascii value of 'a'
         // so that it becomes in the desired range i.e. a-z
         str1[i] = (char)(m + 'a');

     }

     String str2 = String.Join("",str1);
     Console.WriteLine(str2);

    }

    //Driver code
    public static void Main() {

        // Declaring str as 'geeksforgeeks'
         String str = "geeksforgeeks";
         manipulateString(str);

    }
}
// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// Javascript program for Replace every character of a
// string by a different character

// Function to manipulate the string
function manipulateString(str)
{

    // looping through each character of string
    for (var i = 0; i < str.length; i++) {

        // storing integer ASCII value of
        // the character in 'asc'
        var asc = str[i];

        // 'rem' contains coded value which
        // needs to be rounded to 26
        var rem = asc.charCodeAt(0) - (26 - (str[i].charCodeAt(0) - 'a'.charCodeAt(0)));

        // converting 'rem' character in range
        // 0-25 and storing in 'm'
        var m = (rem % 26);

        // printing character by adding ascii value of 'a'
        // so that it becomes in the desired range i.e. a-z
        str[i] = String.fromCharCode(m + 'a'.charCodeAt(0));
    }
    return str;
}

// Driver code
// Declaring str as 'geeksforgeeks'
var str = "geeksforgeeks";
document.write(manipulateString(str.split('')).join(''));

</script>
```

****Output:** 

```
fbbnddvbfbbnd
```**