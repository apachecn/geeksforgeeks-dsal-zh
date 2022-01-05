# 查找以给定后缀结束的字符串

> 原文:[https://www . geesforgeks . org/find-strings-以给定后缀结尾/](https://www.geeksforgeeks.org/find-strings-that-end-with-a-given-suffix/)

给定一组字符串 **S** 和一个字符串 **P** ，任务是用后缀 **P** 打印该组中的所有字符串。

**示例:**

> **输入:**
> S = {“极客”、“极客暴发户”、“极客”、“新极客”、“friendsongeeks”、“toppergek”}
> P =“极客”
> **输出:**
> 极客
> friendsongeeks
> 极客暴发户
> 新极客
> 
> **输入:**
> S = {“wide world”“web world”“classic word”“world”“world class”}
> P =“world”
> T5】输出:
> wide world
> web world
> world

**方法:**想法是使用[模式搜索，使用所有后缀的三元组](https://www.geeksforgeeks.org/pattern-searching-using-trie-suffixes/)。

*   将琴弦以相反的顺序储存在[特里](https://www.geeksforgeeks.org/trie-insert-and-search/)中。
*   反转字符串 **P** 并使用标准的[特里搜索算法进行搜索。](https://www.geeksforgeeks.org/trie-insert-and-search/)
*   检查倒排的字符串 **P** 本身是否是 Trie 中的一个单词，可以通过查看最后一个匹配节点是否设置了 **isEndWord** 标志来检查。
*   否则如果反串 **P** 形成后缀，则递归打印最后一个匹配节点的子树下的所有节点。

下面是上述方法的实现:

## C++

```
// C++ code to print all
// strings from a given set
// with suffix P
#include <bits/stdc++.h>
using namespace std;

#define CHILD (26)

// Converts key current character
// into index use only 'a' through
// 'z' and lower case
#define CHAR_TO_INDEX(c) (int)(c - 'a')

// Trie node
struct TrieNode {
    struct TrieNode* children[CHILD];

    // isWordEnd is true if the node
    // represents end of a word
    bool isWordEnd;
};

// Function to reverse a string
string reverseStr(string str)
{
    int n = str.length();

    // Swap character starting from
    // two corners
    for (int i = 0; i < n / 2; i++)
        swap(str[i], str[n - i - 1]);
    return str;
}

// Returns new trie node
struct TrieNode* getNode(void)
{
    struct TrieNode* pNode = new TrieNode;
    pNode->isWordEnd = false;

    for (int i = 0; i < CHILD; i++)
        pNode->children[i] = NULL;

    return pNode;
}

// If not present, inserts key into
// trie. If the key is suffix of trie
// node, just mark leaf node
void insert(struct TrieNode* root,
            const string key)
{
    struct TrieNode* pCrawl = root;

    for (int level = 0;
         level < key.length();
         level++) {

        int index = CHAR_TO_INDEX(key[level]);

        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        pCrawl = pCrawl->children[index];
    }

    // Mark last node as leaf
    pCrawl->isWordEnd = true;
}

// Returns true if key presents in
// the trie, else false
bool search(struct TrieNode* root,
            const string key)
{
    int length = key.length();
    struct TrieNode* pCrawl = root;
    for (int level = 0;
         level < length; level++) {

        int index = CHAR_TO_INDEX(key[level]);

        if (!pCrawl->children[index])
            return false;

        pCrawl = pCrawl->children[index];
    }

    return (pCrawl != NULL
            && pCrawl->isWordEnd);
}

// Returns 0 if current node has
// a child
// If all children are NULL, return 1
bool isLastNode(struct TrieNode* root)
{
    for (int i = 0; i < CHILD; i++)
        if (root->children[i])
            return 0;
    return 1;
}

// Recursive function to print strings
// having given suffix
void printStrings(struct TrieNode* root,
                  string currsuffix)
{

    // If a string with currsuffix
    // is found
    if (root->isWordEnd) {
        cout << reverseStr(currsuffix);
        cout << endl;
        reverseStr(currsuffix);
    }

    // All children struct node
    // pointers are NULL
    if (isLastNode(root))
        return;

    for (int i = 0; i < CHILD; i++) {
        if (root->children[i]) {

            // Append current character
            // to currsuffix string
            currsuffix.push_back(97 + i);

            // recur over the rest
            printStrings(root->children[i],
                         currsuffix);
            // remove last character
            currsuffix.pop_back();
        }
    }
}

// print strings with given suffix
int printStringsWithGivenSuffix(
    TrieNode* root, const string query)
{
    struct TrieNode* pCrawl = root;

    // Check if suffix is present
    // and find the node (of last
    // level) with last character
    // of given string.
    int level;
    int n = query.length();
    for (level = 0; level < n;
         level++) {

        int index = CHAR_TO_INDEX(query[level]);

        // no string in the Trie has
        // this suffix
        if (!pCrawl->children[index])
            return 0;

        pCrawl = pCrawl->children[index];
    }

    // If suffix is present as a word.
    bool isWord = (pCrawl->isWordEnd
                   == true);

    // If suffix is last node of
    // tree (has no children)
    bool isLast = isLastNode(pCrawl);

    // If suffix is present as a word,
    // but there is no subtree below
    // the last matching node.
    if (isWord && isLast) {
        cout << query << endl;
        return -1;
    }

    // If there are are nodes below
    // last matching character.
    if (!isLast) {
        string suffix = query;
        printStrings(pCrawl, suffix);
        return 1;
    }
}

// Driver Code
int main()
{
    struct TrieNode* root = getNode();
    vector<string> S
        = { "geeks", "geeksforgeeks",
            "geek", "newgeeks",
            "friendsongeeks",
            "toppergeek" };

    for (string str : S) {
        insert(root,
               reverseStr(str));
    }

    string P = "eek";

    printStringsWithGivenSuffix(
        root, reverseStr(P));

    return 0;
}
```

## 计算机编程语言

```
# Python3 code for the above program
class TrieNode(): 
    def __init__(self): 

        # Initialize one node for trie 
        self.children = {} 
        self.last = False

def reverse(s): 
    str = "" 
    for i in s: 
        str = i + str
    return str

class Trie(): 
    def __init__(self): 

        # Initialize the trie structure
        self.root = TrieNode() 
        self.word_list = [] 

    def formTrie(self, keys): 

        # Forms a trie structure
        # with the given set of 
        # strings if it does not
        # exists already else it 
        # merges the key into it
        # by extending the 
        # structure as required 
        for key in keys:

            # inserting one key
            # to the trie.
            self.insert(key)  

    def insert(self, key): 

        # Inserts a key into 
        # trie if it does not 
        # exist already. And if 
        # the key is a suffix
        # of the trie node, just 
        # marks it as leaf node. 
        node = self.root 

        for a in list(key): 
            if not node.children.get(a): 
                node.children[a] = TrieNode() 

            node = node.children[a] 

        node.last = True

    def search(self, key): 

        # Searches the given key
        # in trie for a full match 
        # and returns True on
        # success else returns False 
        node = self.root 
        found = True

        for a in list(key): 
            if not node.children.get(a): 
                found = False
                break

            node = node.children[a] 

        return node and node.last and found 

    def printStrings(self, node, word): 

        # Method to recursively
        # traverse the trie 
        # and return a whole word
        if node.last: 
            self.word_list.append(word) 

        for a, n in node.children.items(): 
            self.printStrings(n, word + a) 

    def printStringsWithGivenSuffix(self, key): 

        # Returns all the words in 
        # the trie whose common 
        # suffix is the given key
        # thus listing out all 
        # the strings
        node = self.root 
        not_found = False
        temp_word = '' 

        for a in list(key): 
            if not node.children.get(a): 
                not_found = True
                break

            temp_word += a 
            node = node.children[a] 

        if not_found: 
            return 0
        elif node.last and not node.children: 
            return -1

        self.printStrings(node, temp_word) 

        for s in self.word_list: 
            print(reverse(s)) 
        return 1

# Driver Code 

# keys to form the trie structure
keys = [reverse("geeks"), 
reverse("geeksforgeeks"), 
reverse("geek"), 
reverse("newgeeks"), 
reverse("friendsongeeks"), 
reverse("toppergeek")] 

# key 
key = "eek" 
status = ["Not found", "Found"] 

# creating trie object 
t = Trie() 

# creating the trie structure 
# with the given set of strings
t.formTrie(keys) 

# print string having suffix 'P'
# our trie structure
comp = t.printStringsWithGivenSuffix(reverse(key))   
```

**Output:**

```
geek
toppergeek

```

s