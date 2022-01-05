# 给定一个单词序列，一起打印所有的字谜|第 2 集

> 原文:[https://www . geeksforgeeks . org/给定单词序列-打印-所有字谜-集合-2/](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together-set-2/)

给定一组单词，一起打印所有的字谜。例如，如果给定的数组是{“猫”、“狗”、“tac”、“神”、“act”}，那么输出可能是“猫 tac act 狗神”。

我们在[之前的帖子](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together/)中讨论了两种不同的方法。在这篇文章中，讨论了一个更有效的解决方案。
Trie 数据结构可以用于更高效的解决方案。在 trie 中插入每个单词的排序顺序。因为所有的字谜都会在同一个叶节点结束。我们可以在叶节点处开始一个链表，其中每个节点代表原始单词数组的索引。最后，遍历 Trie。遍历 Trie 时，一次遍历一行每个链表。以下是详细步骤。
**1)** 创建一个空的 Trie
**2)** 一个一个的取输入序列的所有单词。对每个单词执行以下操作
… **a)** 将单词复制到缓冲区。
……**b)**对缓冲区进行排序
……**c)**将排序后的缓冲区和这个词的索引插入到 Trie 中。特里的每个叶节点都是索引列表的头。索引列表按原始顺序存储单词索引。如果排序的缓冲区已经存在，我们将这个单词的索引插入索引列表。
**3)** 穿越特里尔。遍历时，如果到达叶节点，遍历索引列表。并使用从索引列表中获得的索引打印所有单词。

下面是上述方法的实现:

## C++

