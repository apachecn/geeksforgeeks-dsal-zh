# 根据给定的索引重新排列字符串

> 原文:[https://www . geeksforgeeks . org/根据给定的索引重新排列字符串/](https://www.geeksforgeeks.org/rearrange-a-string-according-to-the-given-indices/)

给定一个字符串 **S** 和一个数组**索引[]** ，任务是通过将每个字符**S【I】**放置到**索引【I】**来重新排列字符串 **S** 。
**例**

> **输入:**S =“geeks forgeeks”，index[] = {5，6，7，0，1，2，8，9，10，3，4，11，12}
> **输出:**ksfeegeorgks
> **输入:**S =“math”，index[] = {0，1，2，3}
> **输出:** math

**方法:**
要解决问题，请按照下面给出的步骤操作:

*   将字符串 **S** 转换为[列表](https://www.geeksforgeeks.org/python-list/)字符，因为字符串本质上是不可变的。
*   复制列表。根据**索引【I】**中的值重新排列列表中的字符。
*   将列表转换为字符串并打印最终字符串。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert the strings
// to proper
void Convertstrings(string s, int index[],
                              int n)
{
    char a[s.length()];
    char b[s.length()];

    // Convert string to array
    for(int ii = 0; ii < s.length(); ii++)
    {
        a[ii] = s[ii];
        b[ii] = s[ii];
    }

    int i = 0, j = 0;

    // Move characters to specified indices
    while(j < s.length() && i < n)
    {
        int k = index[i];
        int temp = a[j];
        b[k] = temp;

        j += 1;
        i += 1;
    }

    string tmp = "";

    // Convert the list to string
    for(i = 0; i < s.length(); i++)
    {
        tmp += b[i];
    }

    // Print the answer
    cout << tmp << endl;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";
    int index[] = { 5, 6, 7, 0, 1, 2, 8,
                    9, 10, 3, 4, 11, 12};

    int n = sizeof(index) / sizeof(index[0]);

    Convertstrings(s, index, n);
    return 0;
}

// This code is contributed by rutvik_56   
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to convert the Strings
// to proper
static void ConvertStrings(char []s,
                           int index[],
                           int n)
{
    char []a = new char[s.length];
    char []b = new char[s.length];

    // Convert String to array
    for(int ii = 0; ii < s.length; ii++)
    {
        a[ii] = s[ii];
        b[ii] = s[ii];
    }

    int i = 0, j = 0;

    // Move characters to specified indices
    while(j < s.length && i < n)
    {
        int k = index[i];
        int temp = a[j];
        b[k] = (char) temp;

        j += 1;
        i += 1;
    }

    String tmp = "";

    // Convert the list to String
    for(i = 0; i < s.length; i++)
    {
        tmp += b[i];
    }

    // Print the answer
    System.out.print(tmp +"\n");
}

// Driver Code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    int index[] = { 5, 6, 7, 0, 1, 2, 8,
                    9, 10, 3, 4, 11, 12};

    int n = index.length;

    ConvertStrings(s.toCharArray(), index, n);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to convert the strings
# to proper
def Convertstrings(s, index):
    a = []
    j = 0
    i = 0

    # Convert string to list
    for ii in str(s):
        a.append(ii)

    # Copy the list to another list
    b = a[:]

    # Move characters to specified indices
    while j < len(a) and i < len(index):
        k = index[i]
        temp = a[j]
        b[k] = temp
        j += 1
        i += 1
    s = ''

    # Convert the list to string
    for i in range(len(b)):
        s += b[i]

    # Print the answer
    print(s)

# Driver Code
s = "geeksforgeeks"
index = [5, 6, 7, 0, 1, 2, 8, 9, 10, 3, 4, 11, 12]
Convertstrings(s, index)
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to convert the Strings
// to proper
static void ConvertStrings(char []s,
                           int []index,
                           int n)
{
    char []a = new char[s.Length];
    char []b = new char[s.Length];

    // Convert String to array
    for(int ii = 0; ii < s.Length; ii++)
    {
        a[ii] = s[ii];
        b[ii] = s[ii];
    }

    int i = 0, j = 0;

    // Move characters to specified indices
    while(j < s.Length && i < n)
    {
        int k = index[i];
        int temp = a[j];
        b[k] = (char) temp;

        j += 1;
        i += 1;
    }

    String tmp = "";

    // Convert the list to String
    for(i = 0; i < s.Length; i++)
    {
        tmp += b[i];
    }

    // Print the answer
    Console.Write(tmp +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    String s = "geeksforgeeks";
    int []index = { 5, 6, 7, 0, 1, 2, 8,
                    9, 10, 3, 4, 11, 12};

    int n = index.Length;

    ConvertStrings(s.ToCharArray(), index, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to implement the above approach

    // Function to convert the Strings to proper
    function ConvertStrings(s, index, n)
    {
        let a = new Array(s.length);
        a.fill('0');
        let b = new Array(s.length);
        b.fill('0');

        // Convert String to array
        for(let ii = 0; ii < s.length; ii++)
        {
            a[ii] = s[ii];
            b[ii] = s[ii];
        }

        let i = 0, j = 0;

        // Move characters to specified indices
        while(j < s.length && i < n)
        {
            let k = index[i];
            let temp = a[j].charCodeAt();
            b[k] = String.fromCharCode(temp);

            j += 1;
            i += 1;
        }

        let tmp = "";

        // Convert the list to String
        for(i = 0; i < s.length; i++)
        {
            tmp = tmp + b[i];
        }

        // Print the answer
        document.write(tmp +"</br>");
    }

    let s = "geeksforgeeks";
    let index = [ 5, 6, 7, 0, 1, 2, 8, 9, 10, 3, 4, 11, 12];

    let n = index.length;

    ConvertStrings(s.split(''), index, n);

</script>
```

**Output:** 

```
ksfeegeeorgks
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*