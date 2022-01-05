# 以整数和的形式重新排列一个字符串，后跟最小化字符

> 原文:[https://www . geeksforgeeks . org/replace-a-string-in-form-of-integer-sum-后跟最小化字符/](https://www.geeksforgeeks.org/rearrange-a-string-in-the-form-of-integer-sum-followed-by-the-minimized-character/)

给定一个包含小写字母和数字的字符串。任务是构造另一个字符串，该字符串由数字的总和加上最小化为单个字符的所有字母的总和组成。如果没有数字，则在字符串中添加 0。
**注:**字母求和是这样做的:a+a = b，d+y = c.
**例:**

```
Input: str = "ab37b3a8"
Output: 21f
Sum of digits = 3 + 7 + 3 + 8 = 21
Sum of alphabets = a + b + b + a = 1 + 2 + 2 + 1 = 6
Alphabet at 6th position is f.

Input: str = "3by2b2a2"
Output: str = 9d
```

**方法:**为了分隔数字和字母，遍历给定的字符串，如果字符是数字，将其添加到数字和，如果是字母，将其添加到字母和。

1.  开始解开绳子。
2.  如果数字是数字，将其值(str[I]–' 0 ')加到 digitSum。
3.  否则，将 str[i]-'a'+1 添加到 alphabetSum。
4.  将 alphabetSum 转换为 char，并将其添加到 digitSum 的字符格式中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// function to return maximum volume
string separateChar(string str)
{
    int n = str.size(), digitSum = 0;
    int alphabetSum = 0, j = 0;

    // separate digits and alphabets
    for (int i = 0; i < n; i++) {
        if (isdigit(str[i]))
            digitSum += str[i] - '0';

        else {
            alphabetSum += str[i] - 'a' + 1;
            alphabetSum %= 26;
        }
    }

    // change digit sum to string
    string sumStr = to_string(digitSum);

    // change alphabet sum to string
    char alphabetStr = char(alphabetSum + 'a' - 1);

    // concatenate sum to alphabets string
    sumStr += alphabetStr;

    return sumStr;
}

// Driver code
int main()
{
    string str = "3652adyz3423";
    cout << separateChar(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class Solution
{

// function to return maximum volume
static String separateChar(String str)
{
    int n = str.length(), digitSum = 0;
    int alphabetSum = 0, j = 0;

    // separate digits and alphabets
    for (int i = 0; i < n; i++) {
        if (str.charAt(i)>='0'&&str.charAt(i)<='9') {
            digitSum += (int)(str.charAt(i) - '0');
        }
        else {
            alphabetSum += str.charAt(i) - 'a' + 1;
            alphabetSum %= 26;
        }
    }

    // change digit sum to string
    String sumStr = ""+(digitSum);

    // change alphabet sum to string
    char alphabetStr = (char)(alphabetSum + 'a' - 1);

    // concatenate sum to alphabets string
    sumStr += alphabetStr;

    return sumStr;
}

// Driver code
public static void main(String args[])
{
    String str = "3652adyz3423";
    System.out.println(separateChar(str));

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# function to return maximum volume
def separateChar(str__):
    n = len(str__)
    digitSum = 0
    alphabetSum = 0
    j = 0

    # separate digits and alphabets
    for i in range(n):
        if (ord(str__[i]) >= 48 and
            ord(str__[i]) <= 56):
            digitSum += ord(str__[i]) - ord('0')

        else:
            alphabetSum += ord(str__[i]) - ord('a') + 1
            alphabetSum %= 26

    # change digit sum to string
    sumStr = str(digitSum)

    # change alphabet sum to string
    alphabetStr = chr(alphabetSum + ord('a') - 1)

    # concatenate sum to alphabets string
    sumStr += alphabetStr

    return sumStr

# Driver code
if __name__ == '__main__':
    str__ = "3652adyz3423"
    print(separateChar(str__))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of above approach
using System;
public class Solution{

    // function to return maximum volume
    static String separateChar(String str)
    {
        int n = str.Length, digitSum = 0;
        int alphabetSum = 0, j = 0;

        // separate digits and alphabets
        for (int i = 0; i < n; i++) {
            if (str[i]>='0'&&str[i]<='9') {
                digitSum += (int)(str[i] - '0');
            }
            else {
                alphabetSum += str[i] - 'a' + 1;
                alphabetSum %= 26;
            }
        }

        // change digit sum to string
        String sumStr = ""+(digitSum);

        // change alphabet sum to string
        char alphabetStr = (char)(alphabetSum + 'a' - 1);

        // concatenate sum to alphabets string
        sumStr += alphabetStr;

        return sumStr;
    }

    // Driver code
    public static void Main()
    {
        String str = "3652adyz3423";
        Console.WriteLine(separateChar(str));

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// function to return maximum volume
function separateChar(str)
{
    var n = str.length, digitSum = 0;
    var alphabetSum = 0, j = 0;

    // separate digits and alphabets
    for (var i = 0; i < n; i++) {
        if (str[i] >= '0' && str[i] <= '9')
            digitSum += (str[i].charCodeAt(0) - '0'.charCodeAt(0));

        else {
            alphabetSum += (str[i].charCodeAt(0) - 'a'.charCodeAt(0) + 1);
            alphabetSum %= 26;
        }
    }

    // change digit sum to string
    var sumStr = digitSum.toString();

    // change alphabet sum to string
    var alphabetStr = String.fromCharCode(alphabetSum + 'a'.charCodeAt(0) - 1);

    // concatenate sum to alphabets string
    sumStr += alphabetStr;

    return sumStr;
}

// Driver code
var str = "3652adyz3423";
document.write( separateChar(str));

</script>
```

**Output:** 

```
28d
```