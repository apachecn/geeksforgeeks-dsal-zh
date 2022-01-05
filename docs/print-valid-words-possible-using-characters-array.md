# 使用数组字符

打印所有可能的有效单词

> 原文:[https://www . geesforgeks . org/print-valid-word-可能-使用-字符-array/](https://www.geeksforgeeks.org/print-valid-words-possible-using-characters-array/)

给定字典和字符数组，使用数组中的字符打印所有可能的有效单词。

示例:

```
Input : Dict - {"go","bat","me","eat","goal", 
                                "boy", "run"} 
        arr[] = {'e','o','b', 'a','m','g', 'l'} 
Output : go, me, goal. 

```

问于:微软采访

其思想是使用 Trie 数据结构存储字典，然后使用给定数组的字符在 Trie 中搜索单词。

1.  创建一个空的 Trie，并将给定词典中的所有单词插入 Trie。
2.  之后，我们只选择了“Arr[]”中的那些字符，它们是特里根的子级。
3.  为了快速找到一个字符是否存在于数组中，我们创建一个字符数组的散列。

以下是以上想法的实现

## C++

```
// C++ program to print all valid words that
// are possible using character of array
#include<bits/stdc++.h>
using namespace std;

// Converts key current character into index
// use only 'a' through 'z'
#define char_int(c) ((int)c - (int)'a')

//converts current integer into character
#define int_to_char(c) ((char)c + (char)'a')

// Alphabet size
#define SIZE (26)

// trie Node
struct TrieNode
{
    TrieNode *Child[SIZE];

    // isLeaf is true if the node represents
    // end of a word
    bool leaf;
};

// Returns new trie node (initialized to NULLs)
TrieNode *getNode()
{
    TrieNode * newNode = new TrieNode;
    newNode->leaf = false;
    for (int i =0 ; i< SIZE ; i++)
        newNode->Child[i] = NULL;
    return newNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node, just
// marks leaf node
void insert(TrieNode *root, char *Key)
{
    int n = strlen(Key);
    TrieNode * pChild = root;

    for (int i=0; i<n; i++)
    {
        int index = char_int(Key[i]);

        if (pChild->Child[index] == NULL)
            pChild->Child[index] = getNode();

        pChild = pChild->Child[index];
    }

    // make last node as leaf node
    pChild->leaf = true;
}

// A recursive function to print all possible valid
// words present in array
void searchWord(TrieNode *root, bool Hash[], string str)
{
    // if we found word in trie / dictionary
    if (root->leaf == true)
        cout << str << endl ;

    // traverse all child's of current root
    for (int K =0; K < SIZE; K++)
    {
        if (Hash[K] == true && root->Child[K] != NULL )
        {
            // add current character
            char c = int_to_char(K);

            // Recursively search reaming character of word
            // in trie
            searchWord(root->Child[K], Hash, str + c);
        }
    }
}

// Prints all words present in dictionary.
void PrintAllWords(char Arr[], TrieNode *root, int n)
{
    // create a 'has' array that will store all present
    // character in Arr[]
    bool Hash[SIZE];

    for (int i = 0 ; i < n; i++)
        Hash[char_int(Arr[i])] = true;

    // tempary node
    TrieNode *pChild = root ;

    // string to hold output words
    string str = "";

    // Traverse all matrix elements. There are only 26
    // character possible in char array
    for (int i = 0 ; i < SIZE ; i++)
    {
        // we start searching for word in dictionary
        // if we found a character which is child
        // of Trie root
        if (Hash[i] == true && pChild->Child[i] )
        {
            str = str+(char)int_to_char(i);
            searchWord(pChild->Child[i], Hash, str);
            str = "";
        }
    }
}

//Driver program to test above function
int main()
{
    // Let the given dictionary be following
    char Dict[][20] = {"go", "bat", "me", "eat",
                       "goal", "boy", "run"} ;

    // Root Node of Trie
    TrieNode *root = getNode();

    // insert all words of dictionary into trie
    int n = sizeof(Dict)/sizeof(Dict[0]);
    for (int i=0; i<n; i++)
        insert(root, Dict[i]);

    char arr[] = {'e', 'o', 'b', 'a', 'm', 'g', 'l'} ;
    int N = sizeof(arr)/sizeof(arr[0]);

    PrintAllWords(arr, root, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all valid words that
// are possible using character of array
public class SearchDict_charArray {

    // Alphabet size
    static final int SIZE = 26;

    // trie Node
    static class TrieNode
    {
        TrieNode[] Child = new TrieNode[SIZE];

        // isLeaf is true if the node represents
        // end of a word
        boolean leaf;

        // Constructor
        public TrieNode() {
            leaf = false;
            for (int i =0 ; i< SIZE ; i++)
                    Child[i] = null;
        }
    }

    // If not present, inserts key into trie
    // If the key is prefix of trie node, just
    // marks leaf node
    static void insert(TrieNode root, String Key)
    {
        int n = Key.length();
        TrieNode pChild = root;

        for (int i=0; i<n; i++)
        {
            int index = Key.charAt(i) - 'a';

            if (pChild.Child[index] == null)
                pChild.Child[index] = new TrieNode();

            pChild = pChild.Child[index];
        }

        // make last node as leaf node
        pChild.leaf = true;
    }

    // A recursive function to print all possible valid
    // words present in array
    static void searchWord(TrieNode root, boolean Hash[],
                                            String str)
    {
        // if we found word in trie / dictionary
        if (root.leaf == true)
            System.out.println(str);

        // traverse all child's of current root
        for (int K =0; K < SIZE; K++)
        {
            if (Hash[K] == true && root.Child[K] != null )
            {
                // add current character
                char c = (char) (K + 'a');

                // Recursively search reaming character 
                // of word in trie
                searchWord(root.Child[K], Hash, str + c);
            }
        }
    }

    // Prints all words present in dictionary.
    static void PrintAllWords(char Arr[], TrieNode root, 
                                              int n)
    {
        // create a 'has' array that will store all 
        // present character in Arr[]
        boolean[] Hash = new boolean[SIZE];

        for (int i = 0 ; i < n; i++)
            Hash[Arr[i] - 'a'] = true;

        // tempary node
        TrieNode pChild = root ;

        // string to hold output words
        String str = "";

        // Traverse all matrix elements. There are only 
        // 26 character possible in char array
        for (int i = 0 ; i < SIZE ; i++)
        {
            // we start searching for word in dictionary
            // if we found a character which is child
            // of Trie root
            if (Hash[i] == true && pChild.Child[i] != null )
            {
                str = str+(char)(i + 'a');
                searchWord(pChild.Child[i], Hash, str);
                str = "";
            }
        }
    }

    //Driver program to test above function
    public static void main(String args[])
    {
        // Let the given dictionary be following
        String Dict[] = {"go", "bat", "me", "eat",
                           "goal", "boy", "run"} ;

        // Root Node of Trie
        TrieNode root = new TrieNode();

        // insert all words of dictionary into trie
        int n = Dict.length;
        for (int i=0; i<n; i++)
            insert(root, Dict[i]);

        char arr[] = {'e', 'o', 'b', 'a', 'm', 'g', 'l'} ;
        int N = arr.length;

        PrintAllWords(arr, root, N);
    }
}
// This code is contributed by Sumit Ghosh
```

## C#

```
// C# program to print all valid words that 
// are possible using character of array 
using System; 

public class SearchDict_charArray 
{ 

    // Alphabet size 
    static readonly int SIZE = 26; 

    // trie Node 
    public class TrieNode 
    { 
        public TrieNode[] Child = new TrieNode[SIZE]; 

        // isLeaf is true if the node represents 
        // end of a word 
        public Boolean leaf; 

        // Constructor 
        public TrieNode() 
        { 
            leaf = false; 
            for (int i =0 ; i< SIZE ; i++) 
                    Child[i] = null; 
        } 
    } 

    // If not present, inserts key into trie 
    // If the key is prefix of trie node, just 
    // marks leaf node 
    static void insert(TrieNode root, String Key) 
    { 
        int n = Key.Length; 
        TrieNode pChild = root; 

        for (int i = 0; i < n; i++) 
        { 
            int index = Key[i] - 'a'; 

            if (pChild.Child[index] == null) 
                pChild.Child[index] = new TrieNode(); 

            pChild = pChild.Child[index]; 
        } 

        // make last node as leaf node 
        pChild.leaf = true; 
    } 

    // A recursive function to print all possible valid 
    // words present in array 
    static void searchWord(TrieNode root, Boolean []Hash, 
                                            String str) 
    { 
        // if we found word in trie / dictionary 
        if (root.leaf == true) 
            Console.WriteLine(str); 

        // traverse all child's of current root 
        for (int K = 0; K < SIZE; K++) 
        { 
            if (Hash[K] == true && root.Child[K] != null ) 
            { 
                // add current character 
                char c = (char) (K + 'a'); 

                // Recursively search reaming character 
                // of word in trie 
                searchWord(root.Child[K], Hash, str + c); 
            } 
        } 
    } 

    // Prints all words present in dictionary. 
    static void PrintAllWords(char []Arr, TrieNode root, 
                                            int n) 
    { 
        // create a 'has' array that will store all 
        // present character in Arr[] 
        Boolean[] Hash = new Boolean[SIZE]; 

        for (int i = 0 ; i < n; i++) 
            Hash[Arr[i] - 'a'] = true; 

        // tempary node 
        TrieNode pChild = root ; 

        // string to hold output words 
        String str = ""; 

        // Traverse all matrix elements. There are only 
        // 26 character possible in char array 
        for (int i = 0 ; i < SIZE ; i++) 
        { 
            // we start searching for word in dictionary 
            // if we found a character which is child 
            // of Trie root 
            if (Hash[i] == true && pChild.Child[i] != null ) 
            { 
                str = str+(char)(i + 'a'); 
                searchWord(pChild.Child[i], Hash, str); 
                str = ""; 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String []args) 
    { 
        // Let the given dictionary be following 
        String []Dict = {"go", "bat", "me", "eat", 
                        "goal", "boy", "run"} ; 

        // Root Node of Trie 
        TrieNode root = new TrieNode(); 

        // insert all words of dictionary into trie 
        int n = Dict.Length; 
        for (int i = 0; i < n; i++) 
            insert(root, Dict[i]); 

        char []arr = {'e', 'o', 'b', 'a', 'm', 'g', 'l'} ; 
        int N = arr.Length; 

        PrintAllWords(arr, root, N); 
    } 
} 

/* This code is contributed by PrinciRaj1992 */
```

**Output:**

```
go
goal
me

```

本文由 **[尼尚·辛格](https://practice.geeksforgeeks.org/user-profile.php?user=_code)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。