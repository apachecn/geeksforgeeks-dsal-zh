# 组词同组字符

> 原文:[https://www . geesforgeks . org/print-words-together-set-characters/](https://www.geeksforgeeks.org/print-words-together-set-characters/)

给定一个小写的单词列表。实现一个函数来查找所有具有相同唯一字符集的单词。

**示例:**

```
Input: words[] = { "may", "student", "students", "dog",
                 "studentssess", "god", "cat", "act",
                 "tab", "bat", "flow", "wolf", "lambs",
                 "amy", "yam", "balms", "looped", 
                 "poodle"};
Output : 
looped, poodle, 
lambs, balms, 
flow, wolf, 
tab, bat, 
may, amy, yam, 
student, students, studentssess, 
dog, god, 
cat, act, 

All words with same set of characters are printed 
together in a line.
```

想法是使用散列法。我们为所有单词生成一个密钥。密钥包含所有唯一字符(小写字母的密钥大小最多为 26)。我们将单词索引存储为键值。一旦我们填充了哈希表中的所有键和值，我们就可以通过遍历该表来打印结果。

以下是上述想法的实现。

## C++

```
// C++ program to print all words that have
// the same unique character set
#include<bits/stdc++.h>
using namespace std;
#define MAX_CHAR 26

// Generates a key from given string. The key
// contains all unique characters of given string in
// sorted order consisting of only distinct elements.
string getKey(string &str)
{
    bool visited[MAX_CHAR] = { false };

    // store all unique characters of current
    // word in key
    for (int j = 0; j < str.length(); j++)
        visited[str[j] - 'a'] = true ;
    string key = "";
    for (int j=0; j < MAX_CHAR; j++)
        if (visited[j])
            key = key + (char)('a'+j);
    return key;
}

// Print all words together with same character sets.
void wordsWithSameCharSet(string words[], int n)
{
    // Stores indexes of all words that have same
    // set of unique characters.
    unordered_map <string, vector <int> > Hash;

    // Traverse all words
    for (int i=0; i<n; i++)
    {
        string key = getKey(words[i]);
        Hash[key].push_back(i);
    }

    // print all words that have the same unique character set
    for (auto it = Hash.begin(); it!=Hash.end(); it++)
    {
      for (auto v=(*it).second.begin(); v!=(*it).second.end(); v++)
          cout << words[*v] << ", ";
      cout << endl;
    }
}

// Driver program to test above function
int main()
{
    string words[] = { "may", "student", "students", "dog",
                 "studentssess", "god", "cat", "act", "tab",
                 "bat", "flow", "wolf", "lambs", "amy", "yam",
                 "balms", "looped", "poodle"};
    int n = sizeof(words)/sizeof(words[0]);
    wordsWithSameCharSet(words, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all words that have
// the same unique character set
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map.Entry;
public class GFG {

    static final int MAX_CHAR = 26;

    // Generates a key from given string. The key
    // contains all unique characters of given string
    // in sorted order consisting of only distinct elements.
    static String getKey(String str)
    {
        boolean[] visited = new boolean[MAX_CHAR];
        Arrays.fill(visited, false);

        // store all unique characters of current
        // word in key
        for (int j = 0; j < str.length(); j++)
            visited[str.charAt(j) - 'a'] = true ;
        String key = "";
        for (int j=0; j < MAX_CHAR; j++)
            if (visited[j])
                key = key + (char)('a'+j);
        return key;
    }

    // Print all words together with same character sets.
    static void wordsWithSameCharSet(String words[], int n)
    {
        // Stores indexes of all words that have same
        // set of unique characters.
        //unordered_map <string, vector <int> > Hash;
        HashMap<String, ArrayList<Integer>> Hash = new HashMap<>();

        // Traverse all words
        for (int i=0; i<n; i++)
        {
            String key = getKey(words[i]);

            // if the key is already in the map
            // then get its corresponding value
            // and update the list and put it in the map
            if(Hash.containsKey(key))
            {
                ArrayList<Integer> get_al = Hash.get(key);
                get_al.add(i);
                Hash.put(key, get_al);
            }

            // if key is not present in the map
            // then create a new list and add
            // both key and the list
            else
            {
                ArrayList<Integer> new_al = new ArrayList<>();
                new_al.add(i);
                Hash.put(key, new_al);
            }
        }

        // print all words that have the same unique character set
        for (Entry<String, ArrayList<Integer>> it : Hash.entrySet())
        {
            ArrayList<Integer> get =it.getValue();
            for (Integer v:get)
                System.out.print( words[v] + ", ");
            System.out.println();
        }
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        String words[] = { "may", "student", "students", "dog",
                     "studentssess", "god", "cat", "act", "tab",
                     "bat", "flow", "wolf", "lambs", "amy", "yam",
                     "balms", "looped", "poodle"};
        int n = words.length;
        wordsWithSameCharSet(words, n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to print all words that
# have the same unique character set

# Function to group all strings with same characters
from collections import Counter

def groupStrings(input):
    # traverse all strings one by one
    # dict is an empty dictionary
    dict={}

    for word in input:
        # sort the current string and take it's
        # sorted value as key
        # sorted return list of sorted characters
        # we need to join them to get key as string
        # Counter() method returns dictionary with frequency of
        # each character as value
        wordDict=Counter(word)

        # now get list of keys
        key = wordDict.keys()

        # now sort these keys
        key = sorted(key)

        # join these characters to produce key string
        key = ''.join(key)

        # now check if this key already exist in
        # dictionary or not
        # if exist then simply append current word
        # in mapped list on key
        # otherwise first assign empty list to key and
        # then append current word in it
        if key in dict.keys():
            dict[key].append(word)
        else:
            dict[key]=[]
            dict[key].append(word)

        # now traverse complete dictionary and print
        # list of mapped strings in each key separated by ,
    for (key,value) in dict.iteritems():
        print ','.join(dict[key])

# Driver program
if __name__ == "__main__":
    input=['may','student','students','dog','studentssess','god','cat','act','tab','bat','flow','wolf','lambs','amy','yam','balms','looped','poodle']
    groupStrings(input)
```

## C#

```
// C# program to print all words that
// have the same unique character set
using System;
using System.Collections.Generic;

class GFG{

static readonly int MAX_CHAR = 26;

// Generates a key from given string. The
// key contains all unique characters of
// given string in sorted order consisting
// of only distinct elements.
static String getKey(String str)
{
    bool[] visited = new bool[MAX_CHAR];

    // Store all unique characters of current
    // word in key
    for(int j = 0; j < str.Length; j++)
        visited[str[j] - 'a'] = true;

    String key = "";

    for(int j = 0; j < MAX_CHAR; j++)
        if (visited[j])
            key = key + (char)('a' + j);

    return key;
}

// Print all words together with same character sets.
static void wordsWithSameCharSet(String []words, int n)
{

    // Stores indexes of all words that have same
    // set of unique characters.
    //unordered_map <string, vector <int> > Hash;
    Dictionary<String,
               List<int>> Hash = new Dictionary<String,
                                                List<int>>();

    // Traverse all words
    for (int i = 0; i < n; i++)
    {
        String key = getKey(words[i]);

        // If the key is already in the map
        // then get its corresponding value
        // and update the list and put it
        // in the map
        if (Hash.ContainsKey(key))
        {
            List<int> get_al = Hash[key];
            get_al.Add(i);
            Hash[key]= get_al;
        }

        // If key is not present in the map
        // then create a new list and add
        // both key and the list
        else
        {
            List<int> new_al = new List<int>();
            new_al.Add(i);
            Hash.Add(key, new_al);
        }
    }

    // Print all words that have the
    // same unique character set
    foreach(KeyValuePair<String, List<int>> it in Hash)
    {
        List<int> get =it.Value;
        foreach(int v in get)
            Console.Write( words[v] + ", ");

        Console.WriteLine();
    }
}

// Driver code
public static void Main(String []args)
{
    String []words = { "may", "student", "students",
                       "dog", "studentssess", "god",
                       "cat", "act", "tab",
                       "bat", "flow", "wolf",
                       "lambs", "amy", "yam",
                       "balms", "looped", "poodle"};

    int n = words.Length;

    wordsWithSameCharSet(words, n);
}
}

// This code is contributed by Princi Singh
```

**输出:**

```
looped, poodle, 
lambs, balms, 
flow, wolf, 
tab, bat, 
may, amy, yam, 
student, students, studentssess, 
dog, god, 
cat, act, 
```

**时间复杂度:** O(n*k)其中 n 是字典中的字数，k 是一个单词的最大长度。

本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。