# 从字符串中删除重复项，根据最后一次出现的情况保持顺序

> 原文:[https://www . geesforgeks . org/remove-replications-from-string-按最后出现次数保持顺序/](https://www.geeksforgeeks.org/remove-duplicates-from-string-keeping-the-order-according-to-last-occurrences/)

给定一个字符串，从字符串中删除重复字符，保留重复字符的最后一次出现。假设字符区分大小写。
**例:**

> **输入:**极客伪造
> **输出:**伪造
> 解释:请注意，我们只保留重复字符的最后出现，其顺序与它们在输入中出现的顺序相同。如果我们从右侧看到结果，我们可以注意到我们保留最后一个' s '，然后是最后一个' k '，依此类推。
> **输入:**在这是示例测试
> **输出:** hiampl est
> 说明:这里，输出包含每个字符的最后一次出现，甚至是" "(空格)，并删除重复项。就像在这个例子中，有 4 个空格，所以我们只有最后一次出现的空格，其他的都去掉了。并且每个字符只有最后一次出现，没有重复。
> **输入:** Abcda
> **输出:** Abcda

**天真解:**从左到右遍历给定的字符串。对于每个字符，检查它是否也出现在右侧。如果有，那么不要包含在输出中，否则包含它。

## C++

```
// C++ program to remove duplicate character
// from character array and print in sorted
// order
#include <bits/stdc++.h>
using namespace std;

string removeDuplicates(string str)
{
    // Used as index in the modified string
    int n = str.length();

    // Traverse through all characters
    string res = "";
    for (int i = 0; i < n; i++) {

        // Check if str[i] is present before it
        int j;
        for (j = i+1; j < n; j++)
            if (str[i] == str[j])
                break;

        // If not present, then add it to
        // result.
        if (j == n)
            res = res + str[i];
    }
    return res;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    cout << removeDuplicates(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicate character
// from character array and print in sorted
// order

import java.util.*;

class GFG{

static String removeDuplicates(String str)
{
    // Used as index in the modified String
    int n = str.length();

    // Traverse through all characters
    String res = "";
    for (int i = 0; i < n; i++)
    {
        // Check if str[i] is present before it
        int j;
        for (j = i + 1; j < n; j++)
            if (str.charAt(i) == str.charAt(j))
                break;

        // If not present, then add it to
        // result.
        if (j == n)
            res = res + str.charAt(i);
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    System.out.print(removeDuplicates(str));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to remove duplicate character
# from character array and print sorted
# order

def removeDuplicates(str):

    # Used as index in the modified string
    n = len(str)

    # Traverse through all characters
    res = ""
    for i in range(n):

        # Check if str[i] is present before it
        j = i + 1
        while j < n:
            if (str[i] == str[j]):
                break
            j += 1

        # If not present, then add it to
        # result.
        if (j == n):
            res = res + str[i]
    return res

# Driver code
if __name__ == '__main__':
    str = "geeksforgeeks"
    print(removeDuplicates(str))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to remove duplicate character
// from character array and print in sorted
// order
using System;

class GFG{

static String removeDuplicates(String str)
{

    // Used as index in the modified String
    int n = str.Length;

    // Traverse through all characters
    String res = "";
    for(int i = 0; i < n; i++)
    {

       // Check if str[i] is present before it
       int j;
       for(j = i + 1; j < n; j++)
          if (str[i] == str[j])
              break;

       // If not present, then add it to
       // result.
       if (j == n)
           res = res + str[i];
    }

    return res;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    Console.Write(removeDuplicates(str));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to remove duplicate character
// from character array and print in sorted
// order

  function removeDuplicates(str)
{
    // Used as index in the modified String
    let n = str.length;

    // Traverse through all characters
    let res = "";
    for (let i = 0; i < n; i++)
    {
        // Check if str[i] is present before it
        let j;
        for (j = i + 1; j < n; j++)
            if (str[i] == str[j])
                break;

        // If not present, then add it to
        // result.
        if (j == n)
            res = res + str[i];
    }
    return res;
}

// Driver code

    let str = "geeksforgeeks";
    document.write(removeDuplicates(str));

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
forgeks
```

时间复杂度:O(n*n)
**高效解决方案:**想法是使用哈希。
1)初始化一个空哈希表，并从右向左遍历输入字符串。如果当前字符不在哈希表中，将其附加到 res 并插入哈希表中。否则忽略它。

