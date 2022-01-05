# 检查一个字符串的字符是否可以交换成其他的

> 原文:[https://www . geesforgeks . org/check-if-characters-of-one-string-to-form-other/](https://www.geeksforgeeks.org/check-if-characters-of-one-string-can-be-swapped-to-form-other/)

给定两个字符串，我们需要通过交换第一个字符串的字符来寻找是否可以形成第二个字符串。
**例:**

```
Input : str1 = "geeksforgeeks" 
        str2 = "geegeeksksfor"
Output : YES

Input : str1 = "geeksfor"  
        str2 = "geeekfor"
Output : NO
```

首先，我们将找到字符串的长度，如果长度不相等，这意味着我们不能通过交换第一个字符串的字符来形成目标字符串。如果长度相等，那么我们遍历第一个字符串并为其创建一个映射，之后，如果映射中的任何索引为负，我们将遍历第二个字符串并减少映射的计数，这意味着我们不能形成目标字符串，否则我们可以形成目标字符串。

```
Algorithm-
1- l1 = str1.length()  &&   l2 = str2.length()
2- if (l1 != l2)
    print "NO" 
3- Else
   map[26] = {0};
   for i=0 to l1
    map[str1[i]-'a']++;
   for i=0 to l2
     map[str2[i]-'a']--;
     if (map[str[2]-'a'<0)
      print "NO"
4- if no index goes negative print "YES"
5- End
```

## C++

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 26;

bool targetstring(string str1, string str2)
{
    int l1 = str1.length();
    int l2 = str2.length();

    // if length is not same print no
    if (l1 != l2)
        return false;

    int map[MAX] = { 0 };

    // Count frequencies of character in
    // first string.
    for (int i = 0; i < l1; i++)
        map[str1[i] - 'a']++;

    // iterate through the second string
    // decrement counts of characters in
    // second string
    for (int i = 0; i < l2; i++) {
        map[str2[i] - 'a']--;

        // Since lengths are same, some
        // value would definitely become
        // negative if result is false.
        if (map[str2[i] - 'a'] < 0)
            return false;
    }

    return true;
}

// driver function
int main()
{
    string str1 = "geeksforgeeks";
    string str2 = "geegeeksksfor";
    if (targetstring(str1, str2))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// characters of one string
// can be swapped to form other
class GFG
{
static int MAX = 26;

static boolean targetstring(String str1,
                            String str2)
{
    int l1 = str1.length();
    int l2 = str2.length();

    // if length is not same print no
    if (l1 != l2)
        return false;

    int []map = new int[MAX];

    // Count frequencies of
    // character in first string.
    for (int i = 0; i < l1; i++)
        map[str1.charAt(i) - 'a']++;

    // iterate through the second
    // string decrement counts of
    // characters in second string
    for (int i = 0; i < l2; i++)
    {
        map[str2.charAt(i) - 'a']--;

        // Since lengths are same,
        // some value would definitely
        // become negative if result
        // is false.
        if (map[str2.charAt(i) - 'a'] < 0)
            return false;
    }

    return true;
}

// Driver Code
public static void main(String args[])
{
    String str1 = "geeksforgeeks";
    String str2 = "geegeeksksfor";
    if (targetstring(str1, str2))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by
// Akanksha Rai
```

## 蟒蛇 3

```
# Python3 program to check if
# characters of one string
# can be swapped to form other
MAX = 26

def targetstring(str1, str2):

    l1 = len(str1)
    l2 = len(str2)

    # if length is not same print no
    if (l1 != l2):
        return False

    map = [0] * MAX

    # Count frequencies of character
    # in first string.
    for i in range (l1):
        map[ord(str1[i]) - ord('a')] += 1

    # iterate through the second string
    # decrement counts of characters in
    # second string
    for i in range(l2) :
        map[ord(str2[i]) - ord('a')] -= 1

        # Since lengths are same, some
        # value would definitely become
        # negative if result is false.
        if (map[ord(str2[i]) - ord('a')] < 0):
            return False

    return True

# Driver Code
if __name__ == "__main__":

    str1 = "geeksforgeeks"
    str2 = "geegeeksksfor"
    if (targetstring(str1, str2)):
        print("YES")
    else:
        print("NO")

# This code is contributed by ita_c
```

## C#

```
// C# program to check if
// characters of one string
// can be swapped to form other
using System;

class GFG
{
    static int MAX = 26;

    static bool targetstring(string str1,
                             string str2)
    {
        int l1 = str1.Length;
        int l2 = str2.Length;

        // if length is not
        // same print no
        if (l1 != l2)
            return false;

        int []map = new int[MAX];
        Array.Clear(map, 0, 26);

        // Count frequencies of
        // character in first string.
        for (int i = 0; i < l1; i++)
            map[str1[i] - 'a']++;

        // iterate through the second
        // string decrement counts of
        // characters in second string
        for (int i = 0; i < l2; i++)
        {
            map[str2[i] - 'a']--;

            // Since lengths are same,
            // some value would definitely
            // become negative if result
            // is false.
            if (map[str2[i] - 'a'] < 0)
                return false;
        }

        return true;
    }

    // Driver Code
    static void Main()
    {
        string str1 = "geeksforgeeks";
        string str2 = "geegeeksksfor";
        if (targetstring(str1, str2))
            Console.Write("YES");
        else
            Console.Write("NO");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// characters of one string
// can be swapped to form other
$MAX = 26;

function targetstring($str1, $str2)
{
    global $MAX;
    $l1 = strlen($str1);
    $l2 = strlen($str2);

    // if length is not same print no
    if ($l1 != $l2)
        return false;

    $map[$MAX] = array(0);

    // Count frequencies of character
    // in first string.
    for ($i = 0; $i < $l1; $i++)
        $map[$str1[$i] - 'a']++;

    // iterate through the second string
    // decrement counts of characters in
    // second string
    for ($i = 0; $i < $l2; $i++)
    {
        $map[$str2[$i] - 'a']--;

        // Since lengths are same, some
        // value would definitely become
        // negative if result is false.
        if ($map[$str2[$i] - 'a'] < 0)
            return false;
    }

    return true;
}

// Driver Code
$str1 = "geeksforgeeks";
$str2 = "geegeeksksfor";
if (targetstring($str1, $str2))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to check if
// characters of one string
// can be swapped to form other
let MAX = 26;

function targetstring(str1,str2)
{
    let l1 = str1.length;
    let l2 = str2.length;

    // if length is not same print no
    if (l1 != l2)
        return false;

    let map = new Array(MAX);
    for(let i = 0; i < map.length; i++)
    {
        map[i] = 0;
    }

    // Count frequencies of
    // character in first string.
    for (let i = 0; i < l1; i++)
        map[str1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // iterate through the second
    // string decrement counts of
    // characters in second string
    for (let i = 0; i < l2; i++)
    {
        map[str2[i].charCodeAt(0) - 'a'.charCodeAt(0)]--;

        // Since lengths are same,
        // some value would definitely
        // become negative if result
        // is false.
        if (map[str2[i] - 'a'.charCodeAt(0)] < 0)
            return false;
    } 
    return true;
}

// Driver Code
let str1 = "geeksforgeeks";
let str2 = "geegeeksksfor";
if (targetstring(str1, str2))
    document.write("YES");
else
    document.write("NO");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
YES
```

**时间复杂度**–O(n)