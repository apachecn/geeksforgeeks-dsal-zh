# 快速检查一个字符串的所有字符是否相同的方法

> 原文:[https://www . geesforgeks . org/quick-way-check-characters-string/](https://www.geeksforgeeks.org/quick-way-check-characters-string/)

给定一个字符串，检查该字符串的所有字符是否相同。

**示例:**

```
Input : s = "geeks"
Output : No

Input : s = "gggg" 
Output : Yes
```

**简单方式**

查找字符串是否包含所有相同的字符。遍历索引 1 中的整个字符串，检查该字符是否与字符串的第一个字符匹配。如果是，则匹配直到字符串大小。如果没有，那就打破循环。

## C++

```
// C++ program to find whether the string
// has all same characters or not.
#include <iostream>
using namespace std;

bool allCharactersSame(string s)
{
    int n = s.length();
    for (int i = 1; i < n; i++)
        if (s[i] != s[0])
            return false;

    return true;
}

// Driver code
int main()
{
    string s = "aaa";
    if (allCharactersSame(s))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find whether the String
// has all same characters or not.
import java.io.*;

public class GFG{

static boolean allCharactersSame(String s)
{
    int n = s.length();
    for (int i = 1; i < n; i++)
        if (s.charAt(i) != s.charAt(0))
            return false;

    return true;
}

// Driver code
    static public void main (String[] args){
        String s = "aaa";
    if (allCharactersSame(s))
        System.out.println("Yes");
    else
        System.out.println("No");

    }
}

// This Code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find whether the string
# has all same characters or not.

# Function to check the string has
# all same characters or not .
def allCharactersSame(s) :
    n = len(s)
    for i in range(1, n) :
        if s[i] != s[0] :
            return False

    return True

# Driver code
if __name__ == "__main__" :

    s = "aaa"
    if allCharactersSame(s) :
        print("Yes")
    else :
        print("No")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find whether the string
// has all same characters or not.
using System;

public class GFG{

static bool allCharactersSame(string s)
{
    int n = s.Length;
    for (int i = 1; i < n; i++)
        if (s[i] != s[0])
            return false;

    return true;
}

// Driver code
    static public void Main (String []args){
        string s = "aaa";
    if (allCharactersSame(s))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find whether
// the string has all same
// characters or not.
function allCharactersSame($s)
{
    $n = strlen($s);
    for ($i = 1; $i < $n; $i++)
        if ($s[$i] != $s[0])
            return false;

    return true;
}

// Driver code
$s = "aaa";
if (allCharactersSame($s))
echo "Yes";
else
echo "No";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
    // Javascript program to find whether the string
    // has all same characters or not.

    function allCharactersSame(s)
    {
        let n = s.length;
        for (let i = 1; i < n; i++)
            if (s[i] != s[0])
                return false;

        return true;
    }

    let s = "aaa";
    if (allCharactersSame(s))
        document.write("Yes");
    else
        document.write("No");

        // This code is contributed by suresh07.
</script>
```

**Output**

```
Yes
```

**快速方式(不是时间复杂度，而是代码行数)**

想法是在 C++ STL 中使用 find_first_not_of()方法。
**find_first_not_of()** 查找并返回第一个与指定字符(或字符串中任何指定字符)不匹配的字符的位置。

## C++

```
// A quick C++ program to find whether the
// string has all same characters or not.
#include <iostream>
using namespace std;

bool allCharactersSame(string s)
{
    return (s.find_first_not_of(s[0]) == string::npos);
}

// Driver code
int main()
{
    string s = "aaa";
    if (allCharactersSame(s))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

**Output**

```
Yes
```

**另一种方法是使用 SET**

其思想是将字符串的所有字符添加到一个集合中。添加后，如果集合的大小大于 1，则表示存在不同的字符，如果大小正好是 1，则表示只有一个唯一的字符。

下面是上述逻辑的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check is all the
// characters in string are or not
void allCharactersSame(string s)
{
    set <char> s1;

    // Insert characters in the set
    for ( int i=0 ; i < s.length() ; i++)
        s1.insert(s[i]);

    // If all characters are same
    // Size of set will always be 1
    if ( s1.size() == 1 )
        cout << "YES";
    else
        cout << "NO";
}

// Driver code
int main()
{
    string str = "nnnn";
    allCharactersSame(str);
      return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check is all the
// characters in string are or not
public static void allCharactersSame(String s)
{
    Set<Character> s1 = new HashSet<Character>();

    // Insert characters in the set
    for(int i = 0; i < s.length(); i++)
        s1.add(s.charAt(i));

    // If all characters are same
    // Size of set will always be 1
    if (s1.size() == 1)
        System.out.println("YES");
    else
        System.out.println("NO");
}

// Driver Code
public static void main(String[] args)
{
    String str = "nnnn";

    allCharactersSame(str);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to check is
# all the characters in
# string are or not
def allCharactersSame(s):

    s1 = []

    # Insert characters in
    # the set
    for i in range(len(s)):
        s1.append(s[i])

    # If all characters are same
    # Size of set will always be 1
    s1 = list(set(s1))
    if(len(s1) == 1):
        print("YES")
    else:
        print("NO")

# Driver code
Str = "nnnn"
allCharactersSame(Str)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check is all the
// characters in string are or not
static void allCharactersSame(string s)
{
    HashSet<char> s1 = new HashSet<char>();

    // Insert characters in the set
    for(int i = 0; i < s.Length; i++)
        s1.Add(s[i]);

    // If all characters are same
    // Size of set will always be 1
    if (s1.Count == 1)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}

// Driver code 
static void Main()
{
    string str = "nnnn";

    allCharactersSame(str);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// Javascript program for above approach

    // Function to check is all the
    // characters in string are or not
    function allCharactersSame(s)
    {
        let s1 = new Set();
        // Insert characters in the set
    for(let i = 0; i < s.length; i++)
    {   
        s1.add(s[i]);
     }

    // If all characters are same
    // Size of set will always be 1
    if (s1.size == 1)
        document.write("YES");
    else
        document.write("NO");
    }

    // Driver Code
    let str = "nnnn";
    allCharactersSame(str);

    //This code is contributed by rag2127

</script>
```

**Output**

```
YES
```

**时间复杂度:** O(nLogn)

本文由 **Jatin Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。