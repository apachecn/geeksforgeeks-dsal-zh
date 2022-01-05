# 将给定字符串转换为有效的手机号码

> 原文:[https://www . geesforgeks . org/convert-given-string-to-valid-mobile-number/](https://www.geeksforgeeks.org/convert-given-string-to-a-valid-mobile-number/)

给定一个由字母、数字和符号组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **M** ，任务是通过删除除数字以外的所有字符，将该字符串转换为有效的手机号码，格式如下:

*   形成一个 **3** 位的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)，剩余串的长度大于 **3** 。
*   每个子串用括号**“()”**括起来，用**“-”**隔开。

如果无法获得有效的手机号码，即字符串不是由 10 位数字组成，则打印 **-1** 。否则，打印获得的字符串。

**示例:**

> **输入:**M =“91 234 rt5 % 34 * 0 3”
> T3】输出:“(912)-(345)-(340)-(3)”
> **说明:**去掉所有多余字符后，M =“9123453403”。因此，最终得到的字符串是“(912)-(345)-(340)-(3)”。
> 
> **输入:**M =【9 9 ry7 % 64 9 7】
> T3】输出:【无效】
> **说明:**去掉多余字符后 M =【9976497】。由于字符串的长度不等于 10，因此所需的输出为-1。

**方法:**按照以下步骤解决问题:

*   初始化一个字符串，说 **S** 并按照给定的顺序追加 **S** 中 **M** 的所有数字。
*   现在如果 **S** 的长度不是 **10** ，打印**“无效”**，结束程序。
*   否则，如果字符串 **S** 的[长度为 **10** ，则制作一组 **3** 字符，并将其括在括号**“()”**内，并与**“-”**分开。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)
*   将最终字符串打印为 **S** 。

以下是上述问题的解决方案。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the valid
// and formatted phone number
void Validate(string M)
{
    // Length of given string
    int len = M.size();

    // Store digits in temp
    string temp = "";

    // Iterate given M
    for (int i = 0; i < len; i++) {
        // If any digit, append it to temp
        if (isdigit(M[i]))
            temp += M[i];
    }

    // Find new length of string
    int nwlen = temp.size();

    // If length is not equal to 10
    if (nwlen != 10) {
        cout << "Invalid\n";
        return;
    }

    // Store final result
    string res = "";

    // Make groups of 3 digits and
    // enclose them within () and
    // separate them with "-"
    // 0 to 2 index 1st group
    string x = temp.substr(0, 3);
    res += "(" + x + ")-";

    // 3 to 5 index 2nd group
    x = temp.substr(3, 3);
    res += "(" + x + ")-";

    // 6 to 8 index 3rd group
    x = temp.substr(6, 3);
    res += "(" + x + ")-";

    // 9 to 9 index last group
    x = temp.substr(9, 1);
    res += "(" + x + ")";

    // Print final result
    cout << res << "\n";
}

// Driver Code
int main()
{

    // Given string
    string M = "91 234rt5%34*0 3";

    // Function Call
    Validate(M);
}

// contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to print the valid
// and formatted phone number
static void Validate(String M)
{

    // Length of given String
    int len = M.length();

    // Store digits in temp
    String temp = "";

    // Iterate given M
    for (int i = 0; i < len; i++)
    {

        // If any digit, append it to temp
        if (Character.isDigit(M.charAt(i)))
            temp += M.charAt(i);
    }

    // Find new length of String
    int nwlen = temp.length();

    // If length is not equal to 10
    if (nwlen != 10)
    {
        System.out.print("Invalid\n");
        return;
    }

    // Store final result
    String res = "";

    // Make groups of 3 digits and
    // enclose them within () and
    // separate them with "-"
    // 0 to 2 index 1st group
    String x = temp.substring(0, 3);
    res += "(" + x + ")-";

    // 3 to 5 index 2nd group
    x = temp.substring(3, 6);
    res += "(" + x + ")-";

    // 6 to 8 index 3rd group
    x = temp.substring(6, 9);
    res += "(" + x + ")-";

    // 9 to 9 index last group
    x = temp.substring(9, 10);
    res += "(" + x + ")";

    // Print final result
    System.out.print(res+ "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String M = "91 234rt5%34*0 3";

    // Function Call
    Validate(M);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print valid
# and formatted phone number
def Validate(M):

    # Length of given
    lenn = len(M)

    # Store digits in temp
    temp = ""

    # Iterate given M
    for i in range(lenn):

        # If any digit:append it to temp
        if (M[i].isdigit()):
            temp += M[i]

    # Find new length of
    nwlenn = len(temp)

    # If length is not equal to 10
    if (nwlenn != 10):
        print ("Invalid")
        return

    # Store final result
    res = ""

    # Make groups of 3 digits and
    # enclose them within () and
    # separate them with "-"
    # 0 to 2 index 1st group
    x = temp[0:3]
    res += "(" + x + ")-"

    # 3 to 5 index 2nd group
    x = temp[3 : 3 + 3]
    res += "(" + x + ")-"

    # 6 to 8 index 3rd group
    x = temp[6 : 3 + 6]
    res += "(" + x + ")-"

    # 9 to 9 index last group
    x = temp[9 : 1 + 9]
    res += "(" + x + ")"

    # Print final result
    print(res)

# Driver Code
if __name__ == '__main__':

    # Given
    M = "91 234rt5%34*0 3"

    # Function Call
    Validate(M)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to print the valid
  // and formatted phone number
  static void Validate(string M)
  {

    // Length of given String
    int len = M.Length;

    // Store digits in temp
    string temp = "";

    // Iterate given M
    for (int i = 0; i < len; i++)
    {

      // If any digit, append it to temp
      if (Char.IsDigit(M[i]))
        temp += M[i];
    }

    // Find new length of String
    int nwlen = temp.Length;

    // If length is not equal to 10
    if (nwlen != 10)
    {
      Console.Write("Invalid\n");
      return;
    }

    // Store final result
    string res = "";

    // Make groups of 3 digits and
    // enclose them within () and
    // separate them with "-"
    // 0 to 2 index 1st group
    string x = temp.Substring(0, 3);
    res += "(" + x + ")-";

    // 3 to 5 index 2nd group
    x = temp.Substring(3, 3);
    res += "(" + x + ")-";

    // 6 to 8 index 3rd group
    x = temp.Substring(6, 3);
    res += "(" + x + ")-";

    // 9 to 9 index last group
    x = temp.Substring(9, 1);
    res += "(" + x + ")";

    // Print final result
    Console.WriteLine(res);
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given String
    string M = "91 234rt5%34*0 3";

    // Function Call
    Validate(M);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the valid
// and formatted phone number
function Validate(M)
{
    // Length of given String
    let len = M.length;

    // Store digits in temp
    let temp = "";

    // Iterate given M
    for (let i = 0; i < len; i++)
    {

        // If any digit, append it to temp
        if (! isNaN( parseInt(M[i]) ))
            temp += M[i];
    }

    // Find new length of String
    let nwlen = temp.length;

    // If length is not equal to 10
    if (nwlen != 10)
    {
        document.write("Invalid<br>");
        return;
    }

    // Store final result
    let res = "";

    // Make groups of 3 digits and
    // enclose them within () and
    // separate them with "-"
    // 0 to 2 index 1st group
    let x = temp.substring(0, 3);
    res += "(" + x + ")-";

    // 3 to 5 index 2nd group
    x = temp.substring(3, 6);
    res += "(" + x + ")-";

    // 6 to 8 index 3rd group
    x = temp.substring(6, 9);
    res += "(" + x + ")-";

    // 9 to 9 index last group
    x = temp.substring(9, 10);
    res += "(" + x + ")";

    // Print final result
    document.write(res+ "<br>");
}

// Driver Code
// Given String
let M = "91 234rt5%34*0 3";
// Function Call
Validate(M);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
(912)-(345)-(340)-(3)
```

***时间复杂度:** O(|M|+|S|)*
***辅助空间:** O(|M|+|S|)*