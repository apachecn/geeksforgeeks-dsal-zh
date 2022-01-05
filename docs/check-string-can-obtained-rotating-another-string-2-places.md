# 检查将另一根弦旋转 2 个位置是否可以得到一根弦

> 原文:[https://www . geesforgeks . org/check-string-can-get-rotating-other-string-2-places/](https://www.geeksforgeeks.org/check-string-can-obtained-rotating-another-string-2-places/)

给定两个字符串，任务是找出一个字符串是否可以通过将另一个字符串旋转两个位置来获得。

**示例:**

> **输入**:string 1 =“Amazon”，string 2 =“azonam”
> **输出:**是
> //逆时针旋转
> **输入**:string 1 =“Amazon”，string 2 =“onamaz”
> **输出**:是
> //顺时针旋转

**在**问:[亚马逊采访](https://www.geeksforgeeks.org/amazons-asked-interview-questions/)

```
1- There can be only two cases:
    a) Clockwise rotated
    b) Anti-clockwise rotated

2- If clockwise rotated that means elements
   are shifted in right.
   So, check if a substring[2.... len-1] of 
   string2 when concatenated with substring[0,1]
   of string2 is equal to string1\. Then, return true.

3- Else, check if it is rotated anti-clockwise 
   that means elements are shifted to left.
   So, check if concatenation of substring[len-2, len-1]
   with substring[0....len-3] makes it equals to
   string1\. Then return true.

4- Else, return false.
```

下面是上述方法的实现。

## C++

```
// C++ program to check if a string is two time
// rotation of another string.
#include<bits/stdc++.h>
using namespace std;

// Function to check if string2 is obtained by
// string 1
bool isRotated(string str1, string str2)
{
    if (str1.length() != str2.length())
        return false;
    if(str1.length()<2){
      return str1.compare(str2) == 0;
    }
    string clock_rot = "";
    string anticlock_rot = "";
    int len = str2.length();

    // Initialize string as anti-clockwise rotation
    anticlock_rot = anticlock_rot +
                    str2.substr(len-2, 2) +
                    str2.substr(0, len-2) ;

    // Initialize string as clock wise rotation
    clock_rot = clock_rot +
                str2.substr(2) +
                str2.substr(0, 2) ;

    // check if any of them is equal to string1
    return (str1.compare(clock_rot) == 0 ||
            str1.compare(anticlock_rot) == 0);
}

// Driver code
int main()
{
    string str1 = "geeks";
    string str2 = "eksge";

    isRotated(str1, str2) ? cout << "Yes"
                          : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string is two time
// rotation of another string.

class Test
{
    // Method to check if string2 is obtained by
    // string 1
    static boolean isRotated(String str1, String str2)
    {
        if (str1.length() != str2.length())
            return false;
        if(str1.length() < 2)
        {
            return str1.equals(str2);
        }

        String clock_rot = "";
        String anticlock_rot = "";
        int len = str2.length();

        // Initialize string as anti-clockwise rotation
        anticlock_rot = anticlock_rot +
                        str2.substring(len-2, len) +
                        str2.substring(0, len-2) ;

        // Initialize string as clock wise rotation
        clock_rot = clock_rot +
                    str2.substring(2) +
                    str2.substring(0, 2) ;

        // check if any of them is equal to string1
        return (str1.equals(clock_rot) ||
                str1.equals(anticlock_rot));
    }

    // Driver method
    public static void main(String[] args)
    {
        String str1 = "geeks";
        String str2 = "eksge";

        System.out.println(isRotated(str1, str2) ?  "Yes"
                              : "No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check if a string
# is two time rotation of another string.

# Function to check if string2 is
# obtained by string 1
def isRotated(str1, str2):

    if (len(str1) != len(str2)):
        return False

    if(len(str1) < 2):
        return str1 == str2
    clock_rot = ""
    anticlock_rot = ""
    l = len(str2)

    # Initialize string as anti-clockwise rotation
    anticlock_rot = (anticlock_rot + str2[l - 2:] +
                                     str2[0: l - 2])

    # Initialize string as clock wise rotation
    clock_rot = clock_rot + str2[2:] + str2[0:2]

    # check if any of them is equal to string1
    return (str1 == clock_rot or
            str1 == anticlock_rot)

# Driver code
if __name__ == "__main__":

    str1 = "geeks"
    str2 = "eksge"
if isRotated(str1, str2):
    print("Yes") 
else:
    print("No")

# This code is contributed by ita_c
```

## C#

```
using System;

// C# program to check if a string is two time
// rotation of another string.

public class Test {
    // Method to check if string2 is obtained by
    // string 1
    public static bool isRotated(string str1, string str2)
    {
        if (str1.Length != str2.Length) {
            return false;
        }

        if (str1.Length < 2) {
            return str1.Equals(str2);
        }

        string clock_rot = "";
        string anticlock_rot = "";
        int len = str2.Length;

        // Initialize string as anti-clockwise rotation
        anticlock_rot
            = anticlock_rot
              + str2.Substring(len - 2, len - (len - 2))
              + str2.Substring(0, len - 2);

        // Initialize string as clock wise rotation
        clock_rot = clock_rot + str2.Substring(2)
                    + str2.Substring(0, 2);

        // check if any of them is equal to string1
        return (str1.Equals(clock_rot)
                || str1.Equals(anticlock_rot));
    }

    // Driver code
    public static void Main(string[] args)
    {
        string str1 = "geeks";
        string str2 = "eksge";

        Console.WriteLine(isRotated(str1, str2) ? "Yes"
                                                : "No");
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to check if a
// string is two time rotation of
// another string.

// Method to check if string2 is
// obtained by string 1
function isRotated(str1, str2)
{
    if (str1.length != str2.length)
        return false;

    if (str1.length < 2)
    {
        return str1.localeCompare(str2);
    }

    let clock_rot = "";
    let anticlock_rot = "";
    let len = str2.length;

    // Initialize string as anti-clockwise rotation
    anticlock_rot = anticlock_rot +
                    str2.substring(len - 2, len + 1) +
                    str2.substring(0, len - 1) ;

    // Initialize string as clock wise rotation
    clock_rot = clock_rot +
                str2.substring(2, str2.length - 2 + 1) +
                str2.substring(0, 2 + 1);

    // Check if any of them is equal to string1
    return (str1.localeCompare(clock_rot) ||
            str1.localeCompare(anticlock_rot));
}

// Driver code
let str1 = "geeks";
let str2 = "eksge";

document.write(isRotated(str1, str2) ? 
               "Yes" : "No");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Yes
```

练习:检查 string2 是否是通过将 string1 旋转 k 位获得的。

参考:[https://www.careercup.com/question?id=5734821229756416](https://www.careercup.com/question?id=5734821229756416)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。