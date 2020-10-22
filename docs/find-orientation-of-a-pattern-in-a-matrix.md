# 查找矩阵中模式的方向

> 原文： [https://www.geeksforgeeks.org/find-orientation-of-a-pattern-in-a-matrix/](https://www.geeksforgeeks.org/find-orientation-of-a-pattern-in-a-matrix/)

给定一个字符矩阵和一个模式，请在矩阵中找到模式的方向。 换句话说，找出图案是在水平方向还是垂直方向上出现在矩阵中。 在尽可能短的时间内实现这一目标。

```
Input:
mat[N][N] = { {'a', 'b', 'c', 'd', 'e'},
              {'f', 'g', 'h', 'i', 'j'},
              {'k', 'l', 'm', 'n', 'o'},
              {'p', 'q', 'r', 's', 't'},
              {'u', 'v', 'w', 'x', 'y'}};
pattern = "pqrs";

Output: Horizontal
```

**我们强烈建议您最小化浏览器，然后自己尝试。**

一个简单的解决方案是针对每一行和每一列，使用[朴素模式搜索算法](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)查找矩阵中模式的方向。 每行的朴素模式搜索算法的时间复杂度为`O(NM)`，其中`N`是矩阵的大小，`M`是模式的长度。 因此，此解决方案的时间复杂度将为`O(N * (NM))`，因为`N`行和`N`列中的每一个都需要`O(NM)`时间。

**我们可以做得更好吗？**

这个想法是针对每一行和每一列使用 [KMP 模式匹配算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)。 KMP 匹配算法将最坏情况改善为`O(N + M)`。 KMP 搜索的总成本与字符串和模式的字符数成线性关系。 对于`N x N`矩阵和长度为`M`的模式，此解决方案的复杂度将为`O(N * (N + M))`，因为`N`行和`N`列中的每一个都将为`O(N + M)`时间。

## C++ 

```cpp

// C++ program for finding orientation of the pattern  
// using KMP pattern searching algorithm  
#include<bits/stdc++.h> 
using namespace std; 
#define N 5  

// Used in KMP Search for preprocessing the pattern  
void computeLPSArray(char *pat, int M, int *lps)  
{  
    // length of the previous longest prefix suffix  
    int len = 0;  
    int i = 1;  

    lps[0] = 0; // lps[0] is always 0  

    // the loop calculates lps[i] for i = 1 to M-1  
    while (i < M)  
    {  
        if (pat[i] == pat[len])  
        {  
            len++;  
            lps[i++] = len;  
        }  
        else // (pat[i] != pat[len])  
        {  
            if (len != 0)  
            {  
                // This is tricky. Consider the example  
                // AAACAAAA and i = 7.  
                len = lps[len - 1];  

                // Also, note that we do not increment i here  
            }  
            else // if (len == 0)  
            {  
                lps[i++] = 0;  
            }  
        }  
    }  
}  

int KMPSearch(char *pat, char *txt)  
{  
    int M = strlen(pat);  

    // create lps[] that will hold the longest  
    // prefix suffix values for pattern  
    int *lps = (int *)malloc(sizeof(int)*M);  
    int j = 0; // index for pat[]  

    // Preprocess the pattern (calculate lps[] array)  
    computeLPSArray(pat, M, lps);  

    int i = 0; // index for txt[]  
    while (i < N)  
    {  
        if (pat[j] == txt[i])  
        {  
            j++;  
            i++;  
        }  
        if (j == M)  
        {  
            // return 1 is pattern is found  
            return 1;  
        }  

        // mismatch after j matches  
        else if (i < N && pat[j] != txt[i])  
        {  
            // Do not match lps[0..lps[j-1]] characters,  
            // they will match anyway  
            if (j != 0)  
                j = lps[j - 1];  
            else
                i = i + 1;  
        }  
    }  
    free(lps); // to avoid memory leak  

    // return 0 is pattern is not found  
    return 0;  
}  

// Function to find orientation of pattern in the matrix  
// It uses KMP pattern searching algorithm  
void findOrientation(char mat[][N], char *pat)  
{  
    // allocate memory for string contaning cols  
    char *col = (char*) malloc(N);  

    for (int i = 0; i < N; i++)  
    {  
        // search in row i  
        if (KMPSearch(pat, mat[i]))  
        {  
            cout << "Horizontal" << endl; 
            return;  
        }  

        // Construct an array to store i'th column  
        for (int j = 0; j < N; j++)  
            col[j] = *(mat[j] + i);  

        // Search in column i  
        if (KMPSearch(pat, col))  
            cout << "Vertical" << endl;  
    }  

    // to avoid memory leak  
    free(col);  
}  

// Driver Code 
int main()  
{  
    char mat[N][N] = {{'a', 'b', 'c', 'd', 'e'},  
                      {'f', 'g', 'h', 'i', 'j'},  
                       {'k', 'l', 'm', 'n', 'o'},  
                      {'p', 'q', 'r', 's', 't'},  
                      {'u', 'v', 'w', 'x', 'y'}};  
    char pat[] = "pqrs";  

    findOrientation(mat, pat);  

    return 0;  
}  

// This code is contributed by kumar65 

```

## C

```c
// C program for finding orientation of the pattern 
// using KMP pattern searching algorithm 
#include<stdio.h> 
#include<string.h> 
#include<stdlib.h> 
#define N 5 
  
// Used in KMP Search for preprocessing the pattern 
void computeLPSArray(char *pat, int M, int *lps) 
{ 
    // length of the previous longest prefix suffix 
    int len = 0; 
    int i = 1; 
  
    lps[0] = 0; // lps[0] is always 0 
  
    // the loop calculates lps[i] for i = 1 to M-1 
    while (i < M) 
    { 
        if (pat[i] == pat[len]) 
        { 
            len++; 
            lps[i++] = len; 
        } 
        else // (pat[i] != pat[len]) 
        { 
            if (len != 0) 
            { 
                // This is tricky. Consider the example 
                // AAACAAAA and i = 7. 
                len = lps[len-1]; 
  
                // Also, note that we do not increment i here 
            } 
            else // if (len == 0) 
            { 
                lps[i++] = 0; 
            } 
        } 
    } 
} 
  
int KMPSearch(char *pat, char *txt) 
{ 
    int M = strlen(pat); 
  
    // create lps[] that will hold the longest prefix suffix 
    // values for pattern 
    int *lps = (int *)malloc(sizeof(int)*M); 
    int j = 0; // index for pat[] 
  
    // Preprocess the pattern (calculate lps[] array) 
    computeLPSArray(pat, M, lps); 
  
    int i = 0; // index for txt[] 
    while (i < N) 
    { 
        if (pat[j] == txt[i]) 
        { 
            j++; 
            i++; 
        } 
        if (j == M) 
        { 
            // return 1 is pattern is found 
            return 1; 
        } 
        // mismatch after j matches 
        else if (i < N && pat[j] != txt[i]) 
        { 
            // Do not match lps[0..lps[j-1]] characters, 
            // they will match anyway 
            if (j != 0) 
                j = lps[j-1]; 
            else
                i = i+1; 
        } 
    } 
    free(lps); // to avoid memory leak 
    // return 0 is pattern is not found 
    return 0; 
} 
  
// Function to find orientation of pattern in the matrix 
// It uses KMP pattern searching algorithm 
void findOrientation(char mat[][N], char *pat) 
{ 
    // allocate memory for string contaning cols 
    char *col = (char*) malloc(N); 
  
    for (int i = 0; i < N; i++) 
    { 
        // search in row i 
        if (KMPSearch(pat, mat[i])) 
        { 
            printf("Horizontal\n"); 
            return; 
        } 
  
        // Construct an array to store i'th column 
        for (int j = 0; j < N; j++) 
            col[j] = *(mat[j] + i); 
  
        // Search in column i 
        if (KMPSearch(pat, col)) 
            printf("Vertical\n"); 
    } 
  
    // to avoid memory leak 
    free(col); 
} 
  
// Driver program to test above function 
int main() 
{ 
    char mat[N][N] = 
    { 
        {'a', 'b', 'c', 'd', 'e'}, 
        {'f', 'g', 'h', 'i', 'j'}, 
        {'k', 'l', 'm', 'n', 'o'}, 
        {'p', 'q', 'r', 's', 't'}, 
        {'u', 'v', 'w', 'x', 'y'} 
  
    }; 
    char pat[] = "pqrs"; 
  
    findOrientation(mat, pat); 
  
    return 0; 
}
```

## Python

```py
# Python3 program for finding orientation of the pattern 
# using KMP pattern searching algorithm 
N = 5
  
# Used in KMP Search for preprocessing the pattern 
def computeLPSArray(pat, M, lps): 
      
    # lenlgth of the previous longest prefix suffix 
    lenl = 0
    i = 1
  
    lps[0] = 0 # lps[0] is always 0 
  
    # the loop calculates lps[i] for i = 1 to M-1 
    while (i < M): 
        if (pat[i] == pat[lenl]): 
            lenl += 1
            lps[i] = lenl 
            i += 1
        else: # (pat[i] != pat[lenl]) 
            if (lenl != 0) : 
                  
                # This is tricky. Consider the example 
                # AAACAAAA and i = 7. 
                lenl = lps[lenl - 1] 
  
                # Also, note that we do not increment i here 
              
            # if (lenl == 0) 
            else: 
                lps[i] = 0
                i += 1
  
def KMPSearch(pat, txt): 
    M = len(pat) 
  
    # create lps[] that will hold the longest 
    # prefix suffix values for pattern 
    lps = [0] * M 
    j = 0 # index for pat[] 
  
    # Preprocess the pattern (calculate lps[] array) 
    computeLPSArray(pat, M, lps) 
  
    # index for txt[] 
    i = 0 
    while (i < N): 
        if (pat[j] == txt[i]): 
            j += 1
            i += 1
        if (j == M): 
              
            # return 1 is pattern is found 
            return 1
  
        # mismatch after j matches 
        elif (i < N and pat[j] != txt[i]): 
              
            # Do not match lps[0..lps[j-1]] characters, 
            # they will match anyway 
            if (j != 0): 
                j = lps[j - 1] 
            else: 
                i = i + 1
  
    # to amemory leak 
  
    # return 0 is pattern is not found 
    return 0
  
# Function to find orientation of pattern in the matrix 
# It uses KMP pattern searching algorithm 
def findOrientation(mat, pat): 
      
    # allocate memory for string contaning cols 
    col = ['a'] * (N) 
  
    for i in range(N): 
          
        # search in row i 
        if (KMPSearch(pat, mat[i])): 
            print("Horizontal") 
            return
  
        # Construct an array to store i'th column 
        for j in range(N): 
            col[j] = mat[j][i] 
  
        # Search in column i 
        if (KMPSearch(pat, col)): 
            print("Vertical") 
  
# Driver Code 
mat=[['a', 'b', 'c', 'd', 'e'], 
    ['f', 'g', 'h', 'i', 'j'], 
    ['k', 'l', 'm', 'n', 'o'], 
    ['p', 'q', 'r', 's', 't'], 
    ['u', 'v', 'w', 'x', 'y']] 
pat= "pqrs"
  
findOrientation(mat, pat) 
  
# This code is contributed by Mohit kumar 29
```

输出：

```
Horizontal
```

