# 按字母顺序重新排列单词的位置

> 原文:[https://www . geesforgeks . org/按字母顺序重新排列单词的位置/](https://www.geeksforgeeks.org/reorder-the-position-of-the-words-in-alphabetical-order/)

给定一个字符串数组 **arr[]** ，任务是按字典顺序对字符串重新排序，并打印它们在原始列表中的位置。

**示例:**

> **输入:**arr[]= {“zxc”、“efg”、“jkl”}
> **输出:** 2 3 1
> 排序后的列表将为{“EFG”、“jkl”、“zxc”}，它们的
> 原始位置分别为 2、3 和 1。
> 
> **输入:** arr[] = {“住”、“处”、“行”、“字”、“天”}
> T3】输出: 1 2 5 3 4

**方法:**给所有的单词赋值一个等于它们在数组中位置的整数。然后，他们按照字典顺序对单词列表进行排序，并且改变它们的位置，因此，从排序列表中的第一个单词开始打印它们的位置。

下面是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the ordering of words
void reArrange(string words[], int n)
{

    // Creating list of words and assigning
    // them index numbers
    map<string, int> mp;
    for (int i = 0; i < n; i++)
        mp[words[i]] = i + 1;

    // Sort the list of words
    // lexicographically
    sort(words, words + n);

    // Print the ordering
    for (int i = 0; i < n; i++)
        cout << mp[words[i]] << " ";
}

// Driver Code
int main()
{
    string words[] = { "live", "place", "travel", "word", "sky" };
    int n = sizeof(words) / sizeof(words[0]);
    reArrange(words, n);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    // Function to print the ordering of words
    static void reArrange(String words[], int n)
    {

        // Creating list of words and assigning
        // them index numbers
        HashMap<String, Integer> freq = new HashMap<>();
        for (int i = 0; i < n; i++) {
            freq.put(words[i], (i + 1));
        }

        // Sort the list of words
        // lexicographically
        Arrays.sort(words);

        // Print the ordering
        for (int i = 0; i < n; i++)
            System.out.print(freq.get(words[i]) + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String words[] = { "live", "place", "travel", "word", "sky" };
        int n = words.length;
        reArrange(words, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the ordering of words
def reArrange(words, n):
    # Creating list of words and assigning
    # them index numbers
    mp = {}
    for i in range(n):
        mp[words[i]] = i + 1

    # Sort the list of words
    # lexicographically
    words.sort();

    # Print the ordering
    for i in range(n):
        print(mp[words[i]], end = " ")

# Driver Code

words = [ "live", "place", "travel", "word", "sky" ]
n = len(words)
reArrange(words, n);

# This code is contributed by
# Rajnis09
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to print the ordering of words
    static void reArrange(String[] words, int n)
    {

        // Creating list of words and assigning
        // them index numbers
        Dictionary<String, int> freq = new Dictionary<String, int>();
        for (int i = 0; i < n; i++) {
            freq.Add(words[i], (i + 1));
        }

        // Sort the list of words
        // lexicographically
        Array.Sort(words);

        // Print the ordering
        for (int i = 0; i < n; i++)
            Console.Write(freq[words[i]] + " ");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String[] words = { "live", "place", "travel", "word", "sky" };
        int n = words.Length;
        reArrange(words, n);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

    // Function to print the ordering of words
    function reArrange($words, $n)
    {

        // Creating list of words and assigning
        // them index numbers
        $freq = array();
        for ($i = 0; $i < $n; $i++)
        {
            $freq[$words[$i]] = ($i + 1) ;
        }

        // Sort the list of words
        // lexicographically
        sort($words);

        // Print the ordering
        for ($i = 0; $i < $n; $i++)
            echo $freq[$words[$i]], " " ;
    }

    // Driver Code
    $words = array( "live", "place", "travel", "word", "sky" );
    $n = count($words);
    reArrange($words, $n);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the ordering of words
function reArrange(words, n)
{

    // Creating list of words and assigning
    // them index numbers
    var mp = new Map();
    for (var i = 0; i < n; i++)
        mp.set(words[i], i + 1);

    // Sort the list of words
    // lexicographically
    words.sort();

    // Print the ordering
    for (var i = 0; i < n; i++)
    {
        document.write(mp.get(words[i])+" ");
    }
}

// Driver Code
var words = ["live", "place", "travel", "word", "sky"];
var n = words.length;
reArrange(words, n);

</script>
```

**Output:** 

```
1 2 5 3 4
```