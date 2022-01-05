# 在字符串中多找一个字符

> 原文:[https://www . geesforgeks . org/find-one-extra-character-string/](https://www.geeksforgeeks.org/find-one-extra-character-string/)

给定两个长度为 n 和 n+1 的字符串。第二个字符串包含第一个字符串的所有字符，但还有一个额外的字符。您的任务是在第二个字符串中找到多余的字符。
**例:**

```
Input : string strA = "abcd";
        string strB = "cbdae";
Output : e
string B contain all the element 
there is a one extra character which is e

Input : string strA = "kxml";
        string strB = "klxml";
Output : l
string B contain all the element 
there is a one extra character which is l
```

**方法 1(蛮力):-**
用两个进行循环检查。
时间复杂度:- O(n^2)
空间复杂度:- O(1)。
**方法 2(哈希表):-**
创建一个空哈希表，插入第二个字符串的所有字符。现在删除第一个字符串的所有字符。剩余字符是额外字符。
时间复杂度:- O(n)
辅助空间:- O(n)。

## C++

```
// CPP program to find extra character in one
// string
#include <bits/stdc++.h>
using namespace std;

char findExtraCharcter(string strA, string strB)
{
    // store string values in map
    unordered_map<char, int> m1;

    // store second string in map with frequency
    for (int i = 0; i < strB.length(); i++)
        m1[strB[i]]++;

    // store first string in map with frequency
    for (int i = 0; i < strA.length(); i++)
        m1[strA[i]]--;

    for (auto h1 = m1.begin(); h1 != m1.end(); h1++) {

        // if the frequency is 1 then this
        // character is which is added extra
        if (h1->second == 1)
            return h1->first;
    }
}

int main()
{
    // given string
    string strA = "abcd";
    string strB = "cbdad";

    // find Extra Character
    cout << findExtraCharcter(strA, strB);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find extra character in one
// string
class GFG
{

static char findExtraCharcter(char []strA, char[] strB)
{
    // store string values in map
    int[] m1 = new int[256];

    // store second string in map with frequency
    for (int i = 0; i < strB.length; i++)
        m1[strB[i]]++;

    // store first string in map with frequency
    for (int i = 0; i < strA.length; i++)
        m1[strA[i]]--;

    for (int i=0;i<m1.length;i++)
    {

        // if the frequency is 1 then this
        // character is which is added extra
        if (m1[i]== 1)
            return (char) i;
    }
    return Character.MIN_VALUE;
}

// Driver code
public static void main(String[] args)
{
    // given string
    String strA = "abcd";
    String strB = "cbdad";

    // find Extra Character
    System.out.println(findExtraCharcter(strA.toCharArray(), strB.toCharArray()));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find extra character
# in one string
def findExtraCharacter(strA, strB):

    # store string values in map
    m1 = {}

    # store second string in map
    # with frequency
    for i in strB:
        if i in m1:
            m1[i] += 1
        else:
            m1[i] = 1

    # store first string in map
    # with frequency
    for i in strA:
        m1[i] -= 1

    for h1 in m1:

        # if the frequency is 1 then this
        # character is which is added extra
        if m1[h1] == 1:
            return h1

# Driver Code
if __name__ == "__main__":

    # given string
    strA = 'abcd'
    strB = 'cbdad'

    # find Extra Character
    print(findExtraCharacter(strA, strB))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find extra character in one
// string
using System;

class GFG
{

static char findExtraCharcter(char []strA, char[] strB)
{
    // store string values in map
    int[] m1 = new int[256];

    // store second string in map with frequency
    for (int i = 0; i < strB.Length; i++)
        m1[strB[i]]++;

    // store first string in map with frequency
    for (int i = 0; i < strA.Length; i++)
        m1[strA[i]]--;

    for (int i = 0; i < m1.Length; i++)
    {

        // if the frequency is 1 then this
        // character is which is added extra
        if (m1[i]== 1)
            return (char) i;
    }
    return char.MinValue;
}

// Driver code
public static void Main(String[] args)
{
    // given string
    String strA = "abcd";
    String strB = "cbdad";

    // find Extra Character
    Console.WriteLine(findExtraCharcter(strA.ToCharArray(),
                                        strB.ToCharArray()));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program to find extra character in one
// string
function findExtraCharcter(strA,strB)
{

    // store string values in map
    let m1 = new Array(256);
     for(let i = 0; i < 256; i++)
        m1[i] = 0;

    // store second string in map with frequency
    for (let i = 0; i < strB.length; i++)
        m1[strB[i].charCodeAt(0)]++;

    // store first string in map with frequency
    for (let i = 0; i < strA.length; i++)
        m1[strA[i].charCodeAt(0)]--;

    for (let i = 0; i < m1.length; i++)
    {

        // if the frequency is 1 then this
        // character is which is added extra
        if (m1[i] == 1)
            return String.fromCharCode(i);
    }
    return Number.MIN_VALUE;
}

// given string
let strA = "abcd";
let strB = "cbdad";

// find Extra Character
document.write(findExtraCharcter(strA.split(""), strB.split("")));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
d
```