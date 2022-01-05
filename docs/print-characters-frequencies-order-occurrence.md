# 按出现顺序打印字符及其频率

> 原文:[https://www . geesforgeks . org/print-characters-frequency-order-occurrence/](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)

给定字符串**字符串**只包含小写字符。问题是按照字符出现的顺序和下面示例中解释的给定格式打印字符及其频率。

**示例:**

```
Input : str = "geeksforgeeks"
Output : g2 e4 k2 s2 f1 o1 r1

Input : str = "elephant"
Output : e2 l1 p1 h1 a1 n1 t1
```

**来源:** [SAP 面试体验|第 26 集](https://www.geeksforgeeks.org/sap-interview-experience-set-26-campus/)

**方法:**创建一个计数数组来存储给定字符串中每个字符的频率**字符串**。再次遍历字符串**字符串**，检查该字符的频率是否为 0。如果不是 0，则打印字符及其频率，并在哈希表中将其频率更新为 0。这样做是为了不再打印相同的字符。

## C++

```
// C++ implementation to print the character and
// its frequency in order of its occurrence
#include <bits/stdc++.h>
using namespace std;

#define SIZE 26

// function to print the character and its frequency
// in order of its occurrence
void printCharWithFreq(string str)
{
    // size of the string 'str'
    int n = str.size();

    // 'freq[]' implemented as hash table
    int freq[SIZE];

    // initialize all elements of freq[] to 0
    memset(freq, 0, sizeof(freq));

    // accumulate frequency of each character in 'str'
    for (int i = 0; i < n; i++)
        freq[str[i] - 'a']++;

    // traverse 'str' from left to right
    for (int i = 0; i < n; i++) {

        // if frequency of character str[i] is not
        // equal to 0
        if (freq[str[i] - 'a'] != 0) {

            // print the character along with its
            // frequency
            cout << str[i] << freq[str[i] - 'a'] << " ";

            // update frequency of str[i] to 0 so
            // that the same character is not printed
            // again
            freq[str[i] - 'a'] = 0;
        }
    }
}

// Driver program to test above
int main()
{
    string str = "geeksforgeeks";
    printCharWithFreq(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the character and
// its frequency in order of its occurrence
public class Char_frequency {

    static final int SIZE = 26;

    // function to print the character and its
    // frequency in order of its occurrence
    static void printCharWithFreq(String str)
    {
         // size of the string 'str'
        int n = str.length();

        // 'freq[]' implemented as hash table
        int[] freq = new int[SIZE];

        // accumulate frequency of each character
        // in 'str'
        for (int i = 0; i < n; i++)
            freq[str.charAt(i) - 'a']++;

        // traverse 'str' from left to right
        for (int i = 0; i < n; i++) {

            // if frequency of character str.charAt(i)
            // is not equal to 0
            if (freq[str.charAt(i) - 'a'] != 0) {

                // print the character along with its
                // frequency
                System.out.print(str.charAt(i));
                System.out.print(freq[str.charAt(i) - 'a'] + " ");

                // update frequency of str.charAt(i) to
                // 0 so that the same character is not
                // printed again
                freq[str.charAt(i) - 'a'] = 0;
            }
        }
    }

    // Driver program to test above
    public static void main(String args[])
    {
        String str = "geeksforgeeks";
        printCharWithFreq(str);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 implementation to pr the character and
# its frequency in order of its occurrence

# import library
import numpy as np

# Function to print the character and its
# frequency in order of its occurrence
def prCharWithFreq(str) :

    # Size of the 'str'
    n = len(str)

    # Initialize all elements of freq[] to 0
    freq = np.zeros(26, dtype = np.int)

    # Accumulate frequency of each
    # character in 'str'
    for i in range(0, n) :
        freq[ord(str[i]) - ord('a')] += 1

    # Traverse 'str' from left to right
    for i in range(0, n) :

        # if frequency of character str[i] 
        # is not equal to 0
        if (freq[ord(str[i])- ord('a')] != 0) :

            # print the character along
            # with its frequency
            print (str[i], freq[ord(str[i]) - ord('a')],
                                                end = " ")

            # Update frequency of str[i] to 0 so that
            # the same character is not printed again
            freq[ord(str[i]) - ord('a')] = 0

# Driver Code
if __name__ == "__main__" :

    str = "geeksforgeeks";
    prCharWithFreq(str);

# This code is contributed by 'Saloni1297'
```

## C#

```
// C# implementation to print the
// character and its frequency in
// order of its occurrence
using System;

class GFG {
    static int SIZE = 26;

    // function to print the character and its
    // frequency in order of its occurrence
    static void printCharWithFreq(String str)
    {
        // size of the string 'str'
        int n = str.Length;

        // 'freq[]' implemented as hash table
        int[] freq = new int[SIZE];

        // accumulate frequency of each character
        // in 'str'
        for (int i = 0; i < n; i++)
            freq[str[i] - 'a']++;

        // traverse 'str' from left to right
        for (int i = 0; i < n; i++) {

            // if frequency of character str.charAt(i)
            // is not equal to 0
            if (freq[str[i] - 'a'] != 0) {

                // print the character along with its
                // frequency
                Console.Write(str[i]);
                Console.Write(freq[str[i] - 'a'] + " ");

                // update frequency of str.charAt(i) to
                // 0 so that the same character is not
                // printed again
                freq[str[i] - 'a'] = 0;
            }
        }
    }

    // Driver program to test above
    public static void Main()
    {
        String str = "geeksforgeeks";
        printCharWithFreq(str);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to print the
// character and its frequency in
// order of its occurrence
$SIZE = 26;

// function to print the character and
// its frequency in order of its occurrence
function printCharWithFreq($str)
{
    global $SIZE;

    // size of the string 'str'
    $n = strlen($str);

    // 'freq[]' implemented as hash table
    $freq = array_fill(0, $SIZE, NULL);

    // accumulate frequency of each
    // character in 'str'
    for ($i = 0; $i < $n; $i++)
        $freq[ord($str[$i]) - ord('a')]++;

    // traverse 'str' from left to right
    for ($i = 0; $i < $n; $i++)
    {

        // if frequency of character str[i]
        // is not equal to 0
        if ($freq[ord($str[$i]) - ord('a')] != 0)
        {

            // print the character along with
            // its frequency
            echo $str[$i] . $freq[ord($str[$i]) -
                                  ord('a')] . " ";

            // update frequency of str[i] to 0
            // so that the same character is
            // not printed again
            $freq[ord($str[$i]) - ord('a')] = 0;
        }
    }
}

// Driver Code
$str = "geeksforgeeks";
printCharWithFreq($str);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation to print the character and
// its frequency in order of its occurrence

    let SIZE = 26;

    // function to print the character and its
    // frequency in order of its occurrence
    function printCharWithFreq(str)
    {

        // size of the string 'str'
        let n = str.length;

        // 'freq[]' implemented as hash table
        let freq = new Array(SIZE);
        for(let i = 0; i < freq.length; i++)
        {
            freq[i] = 0;
        }

        // accumulate frequency of each character
        // in 'str'
        for (let i = 0; i < n; i++)
            freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // traverse 'str' from left to right
        for (let i = 0; i < n; i++) {

            // if frequency of character str.charAt(i)
            // is not equal to 0
            if (freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] != 0) {

                // print the character along with its
                // frequency
                document.write(str[i]);
                document.write(freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] + " ");

                // update frequency of str.charAt(i) to
                // 0 so that the same character is not
                // printed again
                freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] = 0;
            }
        }
    }

    // Driver program to test above
    let str = "geeksforgeeks";
    printCharWithFreq(str);

    // This code is contributed by rag2127.

</script>
```

**Output**

```
g2 e4 k2 s2 f1 o1 r1 
```

**时间复杂度:** O(n)，其中 **n** 为字符串中的字符数。
**辅助空格:** O(1)，因为只有小写字母。

**替代解决方案(使用哈希)**
我们也可以使用哈希来解决问题。

## C++

```
// C++ implementation to
//print the characters and
// frequencies in order
// of its occurrence
#include <bits/stdc++.h>
using namespace std;

void prCharWithFreq(string s)
{
  // Store all characters and
  // their frequencies in dictionary
  unordered_map<char, int> d;

  for(char i : s)
  {
    d[i]++;
  }

  // Print characters and their
  // frequencies in same order
  // of their appearance
  for(char i : s)
  {
    // Print only if this
    // character is not printed
    // before
    if(d[i] != 0)
    {
      cout << i << d[i] << " ";
      d[i] = 0;
    }
  }
}

// Driver Code
int main()
{
  string s="geeksforgeeks";
  prCharWithFreq(s);
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// print the characters and
// frequencies in order
// of its occurrence
import java.util.*;
class Gfg{
    public static void prCharWithFreq(String s)
    {

        // Store all characters and
        // their frequencies in dictionary
        Map<Character, Integer> d = new HashMap<Character, Integer>();

        for(int i = 0; i < s.length(); i++)
        {
            if(d.containsKey(s.charAt(i)))
            {
                d.put(s.charAt(i), d.get(s.charAt(i)) + 1);
            }
            else
            {
                d.put(s.charAt(i), 1);
            }
        }

        // Print characters and their
        // frequencies in same order
        // of their appearance
        for(int i = 0; i < s.length(); i++)
        {

            // Print only if this
            // character is not printed
            // before
            if(d.get(s.charAt(i)) != 0)
            {
                System.out.print(s.charAt(i));
                System.out.print(d.get(s.charAt(i)) + " ");
                d.put(s.charAt(i), 0);
            }           
        }
    }

    // Driver code
     public static void main(String []args)
     {
       String S = "geeksforgeeks";
       prCharWithFreq(S);
     }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation to print the characters and
# frequencies in order of its occurrence

def prCharWithFreq(str):

    # Store all characters and their frequencies
    # in dictionary
    d = {}
    for i in str:
        if i in d:
            d[i] += 1
        else:
            d[i] = 1

    # Print characters and their frequencies in
    # same order of their appearance
    for i in str:

        # Print only if this character is not printed
        # before. 
        if d[i] != 0:
            print("{}{}".format(i,d[i]), end =" ")
            d[i] = 0

# Driver Code
if __name__ == "__main__" :

    str = "geeksforgeeks";
    prCharWithFreq(str);

# This code is contributed by 'Ankur Tripathi'
```

## C#

```
// C# implementation to
// print the characters and
// frequencies in order
// of its occurrence

using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

public static void prCharWithFreq(string s)
{

  // Store all characters and
  // their frequencies in dictionary
  Dictionary<char,int> d = new Dictionary<char,int>();

  foreach(char i in s)
  {
      if(d.ContainsKey(i))
      {
        d[i]++;
      }
      else
      {
        d[i]=1; 
      }
  }

  // Print characters and their
  // frequencies in same order
  // of their appearance
  foreach(char i in s)
  {
    // Print only if this
    // character is not printed
    // before
    if(d[i] != 0)
    {
        Console.Write(i+d[i].ToString() + " ");
        d[i] = 0;
    }
  }
}

// Driver Code
public static void Main(string []args)
{
  string s="geeksforgeeks";
  prCharWithFreq(s);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>
// Javascript implementation to
//print the characters and
// frequencies in order
// of its occurrence

function prCharWithFreq(s)
{
  // Store all characters and
  // their frequencies in dictionary
  var d = new Map();

  s.split('').forEach(element => {

        if(d.has(element))
        {
            d.set(element, d.get(element)+1);
        }
        else
            d.set(element, 1);
  });

  // Print characters and their
  // frequencies in same order
  // of their appearance

  s.split('').forEach(element => {
    // Print only if this
    // character is not printed
    // before
    if(d.has(element) && d.get(element)!=0)
    {
      document.write( element + d.get(element) + " ");
      d.set(element, 0);
    }
  });
}

// Driver Code
var s="geeksforgeeks";
prCharWithFreq(s);

</script>
```

**Output**

```
g2 e4 k2 s2 f1 o1 r1 
```

#### 方法 3:使用内置的 Python 函数:

我们可以使用 python [Counter()](https://www.geeksforgeeks.org/python-counter-objects-elements/) 方法快速解决这个问题。方法很简单。

1)首先使用 Counter 方法创建一个字典，将字符串作为键，将它们的频率作为值。

2)在本词典中遍历打印关键字及其值

## 蟒蛇 3

```
# Python3 implementation to print the characters and
# frequencies in order of its occurrence
from collections import Counter

def prCharWithFreq(string):

    # Store all characters and their
    # frequencies suing Counter function
    d = Counter(string)

    # Print characters and their frequencies in
    # same order of their appearance
    for i in d:
        print(i+str(d[i]), end=" ")

string = "geeksforgeeks"
prCharWithFreq(string)

# This code is contributed by vikkycirus
```

**Output**

```
g2 e4 k2 s2 f1 o1 r1 
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。