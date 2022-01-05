# 使用 Trie

实现字典

> 原文:[https://www . geeksforgeeks . org/implement-a-dictionary-using-trie/](https://www.geeksforgeeks.org/implement-a-dictionary-using-trie/)

使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 实现一个字典，这样如果输入是一个代表一个单词的字符串，程序会从预先构建的字典中打印出它的意思。

**示例:**

> **输入:** str = "map"
> **输出:**一个区域的图解表示
> 
> **输入:** str = "language"
> **输出:**人类交流的方法

**方法:**我们可以使用一个 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 来高效地存储字符串并进行搜索。这里，讨论了使用 Trie(使用哈希映射的内存优化)的字典的实现。我们向 Trie 节点添加另一个字段，它是一个保存单词含义的字符串。在搜索所需单词的含义时，我们在 Trie 中搜索该单词，如果该单词存在(即 isEndOfWord = true)，则返回其含义，否则返回空字符串。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure for Trie
struct Trie {
    bool isEndOfWord;
    unordered_map<char, Trie*> map;
    string meaning;
};

// Function to create a new Trie node
Trie* getNewTrieNode()
{
    Trie* node = new Trie;
    node->isEndOfWord = false;
    return node;
}

// Function to insert a word with its meaning
// in the dictionary built using a Trie
void insert(Trie*& root, const string& str,
            const string& meaning)
{

    // If root is null
    if (root == NULL)
        root = getNewTrieNode();

    Trie* temp = root;
    for (int i = 0; i < str.length(); i++) {
        char x = str[i];

        // Make a new node if there is no path
        if (temp->map.find(x) == temp->map.end())
            temp->map[x] = getNewTrieNode();

        temp = temp->map[x];
    }

    // Mark end of word and store the meaning
    temp->isEndOfWord = true;
    temp->meaning = meaning;
}

// Function to search a word in the Trie
// and return its meaning if the word exists
string getMeaning(Trie* root, const string& word)
{

    // If root is null i.e. the dictionary is empty
    if (root == NULL)
        return "";

    Trie* temp = root;

    // Search a word in the Trie
    for (int i = 0; i < word.length(); i++) {
        temp = temp->map[word[i]];
        if (temp == NULL)
            return "";
    }

    // If it is the end of a valid word stored
    // before then return its meaning
    if (temp->isEndOfWord)
        return temp->meaning;
    return "";
}

// Driver code
int main()
{
    Trie* root = NULL;

    // Build the dictionary
    insert(root, "language", "the method of human communication");
    insert(root, "computer", "A computer is a machine that can be \
    instructed to carry out sequences of arithmetic or \
logical operations automatically via computer programming");
    insert(root, "map", "a diagrammatic representation \
of an area");
    insert(root, "book", "a written or printed work \
consisting of pages glued or sewn together along one \
side and bound in covers.");
    insert(root, "science", "the intellectual and \
practical activity encompassing the systematic study \
of the structure and behaviour of the physical and \
natural world through observation and experiment.");

    string str = "map";
    cout << getMeaning(root, str);

    return 0;
}
```

**Output:**

```
a diagrammatic representation of an area

```