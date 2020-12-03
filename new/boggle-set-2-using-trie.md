# Boggle | 系列 2（使用 Trie）

> 原文： [https://www.geeksforgeeks.org/boggle-set-2-using-trie/](https://www.geeksforgeeks.org/boggle-set-2-using-trie/)

给定字典，这是一种在字典和 M x N 板中进行查询的方法，其中每个单元格都有一个字符。 查找可以由一系列相邻字符组成的所有可能单词。 请注意，我们可以移至 8 个相邻字符中的任何一个，但一个单词不应包含同一单元格的多个实例。

**示例**：

```
Input: dictionary[] = {"GEEKS", "FOR", "QUIZ", "GO"};
       boggle[][]   = {{'G', 'I', 'Z'},
                       {'U', 'E', 'K'},
                       {'Q', 'S', 'E'}};

Output: Following words of the dictionary are present
         GEEKS
         QUIZ

Explanation:

Input: dictionary[] = {"GEEKS", "ABCFIHGDE"};
       boggle[][]   = {{'A', 'B', 'C'},
                       {'D', 'E', 'F'},
                       {'G', 'H', 'I'}};
Output: Following words of the dictionary are present
         ABCFIHGDE
Explanation:

```

我们在下面的文章中讨论了基于 Graph DFS 的解决方案。

[Boggle（在一个字符板上查找所有可能的单词） | 系列 1](https://www.geeksforgeeks.org/boggle-find-possible-words-board-characters/)

在这里，我们讨论基于 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 的解决方案，它比基于 DFS 的解决方案更好。

给定字典 dictionary [] = {“ GEEKS”，“ FOR”，“ QUIZ”，“ GO”}

1.创建一个空的 trie，并将给定字典的所有单词插入 trie

```
After insertion, Trie looks like(leaf nodes are in RED)
                       root
                    /       
                    G   F     Q
                 /  |   |     |
                O   E   O     U
                    |   |     |
                    E    R     I
                    |         |  
                    K         Z 
                    |   
                    S   

```

2.之后，我们仅在 boggle [] []中选择那些是 Trie

根节点的字符。让我们在上面选择'G'boggle [0] [0]，'Q'boggle [2] [ 0]（它们都存在于 boggle 矩阵中）

3.在 trie 中搜索一个单词，该单词以我们在步骤 2 中选择的字符开头

```
1) Create bool visited boolean matrix (Visited[M][N] = false )
2) Call SearchWord() for every cell (i, j) which has one of the
   first characters of dictionary words. In above example,
   we have 'G' and 'Q' as first characters.

SearchWord(Trie *root, i, j, visited[][N])
if root->leaf == true 
   print word 

if we have seen this element first time then make it visited.
   visited[i][j] = true
   do
      traverse all child of current root 
      k goes (0 to 26 ) [there are only 26 Alphabet] 
      add current char and search for next character 

      find next character which is adjacent to boggle[i][j]
      they are 8 adjacent cells of boggle[i][j] (i+1, j+1), 
      (i+1, j) (i-1, j) and so on.

   make it unvisited visited[i][j] = false 

```

以下是上述想法的实现：

## C++

```cpp

// C++ program for Boggle game 
#include <bits/stdc++.h> 
using namespace std; 

// Converts key current character into index 
// use only 'A' through 'Z' 
#define char_int(c) ((int)c - (int)'A') 

// Alphabet size 
#define SIZE (26) 

#define M 3 
#define N 3 

// trie Node 
struct TrieNode { 
    TrieNode* Child[SIZE]; 

    // isLeaf is true if the node represents 
    // end of a word 
    bool leaf; 
}; 

// Returns new trie node (initialized to NULLs) 
TrieNode* getNode() 
{ 
    TrieNode* newNode = new TrieNode; 
    newNode->leaf = false; 
    for (int i = 0; i < SIZE; i++) 
        newNode->Child[i] = NULL; 
    return newNode; 
} 

// If not present, inserts a key into the trie 
// If the key is a prefix of trie node, just 
// marks leaf node 
void insert(TrieNode* root, char* Key) 
{ 
    int n = strlen(Key); 
    TrieNode* pChild = root; 

    for (int i = 0; i < n; i++) { 
        int index = char_int(Key[i]); 

        if (pChild->Child[index] == NULL) 
            pChild->Child[index] = getNode(); 

        pChild = pChild->Child[index]; 
    } 

    // make last node as leaf node 
    pChild->leaf = true; 
} 

// function to check that current location 
// (i and j) is in matrix range 
bool isSafe(int i, int j, bool visited[M][N]) 
{ 
    return (i >= 0 && i < M && j >= 0 && j < N && !visited[i][j]); 
} 

// A recursive function to print all words present on boggle 
void searchWord(TrieNode* root, char boggle[M][N], int i, 
                int j, bool visited[][N], string str) 
{ 
    // if we found word in trie / dictionary 
    if (root->leaf == true) 
        cout << str << endl; 

    // If both I and j in  range and we visited 
    // that element of matrix first time 
    if (isSafe(i, j, visited)) { 
        // make it visited 
        visited[i][j] = true; 

        // traverse all childs of current root 
        for (int K = 0; K < SIZE; K++) { 
            if (root->Child[K] != NULL) { 
                // current character 
                char ch = (char)K + (char)'A'; 

                // Recursively search reaming character of word 
                // in trie for all 8 adjacent cells of boggle[i][j] 
                if (isSafe(i + 1, j + 1, visited) 
                    && boggle[i + 1][j + 1] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i + 1, j + 1, visited, str + ch); 
                if (isSafe(i, j + 1, visited) 
                    && boggle[i][j + 1] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i, j + 1, visited, str + ch); 
                if (isSafe(i - 1, j + 1, visited) 
                    && boggle[i - 1][j + 1] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i - 1, j + 1, visited, str + ch); 
                if (isSafe(i + 1, j, visited) 
                    && boggle[i + 1][j] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i + 1, j, visited, str + ch); 
                if (isSafe(i + 1, j - 1, visited) 
                    && boggle[i + 1][j - 1] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i + 1, j - 1, visited, str + ch); 
                if (isSafe(i, j - 1, visited) 
                    && boggle[i][j - 1] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i, j - 1, visited, str + ch); 
                if (isSafe(i - 1, j - 1, visited) 
                    && boggle[i - 1][j - 1] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i - 1, j - 1, visited, str + ch); 
                if (isSafe(i - 1, j, visited) 
                    && boggle[i - 1][j] == ch) 
                    searchWord(root->Child[K], boggle, 
                               i - 1, j, visited, str + ch); 
            } 
        } 

        // make current element unvisited 
        visited[i][j] = false; 
    } 
} 

// Prints all words present in dictionary. 
void findWords(char boggle[M][N], TrieNode* root) 
{ 
    // Mark all characters as not visited 
    bool visited[M][N]; 
    memset(visited, false, sizeof(visited)); 

    TrieNode* pChild = root; 

    string str = ""; 

    // traverse all matrix elements 
    for (int i = 0; i < M; i++) { 
        for (int j = 0; j < N; j++) { 
            // we start searching for word in dictionary 
            // if we found a character which is child 
            // of Trie root 
            if (pChild->Child[char_int(boggle[i][j])]) { 
                str = str + boggle[i][j]; 
                searchWord(pChild->Child[char_int(boggle[i][j])], 
                           boggle, i, j, visited, str); 
                str = ""; 
            } 
        } 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    // Let the given dictionary be following 
    char* dictionary[] = { "GEEKS", "FOR", "QUIZ", "GEE" }; 

    // root Node of trie 
    TrieNode* root = getNode(); 

    // insert all words of dictionary into trie 
    int n = sizeof(dictionary) / sizeof(dictionary[0]); 
    for (int i = 0; i < n; i++) 
        insert(root, dictionary[i]); 

    char boggle[M][N] = { { 'G', 'I', 'Z' }, 
                          { 'U', 'E', 'K' }, 
                          { 'Q', 'S', 'E' } }; 

    findWords(boggle, root); 

    return 0; 
} 

```