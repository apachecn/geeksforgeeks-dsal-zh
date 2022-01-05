# 检查给定的单词串是否可以由字典中的单词构成

> 原文:[https://www . geesforgeks . org/check-if-给定的单词串可以由字典中的单词构成/](https://www.geeksforgeeks.org/check-if-the-given-string-of-words-can-be-formed-from-words-present-in-the-dictionary/)

给定 M 个单词的字符串数组和 N 个单词的字典。任务是检查给定的单词串是否可以由字典中的单词组成。

**示例:**

> dict[] = { find，a，geek，all，for，on，geek，answers，inter }
> **输入:**str[]= {“find”，“all”，“answers”，“on”，“geek”，“for”，“geek”}；
> **输出:**是
> str[]的所有单词都存在于字典中，因此输出为是
> 
> **输入:**str = {“find”、“a”、“geek”}
> **输出:** NO
> 在 str[]中，“find”和“a”出现在字典中，但“geek”不出现在字典中，因此输出为 NO

一种**天真的方法**是将输入句子的所有单词分别与字典中的每个单词进行匹配，并保持字典中所有单词的出现次数的计数。因此，如果字典中的单词数是 N，句子中的单词数是 M，这个算法将花费 O(M*N)个时间。

一种**更好的方法**将是使用高级数据结构的修改版本 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 时间复杂度可以降低到 **O(M * t)** 其中 t 是字典中最长单词的长度，小于 n。因此这里对 Trie 节点进行了修改，使得 *isEnd* 变量现在是存储在该节点上结束的单词的出现计数的整数。此外，搜索功能已被修改为在 trie 中查找单词，一旦找到，则减少该节点的 isEnd 计数，以便对于一个单词在句子中的多次出现，每个单词都与词典中该单词的单独出现相匹配。

以下是上述方法的图示:

## C++

```
// C++ program to check if a sentence
// can be formed from a given set of words.
#include <bits/stdc++.h>
using namespace std;
const int ALPHABET_SIZE = 26;

// here isEnd is an integer that will store
// count of words ending at that node
struct trieNode {
    trieNode* t[ALPHABET_SIZE];
    int isEnd;
};

// utility function to create a new node
trieNode* getNode()
{
    trieNode* temp = new (trieNode);

    // Initialize new node with null
    for (int i = 0; i < ALPHABET_SIZE; i++)
        temp->t[i] = NULL;
    temp->isEnd = 0;
    return temp;
}

// Function to insert new words in trie
void insert(trieNode* root, string key)
{
    trieNode* trail;
    trail = root;

    // Iterate for the length of a word
    for (int i = 0; i < key.length(); i++) {

        // If the next key does not contains the character
        if (trail->t[key[i] - 'a'] == NULL) {
            trieNode* temp;
            temp = getNode();
            trail->t[key[i] - 'a'] = temp;
        }
        trail = trail->t[key[i] - 'a'];
    }

    // isEnd is increment so not only the word but its count is also stored
    (trail->isEnd)++;
}
// Search function to find a word of a sentence
bool search_mod(trieNode* root, string word)
{
    trieNode* trail;
    trail = root;

    // Iterate for the complete length of the word
    for (int i = 0; i < word.length(); i++) {

        // If the character is not present then word
        // is also not present
        if (trail->t[word[i] - 'a'] == NULL)
            return false;

        // If present move to next character in Trie
        trail = trail->t[word[i] - 'a'];
    }

    // If word foundthen decrement count of the word
    if ((trail->isEnd) > 0 && trail != NULL) {
        // if the word is found decrement isEnd showing one
        // occurrence of this word is already taken so
        (trail->isEnd)--;
        return true;
    }
    else
        return false;
}
// Function to check if string can be
// formed from the sentence
void checkPossibility(string sentence[], int m, trieNode* root)
{
    int flag = 1;

    // Iterate for all words in the string
    for (int i = 0; i < m; i++) {

        if (search_mod(root, sentence[i]) == false) {

            // if a word is not found in a string then the
            // sentence cannot be made from this dictionary of words
            cout << "NO";

            return;
        }
    }

    // If possible
    cout << "YES";
}

// Function to insert all the words of dictionary in the Trie
void insertToTrie(string dictionary[], int n,
                  trieNode* root)
{

    for (int i = 0; i < n; i++)
        insert(root, dictionary[i]);
}

// Driver Code
int main()
{
    trieNode* root;
    root = getNode();

    // Dictionary of words
    string dictionary[] = { "find", "a", "geeks",
                            "all", "for", "on",
                            "geeks", "answers", "inter" };
    int N = sizeof(dictionary) / sizeof(dictionary[0]);

    // Calling Function to insert words of dictionary to tree
    insertToTrie(dictionary, N, root);

    // String to be checked
    string sentence[] = { "find", "all", "answers", "on",
                          "geeks", "for", "geeks" };

    int M = sizeof(sentence) / sizeof(sentence[0]);

    // Function call to check possibility
    checkPossibility(sentence, M, root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to check if a sentence
# can be formed from a given set of words.
#include <bits/stdc++.h>

ALPHABET_SIZE = 26;

# here isEnd is an integer that will store
# count of words ending at that node
class trieNode:

    def __init__(self):

        self.t = [None for i in range(ALPHABET_SIZE)]
        self.isEnd = 0

# utility function to create a new node
def getNode():

    temp = trieNode()
    return temp;

# Function to insert new words in trie
def insert(root, key):

    trail = None
    trail = root;

    # Iterate for the length of a word
    for i in range(len(key)):

        # If the next key does not contains the character
        if (trail.t[ord(key[i]) - ord('a')] == None):
            temp = None
            temp = getNode();
            trail.t[ord(key[i]) - ord('a')] = temp;

        trail = trail.t[ord(key[i]) - ord('a')];

    # isEnd is increment so not only
    # the word but its count is also stored
    (trail.isEnd) += 1

# Search function to find a word of a sentence
def search_mod(root, word):

    trail = root;

    # Iterate for the complete length of the word
    for i in range(len(word)):

        # If the character is not present then word
        # is also not present
        if (trail.t[ord(word[i]) - ord('a')] == None):
            return False;

        # If present move to next character in Trie
        trail = trail.t[ord(word[i]) - ord('a')];

    # If word found then decrement count of the word
    if ((trail.isEnd) > 0 and trail != None):

        # if the word is found decrement isEnd showing one
        # occurrence of this word is already taken so
        (trail.isEnd) -= 1
        return True;  
    else:
        return False;

# Function to check if string can be
# formed from the sentence
def checkPossibility(sentence, m, root):
    flag = 1;

    # Iterate for all words in the string
    for i in range(m):

        if (search_mod(root, sentence[i]) == False):

            # if a word is not found in a string then the
            # sentence cannot be made from this dictionary of words
            print('NO', end='')

            return;

    # If possible
    print('YES')

# Function to insert all the words of dict in the Trie
def insertToTrie(dictionary, n, root):
    for i in range(n):
        insert(root, dictionary[i]);

# Driver Code
if __name__=='__main__':

    root = getNode();

    # Dictionary of words
    dictionary = [ "find", "a", "geeks",
                            "all", "for", "on",
                            "geeks", "answers", "inter" ]

    N = len(dictionary)

    # Calling Function to insert words of dictionary to tree
    insertToTrie(dictionary, N, root);

    # String to be checked
    sentence = [ "find", "all", "answers", "on",
                          "geeks", "for", "geeks" ]

    M = len(sentence)

    # Function call to check possibility
    checkPossibility(sentence, M, root);

# This code is contributed by pratham76
```

**Output:** 

```
YES
```

一个有效的方法是使用 T2 地图。记录地图中的字数，迭代字符串，检查地图中是否有单词。如果存在，则减少地图中单词的数量。如果它不存在，那么就不可能从给定的单词字典中得到给定的字符串。

下面是上述方法的实现:

## C++

```
// C++ program to check if a sentence
// can be formed from a given set of words.
#include <bits/stdc++.h>
using namespace std;

// Function to check if the word
// is in the  dictionary or not
bool match_words(string dictionary[], string sentence[],
                 int n, int m)
{
    // map to store all words in
    // dictionary with their count
    unordered_map<string, int> mp;

    // adding all words in map
    for (int i = 0; i < n; i++) {
        mp[dictionary[i]]++;
    }

    // search in map for all
    // words in the sentence
    for (int i = 0; i < m; i++) {
        if (mp[sentence[i]])
            mp[sentence[i]] -= 1;
        else
            return false;
    }

    // all words of sentence are present
    return true;
}

// Driver Code
int main()
{
    string dictionary[] = { "find", "a", "geeks",
                            "all", "for", "on",
                            "geeks", "answers", "inter" };

    int n = sizeof(dictionary) / sizeof(dictionary[0]);

    string sentence[] = { "find", "all", "answers", "on",
                          "geeks", "for", "geeks" };

    int m = sizeof(sentence) / sizeof(sentence[0]);

    // Calling function to check if words are
    // present in the dictionary or not
    if (match_words(dictionary, sentence, n, m))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a sentence
// can be formed from a given set of words.
import java.util.*;

class GFG
{

// Function to check if the word
// is in the dictionary or not
static boolean match_words(String dictionary[], String sentence[],
                                                    int n, int m)
{
    // map to store all words in
    // dictionary with their count
    Map<String,Integer> mp = new HashMap<>();

    // adding all words in map
    for (int i = 0; i < n; i++)
    {
        if(mp.containsKey(dictionary[i]))
        {
            mp.put(dictionary[i], mp.get(dictionary[i])+1);
        }
        else
        {
            mp.put(dictionary[i], 1);
        }
    }

    // search in map for all
    // words in the sentence
    for (int i = 0; i < m; i++)
    {
        if (mp.containsKey(sentence[i]))
            mp.put(sentence[i],mp.get(sentence[i])-1);
        else
            return false;
    }

    // all words of sentence are present
    return true;
}

// Driver Code
public static void main(String[] args)
{
    String dictionary[] = { "find", "a", "geeks",
                            "all", "for", "on",
                            "geeks", "answers", "inter" };

    int n = dictionary.length;

    String sentence[] = { "find", "all", "answers", "on",
                        "geeks", "for", "geeks" };

    int m = sentence.length;

    // Calling function to check if words are
    // present in the dictionary or not
    if (match_words(dictionary, sentence, n, m))
        System.out.println("YES");
    else
        System.out.println("NO");
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to check if a sentence
# can be formed from a given set of words.

# Function to check if the word
# is in the dictionary or not
def match_words(dictionary, sentence, n, m):

    # map to store all words in
    # dictionary with their count
    mp = dict()

    # adding all words in map
    for i in range(n):
        mp[dictionary[i]] = mp.get(dictionary[i], 0) + 1

    # search in map for all
    # words in the sentence
    for i in range(m):
        if (mp[sentence[i]]):
            mp[sentence[i]] -= 1
        else:
            return False

    # all words of sentence are present
    return True

# Driver Code
dictionary = ["find", "a", "geeks", "all", "for",
              "on", "geeks", "answers", "inter"]

n = len(dictionary)

sentence = ["find", "all", "answers", "on",
            "geeks", "for", "geeks"]

m = len(sentence)

# Calling function to check if words are
# present in the dictionary or not
if (match_words(dictionary, sentence, n, m)):
    print("YES")
else:
    print("NO")

# This code is contributed by mohit kumar
```

## C#

```
// C# program to check if a sentence
// can be formed from a given set of words.
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if the word
// is in the dictionary or not
static Boolean match_words(String []dictionary,
                           String []sentence,
                           int n, int m)
{
    // map to store all words in
    // dictionary with their count
    Dictionary<String,
               int> mp = new Dictionary<String,
                                        int>();

    // adding all words in map
    for (int i = 0; i < n; i++)
    {
        if(mp.ContainsKey(dictionary[i]))
        {
            mp[dictionary[i]] = mp[dictionary[i]] + 1;
        }
        else
        {
            mp.Add(dictionary[i], 1);
        }
    }

    // search in map for all
    // words in the sentence
    for (int i = 0; i < m; i++)
    {
        if (mp.ContainsKey(sentence[i]) && mp[sentence[i]] > 0)
            mp[sentence[i]] = mp[sentence[i]] - 1;
        else
            return false;
    }

    // all words of sentence are present
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    String []dictionary = { "find", "a", "geeks",
                            "all", "for", "on",
                            "geeks", "answers", "inter" };

    int n = dictionary.Length;

    String []sentence = { "find", "all", "answers", "on",
                          "geeks", "for", "geeks", "geeks" };

    int m = sentence.Length;

    // Calling function to check if words are
    // present in the dictionary or not
    if (match_words(dictionary, sentence, n, m))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to check if a sentence
// can be formed from a given set of words.

// Function to check if the word
// is in the  dictionary or not   
function match_words(dictionary, sentence, n, m)
{

    // map to store all words in
    // dictionary with their count
    let mp = new Map();

    // Adding all words in map
    for(let i = 0; i < n; i++)
    {
        if(mp.has(dictionary[i]))
        {
            mp.set(dictionary[i],
            mp.get(dictionary[i]) + 1);
        }
        else
        {
            mp.set(dictionary[i], 1);
        }
    }

    // Search in map for all
    // words in the sentence
    for(let i = 0; i < m; i++)
    {
        if (mp.has(sentence[i]))
            mp.set(sentence[i],
            mp.get(sentence[i]) - 1);
        else
            return false;
    }

    // All words of sentence are present
    return true;
}

// Driver code
let dictionary = [ "find", "a", "geeks",
                   "all", "for", "on",
                   "geeks", "answers", "inter" ];

let n = dictionary.length;

let sentence = [ "find", "all", "answers", "on",
                 "geeks", "for", "geeks" ];

let m = sentence.length;

// Calling function to check if words are
// present in the dictionary or not
if (match_words(dictionary, sentence, n, m))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(M)