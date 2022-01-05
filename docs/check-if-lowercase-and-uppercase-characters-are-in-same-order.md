# 检查小写和大写字符的顺序是否相同

> 原文:[https://www . geesforgeks . org/check-如果小写和大写字符的顺序相同/](https://www.geeksforgeeks.org/check-if-lowercase-and-uppercase-characters-are-in-same-order/)

给定一个只包含小写字母和大写字母的字符串。任务是检查小写字符和大写字符是否分别遵循相同的顺序。
**注意:**如果一个字符在小写中出现不止一次，那么同一字符在大写中出现的次数应该是相同的。
**例:**

```
Input: str = "geeGkEEsKS"
Output: Yes
Lowercase = geeks, Uppercase = GEEKS

Input: str = "GeEkKg"
Output: No
Lowercase = ekg, Uppercase = GEK
```

**进场:**

1.  遍历字符串。
2.  将小写字母和大写字母分别存储在两个单独的字符串中*下部*和*上部*。
3.  将小写字符串转换为大写。
4.  检查两个大写字符串是否相等。
5.  如果相等，则打印是，否则打印否

以下是上述方法的实现:

## C++

```
// C++ program to check if lowercase and
// uppercase characters are in same order
#include <bits/stdc++.h>
using namespace std;

// Function to check if both the
// case follow the same order
bool isCheck(string str)
{

    int len = str.length();
    string lowerStr = "", upperStr = "";

    // Traverse the string
    for (int i = 0; i < len; i++) {

        // Store both lowercase and uppercase
        // in two different strings
        if (str[i] >= 65 && str[i] <= 91)
            upperStr = upperStr + str[i];

        else
            lowerStr = lowerStr + str[i];
    }

    // using transform() function and ::toupper in STL
    transform(lowerStr.begin(), lowerStr.end(),
              lowerStr.begin(), ::toupper);

    return lowerStr == upperStr;
}

// Driver code
int main()
{
    string str = "geeGkEEsKS";

    isCheck(str) ? cout << "Yes"
                 : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to check if lowercase and
// uppercase characters are in same order

public class GFG {

    //Function to check if both the
    //case follow the same order
    static boolean isCheck(String str)
    {

     int len = str.length();
     String lowerStr = "", upperStr = "";

     char[] str1 = str.toCharArray();
     // Traverse the string
     for (int i = 0; i < len; i++) {

         // Store both lowercase and uppercase
         // in two different strings

         if ((int)(str1[i]) >= 65 && (int)str1[i] <= 91)
             upperStr = upperStr + str1[i];

         else
             lowerStr = lowerStr + str1[i];
     }

     // transform lowerStr1 to upper
     String transformStr = lowerStr.toUpperCase();

     return(transformStr.equals(upperStr));

    }

    //Driver code
    public static void main(String[] args) {

        String str = "geeGkEEsKS";

        if (isCheck(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to Check if lowercase and
# uppercase characters are in same order

# Function to check if both the
# case follow the same order
def isCheck(str) :

    length = len(str)
    lowerStr, upperStr = "", ""

    # Traverse the string
    for i in range(length) :

        # Store both lowercase and
        # uppercase in two different
        # strings
        if (ord(str[i]) >= 65 and
            ord(str[i]) <= 91) :
            upperStr = upperStr + str[i]

        else :
            lowerStr = lowerStr + str[i]

    # transfor lowerStr to uppercase
    transformStr = lowerStr.upper()

    return transformStr == upperStr

# Driver Code
if __name__ == "__main__" :

    str = "geeGkEEsKS"

    if isCheck(str) :
        print("Yes")
    else :
        print("No")

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to check if lowercase and
// uppercase characters are in same order
using System;

class GFG {

    //Function to check if both the
    //case follow the same order
    static bool isCheck(string str)
    {

    int len = str.Length;
    string lowerStr = "", upperStr = "";

    char[] str1 = str.ToCharArray();
    // Traverse the string
    for (int i = 0; i < len; i++) {

        // Store both lowercase and uppercase
        // in two different strings

        if ((int)(str1[i]) >= 65 && (int)str1[i] <= 91)
            upperStr = upperStr + str1[i];

        else
            lowerStr = lowerStr + str1[i];
    }

    // transform lowerStr1 to upper
    String transformStr = lowerStr.ToUpper();

    return(transformStr.Equals(upperStr));

    }

    //Driver code
    public static void Main(String[] args) {

        String str = "geeGkEEsKS";

        if (isCheck(str))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}
```

## java 描述语言

```
<script>

// Javascript program to check if lowercase and
// uppercase characters are in same order

// Function to check if both the
// case follow the same order
function isCheck(str)
{

    var len = str.length;
    var lowerStr = "", upperStr = "";

    // Traverse the string
    for (var i = 0; i < len; i++) {

        // Store both lowercase and uppercase
        // in two different strings
        if (str[i] >= 'A' && str[i] < 'a')
            upperStr = upperStr + str[i];

        else
            lowerStr = lowerStr + str[i];
    }

    lowerStr = lowerStr.toUpperCase();
    console.log(lowerStr);
    return lowerStr === upperStr;
}

// Driver code
var str = "geeGkEEsKS";
isCheck(str) ? document.write( "Yes")
             : document.write( "No");

</script>
```

**Output:** 

```
Yes
```