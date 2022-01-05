# 检查两个给定字符串中是否有共同的字符

> 原文:[https://www . geesforgeks . org/check-if-any-common-in-two-given-string/](https://www.geeksforgeeks.org/check-if-there-is-any-common-character-in-two-given-strings/)

给定两个字符串。任务是检查两个字符串之间是否有任何共同的字符。

**示例:**

```
Input: s1 = "geeksforgeeks", s2 = "geeks"
Output: Yes

Input: s1 = "geeks", s2 = "for"
Output: No
```

**方法:**遍历第一个字符串，将字符串的字符与其频率进行映射，在该映射中，字符充当键，频率作为其值。然后遍历第二个字符串，我们将检查两个字符串中是否有任何字符，然后确认有一个公共的子序列。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to match character
bool check(string s1, string s2)
{
    // Create a map to map
    // characters of 1st string
    map<char, int> map;

    // traverse the first string
    // and create a hash map
    for (int i = 0; i < s1.length(); i++)
        map[s1[i]]++;

    // traverse the second string
    // and if there is any
    // common character than return 1
    for (int i = 0; i < s2.length(); i++)
        if (map[s2[i]] > 0)
            return true;

    // else return 0
    return false;
}

// Driver code
int main()
{
    // Declare two strings
    string s1 = "geeksforgeeks", s2 = "geeks";

    // Find if there is a common subsequence
    bool yes_or_no = check(s1, s2);

    if (yes_or_no == true)
        cout << "Yes" << endl;

    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to match character
static boolean check(String s1, String s2)
{
    // Create a map to map
    // characters of 1st string
    Map<Character, Integer> mp = new HashMap<>();

    // traverse the first string
    // and create a hash map
    for (int i = 0; i < s1.length(); i++)
    {
        mp.put(s1.charAt(i), mp.get(s1.charAt(i)) == null ? 1 : mp.get(s1.charAt(i)) + 1);
    }

    // traverse the second string
    // and if there is any
    // common character than return 1
    for (int i = 0; i < s2.length(); i++)
    {
        if (mp.get(s2.charAt(i)) > 0)
        {
            return true;
        }
    }

    // else return 0
    return false;
}

// Driver code
public static void main(String[] args)
{
    // Declare two strings
    String s1 = "geeksforgeeks", s2 = "geeks";

    // Find if there is a common subsequence
    boolean yes_or_no = check(s1, s2);

    if (yes_or_no == true)
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to check whether
# two lists are overlapping or not
def is_member(List, key):

    for i in range(0, len(List)):
        if key == List[i]:
            return True
    return False

def overlap(List1 , List2):

    for key in List1:
        if is_member( List2, key ):
            return True

    return False

# Driver Code
if __name__ == '__main__':

    s1 = 'geeksforgeeks'
    s2 = 'geeks'

    List1 = list( s1 )
    List2 = list( s2 )

    yes_or_no = str(overlap( List1, List2 ))

    if (yes_or_no):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Krishna_Yadav
```

## C#

```
// C# program to check if successive
// pair of numbers in the queue are
// consecutive or not
using System;
using System.Collections.Generic;

class GFG
{

// Function to match character
static Boolean check(String s1, String s2)
{
    // Create a map to map
    // characters of 1st string
    Dictionary<char,int> mp = new Dictionary<char,int>();

    // traverse the first string
    // and create a hash map
    for (int i = 0; i < s1.Length; i++)
    {
        if(mp.ContainsKey(s1[i]))
        {
            var val = mp[s1[i]];
            mp.Remove(s1[i]);
            mp.Add(s1[i], val + 1);
        }
        else
        {
            mp.Add(s1[i], 1);
        }
    }

    // traverse the second string
    // and if there is any
    // common character than return 1
    for (int i = 0; i < s2.Length; i++)
    {
        if (mp[s2[i]] > 0)
        {
            return true;
        }
    }

    // else return 0
    return false;
}

// Driver code
public static void Main(String[] args)
{
    // Declare two strings
    String s1 = "geeksforgeeks", s2 = "geeks";

    // Find if there is a common subsequence
    Boolean yes_or_no = check(s1, s2);

    if (yes_or_no == true)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to match character
function check( s1, s2)
{
    // Create a map to map
    // characters of 1st string
    var map = new Map();

    // traverse the first string
    // and create a hash map
    for (var i = 0; i < s1.length; i++)
    {
        if(map.has(s1[i].charCodeAt(0)))
        {
            map[s1[i].charCodeAt(0)]++;
        }
        else
        {
            map[s1[i].charCodeAt(0)]=1;
        }

    }

    // traverse the second string
    // and if there is any
    // common character than return 1
    for (var i = 0; i < s2.length; i++)
        if (map[s2[i].charCodeAt(0)] > 0)
            return true;

    // else return 0
    return false;
}

// Driver code
// Declare two strings
var s1 = "geeksforgeeks", s2 = "geeks";
// Find if there is a common subsequence
var yes_or_no = check(s1, s2);
if (yes_or_no)
    document.write( "Yes");
else
    document.write( "No" );

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(n)其中 n 是弦的长度