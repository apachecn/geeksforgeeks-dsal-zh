# 查找与字典中特定模式匹配的所有字符串

给定单词词典，找到与给定模式匹配的所有字符串，其中模式中的每个字符都唯一映射到词典中的字符。

**示例**：

```
Input:  
dict = ["abb", "abc", "xyz", "xyy"];
pattern = "foo"
Output: [xyy abb]
xyy and abb have same character at 
index 1 and 2 like the pattern

Input: 
dict = ["abb", "abc", "xyz", "xyy"];
pat = "mno"
Output: [abc xyz]
abc and xyz have all distinct characters,
similar to the pattern.

Input:  
dict = ["abb", "abc", "xyz", "xyy"];
pattern = "aba"
Output: [] 
Pattern has same character at index 0 and 2\. 
No word in dictionary follows the pattern.

Input:  
dict = ["abab", "aba", "xyz", "xyx"];
pattern = "aba"
Output: [aba xyx]
aba and xyx have same character at 
index 0 and 2 like the pattern

```

**<u>方法 1</u> **：

**方法**：目的是确定单词是否具有与模式相同的结构。 解决此问题的方法可以是对单词和模式进行哈希处理，然后比较它们是否相等。 在简单的语言中，我们为单词的不同字符分配不同的整数，并根据该单词中某个特定字符的出现，生成一串整数**（单词的哈希）**，然后将其与 模式的哈希值。

**示例**：

```
Word='xxyzzaabcdd'
Pattern='mmnoopplfmm'
For word-:
map['x']=1;
map['y']=2;
map['z']=3;
map['a']=4;
map['b']=5;
map['c']=6;
map['d']=7;
Hash for Word="11233445677"

For Pattern-:
map['m']=1;
map['n']=2;
map['o']=3;
map['p']=4;
map['l']=5;
map['f']=6;
Hash for Pattern="11233445611"
Therefore in the given example Hash of word 
is not equal to Hash of pattern so this word 
is not included in the answer

```

**算法**：

*   根据上述方法对模式进行编码，并将模式的相应哈希存储在字符串变量**哈希**中。

*   **编码算法-**：

    *   初始化计数器 **i = 0** ，该计数器将使用不同的整数映射不同的字符。

    *   读取字符串，如果当前字符未映射为整数，则将其映射为计数器值并递增。

    *   将映射到当前字符的整数连接到**哈希字符串**。

*   现在读取每个单词，并使用相同的算法对其进行哈希处理。

*   如果当前单词的哈希值等于模式的哈希值，则该单词将包含在最终答案中。

**伪代码**：

```
int i=0
Declare map
for character in pattern:
   if(map[character]==map.end())
      map[character]=i++;

   hash_pattern+=to_string(mp[character])

for words in dictionary:
   i=0;
   Declare map
   if(words.length==pattern.length)
     for character in words:
         if(map[character]==map.end())
            map[character]=i++

          hash_word+=to_string(map[character)

      if(hash_word==hash_pattern)
      print words

```

## C++

```cpp

// C++ program to print all
// the strings that match the
// given pattern where every
// character in the pattern is
// uniquely mapped to a character
// in the dictionary
#include <bits/stdc++.h>
using namespace std;

// Function to encode given string
string encodeString(string str)
{
    unordered_map<char, int> map;
    string res = "";
    int i = 0;

    // for each character in given string
    for (char ch : str) {

        // If the character is occurring
        // for the first time, assign next
        // unique number to that char
        if (map.find(ch) == map.end())
            map[ch] = i++;

        // append the number associated
        // with current character into the
        // output string
        res += to_string(map[ch]);
    }

    return res;
}

// Function to print all the
// strings that match the
// given pattern where every
// character in the pattern is
// uniquely mapped to a character
// in the dictionary
void findMatchedWords(unordered_set<string> dict,
                      string pattern)
{
    // len is length of the pattern
    int len = pattern.length();

    // Encode the string
    string hash = encodeString(pattern);

    // for each word in the dictionary
    for (string word : dict) {
        // If size of pattern is same as
        // size of current dictionary word
        // and both pattern and the word
        // has same hash, print the word
        if (word.length() == len
            && encodeString(word) == hash)
            cout << word << " ";
    }
}

// Driver code
int main()
{
    unordered_set<string> dict = { "abb", "abc",
                                   "xyz", "xyy" };
    string pattern = "foo";

    findMatchedWords(dict, pattern);

    return 0;
}

```

