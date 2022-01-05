# 从给定的字符串中删除“b”和“AC”

> 原文:[https://www . geesforgeks . org/remove-a-and-BC-from-a-给定字符串/](https://www.geeksforgeeks.org/remove-a-and-bc-from-a-given-string/)

给定一个字符串，去掉字符串中所有的“b”和“ac”，你必须就地替换它们，并且你只被允许遍历字符串一次。(来源[谷歌面试问题](http://www.careercup.com/question?id=18460667))

**示例:**

```
acbac   ==>  ""
aaac    ==>  aa
ababac  ==>   aa
bbbbd   ==>   d
```

[](https://practice.geeksforgeeks.org/problems/remove-b-and-ac-from-a-given-string4336/1)

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/remove-b-and-ac-from-a-given-string4336/1)

[](https://practice.geeksforgeeks.org/problems/remove-b-and-ac-from-a-given-string4336/1)
这两个条件是:
**1。**所有‘b’和‘AC’的过滤应在单程
**2 中进行。**不允许有额外空间。

方法是使用两个索引变量 I 和 j。我们使用“I”在字符串中向前移动，并使用除“b”和“ac”之外的索引 j 添加字符。这里的诀窍是如何在“c”之前跟踪“a”。一个有趣的方法是使用双状态机。当前一个字符为“a”时，状态保持为“2”，否则状态为“1”。
**1)** 如果状态为 ONE，则不要复制当前字符进行输出如果以下条件之一为真
……**a)**当前字符为‘b’(我们需要删除‘b’)
……**b)**当前字符为‘a’(下一个字符可能为‘c’)
**2)**如果状态为 TWO，当前字符不是‘c’，我们首先需要确定我们复制了上一个字符‘a’。然后我们检查当前字符，如果当前字符不是‘b’也不是‘a’，那么我们就复制它输出。

## C++

