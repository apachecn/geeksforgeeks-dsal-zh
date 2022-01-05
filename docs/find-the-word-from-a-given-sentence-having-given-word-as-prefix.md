# 从一个给定的句子中找出一个单词作为前缀

> 原文:[https://www . geeksforgeeks . org/从给定句子中找到单词以给定单词作为前缀/](https://www.geeksforgeeks.org/find-the-word-from-a-given-sentence-having-given-word-as-prefix/)

给定一个代表一个句子的字符串 **S** 和另一个字符串**单词**，任务是从 **S** 中找到这个单词，这个单词有字符串**单词**作为[前缀](https://www.geeksforgeeks.org/longest-common-prefix-using-divide-and-conquer-algorithm/)。如果字符串中没有这样的单词，打印 **-1** 。

**示例:**

> **输入:** S =“欢迎来到 Geeksforgeeks”，word =“Gee”
> **输出:** Geeksforgeeks
> **解释:**
> 句子中的“Geeksforgeeks”一词有前缀“Gee”。
> 
> **输入:** s=“竞技编程”，word =“kdflk”
> **输出:** -1
> **解释:**
> 字符串中没有单词以“kdflk”为前缀。

**方法:**按照以下步骤查找哪个单词有给定的前缀:

1.  使用[字符串流](https://www.geeksforgeeks.org/stringstream-c-applications/)从句子中提取单词，并将它们存储在字符串向量中。
2.  现在，遍历数组并检查哪个单词包含给定的单词作为它自己的前缀。
3.  如果发现任何一个单词都是正确的，那么打印这个单词。否则，如果没有找到这样的字，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the position
// of the string having word as prefix
string isPrefixOfWord(string sentence,
                      string Word)
{
    stringstream ss(sentence);

    // Initialize a vector
    vector<string> v;
    string temp;

    // Extract words from the sentence
    while (ss >> temp) {
        v.push_back(temp);
    }

    // Traverse each word
    for (int i = 0; i < v.size(); i++) {

        // Traverse the characters of word
        for (int j = 0; j < v[i].size(); j++) {

            // If prefix does not match
            if (v[i][j] != Word[j])
                break;

            // Otherwise
            else if (j == Word.size() - 1)

                // Return  the word
                return v[i];
        }
    }

    // Return -1 if not present
    return "-1";
}

// Driver code
int main()
{
    string s = "Welcome to Geeksforgeeks";
    string word = "Gee";

    cout << isPrefixOfWord(s, word) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;
import java.lang.Math;

class GFG{

// Function to find the position
// of the string having word as prefix
static String isPrefixOfWord(String sentence,
                             String Word)
{
    String a[] = sentence.split(" ");

    // Initialize an ArrayList
    ArrayList<String> v = new ArrayList<>();

    // Extract words from the sentence
    for(String e : a)
        v.add(e);

    // Traverse each word
    for(int i = 0; i < v.size(); i++)
    {

        // Traverse the characters of word
        for(int j = 0; j < v.get(i).length(); j++)
        {

            // If prefix does not match
            if (v.get(i).charAt(j) != Word.charAt(j))
                break;

            // Otherwise
            else if (j == Word.length() - 1)

                // Return  the word
                return v.get(i);
        }
    }

    // Return -1 if not present
    return "-1";
}

// Driver code 
public static void main(final String[] args)
{
    String s = "Welcome to Geeksforgeeks";
    String word = "Gee";

    System.out.println(isPrefixOfWord(s, word));
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the
# position of the string
# having word as prefix
def isPrefixOfWord(sentence, word):

    a=sentence.split(" ")

    # Initialize an List
    v = []

    # Extract words from
    # the sentence
    for i in a:
        v.append(i)

    # Traverse each word
    for i in range(len(v)):

        # Traverse the characters of word
        for j in range(len(v[i])):

            # If prefix does not match
            if(v[i][j] != word[j]):
                break

            # Otherwise
            elif(j == len(word) - 1):

                # Return  the word
                return v[i]

    # Return -1 if not present
    return -1

# Driver code
s = "Welcome to Geeksforgeeks"
word = "Gee"
print(isPrefixOfWord(s, word))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the position
// of the string having word as prefix
static String isPrefixOfWord(String sentence,
                             String Word)
{
  String []a = sentence.Split(' ');

  // Initialize an List
  List<String> v = new List<String>();

  // Extract words from the sentence
  foreach(String e in a)
    v.Add(e);

  // Traverse each word
  for(int i = 0; i < v.Count; i++)
  {
    // Traverse the characters of word
    for(int j = 0; j < v[i].Length; j++)
    {
      // If prefix does not match
      if (v[i][j] != Word[j])
        break;

      // Otherwise
      else if (j == Word.Length - 1)

        // Return  the word
        return v[i];
    }
  }

  // Return -1 if not present
  return "-1";
}

// Driver code 
public static void Main(String[] args)
{
  String s = "Welcome to Geeksforgeeks";
  String word = "Gee";
  Console.WriteLine(isPrefixOfWord(s, word));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
//Javascript  program for the above approach

// Function to find the position
// of the string having word as prefix
function isPrefixOfWord(sentence, Word)
{
    var a = sentence.split(" ");

    // Initialize an ArrayList
    var v = [];

    // Extract words from the sentence
    //for(String e : a)
    for(var i=0;i<a.length;i++)
    {
        v.push(a[i]);
    }
    // Traverse each word
    for(var i = 0; i < v.length; i++)
    {

        // Traverse the characters of word
        for(var j = 0; j < v[i].length; j++)
        {

            // If prefix does not match
            if (v[i].charAt(j) != Word[j])
                break;

            // Otherwise
            else if (j == Word.length- 1)

                // Return  the word
                return v[i];
        }
    }

    // Return -1 if not present
    return "-1";
}

var s = "Welcome to Geeksforgeeks";
var word = "Gee";
document.write(isPrefixOfWord(s, word));

//This code in contributed by SoumikMondal
</script>
```

**Output:** 

```
Geeksforgeeks
```

***时间复杂度:** O(L)，其中 L 表示字符串 S 的长度*
***辅助空间:** O(L)*