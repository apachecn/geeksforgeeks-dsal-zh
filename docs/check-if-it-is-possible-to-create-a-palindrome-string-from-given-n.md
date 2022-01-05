# 检查是否可以从给定的 N

创建回文串

> 原文:[https://www . geeksforgeeks . org/check-如果可能的话-创建一个回文字符串-来自给定的-n/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-create-a-palindrome-string-from-given-n/)

给定一个数字 n，任务是根据该数字创建一个小写字母的字符串，并判断该字符串是否是回文。a = 0，b = 1…..等等。

**例如:**如果数字是 61，子字符串“gb”将被打印到 7 (6+1)个字符，即“gbgbgbg”，并检查是否有回文。

**注意:**没有数字会以零开始。仅考虑字母“a 到 j”，即从 0 到 9 的单个数字。

**示例**:

> **输入:** N = 61
> **输出:** YES
> 数字 6、1 分别代表字母‘g’、‘b’。所以子串是“gb”，总和是 7(6+1)。这样形成的字母串就是‘gbg gbg’，是回文。
> 
> **输入:** N = 1998
> **输出:** NO
> 数字 1、9、8 分别代表字母‘b’、‘j’和‘I’。所以子串是‘bjji’，sum 是 27(1+9+9+8)。因此，按字母顺序排列的字符串是 bjjibjjibjjibjj，而不是回文。

**进场:**

1.  获取给定数字 N 对应的子串，并保持其数字之和。
2.  追加子字符串，直到它的长度等于 n 个数字的总和
3.  检查得到的字符串是否是回文。
4.  如果是回文，打印“是”。
5.  否则，打印否

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if a string 
// is palindrome or not
bool isPalindrome(string s)
{
    // String that stores characters
    // of s in reverse order
    string s1 = "";

    // Length of the string s
    int N = s.length();

    for (int i = N - 1; i >= 0; i--)
        s1 += s[i];

    if (s == s1)
        return true;
    return false;
}

bool createString(int N)
{
    string str = "";
    string s = to_string(N);

    // String used to form substring 
    // using N
    string letters = "abcdefghij";

    // Variable to store sum 
    // of digits of N
    int sum = 0;
    string substr = "";

    // Forming the substring 
    // by traversing N
    for (int i = 0; i < s.length(); i++)
    {
        int digit = s[i] - '0';
        substr += letters[digit];
        sum += digit;
    }

    // Appending the substr to str till 
    // it's length becomes equal to sum
    while (str.length() <= sum)
    {
        str += substr;
    }

    // Trimming the string str so that 
    // it's length becomes equal to sum
    str = str.substr(0, sum);

    return isPalindrome(str);
}

// Driver code
int main()
{
    int N = 61;

    // Calling function isPalindrome to 
    // check if str is Palindrome or not
    bool flag = createString(N);
    if (flag)
        cout << "YES";
    else
        cout << "NO";
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

public class GFG {

    // Function to check if a string is palindrome or not
    static boolean isPalindrome(String s)
    {
        // String that stores characters
        // of s in reverse order
        String s1 = "";

        // Length of the string s
        int N = s.length();

        for (int i = N - 1; i >= 0; i--)
            s1 += s.charAt(i);

        if (s.equals(s1))
            return true;
        return false;
    }

    static boolean createString(int N)
    {
        String str = "";
        String s = "" + N;

        // String used to form substring using N
        String letters = "abcdefghij";
        // Variable to store sum of digits of N
        int sum = 0;
        String substr = "";

        // Forming the substring by traversing N
        for (int i = 0; i < s.length(); i++) {
            int digit = s.charAt(i) - '0';
            substr += letters.charAt(digit);
            sum += digit;
        }

        // Appending the substr to str 
        // till it's length becomes equal to sum
        while (str.length() <= sum) {
            str += substr;
        }

        // Trimming the string str so that 
        // it's length becomes equal to sum
        str = str.substring(0, sum);

        return isPalindrome(str);
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 61;

        // Calling function isPalindrome to 
        // check if str is Palindrome or not
        boolean flag = createString(N);
        if (flag)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of 
# the above approach

# Function to check if a string 
# is palindrome or not
def isPalindrome(s):

    # String that stores characters
    # of s in reverse order
    s1 = ""

    # Length of the string s
    N = len(s)
    i = (N - 1)
    while(i >= 0):
        s1 += s[i]
        i = i - 1

    if (s == s1):
        return True
    return False

def createString(N):

    s2 = ""
    s = str(N)

    # String used to form
    # substring using N
    letters = "abcdefghij"

    # Variable to store sum 
    # of digits of N
    sum = 0
    substr = ""

    # Forming the substring 
    # by traversing N
    for i in range(0, len(s)) :
        digit = int(s[i])
        substr += letters[digit]
        sum += digit

    # Appending the substr to str till
    # it's length becomes equal to sum
    while (len(s2) <= sum):
        s2 += substr

    # Trimming the string str so that 
    # it's length becomes equal to sum
    s2 = s2[:sum]

    return isPalindrome(s2)

# Driver code
N = 61;

# Calling function isPalindrome to 
# check if str is Palindrome or not
flag = createString(N)
if (flag):
    print("YES")
else:
    print("NO")

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG 
{

// Function to check if a string 
// is palindrome or not
static bool isPalindrome(String s)
{
    // String that stores characters
    // of s in reverse order
    String s1 = "";

    // Length of the string s
    int N = s.Length;

    for (int i = N - 1; i >= 0; i--)
        s1 += s[i];

    if (s.Equals(s1))
        return true;
    return false;
}

static bool createString(int N)
{
    String str = "";
    String s = "" + N;

    // String used to form substring 
    // using N
    String letters = "abcdefghij";

    // Variable to store sum 
    // of digits of N
    int sum = 0;
    String substr = "";

    // Forming the substring 
    // by traversing N
    for (int i = 0; i < s.Length; i++) 
    {
        int digit = s[i] - '0';
        substr += letters[digit];
        sum += digit;
    }

    // Appending the substr to str till 
    // it's length becomes equal to sum
    while (str.Length <= sum) 
    {
        str += substr;
    }

    // Trimming the string str so that 
    // it's length becomes equal to sum
    str = str.Substring(0, sum);

    return isPalindrome(str);
}

// Driver code
public static void Main()
{
    int N = 61;

    // Calling function isPalindrome to 
    // check if str is Palindrome or not
    bool flag = createString(N);
    if (flag)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed 
// by ihritik
```

**Output:**

```
YES

```