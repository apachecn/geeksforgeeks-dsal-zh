# 检查输入是整数还是字符串的程序

> 原文:[https://www . geesforgeks . org/program-check-input-integer-string/](https://www.geeksforgeeks.org/program-check-input-integer-string/)

编写一个函数来检查给定的输入是整数还是字符串。

**整数的定义:**

```
Every element should be a valid digit, i.e '0-9'.
```

**字符串的定义:**

```
Any one element should be an invalid digit, i.e any symbol other than '0-9'.
```

**示例:**

```
Input : 127
Output : Integer
Explanation : All digits are in the range '0-9'.

Input : 199.7
Output : String
Explanation : A dot is present. 

Input : 122B
Output : String
Explanation : A alphabet is present.
```

想法是使用[是 digit()函数，](https://www.geeksforgeeks.org/isalpha-isdigit-functions-c-example/)是 T2 _ numeric()函数..

以下是上述想法的实现。

## C++

```
// CPP program to check if a given string
// is a valid integer
#include <iostream>
using namespace std;

// Returns true if s is a number else false
bool isNumber(string s)
{
    for (int i = 0; i < s.length(); i++)
        if (isdigit(s[i]) == false)
            return false;

    return true;
}

// Driver code
int main()
{
    // Saving the input in a string
    string str = "6790";

    // Function returns 1 if all elements
    // are in range '0-9'
    if (isNumber(str))
        cout << "Integer";

    // Function returns 0 if the input is
    // not an integer
    else
        cout << "String";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// string is a valid integer
import java.io.*;

public class GFG {

    // Returns true if s is
    // a number else false
    static boolean isNumber(String s)
    {
        for (int i = 0; i < s.length(); i++)
            if (Character.isDigit(s.charAt(i)) == false)
                return false;

        return true;
    }

    // Driver code
    static public void main(String[] args)
    {
        // Saving the input in a string
        String str = "6790";

        // Function returns 1 if all elements
        // are in range '0 - 9'
        if (isNumber(str))
            System.out.println("Integer");

        // Function returns 0 if the
        // input is not an integer
        else
            System.out.println("String");
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to check if a given string
# is a valid integer

# This function Returns true if
# s is a number else false
def isNumber(s):

    for i in range(len(s)):
        if s[i].isdigit() != True:
            return False

    return True

# Driver code
if __name__ == "__main__":

    # Store the input in a str variable
    str = "6790"

    # Function Call
    if isNumber(str):
        print("Integer")

    else:
        print("String")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to check if a given
// string is a valid integer
using System;

public class GFG {

    // Returns true if s is a
    // number else false
    static bool isNumber(string s)
    {
        for (int i = 0; i < s.Length; i++)
            if (char.IsDigit(s[i]) == false)
                return false;

        return true;
    }

    // Driver code
    static public void Main(String[] args)
    {

        // Saving the input in a string
        string str = "6790";

        // Function returns 1 if all elements
        // are in range '0 - 9'
        if (isNumber(str))
            Console.WriteLine("Integer");

        // Function returns 0 if the
        // input is not an integer
        else
            Console.WriteLine("String");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// given string is a valid integer

// Returns true if s
// is a number else false
function isNumber($s)
{
    for ($i = 0; $i < strlen($s); $i++)
        if (is_numeric($s[$i]) == false)
            return false;

    return true;
}

// Driver code

// Saving the input
// in a string
$str = "6790";

// Function returns
// 1 if all elements
// are in range '0-9'
if (isNumber($str))
    echo "Integer";
else
    echo "String";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if a given
    // string is a valid integer

    // Returns true if s is a
    // number else false
    function isNumber(s)
    {
        for (let i = 0; i < s.length; i++)
            if (s[i] < '0' || s[i] > '9')
                return false;

        return true;
    }

    // Saving the input in a string
    let str = "6790";

    // Function returns 1 if all elements
    // are in range '0 - 9'
    if (isNumber(str))
      document.write("Integer");

    // Function returns 0 if the
    // input is not an integer
    else
      document.write("String");

</script>
```

**Output**

```
Integer
```

**使用特殊 Python 内置 type()函数:**

type()是 python 提供的内置函数。type()以 object 为参数，并按其名称返回其类类型。

下面是上述想法的实现:

## 蟒蛇 3

```
# Python program to find
# whether the user input
# is int or string type

# Function to determine whether
# the user input is string or
# integer type
def isNumber(x):
    if type(x) == int:
         return True
    else:
         return False

# Driver Code
input1 = 122
input2 = '122'

# Function Call

# for input1
if isNumber(input1):
    print("Integer")
else:
    print("String")

# for input2
if isNumber(input2):
    print("Integer")
else:
    print("String")
```

**Output**

```
Integer
String
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。