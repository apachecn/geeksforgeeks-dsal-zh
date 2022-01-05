# 在 CamelCase 符号字典

中打印所有匹配模式的单词

> 原文:[https://www . geeksforgeeks . org/print-words-matching-pattern-camel case-notification-dictionary/](https://www.geeksforgeeks.org/print-words-matching-pattern-camelcase-notation-dictonary/)

给定一个单词字典，其中每个单词都遵循 CamelCase 符号，打印字典中与给定的仅由大写字符组成的模式匹配的所有单词。
*CamelCase 是写复合词或短语的做法，这样每个单词或缩写都以大写字母开头。常见的例子包括:“PowerPoint”和“WikiPedia”、“GeeksForGeeks”、“CodeBlocks”等。*
**例:**

```
Input: 
dict[] = ["Hi", "Hello", "HelloWorld",  "HiTech", "HiGeek", 
"HiTechWorld", "HiTechCity", "HiTechLab"]

For pattern "HT",
Output: ["HiTech", "HiTechWorld", "HiTechCity", "HiTechLab"]

For pattern "H",
Output: ["Hi", "Hello", "HelloWorld",  "HiTech", "HiGeek", 
    "HiTechWorld", "HiTechCity", "HiTechLab"]

For pattern "HTC",
Output: ["HiTechCity"]

Input: 
dict[] = ["WelcomeGeek","WelcomeToGeeksForGeeks", "GeeksForGeeks"]

For pattern "WTG",
Output: ["WelcomeToGeeksForGeeks"]

For pattern "GFG",
Output: [GeeksForGeeks]

For pattern "GG",
Output: No match found
```

这个想法是将所有的字典键一个接一个地插入到 Trie 中。此处的关键字仅指 CamelCase 符号中原始单词的大写字符。如果我们第一次遇到密钥，我们需要将最后一个节点标记为叶节点，并将该密钥的完整单词插入到与叶节点相关联的向量中。如果我们遇到一个已经在 trie 中的关键字，我们用当前单词更新与叶节点相关的向量。处理完所有词典单词后，我们在 trie 中搜索模式，并打印所有与该模式匹配的单词。
以下是上述思路的实现–

## C++

```
// C++ program to print all words in the CamelCase
// dictionary that matches with a given pattern
#include <bits/stdc++.h>
using namespace std;

// Alphabet size (# of upper-Case characters)
#define ALPHABET_SIZE 26

// A Trie node
struct TrieNode
{
    TrieNode* children[ALPHABET_SIZE];

    // isLeaf is true if the node represents
    // end of a word
    bool isLeaf;

    // vector to store list of complete words
    // in leaf node
    list<string> word;
};

// Returns new Trie node (initialized to NULLs)
TrieNode* getNewTrieNode(void)
{
    TrieNode* pNode = new TrieNode;

    if (pNode)
    {
        pNode->isLeaf = false;

        for (int i = 0; i < ALPHABET_SIZE; i++)
            pNode->children[i] = NULL;
    }

    return pNode;
}

// Function to insert word into the Trie
void insert(TrieNode* root, string word)
{
    int index;
    TrieNode* pCrawl = root;

    for (int level = 0; level < word.length(); level++)
    {
        // consider only uppercase characters
        if (islower(word[level]))
            continue;

        // get current character position
        index = int(word[level]) - 'A';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNewTrieNode();

        pCrawl = pCrawl->children[index];
    }

    // mark last node as leaf
    pCrawl->isLeaf = true;

    // push word into vector associated with leaf node
    (pCrawl->word).push_back(word);
}

// Function to print all children of Trie node root
void printAllWords(TrieNode* root)
{
    // if current node is leaf
    if (root->isLeaf)
    {
        for(string str : root->word)
            cout << str << endl;
    }

    // recurse for all children of root node
    for (int i = 0; i < ALPHABET_SIZE; i++)
    {
        TrieNode* child = root->children[i];
        if (child)
            printAllWords(child);
    }
}

// search for pattern in Trie and print all words
// matching that pattern
bool search(TrieNode* root, string pattern)
{
    int index;
    TrieNode* pCrawl = root;

    for (int level = 0; level < pattern.length(); level++)
    {
        index = int(pattern[level]) - 'A';
        // Invalid pattern
        if (!pCrawl->children[index])
            return false;

        pCrawl = pCrawl->children[index];
    }

    // print all words matching that pattern
    printAllWords(pCrawl);

    return true;
}

// Main function to print all words in the CamelCase
// dictionary that matches with a given pattern
void findAllWords(vector<string> dict, string pattern)
{
    // construct Trie root node
    TrieNode* root = getNewTrieNode();

    // Construct Trie from given dict
    for (string word : dict)
        insert(root, word);

    // search for pattern in Trie
    if (!search(root, pattern))
        cout << "No match found";
}

// Driver function
int main()
{
    // dictionary of words where each word follows
    // CamelCase notation
    vector<string> dict = {
        "Hi", "Hello", "HelloWorld", "HiTech", "HiGeek",
        "HiTechWorld", "HiTechCity", "HiTechLab"
    };

    // pattern consisting of uppercase characters only
    string pattern = "HT";

    findAllWords(dict, pattern);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all words in the CamelCase
// dictionary that matches with a given pattern
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
public class CamelCase {

    // Alphabet size (# of upper-Case characters)
    static final int ALPHABET_SIZE = 26;

    // A Trie node
    static class TrieNode {
        TrieNode[] children = new TrieNode[ALPHABET_SIZE];

        // isLeaf is true if the node represents
        // end of a word
        boolean isLeaf;

        // vector to store list of complete words
        // in leaf node
        List<String> word;

        public TrieNode() {
            isLeaf = false;
            for (int i = 0; i < ALPHABET_SIZE; i++)
                children[i] = null;

            word = new ArrayList<String>();
        }
    }

    static TrieNode root;

    // Function to insert word into the Trie
    static void insert(String word) {
        int index;
        TrieNode pCrawl = root;

        for (int level = 0; level < word.length(); level++) {

              // consider only uppercase characters
            if (Character.isLowerCase(word.charAt(level)))
                continue;

            // get current character position
            index = word.charAt(level) - 'A';
            if (pCrawl.children[index] == null)
                pCrawl.children[index] = new TrieNode();

            pCrawl = pCrawl.children[index];
        }

        // mark last node as leaf
        pCrawl.isLeaf = true;

        // push word into vector associated with leaf node
        (pCrawl.word).add(word);
    }

    // Function to print all children of Trie node root
    static void printAllWords(TrieNode root) {

        // if current node is leaf
        if (root.isLeaf) {
            for (String str : root.word)
                System.out.println(str);
        }

        // recurse for all children of root node
        for (int i = 0; i < ALPHABET_SIZE; i++) {
            TrieNode child = root.children[i];
            if (child != null)
                printAllWords(child);
        }
    }

    // search for pattern in Trie and print all words
    // matching that pattern
    static boolean search(String pattern) {
        int index;
        TrieNode pCrawl = root;

        for (int level = 0; level < pattern.length(); level++) {
            index = pattern.charAt(level) - 'A';

            // Invalid pattern
            if (pCrawl.children[index] == null)
                return false;

            pCrawl = pCrawl.children[index];
        }

        // print all words matching that pattern
        printAllWords(pCrawl);

        return true;
    }

    // Main function to print all words in the CamelCase
    // dictionary that matches with a given pattern
    static void findAllWords(List<String> dict, String pattern)
     {

        // construct Trie root node
        root = new TrieNode();

        // Construct Trie from given dict
        for (String word : dict)
            insert(word);

        // search for pattern in Trie
        if (!search(pattern))
            System.out.println("No match found");
    }

    // Driver function
    public static void main(String args[]) {

        // dictionary of words where each word follows
        // CamelCase notation
        List<String> dict = Arrays.asList("Hi", "Hello",
                           "HelloWorld", "HiTech", "HiGeek",
                          "HiTechWorld", "HiTechCity",
                            "HiTechLab");

        // pattern consisting of uppercase characters only
        String pattern = "HT";

        findAllWords(dict, pattern);
    }
}
// This code is contributed by Sumit Ghosh
```

## C#

```
// C# program to print all words in
// the CamelCase dictionary that
// matches with a given pattern
using System;
using System.Collections.Generic;

class GFG
{

    // Alphabet size (# of upper-Case characters)
    static int ALPHABET_SIZE = 26;

    // A Trie node
    public class TrieNode
    {
        public TrieNode[] children = new
               TrieNode[ALPHABET_SIZE];

        // isLeaf is true if the node represents
        // end of a word
        public bool isLeaf;

        // vector to store list of complete words
        // in leaf node
        public List<String> word;

        public TrieNode()
        {
            isLeaf = false;
            for (int i = 0; i < ALPHABET_SIZE; i++)
                children[i] = null;

            word = new List<String>();
        }
    }

    static TrieNode root;

    // Function to insert word into the Trie
    static void insert(String word)
    {
        int index;
        TrieNode pCrawl = root;

        for (int level = 0;
                 level < word.Length; level++)
        {

            // consider only uppercase characters
            if (char.IsLower(word[level]))
                continue;

            // get current character position
            index = word[level] - 'A';
            if (pCrawl.children[index] == null)
                pCrawl.children[index] = new TrieNode();

            pCrawl = pCrawl.children[index];
        }

        // mark last node as leaf
        pCrawl.isLeaf = true;

        // push word into vector
        // associated with leaf node
        (pCrawl.word).Add(word);
    }

    // Function to print all children
    // of Trie node root
    static void printAllWords(TrieNode root)
    {

        // if current node is leaf
        if (root.isLeaf)
        {
            foreach (String str in root.word)
                Console.WriteLine(str);
        }

        // recurse for all children of root node
        for (int i = 0; i < ALPHABET_SIZE; i++)
        {
            TrieNode child = root.children[i];
            if (child != null)
                printAllWords(child);
        }
    }

    // search for pattern in Trie and
    // print all words matching that pattern
    static bool search(String pattern)
    {
        int index;
        TrieNode pCrawl = root;

        for (int level = 0;
                 level < pattern.Length;
                 level++)
        {
            index = pattern[level] - 'A';

            // Invalid pattern
            if (pCrawl.children[index] == null)
                return false;

            pCrawl = pCrawl.children[index];
        }

        // print all words matching that pattern
        printAllWords(pCrawl);

        return true;
    }

    // Main function to print all words
    // in the CamelCase dictionary that
    // matches with a given pattern
    static void findAllWords(List<String> dict,
                                  String pattern)
    {

        // construct Trie root node
        root = new TrieNode();

        // Construct Trie from given dict
        foreach (String word in dict)
            insert(word);

        // search for pattern in Trie
        if (!search(pattern))
            Console.WriteLine("No match found");
    }

    // Driver Code
    public static void Main(String []args)
    {

        // dictionary of words where each word follows
        // CamelCase notation
        List<String> dict = new List<String>{"Hi", "Hello",
                                             "HelloWorld", "HiTech",
                                             "HiGeek", "HiTechWorld",
                                             "HiTechCity", "HiTechLab"};

        // pattern consisting of
        // uppercase characters only
        String pattern = "HT";

        findAllWords(dict, pattern);
    }
}

// This code is contributed by Princi Singh
```

**输出:**

```
HiTech
HiTechCity
HiTechLab
HiTechWorld
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。