```
// A C++ program to remove "b" and 'ac' from input string
#include <iostream>
using namespace std;
#define ONE 1
#define TWO 2

// The main function that removes occurrences of "a" and "bc"
// in input string
void stringFilter(char *str)
{
    // state is initially ONE (The previous character is not a)
    int state = ONE;

    // i and j are index variables, i is used to read next
    // character of input string, j is used for indexes of output
    // string (modified input string)
    int j = 0;

    // Process all characters of input string one by one
    for (int i = 0; str[i] != '\0'; i++)
    {
        /* If state is ONE, then do NOT copy the current character
          to output if one of the following conditions is true
           ...a) Current character is 'b' (We need to remove 'b')
           ...b) Current character is 'a' (Next character may be 'c') */
        if (state == ONE && str[i] != 'a' && str[i] != 'b')
        {
            str[j] = str[i];
            j++;
        }

        // If state is TWO and current character is not 'c' (other-
        // wise we ignore both previous and current characters)
        if (state == TWO && str[i] != 'c')
        {
            // First copy the previous 'a'
            str[j] = 'a';
            j++;

            // Then copy the current character if it is not 'a'
            // and 'b'
            if (str[i] != 'a' && str[i] != 'b')
            {
                str[j] = str[i];
                j++;
            }
        }

        // Change state according to current character
        state = (str[i] == 'a')? TWO: ONE;
    }

    // If last character was 'a', copy it to output
    if (state == TWO)
    {
        str[j] = 'a';
        j++;
    }

    // Set the string terminator
    str[j] = '\0';
}

/* Driver program to check above functions */
int main()
{
    char str1[] = "ad";
    stringFilter(str1);
    cout << str1 << endl;

    char str2[] = "acbac";
    stringFilter(str2);
    cout << str2 << endl;

    char str3[] = "aaac";
    stringFilter(str3);
    cout << str3 << endl;

    char str4[] = "react";
    stringFilter(str4);
    cout << str4 << endl;

    char str5[] = "aa";
    stringFilter(str5);
    cout << str5 << endl;

    char str6[] = "ababaac";
    stringFilter(str6);
    cout << str6 << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to remove "b" and
// 'ac' from input String
import java.util.*;

class GFG
{
static final int ONE = 1;
static final int TWO = 2;

// The main function that removes occurrences
// of "a" and "bc" in input String
static char[] StringFilter(char []str)
{
    // state is initially ONE
    // (The previous character is not a)
    int state = ONE;

    // i and j are index variables,
    // i is used to read next
    // character of input String,
    // j is used for indexes of output
    // String (modified input String)
    int j = 0;

    // Process all characters of 
    // input String one by one
    for (int i = 0; i < str.length; i++)
    {
        /* If state is ONE, then do NOT copy 
        the current character to output if 
        one of the following conditions is true
        ...a) Current character is 'b'
              (We need to remove 'b')
        ...b) Current character is 'a' 
              (Next character may be 'c') */
        if (state == ONE && str[i] != 'a' && 
                            str[i] != 'b')
        {
            str[j] = str[i];
            j++;
        }

        // If state is TWO and current character 
        // is not 'c' (otherwise we ignore both 
        // previous and current characters)
        if (state == TWO && str[i] != 'c')
        {
            // First copy the previous 'a'
            str[j] = 'a';
            j++;

            // Then copy the current character 
            // if it is not 'a' and 'b'
            if (str[i] != 'a' && str[i] != 'b')
            {
                str[j] = str[i];
                j++;
            }
        }

        // Change state according to current character
        state = (str[i] == 'a') ? TWO : ONE;
    }

    // If last character was 'a',
    // copy it to output
    if (state == TWO)
    {
        str[j] = 'a';
        j++;
    }
    return Arrays.copyOfRange(str, 0, j);
}

// Driver Code
public static void main(String[] args)
{
    char str1[] = "ad".toCharArray();
    str1 = StringFilter(str1);
    System.out.print(String.valueOf(str1) + "\n");

    char str2[] = "acbac".toCharArray();
    str2 = StringFilter(str2);
    System.out.print(String.valueOf(str2) + "\n");

    char str3[] = "aaac".toCharArray();
    str3 = StringFilter(str3);
    System.out.print(String.valueOf(str3) + "\n");

    char str4[] = "react".toCharArray();
    str4 = StringFilter(str4);
    System.out.print(String.valueOf(str4) + "\n");

    char str5[] = "aa".toCharArray();
    str5 = StringFilter(str5);
    System.out.print(String.valueOf(str5) + "\n");

    char str6[] = "ababaac".toCharArray();
    str6 = StringFilter(str6);
    System.out.print(String.valueOf(str6) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# A Python program to remove "b" and 'ac' from input string
ONE = 1
TWO = 2

# Utility function to convert string to list
def toList(string):
    l = []
    for x in string:
        l.append(x)
    return l

# Utility function to convert list to string
def toString(l):
    return ''.join(l)

# The main function that removes occurrences of "a" and "bc"
# in input string
def stringFilter(string):

    # state is initially ONE (The previous character is not a)
    state = ONE

    # i and j are index variables, i is used to read next
    # character of input string, j is used for indexes of
    # output string (modified input string)
    j = 0

    # Process all characters of input string one by one
    for i in xrange(len(string)):

        # If state is ONE, then do NOT copy the current character
        # to output if one of the following conditions is true
        # ...a) Current character is 'b' (We need to remove 'b')
        # ...b) Current character is 'a' (Next character may be 'c')
        if state == ONE and string[i] != 'a' and string[i] != 'b':
            string[j] = string[i]
            j += 1

        # If state is TWO and current character is not 'c' (other-
        # wise we ignore both previous and current characters)
        if state == TWO and string[i] != 'c':
            # First copy the previous 'a'
            string[j] = 'a'
            j += 1

            # Then copy the current character if it is not 'a' and 'b'
            if string[i] != 'a' and string[i] != 'b':
                string[j] = string[i]
                j += 1

        # Change state according to current character
         state = TWO if string[i] == 'a' else ONE

    # If last character was 'a', copy it to output
    if state == TWO:
        string[j] = 'a'
        j += 1

    return toString(string[:j])

# Driver program
string1 = stringFilter(toList("ad"))
print string1

string2 = stringFilter(toList("acbac"))
print string2

string3 = stringFilter(toList("aaac"))
print string3

string4 = stringFilter(toList("react"))
print string4

string5 = stringFilter(toList("aa"))
print string5

string6 = stringFilter(toList("ababaac"))
print string6

# This code is contributed by BHAVYA JAIN
```

## C#