## Java

```java

// Java program to print all the
// strings that match the
// given pattern where every
// character in the pattern is
// uniquely mapped to a character
// in the dictionary
import java.io.*;
import java.util.*;

class GFG {

    // Function to encode given string
    static String encodeString(String str)
    {
        HashMap<Character, Integer> map = new HashMap<>();
        String res = "";
        int i = 0;

        // for each character in given string
        char ch;
        for (int j = 0; j < str.length(); j++) {
            ch = str.charAt(j);

            // If the character is occurring for the first
            // time, assign next unique number to that char
            if (!map.containsKey(ch))
                map.put(ch, i++);

            // append the number associated with current
            // character into the output string
            res += map.get(ch);
        }

        return res;
    }

    // Function to print all
    // the strings that match the
    // given pattern where every
    // character in the pattern is
    // uniquely mapped to a character
    // in the dictionary
    static void findMatchedWords(
        String[] dict, String pattern)
    {
        // len is length of the pattern
        int len = pattern.length();

        // encode the string
        String hash = encodeString(pattern);

        // for each word in the dictionary array
        for (String word : dict) {
            // If size of pattern is same
            // as size of current
            // dictionary word and both
            // pattern and the word
            // has same hash, print the word
            if (word.length() == len
                && encodeString(word).equals(hash))
                System.out.print(word + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String[] dict = { "abb", "abc",
                          "xyz", "xyy" };
        String pattern = "foo";

        findMatchedWords(dict, pattern);
    }

    // This code is contributed
    // by rachana soma
}

```

## Python3

```py

# Python3 program to print all the 
# strings that match the 
# given pattern where every 
# character in the pattern is 
# uniquely mapped to a character 
# in the dictionary 

# Function to encode 
# given string
def encodeString(Str):

    map = {}
    res = ""
    i = 0

    # For each character 
    # in given string 
    for ch in Str:

        # If the character is occurring 
        # for the first time, assign next
        # unique number to that char 
        if ch not in map:
            map[ch] = i
            i += 1

        # Append the number associated 
        # with current character into 
        # the output string 
        res += str(map[ch])
    return res

# Function to print all 
# the strings that match the 
# given pattern where every 
# character in the pattern is 
# uniquely mapped to a character 
# in the dictionary 
def findMatchedWords(dict, pattern):

    # len is length of the 
    # pattern 
    Len = len(pattern)

    # Encode the string 
    hash = encodeString(pattern)

    # For each word in the 
    # dictionary array 
    for word in dict:

        # If size of pattern is same 
          # as size of current 
        # dictionary word and both 
        # pattern and the word 
        # has same hash, print the word 
        if(len(word) == Len and
           encodeString(word) == hash):
            print(word, end = " ")

# Driver code 
dict = ["abb", "abc","xyz", "xyy" ]
pattern = "foo"
findMatchedWords(dict, pattern)

# This code is contributed by avanitrachhadiya2155

```

## C#

```cs

// C# program to print all the strings
// that match the given pattern where
// every character in the pattern is
// uniquely mapped to a character in the dictionary
using System;
using System.Collections.Generic;
public class GFG {

    // Function to encode given string
    static String encodeString(String str)
    {
        Dictionary<char, int> map = new Dictionary<char, int>();
        String res = "";
        int i = 0;

        // for each character in given string
        char ch;
        for (int j = 0; j < str.Length; j++) {
            ch = str[j];

            // If the character is occurring for the first
            // time, assign next unique number to that char
            if (!map.ContainsKey(ch))
                map.Add(ch, i++);

            // append the number associated with current
            // character into the output string
            res += map[ch];
        }

        return res;
    }

    // Function to print all the
    // strings that match the
    // given pattern where every
    // character in the pattern is
    // uniquely mapped to a character
    // in the dictionary
    static void findMatchedWords(String[] dict, String pattern)
    {
        // len is length of the pattern
        int len = pattern.Length;

        // encode the string
        String hash = encodeString(pattern);

        // for each word in the dictionary array
        foreach(String word in dict)
        {
            // If size of pattern is same as
            // size of current dictionary word
            // and both pattern and the word
            // has same hash, print the word
            if (word.Length == len && encodeString(word).Equals(hash))
                Console.Write(word + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String[] dict = { "abb", "abc", "xyz", "xyy" };
        String pattern = "foo";

        findMatchedWords(dict, pattern);
    }
}

// This code is contributed by 29AjayKumar

```