```
// An efficient program to print all anagrams together
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define NO_OF_CHARS 26

// Structure to represent list node for indexes of words in
// the given sequence. The list nodes are used to connect
// anagrams at leaf nodes of Trie
struct IndexNode
{
    int index;
    struct IndexNode* next;
};

// Structure to represent a Trie Node
struct TrieNode
{
    bool isEnd;  // indicates end of word
    struct TrieNode* child[NO_OF_CHARS]; // 26 slots each for 'a' to 'z'
    struct IndexNode* head; // head of the index list
};

// A utility function to create a new Trie node
struct TrieNode* newTrieNode()
{
    struct TrieNode* temp = new TrieNode;
    temp->isEnd = 0;
    temp->head = NULL;
    for (int i = 0; i < NO_OF_CHARS; ++i)
        temp->child[i] = NULL;
    return temp;
}

/* Following function is needed for library function qsort(). Refer
   http://www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
int compare(const void* a, const void* b)
{  return *(char*)a - *(char*)b; }

/* A utility function to create a new linked list node */
struct IndexNode* newIndexNode(int index)
{
    struct IndexNode* temp = new IndexNode;
    temp->index = index;
    temp->next = NULL;
    return temp;
}

// A utility function to insert a word to Trie
void insert(struct TrieNode** root, char* word, int index)
{
    // Base case
    if (*root == NULL)
        *root = newTrieNode();

    if (*word != '\0')
        insert( &( (*root)->child[tolower(*word) - 'a'] ), word+1, index );
    else  // If end of the word reached
    {
        // Insert index of this word to end of index linked list
        if ((*root)->isEnd)
        {
            IndexNode* pCrawl = (*root)->head;
            while( pCrawl->next )
                pCrawl = pCrawl->next;
            pCrawl->next = newIndexNode(index);
        }
        else  // If Index list is empty
        {
            (*root)->isEnd = 1;
            (*root)->head = newIndexNode(index);
        }
    }
}

// This function traverses the built trie. When a leaf node is reached,
// all words connected at that leaf node are anagrams. So it traverses
// the list at leaf node and uses stored index to print original words
void printAnagramsUtil(struct TrieNode* root, char *wordArr[])
{
    if (root == NULL)
        return;

    // If a lead node is reached, print all anagrams using the indexes
    // stored in index linked list
    if (root->isEnd)
    {
        // traverse the list
        IndexNode* pCrawl = root->head;
        while (pCrawl != NULL)
        {
            printf( "%s ", wordArr[ pCrawl->index ] );
            pCrawl = pCrawl->next;
        }
    }

    for (int i = 0; i < NO_OF_CHARS; ++i)
        printAnagramsUtil(root->child[i], wordArr);
}

// The main function that prints all anagrams together. wordArr[] is input
// sequence of words.
void printAnagramsTogether(char* wordArr[], int size)
{
    // Create an empty Trie
    struct TrieNode* root = NULL;

    // Iterate through all input words
    for (int i = 0; i < size; ++i)
    {
        // Create a buffer for this word and copy the word to buffer
        int len = strlen(wordArr[i]);
        char *buffer = new char[len+1];
        strcpy(buffer, wordArr[i]);

        // Sort the buffer
        qsort( (void*)buffer, strlen(buffer), sizeof(char), compare );

        // Insert the sorted buffer and its original index to Trie
        insert(&root,  buffer, i);
    }

    // Traverse the built Trie and print all anagrams together
    printAnagramsUtil(root, wordArr);
}

// Driver program to test above functions
int main()
{
    char* wordArr[] = {"cat", "dog", "tac", "god", "act", "gdo"};
    int size = sizeof(wordArr) / sizeof(wordArr[0]);
    printAnagramsTogether(wordArr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient program to print all
// anagrams together   
import java.util.Arrays;
import java.util.LinkedList;

public class GFG
{
    static final int NO_OF_CHARS = 26;

    // Class to represent a Trie Node
    static class TrieNode
    {
        boolean isEnd;  // indicates end of word

        // 26 slots each for 'a' to 'z'
        TrieNode[] child = new TrieNode[NO_OF_CHARS];

        // head of the index list
        LinkedList<Integer> head;

        // constructor
        public TrieNode()
        {
            isEnd = false;
            head = new LinkedList<>();
            for (int i = 0; i < NO_OF_CHARS; ++i)
                child[i] = null;
        }
    }

    // A utility function to insert a word to Trie
    static TrieNode insert(TrieNode root,String word,
                                int index, int i)
    {
        // Base case
        if (root == null)
        {
            root = new TrieNode();
        }

        if (i < word.length() )
        {
            int index1 = word.charAt(i) - 'a';
            root.child[index1] = insert(root.child[index1],
                                       word, index, i+1 );
        }
        else  // If end of the word reached
        {
            // Insert index of this word to end of
            // index linked list
            if (root.isEnd == true)
            {
                root.head.add(index);
            }
            else // If Index list is empty
            {
                root.isEnd = true;
                root.head.add(index);
            }
        }
        return root;
    }

    // This function traverses the built trie. When a leaf
    // node is reached, all words connected at that leaf
    // node are anagrams. So it traverses the list at leaf 
    // node and uses stored index to print original words
    static void printAnagramsUtil(TrieNode root,
                                      String wordArr[])
    {
        if (root == null)
            return;

        // If a lead node is reached, print all anagrams
        // using the indexes stored in index linked list
        if (root.isEnd)
        {
            // traverse the list
            for(Integer pCrawl: root.head)
                System.out.println(wordArr[pCrawl]);
        }

        for (int i = 0; i < NO_OF_CHARS; ++i)
            printAnagramsUtil(root.child[i], wordArr);
    }

    // The main function that prints all anagrams together.
    // wordArr[] is input sequence of words.
    static void printAnagramsTogether(String wordArr[],
                                               int size)
    {
        // Create an empty Trie
        TrieNode root = null;

        // Iterate through all input words
        for (int i = 0; i < size; ++i)
        {
            // Create a buffer for this word and copy the
            // word to buffer
            char[] buffer = wordArr[i].toCharArray();

            // Sort the buffer
            Arrays.sort(buffer);

            // Insert the sorted buffer and its original
            // index to Trie
            root = insert(root, new String(buffer), i, 0);

        }

        // Traverse the built Trie and print all anagrams
        // together
        printAnagramsUtil(root, wordArr);
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        String wordArr[] = {"cat", "dog", "tac", "god",
                                        "act", "gdo"};
        int size = wordArr.length;
        printAnagramsTogether(wordArr, size);
    }
}
// This code is contributed by Sumit Ghosh
```

## C#

