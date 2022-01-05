# 字符串数组中最常见的单词

> 原文:[https://www.geeksforgeeks.org/frequent-word-array-strings/](https://www.geeksforgeeks.org/frequent-word-array-strings/)

给定一组单词，找出其中出现次数最多的单词
示例:

```
Input : arr[] = {"geeks", "for", "geeks", "a", 
                "portal", "to", "learn", "can",
                "be", "computer", "science", 
                 "zoom", "yup", "fire", "in", 
                 "be", "data", "geeks"}
Output : Geeks 
"geeks" is the most frequent word as it 
occurs 3 times
```

一个**简单的解决方案**是运行两个循环并计算每个单词的出现次数。这个解的时间复杂度为 O(n * n * MAX_WORD_LEN)。
一个**高效的解决方案**是使用 [Trie 数据结构](https://www.geeksforgeeks.org/trie-insert-and-search/)。这个想法很简单，首先我们将在三节中插入。在 trie 中，我们记录以节点结尾的字数。我们进行前序遍历，比较每个节点的计数，找到最大出现单词

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP code to find most frequent word in
// an array of strings
#include <bits/stdc++.h>
using namespace std;

/*structing the trie*/
struct Trie {
    string key;
    int cnt;
    unordered_map<char, Trie*> map;
};

/* Function to return a new Trie node */
Trie* getNewTrieNode()
{
    Trie* node = new Trie;
    node->cnt = 0;
    return node;
}

/* function to insert a string */
void insert(Trie*& root, string& str)
{
    // start from root node
    Trie* temp = root;

    for (int i = 0; i < str.length(); i++) {

        char x = str[i];

        /*a new node if path doesn't exists*/
        if (temp->map.find(x) == temp->map.end())
            temp->map[x] = getNewTrieNode();

        // go to next node
        temp = temp->map[x];
    }

    // store key and its count in leaf nodes
    temp->key = str;
    temp->cnt += 1;
}

/* function for preorder traversal */
bool preorder(Trie* temp, int& maxcnt, string& key)
{
    if (temp == NULL)
        return false;

    for (auto it : temp->map) {

        /*leaf node will have non-zero count*/
        if (maxcnt < it.second->cnt) {
            key = it.second->key;
            maxcnt = it.second->cnt;
        }

        // recurse for current node children
        preorder(it.second, maxcnt, key);
    }
}

void mostFrequentWord(string arr[], int n)
{
    // Insert all words in a Trie
    Trie* root = getNewTrieNode();
    for (int i = 0; i < n; i++)
        insert(root, arr[i]);

    // Do preorder traversal to find the
    // most frequent word
    string key;
    int cnt = 0;
    preorder(root, cnt, key);

    cout << "The word that occurs most is : "
         << key << endl;
    cout << "No of times: " << cnt << endl;
}

// Driver code
int main()
{
    // given set of keys
    string arr[] = { "geeks", "for", "geeks", "a",
                     "portal", "to", "learn", "can", "be",
                     "computer", "science", "zoom", "yup",
                     "fire", "in", "be", "data", "geeks" };
    int n = sizeof(arr) / sizeof(arr[0]);

    mostFrequentWord(arr, n);

    return 0;
}
```

**Output**

```
The word that occurs most is : geeks
No of times: 3
```