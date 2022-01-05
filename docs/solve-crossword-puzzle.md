# 解字谜

> 原文:[https://www.geeksforgeeks.org/solve-crossword-puzzle/](https://www.geeksforgeeks.org/solve-crossword-puzzle/)

提供了一个 **10 x 10 的纵横字谜网格**，以及一组需要填入网格的单词(或地名)。网格中的单元最初是 **+** 标志或**–**标志。标有**'+**的单元格必须保持**原样。标有 **'-'** 的单元格需要用适当的字符填充**。
还会给你一组需要填纵横字谜格子的单词。****

**示例:**

```
Input :
+++++++++-
-++++++++-
-------++-
-++++++++-
-++++++++-
-++++-----
------+++-
-++++++++-
+---------
++++++++++

Output :
+++++++++C
P++++++++H
HISTORY++E
Y++++++++M
S++++++++I
I++++MATHS
CIVICS+++T
S++++++++R
+GEOGRAPHY
++++++++++ 
```

**这背后的方法是递归地检查垂直位置和水平位置的每个单词。然后将矩阵中最适合的单词填充到网格的相应位置，然后通过用该单词填充间隙来更新纵横字谜网格。**

```
// CPP code to fill the crossword puzzle
#include <bits/stdc++.h>
using namespace std;

// ways are to calculate the number of
// possible ways to fill the grid
int ways = 0;

// this function is used to print
// the resultant matrix
void printMatrix(vector<string>& matrix, int n)
{
    for (int i = 0; i < n; i++)
        cout << matrix[i] << endl;
}

// this function checks for the current word
// if it can be placed horizontally or not
// x -> it represent index of row
// y -> it represent index of column
// currentWord -> it represent the
// current word in word array
vector<string> checkHorizontal(int x, int y,
                               vector<string> matrix,
                               string currentWord)
{
    int n = currentWord.length();

    for (int i = 0; i < n; i++) {
        if (matrix[x][y + i] == '#' || 
            matrix[x][y + i] == currentWord[i]) {
            matrix[x][y + i] = currentWord[i];
        }
        else {

            // this shows that word cannot 
            // be placed horizontally
            matrix[0][0] = '@';
            return matrix;
        }
    }

    return matrix;
}

// this function checks for the current word
// if it can be placed vertically or not
// x -> it represent index of row
// y -> it represent index of column
// currentWord -> it represent the
// current word in word array
vector<string> checkVertical(int x, int y,
                             vector<string> matrix,
                             string currentWord)
{
    int n = currentWord.length();

    for (int i = 0; i < n; i++) {
        if (matrix[x + i][y] == '#' || 
            matrix[x + i][y] == currentWord[i]) {
            matrix[x + i][y] = currentWord[i];
        }
        else {

            // this shows that word
            // cannot be placed vertically
            matrix[0][0] = '@';
            return matrix;
        }
    }
    return matrix;
}

// this function recursively checks for every
// word that can align vertically in one loop
// and in another loop it checks for those words
// that can align horizontally words -> it
// contains all the words to fill in a crossword
// puzzle matrix -> it contain the current
// state of crossword index -> it represent
// the index of current word n -> it represent
// the length of row or column of the square matrix
void solvePuzzle(vector<string>& words,
                 vector<string> matrix,
                 int index, int n)
{
    if (index < words.size()) {
        string currentWord = words[index];
        int maxLen = n - currentWord.length();

        // loop to check the words that can align vertically.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= maxLen; j++) {
                vector<string> temp = checkVertical(j, i,
                                        matrix, currentWord);

                if (temp[0][0] != '@') {
                    solvePuzzle(words, temp, index + 1, n);
                }
            }
        }

        // loop to check the words that can align horizontally.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= maxLen; j++) {
                vector<string> temp = checkHorizontal(i, j,
                                      matrix, currentWord);

                if (temp[0][0] != '@') {
                    solvePuzzle(words, temp, index + 1, n);
                }
            }
        }
    }
    else {
        // calling of print function to
        // print the crossword puzzle
        cout << (ways + 1) << " way to solve the puzzle "
             << endl;
        printMatrix(matrix, n);
        cout << endl;

        // increase the ways
        ways++;
        return;
    }
}

// Driver Code
int main()
{
    // length of grid
    int n1 = 10;

    // matrix to hold the grid of puzzle
    vector<string> matrix;

    // take input of puzzle in matrix
    // input of grid of size n1 x n1
    matrix.push_back("*#********");
    matrix.push_back("*#********");
    matrix.push_back("*#****#***");
    matrix.push_back("*##***##**");
    matrix.push_back("*#****#***");
    matrix.push_back("*#****#***");
    matrix.push_back("*#****#***");
    matrix.push_back("*#*######*");
    matrix.push_back("*#********");
    matrix.push_back("***#######");

    vector<string> words;

    // the words matrix will hold all
    // the words need to be filled in the grid
    words.push_back("PUNJAB");
    words.push_back("JHARKHAND");
    words.push_back("MIZORAM");
    words.push_back("MUMBAI");

    // initialize the number of ways
    // to solve the puzzle to zero
    ways = 0;

    // recursive function to solve the puzzle
    // Here 0 is the initial index of words array
    // n1 is length of grid
    solvePuzzle(words, matrix, 0, n1);
    cout << "Number of ways to fill the grid is "
         << ways << endl;

    return 0;
}
```

****Output:**

```
1 way to solve the puzzle 
*J********
*H********
*A****P***
*R#***U#**
*K****N***
*H****J***
*A****A***
*N*MUMBAI*
*D********
***MIZORAM

Number of ways to fill the grid is 1

```**