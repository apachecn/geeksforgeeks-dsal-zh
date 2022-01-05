# 使用 Trie

打印字典中所有可能的单词组合

> 原文:[https://www . geesforgeks . org/print-所有可能的单词组合-来自字典-使用-trie/](https://www.geeksforgeeks.org/print-all-possible-combinations-of-words-from-dictionary-using-trie/)

给定一个字符串数组 **arr[]** ，对于数组中的每个字符串，打印所有可能的字符串组合，这些组合可以连接在一起构成该单词。

**示例:**

```
Input: arr[] = ["sam", "sung", "samsung"]
Output:
sam: 
    sam
sung: 
    sung
samsung: 
    sam sung
    samsung
String 'samsung' can be formed using two different 
strings from the array i.e. 'sam' and 'sung' whereas 
'samsung' itself is also a string in the array.

Input: arr[] = ["ice", "cream", "icecream"]
Output:
ice: 
    ice
cream: 
    cream
icecream: 
    ice cream
    icecream

```

**进场:**

*   将所有给定的字符串添加到 [trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 中。
*   逐个字符地处理每个前缀，并通过搜索检查它是否构成了单词。
*   如果前缀出现在 trie 中，则将其添加到结果中，并继续使用字符串中的剩余后缀。
*   一旦到达字符串的末尾，打印所有找到的组合。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

const int ALPHABET_SIZE = 26;

// Trie node
struct TrieNode {
    struct TrieNode* children[ALPHABET_SIZE];

    // isEndOfWord is true if node
    // represents the end of the word
    bool isEndOfWord;
};

// Returns new trie node
struct TrieNode*
getNode(void)
{
    struct TrieNode* pNode = new TrieNode;

    pNode->isEndOfWord = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode->children[i] = NULL;

    return pNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node,
// marks the node as leaf node
void insert(struct TrieNode* root, string key)
{
    struct TrieNode* pCrawl = root;

    for (int i = 0; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        pCrawl = pCrawl->children[index];
    }

    // Mark node as leaf
    pCrawl->isEndOfWord = true;
}

// Returns true if the key is present in the trie
bool search(struct TrieNode* root, string key)
{
    struct TrieNode* pCrawl = root;

    for (int i = 0; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            return false;

        pCrawl = pCrawl->children[index];
    }

    return (pCrawl != NULL && pCrawl->isEndOfWord);
}

// Result stores the current prefix with
// spaces between words
void wordBreakAll(TrieNode* root,
                  string word, int n, string result)
{
    // Process all prefixes one by one
    for (int i = 1; i <= n; i++) {

        // Extract substring from 0 to i in prefix
        string prefix = word.substr(0, i);

        // If trie conatins this prefix then check
        // for the remaining string.
        // Otherwise ignore this prefix
        if (search(root, prefix)) {

            // If no more elements are there then print
            if (i == n) {

                // Add this element to the previous prefix
                result += prefix;

                // If(result == word) then return
                // If you don't want to print last word
                cout << "\t" << result << endl;
                return;
            }
            wordBreakAll(root, word.substr(i, n - i), n - i,
                         result + prefix + " ");
        }
    }
}

// Driver code
int main()
{
    struct TrieNode* root = getNode();

    string dictionary[] = {
        "sam", "sung",
        "samsung"
    };
    int n = sizeof(dictionary) / sizeof(string);

    for (int i = 0; i < n; i++) {
        insert(root, dictionary[i]);
    }

    for (int i = 0; i < n; i++) {
        cout << dictionary[i] << ": \n";
        wordBreakAll(root, dictionary[i],
                     dictionary[i].length(), "");
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int ALPHABET_SIZE = 26;

// Trie node
static class TrieNode
{
    TrieNode []children = 
    new TrieNode[ALPHABET_SIZE];

    // isEndOfWord is true if node
    // represents the end of the word
    boolean isEndOfWord;

    public TrieNode()
    {
        super();
    }

};

// Returns new trie node
static TrieNode getNode()
{
    TrieNode pNode = new TrieNode();

    pNode.isEndOfWord = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode.children[i] = null;

    return pNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node,
// marks the node as leaf node
static void insert(TrieNode root, String key)
{
    TrieNode pCrawl = root;

    for (int i = 0; i < key.length(); i++)
    {
        int index = key.charAt(i) - 'a';
        if (pCrawl.children[index] == null)
            pCrawl.children[index] = getNode();

        pCrawl = pCrawl.children[index];
    }

    // Mark node as leaf
    pCrawl.isEndOfWord = true;
}

// Returns true if the key is present in the trie
static boolean search(TrieNode root, String key)
{
    TrieNode pCrawl = root;

    for (int i = 0; i < key.length(); i++)
    {
        int index = key.charAt(i) - 'a';
        if (pCrawl.children[index] == null)
            return false;

        pCrawl = pCrawl.children[index];
    }

    return (pCrawl != null && pCrawl.isEndOfWord);
}

// Result stores the current prefix with
// spaces between words
static void wordBreakAll(TrieNode root,
                String word, int n, String result)
{
    // Process all prefixes one by one
    for (int i = 1; i <= n; i++) 
    {

        // Extract subString from 0 to i in prefix
        String prefix = word.substring(0, i);

        // If trie conatins this prefix then check
        // for the remaining String.
        // Otherwise ignore this prefix
        if (search(root, prefix))
        {

            // If no more elements are there then print
            if (i == n) 
            {

                // Add this element to the previous prefix
                result += prefix;

                // If(result == word) then return
                // If you don't want to print last word
                System.out.print("\t" + result +"\n");
                return;
            }
            wordBreakAll(root, word.substring(i, n), n - i,
                        result + prefix + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    new TrieNode();
    TrieNode root = getNode();

    String dictionary[] = {"sam", "sung",
                            "samsung"};
    int n = dictionary.length;

    for (int i = 0; i < n; i++)
    {
        insert(root, dictionary[i]);
    }

    for (int i = 0; i < n; i++)
    {
        System.out.print(dictionary[i]+ ": \n");
        wordBreakAll(root, dictionary[i],
                    dictionary[i].length(), "");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int ALPHABET_SIZE = 26;

// Trie node
class TrieNode
{
    public TrieNode []children = 
    new TrieNode[ALPHABET_SIZE];

    // isEndOfWord is true if node
    // represents the end of the word
    public bool isEndOfWord;

    public TrieNode()
    {
    }

};

// Returns new trie node
static TrieNode getNode()
{
    TrieNode pNode = new TrieNode();

    pNode.isEndOfWord = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode.children[i] = null;

    return pNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node,
// marks the node as leaf node
static void insert(TrieNode root, String key)
{
    TrieNode pCrawl = root;

    for (int i = 0; i < key.Length; i++)
    {
        int index = key[i] - 'a';
        if (pCrawl.children[index] == null)
            pCrawl.children[index] = getNode();

        pCrawl = pCrawl.children[index];
    }

    // Mark node as leaf
    pCrawl.isEndOfWord = true;
}

// Returns true if the key is present in the trie
static bool search(TrieNode root, String key)
{
    TrieNode pCrawl = root;

    for (int i = 0; i < key.Length; i++)
    {
        int index = key[i] - 'a';
        if (pCrawl.children[index] == null)
            return false;

        pCrawl = pCrawl.children[index];
    }

    return (pCrawl != null && pCrawl.isEndOfWord);
}

// Result stores the current prefix with
// spaces between words
static void wordBreakAll(TrieNode root,
                String word, int n, String result)
{
    // Process all prefixes one by one
    for (int i = 1; i <= n; i++) 
    {

        // Extract subString from 0 to i in prefix
        String prefix = word.Substring(0, i);

        // If trie conatins this prefix then check
        // for the remaining String.
        // Otherwise ignore this prefix
        if (search(root, prefix))
        {

            // If no more elements are there then print
            if (i == n) 
            {

                // Add this element to the previous prefix
                result += prefix;

                // If(result == word) then return
                // If you don't want to print last word
                Console.Write("\t" + result +"\n");
                return;
            }
            wordBreakAll(root, word.Substring(i, n - i), n - i,
                        result + prefix + " ");
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    new TrieNode();
    TrieNode root = getNode();

    String []dictionary = {"sam", "sung",
                            "samsung"};
    int n = dictionary.Length;

    for (int i = 0; i < n; i++)
    {
        insert(root, dictionary[i]);
    }

    for (int i = 0; i < n; i++)
    {
        Console.Write(dictionary[i]+ ": \n");
        wordBreakAll(root, dictionary[i],
                    dictionary[i].Length, "");
    }
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
sam: 
    sam
sung: 
    sung
samsung: 
    sam sung
    samsung

```