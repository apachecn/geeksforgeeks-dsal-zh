# 将字符串的字符重新排序为数字的有效英文表示

> 原文:[https://www . geesforgeks . org/将字符串字符重新排序为有效的英语数字表示/](https://www.geeksforgeeks.org/reorder-characters-of-a-string-to-valid-english-representations-of-digits/)

给定长度为 **N、**的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，该字符串由包含数字的重新排序的英文表示的小写字符**【0–9】、**组成，任务是以升序打印这些数字。

**示例:**

> **输入:** S = "fviefuro"
> **输出:** 45
> **说明:**给定的字符串可以重新洗牌为“四五”，所以字符串所代表的数字是 4 和 5。
> 
> **输入:**S = " owoztnoer "
> **输出:** 012
> **说明:**给定的字符串可以重新洗牌得到“零一二”，所以字符串所代表的数字是 0、1、2。

**天真方法:**最简单的方法是[生成给定字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有排列，对于每个排列，检查是否有可能找到字符串表示的有效数字。如果发现为真，则按升序打印这组数字。

***时间复杂度:** O(N * N！)*
***辅助空间:** O(1)*

**高效方法:**这个想法是基于观察到一些字符只出现在一个数字中。

> 在“零”中，字符“z”是唯一的。
> 在‘二’中，字符‘w’是唯一的。
> 在‘四’中，字符‘u’是唯一的。
> 在‘六’中，人物‘x’是独一无二的。
> 在‘八’中，字符‘g’是唯一的。
> 在“三”字中，“h”字是独一无二的，因为已经考虑到“八”字有“h”字。
> 在“一”中，字符“o”是唯一的，因为已经考虑了具有字符“o”的单词。
> 在“五”中，字符 f 是唯一的，因为已经考虑了具有字符 f 的“四”字。
> 在‘七’中，人物‘v’是独一无二的。
> 在“九”中，字符“我”是唯一的，因为已经考虑了具有字符“我”的单词。

按照以下步骤解决问题:

*   初始化一个空的[字符串](https://www.geeksforgeeks.org/string-data-structure/)、**和**来存储需要的结果。
*   [将字符串](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)的每个字符的频率存储在 **M** 中。
*   [创建一个唯一字符到其对应字符串的映射](https://www.geeksforgeeks.org/python-dictionary/)。
*   [遍历地图](https://www.geeksforgeeks.org/iterate-over-a-dictionary-in-python/)，执行以下步骤:
    *   将数字对应的唯一字符存储在变量 **x** 中。
    *   获取 **M** 中 **x** 的出现，并将其存储在变量 **freq** 中。
    *   将相应的数字 **freq** 次数追加到 **ans** 中。
    *   [遍历 **x** 对应的](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)字，在 **M** 中将其字符的频率递减 **freq** 。
*   打印字符串，结果为**和**。**T3】**

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to construct the original set of digits
// from the string in ascending order
static String construct_digits(String s)
{

    // Store the unique characters
    // corresponding to word and number
    char[] k = { 'z', 'w', 'u', 'x', 'g',
                 'h', 'o', 'f', 'v', 'i' };

    String[] l = { "zero", "two", "four", "six", "eight",
                   "three", "one", "five", "seven", "nine" };

    int[] c = { 0, 2, 4, 6, 8, 3, 1, 5, 7, 9 };

    // Store the required result
    List<Integer> ans = new ArrayList<>();

    // Store the frequency of
    // each character of S
    HashMap<Character, Integer> d = new HashMap<>();
    for(int i = 0; i < s.length(); i++)
    {
        d.put(s.charAt(i),
              d.getOrDefault(s.charAt(i), 0) + 1);
    }

    // Traverse the unique characters
    for(int i = 0; i < k.length; i++)
    {

        // Store the count of k[i] in S
        int x = 0;
        if (d.containsKey(k[i]))
            x = d.get(k[i]);

        // Traverse the corresponding word
        for(int j = 0; j < l[i].length(); j++)
        {

            // Decrement the frequency
            // of characters by x
            if (d.containsKey(l[i].charAt(j)))
                d.put(l[i].charAt(j),
                d.get(l[i].charAt(j)) - x);
        }

        // Append the digit x times to ans
        for(int j = 0; j < x; j++)
            ans.add(c[i]);
    }

    // Sort the digits in ascending order
    Collections.sort(ans);
    String str = "";
    for(int val : ans)
        str += val;

    return str;
}

// Driver Code
public static void main(String[] args)
{

    // Given string, s
    String s = "fviefuro";

    // Function Call
    System.out.println(construct_digits(s));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python program to implement the above approach
from collections import Counter

# Function to construct the original set of digits
# from the string in ascending order
def construct_digits(s):

    # Store the unique characters
    # corresponding to word and number
    k = ["z", "w", "u", "x", "g",
         "h", "o", "f", "v", "i"]

    l = ["zero", "two", "four", "six", "eight",
         "three", "one", "five", "seven", "nine"]

    c = [0, 2, 4, 6, 8, 3, 1, 5, 7, 9]

    # Store the required result
    ans = []

    # Store the frequency of
    # each character of S
    d = Counter(s)

    # Traverse the unique characters
    for i in range(len(k)):

        # Store the count of k[i] in S
        x = d.get(k[i], 0)

        # Traverse the corresponding word
        for j in range(len(l[i])):

            # Decrement the frequency
            # of characters by x
            d[l[i][j]]-= x

        # Append the digit x times to ans
        ans.append(str(c[i])*x)

    # Sort the digits in ascending order
    ans.sort()

    return "".join(ans)

# Driver Code

# Given string, s
s = "fviefuro"

# Function Call
print(construct_digits(s))
```

## C#

```
// C# program to implement the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to construct the original set of digits
// from the string in ascending order
static string construct_digits(string s)
{

    // Store the unique characters
    // corresponding to word and number
    char[] k = { 'z', 'w', 'u', 'x', 'g',
                 'h', 'o', 'f', 'v', 'i' };

    string[] l = { "zero", "two", "four", "six", "eight",
                   "three", "one", "five", "seven", "nine" };

    int[] c = { 0, 2, 4, 6, 8, 3, 1, 5, 7, 9 };

    // Store the required result
    List<string> ans = new List<string>();

    // Store the frequency of
    // each character of S
    Dictionary<char,
               int> d = new Dictionary<char,
                                       int>();
    for(int i = 0; i < s.Length; i++)
    {
        if (!d.ContainsKey(s[i]))
            d[s[i]] = 0;

        d[s[i]] += 1;
    }

    // Traverse the unique characters
    for(int i = 0; i < k.Length; i++)
    {

        // Store the count of k[i] in S
        int x = 0;
        if (d.ContainsKey(k[i]))
            x = d[k[i]];

        // Traverse the corresponding word
        for(int j = 0; j < l[i].Length; j++)
        {

            // Decrement the frequency
            // of characters by x
            if (d.ContainsKey(l[i][j]))
                d[l[i][j]] -= x;
        }

        // Append the digit x times to ans
        ans.Add(((c[i]) * x).ToString());
    }

    // Sort the digits in ascending order
    ans.Sort();

    string str = (String.Join("", ans.ToArray()));
    return str.Replace("0", "");
}

// Driver Code
public static void Main(string[] args)
{

    // Given string, s
    string s = "fviefuro";

    // Function Call
    Console.WriteLine(construct_digits(s));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program to implement the above approach

// Function to construct the original set of digits
// from the string in ascending order
function construct_digits(s)
{

    // Store the unique characters
    // corresponding to word and number
    let k = [ 'z', 'w', 'u', 'x', 'g',
                 'h', 'o', 'f', 'v', 'i' ];

    let l = [ "zero", "two", "four", "six", "eight",
                   "three", "one", "five", "seven", "nine" ];

    let c = [ 0, 2, 4, 6, 8, 3, 1, 5, 7, 9 ];

    // Store the required result
    let ans = [];

    // Store the frequency of
    // each character of S
    let d = new Map();
    for(let i = 0; i < s.length; i++)
    {
        if(!d.has(s[i]))
            d.set(s[i],0);
        d.set(s[i],
              d.get(s[i]) + 1);
    }

    // Traverse the unique characters
    for(let i = 0; i < k.length; i++)
    {

        // Store the count of k[i] in S
        let x = 0;
        if (d.has(k[i]))
            x = d.get(k[i]);

        // Traverse the corresponding word
        for(let j = 0; j < l[i].length; j++)
        {

            // Decrement the frequency
            // of characters by x
            if (d.has(l[i][j]))
                d.set(l[i][j],
                d.get(l[i][j]) - x);
        }

        // Append the digit x times to ans
        for(let j = 0; j < x; j++)
            ans.push(c[i]);
    }

    // Sort the digits in ascending order
    ans.sort();

    return ans.join("");
}

// Driver Code
// Given string, s
let s = "fviefuro";
// Function Call
document.write(construct_digits(s));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
45
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*