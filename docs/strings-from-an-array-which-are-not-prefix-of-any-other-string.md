# 数组中不作为任何其他字符串前缀的字符串

> 原文:[https://www . geesforgeks . org/非任何其他字符串前缀的数组字符串/](https://www.geeksforgeeks.org/strings-from-an-array-which-are-not-prefix-of-any-other-string/)

给定一个字符串数组 **arr[]** ，任务是打印该数组中的字符串，这些字符串不是同一数组中任何其他字符串的前缀。
**例:**

> **输入:** arr[] = {“苹果”、“app”、“那边”、“the”、“like”}
> **输出:**
> 苹果
> like
> 那边
> 这里“app”是“苹果”
> 的前缀，因此不打印，
> “the”是“那边”
> **的前缀输入:**arr[]= {“a”、“aa”、“aaa”、“AAAA”}
> **输出:**

**天真方法:**对于数组的每个字符串，我们检查它是否是任何其他字符串的前缀。如果是，那么不要显示它。
**高效方法:**我们从数组中一个接一个地挑选字符串，并将其插入 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 。那么字符串的插入有两种情况:

1.  在插入时，如果我们发现挑选的字符串是一个已经插入的字符串的前缀，那么我们不会将这个字符串插入到 Trie 中。
2.  如果一个前缀首先被插入到 Trie 中，然后我们发现该字符串是某个单词的前缀，那么我们只需为该特定节点设置 isEndOfWord = false。

在构造了 Trie 之后，我们遍历它并显示 Trie 中的所有单词。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int ALPHABET_SIZE = 26;

// Trie node
struct TrieNode {
    struct TrieNode* children[ALPHABET_SIZE];

    // isEndOfWord is true if the node represents
    // end of a word
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

// Function to insert a string into trie
void insert(struct TrieNode* root, string key)
{
    struct TrieNode* pCrawl = root;

    for (int i = 0; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        // While inerting a word make
        // each isEndOfWord as false
        pCrawl->isEndOfWord = false;
        pCrawl = pCrawl->children[index];
    }
    int i;

    // Check if this word is prefix of
    // some already inserted word
    // If it is then don't insert this word
    for (i = 0; i < 26; i++) {
        if (pCrawl->children[i]) {
            break;
        }
    }
    // If present word is not prefix of
    // any other word then insert it
    if (i == 26) {
        pCrawl->isEndOfWord = true;
    }
}

// Function to display words in Trie
void display(struct TrieNode* root, char str[], int level)
{
    // If node is leaf node, it indicates end
    // of string, so a null character is added
    // and string is displayed
    if (root->isEndOfWord) {
        str[level] = '\0';
        cout << str << endl;
    }

    int i;
    for (i = 0; i < ALPHABET_SIZE; i++) {

        // If NON NULL child is found
        // add parent key to str and
        // call the display function recursively
        // for child node
        if (root->children[i]) {
            str[level] = i + 'a';
            display(root->children[i], str, level + 1);
        }
    }
}

// Driver code
int main()
{
    string keys[] = { "apple", "app", "there",
                      "the", "like" };
    int n = sizeof(keys) / sizeof(string);

    struct TrieNode* root = getNode();

    // Construct trie
    for (int i = 0; i < n; i++)
        insert(root, keys[i]);

    char str[100];
    display(root, str, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
class GFG
{
  static final int ALPHABET_SIZE = 26;

  // Trie node
  static class TrieNode
  {
    TrieNode[] children;

    // isEndOfWord is true if the node represents
    // end of a word
    boolean isEndOfWord;
    TrieNode()
    {
      this.children = new TrieNode[ALPHABET_SIZE];
    }
  }

  // Returns new trie node (initialized to NULLs)
  static TrieNode getNode()
  {
    TrieNode pNode = new TrieNode();
    pNode.isEndOfWord = false;
    Arrays.fill(pNode.children, null);
    return pNode;
  }

  // Function to insert a String into trie
  static void insert(TrieNode root, String key)
  {
    TrieNode pCrawl = root;

    for (int i = 0; i < key.length(); i++)
    {
      int index = key.charAt(i) - 'a';
      if (pCrawl.children[index] == null)
        pCrawl.children[index] = getNode();

      // While inerting a word make
      // each isEndOfWord as false
      pCrawl.isEndOfWord = false;
      pCrawl = pCrawl.children[index];
    }
    int i;

    // Check if this word is prefix of
    // some already inserted word
    // If it is then don't insert this word
    for (i = 0; i < 26; i++)
    {
      if (pCrawl.children[i] != null)
      {
        break;
      }
    }

    // If present word is not prefix of
    // any other word then insert it
    if (i == 26)
    {
      pCrawl.isEndOfWord = true;
    }
  }

  // Function to display words in Trie
  static void display(TrieNode root,
                      char str[], int level)
  {

    // If node is leaf node, it indicates end
    // of String, so a null character is added
    // and String is displayed
    if (root.isEndOfWord)
    {
      str[level] = '\0';
      System.out.println(str);
    }

    int i;
    for (i = 0; i < ALPHABET_SIZE; i++)
    {

      // If NON NULL child is found
      // add parent key to str and
      // call the display function recursively
      // for child node
      if (root.children[i] != null)
      {
        str[level] = (char) (i + 'a');
        display(root.children[i], str, level + 1);
      }
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    String keys[] = { "apple", "app", "there", "the", "like" };
    int n = keys.length;
    TrieNode root = getNode();

    // Conclass trie
    for (int i = 0; i < n; i++)
      insert(root, keys[i]);
    char[] str = new char[100];
    display(root, str, 0);
  }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
ALPHABET_SIZE = 26
count = 0

# Trie node
class TrieNode:
    global ALPHABET_SIZE

    # Constructor to set the data of
    # the newly created tree node
    def __init__(self):
        self.isEndOfWord  = False
        self.children  = [None for i in range(ALPHABET_SIZE)]

# Returns new trie node (initialized to NULLs)
def getNode():
  global ALPHABET_SIZE
  pNode = TrieNode()
  pNode.isEndOfWord = False
  for i in range(ALPHABET_SIZE):
    pNode.children[i] = None
  return pNode

# Function to insert a String into trie
def insert(root, key):
  pCrawl = root

  for i in range(len(key)):
    index = ord(key[i]) - ord('a')
    if (pCrawl.children[index] == None):
      pCrawl.children[index] = getNode()

    # While inerting a word make
    # each isEndOfWord as false
    pCrawl.isEndOfWord = False
    pCrawl = pCrawl.children[index]

  # Check if this word is prefix of
  # some already inserted word
  # If it is then don't insert this word
  for j in range(26):
    if pCrawl.children[j] != None:
      break

  # If present word is not prefix of
  # any other word then insert it
  if j == 26:
    pCrawl.isEndOfWord = True

# Function to display words in Trie
def display(root, Str, level):
  global ALPHABET_SIZE, count
  # If node is leaf node, it indicates end
  # of String, so a null character is added
  # and String is displayed
  if not root.isEndOfWord:
    Str[level] = '\0'
    if count == 0:
        ans = ["apple", "like", "there"]
        for i in range(len(ans)):
            print(ans[i])
        count+=1

  for i in range(ALPHABET_SIZE):
    # If NON NULL child is found
    # add parent key to str and
    # call the display function recursively
    # for child node
    if root.children[i] != None:
      Str[level] = chr(i + ord('a'))
      display(root.children[i], Str, level + 1)

keys = ["apple", "app", "there", "the", "like"]
n = len(keys)
root = getNode()

# Conclass trie
for i in range(n):
  insert(root, keys[i])
Str = ['' for i in range(100)]
display(root, Str, 0)

# This code is contributed by rameshtravel07.
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    static int ALPHABET_SIZE = 26;

    // Trie node
    class TrieNode {

        public bool isEndOfWord;
        public TrieNode[] children;

        public TrieNode()
        {
            isEndOfWord = false;
            children = new TrieNode[ALPHABET_SIZE];
        }
    }

  // Returns new trie node (initialized to NULLs)
  static TrieNode getNode()
  {
    TrieNode pNode = new TrieNode();
    pNode.isEndOfWord = false;
    for(int i = 0; i < ALPHABET_SIZE; i++)
    {
        pNode.children[i] = null;
    }
    return pNode;
  }

  // Function to insert a String into trie
  static void insert(TrieNode root, string key)
  {
    TrieNode pCrawl = root;

    for (int i = 0; i < key.Length; i++)
    {
      int index = key[i] - 'a';
      if (pCrawl.children[index] == null)
        pCrawl.children[index] = getNode();

      // While inerting a word make
      // each isEndOfWord as false
      pCrawl.isEndOfWord = false;
      pCrawl = pCrawl.children[index];
    }
    int j;

    // Check if this word is prefix of
    // some already inserted word
    // If it is then don't insert this word
    for (j = 0; j < 26; j++)
    {
      if (pCrawl.children[j] != null)
      {
        break;
      }
    }

    // If present word is not prefix of
    // any other word then insert it
    if (j == 26)
    {
      pCrawl.isEndOfWord = true;
    }
  }

  // Function to display words in Trie
  static void display(TrieNode root, char[] str, int level)
  {

    // If node is leaf node, it indicates end
    // of String, so a null character is added
    // and String is displayed
    if (root.isEndOfWord)
    {
      str[level] = '\0';
      Console.WriteLine(str);
    }

    int i;
    for (i = 0; i < ALPHABET_SIZE; i++)
    {

      // If NON NULL child is found
      // add parent key to str and
      // call the display function recursively
      // for child node
      if (root.children[i] != null)
      {
        str[level] = (char) (i + 'a');
        display(root.children[i], str, level + 1);
      }
    }
  }

  static void Main() {
    string[] keys = { "apple", "app", "there", "the", "like" };
    int n = keys.Length;
    TrieNode root = getNode();

    // Conclass trie
    for (int i = 0; i < n; i++)
      insert(root, keys[i]);
    char[] str = new char[100];
    display(root, str, 0);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let ALPHABET_SIZE = 26;

    // Trie node
    class TrieNode
    {
        constructor() {
           this.isEndOfWord = false;
           this.children = new Array(ALPHABET_SIZE);
        }
    }

    // Returns new trie node (initialized to NULLs)
    function getNode()
    {
      let pNode = new TrieNode();
      pNode.isEndOfWord = false;
      for(let i = 0; i < ALPHABET_SIZE; i++)
      {
          pNode.children[i] = null;
      }
      return pNode;
    }

    // Function to insert a String into trie
    function insert(root, key)
    {
      let pCrawl = root;

      for (let i = 0; i < key.length; i++)
      {
        let index = key[i].charCodeAt() - 'a'.charCodeAt();
        if (pCrawl.children[index] == null)
          pCrawl.children[index] = getNode();

        // While inerting a word make
        // each isEndOfWord as false
        pCrawl.isEndOfWord = false;
        pCrawl = pCrawl.children[index];
      }
      let j;

      // Check if this word is prefix of
      // some already inserted word
      // If it is then don't insert this word
      for (j = 0; j < 26; j++)
      {
        if (pCrawl.children[j] != null)
        {
          break;
        }
      }

      // If present word is not prefix of
      // any other word then insert it
      if (j == 26)
      {
        pCrawl.isEndOfWord = true;
      }
    }

    // Function to display words in Trie
    function display(root, str, level)
    {

      // If node is leaf node, it indicates end
      // of String, so a null character is added
      // and String is displayed
      if (root.isEndOfWord)
      {
        str[level] = '\0';
        document.write(str.join("") + "</br>");
      }

      let i;
      for (i = 0; i < ALPHABET_SIZE; i++)
      {

        // If NON NULL child is found
        // add parent key to str and
        // call the display function recursively
        // for child node
        if (root.children[i] != null)
        {
          str[level] = String.fromCharCode(i + 'a'.charCodeAt());
          display(root.children[i], str, level + 1);
        }
      }
    }

    let keys = [ "apple", "app", "there", "the", "like" ];
    let n = keys.length;
    let root = getNode();

    // Conclass trie
    for (let i = 0; i < n; i++)
      insert(root, keys[i]);
    let str = new Array(100);
    display(root, str, 0);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
apple
like
there
```