# Boggle（在一个字符板上查找所有可能的单词）| 设置 1

> 原文： [https://www.geeksforgeeks.org/boggle-find-possible-words-board-characters/](https://www.geeksforgeeks.org/boggle-find-possible-words-board-characters/)

给定字典，这是一种在字典中进行查找的方法以及一个 M x N 板，其中每个单元格都有一个字符。 查找可以由一系列相邻字符组成的所有可能单词。 请注意，我们可以移至 8 个相邻字符中的任何一个，但一个单词不应包含同一单元格的多个实例。

**示例**：

```
Input: dictionary[] = {"GEEKS", "FOR", "QUIZ", "GO"};
       boggle[][]   = {{'G', 'I', 'Z'},
                       {'U', 'E', 'K'},
                       {'Q', 'S', 'E'}};
      isWord(str): returns true if str is present in dictionary
                   else false.

Output:  Following words of dictionary are present
         GEEKS
         QUIZ
```

![Boggle](img/2567bb295383f5356055b2b394dc6675.png)

### [我们强烈建议您单击此处并进行实践，然后再继续解决方案。](https://practice.geeksforgeeks.org/problem-page.php?pid=1653)

想法是将每个字符都视为起始字符，并找到所有以此字符开头的单词。 可以使用[深度优先遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)找到所有字符开头的单词。 我们从每个像元开始进行深度优先遍历。 我们会跟踪访问过的单元格，以确保一个单词只被考虑一次。

## C++

```cpp

// C++ program for Boggle game 
#include <cstring> 
#include <iostream> 
using namespace std; 

#define M 3 
#define N 3 

// Let the given dictionary be following 
string dictionary[] = { "GEEKS", "FOR", "QUIZ", "GO" }; 
int n = sizeof(dictionary) / sizeof(dictionary[0]); 

// A given function to check if a given string is present in 
// dictionary. The implementation is naive for simplicity. As 
// per the question dictionary is given to us. 
bool isWord(string& str) 
{ 
    // Linearly search all words 
    for (int i = 0; i < n; i++) 
        if (str.compare(dictionary[i]) == 0) 
            return true; 
    return false; 
} 

// A recursive function to print all words present on boggle 
void findWordsUtil(char boggle[M][N], bool visited[M][N], int i, 
                   int j, string& str) 
{ 
    // Mark current cell as visited and append current character 
    // to str 
    visited[i][j] = true; 
    str = str + boggle[i][j]; 

    // If str is present in dictionary, then print it 
    if (isWord(str)) 
        cout << str << endl; 

    // Traverse 8 adjacent cells of boggle[i][j] 
    for (int row = i - 1; row <= i + 1 && row < M; row++) 
        for (int col = j - 1; col <= j + 1 && col < N; col++) 
            if (row >= 0 && col >= 0 && !visited[row][col]) 
                findWordsUtil(boggle, visited, row, col, str); 

    // Erase current character from string and mark visited 
    // of current cell as false 
    str.erase(str.length() - 1); 
    visited[i][j] = false; 
} 

// Prints all words present in dictionary. 
void findWords(char boggle[M][N]) 
{ 
    // Mark all characters as not visited 
    bool visited[M][N] = { { false } }; 

    // Initialize current string 
    string str = ""; 

    // Consider every character and look for all words 
    // starting with this character 
    for (int i = 0; i < M; i++) 
        for (int j = 0; j < N; j++) 
            findWordsUtil(boggle, visited, i, j, str); 
} 

// Driver program to test above function 
int main() 
{ 
    char boggle[M][N] = { { 'G', 'I', 'Z' }, 
                          { 'U', 'E', 'K' }, 
                          { 'Q', 'S', 'E' } }; 

    cout << "Following words of dictionary are present\n"; 
    findWords(boggle); 
    return 0; 
} 

```

## Java

```java

// Java program for Boggle game 
class GFG { 
    // Let the given dictionary be following 
    static final String dictionary[] = { "GEEKS", "FOR", "QUIZ", "GUQ", "EE" }; 
    static final int n = dictionary.length; 
    static final int M = 3, N = 3; 

    // A given function to check if a given string is present in 
    // dictionary. The implementation is naive for simplicity. As 
    // per the question dictionary is given to us. 
    static boolean isWord(String str) 
    { 
        // Linearly search all words 
        for (int i = 0; i < n; i++) 
            if (str.equals(dictionary[i])) 
                return true; 
        return false; 
    } 

    // A recursive function to print all words present on boggle 
    static void findWordsUtil(char boggle[][], boolean visited[][], int i, 
                              int j, String str) 
    { 
        // Mark current cell as visited and append current character 
        // to str 
        visited[i][j] = true; 
        str = str + boggle[i][j]; 

        // If str is present in dictionary, then print it 
        if (isWord(str)) 
            System.out.println(str); 

        // Traverse 8 adjacent cells of boggle[i][j] 
        for (int row = i - 1; row <= i + 1 && row < M; row++) 
            for (int col = j - 1; col <= j + 1 && col < N; col++) 
                if (row >= 0 && col >= 0 && !visited[row][col]) 
                    findWordsUtil(boggle, visited, row, col, str); 

        // Erase current character from string and mark visited 
        // of current cell as false 
        str = "" + str.charAt(str.length() - 1); 
        visited[i][j] = false; 
    } 

    // Prints all words present in dictionary. 
    static void findWords(char boggle[][]) 
    { 
        // Mark all characters as not visited 
        boolean visited[][] = new boolean[M][N]; 

        // Initialize current string 
        String str = ""; 

        // Consider every character and look for all words 
        // starting with this character 
        for (int i = 0; i < M; i++) 
            for (int j = 0; j < N; j++) 
                findWordsUtil(boggle, visited, i, j, str); 
    } 

    // Driver program to test above function 
    public static void main(String args[]) 
    { 
        char boggle[][] = { { 'G', 'I', 'Z' }, 
                            { 'U', 'E', 'K' }, 
                            { 'Q', 'S', 'E' } }; 

        System.out.println("Following words of dictionary are present"); 
        findWords(boggle); 
    } 
} 

```

## C#

```cs

// C# program for Boggle game 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    // Let the given dictionary be following 
    static readonly String []dictionary = { "GEEKS", "FOR",  
                                            "QUIZ", "GUQ", "EE" }; 
    static readonly int n = dictionary.Length; 
    static readonly int M = 3, N = 3; 

    // A given function to check if a given string  
    // is present in dictionary. The implementation is  
    // naive for simplicity. As per the question  
    // dictionary is given to us. 
    static bool isWord(String str) 
    { 
        // Linearly search all words 
        for (int i = 0; i < n; i++) 
            if (str.Equals(dictionary[i])) 
                return true; 
        return false; 
    } 

    // A recursive function to print all words present on boggle 
    static void findWordsUtil(char [,]boggle, bool [,]visited,  
                              int i, int j, String str) 
    { 
        // Mark current cell as visited and 
        // append current character to str 
        visited[i, j] = true; 
        str = str + boggle[i, j]; 

        // If str is present in dictionary, 
        // then print it 
        if (isWord(str)) 
            Console.WriteLine(str); 

        // Traverse 8 adjacent cells of boggle[i,j] 
        for (int row = i - 1; row <= i + 1 && row < M; row++) 
            for (int col = j - 1; col <= j + 1 && col < N; col++) 
                if (row >= 0 && col >= 0 && !visited[row, col]) 
                    findWordsUtil(boggle, visited, row, col, str); 

        // Erase current character from string and  
        // mark visited of current cell as false 
        str = "" + str[str.Length - 1]; 
        visited[i, j] = false; 
    } 

    // Prints all words present in dictionary. 
    static void findWords(char [,]boggle) 
    { 
        // Mark all characters as not visited 
        bool [,]visited = new bool[M, N]; 

        // Initialize current string 
        String str = ""; 

        // Consider every character and look for all words 
        // starting with this character 
        for (int i = 0; i < M; i++) 
            for (int j = 0; j < N; j++) 
                findWordsUtil(boggle, visited, i, j, str); 
    } 

    // Driver Code 
    public static void Main(String []args) 
    { 
        char [,]boggle = { { 'G', 'I', 'Z' }, 
                           { 'U', 'E', 'K' }, 
                           { 'Q', 'S', 'E' } }; 

        Console.WriteLine("Following words of " +   
                          "dictionary are present"); 
        findWords(boggle); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

请注意，上述解决方案可能会多次打印相同的单词。 例如，如果我们在字典中添加“ SEEK”，则会多次打印。 为了避免这种情况，我们可以使用散列来跟踪所有打印的单词。

在下面的第二组中，我们讨论了基于 Trie 的优化解决方案：

[**第 2 组（使用 Trie）**](https://www.geeksforgeeks.org/boggle-set-2-using-trie/)

本文由 **Rishabh** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

