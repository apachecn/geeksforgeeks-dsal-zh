# 复制字符串的函数(迭代和递归)

> 原文:[https://www . geesforgeks . org/function-copy-string-iterative-recursive/](https://www.geeksforgeeks.org/function-copy-string-iterative-recursive/)

给定两个字符串，使用递归将一个字符串复制到另一个字符串。我们基本上需要用 C/C++ 编写自己的递归版本 [strcpy](https://www.geeksforgeeks.org/strcpy-in-c-cpp/)

**示例:**

```
Input : s1 = "hello"
        s2 = "geeksforgeeks"
Output : s2 = "hello"

Input :  s1 = "geeksforgeeks"
         s2 = ""
Output : s2 = "geeksforgeeks"
```

**迭代:**
从 index = 0 开始将每个字符从 s1 复制到 s2，并在每次调用中将 index 增加 1，直到 s1 没有到达终点；

## C++

```
// Iterative CPP Program to copy one String 
// to another.
#include <bits/stdc++.h>
using namespace std;

// Function to copy one string to other
// assuming that other string has enough
// space.
void myCopy(char s1[], char s2[])
{
    int i = 0;
    for (i=0; s1[i] != '\0'; i++)
       s2[i] = s1[i];
    s2[i] = '\0';
}

// Driver function
int main()
{
    char s1[100] = "GEEKSFORGEEKS";
    char s2[100] = "";
    myCopy(s1, s2);
    cout << s2;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java Program to copy one String
// to another.
class GFG
{

// Function to copy one string to other
// assuming that other string has enough
// space.
static void myCopy(char s1[], char s2[])
{
    int i = 0;
    for (i = 0; i < s1.length; i++)
         s2[i] = s1[i];
}

// Driver code
public static void main(String[] args)
{
    char s1[] = "GEEKSFORGEEKS".toCharArray();
    char s2[] = new char[s1.length];
    myCopy(s1, s2);
    System.out.println(String.valueOf(s2));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# recursive Python Program to copy one String
# to another.

# Function to copy one string to other
def copy_str(x,y):
    if len(y)==0:
        return x
    else:
        c = copy_str(x,(y)[1:-1])
        return c
x = input()
y = input()
print(copy_str(x,y))

# This code contributed by deeksha20049@iiid.ac.in
#deeksha20049
```

## C#

```
// Iterative C# Program to copy one String
// to another.
using System;

class GFG
{

// Function to copy one string to other
// assuming that other string has enough
// space.
static void myCopy(char []s1, char []s2)
{
    int i = 0;
    for (i = 0; i < s1.Length; i++)
        s2[i] = s1[i];
}

// Driver code
public static void Main(String[] args)
{
    char []s1 = "GEEKSFORGEEKS".ToCharArray();
    char []s2 = new char[s1.Length];
    myCopy(s1, s2);
    Console.WriteLine(String.Join("", s2));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Iterative Javascript Program to copy one String
// to another.

// Function to copy one string to other
// assuming that other string has enough
// space.
function myCopy(s1, s2)
{
    let i = 0;
    for (i = 0; i < s1.length; i++)
         s2[i] = s1[i];
}

// Driver code
    // Driver Code
let s1 = "GEEKSFORGEEKS";
let s2 = [];
let index = 0;

myCopy(s1, s2, index);

document.write(s2.join(""));

// This code contributed by shivanisinghss2110

</script>
```

**Output:** 

```
GEEKSFORGEEKS
```