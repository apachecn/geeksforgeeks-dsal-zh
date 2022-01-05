# 检查一个字符串是否可以在 K 个变化中转换成 Pangram

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-convert-to-pangram-in-k-changes/](https://www.geeksforgeeks.org/check-if-a-string-can-be-converted-to-pangram-in-k-changes/)

给定一个只包含小写英文字母的字符串和一个整数 T2。任务是通过最多执行 K 次更改来检查字符串是否可以转换为 Pangram。在一个变化中，我们可以删除任何现有的字符，并添加一个新的字符。
[**Pangram**](https://www.geeksforgeeks.org/pangram-checking/):Pangram 是包含英语字母表中每个字母的句子。
**注意**:假设字符串的长度总是大于 26，并且在一次操作中，我们必须移除一个现有的元素来添加一个新的元素。
**示例** :

```
Input : str = "qwqqwqeqqwdsdadsdasadsfsdsdsdasasas"
        K = 4
Output : False
Explanation : Making just 4 modifications in this string, 
it can't be changed to a pangram. 

Input : str = "qwqqwqeqqwdsdadsdasadsfsdsdsdasasas"
        K = 24
Output : True
Explanation : By making 19 modifications in the string, 
it can be changed to a pangram.
```

[Recommended: Please solve it on “***<u>PRACTICE</u>*** ” first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/k-pangrams/0) 

**进场:**

1.  使用布尔访问数组逐字符遍历字符串以跟踪数组中的所有字符。
2.  使用变量计数，遍历访问数组以记录丢失的字符。
3.  如果计数值小于或等于 K，则打印“真”。
4.  否则打印假。

以下是上述方法的实现:

## C++

```
// C++ program to check if a
// String can be converted
// to Pangram by atmost k modifications
#include<bits/stdc++.h>
using namespace std;

// Function to find if string
// can be converted to Pangram
// by atmost k modifications
bool isPangram(string S, int k)
{
    if (S.length() < 26)
        return false;

    // visit array to keep track
    // of all the characters
    // present in the array
    int visited[26];

    for(int i = 0; i < S.length(); i++)
        visited[S[i] - 'a'] = true;

    // A variable to keep count
    // of characters missing
    // in the string
    int count = 0;

    for(int i = 0; i < 26; i++)
    {
        if (!visited[i])
            count += 1;
    }

    // Comparison of count
    // with given value K
    if(count <= k )
        return true;
    return false;
}

// Driver Code
int main()
{

    string S = "thequickquickfoxmumpsoverthelazydog";
    int k = 15;

    // function calling
    isPangram(S, k) ? cout<< "true" :
                      cout<< "false";

    return 0;
}

// This code is contributed by ChitraNayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a String can be
// converted to Pangram by atmost k modifications

public class GFG {

    // Function to find if string can be converted
    // to Pangram by atmost k modifications
    static boolean isPangram(String S, int k)
    {
        if (S.length() < 26)
            return false;

        // visit array to keep track of all
        // the characters present in the array
        boolean[] visited = new boolean[26];

        for (int i = 0; i < S.length(); i++) {
            visited[S.charAt(i) - 'a'] = true;
        }

        // A variable to keep count of
        // characters missing in the string
        int count = 0;

        for (int i = 0; i < 26; i++) {
            if (!visited[i])
                count++;
        }

        // Comparison of count with given value K
        if (count <= k)
            return true;
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String S = "thequickquickfoxmumpsoverthelazydog";

        int k = 15;

        System.out.print(isPangram(S, k));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check
# if a String can be converted
# to Pangram by atmost k modifications

# Function to find if string
# can be converted to Pangram
# by atmost k modifications
def isPangram(S, k) :

    if len(S) < 26 :
        return False

    # visit array to keep track
    # of all the characters
    # present in the array
    visited = [0] * 26

    for char in S :
        visited[ord(char) - ord('a')] = True

    # A variable to keep count
    # of characters missing
    # in the string
    count = 0

    for i in range(26) :

        if visited[i] != True :
            count += 1

    # Comparison of count
    # with given value K
    if count <= k :
        return True
    return False

# Driver Code
if __name__ == "__main__" :

    S = "thequickquickfoxmumpsoverthelazydog"
    k = 15

    # function calling
    print(isPangram(S,k))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to check if a
// String can be converted to
// Pangram by atmost k modifications
using System;

class GFG
{

// Function to find if string
// can be converted to Pangram
// by atmost k modifications
static bool isPangram(String S, int k)
{
    if (S.Length < 26)
        return false;

    // visit array to keep track
    // of all the characters present
    // in the array
    bool[] visited = new bool[26];

    for (int i = 0; i < S.Length; i++)
    {
        visited[S[i] - 'a'] = true;
    }

    // A variable to keep count
    // of characters missing in
    // the string
    int count = 0;

    for (int i = 0; i < 26; i++)
    {
        if (!visited[i])
            count++;
    }

    // Comparison of count with
    // given value K
    if (count <= k)
        return true;
    return false;
}

// Driver code
public static void Main()
{
    string S = "thequickquickfoxmumpsoverthelazydog";

    int k = 15;

    Console.WriteLine(isPangram(S, k));
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// String can be converted
// to Pangram by atmost k modifications

// Function to find if string
// can be converted to Pangram
// by atmost k modifications
function isPangram($S, $k)
{
    if (strlen($S) < 26)
        return false;

    // visit array to keep track
    // of all the characters
    // present in the array
    $visited = array_fill(0, 26, NULL);

    for($i = 0; $i < strlen($S); $i++)
        $visited[ord($S[$i]) -
                 ord('a')] = true;

    // A variable to keep count
    // of characters missing
    // in the string
    $count = 0;

    for($i = 0; $i < 26; $i++)
    {
        if ($visited[$i] != true)
            $count += 1;
    }

    // Comparison of count
    // with given value K
    if ($count <= $k )
        return true;
    return false;
}

// Driver Code
$S = "thequickquickfoxmumpsoverthelazydog";
$k = 15;

// function calling
echo isPangram($S, $k)? "true" : "false";

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
      // JavaScript Program to check if a
      // String can be converted to
      // Pangram by atmost k modifications
      // Function to find if string
      // can be converted to Pangram
      // by atmost k modifications
      function isPangram(S, k) {
        if (S.length < 26) return false;

        // visit array to keep track
        // of all the characters present
        // in the array
        var visited = new Array(26);

        for (var i = 0; i < S.length; i++) {
          visited[S[i].charCodeAt(0) - "a".charCodeAt(0)] = true;
        }

        // A variable to keep count
        // of characters missing in
        // the string
        var count = 0;

        for (var i = 0; i < 26; i++) {
          if (!visited[i]) count++;
        }

        // Comparison of count with
        // given value K
        if (count <= k) return true;
        return false;
      }

      // Driver code
      var S = "thequickquickfoxmumpsoverthelazydog";
      var k = 15;

      document.write(isPangram(S, k));
    </script>
```

**Output:** 

```
true
```