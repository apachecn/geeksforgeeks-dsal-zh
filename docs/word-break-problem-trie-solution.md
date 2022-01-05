# 断字问题| (Trie 解决方案)

> 原文:[https://www . geesforgeks . org/word-break-problem-trie-solution/](https://www.geeksforgeeks.org/word-break-problem-trie-solution/)

给定一个输入字符串和一个单词字典，找出输入字符串是否可以被分割成一个用空格分隔的字典单词序列。有关更多详细信息，请参见以下示例。
这是一个著名的谷歌面试问题，现在一天之内也被很多其他公司问到。

```
Consider the following dictionary 
{ i, like, sam, sung, samsung, mobile, ice, 
  cream, icecream, man, go, mango}

Input:  ilike
Output: Yes 
The string can be segmented as "i like".

Input:  ilikesamsung
Output: Yes
The string can be segmented as "i like samsung" or 
"i like sam sung".

```

这里讨论的解决方案主要是下面基于 DP 的解决方案的扩展。
[动态编程|第 32 集(断字问题)](https://www.geeksforgeeks.org/dynamic-programming-set-32-word-break-problem/)

在上面的文章中，一个简单的数组被用来在字典中存储和搜索单词。这里我们使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 快速完成这些任务。

## C++

```
// A DP and Trie based program to test whether
// a given string can be segmented into
// space separated words in dictionary
#include <iostream>
using namespace std;

const int ALPHABET_SIZE = 26;

// trie node
struct TrieNode
{
    struct TrieNode *children[ALPHABET_SIZE];

    // isEndOfWord is true if the node represents
    // end of a word
    bool isEndOfWord;
};

// Returns new trie node (initialized to NULLs)
struct TrieNode *getNode(void)
{
    struct TrieNode *pNode =  new TrieNode;

    pNode->isEndOfWord = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode->children[i] = NULL;

    return pNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node, just
// marks leaf node
void insert(struct TrieNode *root, string key)
{
    struct TrieNode *pCrawl = root;

    for (int i = 0; i < key.length(); i++)
    {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        pCrawl = pCrawl->children[index];
    }

    // mark last node as leaf
    pCrawl->isEndOfWord = true;
}

// Returns true if key presents in trie, else
// false
bool search(struct TrieNode *root, string key)
{
    struct TrieNode *pCrawl = root;

    for (int i = 0; i < key.length(); i++)
    {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            return false;

        pCrawl = pCrawl->children[index];
    }

    return (pCrawl != NULL && pCrawl->isEndOfWord);
}

// returns true if string can be segmented into
// space separated words, otherwise returns false
bool wordBreak(string str, TrieNode *root)
{
    int size = str.size();

    // Base case
    if (size == 0)  return true;

    // Try all prefixes of lengths from 1 to size
    for (int i=1; i<=size; i++)
    {
        // The parameter for search is str.substr(0, i)
        // str.substr(0, i) which is prefix (of input
        // string) of length 'i'. We first check whether
        // current prefix is in dictionary. Then we
        // recursively check for remaining string
        // str.substr(i, size-i) which is suffix of
        // length size-i
        if (search(root, str.substr(0, i)) &&
            wordBreak(str.substr(i, size-i), root))
            return true;
    }

    // If we have tried all prefixes and none
    // of them worked
    return false;
}

// Driver program to test above functions
int main()
{
    string dictionary[] = {"mobile","samsung","sam",
                           "sung","ma\n","mango",
                           "icecream","and","go","i",
                           "like","ice","cream"};
    int n = sizeof(dictionary)/sizeof(dictionary[0]);
    struct TrieNode *root = getNode();

    // Construct trie
    for (int i = 0; i < n; i++)
        insert(root, dictionary[i]);

    wordBreak("ilikesamsung", root)? cout <<"Yes\n": cout << "No\n";
    wordBreak("iiiiiiii", root)? cout <<"Yes\n": cout << "No\n";
    wordBreak("", root)? cout <<"Yes\n": cout << "No\n";
    wordBreak("ilikelikeimangoiii", root)? cout <<"Yes\n": cout << "No\n";
    wordBreak("samsungandmango", root)? cout <<"Yes\n": cout << "No\n";
    wordBreak("samsungandmangok", root)? cout <<"Yes\n": cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A DP and Trie based program to test whether
// a given string can be segmented into
// space separated words in dictionary
import java.util.*;
import java.io.*;

class GFG{

static final int ALPHABET_SIZE = 26;

// trie node
static class TrieNode
{
    TrieNode children[];

    // isEndOfWord is true if the node
    // represents end of a word
    boolean isEndOfWord;

    // Constructor of TrieNode
    TrieNode()
    {
        children = new TrieNode[ALPHABET_SIZE];
        for(int i = 0; i < ALPHABET_SIZE; i++)
            children[i] = null;

        isEndOfWord = false;
    }
}

// If not present, inserts key into trie
// If the key is prefix of trie node, just
// marks leaf node
static void insert(TrieNode root, String key)
{
    TrieNode pCrawl = root;

    for(int i = 0; i < key.length(); i++) 
    {
        int index = key.charAt(i) - 'a';
        if (pCrawl.children[index] == null)
            pCrawl.children[index] = new TrieNode();

        pCrawl = pCrawl.children[index];
    }

    // Mark last node as leaf
    pCrawl.isEndOfWord = true;
}

// Returns true if key presents in trie, else
// false
static boolean search(TrieNode root, String key)
{
    TrieNode pCrawl = root;

    for(int i = 0; i < key.length(); i++)
    {
        int index = key.charAt(i) - 'a';
        if (pCrawl.children[index] == null)
            return false;

        pCrawl = pCrawl.children[index];
    }
    return (pCrawl != null && pCrawl.isEndOfWord);
}

// Returns true if string can be segmented
// into space separated words, otherwise 
// returns false
static boolean wordBreak(String str, TrieNode root)
{
    int size = str.length();

    // Base case
    if (size == 0)
        return true;

    // Try all prefixes of lengths from 1 to size
    for(int i = 1; i <= size; i++) 
    {

        // The parameter for search is 
        // str.substring(0, i) 
        // str.substrinf(0, i) which is
        // prefix (of input string) of 
        // length 'i'. We first check whether
        // current prefix is in dictionary. 
        // Then we recursively check for remaining
        // string str.substr(i, size) which 
        // is suffix of length size-i.
        if (search(root, str.substring(0, i)) && 
            wordBreak(str.substring(i, size), root))
            return true;
    }

    // If we have tried all prefixes and none
    // of them worked
    return false;
}

// Driver code
public static void main(String []args)
{
    String dictionary[] = { "mobile", "samsung",
                            "sam", "sung", "ma",
                            "mango", "icecream", 
                            "and", "go", "i", "like",
                            "ice", "cream" };

    int n = dictionary.length;
    TrieNode root = new TrieNode();

    // Construct trie
    for(int i = 0; i < n; i++)
        insert(root, dictionary[i]);

    System.out.print(wordBreak("ilikesamsung", root) ?
                               "Yes\n" : "No\n");
    System.out.print(wordBreak("iiiiiiii", root) ? 
                               "Yes\n" : "No\n");
    System.out.print(wordBreak("", root) ?
                               "Yes\n" : "No\n");
    System.out.print(wordBreak("ilikelikeimangoiii", root) ?
                               "Yes\n" : "No\n");
    System.out.print(wordBreak("samsungandmango", root) ?
                               "Yes\n" : "No\n");
    System.out.print(wordBreak("samsungandmangok", root) ?
                               "Yes\n" : "No\n");
}
}

// This code is contributed by Ganeshchowdharysadanala
```

## 蟒蛇 3

```
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        Author : @amitrajitbose
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        """CREATING THE TRIE CLASS"""

        class TrieNode(object):

            def __init__(self):
                self.children = [] #will be of size = 26
                self.isLeaf = False

            def getNode(self):
                p = TrieNode() #new trie node
                p.children = []
                for i in range(26):
                    p.children.append(None)
                p.isLeaf = False
                return p

            def insert(self, root, key):
                key = str(key)
                pCrawl = root
                for i in key:
                    index = ord(i)-97
                    if(pCrawl.children[index] == None):
                        # node has to be initialised
                        pCrawl.children[index] = self.getNode()
                    pCrawl = pCrawl.children[index]
                pCrawl.isLeaf = True #marking end of word

            def search(self, root, key):
                #print("Searching %s" %key) #DEBUG
                pCrawl = root
                for i in key:
                    index = ord(i)-97
                    if(pCrawl.children[index] == None):
                        return False
                    pCrawl = pCrawl.children[index]
                if(pCrawl and pCrawl.isLeaf):
                    return True

        def checkWordBreak(strr, root):
            n = len(strr)
            if(n == 0):
                return True
            for i in range(1,n+1):
                if(root.search(root, strr[:i]) and checkWordBreak(strr[i:], root)):
                    return True
            return False

        """IMPLEMENT SOLUTION"""
        root = TrieNode().getNode()
        for w in wordDict:
            root.insert(root, w)
        out = checkWordBreak(s, root)
        if(out):
            return "Yes"
        else:
            return "No"

print(Solution().wordBreak("thequickbrownfox", ["the", "quick", "fox", "brown"]))
print(Solution().wordBreak("bedbathandbeyond", ["bed", "bath", "bedbath", "and", "beyond"]))
print(Solution().wordBreak("bedbathandbeyond", ["teddy", "bath", "bedbath", "and", "beyond"]))
print(Solution().wordBreak("bedbathandbeyond", ["bed", "bath", "bedbath", "and", "away"]))
```

**输出:**

```
Yes
Yes
Yes
Yes
Yes
No

```

本文由**普拉纳夫**供稿。Python 代码由 **Jeet9** 提供。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。