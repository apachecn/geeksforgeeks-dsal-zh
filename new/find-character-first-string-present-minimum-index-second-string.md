# 查找第二个字符串

> 原文：[https://www.geeksforgeeks.org/find-character-first-string-present-minimum-index-second-string/](https://www.geeksforgeeks.org/find-character-first-string-present-minimum-index-second-string/)

中最小索引处出现的第一个字符串中的字符

给定一个字符串`str`和另一个字符串`patt`。 在`patt`中找到出现在`str`中最小索引处的字符。 如果`str`中没有`patt`字符，则打印`"No character present"`。

**示例**：

> **输入**：`str = "geeksforgeeks", patt = "set"`
>
> **输出**：`e`
>
> `patt`的`e`和`s`都出现在`str`中，但是`e`的索引最小，为 **1**。
>
> **输入**：`str = "adcffaet", patt = "onkl"`
>
> **输出**：`"No character present"`

**来源**：[OLA 面试经验 | 系列 12](https://www.geeksforgeeks.org/ola-interview-experience-set-12/) 。

**朴素的方法**：使用两个循环，在`str`中找到`patt`的每个字符的第一个索引。 打印具有最小索引的字符。 如果`str`中没有`patt`字符，则打印“无字符”。

## C++

```cpp

// C++ implementation to find the character in 
// first string that is present at minimum index
// in second string
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum index character
void printMinIndexChar(string str, string patt)
{
    // to store the index of character having
    // minimum index
    int minIndex = INT_MAX;

    // lengths of the two strings
    int m = str.size();
    int n = patt.size();

    // traverse 'patt'
    for (int i = 0; i < n; i++) {

        // for each character of 'patt' traverse 'str'
        for (int j = 0; j < m; j++) {

            // if patt[i] is found in 'str', check if
            // it has the minimum index or not. If yes, 
            // then update 'minIndex' and break
            if (patt[i] == str[j] && j < minIndex) {
                minIndex = j;
                break;
            }
        }
    }

    // print the minimum index character
    if (minIndex != INT_MAX)
        cout << "Minimum Index Character = "
             << str[minIndex];

    // if no character of 'patt' is present in 'str'
    else
        cout << "No character present";
}

// Driver program to test above
int main()
{
    string str = "geeksforgeeks";
    string patt = "set";
    printMinIndexChar(str, patt);
    return 0;
}

```

## Java

```java

// Java implementation to find the character in 
// first string that is present at minimum index
// in second string

public class GFG 
{
    // method to find the minimum index character
    static void printMinIndexChar(String str, String patt)
    {
        // to store the index of character having
        // minimum index
        int minIndex = Integer.MAX_VALUE;

        // lengths of the two strings
        int m = str.length();
        int n = patt.length();

        // traverse 'patt'
        for (int i = 0; i < n; i++) {

            // for each character of 'patt' traverse 'str'
            for (int j = 0; j < m; j++) {

                // if patt.charAt(i)is found in 'str', check if
                // it has the minimum index or not. If yes, 
                // then update 'minIndex' and break
                if (patt.charAt(i)== str.charAt(j) && j < minIndex) {
                    minIndex = j;
                    break;
                }
            }
        }

        // print the minimum index character
        if (minIndex != Integer.MAX_VALUE)
            System.out.println("Minimum Index Character = " +
                                str.charAt(minIndex));

        // if no character of 'patt' is present in 'str'
        else
            System.out.println("No character present");
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        String patt = "set";
        printMinIndexChar(str, patt);
    }
}

```

## Python3

```py

# Python3 implementation to find the character in
# first that is present at minimum index
# in second String

# function to find the minimum index character
def printMinIndexChar(Str, patt):

    # to store the index of character having
    # minimum index
    minIndex = 10**9

    # lengths of the two Strings
    m =len(Str)
    n =len(patt)

    # traverse 'patt'
    for i in range(n):

        # for each character of 'patt' traverse 'Str'
        for j in range(m):

            # if patt[i] is found in 'Str', check if
            # it has the minimum index or not. If yes,
            # then update 'minIndex' and break
            if (patt[i] == Str[j] and j < minIndex):
                minIndex = j
                break

    # print the minimum index character
    if (minIndex != 10**9):
        print("Minimum Index Character = ",Str[minIndex])

    # if no character of 'patt' is present in 'Str'
    else:
        print("No character present")

# Driver code

Str = "geeksforgeeks"
patt = "set"
printMinIndexChar(Str, patt)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# implementation to find the character in 
// first string that is present at minimum index
// in second string
using System;

class GFG
{ 
    // method to find the minimum index character
    static void printMinIndexChar(String str, String patt)
    {
        // to store the index of character having
        // minimum index
        int minIndex = int.MaxValue;

        // lengths of the two strings
        int m = str.Length;
        int n = patt.Length;

        // traverse 'patt'
        for (int i = 0; i < n; i++) {

            // for each character of 'patt' traverse 'str'
            for (int j = 0; j < m; j++) {

                // if patt.charAt(i)is found in 'str', check if
                // it has the minimum index or not. If yes, 
                // then update 'minIndex' and break
                if (patt[i]== str[j] && j < minIndex) {
                    minIndex = j;
                    break;
                }
            }
        }

        // print the minimum index character
        if (minIndex != int.MaxValue)
            Console.WriteLine("Minimum Index Character = " +
                                str[minIndex]);

        // if no character of 'patt' is present in 'str'
        else
            Console.WriteLine("No character present");
    }

    // Driver Methoda
    public static void Main()
    {
        String str = "geeksforgeeks";
        String patt = "set";
        printMinIndexChar(str, patt);
    }
}
// This code is contributed by Sam007

```

**输出**：

```
Minimum Index Character = e

```

**时间复杂度**：`O(mn)`，其中`m`和`n`是两个字符串的长度。

**辅助空间**：`O(1)`

**方法 2 有效方法（散列）**：

*   用（键，值）元组表示为（字符，索引）元组创建哈希表。

*   将`str`的每个字符的第一个索引存储在哈希表中。

*   现在，对于`patt`的每个字符，检查其是否在哈希表中。

    *   如果存在，则从哈希表中获取其索引，并更新`minIndex`（到目前为止遇到的最小索引）。

    *   对于不匹配的字符，请打印“不存在字符”。

哈希表是使用 C++ 中的[`unordered_set`](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)实现的。

下图是上述方法的模拟：

![](img/3e573678674decc4ea707509c440194d.png)

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the character in first 
// string that is present at minimum index in second
// string
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum index character
void printMinIndexChar(string str, string patt)
{
    // unordered_map 'um' implemented as hash table
    unordered_map<char, int> um;

    // to store the index of character having
    // minimum index
    int minIndex = INT_MAX;

    // lengths of the two strings
    int m = str.size();
    int n = patt.size();-

    // store the first index of each character of 'str'
    for (int i = 0; i < m; i++)
        if (um.find(str[i]) == um.end())
            um[str[i]] = i;

    // traverse the string 'patt'
    for (int i = 0; i < n; i++)

        // if patt[i] is found in 'um', check if 
        // it has the minimum index or not accordingly 
        // update 'minIndex'
        if (um.find(patt[i]) != um.end() && 
            um[patt[i]] < minIndex)
            minIndex = um[patt[i]];

    // print the minimum index character
    if (minIndex != INT_MAX)
        cout << "Minimum Index Character = "
             << str[minIndex];

    // if no character of 'patt' is present in 'str'
    else
        cout << "No character present";
}

// Driver program to test above
int main()
{
    string str = "geeksforgeeks";
    string patt = "set";
    printMinIndexChar(str, patt);
    return 0;
}

```

## Java

```java

// Java implementation to find the character in 
// first string that is present at minimum index
// in second string

import java.util.HashMap;

public class GFG 
{
    // method to find the minimum index character
    static void printMinIndexChar(String str, String patt)
    {
        // map to store the first index of each character of 'str'
        HashMap<Character, Integer> hm = new HashMap<>();

        // to store the index of character having
        // minimum index
        int minIndex = Integer.MAX_VALUE;

        // lengths of the two strings
        int m = str.length();
        int n = patt.length();

        // store the first index of each character of 'str'
        for (int i = 0; i < m; i++)
            if(!hm.containsKey(str.charAt(i)))
                hm.put(str.charAt(i),i);

        // traverse the string 'patt'
        for (int i = 0; i < n; i++)
            // if patt[i] is found in 'um', check if 
            // it has the minimum index or not accordingly 
            // update 'minIndex'
            if (hm.containsKey(patt.charAt(i)) && 
                hm.get(patt.charAt(i)) < minIndex)
                minIndex = hm.get(patt.charAt(i));

        // print the minimum index character
        if (minIndex != Integer.MAX_VALUE)
            System.out.println("Minimum Index Character = " +
                                str.charAt(minIndex));

        // if no character of 'patt' is present in 'str'
        else
            System.out.println("No character present");
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        String patt = "set";
        printMinIndexChar(str, patt);
    }
}

```

## Python3

```py

# Python3 implementation to 
# find the character in first 
# string that is present at
# minimum index in second string
import sys

# Function to find the 
# minimum index character
def printMinIndexChar(st, patt):

    # unordered_map 'um' 
    # implemented as hash table
    um = {}

    # to store the index of 
    # character having minimum index
    minIndex = sys.maxsize

    # Lengths of the two strings
    m = len(st)
    n = len(patt)

    # Store the first index of 
    # each character of 'str'
    for i in range (m):
        if (st[i] not in um):
            um[st[i]] = i

    # traverse the string 'patt'
    for i in range(n):

        # If patt[i] is found in 'um', 
        # check if  it has the minimum 
        # index or not accordingly 
        # update 'minIndex'
        if (patt[i] in um and
            um[patt[i]] < minIndex):
            minIndex = um[patt[i]]

    # Print the minimum index character
    if (minIndex != sys.maxsize):
        print ("Minimum Index Character = ", 
                st[minIndex])

    # If no character of 'patt'
    # is present in 'str'
    else:
        print ("No character present")

# Driver program to test above
if __name__ == "__main__":

  st = "geeksforgeeks"
  patt = "set"
  printMinIndexChar(st, patt)

# This code is contributed by Chitranayal

```

## C#

```cs

// C# implementation to find the character in 
// first string that is present at minimum index
// in second string
using System;
using System.Collections.Generic;

class GFG 
{
    // method to find the minimum index character
    static void printMinIndexChar(String str, String patt)
    {
        // map to store the first index of 
        // each character of 'str'
        Dictionary<char, 
                   int> hm = new Dictionary<char, 
                                            int>();

        // to store the index of character having
        // minimum index
        int minIndex = int.MaxValue;

        // lengths of the two strings
        int m = str.Length;
        int n = patt.Length;

        // store the first index of 
        // each character of 'str'
        for (int i = 0; i < m; i++)
            if(!hm.ContainsKey(str[i]))
                hm.Add(str[i], i);

        // traverse the string 'patt'
        for (int i = 0; i < n; i++)

            // if patt[i] is found in 'um', 
            // check if it has the minimum index 
            // or not, accordingly update 'minIndex'
            if (hm.ContainsKey(patt[i]) && 
                hm[patt[i]] < minIndex)
                minIndex = hm[patt[i]];

        // print the minimum index character
        if (minIndex != int.MaxValue)
            Console.WriteLine("Minimum Index Character = " +
                                             str[minIndex]);

        // if no character of 'patt' is present in 'str'
        else
            Console.WriteLine("No character present");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        String patt = "set";
        printMinIndexChar(str, patt);
    }
}

// This code is contributed by Princi Singh

```

**输出**：

```
Minimum Index Character = e

```

**时间复杂度**：`O(m + n)`，其中`m`和`n`是两个字符串的长度。

**辅助空间**：`O(d)`，其中`d`是哈希表的大小，它是`str`中不同字符的计数。

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，也可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