```
// An efficient C# program to print all
// anagrams together
using System;
using System.Collections.Generic;

class GFG
{
    static readonly int NO_OF_CHARS = 26;

    // Class to represent a Trie Node
    public class TrieNode
    {
        // indicates end of word
        public bool isEnd;

        // 26 slots each for 'a' to 'z'
        public TrieNode[] child = new TrieNode[NO_OF_CHARS];

        // head of the index list
        public List<int> head;

        // constructor
        public TrieNode()
        {
            isEnd = false;
            head = new List<int>();
            for (int i = 0; i < NO_OF_CHARS; ++i)
                child[i] = null;
        }
    }

    // A utility function to insert a word to Trie
    static TrieNode insert(TrieNode root,String word,
                                int index, int i)
    {
        // Base case
        if (root == null)
        {
            root = new TrieNode();
        }

        if (i < word.Length )
        {
            int index1 = word[i] - 'a';
            root.child[index1] = insert(root.child[index1],
                                    word, index, i + 1 );
        }

        // If end of the word reached
        else
        {
            // Insert index of this word to end of
            // index linked list
            if (root.isEnd == true)
            {
                root.head.Add(index);
            }

            // If Index list is empty
            else
            {
                root.isEnd = true;
                root.head.Add(index);
            }
        }
        return root;
    }

    // This function traverses the built trie.
    // When a leaf node is reached, all words
    // connected at that leaf node are anagrams.
    // So it traverses the list at leaf node
    // and uses stored index to print original words
    static void printAnagramsUtil(TrieNode root,
                                    String []wordArr)
    {
        if (root == null)
            return;

        // If a lead node is reached,
        // print all anagrams using the
        // indexes stored in index linked list
        if (root.isEnd)
        {
            // traverse the list
            foreach(int pCrawl in root.head)
                Console.WriteLine(wordArr[pCrawl]);
        }

        for (int i = 0; i < NO_OF_CHARS; ++i)
            printAnagramsUtil(root.child[i], wordArr);
    }

    // The main function that prints
    // all anagrams together. wordArr[]
    // is input sequence of words.
    static void printAnagramsTogether(String []wordArr,
                                            int size)
    {
        // Create an empty Trie
        TrieNode root = null;

        // Iterate through all input words
        for (int i = 0; i < size; ++i)
        {
            // Create a buffer for this word 
            // and copy the word to buffer
            char[] buffer = wordArr[i].ToCharArray();

            // Sort the buffer
            Array.Sort(buffer);

            // Insert the sorted buffer and 
            // its original index to Trie
            root = insert(root, new String(buffer), i, 0);

        }

        // Traverse the built Trie and 
        // print all anagrams together
        printAnagramsUtil(root, wordArr);
    }

    // Driver code
    public static void Main(String []args)
    {
        String []wordArr = {"cat", "dog", "tac", "god",
                                        "act", "gdo"};
        int size = wordArr.Length;
        printAnagramsTogether(wordArr, size);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// An efficient program to print all
// anagrams together  
let NO_OF_CHARS = 26;

// Class to represent a Trie Node
class TrieNode
{
    constructor()
    {
        this.isEnd = false;  // indicates end of word

        // 26 slots each for 'a' to 'z'
        this.child = new Array(NO_OF_CHARS);

        for (let i = 0; i < NO_OF_CHARS; ++i)
                this.child[i] = null;

        // head of the index list
        this.head=[];
    }
}

 // A utility function to insert a word to Trie
function insert(root,word,index,i)
{

    // Base case
        if (root == null)
        {
            root = new TrieNode();
        }
        if (i < word.length )
        {
            let index1 = word[i].charCodeAt(0) - 'a'.charCodeAt(0);

            root.child[index1] = insert(root.child[index1],
                                       word, index, i+1 );
        }
        else  // If end of the word reached
        {
            // Insert index of this word to end of
            // index linked list
            if (root.isEnd == true)
            {
                root.head.push(index);
            }
            else // If Index list is empty
            {
                root.isEnd = true;
                root.head.push(index);
            }
        }
        return root;
}

// This function traverses the built trie. When a leaf
    // node is reached, all words connected at that leaf
    // node are anagrams. So it traverses the list at leaf 
    // node and uses stored index to print original words
function printAnagramsUtil(root,wordArr)
{
    if (root == null)
            return;

        // If a lead node is reached, print all anagrams
        // using the indexes stored in index linked list
        if (root.isEnd)
        {
            // traverse the list
            for(let pCrawl=0;pCrawl<root.head.length;pCrawl++)
                document.write(wordArr[root.head[pCrawl]]+"<br>");
        }

        for (let i = 0; i < NO_OF_CHARS; ++i)
            printAnagramsUtil(root.child[i], wordArr);
}

// The main function that prints all anagrams together.
    // wordArr[] is input sequence of words.
function printAnagramsTogether(wordArr,size)
{
    // Create an empty Trie
        let root = null;

        // Iterate through all input words
        for (let i = 0; i < size; ++i)
        {
            // Create a buffer for this word and copy the
            // word to buffer
            let buffer = wordArr[i].split("");

            // Sort the buffer
            (buffer).sort();

            // Insert the sorted buffer and its original
            // index to Trie
            root = insert(root, (buffer).join(""), i, 0);

        }

        // Traverse the built Trie and print all anagrams
        // together
        printAnagramsUtil(root, wordArr);
}

// Driver program to test above functions
let wordArr=["cat", "dog", "tac", "god",
                                        "act", "gdo"];

let size = wordArr.length;
printAnagramsTogether(wordArr, size);

// This code is contributed by rag2127
</script>
```

**输出:**

```
cat
tac
act
dog
god
gdo
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。