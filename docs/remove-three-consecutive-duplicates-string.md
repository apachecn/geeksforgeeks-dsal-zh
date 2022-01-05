# 从字符串中删除三个连续的副本

> 原文:[https://www . geesforgeks . org/remove-三个连续重复-string/](https://www.geeksforgeeks.org/remove-three-consecutive-duplicates-string/)

给定一个字符串，您必须从该字符串中删除三个连续的重复项。如果没有三个连续的，那么输出字符串。
**例:**

```
Input : aabbbaccddddc
Output :ccdc

Input :aabbaccddc
Output :aabbaccddc
```

**说明:**
我们把字符串的字符一个一个的插入到向量中，不断的检查向量的大小。如果向量的大小大于 2，那么我们将检查字符串的最后 3 个字符是否相同。如果字符相同
，那么我们将使用 resize()在数组中向后移动三步，否则不移动。

## C++

```
// C++ program to remove three consecutive
// duplicates
#include <bits/stdc++.h>
using namespace std;

// function to remove three consecutive
// duplicates
void remove3ConsecutiveDuplicates(string str)
{
    vector<char> v;
    for (int i = 0; i < str.size(); ++i) {
        v.push_back(str[i]);

        if (v.size() > 2) {
            int sz = v.size();

            // removing three consecutive duplicates
            if (v[sz - 1] == v[sz - 2] &&
                v[sz - 2] == v[sz - 3]) {
                v.resize(sz - 3); // Removing three characters
                                 // from the string
            }
        }
    }

    // printing the string final string
    for (int i = 0; i < v.size(); ++i)
        cout << v[i];
}

// driver code
int main()
{
    string str = "aabbbaccddddc";

    remove3ConsecutiveDuplicates(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove three consecutive
// duplicates
import java.util.*;

class GFG
{

// function to remove three consecutive
// duplicates
static void remove3ConsecutiveDuplicates(String str)
{
    Vector<Character> v = new Vector<>();
    for (int i = 0; i < str.length(); ++i)
    {
        v.add(str.charAt(i));

        if (v.size() > 2)
        {
            int sz = v.size();

            // removing three consecutive duplicates
            if (v.get(sz - 1) == v.get(sz - 2) &&
                v.get(sz - 2) == v.get(sz - 3))
            {
                v.setSize(sz - 3); // Removing three characters
                                // from the string
            }
        }
    }

    // printing the string final string
    for (int i = 0; i < v.size(); ++i)
        System.out.print(v.get(i));
}

// Driver code
public static void main(String[] args)
{
    String str = "aabbbaccddddc";
    remove3ConsecutiveDuplicates(str);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to remove three consecutive duplicates

# function to remove three consecutive duplicates
def remove3ConsecutiveDuplicates(string):
    val = ""
    i = 0
    while (i < len(string)):
        if (i < len(string) - 2 and
            string[i] * 3 == string[i:i + 3]):
            i += 3
        else:
            val += string[i]
            i += 1

    if (len(val) == len(string)):
        return val
    else:
        return remove3ConsecutiveDuplicates(val)

# Driver code
string = "aabbbaccddddc"
val = remove3ConsecutiveDuplicates(string)
print(val)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to remove three consecutive
// duplicates
using System;
using System.Collections.Generic;

class GFG
{

// function to remove three consecutive
// duplicates
static void remove3ConsecutiveDuplicates(String str)
{
    List<char> v = new List<char>();
    for (int i = 0; i < str.Length; ++i)
    {
        v.Add(str[i]);

        if (v.Count > 2)
        {
            int sz = v.Count;

            // removing three consecutive duplicates
            if (v[sz - 1] == v[sz - 2] &&
                v[sz - 2] == v[sz - 3])
            {
                v.RemoveRange(sz-3,3); // Removing three characters
                                // from the string
            }
        }
    }

    // printing the string final string
    for (int i = 0; i < v.Count; ++i)
        Console.Write(v[i]);
}

// Driver code
public static void Main(String[] args)
{
    String str = "aabbbaccddddc";
    remove3ConsecutiveDuplicates(str);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to remove three consecutive
// duplicates

// function to remove three consecutive
// duplicates
function remove3ConsecutiveDuplicates($str)
{
    $v = array();
    for ($i = 0; $i < strlen($str); ++$i)
    {
        array_push($v, $str[$i]);

        if (count($v) > 2)
        {
            $sz = count($v);

            // removing three consecutive duplicates
            if ($v[$sz - 1] == $v[$sz - 2] &&
                $v[$sz - 2] == $v[$sz - 3])
            {
                array_pop($v);
                array_pop($v);
                array_pop($v);
                // Removing three characters
                                // from the string
            }
        }
    }

    // printing the string final string
    for ($i = 0; $i < count($v); ++$i)
        echo $v[$i];
}

    // Driver code
    $str = "aabbbaccddddc";

    remove3ConsecutiveDuplicates($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to remove three consecutive
// duplicates

// function to remove three consecutive
// duplicates
function remove3ConsecutiveDuplicates(str)
{
    let v = [];
    for (let i = 0; i < str.length; ++i)
    {
        v.push(str[i]);

        if (v.length > 2)
        {
            let sz = v.length;

            // removing three consecutive duplicates
            if (v[sz - 1] == v[sz - 2] &&
                v[sz - 2] == v[sz - 3])
            {
                v.pop();
                v.pop();
                v.pop();
                // Removing three characters
                                // from the string
            }
        }
    }

    // printing the string final string
    for (let i = 0; i < v.length; ++i)
        document.write(v[i]);
}

// Driver code
let str = "aabbbaccddddc";
remove3ConsecutiveDuplicates(str);

// This code is contributed by rag2127
</script>
```

**输出:**

```
ccdc
```

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。