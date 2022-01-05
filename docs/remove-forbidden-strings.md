# 移除禁止的弦

> 原文:[https://www.geeksforgeeks.org/remove-forbidden-strings/](https://www.geeksforgeeks.org/remove-forbidden-strings/)

给定一个字符串 W，以这样的方式更改该字符串，即它不包含任何“禁止”的字符串 S1 到锡作为其子字符串之一。管理此更改的规则如下:
1。字符的大小写无关紧要，即“xYZ”与“XyZ”相同。
2。更改原始字符串中由子字符串覆盖的所有字符 **W** ，使得特定字母 **lt** 在更改后的字符串中出现的次数最多，并且更改后的字符串在字典顺序上是可以从所有可能的组合中获得的最小字符串。
3。不在禁止的子字符串内的字符不允许更改。
4。改变字符的大小写必须与字符串 **W** 中该位置的原字符大小写相同。
5。如果字母 **lt** 是子串的一部分，则必须根据上述规则将其更改为其他字符。
**举例:**

```
Input : n = 3  
        s1 = "etr"
        s2 = "ed" 
        s3 = "ied"
        W = "PEtrUnited"
        letter = "d"
Output : PDddUnitda

Input : n = 1
        s1 = "PetrsDreamOh"
        W = "PetrsDreamOh"
        letter = h
Output : HhhhhHhhhhHa
```

**解释:**
**例 1:** 第一个字符 P 不属于任何子串，因此不改变。接下来的三个字符组成子字符串“etr”，并被改为“Ddd”。接下来的四个字符不属于任何禁止的子字符串，并且保持不变。接下来的两个字符组成子字符串“ed”，并被改为“da”，因为 d 是最后一个字符本身，它被另一个字符“a”替换，这样字符串在字典上是最小的。
**注意:**“Etr”=“ETR”，由于“ETR”的第一个字母是大写的，因此更改后的子字符串“Ddd”的第一个字符为“D”。
**例 2:** 由于整个字符串是禁止字符串，根据情况从第一个到第二个最后一个字符用字母‘h’替换。最后一个字符是“h ”,因此它被字母“a”代替，这样字符串在字典上是最小的。

**方法:**
检查字符串 W 的每个字符，无论它是否是任何子字符串的开头。使用另一个数组记录 W 的字符，这些字符是禁止字符串的一部分，需要更改。
字符按照以下规则变化:
1。如果 W[i] =字母和字母= 'a '，那么 W[i] = 'b'
2。如果 W[i] =字母和字母！='a '然后 W[i] = 'a'
3。如果 W[i]！=字母然后 W[i] =字母
当 W[i]是大写字符时，也将使用第一个和第二个条件。
以下是上述方法的实施:

## C++

```
// CPP program to remove the forbidden strings
#include <bits/stdc++.h>
using namespace std;

// pre[] keeps record of the characters
// of w that need to be changed
bool pre[100];

// number of forbidden strings
int n;

// given string
string w;

// stores the forbidden strings
string s[110];

// letter to replace and occur
// max number of times
char letter;

// Function to check if the particula
// r substring is present in w at position
void verify(int position, int index)
{
    int l = w.length();
    int k = s[index].length();

    // If length of substring from this
    // position is greater than length
    // of w then return
    if (position + k > l)
        return;

    bool same = true;
    for (int i = position; i < position + k;
                                      i++) {

        // n and n1 are used to check for
        // substring without considering
        // the case of the letters in w
        // by comparing the difference
        // of ASCII values
        int n, n1;
        char ch = w[i];
        char ch1 = s[index][i - position];
        if (ch >= 'a' && ch <= 'z')
            n = ch - 'a';
        else
            n = ch - 'A';
        if (ch1 >= 'a' && ch1 <= 'z')
            n1 = ch1 - 'a';
        else
            n1 = ch1 - 'A';
        if (n != n1)
            same = false;
    }

    // If same == true then it means a
    // substring was found starting at
    // position therefore all characters
    // from position to length of substring
    // found need to be changed therefore
    // they needs to be marked
    if (same == true) {
        for (int i = position; i < position + k;
                                           i++)
            pre[i] = true;
        return;
    }
}

// Function implementing logic
void solve()
{
    int l = w.length();
    int p = letter - 'a';

    for (int i = 0; i < 100; i++)
        pre[i] = false;

    // To verify if any substring is
    // starting from index i
    for (int i = 0; i < l; i++) {
        for (int j = 0; j < n; j++)
            verify(i, j);
    }

    // Modifying the string w
    // according to th rules
    for (int i = 0; i < l; i++) {
        if (pre[i] == true) {
            if (w[i] == letter)
                w[i] = (letter == 'a') ? 'b' : 'a';

            // This condition checks
            // if w[i]=upper(letter)
            else if (w[i] == 'A' + p)
                w[i] = (letter == 'a') ? 'B' : 'A';

            // This condition checks if w[i]
            // is any lowercase letter apart
            // from letter. If true replace
            // it with letter
            else if (w[i] >= 'a' && w[i] <= 'z')
                w[i] = letter;

            // This condition checks if w[i]
            // is any uppercase letter apart
            // from letter. If true then
            // replace it with upper(letter).
            else if (w[i] >= 'A' && w[i] <= 'Z')
                w[i] = 'A' + p;
        }
    }
    cout << w;
}

// Driver function for the program
int main()
{
    n = 3;
    s[0] = "etr";
    s[1] = "ed";
    s[2] = "ied";
    w = "PEtrUnited";
    letter = 'd';

    // Calling function
    solve();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove forbidden strings
import java.io.*;

class rtf {

    // number of forbidden strings
    public static int n;

    // original string
    public static String z;

    // forbidden strings
    public static String s[] = new String[100];

    // to store original string
    // as character array
    public static char w[];

    // letter to replace and occur
    // max number of times
    public static char letter;  

    // pre[] keeps record of the characters
    // of w that need to be changed
    public static boolean pre[] = new boolean[100];

    // Function to check if the particular
    // substring is present in w at position
    public static void verify(int position, int index)
    {
        int l = z.length();
        int k = s[index].length();

        // If length of substring from this
        // position is greater than length
        // of w then return
        if (position + k > l)
            return;

        boolean same = true;
        for (int i = position; i < position + k; i++) {

            // n and n1 are used to check for
            // substring without considering
            // the case of the letters in w
            // by comparing the difference
            // of ASCII values
            int n, n1;
            char ch = w[i];
            char ch1 = s[index].charAt(i - position);
            if (ch >= 'a' && ch <= 'z')
                n = ch - 'a';
            else
                n = ch - 'A';
            if (ch1 >= 'a' && ch1 <= 'z')
                n1 = ch1 - 'a';
            else
                n1 = ch1 - 'A';
            if (n != n1)
                same = false;
        }

        // If same == true then it means a substring
        // was found starting at position therefore
        // all characters from position to length
        // of substring found need to be changed
        // therefore they need to be marked
        if (same == true) {
            for (int i = position; i < position + k;
                                               i++)
                pre[i] = true;
            return;
        }
    }

    // Function performing calculations.
    public static void solve()
    {
        w = z.toCharArray();
        letter = 'd';
        int l = z.length();
        int p = letter - 'a';
        for (int i = 0; i < 100; i++)
            pre[i] = false;

        // To verify if any substring is
        // starting from index i
        for (int i = 0; i < l; i++) {
            for (int j = 0; j < n; j++)
                verify(i, j);
        }

        // Modifying the string w
        // according to th rules
        for (int i = 0; i < l; i++) {
            if (pre[i] == true) {
                if (w[i] == letter)
                    w[i] = (letter == 'a') ? 'b' : 'a';

                // This condition checks
                // if w[i]=upper(letter)
                else if (w[i] == (char)((int)'A' + p))
                    w[i] = (letter == 'a') ? 'B' : 'A';

                // This condition checks if w[i]
                // is any lowercase letter apart
                // from letter. If true replace
                // it with letter
                else if (w[i] >= 'a' && w[i] <= 'z')
                    w[i] = letter;

                // This condition checks if w[i]
                // is any uppercase letter apart
                // from letter. If true then
                // replace it with upper(letter).
                else if (w[i] >= 'A' && w[i] <= 'Z')
                    w[i] = (char)((int)'A' + p);
            }
        }
        System.out.println(w);
    }

    // Driver function for the program
    public static void main(String args[])
    {
        n = 3;
        s[0] = "etr";
        s[1] = "ed";
        s[2] = "ied";
        z = "PEtrUnited";
        solve();
    }
}
```

## 蟒蛇 3

```
# Python program to remove the forbidden strings

# pre[] keeps record of the characters
# of w that need to be changed
pre = [False]*100

# stores the forbidden strings
s = [None]*110

# Function to check if the particula
# r substring is present in w at position
def verify(position, index):
    l = len(w)
    k = len(s[index])

    # If length of substring from this
    # position is greater than length
    # of w then return
    if (position + k > l):
        return

    same = True
    for i in range(position, position + k):
        # n and n1 are used to check for
        # substring without considering
        # the case of the letters in w
        # by comparing the difference
        # of ASCII values
        ch = w[i]
        ch1 = s[index][i - position]
        if (ch >= 'a' and ch <= 'z'):
            n = ord(ch) - ord('a')
        else:
            n = ord(ch) - ord('A')
        if (ch1 >= 'a' and ch1 <= 'z'):
            n1 = ord(ch1) - ord('a')
        else:
            n1 = ord(ch1) - ord('A')
        if (n != n1):
            same = False

    # If same == true then it means a
    # substring was found starting at
    # position therefore all characters
    # from position to length of substring
    # found need to be changed therefore
    # they needs to be marked
    if (same == True):
        for i in range( position, position + k):
            pre[i] = True
        return

# Function implementing logic
def solve():

    l = len(w)
    p = ord(letter) - ord('a')

    # To verify if any substring is
    # starting from index i
    for i in range(l):
        for j in range(n):
            verify(i, j)

    # Modifying the string w
    # according to th rules
    for i in range(l):
        if (pre[i] == True):
            if (w[i] == letter):
                w[i] = 'b' if (letter == 'a') else 'a'

            # This condition checks
            # if w[i]=upper(letter)
            elif (w[i] == str(ord('A') + p)):
                w[i] = 'B' if (letter == 'a') else 'A'

            # This condition checks if w[i]
            # is any lowercase letter apart
            # from letter. If true replace
            # it with letter
            elif (w[i] >= 'a' and w[i] <= 'z'):
                w[i] = letter

            # This condition checks if w[i]
            # is any uppercase letter apart
            # from letter. If true then
            # replace it with upper(letter).
            elif (w[i] >= 'A' and w[i] <= 'Z'):
                w[i] = chr(ord('A') + p)

    print(''.join(w))

# Driver function for the program

# number of forbidden strings
n = 3

s[0] = "etr"
s[1] = "ed"
s[2] = "ied"

# given string
w = "PEtrUnited"
w = list(w)

# letter to replace and occur
# max number of times
letter = 'd'

# Calling function
solve()

# This code is contributed by ankush_953
```

## C#

```
// C# program to remove forbidden strings
using System;

class GFG
{

// number of forbidden strings
public static int n;

// original string
public static string z;

// forbidden strings
public static string[] s = new string[100];

// to store original string
// as character array
public static char[] w;

// letter to replace and occur
// max number of times
public static char letter;

// pre[] keeps record of the characters
// of w that need to be changed
public static bool[] pre = new bool[100];

// Function to check if the particular
// substring is present in w at position
public static void verify(int position,
                          int index)
{
    int l = z.Length;
    int k = s[index].Length;

    // If length of substring from this
    // position is greater than length
    // of w then return
    if (position + k > l)
    {
        return;
    }

    bool same = true;
    for (int i = position;
             i < position + k; i++)
    {

        // n and n1 are used to check for
        // substring without considering
        // the case of the letters in w
        // by comparing the difference
        // of ASCII values
        int n, n1;
        char ch = w[i];
        char ch1 = s[index][i - position];
        if (ch >= 'a' && ch <= 'z')
        {
            n = ch - 'a';
        }
        else
        {
            n = ch - 'A';
        }
        if (ch1 >= 'a' && ch1 <= 'z')
        {
            n1 = ch1 - 'a';
        }
        else
        {
            n1 = ch1 - 'A';
        }
        if (n != n1)
        {
            same = false;
        }
    }

    // If same == true then it means a
    // substring was found starting at
    // position therefore all characters
    // from position to length of substring
    // found need to be changed therefore
    // they need to be marked
    if (same == true)
    {
        for (int i = position;
                 i < position + k; i++)
        {
            pre[i] = true;
        }
        return;
    }
}

// Function performing calculations.
public static void solve()
{
    w = z.ToCharArray();
    letter = 'd';
    int l = z.Length;
    int p = letter - 'a';
    for (int i = 0; i < 100; i++)
    {
        pre[i] = false;
    }

    // To verify if any substring is
    // starting from index i
    for (int i = 0; i < l; i++)
    {
        for (int j = 0; j < n; j++)
        {
            verify(i, j);
        }
    }

    // Modifying the string w
    // according to th rules
    for (int i = 0; i < l; i++)
    {
        if (pre[i] == true)
        {
            if (w[i] == letter)
            {
                w[i] = (letter == 'a') ? 'b' : 'a';
            }

            // This condition checks
            // if w[i]=upper(letter)
            else if (w[i] == (char)((int)'A' + p))
            {
                w[i] = (letter == 'a') ? 'B' : 'A';
            }

            // This condition checks if w[i]
            // is any lowercase letter apart
            // from letter. If true replace
            // it with letter
            else if (w[i] >= 'a' && w[i] <= 'z')
            {
                w[i] = letter;
            }

            // This condition checks if w[i]
            // is any uppercase letter apart
            // from letter. If true then
            // replace it with upper(letter).
            else if (w[i] >= 'A' && w[i] <= 'Z')
            {
                w[i] = (char)((int)'A' + p);
            }
        }
    }
    Console.WriteLine(w);
}

// Driver Code
public static void Main(string[] args)
{
    n = 3;
    s[0] = "etr";
    s[1] = "ed";
    s[2] = "ied";
    z = "PEtrUnited";
    solve();
}
}

// This code is contributed by Shrikanth13
```

**输出:**

```
PDddUnitda
```