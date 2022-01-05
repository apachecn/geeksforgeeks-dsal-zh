# 根据给定模式生成所有二进制字符串

> 原文:[https://www . geesforgeks . org/generate-all-binary-strings-from-给定-pattern/](https://www.geeksforgeeks.org/generate-all-binary-strings-from-given-pattern/)

给定包含“0”、“1”和“？”的字符串通配符，生成可以通过用“0”或“1”替换每个通配符而形成的所有二进制字符串。
**例:**

```
Input str = "1??0?101"
Output: 
        10000101
        10001101
        10100101
        10101101
        11000101
        11001101
        11100101
        11101101
```

**方法 1(使用递归)**
我们将下一个字符的索引传递给递归函数。如果当前字符是通配符“？”，我们将其替换为“0”或“1 ”,并递归查找剩余的字符。如果我们到达绳子的末端，我们就把它打印出来。
下面是递归的实现。

## C++

```
// Recursive C++ program to generate all binary strings
// formed by replacing each wildcard character by 0 or 1
#include <iostream>
using namespace std;

// Recursive function to generate all binary strings
// formed by replacing each wildcard character by 0 or 1
void print(string str, int index)
{
    if (index == str.size())
    {
        cout << str << endl;
        return;
    }

    if (str[index] == '?')
    {
        // replace '?' by '0' and recurse
        str[index] = '0';
        print(str, index + 1);

        // replace '?' by '1' and recurse
        str[index] = '1';
        print(str, index + 1);

        // No need to backtrack as string is passed
        // by value to the function
    }
    else
        print(str, index + 1);
}

// Driver code to test above function
int main()
{
    string str = "1??0?101";

    print(str, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to generate all
// binary strings formed by replacing
// each wildcard character by 0 or 1
import java.util.*;
import java.lang.*;
import java.io.*;

class binStr
{  
    // Recursive function to generate all binary
    // strings formed by replacing each wildcard
    // character by 0 or 1
    public static void print(char str[], int index)
    {
        if (index == str.length)
        {
            System.out.println(str);
            return;
        }

        if (str[index] == '?')
        {
            // replace '?' by '0' and recurse
            str[index] = '0';
            print(str, index + 1);

            // replace '?' by '1' and recurse
            str[index] = '1';
            print(str, index + 1);

            // NOTE: Need to backtrack as string
            // is passed by reference to the
            // function
            str[index] = '?';
        }
        else
            print(str, index + 1);
    }

    // driver code
    public static void main (String[] args)
    {
        String input = "1??0?101";
        char[] str = input.toCharArray();
        print(str, 0);
    }
}

// This code is contributed by Chhavi
```

## 蟒蛇 3

```
# Recursive Python program to generate all
# binary strings formed by replacing
# each wildcard character by 0 or 1

# Recursive function to generate all binary
# strings formed by replacing each wildcard
# character by 0 or 1
def _print(string, index):
    if index == len(string):
        print(''.join(string))
        return

    if string[index] == "?":

        # replace '?' by '0' and recurse
        string[index] = '0'
        _print(string, index + 1)

        # replace '?' by '1' and recurse
        string[index] = '1'
        _print(string, index + 1)

        # NOTE: Need to backtrack as string
        # is passed by reference to the
        # function
        string[index] = '?'
    else:
        _print(string, index + 1)

# Driver code
if __name__ == "__main__":

    string = "1??0?101"
    string = list(string)
    _print(string, 0)

    # This code is contributed by
    # sanjeev2552

# Note: function name _print is used because
# print is already a predefined function in Python
```

## C#

```
// Recursive C# program to generate all
// binary strings formed by replacing
// each wildcard character by 0 or 1
using System;

class GFG
{
    // Recursive function to generate
    // all binary strings formed by
    // replacing each wildcard character
    // by 0 or 1
    public static void print(char []str,
                             int index)
    {
        if (index == str.Length)
        {
            Console.WriteLine(str);
            return;
        }

        if (str[index] == '?')
        {
            // replace '?' by
            // '0' and recurse
            str[index] = '0';
            print(str, index + 1);

            // replace '?' by
            // '1' and recurse
            str[index] = '1';
            print(str, index + 1);

            // NOTE: Need to backtrack
            // as string is passed by
            // reference to the function
            str[index] = '?';
        }
        else
            print(str, index + 1);
    }

    // Driver Code
    public static void Main ()
    {
        string input = "1??0?101";
        char []str = input.ToCharArray();
        print(str, 0);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to generate all binary strings
// formed by replacing each wildcard character by 0 or 1

// Recursive function to generate all binary strings
// formed by replacing each wildcard character by 0 or 1
function print1($str, $index)
{
    if ($index == strlen($str))
    {
        echo $str."\n";
        return;
    }

    if ($str[$index] == '?')
    {
        // replace '?' by '0' and recurse
        $str[$index] = '0';
        print1($str, $index + 1);

        // replace '?' by '1' and recurse
        $str[$index] = '1';
        print1($str, $index + 1);

        // No need to backtrack as string is passed
        // by value to the function
    }
    else
        print1($str, $index + 1);
}

// Driver code

    $str = "1??0?101";

    print1($str, 0);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

      // Recursive JavaScript program to generate all
      // binary strings formed by replacing
      // each wildcard character by 0 or 1

      // Recursive function to generate
      // all binary strings formed by
      // replacing each wildcard character
      // by 0 or 1
      function print(str, index) {
        if (index === str.length) {
          document.write(str.join("") + "<br>");
          return;
        }

        if (str[index] === "?") {
          // replace '?' by
          // '0' and recurse
          str[index] = "0";
          print(str, index + 1);

          // replace '?' by
          // '1' and recurse
          str[index] = "1";
          print(str, index + 1);

          // NOTE: Need to backtrack
          // as string is passed by
          // reference to the function
          str[index] = "?";
        } else print(str, index + 1);
      }

      // Driver Code

      var input = "1??0?101";
      var str = input.split("");
      print(str, 0);

</script>
```

**Output:** 

```
10000101
10001101
10100101
10101101
11000101
11001101
11100101
11101101
```