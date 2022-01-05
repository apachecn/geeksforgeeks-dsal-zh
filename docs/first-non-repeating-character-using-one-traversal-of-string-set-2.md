# 使用字符串的一次遍历的第一个非重复字符|集合 2

> 原文:[https://www . geesforgeks . org/first-非重复字符-使用字符串集的一次遍历-2/](https://www.geeksforgeeks.org/first-non-repeating-character-using-one-traversal-of-string-set-2/)

给定一个字符串，找到其中的第一个非重复字符。例如，如果输入字符串是“极客”，那么输出应该是“f”，如果输入字符串是“极客”，那么输出应该是“G”。

![find-first-non-repeated-character-in-a-string](img/b6a262da4da0b0bf9c7db07dcb1adecc.png)

我们已经在[中讨论了两种解决方案，给定一个字符串，找到它的第一个非重复字符](https://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)。本文讨论了一个进一步优化的解决方案(相对于前一篇文章的[方法 2)。想法是优化空间。我们不是使用一对来存储计数和索引，而是使用存储索引的单个元素。如果一个元素出现一次，则存储负值。](https://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/) 

## C++

```
// CPP program to find first non-repeating
// character using 1D array and one traversal.
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

/* The function returns index of the first
non-repeating character in a string. If
all characters are repeating then
returns INT_MAX */
int firstNonRepeating(char* str)
{

    // Initialize all characters as
    // absent.
    int arr[NO_OF_CHARS];
    for (int i = 0; i < NO_OF_CHARS; i++)
        arr[i] = -1;

    // After below loop, the value of
    // arr[x] is going to be index of
    // of x if x appears only once. Else
    // the value is going to be either
    // -1 or -2.
    for (int i = 0; str[i]; i++) {
        if (arr[str[i]] == -1)
            arr[str[i]] = i;
        else
            arr[str[i]] = -2;
    }

    int res = INT_MAX;
    for (int i = 0; i < NO_OF_CHARS; i++)

        // If this character occurs only
        // once and appears before the
        // current result, then update the
        // result
        if (arr[i] >= 0)
            res = min(res, arr[i]);

    return res;
}

/* Driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    int index = firstNonRepeating(str);
    if (index == INT_MAX)
        cout <<"Either all characters are "
               "repeating or string is empty";
    else
        cout <<"First non-repeating character"
               " is "<< str[index];
    return 0;
}

// This code is contributed by shivanisinghss210
```

## C

```
// CPP program to find first non-repeating
// character using 1D array and one traversal.
#include <limits.h>
#include <stdio.h>
#include <math.h>
#define NO_OF_CHARS 256

/* The function returns index of the first
non-repeating character in a string. If
all characters are repeating then
returns INT_MAX */
int firstNonRepeating(char* str)
{
    // Initialize all characters as
    // absent.
    int arr[NO_OF_CHARS];
    for (int i = 0; i < NO_OF_CHARS; i++)
        arr[i] = -1;

    // After below loop, the value of
    // arr[x] is going to be index of
    // of x if x appears only once. Else
    // the value is going to be either
    // -1 or -2.
    for (int i = 0; str[i]; i++) {
        if (arr[str[i]] == -1)
            arr[str[i]] = i;
        else
            arr[str[i]] = -2;
    }

    int res = INT_MAX;
    for (int i = 0; i < NO_OF_CHARS; i++)

        // If this character occurs only
        // once and appears before the
        // current result, then update the
        // result
        if (arr[i] >= 0)
            res = min(res, arr[i]);

    return res;
}

/* Driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    int index = firstNonRepeating(str);
    if (index == INT_MAX)
        printf("Either all characters are "
               "repeating or string is empty");
    else
        printf("First non-repeating character"
               " is %c", str[index]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first
// non-repeating character
// using 1D array and one
// traversal.
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
/* The function returns index
of the first non-repeating
character in a string. If
all characters are repeating
then returns INT_MAX */
static int firstNonRepeating(String str)
{
    int NO_OF_CHARS = 256;

    // Initialize all characters
    // as absent.
    int arr[] = new int[NO_OF_CHARS];
    for (int i = 0;
             i < NO_OF_CHARS; i++)
        arr[i] = -1;

    // After below loop, the
    // value of arr[x] is going
    // to be index of x if x
    // appears only once. Else
    // the value is going to be
    // either -1 or -2.
    for (int i = 0;
             i < str.length(); i++)
    {
        if (arr[str.charAt(i)] == -1)
            arr[str.charAt(i)] = i;
        else
            arr[str.charAt(i)] = -2;
    }

    int res = Integer.MAX_VALUE;
    for (int i = 0; i < NO_OF_CHARS; i++)

        // If this character occurs
        // only once and appears before
        // the current result, then
        // update the result
        if (arr[i] >= 0)
            res = Math.min(res, arr[i]);

    return res;
}

// Driver Code
public static void main(String args[])
{
    String str = "geeksforgeeks";

    int index = firstNonRepeating(str);
    if (index == Integer.MAX_VALUE)
        System.out.print("Either all characters are " +
                       "repeating or string is empty");
    else
        System.out.print("First non-repeating character"+
                             " is " + str.charAt(index));
}
}
```

## 蟒蛇 3

```
'''
Python3 implementation to find non repeating character using
1D array and one traversal'''
import math as mt

NO_OF_CHARS = 256

'''
The function returns index of the first
non-repeating character in a string. If
all characters are repeating then
returns INT_MAX '''

def firstNonRepeating(string):
    #initialize all character as absent

    arr=[-1 for i in range(NO_OF_CHARS)]

    '''
    After below loop, the value of
    arr[x] is going to be index of
    of x if x appears only once. Else
    the value is going to be either
    -1 or -2.'''

    for i in range(len(string)):
        if arr[ord(string[i])]==-1:
            arr[ord(string[i])]=i
        else:
            arr[ord(string[i])]=-2
    res=10**18

    for i in range(NO_OF_CHARS):
        '''
        If this character occurs only
        once and appears before the
        current result, then update the
        result'''
        if arr[i]>=0:
            res=min(res,arr[i])
    return res

#Driver prohram to test above function

string="geeksforgeeks"

index=firstNonRepeating(string)

if index==10**18:
    print("Either all characters are repeating or string is empty")
else:
    print("First non-repeating character is",string[index])

#this code is contributed by Mohit Kumar 29

```

## C#

```
// C# program to find first
// non-repeating character
// using 1D array and one
// traversal.
using System;

class GFG
{
    /* The function returns index
    of the first non-repeating
    character in a string. If
    all characters are repeating
    then returns INT_MAX */
    static int firstNonRepeating(String str)
    {
        int NO_OF_CHARS = 256;

        // Initialize all characters
        // as absent.
        int []arr = new int[NO_OF_CHARS];
        for (int i = 0; i < NO_OF_CHARS; i++)
            arr[i] = -1;

        // After below loop, the
        // value of arr[x] is going
        // to be index of x if x
        // appears only once. Else
        // the value is going to be
        // either -1 or -2.
        for (int i = 0; i < str.Length; i++)
        {
            if (arr[str[i]] == -1)
                arr[str[i]] = i;
            else
                arr[str[i]] = -2;
        }

        int res = int.MaxValue;
        for (int i = 0; i < NO_OF_CHARS; i++)

            // If this character occurs
            // only once and appears before
            // the current result, then
            // update the result
            if (arr[i] >= 0)
                res = Math.Min(res, arr[i]);

        return res;
    }

    // Driver Code
    public static void Main()
    {
        String str = "geeksforgeeks";
        int index = firstNonRepeating(str);
        if (index == int.MaxValue)
            Console.Write("Either all characters are " +
                        "repeating or string is empty");
        else
            Console.Write("First non-repeating character"+
                                " is " + str[index]);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find first
// non-repeating character
// using 1D array and one
// traversal.

    /* The function returns index
of the first non-repeating
character in a string. If
all characters are repeating
then returns INT_MAX */
    function firstNonRepeating(str)
    {
        let NO_OF_CHARS = 256;

    // Initialize all characters
    // as absent.
    let arr = new Array(NO_OF_CHARS);
    for (let i = 0;
             i < NO_OF_CHARS; i++)
        arr[i] = -1;

    // After below loop, the
    // value of arr[x] is going
    // to be index of x if x
    // appears only once. Else
    // the value is going to be
    // either -1 or -2.
    for (let i = 0;
             i < str.length; i++)
    {
        if (arr[str[i].charCodeAt(0)] == -1)
            arr[str[i].charCodeAt(0)] = i;
        else
            arr[str[i].charCodeAt(0)] = -2;
    }

    let res = Number.MAX_VALUE;
    for (let i = 0; i < NO_OF_CHARS; i++)

        // If this character occurs
        // only once and appears before
        // the current result, then
        // update the result
        if (arr[i] >= 0)
            res = Math.min(res, arr[i]);

    return res;
    }

    // Driver Code
    let str = "geeksforgeeks";
    let index = firstNonRepeating(str);
    if (index == Number.MAX_VALUE)
        document.write("Either all characters are " +
                       "repeating or string is empty");
    else
        document.write("First non-repeating character"+
                             " is " + str[index]);

// This code is contributed by patel2127

</script>
```

**Output**

```
First non-repeating character is f
```

**时间复杂度:**O(n)
T3】交替实现

这是使用哈希映射或哈希技术编码的。

如果元素(或键)在字符串中重复，哈希映射(或字典)会将该键的值更改为无。

这样，我们以后只能找到值为“非无”的键。

## 蟒蛇 3

```
# Python implementation of
# above approach
from collections import Counter

def makeHashMap(string):

    # Use Counter to make a frequency
    # dictionary of characters in a string.

    d1 = Counter(string)

    # Update value of each key such that
    # if frequency of  frequency of  a key
    # is equal to 1, then it is set to 0,
    # else set the value equal to None
    d1 = {(key): (0 if d1[key] == 1 else None)
          for key, value in d1.items()}

    return d1

def firstNotRepeatingCharacter(s):

    d = makeHashMap(s)

    # variable to store the first
    # non repeating character.
    nonRep = None

    # Traversing through the string only once.
    for i in s:
        if d[i] is not None:

            '''
            As soon as the first character in the string is
            found whose value in the HashMap is "not None",
            that is our first non-repeating character.
            So we store it in nonRep and break out of the
            loop. Thus saving on time.
            '''
            nonRep = i
            break

    if nonRep is not None:
        return nonRep
    else:

        # If there are no non-repeating characters
        # then "_" is returned
        return str("_")

# Driver Code
print(firstNotRepeatingCharacter('bbcdcca'))

# This code is contributed by Vivek Nigam (@viveknigam300)
```

**Output**

```
d
```

**时间复杂度:** O(N)

#### **方法 3:** 这个问题的另一个简单方法<u>不使用任何散列表或数组，如下所述。</u>我们只要用 single for loop 就可以找到第一个不重复的字符。

**另一种方法:**

要计算字符出现的频率，我们可以执行以下步骤:

字符的频率=字符串长度–不带该字符的字符串长度

例如:给字符串是**“helloh”**，我们要计算字符“h”的频率，所以通过使用上面的公式，我们可以说

**字符“h”的频率= 6(字符串长度)–4(不带“h”的字符串长度)**

**= 2**

因此，通过这种方式，我们可以计算字符串中每个字符的频率，如果我们发现 count == 1，这意味着该字符是字符串中第一个不重复的字符。

**实现:**上述方法在 java 中的实现如下:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class first_non_repeating {

    static int firstNonRepeating(String str)
    {
        boolean flag = false;

        int index = -1;

        for (int i = 0; i < s.length(); i++) {

            // Here I am replacing a character with "" and
            // then finding the length after replacing and
            // then subtracting  length of that replaced
            // string from the total length of the original
            // string
            int count_occurence
                = s.length()
                  - s.replace(
                         Character.toString(s.charAt(i)),
                         "")
                        .length();

            if (count_occurence == 1) {

                flag = true;

                index = i;

                break;
            }
        }

        if (flag)
            System.out.println(
                "First non repeating character is "
                + s.charAt(index));

        else
            System.out.println(
                "There is no non-repeating character
                         is present in the string");
    }

    // Driver Code
    public static void main(String arg[])
    {

        String s = "GeeksforGeeks";

        firstNonRepeating(s);
    }
}
// This Solution is contributed by Sourabh Sharma.
```

**Output**

```
First non repeating character is f
```

**时间复杂度:** O(N)

**辅助空间:** O(1)