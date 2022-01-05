# 检查密码强度的程序

> 原文:[https://www . geesforgeks . org/program-check-strength-password/](https://www.geeksforgeeks.org/program-check-strength-password/)

如果密码满足以下条件，则称其为**强**:

1.  它至少包含一个小写英文字符。
2.  它至少包含一个大写英文字符。
3.  它至少包含一个特殊字符。特殊字符为:**！@#$%^ & *()-+**
4.  它的长度至少是 8。
5.  它至少包含一个数字。

给定一根弦，找到它的力量。让强密码满足以上所有条件。中等密码满足前三个条件，长度至少为 6。否则密码为周。

**示例:**

> **输入:**“geeks forgeeks！@ 12 "
> T3】输出:强
> 
> **输入:**“gfg！@ 12 "
> T3】输出:中等

## C++

```
// C++ program to check if a given password is
// strong or not.
#include <bits/stdc++.h>
using namespace std;

void printStrongNess(string& input)
{
    int n = input.length();

    // Checking lower alphabet in string
    bool hasLower = false, hasUpper = false;
    bool hasDigit = false, specialChar = false;
    string normalChars = "abcdefghijklmnopqrstu"
        "vwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890 ";

    for (int i = 0; i < n; i++) {
        if (islower(input[i]))
            hasLower = true;
        if (isupper(input[i]))
            hasUpper = true;
        if (isdigit(input[i]))
            hasDigit = true;

        size_t special = input.find_first_not_of(normalChars);
        if (special != string::npos)
            specialChar = true;
    }

    // Strength of password
    cout << "Strength of password:-";
    if (hasLower && hasUpper && hasDigit &&
        specialChar && (n >= 8))
        cout << "Strong" << endl;
    else if ((hasLower || hasUpper) &&
             specialChar && (n >= 6))
        cout << "Moderate" << endl;
    else
        cout << "Weak" << endl;
}

// Driver code
int main()
{
    string input = "GeeksforGeeks!@12";
    printStrongNess(input);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation fo the above approach
import java.io.*;
import java.util.*;

class GFG {

    public static void printStrongNess(String input)
    {
        // Checking lower alphabet in string
        int n = input.length();
        boolean hasLower = false, hasUpper = false,
                hasDigit = false, specialChar = false;
        Set<Character> set = new HashSet<Character>(
            Arrays.asList('!', '@', '#', '{content}apos;, '%', '^', '&',
                          '*', '(', ')', '-', '+'));
        for (char i : input.toCharArray())
        {
            if (Character.isLowerCase(i))
                hasLower = true;
            if (Character.isUpperCase(i))
                hasUpper = true;
            if (Character.isDigit(i))
                hasDigit = true;
            if (set.contains(i))
                specialChar = true;
        }

        // Strength of password
        System.out.print("Strength of password:- ");
        if (hasDigit && hasLower && hasUpper && specialChar
            && (n >= 8))
            System.out.print(" Strong");
        else if ((hasLower || hasUpper || specialChar)
                 && (n >= 6))
            System.out.print(" Moderate");
        else
            System.out.print(" Weak");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String input = "GeeksforGeeks!@12";
        printStrongNess(input);
    }

}
// contributed by Ashish Chhabra
```

## 蟒蛇 3

```
# Python3 program to check if a given
# password is strong or not.
def printStrongNess(input_string):

    n = len(input_string)

    # Checking lower alphabet in string
    hasLower = False
    hasUpper = False
    hasDigit = False
    specialChar = False
    normalChars = "abcdefghijklmnopqrstu"
    "vwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890 "

    for i in range(n):
        if input_string[i].islower():
            hasLower = True
        if input_string[i].isupper():
            hasUpper = True
        if input_string[i].isdigit():
            hasDigit = True
        if input_string[i] not in normalChars:
            specialChar = True

    # Strength of password
    print("Strength of password:-", end = "")
    if (hasLower and hasUpper and
        hasDigit and specialChar and n >= 8):
        print("Strong")

    elif ((hasLower or hasUpper) and
          specialChar and n >= 6):
        print("Moderate")
    else:
        print("Weak")

# Driver code
if __name__=="__main__":

    input_string = "GeeksforGeeks!@12"

    printStrongNess(input_string)

# This code is contributed by Yash_R
```

**Output**

```
Strength of password:-Strong
```

本文由 [**阿普瓦·阿加瓦尔**](https://auth.geeksforgeeks.org/profile.php?user=Apurva Agarwal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。