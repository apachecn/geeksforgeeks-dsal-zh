# 检查是否所有敌人都被放置在矩阵中的炸弹杀死

> 原文:[https://www . geeksforgeeks . org/check-如果所有敌人都被放置在矩阵中的炸弹杀死/](https://www.geeksforgeeks.org/check-if-all-enemies-are-killed-with-bombs-placed-in-a-matrix/)

给定一个角色矩阵作为输入，任务是根据以下条件检查是否所有敌人都被杀死:

> 1.矩阵可以包含 3 个字符
> X–>表示战争区域。
> B–>表示炸弹。
> E–>表示敌人。
> 2。炸弹“B”只能从一端向另一端沿水平和垂直方向爆炸。
> 3。如果所有敌人都被当前炸弹杀死，打印**是**，否则打印**否**T9】

**示例:**

```
Input: matrix =
XXEX
XBXX
XEXX
XXBX 
Output: Yes

Input: matrix =
XXEX
XBXX
XEXX
XXXX
Output: No
```

**方法:**给定的问题可以通过以下方法解决:

1.  获取字符矩阵
2.  遍历查找矩阵中的所有炸弹索引
3.  并将这些行和列存储在 rs 和 cls 数组中。
4.  在所有的旅行之后，检查每一个敌人在那一行或那一列是否有炸弹。
5.  如果没有炸弹的行或列中有任何敌人，则打印否，否则打印是。

**实施:**

## C++

```
// C++ program to kill all enemies

#include <iostream>
using namespace std;

// Function to find Enemies killed or not
int Kill_Enemy(string s[], int row, int col)
{

    int rs[row]={0},cls[col]={0};

 for(int i=0;i<row;i++){

  for(int j=0;j<col;j++){

    if(s[i][j]=='B'){

        rs[i]++;cls[j]++;

       }

   }

 }

 for(int i=0;i<row;i++){

  for(int j=0;j<col;j++){

    if(s[i][j]=='E'){

        if(rs[i]==0&&cls[j]==0)return 0;

       }

   }

 }

 return 1;
}

// Driver Code
int main(int argc, char** argv)
{
    // Get the input matrix
    string s[] = { "XXEX",
                   "XBXX",
                   "XEXX",
                   "XXBX" };

    // Calculate Rows and columns of the string
    int row = sizeof(s) / sizeof(s[0]),
        col = s[0].length();

    // Check if all enemies will be killed or not
    if (Kill_Enemy(s, row, col) == 1)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to kill all enemies
class GFG
{

// Function to find Enemies killed or not
static int Kill_Enemy(char [][]s, int row, int col)
{

    int i, j, x, y;

    // Loop to evaluate the Bomb
    for (i = 0; i < row; i++)
    {
        for (j = 0; j < col; j++)
        {

            // Check if this index is a bomb
            if (s[i][j] == 'B')
            {

                // Kill all enemies
                // in horizontal direction
                for (x = 0; x < row; x++)
                {
                    if (s[x][j] != 'B')
                        s[x][j] = 'X';
                }

                // Kill all enemies
                // in vertical direction
                for (y = 0; y < col; y++)
                {
                    if (s[i][y] != 'B')
                        s[i][y] = 'X';
                }
            }
        }
    }

    // All bombs have been found

    // Check if any enemy is still present
    for (i = 0; i < row; i++)
    {
        for (j = 0; j < col; j++)
        {

            if (s[i][j] == 'E')

                // Since an enemy is present
                // Return 0 denoting No as output
                return 0;
        }
    }

    // Since all enemies are killed
    // Return 1 denoting Yes as output
    return 1;
}

// Driver Code
public static void main(String[] args)
{
    // Get the input matrix
    char [][]s = { "XXEX".toCharArray(),
                "XBXX".toCharArray(),
                "XEXX".toCharArray(),
                "XXBX".toCharArray() };

    // Calculate Rows and columns of the String
    int row = s.length,
        col = s[0].length;

    // Check if all enemies will be killed or not
    if (Kill_Enemy(s, row, col) == 1)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to kill all enemies

# Function to find Enemies killed or not
def Kill_Enemy(s, row, col):
    i, j, x, y = 0, 0, 0, 0;

    # Loop to evaluate the Bomb
    for i in range(row):
        for j in range(col):

            # Check if this index is a bomb
            if (s[i][j] == 'B'):

                # Kill all enemies
                # in horizontal direction
                for x in range(row):
                    if (s[x][j] != 'B'):
                        s[x][j] = 'X';

                # Kill all enemies
                # in vertical direction
                for y in range(col):
                    if (s[i][y] != 'B'):
                        s[i][y] = 'X';

    # All bombs have been found

    # Check if any enemy is still present
    for i in range(row):
        for j in range(col):

            if (s[i][j] == 'E'):

                # Since an enemy is present
                # Return 0 denoting No as output
                return 0;

    # Since all enemies are killed
    # Return 1 denoting Yes as output
    return 1;

# Driver Code
if __name__ == '__main__':

    # Get the input matrix
    s = [['X','X','E','X'],
        ['X','B','X','X'],
        ['X','E','X','X'],
        ['X','X','B','X']]

    # Calculate Rows and columns of the String
    row = len(s);
    col = len(s[0]);

    # Check if all enemies will be killed or not
    if (Kill_Enemy(s, row, col) == 1):
        print("Yes");
    else:
        print("No");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to kill all enemies
using System;

class GFG
{

// Function to find Enemies killed or not
static int Kill_Enemy(char [,]s,
                      int row, int col)
{
    int i, j, x, y;

    // Loop to evaluate the Bomb
    for (i = 0; i < row; i++)
    {
        for (j = 0; j < col; j++)
        {

            // Check if this index is a bomb
            if (s[i, j] == 'B')
            {

                // Kill all enemies
                // in horizontal direction
                for (x = 0; x < row; x++)
                {
                    if (s[x, j] != 'B')
                        s[x, j] = 'X';
                }

                // Kill all enemies
                // in vertical direction
                for (y = 0; y < col; y++)
                {
                    if (s[i, y] != 'B')
                        s[i, y] = 'X';
                }
            }
        }
    }

    // All bombs have been found

    // Check if any enemy is still present
    for (i = 0; i < row; i++)
    {
        for (j = 0; j < col; j++)
        {

            if (s[i, j] == 'E')

                // Since an enemy is present
                // Return 0 denoting No as output
                return 0;
        }
    }

    // Since all enemies are killed
    // Return 1 denoting Yes as output
    return 1;
}

// Driver Code
public static void Main(String[] args)
{
    // Get the input matrix
    char [,]s = {{'X', 'B', 'X', 'X'},
                 {'X', 'E', 'X', 'X'},
                 {'X', 'X', 'B', 'X'}};

    // Calculate Rows and columns of the String
    int row = s.GetLength(0),
        col = s.GetLength(1);

    // Check if all enemies will be killed or not
    if (Kill_Enemy(s, row, col) == 1)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to kill all enemies

    // Function to find Enemies killed or not
    function Kill_Enemy(s, row, col)
    {

        let i, j, x, y;

        // Loop to evaluate the Bomb
        for (i = 0; i < row; i++)
        {
            for (j = 0; j < col; j++)
            {

                // Check if this index is a bomb
                if (s[i][j] == 'B')
                {

                    // Kill all enemies
                    // in horizontal direction
                    for (x = 0; x < row; x++)
                    {
                        if (s[x][j] != 'B')
                            s[x][j] = 'X';
                    }

                    // Kill all enemies
                    // in vertical direction
                    for (y = 0; y < col; y++)
                    {
                        if (s[i][y] != 'B')
                            s[i][y] = 'X';
                    }
                }
            }
        }

        // All bombs have been found

        // Check if any enemy is still present
        for (i = 0; i < row; i++)
        {
            for (j = 0; j < col; j++)
            {

                if (s[i][j] == 'E')

                    // Since an enemy is present
                    // Return 0 denoting No as output
                    return 0;
            }
        }

        // Since all enemies are killed
        // Return 1 denoting Yes as output
        return 1;
    }

    // Get the input matrix
    let s = [ "XXEX".split(''),
                "XBXX".split(''),
                "XEXX".split(''),
                "XXBX".split('') ];

    // Calculate Rows and columns of the String
    let row = s.length, col = s[0].length;

    // Check if all enemies will be killed or not
    if (Kill_Enemy(s, row, col) == 1)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```