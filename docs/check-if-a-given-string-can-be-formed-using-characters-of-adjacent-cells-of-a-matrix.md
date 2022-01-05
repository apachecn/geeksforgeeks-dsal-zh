# 检查给定的字符串是否可以用矩阵相邻单元格的字符构成

> 原文:[https://www . geeksforgeeks . org/check-如果给定字符串可以使用矩阵相邻单元格的字符来形成/](https://www.geeksforgeeks.org/check-if-a-given-string-can-be-formed-using-characters-of-adjacent-cells-of-a-matrix/)

给定一个字符矩阵**板**和一个字符串**单词**，任务是检查**单词**是否存在于仅由水平和垂直相邻字符序列构成的**板**上。每个字符只能使用一次。

**示例:**

> **输入:**
> 棋盘= {'A '，' B '，' C '，' E'}，{'S '，' F '，' C '，' S'}，{ ' A '，' D '，' E '，' E ' }
> Word = " SEE "
> T5】输出: True
> **说明:**“SEE”可以用(1，3)【S】、(2，3)【E】和(2，2)【E】的字符构成。
> 
> **输入:**
> board = { {'A '，' B '，' C '，' E'}，{'S '，' F '，' C '，' S'}，{'A '，' D '，' E '，' E ' }
> Word = " ABCB "
> T5】输出: False
> **说明:**“ABCB”不能用相邻字符不重复构成。

**方法:**解决这个问题的方法是遍历矩阵中的所有字符，找到单词第一个字符的出现。每当找到时，递归地检查其相邻的水平和垂直单元格中的下一个字符。重复这个过程，直到所有的字符都被一个一个找到。所有字符匹配的任何实例都表示找到了**单词**。如果没有这种情况发生，就找不到**字**。

下面是上述逻辑的实现:

## C++

```
// C++ Program to check if a given
// word can be formed from the
// adjacent characters in a matrix
// of characters

#include <bits/stdc++.h>
using namespace std;

// Function to check if the word exists
bool checkWord(vector<vector<char> >& board,
               string& word, int index,
               int row, int col)
{
    // If index exceeds board range
    if (row < 0 || col < 0
        || row >= board.size()
        || col >= board[0].size())
        return false;

    // If the current cell does not
    // contain the required character
    if (board[row][col] != word[index])
        return false;

    // If the cell contains the required
    // character and is the last character
    // of the word required to be matched
    else if (index == word.size() - 1)

        // Return true as word is found
        return true;

    char temp = board[row][col];

    // Mark cell visited
    board[row][col] = '*';

    // Check Adjacent cells
    // for the next character
    if (checkWord(board, word,
                  index + 1, row + 1, col)
        || checkWord(board, word,
                     index + 1, row - 1, col)
        || checkWord(board, word,
                     index + 1, row, col + 1)
        || checkWord(board, word,
                     index + 1, row, col - 1)) {

        board[row][col] = temp;

        return true;
    }

    // Restore cell value
    board[row][col] = temp;
    return false;
}

// Driver Code
int main()
{
    vector<vector<char> > board
        = { { 'A', 'B', 'C', 'E' },
            { 'S', 'F', 'C', 'S' },
            { 'A', 'D', 'E', 'E' } };
    string word = "CFDASABCESEE";

    for (int i = 0; i < board.size(); i++) {
        for (int j = 0; j < board[0].size(); j++) {

            if (board[i][j] == word[0]
                && checkWord(
                       board, word,
                       0, i, j)) {

                cout << "True" << '\n';
                return 0;
            }
        }
    }
    cout << "False" << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a given
// word can be formed from the
// adjacent characters in a matrix
// of characters
import java.util.*;
class GFG{

// Function to check if the word exists
static boolean checkWord(char [][]board,
                 String word, int index,
                       int row, int col)
{
    // If index exceeds board range
    if (row < 0 || col < 0 ||
        row >= board.length ||
        col >= board[0].length)
        return false;

    // If the current cell does not
    // contain the required character
    if (board[row][col] != word.charAt(index))
        return false;

    // If the cell contains the required
    // character and is the last character
    // of the word required to be matched
    else if (index == word.length() - 1)

        // Return true as word is found
        return true;

    char temp = board[row][col];

    // Mark cell visited
    board[row][col] = '*';

    // Check Adjacent cells
    // for the next character
    if (checkWord(board, word,
                  index + 1, row + 1, col) ||
        checkWord(board, word,
                  index + 1, row - 1, col) ||
        checkWord(board, word,
                  index + 1, row, col + 1) ||
        checkWord(board, word,
                  index + 1, row, col - 1))
    {
        board[row][col] = temp;

        return true;
    }

    // Restore cell value
    board[row][col] = temp;
    return false;
}

// Driver Code
public static void main(String[] args)
{
    char[][] board = { { 'A', 'B', 'C', 'E' },
                       { 'S', 'F', 'C', 'S' },
                       { 'A', 'D', 'E', 'E' } };
    String word = "CFDASABCESEE";

    for (int i = 0; i < board.length; i++)
    {
        for (int j = 0; j < board[0].length; j++)
        {
            if (board[i][j] == word.charAt(0) &&
                checkWord(board, word, 0, i, j))
            {
                System.out.println("True");
                return;
            }
        }
    }
    System.out.println("False");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 Program to check if a given
# word can be formed from the
# adjacent characters in a matrix
# of characters

# Function to check if
# the word exists
def checkWord(board, word,
              index, row, col):

    # If index exceeds board range
    if (row < 0 or col < 0 or
        row >= len(board) or
        col >= len(board[0])):
        return False

    # If the current cell does not
    # contain the required character
    if (board[row][col] != word[index]):
        return False

    # If the cell contains the required
    #character and is the last character
    # of the word required to be matched
    elif (index == len(word) - 1):

        # Return true as word is found
        return True

    temp = board[row][col]

    # Mark cell visited
    board[row][col] = '*'

    # Check Adjacent cells
    # for the next character
    if (checkWord(board, word,
                  index + 1,
                  row + 1, col) or
        checkWord(board, word,
                  index + 1,
                  row - 1, col) or
        checkWord(board, word,
                  index + 1,
                  row, col + 1) or
        checkWord(board, word,
                  index + 1,
                  row, col - 1)):
        board[row][col] = temp
        return True

    # Restore cell value
    board[row][col] = temp
    return False

# Driver Code
if __name__ == "__main__":

    board = [['A', 'B', 'C', 'E'],
            ['S', 'F', 'C', 'S'],
            ['A', 'D', 'E', 'E']]
    word = "CFDASABCESEE"
    f = 0

    for i in range (len(board)):
        for j in range (len(board[0])):
            if (board[i][j] == word[0] and
                checkWord(board, word,
                          0, i, j)):
                print ("True" )
                f = 1
                break
        if f == 1:
          break

    if f == 0:
       print ("False")

# This code is contributed by Chitranayal
```

## C#

```
// C# program to check if a given word
// can be formed from the adjacent
// characters in a matrix of characters
using System;

class GFG{

// Function to check if the word exists
static bool checkWord(char [,]board, String word,
                      int index, int row, int col)
{

    // If index exceeds board range
    if (row < 0 || col < 0 ||
        row >= board.GetLength(0) ||
        col >= board.GetLength(1))
        return false;

    // If the current cell does not
    // contain the required character
    if (board[row, col] != word[index])
        return false;

    // If the cell contains the required
    // character and is the last character
    // of the word required to be matched
    else if (index == word.Length - 1)

        // Return true as word is found
        return true;

    char temp = board[row, col];

    // Mark cell visited
    board[row, col] = '*';

    // Check adjacent cells
    // for the next character
    if (checkWord(board, word,
                  index + 1, row + 1, col) ||
        checkWord(board, word,
                  index + 1, row - 1, col) ||
        checkWord(board, word,
                  index + 1, row, col + 1) ||
        checkWord(board, word,
                  index + 1, row, col - 1))
    {
        board[row, col] = temp;

        return true;
    }

    // Restore cell value
    board[row, col] = temp;
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    char[,] board = { { 'A', 'B', 'C', 'E' },
                      { 'S', 'F', 'C', 'S' },
                      { 'A', 'D', 'E', 'E' } };
    String word = "CFDASABCESEE";

    for(int i = 0; i < board.GetLength(0); i++)
    {
       for(int j = 0; j < board.GetLength(1); j++)
       {
          if (board[i, j] == word[0] &&
              checkWord(board, word, 0, i, j))
          {
              Console.WriteLine("True");
              return;
          }
       }
    }
    Console.WriteLine("False");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to check if a given word
// can be formed from the adjacent
// characters in a matrix of characters

// Function to check if the word exists
function checkWord(board, word, index, row, col)
{

    // If index exceeds board range
    if (row < 0 || col < 0 ||
        row >= board.length ||
        col >= board[0].length)
        return false;

    // If the current cell does not
    // contain the required character
    if (board[row][col] !== word[index])
        return false;

    // If the cell contains the required
    // character and is the last character
    // of the word required to be matched
    else if (index === word.length - 1)

        // Return true as word is found
        return true;

    var temp = board[row][col];

    // Mark cell visited
    board[row][col] = "*";

    // Check adjacent cells
    // for the next character
    if (checkWord(board, word,
                  index + 1, row + 1, col) ||
        checkWord(board, word,
                  index + 1, row - 1, col) ||
        checkWord(board, word,
                  index + 1, row, col + 1) ||
        checkWord(board, word,
                  index + 1, row, col - 1))
    {
        board[row][col] = temp;
        return true;
    }

    // Restore cell value
    board[row][col] = temp;
    return false;
}

// Driver Code
var board = [ [ "A", "B", "C", "E" ],
              [ "S", "F", "C", "S" ],
              [ "A", "D", "E", "E" ],];
var word = "CFDASABCESEE";
var f = 0;

for(var i = 0; i < board.length; i++)
{
    for(var j = 0; j < board[0].length; j++)
    {
        if (board[i][j] === word[0] &&
            checkWord(board, word, 0, i, j))
        {
            document.write("True");
            f = 1;
        }
    }
    if (f === 1)
    {
        i = board.length + 1;
    }
}
if (f === 0)
{
    document.write("False");
}

// This code is contributed by rdtank

</script>
```

**Output:** 

```
True
```