# 使用 Trie | Set-2(处理重复项)

对字符串(或单词)数组进行排序

> 原文:[https://www . geesforgeks . org/sorting-array-strings-word-using-trie-set-2-handling-duplicates/](https://www.geeksforgeeks.org/sorting-array-strings-words-using-trie-set-2-handling-duplicates/)

给定一组字符串，按字母(字典)顺序打印它们。如果输入数组中有重复项，我们需要打印所有重复项。
示例:

```
Input : arr[] = { "abc", "xyz", "abcd", "bcd", "abc" }
Output : abc abc abcd bcd xyz

Input : arr[] = { "geeks", "for", "geeks", "a", "portal", 
                  "to", "learn" }
Output : a for geeks geeks learn portal to
```

**先决条件:** [特里|(插入并搜索)。](https://www.geeksforgeeks.org/trie-insert-and-search/)
**方法:**在[之前的帖子中](https://www.geeksforgeeks.org/sorting-array-strings-words-using-trie/)的字符串数组正在被排序，只打印单次出现的重复字符串。在这篇文章中，所有出现的重复字符串都按照字典顺序打印。要按字母顺序打印字符串，我们必须首先将它们插入 trie，然后执行前序遍历以按字母顺序打印。trie 的节点包含一个**索引[]** 数组，该数组存储在该节点结束的 **arr[]** 的所有字符串的索引位置。对于**索引[]** 数组，除了 trie 的叶节点，所有其他节点的大小都为 0。
以下是上述办法的实施情况。

## C++

```
// C++ implementation to sort an array
// of strings using Trie
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

struct Trie {

    // 'index' vectors size is greater than
    // 0 when node/ is a leaf node, otherwise
    // size is 0;
    vector<int> index;

    Trie* child[MAX_CHAR];

    /*to make new trie*/
    Trie()
    {
        // initializing fields
        for (int i = 0; i < MAX_CHAR; i++)
            child[i] = NULL;
    }
};

// function to insert a string in trie
void insert(Trie* root, string str, int index)
{
    Trie* node = root;

    for (int i = 0; i < str.size(); i++) {

        // taking ascii value to find index of
        // child node
        char ind = str[i] - 'a';

        // making a new path if not already
        if (!node->child[ind])
            node->child[ind] = new Trie();

        // go to next node
        node = node->child[ind];
    }

    // Mark leaf (end of string) and store
    // index of 'str' in index[]
    (node->index).push_back(index);
}

// function for preorder traversal of trie
void preorder(Trie* node, string arr[])
{
    // if node is empty
    if (node == NULL)
        return;

    for (int i = 0; i < MAX_CHAR; i++) {
        if (node->child[i] != NULL) {

            // if leaf node then print all the strings
            // for (node->child[i]->index).size() > 0)
            for (int j = 0; j < (node->child[i]->index).size(); j++)
                cout << arr[node->child[i]->index[j]] << " ";

            preorder(node->child[i], arr);
        }
    }
}

// function to sort an array
// of strings using Trie
void printSorted(string arr[], int n)
{
    Trie* root = new Trie();

    // insert all strings of dictionary into trie
    for (int i = 0; i < n; i++)
        insert(root, arr[i], i);

    // print strings in lexicographic order
    preorder(root, arr);
}

// Driver program to test above
int main()
{
    string arr[] = { "abc", "xyz", "abcd", "bcd", "abc" };
    int n = sizeof(arr) / sizeof(arr[0]);
    printSorted(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// to sort an array of
// strings using Trie
import java.util.*;

class Trie {

    private Node rootNode;

    /*to make new trie*/
    Trie()
    {
        rootNode = null;
    }

    // function to insert
    // a string in trie
    void insert(String key, int index)
    {
        // making a new path
        // if not already
        if (rootNode == null)
        {
            rootNode = new Node();
        }

        Node currentNode = rootNode;

        for (int i = 0;i < key.length();i++)
        {
            char keyChar = key.charAt(i);

            if (currentNode.getChild(keyChar) == null)
            {
                currentNode.addChild(keyChar);
            }

            // go to next node
            currentNode = currentNode.getChild(keyChar);
        }

        // Mark leaf (end of string)
        // and store index of 'str'
        // in index[]
        currentNode.addIndex(index);
    }

    void traversePreorder(String[] array)
    {
        traversePreorder(rootNode, array);
    }

    // function for preorder
    // traversal of trie
    private void traversePreorder(Node node,
                             String[] array)
    {
        if (node == null)
        {
            return;
        }

        if (node.getIndices().size() > 0)
        {
            for (int index : node.getIndices())
            {
                System.out.print(array[index] + " ");
            }
        }

        for (char index = 'a';index <= 'z';index++)
        {
            traversePreorder(node.getChild(index), array);
        }
    }

    private static class Node {

        private Node[] children;
        private List<Integer> indices;

        Node()
        {
            children = new Node[26];
            indices = new ArrayList<>(0);
        }

        Node getChild(char index)
        {
            if (index < 'a' || index > 'z')
            {
                return null;
            }

            return children[index - 'a'];
        }

        void addChild(char index)
        {
            if (index < 'a' || index > 'z')
            {
                return;
            }

            Node node = new Node();
            children[index - 'a'] = node;
        }

        List<Integer> getIndices()
        {
            return indices;
        }

        void addIndex(int index)
        {
            indices.add(index);
        }
    }
}

class SortStrings {

    // Driver program
    public static void main(String[] args)
    {
        String[] array = { "abc", "xyz",
                    "abcd", "bcd", "abc" };
        printInSortedOrder(array);
    }

    // function to sort an array
    // of strings using Trie
    private static void printInSortedOrder(String[] array)
    {
        Trie trie = new Trie();

        for (int i = 0;i < array.length;i++)
        {
            trie.insert(array[i], i);
        }

        trie.traversePreorder(array);
    }
}

// Contributed by Harikrishnan Rajan
```

## C#

```
// C# implementation
// to sort an array of
// strings using Trie
using System;
using System.Collections.Generic;

public class Trie
{

    public Node rootNode;

    /* to make new trie*/
    public Trie()
    {
        rootNode = null;
    }

    // function to insert
    // a string in trie
    public void insert(String key, int index)
    {
        // making a new path
        // if not already
        if (rootNode == null)
        {
            rootNode = new Node();
        }

        Node currentNode = rootNode;

        for (int i = 0;i < key.Length;i++)
        {
            char keyChar = key[i];

            if (currentNode.getChild(keyChar) == null)
            {
                currentNode.addChild(keyChar);
            }

            // go to next node
            currentNode = currentNode.getChild(keyChar);
        }

        // Mark leaf (end of string)
        // and store index of 'str'
        // in index[]
        currentNode.addIndex(index);
    }

    public void traversePreorder(String[] array)
    {
        traversePreorder(rootNode, array);
    }

    // function for preorder
    // traversal of trie
    public void traversePreorder(Node node,
                            String[] array)
    {
        if (node == null)
        {
            return;
        }

        if (node.getIndices().Count > 0)
        {
            foreach (int index in node.getIndices())
            {
                Console.Write(array[index] + " ");
            }
        }

        for (char index = 'a';index <= 'z';index++)
        {
            traversePreorder(node.getChild(index), array);
        }
    }

    public class Node
    {

        public Node[] children;
        public List<int> indices;

        public Node()
        {
            children = new Node[26];
            indices = new List<int>(0);
        }

        public Node getChild(char index)
        {
            if (index < 'a' || index > 'z')
            {
                return null;
            }

            return children[index - 'a'];
        }

        public void addChild(char index)
        {
            if (index < 'a' || index > 'z')
            {
                return;
            }

            Node node = new Node();
            children[index - 'a'] = node;
        }

        public List<int> getIndices()
        {
            return indices;
        }

        public void addIndex(int index)
        {
            indices.Add(index);
        }
    }
}

public class SortStrings
{

    // Driver code
    public static void Main(String[] args)
    {
        String[] array = { "abc", "xyz",
                    "abcd", "bcd", "abc" };
        printInSortedOrder(array);
    }

    // function to sort an array
    // of strings using Trie
    static void printInSortedOrder(String[] array)
    {
        Trie trie = new Trie();

        for (int i = 0;i < array.Length;i++)
        {
            trie.insert(array[i], i);
        }

        trie.traversePreorder(array);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation to sort an array
# of strings using Trie
from typing import List
MAX_CHAR = 26
class Trie:
    def __init__(self) -> None:

        # 'index' vectors size is greater than
        # 0 when node/ is a leaf node, otherwise
        # size is 0;
        self.index = []
        self.child = [None for _ in range(MAX_CHAR)]

# function to insert a string in trie
def insert(root: Trie, string: str, index: int) -> None:
    node = root
    for i in range(len(string)):

        # taking ascii value to find index of
        # child node
        ind = ord(string[i]) - ord('a')

        # making a new path if not already
        if (node.child[ind] == None):
            node.child[ind] = Trie()

        # go to next node
        node = node.child[ind]

    # Mark leaf (end of string) and store
    # index of 'str' in index[]
    (node.index).append(index)

# function for preorder traversal of trie
def preorder(node: Trie, arr: List[str]) -> None:

    # if node is empty
    if (node == None):
        return
    for i in range(MAX_CHAR):
        if (node.child[i] != None):

            # if leaf node then print all the strings
            # for (node.child[i].index).size() > 0)
            for j in range(len(node.child[i].index)):
                print(arr[node.child[i].index[j]], end = " ")
            preorder(node.child[i], arr)

# function to sort an array
# of strings using Trie
def printSorted(arr: List[str], n: int) -> None:
    root = Trie()

    # insert all strings of dictionary into trie
    for i in range(n):
        insert(root, arr[i], i)

    # print strings in lexicographic order
    preorder(root, arr)

# Driver program to test above
if __name__ == "__main__":

    arr = ["abc", "xyz", "abcd", "bcd", "abc"]
    n = len(arr)
    printSorted(arr, n)

# This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>

// JavaScript implementation
// to sort an array of
// strings using Trie

let rootNode=null;

 // function to insert
    // a string in trie
function insert(key,index)
{
    // making a new path
        // if not already
        if (rootNode == null)
        {
            rootNode = new Node();
        }

        let currentNode = rootNode;

        for (let i = 0;i < key.length;i++)
        {
            let keyChar = key[i];

            if (currentNode.getChild(keyChar) == null)
            {
                currentNode.addChild(keyChar);
            }

            // go to next node
            currentNode = currentNode.getChild(keyChar);
        }

        // Mark leaf (end of string)
        // and store index of 'str'
        // in index[]
        currentNode.addIndex(index);
}

// function for preorder
    // traversal of trie
function traversePreorder(array)
{
    _traversePreorder(rootNode, array);
}

function _traversePreorder(node,array)
{
    if (node == null)
        {
            return;
        }

        if (node.getIndices().length > 0)
        {
            for (let index=0;index<
            node.getIndices().length;index++)
            {
                document.write(array[node.getIndices()[index]] + " ");
            }
        }

        for (let index = 'a'.charCodeAt(0);index <=
        'z'.charCodeAt(0);index++)
        {
           _traversePreorder(node.getChild(String.fromCharCode(index)),
           array);
        }
}

class Node
{
    constructor()
    {
        this.children = new Array(26);
        this.indices = [];
    }

    getChild(index)
    {
        if (index < 'a' || index > 'z')
            {
                return null;
            }

            return this.children[index.charCodeAt(0) -
            'a'.charCodeAt(0)];
    }

    addChild(index)
    {
        if (index < 'a' || index > 'z')
            {
                return;
            }

            let node = new Node();
            this.children[index.charCodeAt(0) -
            'a'.charCodeAt(0)] = node;
    }

    getIndices()
    {
        return this.indices;
    }

    addIndex(index)
    {
        this.indices.push(index);
    }

}

// function to sort an array
    // of strings using Trie
function printInSortedOrder(array)
{

        for (let i = 0;i < array.length;i++)
        {
            insert(array[i], i);
        }

        traversePreorder(array);
}

// Driver program
array=["abc", "xyz","abcd", "bcd", "abc"];

printInSortedOrder(array);

// This code is contributed by rag2127

</script>
```

**输出:**

```
abc abc abcd bcd xyz
```

**时间复杂度:**当每个字符串都以不同的字符开始时，会出现最坏的情况。在这种情况下，它将访问每个字符串中每个字符的所有节点。因此，最坏情况下的时间复杂度将是每个字符串的长度之和，即 O(|S1| + |S2| + |S3| + … + |Sn|)，其中|S|是字符串的长度。