```
// A C# program to remove "b" and
// 'ac' from input String
using System;

class GFG
{
static readonly int ONE = 1;
static readonly int TWO = 2;

// The main function that removes occurrences
// of "a" and "bc" in input String
static char[] StringFilter(char []str)
{

    // state is initially ONE
    // (The previous character is not a)
    int state = ONE;

    // i and j are index variables,
    // i is used to read next
    // character of input String,
    // j is used for indexes of output
    // String (modified input String)
    int j = 0;

    // Process all characters of 
    // input String one by one
    for (int i = 0; i < str.Length; i++)
    {
        /* If state is ONE, then do NOT copy 
        the current character to output if 
        one of the following conditions is true
        ...a) Current character is 'b'
            (We need to remove 'b')
        ...b) Current character is 'a' 
            (Next character may be 'c') */
        if (state == ONE && str[i] != 'a' && 
                            str[i] != 'b')
        {
            str[j] = str[i];
            j++;
        }

        // If state is TWO and current character 
        // is not 'c' (otherwise we ignore both 
        // previous and current characters)
        if (state == TWO && str[i] != 'c')
        {
            // First copy the previous 'a'
            str[j] = 'a';
            j++;

            // Then copy the current character 
            // if it is not 'a' and 'b'
            if (str[i] != 'a' && str[i] != 'b')
            {
                str[j] = str[i];
                j++;
            }
        }

        // Change state according to
        // current character
        state = (str[i] == 'a') ? TWO : ONE;
    }

    // If last character was 'a',
    // copy it to output
    if (state == TWO)
    {
        str[j] = 'a';
        j++;
    }
    return String.Join("", str).
           Substring(0, j).ToCharArray();
}

// Driver Code
public static void Main(String[] args)
{
    char []str1 = "ad".ToCharArray();
    str1 = StringFilter(str1);
    Console.Write(String.Join("", str1) + "\n");

    char []str2 = "acbac".ToCharArray();
    str2 = StringFilter(str2);
    Console.Write(String.Join("", str2) + "\n");

    char []str3 = "aaac".ToCharArray();
    str3 = StringFilter(str3);
    Console.Write(String.Join("", str3) + "\n");

    char []str4 = "react".ToCharArray();
    str4 = StringFilter(str4);
    Console.Write(String.Join("", str4) + "\n");

    char []str5 = "aa".ToCharArray();
    str5 = StringFilter(str5);
    Console.Write(String.Join("", str5) + "\n");

    char []str6 = "ababaac".ToCharArray();
    str6 = StringFilter(str6);
    Console.Write(String.Join("", str6) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
ad

aa
ret
aa
aaa
```

**上述问题的一个扩展，我们根本不希望“ac”出现在输出中:**
上面的代码看起来很好，似乎可以处理所有情况，但是如果输入字符串是“aacacc”，那么上面的代码将输出生成为“ac”，这看起来是正确的，因为它删除了连续出现的“a”和“c”。如果要求在输出字符串中根本没有“ac”呢。我们能否修改上述程序，在输入为“aacacc”时，以空字符串形式产生输出，在输入为“abcaaccd”时，以“d”形式产生输出？事实证明，在给定限制的情况下，这也是可以做到的。想法很简单。我们需要在上述程序的循环中添加以下行。

```
if (j>1 && str[j-2] == 'a' && str[j-1] =='c')
  j = j-2;
```

