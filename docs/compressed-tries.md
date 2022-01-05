# 压缩尝试

> 原文:[https://www.geeksforgeeks.org/compressed-tries/](https://www.geeksforgeeks.org/compressed-tries/)

一个 [trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 是一个[数据结构](https://www.geeksforgeeks.org/data-structures/)，它像一个[树形数据结构](https://www.geeksforgeeks.org/binary-tree-data-structure/)一样存储[字符串](https://www.geeksforgeeks.org/string-data-structure/)。一个节点中的最大子节点数等于字母表的大小。人们可以很容易地按字母顺序打印字母，这是[散列](https://www.geeksforgeeks.org/hashing-data-structure/)所不能做到的。

**<u>特里尔</u>属性:**

*   这是一棵多路树。
*   每个节点都有从 **1** 到 **N** 的子节点。
*   每个叶节点对应于存储的字符串，该字符串是从根到其边的路径上的一串字符。

[**特里类型**](https://www.geeksforgeeks.org/types-of-tries/)T4:

*   标准排序
*   后缀排序
*   压缩 Trie

**<u>压缩特里</u> :**

尝试至少 2 个度的节点。它是通过压缩标准 trie 的节点来实现的。也被称为**根试**。它用于实现空间优化

因为节点被压缩了。让我们直观地比较标准树的[结构](https://www.geeksforgeeks.org/structures-c/)和**压缩树**以获得更好的方法。就[内存](https://www.geeksforgeeks.org/what-is-memory-leak-how-can-we-avoid/)而言，压缩的 trie 树使用的节点数量非常少，这为具有长公共前缀的字符串提供了巨大的内存优势(尤其是对于长字符串)。就速度而言，常规的 trie 树会稍微快一些，因为它的操作不涉及任何字符串操作，它们是简单的循环。

在下图中，左边的树是标准树，右边的树是压缩树。

[![](img/bc180d3dba7c2ba793d257b5b601a2a3.png)](https://media.geeksforgeeks.org/wp-content/uploads/20201124222534/GFGFINAL.png)

**实施:**

标准的 trie 节点如下所示:

## Java 语言(一种计算机语言，尤用于创建网站)

```
class node {
    node[] children = new node[26];
    boolean isWordEnd;
}
```

## 蟒蛇 3

```
class node:
  def __init__(self):
      self.node = [None]*26
    self.isWordEnd=False
```

但是对于压缩的 trie，树的重新设计如下，在一般的 trie 中，边‘a’由引用数组中的这个特定元素表示，但是在压缩的 trie 中，“边‘面’由引用数组中的这个特定元素表示”。守则是:

## Java 语言(一种计算机语言，尤用于创建网站)

```
class node {
    node[] children = new node[26];
    StringBuilder[] edgeLabel = new StringBuilder[26];
    boolean isEnd;
}
```

## 蟒蛇 3

```
class node:
    def __init__(self):
      self.children = [None]*26
      sefl.edgeLabel = [None]*26
      self.isEnd=False
```

**压缩特里中的节点:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
class CompressedNode {
    int bitNumber;
    int data;
    CompressedNode leftChild, rightChild;
}
```

## 蟒蛇 3

```
class node:
    def __init__(self):
      self.bitNumber=0
      self.data=None
      self.leftChild, self.rightChild=None,None
```

**压缩等级:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
class CompressedNode {

    // Root Node
    private CompressedNode root;

    private static final int MaxBits = 10;

    // Constructor
    public CompressedNode() { root = null; }

    // Function to check if empty
    public boolean isEmpty() { return root == null; }

    // Function to clear
    public void makeEmpty() { root = null; }
}
```

## 蟒蛇 3

```
class CompressedNode {

    #Root Node
    root=CompressedNode()

       MaxBits = 10

    #Constructor
    def __init__(self):
          self.root = None

    #Function to check if empty
    def isEmpty(self):
          return self.root == None

    #Function to clear
    def makeEmpty(self):
          self.root = None
```

**在压缩特里中搜索:**

在压缩的 Trie 树中搜索很像[搜索](https://www.geeksforgeeks.org/searching-algorithms/)。这里，我们不是比较单个字符，而是比较字符串。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to search a key k
// in the trie
public boolean search(int k)
{
    // Find the number of bits
    int numOfBits = (int)(Math.log(k) / Math.log(2)) + 1;

    // If error occurs
    if (numOfBits > MaxBits) {
        System.out.println("Error : Number too large");
        return false;
    }

    // Search Node
    CompressedNode searchNode = search(root, k);

    // If the data matches
    if (searchNode.data == k)
        return true;

    // Else return false
    else
        return false;
}
```

## 蟒蛇 3

```
# Function to search a key k
# in the trie
import math
def search(k):

    # Find the number of bits
    numOfBits = int(math.log2(k)) + 1

    # If error occurs
    if (numOfBits > MaxBits) :
        print("Error : Number too large")
        return False

    # Search Node
    searchNode = search(root, k)

    # If the data matches
    if (searchNode.data == k):
        return True

    # Else return false
    else:
        return False
```

**在压缩特里中插入元素:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to implement the insert
// functionality in the trie
private CompressedNode insert(
    CompressedNode t, int ele)
{
    CompressedNode current, parent;
    CompressedNode lastNode, newNode;
    int i;

    // If Node is NULL
    if (t == null) {
        t = new CompressedNode();
        t.bitNumber = 0;
        t.data = ele;
        t.leftChild = t;
        t.rightChild = null;
        return t;
    }

    // Search the key ele
    lastNode = search(t, ele);

    // If already present key
    if (ele == lastNode.data) {
        System.out.println(
            "Error : key is already present\n");
        return t;
    }

    for (i = 1; bit(ele, i) == bit(lastNode.data, i); i++)
        ;

    current = t.leftChild;
    parent = t;
    while (current.bitNumber > parent.bitNumber
           && current.bitNumber < i) {
        parent = current;
        current = (bit(ele, current.bitNumber))
                      ? current.rightChild
                      : current.leftChild;
    }

    newNode = new CompressedNode();
    newNode.bitNumber = i;
    newNode.data = ele;
    newNode.leftChild = bit(ele, i) ? current : newNode;
    newNode.rightChild = bit(ele, i) ? newNode : current;

    if (current == parent.leftChild)
        parent.leftChild = newNode;
    else
        parent.rightChild = newNode;

    return t;
}
```

## 蟒蛇 3

```
# Function to implement the insert
# functionality in the trie
def insert( t, ele):
    # If Node is None
    if (t == None) :
        t = CompressedNode()
        t.bitNumber = 0
        t.data = ele
        t.leftChild = t
        t.rightChild = None
        return t

    # Search the key ele
    lastNode = search(t, ele)

    # If already present key
    if (ele == lastNode.data) :
        print(
            "Error : key is already present")
        return t

    i=1
    while(bit(ele, i) == bit(lastNode.data, i)):
        i+=1

    current = t.leftChild
    parent = t
    while (current.bitNumber > parent.bitNumber and current.bitNumber < i) :
        parent = current
        current = current.rightChild if (bit(ele, current.bitNumber)) else current.leftChild

    newNode = CompressedNode()
    newNode.bitNumber = i
    newNode.data = ele
    newNode.leftChild = current if bit(ele, i) else newNode
    newNode.rightChild = newNode if bit(ele, i) else current

    if (current == parent.leftChild):
        parent.leftChild = newNode
    else:
        parent.rightChild = newNode

    return t
```

以下是实现压缩 Trie 所有功能的程序:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// Compressed Trie

class Trie {

    // Root Node
    private final Node root = new Node(false);

    // 'a' for lower, 'A' for upper
    private final char CASE;

    // Default case
    public Trie() { CASE = 'a'; }

    // Constructor accepting the
    // starting symbol
    public Trie(char CASE)
    {
        this.CASE = CASE;
    }

    // Function to insert a word in
    // the compressed trie
    public void insert(String word)
    {
        // Store the root
        Node trav = root;
        int i = 0;

        // Iterate i less than word
        // length
        while (i < word.length()
               && trav.edgeLabel[word.charAt(i) - CASE]
                      != null) {

            // Find the index
            int index = word.charAt(i) - CASE, j = 0;
            StringBuilder label = trav.edgeLabel[index];

            // Iterate till j is less
            // than label length
            while (j < label.length() && i < word.length()
                   && label.charAt(j) == word.charAt(i)) {
                ++i;
                ++j;
            }

            // If is the same as the
            // label length
            if (j == label.length()) {
                trav = trav.children[index];
            }
            else {

                // Inserting a prefix of
                // the existing word
                if (i == word.length()) {
                    Node existingChild
                        = trav.children[index];
                    Node newChild = new Node(true);
                    StringBuilder remainingLabel
                        = strCopy(label, j);

                    // Making "facebook"
                    // as "face"
                    label.setLength(j);

                    // New node for "face"
                    trav.children[index] = newChild;
                    newChild
                        .children[remainingLabel.charAt(0)
                                  - CASE]
                        = existingChild;
                    newChild
                        .edgeLabel[remainingLabel.charAt(0)
                                   - CASE]
                        = remainingLabel;
                }
                else {

                    // Inserting word which has
                    // a partial match with
                    // existing word
                    StringBuilder remainingLabel
                        = strCopy(label, j);

                    Node newChild = new Node(false);
                    StringBuilder remainingWord
                        = strCopy(word, i);

                    // Store the trav in
                    // temp node
                    Node temp = trav.children[index];

                    label.setLength(j);
                    trav.children[index] = newChild;
                    newChild
                        .edgeLabel[remainingLabel.charAt(0)
                                   - CASE]
                        = remainingLabel;
                    newChild
                        .children[remainingLabel.charAt(0)
                                  - CASE]
                        = temp;
                    newChild
                        .edgeLabel[remainingWord.charAt(0)
                                   - CASE]
                        = remainingWord;
                    newChild
                        .children[remainingWord.charAt(0)
                                  - CASE]
                        = new Node(true);
                }

                return;
            }
        }

        // Insert new node for new word
        if (i < word.length()) {
            trav.edgeLabel[word.charAt(i) - CASE]
                = strCopy(word, i);
            trav.children[word.charAt(i) - CASE]
                = new Node(true);
        }
        else {

            // Insert "there" when "therein"
            // and "thereafter" are existing
            trav.isEnd = true;
        }
    }

    // Function that creates new String
    // from an existing string starting
    // from the given index
    private StringBuilder strCopy(
        CharSequence str, int index)
    {
        StringBuilder result
            = new StringBuilder(100);

        while (index != str.length()) {
            result.append(str.charAt(index++));
        }

        return result;
    }

    // Function to print the Trie
    public void print()
    {
        printUtil(root, new StringBuilder());
    }

    // Function to print the word
    // starting from the given node
    private void printUtil(
        Node node, StringBuilder str)
    {
        if (node.isEnd) {
            System.out.println(str);
        }

        for (int i = 0;
             i < node.edgeLabel.length; ++i) {

            // If edgeLabel is not
            // NULL
            if (node.edgeLabel[i] != null) {
                int length = str.length();

                str = str.append(node.edgeLabel[i]);
                printUtil(node.children[i], str);
                str = str.delete(length, str.length());
            }
        }
    }

    // Function to search a word
    public boolean search(String word)
    {
        int i = 0;

        // Stores the root
        Node trav = root;

        while (i < word.length()
               && trav.edgeLabel[word.charAt(i) - CASE]
                      != null) {
            int index = word.charAt(i) - CASE;
            StringBuilder label = trav.edgeLabel[index];
            int j = 0;

            while (i < word.length()
                   && j < label.length()) {

                // Character mismatch
                if (word.charAt(i) != label.charAt(j)) {
                    return false;
                }

                ++i;
                ++j;
            }

            if (j == label.length() && i <= word.length()) {

                // Traverse further
                trav = trav.children[index];
            }
            else {

                // Edge label is larger
                // than target word
                // searching for "face"
                // when tree has "facebook"
                return false;
            }
        }

        // Target word fully traversed
        // and current node is word
        return i == word.length() && trav.isEnd;
    }

    // Function to search the prefix
    public boolean startsWith(String prefix)
    {
        int i = 0;

        // Stores the root
        Node trav = root;

        while (i < prefix.length()
               && trav.edgeLabel[prefix.charAt(i) - CASE]
                      != null) {
            int index = prefix.charAt(i) - CASE;
            StringBuilder label = trav.edgeLabel[index];
            int j = 0;

            while (i < prefix.length()
                   && j < label.length()) {

                // Character mismatch
                if (prefix.charAt(i) != label.charAt(j)) {
                    return false;
                }

                ++i;
                ++j;
            }

            if (j == label.length()
                && i <= prefix.length()) {

                // Traverse further
                trav = trav.children[index];
            }
            else {

                // Edge label is larger
                // than target word,
                // which is fine
                return true;
            }
        }

        return i == prefix.length();
    }
}

// Node class
class Node {

    // Number of symbols
    private final static int SYMBOLS = 26;
    Node[] children = new Node[SYMBOLS];
    StringBuilder[] edgeLabel = new StringBuilder[SYMBOLS];
    boolean isEnd;

    // Function to check if the end
    // of the string is reached
    public Node(boolean isEnd)
    {
        this.isEnd = isEnd;
    }
}

class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        Trie trie = new Trie();

        // Insert words
        trie.insert("facebook");
        trie.insert("face");
        trie.insert("this");
        trie.insert("there");
        trie.insert("then");

        // Print inserted words
        trie.print();

        // Check if these words
        // are present or not
        System.out.println(
            trie.search("there"));
        System.out.println(
            trie.search("therein"));
        System.out.println(
            trie.startsWith("th"));
        System.out.println(
            trie.startsWith("fab"));
    }
}
```

## 蟒蛇 3

```
# Java program to implement the
# Compressed Trie

class Trie:

    # Root Node
    root = Node(False)
    CASE=''

    # Default self.CASE
    def Trie(self, CASE='a') : self.CASE = CASE

    # Function to insert a word in
    # the compressed trie
    def insert(self,word):
        # Store the root
        trav = root
        i = 0

        # Iterate i less than word
        # length
        while (i < word.length() and trav.edgeLabel[word.charAt(i) - self.CASE] is not None) :

            # Find the index
            index = ord(word[i]) - ord(self.CASE); j = 0
            label = trav.edgeLabel[index]

            # Iterate till j is less
            # than label length
            while (j < len(label) and i < len(word) and label[j] == word[i]) :
                i+=1
                j+=1

            # If is the same as the
            # label length
            if (j == label.length()) :
                trav = trav.children[index]

            else :

                # Inserting a prefix of
                # the existing word
                if (i == word.length()) :
                    existingChild = trav.children[index]
                    newChild = Node(True)
                    remainingLabel = strCopy(label, j)

                    # Making "facebook"
                    # as "face"
                    label.setLength(j)

                    # New node for "face"
                    trav.children[index] = newChild
                    newChild.children[ord(remainingLabel[0])-ord(self.CASE)] = existingChild
                    newChild.edgeLabel[ord(remainingLabel.charAt(0))- ord(self.CASE)] = remainingLabel

                else :

                    # Inserting word which has
                    # a partial match with
                    # existing word
                    remainingLabel = strCopy(label, j)

                    newChild = Node(False)
                    remainingWord = strCopy(word, i)

                    # Store the trav in
                    # temp node
                    temp = trav.children[index]

                    trav.children[index] = newChild
                    newChild.edgeLabel[ord(remainingLabel.charAt(0)) - ord(self.CASE)]=remainingLabel
                    newChild.children[ord(remainingLabel.charAt(0)) - ord(self.CASE)]=temp
                    newChild.edgeLabel[ord(remainingWord.charAt(0)) - ord(self.CASE)] = remainingWord
                    newChild.children[ord(remainingWord.charAt(0)) - ord(self.CASE)] = Node(True)
                return

        # Insert new node for new word
        if (i < len(word)):
            trav.edgeLabel[ord(word.charAt(i)) - ord(self.CASE)] = strCopy(word, i)
            trav.children[ord(word.charAt(i)) - ord(self.CASE)] = Node(True)

        else :

            # Insert "there" when "therein"
            # and "thereafter" are existing
            trav.isEnd = True

    # Function that creates new String
    # from an existing string starting
    # from the given index
    def strCopy(self, str, index):
        result = ''

        while (index != len(str)) :
            result+=str.charAt(index)
            index+=1

        return result

    # Function to print the word
    # starting from the given node
    def printUtil(self,node, str):
        if (node.isEnd) :
            print(str)

        for i in range(node.edgeLabel.length):

            # If edgeLabel is not
            # None
            if (node.edgeLabel[i] != None) :
                length = len(str)

                str = str.append(node.edgeLabel[i])
                printUtil(node.children[i], str)
                str = str.delete(length, str.length())

    # Function to search a word
    def search(self,word):
        i = 0

        # Stores the root
        trav = root

        while (i < len(word) and trav.edgeLabel[ord(word.charAt(i)) - ord(self.CASE)]
                      != None) :
            index = ord(word.charAt(i)) - ord(self.CASE)
            label = trav.edgeLabel[index]
            j = 0

            while (i < word.length() and j < label.length()) :

                # Character mismatch
                if (word.charAt(i) != label.charAt(j)) :
                    return False

                i+=1
                j+=1

            if (j == len(label) and i <= len(word)) :

                # Traverse further
                trav = trav.children[index]

            else :

                # Edge label is larger
                # than target word
                # searching for "face"
                # when tree has "facebook"
                return False

        # Target word fully traversed
        # and current node is word
        return i == len(word) and trav.isEnd

    # Function to search the prefix
    def startsWith(self,prefix):
        i = 0

        # Stores the root
        trav = root

        while (i < prefix.length() and trav.edgeLabel[prefix.charAt(i) - self.CASE]is not None) :
            index = ord(prefix.charAt(i)) - ord(self.CASE)
            label = trav.edgeLabel[index]
            j = 0

            while (i < prefix.length() and j < label.length()) :

                # Character mismatch
                if (prefix.charAt(i) != label.charAt(j)) :
                    return False

                i+=1
                j+=1

            if (j == len(label) and j<= len(prefix)) :

                # Traverse further
                trav = trav.children[index]

            else :

                # Edge label is larger
                # than target word,
                # which is fine
                return True

        return i == prefix.length()

# Node class
class Node :

    def __init__(self):
        # Number of symbols
        self.SYMBOLS = 26
        self.children = [None]*26
        self.edgeLabel = [None]*SYMBOLS
        self.isEnd=False

    # Function to check if the end
    # of the string is reached
    def Node(self,isEnd):
        self.isEnd = isEnd

class GFG :

    # Driver Code
    if __name__ == '__main__':
        trie = Trie()

        # Insert words
        trie.insert("facebook")
        trie.insert("face")
        trie.insert("this")
        trie.insert("there")
        trie.insert("then")

        # Print inserted words
        trie.print()

        # Check if these words
        # are present or not
        print(
            trie.search("there"))
        print(
            trie.search("therein"))
        print(
            trie.startsWith("th"))
        print(
            trie.startsWith("fab"))
```

**Output:** 

```
face
facebook
then
there
this
true
false
true
false
```