## C++

```
// C++ program to remove duplicate character
// from character array and print in sorted
// order
#include <bits/stdc++.h>
using namespace std;

string removeDuplicates(string str)
{
    // Used as index in the modified string
    int n = str.length();

    // Create an empty hash table
    unordered_set<char> s;

    // Traverse through all characters from
    // right to left
    string res = "";
    for (int i = n-1; i >= 0; i--) {

       // If current character is not in
       if (s.find(str[i]) == s.end())
       {
          res = res + str[i];
          s.insert(str[i]);
       }
    }

    // Reverse the result string
    reverse(res.begin(), res.end());

    return res;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    cout << removeDuplicates(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicate character
// from character array and print in sorted
// order
import java.util.*;

class GFG{

static String removeDuplicates(String str)
{

    // Used as index in the modified String
    int n = str.length();

    // Create an empty hash table
    HashSet<Character> s = new HashSet<Character>();

    // Traverse through all characters from
    // right to left
    String res = "";
    for(int i = n - 1; i >= 0; i--)
    {

       // If current character is not in
       if (!s.contains(str.charAt(i)))
       {
           res = res + str.charAt(i);
           s.add(str.charAt(i));
       }
    }

    // Reverse the result String
    res = reverse(res);
    return res;
}

static String reverse(String input)
{

    char[] a = input.toCharArray();
    int l, r = a.length - 1;

    for(l = 0; l < r; l++, r--)
    {
       char temp = a[l];
       a[l] = a[r];
       a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    System.out.print(removeDuplicates(str));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to remove duplicate character
# from character array and print sorted order
def removeDuplicates(str):

    # Used as index in the modified string
    n = len(str)

    # Create an empty hash table
    s = set()

    # Traverse through all characters from
    # right to left
    res = ""
    for i in range(n - 1, -1, -1):

        # If current character is not in
        if (str[i] not in s):
            res = res + str[i]
            s.add(str[i])

    # Reverse the result string
    res = res[::-1]
    return res

# Driver code
str = "geeksforgeeks"

print(removeDuplicates(str))

# This code is contributed by ShubhamCoder
```

## C#

```
// C# program to remove duplicate character
// from character array and print in sorted
// order
using System;
using System.Collections.Generic;

class GFG{

static String removeDuplicates(String str)
{

    // Used as index in the modified String
    int n = str.Length;

    // Create an empty hash table
    HashSet<char> s = new HashSet<char>();

    // Traverse through all characters
    // from right to left
    String res = "";
    for(int i = n - 1; i >= 0; i--)
    {

        // If current character is not in
        if (!s.Contains(str[i]))
        {
            res = res + str[i];
            s.Add(str[i]);
        }
    }

    // Reverse the result String
    res = reverse(res);
    return res;
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("", a);
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    Console.Write(removeDuplicates(str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to remove duplicate character
// from character array and print in sorted
// order

function removeDuplicates(str)
{
    // Used as index in the modified string
    var n = str.length;

    // Create an empty hash table
    var s = new Set();

    // Traverse through all characters from
    // right to left
    var res = "";
    for (var i = n-1; i >= 0; i--) {

       // If current character is not in
       if (!s.has(str[i]))
       {
          res = res + str[i];
          s.add(str[i]);
       }
    }

    // Reverse the result string
    res = res.split('').reverse().join('');

    return res;
}

// Driver code
var str = "geeksforgeeks";
document.write( removeDuplicates(str));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
forgeks
```

时间复杂度:O(n)