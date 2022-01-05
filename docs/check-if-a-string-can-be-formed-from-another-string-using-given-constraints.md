# 使用给定的约束条件检查一个字符串是否可以由另一个字符串组成

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-formed-from-other-string-use-given-constraints/](https://www.geeksforgeeks.org/check-if-a-string-can-be-formed-from-another-string-using-given-constraints/)

给定两个字符串 S1 和 S2(所有字符都是小写)。任务是检查 S2 是否可以利用给定的约束条件从 S1 形成:
1。S1 有 S2 的人物如果 S2 有两个 a，那么 S1 也应该有两个 a。
2。如果 S1 没有 S2 的任何字符，请检查 S1 是否有前两个 ASCII 字符。例如，如果“e”在 S2 而不在 S1，那么“c”和“d”可以从 S1 用来表示“e”。
**注:**所有来自 S1 的字符只能使用一次。

**示例:**

> **输入:** S= abbat，W= cat
> **输出:**YES
> “c”由“a”和“b”构成，“a”和“t”出现在 S1。
> 
> **输入:** S= abbt，W= cat
> **输出:**NO
> “c”由‘a’和‘b’组成，但要组成 S2 的下一个字符
> ‘a’，S1 就没有更多没用过的‘a’了。

**方法:**上述问题可以用哈希法解决。S1 所有字符的计数都存储在一个散列表中。遍历字符串，检查哈希表中是否有 S2 字符，减少哈希表中特定字符的数量。如果哈希表中没有该字符，请检查哈希表中是否有前两个 ASCII 字符，然后减少哈希表中前两个 ASCII 字符的数量。如果所有的字符都可以使用给定的约束由 S1 构成，那么字符串 S2 可以由 S1 构成，否则就不能构成。

下面是上述方法的实现:

## C++

```
// CPP program to Check if a given
// string can be formed from another
// string using given constraints
#include <bits/stdc++.h>
using namespace std;

// Function to check if S2 can be formed of S1
bool check(string S1, string S2)
{
    // length of strings
    int n1 = S1.size();
    int n2 = S2.size();

    // hash-table to store count
    unordered_map<int, int> mp;

    // store count of each character
    for (int i = 0; i < n1; i++) {
        mp[S1[i]]++;
    }

    // traverse and check for every character
    for (int i = 0; i < n2; i++) {

        // if the character of s2 is present in s1
        if (mp[S2[i]]) {
            mp[S2[i]]--;
        }

        // if the character of s2 is not present in
        // S1, then check if previous two ASCII characters
        // are present in S1
        else if (mp[S2[i] - 1] && mp[S2[i] - 2]) {

            mp[S2[i] - 1]--;
            mp[S2[i] - 2]--;
        }
        else {
            return false;
        }
    }

   return true;
}

// Driver Code
int main()
{
    string S1 = "abbat";
    string S2 = "cat";

    // Calling function to check
    if (check(S1, S2))
        cout << "YES";
    else
        cout << "NO";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to Check if a given
// String can be formed from another
// String using given constraints
import java.util.*;

class GFG
{

// Function to check if S2 can be formed of S1
static boolean check(String S1, String S2)
{
    // length of Strings
    int n1 = S1.length();
    int n2 = S2.length();

    // hash-table to store count
    HashMap<Integer,Integer> mp =
        new HashMap<Integer,Integer>();

    // store count of each character
    for (int i = 0; i < n1; i++)
    {
        if(mp.containsKey((int)S1.charAt(i)))
        {
            mp.put((int)S1.charAt(i),
            mp.get((int)S1.charAt(i)) + 1);
        }
        else
        {
            mp.put((int)S1.charAt(i), 1);
        }
    }

    // traverse and check for every character
    for (int i = 0; i < n2; i++)
    {

        // if the character of s2 is present in s1
        if(mp.containsKey((int)S2.charAt(i)))
        {
            mp.put((int)S2.charAt(i),
            mp.get((int)S2.charAt(i)) - 1);
        }

        // if the character of s2 is not present in
        // S1, then check if previous two ASCII characters
        // are present in S1
        else if (mp.containsKey(S2.charAt(i)-1) &&
                    mp.containsKey(S2.charAt(i)-2))
        {
            mp.put((S2.charAt(i) - 1),
            mp.get(S2.charAt(i) - 1) - 1);
            mp.put((S2.charAt(i) - 2),
            mp.get(S2.charAt(i) - 2) - 1);
        }
        else
        {
            return false;
        }
    }

    return true;
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "abbat";
    String S2 = "cat";

    // Calling function to check
    if (check(S1, S2))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to Check if a given string
# can be formed from another string using
# given constraints
from collections import defaultdict

# Function to check if S2 can
# be formed of S1
def check(S1, S2):

    # length of strings
    n1 = len(S1)
    n2 = len(S2)

    # hash-table to store count
    mp = defaultdict(lambda:0)

    # store count of each character
    for i in range(0, n1):
        mp[S1[i]] += 1

    # traverse and check for every character
    for i in range(0, n2):

        # if the character of s2 is
        # present in s1
        if mp[S2[i]]:
            mp[S2[i]] -= 1

        # if the character of s2 is not present
        # in S1, then check if previous two ASCII
        # characters are present in S1
        elif (mp[chr(ord(S2[i]) - 1)] and
              mp[chr(ord(S2[i]) - 2)]):

            mp[chr(ord(S2[i]) - 1)] -= 1
            mp[chr(ord(S2[i]) - 2)] -= 1

        else:
            return False

    return True

# Driver Code
if __name__ == "__main__":

    S1 = "abbat"
    S2 = "cat"

    # Calling function to check
    if check(S1, S2):
        print("YES")
    else:
        print("NO")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to Check if a given
// String can be formed from another
// String using given constraints
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if S2 can be formed of S1
static bool check(String S1, String S2)
{
    // length of Strings
    int n1 = S1.Length;
    int n2 = S2.Length;

    // hash-table to store count
    Dictionary<int,int> mp =
        new Dictionary<int,int>();

    // store count of each character
    for (int i = 0; i < n1; i++)
    {
        if(mp.ContainsKey((int)S1[i]))
        {
            mp[(int)S1[i]] = mp[(int)S1[i]] + 1;
        }
        else
        {
            mp.Add((int)S1[i], 1);
        }
    }

    // traverse and check for every character
    for (int i = 0; i < n2; i++)
    {

        // if the character of s2 is present in s1
        if(mp.ContainsKey((int)S2[i]))
        {
            mp[(int)S2[i]] = mp[(int)S2[i]] - 1;
        }

        // if the character of s2 is not present in
        // S1, then check if previous two ASCII characters
        // are present in S1
        else if (mp.ContainsKey(S2[i] - 1) &&
                    mp.ContainsKey(S2[i] - 2))
        {
            mp[S2[i] - 1] = mp[S2[i] - 1] - 1;
            mp[S2[i] - 2] = mp[S2[i] - 2] - 1;
        }
        else
        {
            return false;
        }
    }

    return true;
}

// Driver Code
public static void Main(String[] args)
{
    String S1 = "abbat";
    String S2 = "cat";

    // Calling function to check
    if (check(S1, S2))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to Check if a given
// String can be formed from another
// String using given constraints

// Function to check if S2 can be formed of S1
function check(S1, S2)
{

    // Length of Strings
    var n1 = S1.length;
    var n2 = S2.length;

    // hash-table to store count
    var mp = {};

    // Store count of each character
    for(var i = 0; i < n1; i++)
    {
        if (mp.hasOwnProperty(S1[i]))
        {
            mp[S1[i]] = mp[S1[i]] + 1;
        }
        else
        {
            mp[S1[i]] = 1;
        }
    }

    // Traverse and check for every character
    for(var i = 0; i < n2; i++)
    {

        // If the character of s2 is present in s1
        if (mp.hasOwnProperty(S2[i]))
        {
            mp[S2[i]] = mp[S2[i]] - 1;
        }

        // If the character of s2 is not present
        // in S1, then check if previous two ASCII
        // characters are present in S1
        else if (mp.hasOwnProperty(
            String.fromCharCode(S2[i].charCodeAt(0) - 1)) &&
            mp.hasOwnProperty(
            String.fromCharCode(S2[i].charCodeAt(0) - 2)))
        {
            mp[String.fromCharCode(
                S2[i].charCodeAt(0) - 1)] =
            mp[String.fromCharCode(
                S2[i].charCodeAt(0) - 1)] - 1;
            mp[String.fromCharCode(
                S2[i].charCodeAt(0) - 2)] =
            mp[String.fromCharCode(
                S2[i].charCodeAt(0) - 2)] - 1;
        }
        else
        {
            return false;
        }
    }
    return true;
}

// Driver Code
var S1 = "abbat";
var S2 = "cat";

// Calling function to check
if (check(S1, S2))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by rdtank

</script>
```

**Output:** 

```
YES
```