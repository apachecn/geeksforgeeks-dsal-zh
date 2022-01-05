# 检查字符串的平均字符是否存在

> 原文:[https://www . geesforgeks . org/check-字符串中的平均字符是否存在/](https://www.geeksforgeeks.org/check-whether-the-average-character-of-the-string-is-present-or-not/)

给定一个字母数字字符串，任务是检查该字符串的平均字符是否存在。平均字符是指与 ASCII 值相对应的字符，它是字符串中所有字符的 ASCII 值平均值的下限。

**示例:**

```
Input: abcdef
Output: d 
Yes
Explanation:
    string = "abcdef"
    ASCII values of a = 97, b=98, 
    c=99, d=100, e=101, f=101
    Sum of these values is 597
    Average is 99.5 ~ 100 
    Character of ASCII value 100 = d
    Hence d is present in the string.

Input: MNFGH
Output: J
No

```

**方法:**解决这个问题的方法很简单。可以通过以下步骤解决:

*   找出给定字符串中所有字符的 ASCII 值之和。
*   将 ASCII 值的平均值作为平均值=(总和/字符数)
*   获取这个平均 ASCII 值的字符。打印此字符
*   检查字符串中是否存在该字符。相应地打印是或否。

下面是上述方法的实现:

**执行:**

## C++

```
// CPP program to check if the average character
// is present in the string or not

#include <bits/stdc++.h>
#include <math.h>
using namespace std;

// Checks if the character is present
bool check_char(char* st, char ch)
{

    // Get the length of string
    int l = strlen(st);

    // Iterate from i=0 to
    // the length of the string
    // to check if the character
    // is present in the string
    for (int i = 0; i < l; i++) {
        if (st[i] == ch)
            return true;
    }
    return false;
}

// Finds the average character of the string
char find_avg(char* st)
{
    int i, sm = 0;
    int l = strlen(st);
    char ch;

    for (i = 0; i < l; i++) {
        ch = st[i];

        // Calculate the sum of ASCII
        // values of each character
        sm = sm + (int)(ch);
    }

    // Calculate average of ascii values
    int avg = (int)(floor(sm / l));

    // Convert the ASCII value to character
    // and return it
    return ((char)(avg));
}

// Driver code
int main()
{
    char st[] = "ag23sdfa";

    // Get the average character
    char ch = find_avg(st);
    cout << ch << endl;

    // Check if the average character
    // is present in string or not
    if (check_char(st, ch) == true)
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the average character
// is present in the string or not

import java.math.*;

class GFG {

    // Checks if the character is present
    static boolean check_char(String st, char ch)
    {

        // Get the length of string
        int l = st.length();

        // Iterate from i=0 to
        // the length of the string
        // to check if the character
        // is present in the string
        for (int i = 0; i < l; i++) {
            if (st.charAt(i) == ch)
                return true;
        }
        return false;
    }

    // Finds the average character of the string
    static char find_avg(String st)
    {
        int i, sm = 0;
        int l = st.length();
        char ch;

        for (i = 0; i < l; i++) {
            ch = st.charAt(i);

            // Calculate the sum of ASCII
            // values of each character
            sm = sm + (int)(ch);
        }

        // Calculate the average of ASCII values
        int avg = (int)(Math.floor(sm / l));

        // Convert the ASCII value to character
        // and return it
        return ((char)(avg));
    }

    // Driver code
    public static void main(String[] args)
    {
        String st = "ag23sdfa";

        // Get the average character
        char ch = find_avg(st);
        System.out.println(ch);

        // Check if the average character
        // is present in string or not
        if (check_char(st, ch) == true)
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}
```

## 蟒蛇 3

```
# Python 3 program to check if the average 
# character is present in the string or not
from math import floor

# Checks if the character is present
def check_char(st, ch):

    # Get the length of string
    l = len(st)

    # Iterate from i=0 to
    # the length of the string
    # to check if the character
    # is present in the string
    for i in range(l):
        if (st[i] == ch):
            return True

    return False

# Finds the average character
# of the string
def find_avg(st):
    sm = 0
    l = len(st)

    for i in range(l):
        ch = st[i]

        # Calculate the sum of ASCII
        # values of each character
        sm = sm + ord(ch)

    # Calculate average of ascii values
    avg = int(floor(sm / l))

    # Convert the ASCII value to character
    # and return it
    return (chr(avg))

# Driver code
if __name__ == '__main__':
    st = "ag23sdfa"

    # Get the average character
    ch = find_avg(st)
    print(ch)

    # Check if the average character
    # is present in string or not
    if (check_char(st, ch) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check if the average character
// is present in the string or not
using System;

class GFG 
{

    // Checks if the character is present
    static bool check_char(string st, char ch)
    {

        // Get the length of string
        int l = st.Length;

        // Iterate from i=0 to
        // the length of the string
        // to check if the character
        // is present in the string
        for (int i = 0; i < l; i++) 
        {
            if (st[i] == ch)
                return true;
        }
        return false;
    }

    // Finds the average character of the string
    static char find_avg(string st)
    {
        int i, sm = 0;
        int l = st.Length;
        char ch;

        for (i = 0; i < l; i++)
        {
            ch = st[i];

            // Calculate the sum of ASCII
            // values of each character
            sm = sm + (int)(ch);
        }

        // Calculate the average of ASCII values
        int avg = (int)(Math.Floor((double)(sm / l)));

        // Convert the ASCII value to character
        // and return it
        return ((char)(avg));
    }

    // Driver code
    public static void Main()
    {
        string st = "ag23sdfa";

        // Get the average character
        char ch = find_avg(st);
        Console.WriteLine(ch);

        // Check if the average character
        // is present in string or not
        if (check_char(st, ch) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

    }
}

// This code is contributed by Akanksha Rai
```

**Output:**

```
Y
No

```