修改程序的不同测试用例见[本](http://ideone.com/CER6eq)。

**原问题的更简单解决方案:**

## C++

```
// // A C++ program to remove "b" and 'ac' from input string
#include<bits/stdc++.h>
using namespace std;

void stringFilter(char *str)
{
    int n = strlen(str);

    int i = -1;  // previous character
    int j = 0;   // current character

    while (j < n)
    {
        /* check if current and next character forms ac */
        if (j < n-1 && str[j] == 'a' && str[j+1] == 'c')
            j += 2;

        /* if current character is b */
        else if (str[j] == 'b')
            j++;

        /* if current char is 'c && last char in output
           is 'a' so delete both */
        else if (i >= 0 && str[j] == 'c' && str[i] == 'a')
            i--,j++;

        /* else copy curr char to output string */
        else
            str[++i] = str[j++];
    }
    str[++i] = '\0';
}

// Driver program to test above function
int main()
{
    char str1[] = "ad";
    cout << "Input => " << str1 << "\nOutput => ";
    stringFilter(str1);
    cout << str1 << endl << endl;

    char str2[] = "acbac";
    cout << "Input => " << str2 << "\nOutput => ";
    stringFilter(str2);
    cout << str2 << endl << endl;

    char str3[] = "aaac";
    cout << "Input => " << str3 << "\nOutput => ";
    stringFilter(str3);
    cout << str3 << endl << endl;

    char str4[] = "react";
    cout << "Input => " << str4 << "\nOutput => ";
    stringFilter(str4);
    cout << str4 << endl << endl;

    char str5[] = "aa";
    cout << "Input => " << str5 << "\nOutput => ";
    stringFilter(str5);
    cout << str5 << endl << endl;

    char str6[] = "ababaac";
    cout << "Input => " << str6 << "\nOutput => ";
    stringFilter(str6);
    cout << str6 << endl << endl;

    char str[] = "abc";
    cout << "Input => " << str << "\nOutput => ";
    stringFilter(str);
    cout << str << endl << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to remove "b" and 'ac' from input string 
class GfG {

// The main function that removes occurrences of "a" and "bc" 
// in input string 
static void stringFilter(char str[]) 
{ 
    int n = str.length; 

    int i = -1;  // previous character 
    int j = 0;   // current character 

    while (j < n) 
    { 
        /* check if current and next character forms ac */
        if (j < n-1 && str[j] == 'a' && str[j+1] == 'c') 
            j += 2; 

        /* if current character is b */
        else if (str[j] == 'b') 
            j++; 

        /* if current char is 'c && last char in output 
           is 'a' so delete both */
        else if (i >= 0 && str[j] == 'c' && str[i] == 'a')  {
            i--;
            j++; 
        }

        /* else copy curr char to output string */
        else
            str[++i] = str[j++]; 

    } 
 System.out.println(new String(str).substring(0,i+1));
} 

/* Driver program to check above functions */
public static void main(String[] args) 
{ 
    String str1 = "ad"; 
    stringFilter(str1.toCharArray()); 

    String str2 = "acbac"; 
    stringFilter(str2.toCharArray());

    String str3 = "aaac"; 
    stringFilter(str3.toCharArray()); 

    String str4 = "react"; 
    stringFilter(str4.toCharArray()); 

    String str5 = "aa"; 
    stringFilter(str5.toCharArray()); 

    String str6 = "ababaac"; 
    stringFilter(str6.toCharArray()); 
}
} 
```

## 计算机编程语言

```
# A Python program to remove "b" and 'ac' from input string

# Utility function to convert string to list
def toList(string):
    l = []
    for x in string:
        l.append(x)
    return l

# Utility function to convert list to string
def toString(l):
    return ''.join(l)

def stringFilter(string):

    # length of string
    n = len(string)

    i = -1
    j = 0

    while j < n:

        # Check if current and next character forms ac
        if j < n-1 and string[j] == 'a' and string[j+1] == 'c':
            j += 2

        # If current character is b
        elif string[j] == 'b':
            j += 1

        # if current char is 'c && last char in output
        # is 'a' so delete both
        elif i >= 0 and string[j] == 'c' and string[i] == 'a':
            i -= 1
            j += 1

        # Else copy curr char to output string
        else:
            i += 1
            string[i] = string[j]
            j += 1

    i += 1
    return toString(string[:i])

# Driver program
string1 = "ad"
print "Input => " + string1 + "\nOutput => ",
print stringFilter(toList(string1)) + "\n"

string2 = "acbac"
print "Input => " + string2 + "\nOutput => ",
print stringFilter(toList(string2)) + "\n"

string3 = "aaac"
print "Input => " + string3 + "\nOutput => ",
print stringFilter(toList(string3)) + "\n"

string4 = "react"
print "Input => " + string4 + "\nOutput => ",
print stringFilter(toList(string4)) + "\n"

string5 = "aa"
print "Input => " + string5 + "\nOutput => ",
print stringFilter(toList(string5)) + "\n"

string6 = "ababaac"
print "Input => " + string6 + "\nOutput => ",
print stringFilter(toList(string6)) + "\n"

string7 = "abc"
print "Input => " + string7 + "\nOutput => ",
print stringFilter(toList(string7)) + "\n"

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to remove "b" and 'ac' from input string 
using System;

class GfG 
{ 

    // The main function that removes occurrences of  
    // "a" and "bc" in input string 
    static void stringFilter(char []str) 
    { 
        int n = str.Length; 
        int i = -1; // previous character 
        int j = 0; // current character 
        while (j < n) 
        { 
            /* check if current and next character forms ac */
            if (j < n-1 && str[j] == 'a' && str[j+1] == 'c') 
                j += 2; 

            /* if current character is b */
            else if (str[j] == 'b') 
                j++; 

            /* if current char is 'c && last char in output 
            is 'a' so delete both */
            else if (i >= 0 && str[j] == 'c' && str[i] == 'a') 
            { 
                i--; 
                j++; 
            } 

            /* else copy curr char to output string */
            else
                str[++i] = str[j++]; 

        } 
        Console.WriteLine(new String(str)); 
    } 

    // Driver Code
    public static void Main() 
    {    
        String str1 = "ad"; 
        stringFilter(str1.ToCharArray()); 

        String str2 = "acbac"; 
        stringFilter(str2.ToCharArray()); 

        String str3 = "aaac"; 
        stringFilter(str3.ToCharArray()); 

        String str4 = "react"; 
        stringFilter(str4.ToCharArray()); 

        String str5 = "aa"; 
        stringFilter(str5.ToCharArray()); 

        String str6 = "ababaac"; 
        stringFilter(str6.ToCharArray()); 
    } 
} 

// This code is contributed by 
//PrinciRaj1992 
```

**Output:**

```
Input => ad
Output => ad

Input => acbac
Output =>

Input => aaac
Output => aa

Input => react
Output => ret

Input => aa
Output => aa

Input => ababaac
Output => aaa

Input => abc
Output =>

```

感谢 Gaurav Ahirwar 提出了这个更简单的解决方案。

本文由 [**瓦润耆**](http://in.linkedin.com/pub/varun-jain/18/748/81a) 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论