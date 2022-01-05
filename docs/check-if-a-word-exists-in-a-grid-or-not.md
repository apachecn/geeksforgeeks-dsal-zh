# 检查网格中是否有单词

> 原文:[https://www . geesforgeks . org/check-if-a-word-in-a-grid-or-not/](https://www.geeksforgeeks.org/check-if-a-word-exists-in-a-grid-or-not/)

给定一个由字符和单词组成的 2D 网格，任务是检查该单词是否存在于网格中。一个单词可以在 4 个方向上任意匹配。
4 个方向为，水平左右，垂直上下。
**例:**

```
Input:  grid[][] = {"axmy",
                    "bgdf",
                    "xeet",
                    "raks"};
Output: Yes

a x m y
b g d f
x e e t
r a k s

Input: grid[][] = {"axmy",
                   "brdf",
                   "xeet",
                   "rass"};
Output : No
```

**来源:** [微软采访](https://www.geeksforgeeks.org/microsoft-interview-experience-set-131/)

**方法:**这里使用的思想在下面的步骤中描述:

*   检查每个单元格，如果该单元格有第一个字符，则逐个重复，并尝试该单元格的所有 4 个方向进行匹配。
*   将网格中的位置标记为已访问，并在 4 个可能的方向上重复出现。
*   重复后，再次将该位置标记为未访问。
*   一旦单词中的所有字母都匹配，返回 true。

以下是上述方法的实现:

## C++

```
// C++ program to check if the word
// exists in the grid or not
#include <bits/stdc++.h>
using namespace std;
#define r 4
#define c 5

// Function to check if a word exists in a grid
// starting from the first match in the grid
// level: index till which pattern is matched
// x, y: current position in 2D array
bool findmatch(char mat[r], string pat, int x, int y,
               int nrow, int ncol, int level)
{
    int l = pat.length();

    // Pattern matched
    if (level == l)
        return true;

    // Out of Boundary
    if (x < 0 || y < 0 || x >= nrow || y >= ncol)
        return false;

    // If grid matches with a letter while
    // recursion
    if (mat[x][y] == pat[level]) {

        // Marking this cell as visited
        char temp = mat[x][y];
        mat[x][y] = '#';

        // finding subpattern in 4 directions
        bool res = findmatch(mat, pat, x - 1, y, nrow, ncol, level + 1) |
                   findmatch(mat, pat, x + 1, y, nrow, ncol, level + 1) |
                   findmatch(mat, pat, x, y - 1, nrow, ncol, level + 1) |
                   findmatch(mat, pat, x, y + 1, nrow, ncol, level + 1);

        // marking this cell
        // as unvisited again
        mat[x][y] = temp;
        return res;
    }
    else // Not matching then false
        return false;
}

// Function to check if the word exists in the grid or not
bool checkMatch(char mat[r], string pat, int nrow, int ncol)
{

    int l = pat.length();

    // if total characters in matrix is
    // less then pattern lenghth
    if (l > nrow * ncol)
        return false;

    // Traverse in the grid
    for (int i = 0; i < nrow; i++) {
        for (int j = 0; j < ncol; j++) {

            // If first letter matches, then recur and check
            if (mat[i][j] == pat[0])
                if (findmatch(mat, pat, i, j, nrow, ncol, 0))
                    return true;
        }
    }
    return false;
}

// Driver Code
int main()
{
    char grid[r] = { "axmy",
                        "bgdf",
                        "xeet",
                        "raks" };

    // Function to check if word exists or not
    if (checkMatch(grid, "geeks", r, c))
        cout << "Yes";
    else
        cout << "No";

 return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the word
// exists in the grid or not
class GFG
{

static final int r = 4;
static final int c = 4;

// Function to check if a word exists in a grid
// starting from the first match in the grid
// level: index till which pattern is matched
// x, y: current position in 2D array
static boolean findmatch(char mat[][], String pat, int x, int y,
                        int nrow, int ncol, int level)
{
    int l = pat.length();

    // Pattern matched
    if (level == l)
        return true;

    // Out of Boundary
    if (x < 0 || y < 0 || x >= nrow || y >= ncol)
        return false;

    // If grid matches with a letter while
    // recursion
    if (mat[x][y] == pat.charAt(level))
    {

        // Marking this cell as visited
        char temp = mat[x][y];
        mat[x][y] = '#';

        // finding subpattern in 4 directions
        boolean res = findmatch(mat, pat, x - 1, y, nrow, ncol, level + 1) |
                    findmatch(mat, pat, x + 1, y, nrow, ncol, level + 1) |
                    findmatch(mat, pat, x, y - 1, nrow, ncol, level + 1) |
                    findmatch(mat, pat, x, y + 1, nrow, ncol, level + 1);

        // marking this cell
        // as unvisited again
        mat[x][y] = temp;
        return res;
    }
    else // Not matching then false
        return false;
}

// Function to check if the word exists in the grid or not
static boolean checkMatch(char mat[][], String pat, int nrow, int ncol)
{

    int l = pat.length();

    // if total characters in matrix is
    // less then pattern lenghth
    if (l > nrow * ncol)
        return false;

    // Traverse in the grid
    for (int i = 0; i < nrow; i++)
    {
        for (int j = 0; j < ncol; j++)
        {

            // If first letter matches, then recur and check
            if (mat[i][j] == pat.charAt(0))
                if (findmatch(mat, pat, i, j, nrow, ncol, 0))
                    return true;
        }
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    char grid[][] = { "axmy".toCharArray(),
                        "bgdf".toCharArray(),
                        "xeet".toCharArray(),
                        "raks".toCharArray() };

    // Function to check if word exists or not
    if (checkMatch(grid, "geeks", r, c))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if the word
# exists in the grid or not

r = 4
c = 4

# Function to check if a word exists
# in a grid starting from the first
# match in the grid level: index till 
# which pattern is matched x, y: current
# position in 2D array
def findmatch(mat, pat, x, y,
              nrow, ncol, level) :

    l = len(pat)

    # Pattern matched
    if (level == l) :
        return True

    # Out of Boundary
    if (x < 0 or y < 0 or
        x >= nrow or y >= ncol) :
        return False

    # If grid matches with a letter
    # while recursion
    if (mat[x][y] == pat[level]) :

        # Marking this cell as visited
        temp = mat[x][y]
        mat[x].replace(mat[x][y], "#")

        # finding subpattern in 4 directions
        res = (findmatch(mat, pat, x - 1, y, nrow, ncol, level + 1) |
               findmatch(mat, pat, x + 1, y, nrow, ncol, level + 1) |
               findmatch(mat, pat, x, y - 1, nrow, ncol, level + 1) |
               findmatch(mat, pat, x, y + 1, nrow, ncol, level + 1))

        # marking this cell as unvisited again
        mat[x].replace(mat[x][y], temp)
        return res

    else : # Not matching then false
        return False

# Function to check if the word
# exists in the grid or not
def checkMatch(mat, pat, nrow, ncol) :

    l = len(pat)

    # if total characters in matrix is
    # less then pattern lenghth
    if (l > nrow * ncol) :
        return False

    # Traverse in the grid
    for i in range(nrow) :
        for j in range(ncol) :

            # If first letter matches, then
            # recur and check
            if (mat[i][j] == pat[0]) :
                if (findmatch(mat, pat, i, j,
                              nrow, ncol, 0)) :
                    return True
    return False

# Driver Code
if __name__ == "__main__" :

    grid = ["axmy", "bgdf",
            "xeet", "raks"]

    # Function to check if word
    # exists or not
    if (checkMatch(grid, "geeks", r, c)) :
        print("Yes")
    else :
        print("No")

# This code is contributed by Ryuga
```

## C#

```
// C# program to check if the word
// exists in the grid or not
using System;

class GFG
{

static readonly int r = 4;
static readonly int c = 4;

// Function to check if a word exists in a grid
// starting from the first match in the grid
// level: index till which pattern is matched
// x, y: current position in 2D array
static bool findmatch(char [,]mat, String pat, int x, int y,
                        int nrow, int ncol, int level)
{
    int l = pat.Length;

    // Pattern matched
    if (level == l)
        return true;

    // Out of Boundary
    if (x < 0 || y < 0 || x >= nrow || y >= ncol)
        return false;

    // If grid matches with a letter while
    // recursion
    if (mat[x, y] == pat[level])
    {

        // Marking this cell as visited
        char temp = mat[x, y];
        mat[x, y] = '#';

        // finding subpattern in 4 directions
        bool res = findmatch(mat, pat, x - 1, y, nrow, ncol, level + 1) |
                    findmatch(mat, pat, x + 1, y, nrow, ncol, level + 1) |
                    findmatch(mat, pat, x, y - 1, nrow, ncol, level + 1) |
                    findmatch(mat, pat, x, y + 1, nrow, ncol, level + 1);

        // marking this cell
        // as unvisited again
        mat[x, y] = temp;
        return res;
    }
    else // Not matching then false
        return false;
}

// Function to check if the word exists in the grid or not
static bool checkMatch(char [,]mat, String pat, int nrow, int ncol)
{

    int l = pat.Length;

    // if total characters in matrix is
    // less then pattern lenghth
    if (l > nrow * ncol)
        return false;

    // Traverse in the grid
    for (int i = 0; i < nrow; i++)
    {
        for (int j = 0; j < ncol; j++)
        {

            // If first letter matches, then recur and check
            if (mat[i, j] == pat[0])
                if (findmatch(mat, pat, i, j, nrow, ncol, 0))
                    return true;
        }
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    char [,]grid = { {'a','x','m','y'},
                    {'b','g','d','f'},
                    {'x','e','e','t'},
                    {'r','a','k','s'} };

    // Function to check if word exists or not
    if (checkMatch(grid, "geeks", r, c))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to check if the word
    // exists in the grid or not

    let r = 4;
    let c = 4;

    // Function to check if a word exists in a grid
    // starting from the first match in the grid
    // level: index till which pattern is matched
    // x, y: current position in 2D array
    function findmatch(mat, pat, x, y, nrow, ncol, level)
    {
        let l = pat.length;

        // Pattern matched
        if (level == l)
            return true;

        // Out of Boundary
        if (x < 0 || y < 0 || x >= nrow || y >= ncol)
            return false;

        // If grid matches with a letter while
        // recursion
        if (mat[x][y] == pat[level])
        {

            // Marking this cell as visited
            let temp = mat[x][y];
            mat[x][y] = '#';

            // finding subpattern in 4 directions
            let res =
            findmatch(mat, pat, x - 1, y, nrow, ncol, level + 1) |
            findmatch(mat, pat, x + 1, y, nrow, ncol, level + 1) |
            findmatch(mat, pat, x, y - 1, nrow, ncol, level + 1) |
            findmatch(mat, pat, x, y + 1, nrow, ncol, level + 1);

            // marking this cell
            // as unvisited again
            mat[x][y] = temp;
            return res;
        }
        else // Not matching then false
            return false;
    }

    // Function to check if the word exists in the grid or not
    function checkMatch(mat, pat, nrow, ncol)
    {

        let l = pat.length;

        // if total characters in matrix is
        // less then pattern lenghth
        if (l > nrow * ncol)
            return false;

        // Traverse in the grid
        for (let i = 0; i < nrow; i++)
        {
            for (let j = 0; j < ncol; j++)
            {

                // If first letter matches, then recur and check
                if (mat[i][j] == pat[0])
                    if (findmatch(mat, pat, i, j, nrow, ncol, 0))
                        return true;
            }
        }
        return false;
    }

    let grid = [ "axmy".split(''),
                        "bgdf".split(''),
                        "xeet".split(''),
                        "raks".split('') ];

    // Function to check if word exists or not
    if (checkMatch(grid, "geeks", r, c))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```