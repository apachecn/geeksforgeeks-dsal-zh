# 计算一个 Trie 的字数

> 原文:[https://www.geeksforgeeks.org/counting-number-words-trie/](https://www.geeksforgeeks.org/counting-number-words-trie/)

A [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 用于存储词典单词，以便能够高效地搜索它们并进行前缀搜索。任务是编写一个计算字数的函数。

示例:

```
Input :     root
          /   \    \
         t   a     b
         |   |     |
         h   n     y
         |   |  \  |
         e   s  y  e
         /  |   |
         i  r   w
         |  |   |
         r  e   e
                |
                r
Output : 8
Explanation : Words formed in the Trie : 
"the", "a", "there", "answer", "any", "by", 
"bye", "their".

```

在 Trie 结构中，我们有一个字段来存储单词结束标记，我们在下面的实现中称之为 isLeaf。为了计数单词，我们需要简单地遍历 Trie，并计算 isLeaf 被设置的所有节点。

## C++

```
// C++ implementation to count words in a trie
#include <bits/stdc++.h>
using namespace std;

#define ARRAY_SIZE(a) sizeof(a)/sizeof(a[0])

// Alphabet size (# of symbols)
#define ALPHABET_SIZE (26)

// Converts key current character into index
// use only 'a' through 'z' and lower case
#define CHAR_TO_INDEX(c) ((int)c - (int)'a')

// Trie node
struct TrieNode
{
    struct TrieNode *children[ALPHABET_SIZE];

    // isLeaf is true if the node represents
    // end of a word
    bool isLeaf;
};

// Returns new trie node (initialized to NULLs)
struct TrieNode *getNode(void)
{
    struct TrieNode *pNode = new TrieNode;
        pNode->isLeaf = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode->children[i] = NULL;    

    return pNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node, just
// marks leaf node
void insert(struct TrieNode *root, const char *key)
{
    int length = strlen(key);

    struct TrieNode *pCrawl = root;

    for (int level = 0; level < length; level++)
    {
        int index = CHAR_TO_INDEX(key[level]);
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        pCrawl = pCrawl->children[index];
    }

    // mark last node as leaf
    pCrawl->isLeaf = true;
}

// Function to count number of words
int wordCount(struct TrieNode *root)
{
    int result = 0;

    // Leaf denotes end of a word
    if (root -> isLeaf)
        result++;

    for (int i = 0; i < ALPHABET_SIZE; i++)    
      if (root -> children[i])
         result += wordCount(root -> children[i]);

    return result;   
}

// Driver
int main()
{
    // Input keys (use only 'a' through 'z' 
    // and lower case)
    char keys[][8] = {"the", "a", "there", "answer", 
                     "any", "by", "bye", "their"};

    struct TrieNode *root = getNode();

    // Construct Trie
    for (int i = 0; i < ARRAY_SIZE(keys); i++)
        insert(root, keys[i]);

    cout << wordCount(root);

    return 0;
}
```