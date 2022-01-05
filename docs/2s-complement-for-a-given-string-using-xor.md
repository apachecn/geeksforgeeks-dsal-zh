# 使用异或运算对给定字符串进行 2 的补码

> 原文:[https://www . geesforgeks . org/2s-给定字符串的补码使用-xor/](https://www.geeksforgeeks.org/2s-complement-for-a-given-string-using-xor/)

给定一个二进制字符串，任务是在异或运算符的帮助下将该字符串转换为二进制补码。

**示例:**

```
Input : 00000101
Output :11111011

Input : 10010
Output : 01110
```

我们在上一篇文章中讨论了一种方法来[寻找 2 的补码](https://www.geeksforgeeks.org/efficient-method-2s-complement-binary-string/)

对于 2 的补码，我们首先找到 1 的补码。我们从最低有效位开始遍历 1 的补码，寻找 0。我们翻转所有 1(变为 0)，直到找到 0。最后，我们翻转找到的 0。

我们从最后一个机器人开始遍历，一直忽略所有 0，直到找到 1。我们先忽略 1 也。然后，我们通过与 1 进行异或来切换所有位。

## C++

```
// C++ program to find 2's complement using XOR.
#include <bits/stdc++.h>
using namespace std;

string TwoscomplementbyXOR(string str)
{
    int n = str.length();

    // A flag used to find if a 1 bit is seen
    // or not.
    bool check_bit = 0;

    for (int i = n - 1; i >= 0; i--) {
        if (str[i] == '0' && check_bit == 0) {
            continue;
        }
        else {

            // xor operator is used to flip the  
            if (check_bit == 1)
                str[i] = (str[i] - '0') ^ 1 + '0'; 

            // bits after converting in to
            // ASCII values
            check_bit = 1;
        }
    }

    // if there is no 1 in the string so just add 
    // 1 in starting of string and return
    if (check_bit == 0) 
        return "1" + str; 
    else
        return str;
}

// Driver code
int main()
{
    string str = "101";
    cout << TwoscomplementbyXOR(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 2's complement using XOR.
import java.util.*; 

class GFG{

static void TwoscomplementbyXOR(String str)
{
    int n = str.length();

    // A flag used to find if a 1 bit is seen
    // or not.
    boolean check_bit = false;

    for(int i = n - 1; i >= 0; i--)
    {
        if (str.charAt(i) == '0' && 
            check_bit == false)
        {
            continue;
        }
        else
        {

            // xor operator is used to flip the  
            if (check_bit == true)
            {
                if (str.charAt(i) == '0')
                    str = str.substring(0, i) + '1' +
                          str.substring(i + 1);
                else
                     str = str.substring(0, i) + '0' +
                           str.substring(i + 1);
            }

            // bits after converting in to
            // ASCII values
            check_bit = true;
        }
    }

    // If there is no 1 in the string so just add 
    // 1 in starting of string and return
    if (check_bit == false)
    {
        System.out.println("1" + str); 
    } 
    else
        System.out.println(str);
}

// Driver code
public static void main(String[] args) 
{ 
    String str = "101";

    TwoscomplementbyXOR(str);
}
}

// This code is contributed by amreshkumar3
```

## 蟒蛇 3

```
# Python program to find 2's complement using XOR.
def TwoscomplementbyXOR(str):
    n = len(str)

    # A flag used to find if a 1 bit is seen
    # or not.
    check_bit = 0
    i = n - 1
    s = list(str)
    while (i >= 0):
        if (s[i] == '0' and check_bit == 0):
            continue
        else:

            # xor operator is used to flip the
            if (check_bit == 1):
                s[i] = chr((ord(s[i]) - 48) ^ 1 + 48)

            # bits after converting in to
            # ASCII values
            check_bit = 1
        i -= 1

    # if there is no 1 in the string so just add
    # 1 in starting of string and return
    str = "".join(s)
    if (check_bit == 0):
        return "1" + str
    else:
        return str

# Driver code
str = "101"
print(TwoscomplementbyXOR(str))

# This code is contributed by subhammahato348.
```

## C#

```
// C# program to find 2's complement using XOR.
using System;
class GFG {

  static void TwoscomplementbyXOR(string str)
  {
    int n = str.Length;

    // A flag used to find if a 1 bit is seen
    // or not.
    bool check_bit = false;
    for(int i = n - 1; i >= 0; i--)
    {
      if (str[i] == '0' && 
          check_bit == false)
      {
        continue;
      }
      else
      {

        // xor operator is used to flip the  
        if (check_bit == true)
        {
          if (str[i] == '0')
            str = str.Substring(0, i) + '1' +
            str.Substring(i + 1);
          else
            str = str.Substring(0, i) + '0' +
            str.Substring(i + 1);
        }

        // bits after converting in to
        // ASCII values
        check_bit = true;
      }
    }

    // If there is no 1 in the string so just add 
    // 1 in starting of string and return
    if (check_bit == false)
    {
      Console.WriteLine("1" + str); 
    } 
    else
      Console.WriteLine(str);
  }

  // Driver code
  static void Main() {
    string str = "101";

    TwoscomplementbyXOR(str);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 2's complement 
// using XOR. 

function TwoscomplementbyXOR($str) 
{ 
    $n =strlen($str); 

    // A flag used to find if a 1 
    // bit is seen or not. 
    $check_bit = 0; 

    for ($i = $n - 1; $i >= 0; $i--)
    { 
        if ($str[$i] == '0' && 
            $check_bit == 0) 
        { 
            continue; 
        } 
        else
        { 

            // xor operator is used
            // to flip the 
            if ($check_bit == 1) 
                $str[$i] = ($str[$i] - '0') ^ 1 + '0'; 

            // bits after converting in to 
            // ASCII values 
            $check_bit = 1; 
        } 
    } 

    // if there is no 1 in the string 
    // so just add 1 in starting of 
    // string and return 
    if ($check_bit == 0) 
        return "1" + $str; 
    else
        return $str; 
} 

// Driver code 
$str = "101"; 
echo TwoscomplementbyXOR($str); 

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// Javascript program to find 2's complement 
// using XOR. 

function TwoscomplementbyXOR(str) {
    let n = str.length;

    // A flag used to find if a 1 
    // bit is seen or not. 
    let check_bit = 0;

    for (let i = n - 1; i >= 0; i--) {
        if (str[i] == '0' && check_bit == 0) {
            continue;
        }
        else {

            // xor operator is used
            // to flip the 
            if (check_bit == 1) {
                if (str.charAt(i) == '0')
                    str = str.substr(0, i) + '1' + str.substr(i + 1);
                else
                    str = str.substr(0, i) + '0' + str.substr(i + 1);
            }

            // bits after converting in to 
            // ASCII values 
            check_bit = 1;
        }
    }

    // if there is no 1 in the string 
    // so just add 1 in starting of 
    // string and return 
    if (check_bit == 0)
        return "1" + str;
    else
        return str;
}

// Driver code 
let str = "101";
document.write(TwoscomplementbyXOR(str));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
011
```