**Output:**

```
xyy abb

```

**复杂度分析**：

*   **时间复杂度**：O（N * K）。

    这里的“ N”是单词数，“ K”是其长度。 由于我们必须分别遍历每个单词以创建其哈希。

*   **辅助空间**：O（N）。

    使用 **hash_map** 数据结构映射字符会占用此空间。

**<u>方法 2</u> **：

**方法**：现在让我们讨论一种更具概念性的方法，它是地图的更好应用。 我们可以为每个单词映射对应的单词字母，而不是对每个单词进行散列。 如果当前字符尚未映射，请将其映射到单词的对应字符，如果已经映射，则检查先前映射的值是否与单词的当前值相同 。 下面的示例将使事情变得易于理解。

**例如**：

```
Word='xxyzzaa'
Pattern='mmnoopp'
Step 1-: map['m'] = x
Step 2-: 'm' is already mapped to some value, 
check whether that value is equal to current 
character of word-:YES ('m' is mapped to x).
Step 3-: map['n'] = y
Step 4-: map['o'] = z 
Step 5-: 'o' is already mapped to some value, 
check whether that value is equal to current 
character of word-:YES ('o' is mapped to z).
Step 6-: map['p'] = a
Step 7-: 'p' is already mapped to some value, 
check whether that value is equal to current 
character of word-: YES ('p' is mapped to a).
No contradiction so current word matches the pattern

```

**算法**：

1.  创建一个字符数组，在其中可以将模式的字符与单词的相应字符映射。

2.  首先检查单词和模式的长度是否相等，如果**否**，则检查下一个单词。

3.  如果长度相等，则遍历该模式，如果尚未映射该模式的当前字符，则将其映射到单词的相应字符。

4.  如果当前字符已映射，则检查与它映射的字符是否等于单词的当前字符。

5.  如果**否**，则该单词不遵循给定的模式。

6.  如果单词遵循模式直到最后一个字符，则打印单词。

**伪代码**：

```
for words in dictionary:
   char arr_map[128]=0
   if(words.length==pattern.length)
     for character in pattern:
         if(arr_map[character]==0)
            arr_map[character]=word[character]

          else if(arr_map[character]!=word[character]
          break the loop

If above loop runs successfully
Print(words) 

```

## C++

```cpp

// C++ program to print all
// the strings that match the
// given pattern where every
// character in the pattern is
// uniquely mapped to a character
// in the dictionary
#include <bits/stdc++.h>
using namespace std;

bool check(string pattern, string word)
{
    if (pattern.length() != word.length())
        return false;

    char ch[128] = { 0 };

    int len = word.length();

    for (int i = 0; i < len; i++) {
        if (ch[pattern[i]] == 0)
            ch[pattern[i]] = word[i];
        else if (ch[pattern[i]] != word[i])
            return false;
    }

    return true;
}

// Function to print all the
// strings that match the
// given pattern where every
// character in the pattern is
// uniquely mapped to a character
// in the dictionary
void findMatchedWords(unordered_set<string> dict,
                      string pattern)
{
    // len is length of the pattern
    int len = pattern.length();

    // for each word in the dictionary
    for (string word : dict) {

        if (check(pattern, word))
            cout << word << " ";
    }
}

// Driver code
int main()
{
    unordered_set<string> dict = { "abb", "abc", "xyz", "xyy" };
    string pattern = "foo";

    findMatchedWords(dict, pattern);

    return 0;
}

// This code is contributed by Ankur Goel

```

**Output:**

```
xyy abb

```

**复杂度分析**：

*   **时间复杂度**：O（N * K），其中“ N”是单词数，“ K”是其长度。

    要遍历每个单词，这是时间要求。

*   **辅助空间**：O（N）。

    将 **hash_map** 数据结构用于映射字符会占用 N 空间。

本文由 **Aditya Goel** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

