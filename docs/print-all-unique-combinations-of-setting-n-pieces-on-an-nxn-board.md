# 在 NxN 板上打印设置 N 件的所有唯一组合

> 原文:[https://www . geeksforgeeks . org/print-all-unique-set-n-on-nxn-board 上的 n 件组合/](https://www.geeksforgeeks.org/print-all-unique-combinations-of-setting-n-pieces-on-an-nxn-board/)

给定一个整数 **N** ，任务是打印将 **N** 件放入 **NxN** 板的所有**独特组合**。

注意:打印(“*”)表示片段，打印(“-”)表示空白。

示例:

> **输入:** N = 2
> **输出:**
> * *
> –
> 
> *–
> *–
> 
> *–
> –*
> 
> –*
> *–
> 
> –*
> –*
> 
> ––
> * *
> **说明:**空格总数为 2*2=4，要设置的棋子为 2，所以有 4C2 组合((4！/(2!*2!))=6)可能，如上所述。
> 
> **输入:**N = 1
> T3】输出:*

**方法:**这个问题可以通过使用**递归**生成所有可能的解来解决。现在，按照以下步骤解决这个问题:

1.  创建一个名为 **allCombinations** 的函数，它将生成所有可能的解。
2.  它将取一个整数**pieced**表示放置的总件数，整数 **N** 表示需要放置的件数，两个整数 **row** 和 **col** 表示当前件将要放置的行和列，以及一个字符串 **ans** 作为参数，用于存储放置件的矩阵。
3.  现在，对**所有组合**的初始调用将通过 **0** 作为**分段**、 **N** 、 **0** 和 **0** 作为**行**和**列**，以及一个空字符串作为**和**。
4.  在每次通话中，检查基本情况，即:
    *   如果行变成 **N** 并且所有的片都被放置，即**片被放置=N** 。然后打印 **ans** 返回。否则如果**件**不是 **N** ，那么就从这个调用返回。
5.  现在打两个电话:
    *   一个是在当前位置加一个**' ***，一个是离开该位置加 **'-'** 。
6.  之后，递归调用将打印所有可能的解决方案。

下面是上述方法的实现。

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all
// combinations of setting N
// pieces in N x N board
void allCombinations(int piecesPlaced, int N, int row,
                     int col, string ans)
{

    // If the total 2d array's space
    // is exhausted then backtrack.
    if (row == N) {

        // If all the pieces are
        // placed then print the answer.
        if (piecesPlaced == N) {
            cout << ans;
        }
        return;
    }
    int nr = 0;
    int nc = 0;

    // Declare one string
    // that will set the piece.
    string x = "";

    // Declare one string that
    // will leave the space blank.
    string y = "";

    // If the current column
    // is out of bounds then
    // increase the row
    // and set col to 0.
    if (col == N - 1) {
        nr = row + 1;
        nc = 0;
        x = ans + "*\n";
        y = ans + "-\n";
    }

    // Else increase the col
    else {
        nr = row;
        nc = col + 1;
        x = ans + "*\t";
        y = ans + "-\t";
    }

    // Set the piece in the
    // box and move ahead
    allCombinations(piecesPlaced + 1, N, nr, nc, x);

    // Leave the space blank
    // and move forward
    allCombinations(piecesPlaced, N, nr, nc, y);
}

// Driver Code
int main()
{
    int N = 2;
    allCombinations(0, N, 0, 0, "");
    return 0;
}

    // This code is contributed by rakeshsahni.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach

import java.io.*;
import java.util.*;

public class main {

    // Function to print all
    // combinations of setting N
    // pieces in N x N board
    public static void allCombinations(
        int piecesPlaced,
        int N, int row,
        int col, String ans)
    {
        // If the total 2d array's space
        // is exhausted then backtrack.
        if (row == N) {

            // If all the pieces are
            // placed then print the answer.
            if (piecesPlaced == N) {
                System.out.println(ans);
            }
            return;
        }
        int nr = 0;
        int nc = 0;

        // Declare one string
        // that will set the piece.
        String x = "";

        // Declare one string that
        // will leave the space blank.
        String y = "";

        // If the current column
        // is out of bounds then
        // increase the row
        // and set col to 0.
        if (col == N - 1) {
            nr = row + 1;
            nc = 0;
            x = ans + "*\n";
            y = ans + "-\n";
        }

        // Else increase the col
        else {
            nr = row;
            nc = col + 1;
            x = ans + "*\t";
            y = ans + "-\t";
        }
        // Set the piece in the
        // box and move ahead
        allCombinations(
            piecesPlaced + 1, N,
            nr, nc, x);

        // Leave the space blank
        // and move forward
        allCombinations(piecesPlaced, N,
                        nr, nc, y);
    }

    // Driver Code
    public static void main(String[] args)
        throws Exception
    {
        int N = 2;

        allCombinations(0, N, 0, 0, "");
    }
}
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to print all
# combinations of setting N
# pieces in N x N board
def allCombinations(piecesPlaced, N, row, col, ans):

    # If the total 2d array's space
    # is exhausted then backtrack.
    if row == N:

        # If all the pieces are
        # placed then print the answer.
        if piecesPlaced == N:
            print(ans)
        return;

    nr = 0
    nc = 0

    # Declare one string
    # that will set the piece.
    x = ""

    # Declare one string that
    # will leave the space blank.
    y = ""

    # If the current column
    # is out of bounds then
    # increase the row
    # and set col to 0.

    if col == N - 1:
        nr = row + 1
        nc = 0
        x = ans + "*\n"
        y = ans + "-\n"

    # Else increase the col
    else:
        nr = row
        nc = col + 1
        x = ans + "*    "
        y = ans + "-    "

    # Set the piece in the
    # box and move ahead
    allCombinations(piecesPlaced + 1, N, nr, nc, x);

    # Leave the space blank
    # and move forward
    allCombinations(piecesPlaced, N, nr, nc, y);

# Driver Code
N = 2
allCombinations(0, N, 0, 0, "")

# This code is contributed by rdtank.
```

## C#

```
// C# Program for the above approach
using System;
public class main {

    // Function to print all
    // combinations of setting N
    // pieces in N x N board
    public static void allCombinations(int piecesPlaced,
                                       int N, int row,
                                       int col, String ans)
    {
        // If the total 2d array's space
        // is exhausted then backtrack.
        if (row == N) {

            // If all the pieces are
            // placed then print the answer.
            if (piecesPlaced == N) {
                Console.WriteLine(ans);
            }
            return;
        }
        int nr = 0;
        int nc = 0;

        // Declare one string
        // that will set the piece.
        String x = "";

        // Declare one string that
        // will leave the space blank.
        String y = "";

        // If the current column
        // is out of bounds then
        // increase the row
        // and set col to 0.
        if (col == N - 1) {
            nr = row + 1;
            nc = 0;
            x = ans + "*\n";
            y = ans + "-\n";
        }

        // Else increase the col
        else {
            nr = row;
            nc = col + 1;
            x = ans + "*\t";
            y = ans + "-\t";
        }

        // Set the piece in the
        // box and move ahead
        allCombinations(piecesPlaced + 1, N, nr, nc, x);

        // Leave the space blank
        // and move forward
        allCombinations(piecesPlaced, N, nr, nc, y);
    }

    // Driver Code
    public static void Main(string[] args)

    {
        int N = 2;

        allCombinations(0, N, 0, 0, "");
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
// Javascript Program for the above approach

// Function to print all
// combinations of setting N
// pieces in N x N board
function allCombinations(piecesPlaced, N, row, col, ans) {

  // If the total 2d array's space
  // is exhausted then backtrack.
  if (row == N) {

    // If all the pieces are
    // placed then print the answer.
    if (piecesPlaced == N) {
      document.write(ans);
    }
    return;
  }
  let nr = 0;
  let nc = 0;

  // Declare one string
  // that will set the piece.
  let x = "";

  // Declare one string that
  // will leave the space blank.
  let y = "";

  // If the current column
  // is out of bounds then
  // increase the row
  // and set col to 0.
  if (col == N - 1) {
    nr = row + 1;
    nc = 0;
    x = ans + "*<br>";
    y = ans + "-<br>";
  }

  // Else increase the col
  else {
    nr = row;
    nc = col + 1;
    x = ans + "*     ";
    y = ans + "-     ";
  }

  // Set the piece in the
  // box and move ahead
  allCombinations(piecesPlaced + 1, N, nr, nc, x);

  // Leave the space blank
  // and move forward
  allCombinations(piecesPlaced, N, nr, nc, y);
}

// Driver Code
let N = 2;
allCombinations(0, N, 0, 0, "");

// This code is contributed by Saurabh Jaiswal
```

**Output:** 

```
*    *
-    -

*    -
*    -

*    -
-    *

-    *
*    -

-    *
-    *

-    -
*    *
```

**时间复杂度:** O(2^M)，其中 m = n * n
T3】辅助空间:t5】