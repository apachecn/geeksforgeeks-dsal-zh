# 第一次出现在最左边的重复字符

> 原文:[https://www . geesforgeks . org/repeated-character-其第一次出现是在最左侧/](https://www.geeksforgeeks.org/repeated-character-whose-first-appearance-is-leftmost/)

给定一个字符串，找到字符串中最先出现的重复字符。

![](img/95197010ef5efff430f0ebc4eb3bf562.png)

**例:**

```
Input  : geeksforgeeks
Output : g
(mind that it will be g, not e.)

Input  : abcdabcd
Output : a

Input  : abcd
Output : -1
No character repeats
```

**问于:高盛实习**

我们已经在[中讨论了不同的方法，首先在字符串](https://www.geeksforgeeks.org/find-repeated-character-present-first-string/)中找到重复的字符。
**如何利用输入字符串的一次遍历来解决这个问题？**
**方法 1(从左向右遍历)**我们从左向右遍历字符串。我们跟踪每个字符最左边的索引。如果一个字符重复，我们将它的左边的索引与当前结果进行比较，如果结果大于
则更新结果

## C++

```
// CPP program to find first repeating
// character
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

/* The function returns index of the first
repeating character in a string. If
all characters are repeating then
returns -1 */
int firstRepeating(string& str)
{
    // Initialize leftmost index of every
    // character as -1.
    int firstIndex[NO_OF_CHARS];
    for (int i = 0; i < NO_OF_CHARS; i++)
        firstIndex[i] = -1;

    // Traverse from left and update result
    // if we see a repeating character whose
    // first index is smaller than current
    // result.
    int res = INT_MAX;
    for (int i = 0; i < str.length(); i++) {
        if (firstIndex[str[i]] == -1)
           firstIndex[str[i]] = i;
        else
           res = min(res, firstIndex[str[i]]);
    }

    return (res == INT_MAX) ? -1 : res;
}

/* Driver program to test above function */
int main()
{
    string str = "geeksforgeeks";
    int index = firstRepeating(str);
    if (index == -1)
        printf("Either all characters are "
               "distinct or string is empty");
    else
        printf("First Repeating character"
               " is %c",
               str[index]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first repeating
// character

class GFG
{

    static int NO_OF_CHARS = 256;

    /* The function returns index of the first
    repeating character in a string. If
    all characters are repeating then
    returns -1 */
    static int firstRepeating(char[] str)
    {
        // Initialize leftmost index of every
        // character as -1.
        int[] firstIndex = new int[NO_OF_CHARS];
        for (int i = 0; i < NO_OF_CHARS; i++)
        {
            firstIndex[i] = -1;
        }

        // Traverse from left and update result
        // if we see a repeating character whose
        // first index is smaller than current
        // result.
        int res = Integer.MAX_VALUE;
        for (int i = 0; i < str.length; i++)
        {
            if (firstIndex[str[i]] == -1)
            {
                firstIndex[str[i]] = i;
            }
            else
            {
                res = Math.min(res, firstIndex[str[i]]);
            }
        }

        return (res == Integer.MAX_VALUE) ? -1 : res;
    }

    /* Driver code */
    public static void main(String[] args)
    {
        char[] str = "geeksforgeeks".toCharArray();
        int index = firstRepeating(str);
        if (index == -1)
        {
            System.out.printf("Either all characters are "
                    + "distinct or string is empty");
        }
        else
        {
            System.out.printf("First Repeating character"
                    + " is %c", str[index]);
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find first repeating
# character
import sys

NO_OF_CHARS = 256

# The function returns index of the first
# repeating character in a string. If
# all characters are repeating then
# returns -1 */
def firstRepeating(str):

    # Initialize leftmost index of every
    # character as -1.
    firstIndex = [0 for i in range(NO_OF_CHARS)]
    for i in range(NO_OF_CHARS):
        firstIndex[i] = -1

    # Traverse from left and update result
    # if we see a repeating character whose
    # first index is smaller than current
    # result.
    res = sys.maxsize
    for i in range(len(str)):
        if (firstIndex[ord(str[i])] == -1):
            firstIndex[ord(str[i])] = i
        else:
            res = min(res, firstIndex[ord(str[i])])

    if res == sys.maxsize:
        return -1
    else:
        return res

# Driver function
if __name__ == '__main__':
    str = "geeksforgeeks"
    index = firstRepeating(str)
    if (index == -1):
        print("Either all characters are distinct or string is empty")
    else:
        print("First Repeating character is",str[index])

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find first repeating
// character
using System;
using System.Collections.Generic;

class GFG
{

    static int NO_OF_CHARS = 256;

    /* The function returns index of the first
    repeating character in a string. If
    all characters are repeating then
    returns -1 */
    static int firstRepeating(char[] str)
    {
        // Initialize leftmost index of every
        // character as -1.
        int[] firstIndex = new int[NO_OF_CHARS];
        for (int i = 0; i < NO_OF_CHARS; i++)
        {
            firstIndex[i] = -1;
        }

        // Traverse from left and update result
        // if we see a repeating character whose
        // first index is smaller than current
        // result.
        int res = int.MaxValue;
        for (int i = 0; i < str.Length; i++)
        {
            if (firstIndex[str[i]] == -1)
            {
                firstIndex[str[i]] = i;
            }
            else
            {
                res = Math.Min(res, firstIndex[str[i]]);
            }
        }

        return (res == int.MaxValue) ? -1 : res;
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        char[] str = "geeksforgeeks".ToCharArray();
        int index = firstRepeating(str);
        if (index == -1)
        {
            Console.Write("Either all characters are "
                    + "distinct or string is empty");
        }
        else
        {
            Console.Write("First Repeating character"
                    + " is {0}", str[index]);
        }
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program to find first repeating character

    let NO_OF_CHARS = 256;

    /* The function returns index of the first
    repeating character in a string. If
    all characters are repeating then
    returns -1 */
    function firstRepeating(str)
    {
        // Initialize leftmost index of every
        // character as -1.
        let firstIndex = new Array(NO_OF_CHARS);
        for (let i = 0; i < NO_OF_CHARS; i++)
        {
            firstIndex[i] = -1;
        }

        // Traverse from left and update result
        // if we see a repeating character whose
        // first index is smaller than current
        // result.
        let res = Number.MAX_VALUE;
        for (let i = 0; i < str.length; i++)
        {
            if (firstIndex[str[i].charCodeAt()] == -1)
            {
                firstIndex[str[i].charCodeAt()] = i;
            }
            else
            {
                res = Math.min(res, firstIndex[str[i].charCodeAt()]);
            }
        }

        return (res == Number.MAX_VALUE) ? -1 : res;
    }

    let str = "geeksforgeeks".split('');
    let index = firstRepeating(str);
    if (index == -1)
    {
      document.write("Either all characters are "
                    + "distinct or string is empty");
    }
    else
    {
      document.write("First Repeating character is " + str[index]);
    }

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
First Repeating character is g
```

时间复杂度:O(n)。它只遍历一次输入字符串。
辅助空间:O(1)
**方法 2(从右向左遍历)**我们从右向左遍历字符串。我们跟踪被访问的角色。如果一个字符重复，我们会更新结果。

## C++

```
// CPP program to find first repeating
// character
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

/* The function returns index of the first
repeating character in a string. If
all characters are repeating then
returns -1 */
int firstRepeating(string& str)
{
    // Mark all characters as not visited
    bool visited[NO_OF_CHARS];
    for (int i = 0; i < NO_OF_CHARS; i++)
        visited[i] = false;

    // Traverse from right and update res as soon
    // as we see a visited character.
    int res = -1;
    for (int i = str.length() - 1; i >= 0; i--) {
        if (visited[str[i]] == false)
            visited[str[i]] = true;
        else
            res = i;
    }

    return res;
}

/* Driver program to test above function */
int main()
{
    string str = "geeksforgeeks";
    int index = firstRepeating(str);
    if (index == -1)
        printf("Either all characters are "
               "distinct or string is empty");
    else
        printf("First Repeating character"
               " is %c",
               str[index]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first repeating
// character
import java.util.*;

class GFG
{

static int NO_OF_CHARS= 256;

/* The function returns index of the first
repeating character in a string. If
all characters are repeating then
returns -1 */
static int firstRepeating(String str)
{
    // Mark all characters as not visited
    boolean []visited = new boolean[NO_OF_CHARS];
    for (int i = 0; i < NO_OF_CHARS; i++)
        visited[i] = false;

    // Traverse from right and update res as soon
    // as we see a visited character.
    int res = -1;
    for (int i = str.length() - 1; i >= 0; i--)
    {
        if (visited[str.charAt(i)] == false)
            visited[str.charAt(i)] = true;
        else
            res = i;
    }

    return res;
}

/* Driver code */
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int index = firstRepeating(str);
    if (index == -1)
        System.out.printf("Either all characters are "
            +"distinct or string is empty");
    else
        System.out.printf("First Repeating character"
            +" is %c",
            str.charAt(index));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find first
# repeating character

NO_OF_CHARS = 256

""" The function returns index of the first
repeating character in a string. If
all characters are repeating then
returns -1 """

def firstRepeating(string) :

    # Mark all characters as not visited
    visited = [False] * NO_OF_CHARS;

    for i in range(NO_OF_CHARS) :
        visited[i] = False;

    # Traverse from right and update res as soon
    # as we see a visited character.
    res = -1;
    for i in range(len(string)-1, -1 , -1) :
        if (visited[string.index(string[i])] == False):
            visited[string.index(string[i])] = True;

        else:
            res = i;

    return res;

# Driver program to test above function
if __name__ == "__main__" :

    string = "geeksforgeeks";
    index = firstRepeating(string);

    if (index == -1) :
        print("Either all characters are" ,
        "distinct or string is empty");
    else :
        print("First Repeating character is:", string[index]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find first repeating
// character
using System;

class GFG
{

static int NO_OF_CHARS = 256;

/* The function returns index of the first
repeating character in a string. If
all characters are repeating then
returns -1 */
static int firstRepeating(String str)
{
    // Mark all characters as not visited
    Boolean []visited = new Boolean[NO_OF_CHARS];
    for (int i = 0; i < NO_OF_CHARS; i++)
        visited[i] = false;

    // Traverse from right and update res as soon
    // as we see a visited character.
    int res = -1;
    for (int i = str.Length - 1; i >= 0; i--)
    {
        if (visited[str[i]] == false)
            visited[str[i]] = true;
        else
            res = i;
    }

    return res;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int index = firstRepeating(str);
    if (index == -1)
        Console.Write("Either all characters are " +
                      "distinct or string is empty");
    else
        Console.Write("First Repeating character" +
                      " is {0}", str[index]);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to find first repeating character

    let NO_OF_CHARS = 256;

    /* The function returns index of the first
    repeating character in a string. If
    all characters are repeating then
    returns -1 */
    function firstRepeating(str)
    {
        // Mark all characters as not visited
        let visited = new Array(NO_OF_CHARS);
        for (let i = 0; i < NO_OF_CHARS; i++)
            visited[i] = false;

        // Traverse from right and update res as soon
        // as we see a visited character.
        let res = -1;
        for (let i = str.length - 1; i >= 0; i--)
        {
            if (visited[str[i].charCodeAt()] == false)
                visited[str[i].charCodeAt()] = true;
            else
                res = i;
        }

        return res;
    }

    let str = "geeksforgeeks";
    let index = firstRepeating(str);
    if (index == -1)
        document.write("Either all characters are " +
                      "distinct or string is empty");
    else
        document.write("First Repeating character" +
                      " is " + str[index]);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
First Repeating character is g
```

**时间复杂度:** O(n)。它只遍历一次输入字符串。
**辅助空间:** O(1)
方法 2 比方法 1 好，因为它做的比较少。