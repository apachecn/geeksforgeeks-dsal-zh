# 子串反向模式

> 原文:[https://www.geeksforgeeks.org/substring-reverse-pattern/](https://www.geeksforgeeks.org/substring-reverse-pattern/)

给定字符串 **str** ，任务是打印以下示例中给出的图案:

**示例:**

> **输入:** str = "极客"
> **输出:**
> 极客
> *kee*
> **e**
> 极客的反义词是“skeg”
> 将第一个和最后一个字符替换为“*”即*kee*
> 将修改后的字符串中的第二个和最后一个字符替换为**e**
> 以此类推。
> 
> **输入:** str = "first"
> **输出:**
> first
> *sri*
> **r**

**进场:**

*   打印未修改的字符串。
*   反转字符串并初始化 **i = 0** 和**j = n–1**。
*   替换**s[I]= ' ***和**s[j]= ' ***并更新 **i = i + 1** 和**j = j–1**然后打印修改后的字符串。
*   重复上述步骤，同时**j–I>1**。

下面是上述方法的实现:

## C++

```
// C++ program to print the required pattern
#include <bits/stdc++.h>
using namespace std;

// Function to print the required pattern
void printPattern(char s[], int n)
{

    // Print the unmodified string
    cout << s << "\n";

    // Reverse the string
    int i = 0, j = n - 2;
    while (i < j) {
        char c = s[i];
        s[i] = s[j];
        s[j] = c;
        i++;
        j--;
    }

    // Replace the first and last character by '*' then
    // second and second last character and so on
    // until the string has characters remaining
    i = 0;
    j = n - 2;
    while (j - i > 1) {
        s[i] = s[j] = '*';
        cout << s << "\n";
        i++;
        j--;
    }
}

// Driver code
int main()
{
    char s[] = "geeks";
    int n = sizeof(s) / sizeof(s[0]);

    printPattern(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the required pattern
class GFG
{

// Function to print the required pattern
static void printPattern(char[] s, int n)
{
    // Print the unmodified string
    System.out.println(s);

    // Reverse the string
    int i = 0, j = n - 1;
    while (i < j)
    {
        char c = s[i];
        s[i] = s[j];
        s[j] = c;
        i++;
        j--;
    }

    // Replace the first and last character
    // by '*' then second and second last
    // character and so on until the string
    // has characters remaining
    i = 0;
    j = n - 1;
    while (j - i > 1)
    {
        s[i] = s[j] = '*';
        System.out.println(s);
        i++;
        j--;
    }
}

// Driver Code
public static void main(String []args)
{
    char[] s = "geeks".toCharArray();
    int n = s.length;

    printPattern(s, n);
}
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program to print the required pattern

# Function to print the required pattern
def printPattern(s, n):

    # Print the unmodified string
    print(''.join(s))

    # Reverse the string
    i, j = 0, n - 1

    while i < j:
        s[i], s[j] = s[j], s[i]
        i += 1
        j -= 1

    # Replace the first and last character
    # by '*' then second and second last
    # character and so on until the string
    # has characters remaining
    i, j = 0, n - 1

    while j - i > 1:
        s[i], s[j] = '*', '*'
        print(''.join(s))
        i += 1
        j -= 1

# Driver code
if __name__ == "__main__":

    s = "geeks"
    n = len(s)

    printPattern(list(s), n)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to print the required pattern
using System;

class GFG
{

// Function to print the required pattern
static void printPattern(char[] s, int n)
{
    // Print the unmodified string
    Console.WriteLine(s);

    // Reverse the string
    int i = 0, j = n - 1;
    while (i < j)
    {
        char c = s[i];
        s[i] = s[j];
        s[j] = c;
        i++;
        j--;
    }

    // Replace the first and last character
    // by '*' then second and second last
    // character and so on until the string
    // has characters remaining
    i = 0;
    j = n - 1;
    while (j - i > 1)
    {
        s[i] = s[j] = '*';
        Console.WriteLine(s);
        i++;
        j--;
    }
}

// Driver Code
public static void Main(String []args)
{
    char[] s = "geeks".ToCharArray();
    int n = s.Length;

    printPattern(s, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to print the required pattern

// Function to print the required pattern
function printPattern(s, n)
{

    // Print the unmodified string
    document.write( s.join('') + "<br>");

    // Reverse the string
    var i = 0, j = n - 1;
    while (i < j) {
        var c = s[i];
        s[i] = s[j];
        s[j] = c;
        i++;
        j--;
    }

    // Replace the first and last character by '*' then
    // second and second last character and so on
    // until the string has characters remaining
    i = 0;
    j = n - 1;
    while (j - i > 1) {
        s[i] = s[j] = '*';
        document.write( s.join('') + "<br>");
        i++;
        j--;
    }
}

// Driver code
var s = "geeks".split('');
var n = s.length;
printPattern(s, n);

</script>
```

**Output:** 

```
geeks
*kee*
**e**
```