# 最小断字

> 原文:[https://www.geeksforgeeks.org/minimum-word-break/](https://www.geeksforgeeks.org/minimum-word-break/)

给定一个字符串 s，断开 s，这样分区的每个子字符串都可以在字典中找到。返回所需的最小间隔。
示例:

```
Given a dictionary ["Cat", "Mat", "Ca", 
     "tM", "at", "C", "Dog", "og", "Do"]

Input :  Pattern "CatMat"
Output : 1 
Explanation: we can break the sentences
in three ways, as follows:
CatMat = [ Cat Mat ]  break 1
CatMat = [ Ca tM at ] break 2
CatMat = [ C at Mat ] break 2  so the 
         output is: 1

Input : Dogcat
Output : 1
```

问于:**脸书**T2】

这个问题的解决方案是基于 [WordBreak Trie 解](https://write.geeksforgeeks.org/geek/)和层次有序图。我们开始遍历给定的模式，并开始在[特里](https://www.geeksforgeeks.org/trie-insert-and-search/)中寻找模式的特征。如果我们到达一个 trie 的节点(叶子)，从那里我们可以遍历一个 trie(字典)的新单词，我们增加一级，并调用搜索函数来搜索 trie 中剩余的模式字符。最后，我们返回最小中断。

```
  MinBreak(Trie, key, level, start = 0 )
  ....  If start == key.length()
      ...update min_break
  for i = start to keylenght 
  ....If we found a leaf node in trie 
        MinBreak( Trie, key, level+1, i )
```

以下是以上想法的实现

## C++

```
// C++ program to find minimum breaks needed
// to break a string in dictionary words.
#include <bits/stdc++.h>
using namespace std;

const int ALPHABET_SIZE = 26;

// trie node
struct TrieNode {
    struct TrieNode* children[ALPHABET_SIZE];

    // isEndOfWord is true if the node
    // represents end of a word
    bool isEndOfWord;
};

// Returns new trie node (initialized to NULLs)
struct TrieNode* getNode(void)
{
    struct TrieNode* pNode = new TrieNode;

    pNode->isEndOfWord = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode->children[i] = NULL;

    return pNode;
}

// If not present, inserts the key into the trie
// If the key is the prefix of trie node, just
// marks leaf node
void insert(struct TrieNode* root, string key)
{
    struct TrieNode* pCrawl = root;

    for (int i = 0; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        pCrawl = pCrawl->children[index];
    }

    // mark last node as leaf
    pCrawl->isEndOfWord = true;
}

// function break the string into minimum cut
// such the every substring after breaking
// in the dictionary.
void minWordBreak(struct TrieNode* root,
          string key, int start, int* min_Break,
                                 int level = 0)
{
    struct TrieNode* pCrawl = root;

    // base case, update minimum Break
    if (start == key.length()) {       
        *min_Break = min(*min_Break, level - 1);
        return;
    }

    // traverse given key(pattern)
    int minBreak = 0;  
    for (int i = start; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            return;

        // if we find a condition were we can
        // move to the next word in a trie
        // dictionary
        if (pCrawl->children[index]->isEndOfWord)
            minWordBreak(root, key, i + 1,
                           min_Break, level + 1);

        pCrawl = pCrawl->children[index];
    }
}

// Driver program to test above functions
int main()
{
    string dictionary[] = { "Cat", "Mat",
   "Ca", "Ma", "at", "C", "Dog", "og", "Do" };
    int n = sizeof(dictionary) / sizeof(dictionary[0]);
    struct TrieNode* root = getNode();

    // Construct trie
    for (int i = 0; i < n; i++)
        insert(root, dictionary[i]);
    int min_Break = INT_MAX;

    minWordBreak(root, "CatMatat", 0, &min_Break, 0);
    cout << min_Break << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum breaks needed
// to break a string in dictionary words.
public class Trie {

TrieNode root = new TrieNode();
int minWordBreak = Integer.MAX_VALUE;

    // Trie node
    class TrieNode {
        boolean endOfTree;
        TrieNode children[] = new TrieNode[26];
        TrieNode(){
            endOfTree = false;
            for(int i=0;i<26;i++){
                children[i]=null;
            }
        }
    }

    // If not present, inserts a key into the trie
    // If the key is the prefix of trie node, just
    // marks leaf node
    void insert(String key){
        int length = key.length();

        int index;

        TrieNode pcrawl = root;

        for(int i = 0; i < length; i++)
        {
            index = key.charAt(i)- 'a';

            if(pcrawl.children[index] == null)
                pcrawl.children[index] = new TrieNode();

            pcrawl = pcrawl.children[index];
        }

        // mark last node as leaf
        pcrawl.endOfTree = true;

    }

    // function break the string into minimum cut
    // such the every substring after breaking
    // in the dictionary.
    void minWordBreak(String key)
    {
        minWordBreak = Integer.MAX_VALUE;

        minWordBreakUtil(root, key, 0, Integer.MAX_VALUE, 0);
    }

    void minWordBreakUtil(TrieNode node, String key,
                int start, int min_Break, int level)
    {
        TrieNode pCrawl = node;

        // base case, update minimum Break
        if (start == key.length()) {
            min_Break = Math.min(min_Break, level - 1);
            if(min_Break<minWordBreak){
                minWordBreak = min_Break;
            }
            return;
        }

        // traverse given key(pattern)
        for (int i = start; i < key.length(); i++) {
            int index = key.charAt(i) - 'a';
            if (pCrawl.children[index]==null)
                return;

            // if we find a condition were we can
            // move to the next word in a trie
            // dictionary
            if (pCrawl.children[index].endOfTree) {
                minWordBreakUtil(root, key, i + 1,
                        min_Break, level + 1);

            }
            pCrawl = pCrawl.children[index];
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String keys[] = {"cat", "mat", "ca", "ma",
                    "at", "c", "dog", "og", "do" };

        Trie trie = new Trie();

        // Construct trie

        int i;
        for (i = 0; i < keys.length ; i++)
            trie.insert(keys[i]);

        trie.minWordBreak("catmatat");

        System.out.println(trie.minWordBreak);
    }
}

// This code is contributed by Pavan Koli.
```

## C#

```
// C# program to find minimum breaks needed
// to break a string in dictionary words.
using System;

class Trie
{

    TrieNode root = new TrieNode();
    int minWordBreak = int.MaxValue ;

    // Trie node
    public class TrieNode
    {
        public bool endOfTree;
        public TrieNode []children = new TrieNode[26];
        public TrieNode()
        {
            endOfTree = false;
            for(int i = 0; i < 26; i++)
            {
                children[i] = null;
            }
        }
    }

    // If not present, inserts a key
    // into the trie If the key is the
    // prefix of trie node, just marks leaf node
    void insert(String key)
    {
        int length = key.Length;

        int index;

        TrieNode pcrawl = root;

        for(int i = 0; i < length; i++)
        {
            index = key[i]- 'a';

            if(pcrawl.children[index] == null)
                pcrawl.children[index] = new TrieNode();

            pcrawl = pcrawl.children[index];
        }

        // mark last node as leaf
        pcrawl.endOfTree = true;

    }

    // function break the string into minimum cut
    // such the every substring after breaking
    // in the dictionary.
    void minWordBreaks(String key)
    {
        minWordBreak = int.MaxValue;
        minWordBreakUtil(root, key, 0, int.MaxValue, 0);
    }

    void minWordBreakUtil(TrieNode node, String key,
                int start, int min_Break, int level)
    {
        TrieNode pCrawl = node;

        // base case, update minimum Break
        if (start == key.Length)
        {
            min_Break = Math.Min(min_Break, level - 1);
            if(min_Break < minWordBreak)
            {
                minWordBreak = min_Break;
            }
            return;
        }

        // traverse given key(pattern)
        for (int i = start; i < key.Length; i++)
        {
            int index = key[i] - 'a';
            if (pCrawl.children[index]==null)
                return;

            // if we find a condition were we can
            // move to the next word in a trie
            // dictionary
            if (pCrawl.children[index].endOfTree)
            {
                minWordBreakUtil(root, key, i + 1,
                        min_Break, level + 1);
            }
            pCrawl = pCrawl.children[index];
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String []keys = {"cat", "mat", "ca", "ma",
                    "at", "c", "dog", "og", "do" };

        Trie trie = new Trie();

        // Construct trie
        int i;
        for (i = 0; i < keys.Length ; i++)
            trie.insert(keys[i]);

        trie.minWordBreaks("catmatat");
        Console.WriteLine(trie.minWordBreak);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find minimum breaks needed
// to break a string in dictionary words.

class TrieNode
{
    constructor()
    {
        this.endOfTree=false;
        this.children=new Array(26);
        for(let i=0;i<26;i++)
            this.children[i]=null;
    }
}

let root = new TrieNode();
let minWordBreak = Number.MAX_VALUE;

// If not present, inserts a key into the trie
    // If the key is the prefix of trie node, just
    // marks leaf node
function insert(key)
{
    let length = key.length;

        let index;

        let pcrawl = root;

        for(let i = 0; i < length; i++)
        {
            index = key[i].charAt(0)- 'a'.charAt(0);

            if(pcrawl.children[index] == null)
                pcrawl.children[index] = new TrieNode();

            pcrawl = pcrawl.children[index];
        }

        // mark last node as leaf
        pcrawl.endOfTree = true;
}

// function break the string into minimum cut
    // such the every substring after breaking
    // in the dictionary.
function _minWordBreak(key)
{
    minWordBreak = Number.MAX_VALUE;

    minWordBreakUtil(root, key, 0, Number.MAX_VALUE, 0);
}

function minWordBreakUtil(node,key,start,min_Break,level)
{
    let pCrawl = node;

        // base case, update minimum Break
        if (start == key.length) {
            min_Break = Math.min(min_Break, level - 1);
            if(min_Break<minWordBreak){
                minWordBreak = min_Break;
            }
            return;
        }

        // traverse given key(pattern)
        for (let i = start; i < key.length; i++) {
            let index = key[i].charAt(0) - 'a'.charAt(0);
            if (pCrawl.children[index]==null)
                return;

            // if we find a condition were we can
            // move to the next word in a trie
            // dictionary
            if (pCrawl.children[index].endOfTree) {
                minWordBreakUtil(root, key, i + 1,
                        min_Break, level + 1);

            }
            pCrawl = pCrawl.children[index];
        }
}

// Driver code
let keys=["cat", "mat", "ca", "ma",
                    "at", "c", "dog", "og", "do" ];

let i;
for (i = 0; i < keys.length ; i++)
    insert(keys[i]);

_minWordBreak("catmatat");

document.write(minWordBreak);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```