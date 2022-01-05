# TCS code life 9(zone 1)2020 |星座

> 哎哎哎:# t0]https://www . geeksforgeeks . org/TCS-code life-9-zone-1-2020-constellation/

三个字符 **{#，*，。}** 代表太空中恒星和星系的星座。每个星系由 **#** 字符划分。给定的星系中可以有一颗或多颗恒星。星星只能是元音的形状 **{A，E，I，O，U}** 。元音形状的 ***** 集合是一颗星。一颗恒星包含在一个 3×3 的块中。星星不能重叠。圆点**(。)**字符表示空格。

给定一个尺寸为 3×N 的[矩阵](https://www.geeksforgeeks.org/category/data-structures/matrix/) **mat[][]** ，由 **{#，*，。}** 人物，任务是寻找星系和其中的恒星。

**示例:**

> **输入:** N = 18，mat[][] = {{*。* # * * * # * * * # * * * .* .}, {* .* # * .* # .* .# * * * * * *}, {* * * # * * * # * * * # * * * * .*}}
> **输出:** U#O#I#EA
> **说明:**
> 可以看到，星星分别组成了字母 U、O、I、E、A 的形象。
> 
> **输入:** N = 12，mat[][] = {{*。* # .* * * # .* .}, {* .* # .。* .# * * *}, {* * * # .* * * # * .*}}
> **输出:** U#I#A
> **说明:**
> 可见星星组成了字母 U、I、A 的形象。

**方法:**思路是[使用变量 **i** 从范围**【0，N–1】**开始逐列遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，并检查给定的{#，*，}排列是否正确。}形成一个星系、一个空格或一个元音。出现以下情况:

*   当给定列中遇到所有 **'#'** 时:在这种情况下，打印 **'#'** ，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)遍历矩阵。
*   当所有**’”在给定的列中遇到**:这种情况下，跳过当前列，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)遍历矩阵。
*   对于所有其他情况，检查**的给定排列是否{#，*，。}** 形成元音，然后打印元音，将列索引 **i** 更新为 **(i + 3)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the vowels(stars)
// in order of their occurrence within
// the given galaxy
void printGalaxy(
    vector<vector<char> > mat, int n)
{

    // Iterate the matrix column-wise
    for (int i = 0; i < n; i++) {

        // If all '#' is encountered
        // in the given column, print '#'
        if (mat[0][i] == '#'
            && mat[1][i] == '#'
            && mat[2][i] == '#') {
            cout << '#';
        }

        // If all '.' is encountered in
        // the given column, skip the
        // current column
        else if (mat[0][i] == '.'
                 && mat[1][i] == '.'
                 && mat[2][i] == '.') {
        }

        // If above cases fail
        else {

            char a, b, c, a1, b1;
            char c1, a2, b2, c2;
            int x1 = i;
            a = mat[0][x1];
            b = mat[0][x1 + 1];
            c = mat[0][x1 + 2];
            a1 = mat[1][x1];
            b1 = mat[1][x1 + 1];
            c1 = mat[1][x1 + 2];
            a2 = mat[2][x1];
            b2 = mat[2][x1 + 1];
            c2 = mat[2][x1 + 2];

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'A'
            if (a == '.' && b == '*'
                && c == '.' && a1 == '*'
                && b1 == '*' && c1 == '*'
                && a2 == '*' && b2 == '.'
                && c2 == '*') {

                // If true, print A
                cout << "A";

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'E'
            if (a == '*' && b == '*'
                && c == '*' && a1 == '*'
                && b1 == '*' && c1 == '*'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If true, print E
                cout << "E";

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'I'
            if (a == '*' && b == '*'
                && c == '*' && a1 == '.'
                && b1 == '*' && c1 == '.'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If true, print I
                cout << "I";

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'O'
            if (a == '*' && b == '*'
                && c == '*' && a1 == '*'
                && b1 == '.' && c1 == '*'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If true, print O
                cout << "O";

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'U'
            if (a == '*' && b == '.'
                && c == '*' && a1 == '*'
                && b1 == '.' && c1 == '*'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If True, print U
                cout << "U";

                // Increment column number
                i = i + 2;
            }
        }
    }
}

// Driver Code
int main()
{
    // Given n, number of columns
    int N = 18;

    // Given matrix
    vector<vector<char> > mat
        = { { '*', '.', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '.', '*', '.' },
            { '*', '.', '*', '#', '*', '.', '*', '#', '.',
              '*', '.', '#', '*', '*', '*', '*', '*', '*' },
            { '*', '*', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '*', '.',
              '*' } };

    // Function Call
    printGalaxy(mat, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to print the vowels(stars)
    // in order of their occurrence within
    // the given galaxy
    static void printGalaxy(char mat[][], int n)
    {

        // Iterate the matrix column-wise
        for (int i = 0; i < n; i++)
        {

            // If all '#' is encountered
            // in the given column, print '#'
            if (mat[0][i] == '#' && mat[1][i] == '#'
                && mat[2][i] == '#') {
                System.out.print('#');
            }

            // If all '.' is encountered in
            // the given column, skip the
            // current column
            else if (mat[0][i] == '.' && mat[1][i] == '.'
                     && mat[2][i] == '.') {
            }

            // If above cases fail
            else {

                char a, b, c, a1, b1;
                char c1, a2, b2, c2;
                int x1 = i;
                a = mat[0][x1];
                b = mat[0][x1 + 1];
                c = mat[0][x1 + 2];
                a1 = mat[1][x1];
                b1 = mat[1][x1 + 1];
                c1 = mat[1][x1 + 2];
                a2 = mat[2][x1];
                b2 = mat[2][x1 + 1];
                c2 = mat[2][x1 + 2];

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'A'
                if (a == '.' && b == '*' && c == '.'
                    && a1 == '*' && b1 == '*' && c1 == '*'
                    && a2 == '*' && b2 == '.'
                    && c2 == '*') {

                    // If true, print A
                    System.out.print("A");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'E'
                if (a == '*' && b == '*' && c == '*'
                    && a1 == '*' && b1 == '*' && c1 == '*'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If true, print E
                    System.out.print("E");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'I'
                if (a == '*' && b == '*' && c == '*'
                    && a1 == '.' && b1 == '*' && c1 == '.'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If true, print I
                    System.out.print("I");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'O'
                if (a == '*' && b == '*' && c == '*'
                    && a1 == '*' && b1 == '.' && c1 == '*'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If true, print O
                    System.out.print("O");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'U'
                if (a == '*' && b == '.' && c == '*'
                    && a1 == '*' && b1 == '.' && c1 == '*'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If True, print U
                    System.out.print("U");

                    // Increment column number
                    i = i + 2;
                }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given n, number of columns
        int N = 18;

        // Given matrix
        char mat[][] = {
            { '*', '.', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '.', '*', '.' },
            { '*', '.', '*', '#', '*', '.', '*', '#', '.',
              '*', '.', '#', '*', '*', '*', '*', '*', '*' },
            { '*', '*', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '*', '.', '*' }
        };

        // Function Call
        printGalaxy(mat, N);
    }
}

// This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to print the vowels(stars)
    // in order of their occurrence within
    // the given galaxy
    static void printGalaxy(char [,]mat, int n)
    {

        // Iterate the matrix column-wise
        for (int i = 0; i < n; i++)
        {

            // If all '#' is encountered
            // in the given column, print '#'
            if (mat[0,i] == '#' && mat[1,i] == '#'
                && mat[2,i] == '#') {
                Console.Write('#');
            }

            // If all '.' is encountered in
            // the given column, skip the
            // current column
            else if (mat[0,i] == '.' && mat[1,i] == '.'
                     && mat[2,i] == '.') {
            }

            // If above cases fail
            else {

                char a, b, c, a1, b1;
                char c1, a2, b2, c2;
                int x1 = i;
                a = mat[0,x1];
                b = mat[0,x1 + 1];
                c = mat[0,x1 + 2];
                a1 = mat[1,x1];
                b1 = mat[1,x1 + 1];
                c1 = mat[1,x1 + 2];
                a2 = mat[2,x1];
                b2 = mat[2,x1 + 1];
                c2 = mat[2,x1 + 2];

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'A'
                if (a == '.' && b == '*' && c == '.'
                    && a1 == '*' && b1 == '*' && c1 == '*'
                    && a2 == '*' && b2 == '.'
                    && c2 == '*') {

                    // If true, print A
                    Console.Write("A");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'E'
                if (a == '*' && b == '*' && c == '*'
                    && a1 == '*' && b1 == '*' && c1 == '*'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If true, print E
                    Console.Write("E");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'I'
                if (a == '*' && b == '*' && c == '*'
                    && a1 == '.' && b1 == '*' && c1 == '.'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If true, print I
                    Console.Write("I");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'O'
                if (a == '*' && b == '*' && c == '*'
                    && a1 == '*' && b1 == '.' && c1 == '*'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If true, print O
                    Console.Write("O");

                    // Increment column number
                    i = i + 2;
                }

                // Check if the arrangement
                // of '.' and '*' forms
                // character 'U'
                if (a == '*' && b == '.' && c == '*'
                    && a1 == '*' && b1 == '.' && c1 == '*'
                    && a2 == '*' && b2 == '*'
                    && c2 == '*') {

                    // If True, print U
                    Console.Write("U");

                    // Increment column number
                    i = i + 2;
                }
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given n, number of columns
        int N = 18;

        // Given matrix
        char [,]mat = {
            { '*', '.', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '.', '*', '.' },
            { '*', '.', '*', '#', '*', '.', '*', '#', '.',
              '*', '.', '#', '*', '*', '*', '*', '*', '*' },
            { '*', '*', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '*', '.', '*' }
        };

        // Function Call
        printGalaxy(mat, N);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the vowels(stars)
// in order of their occurrence within
// the given galaxy
function printGalaxy(mat, n)
{

    // Iterate the matrix column-wise
    for (let i = 0; i < n; i++) {

        // If all '#' is encountered
        // in the given column, print '#'
        if (mat[0][i] == '#'
            && mat[1][i] == '#'
            && mat[2][i] == '#') {
            document.write('#');
        }

        // If all '.' is encountered in
        // the given column, skip the
        // current column
        else if (mat[0][i] == '.'
                 && mat[1][i] == '.'
                 && mat[2][i] == '.') {
        }

        // If above cases fail
        else {

            let a, b, c, a1, b1;
            let c1, a2, b2, c2;
            let x1 = i;
            a = mat[0][x1];
            b = mat[0][x1 + 1];
            c = mat[0][x1 + 2];
            a1 = mat[1][x1];
            b1 = mat[1][x1 + 1];
            c1 = mat[1][x1 + 2];
            a2 = mat[2][x1];
            b2 = mat[2][x1 + 1];
            c2 = mat[2][x1 + 2];

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'A'
            if (a == '.' && b == '*'
                && c == '.' && a1 == '*'
                && b1 == '*' && c1 == '*'
                && a2 == '*' && b2 == '.'
                && c2 == '*') {

                // If true, print A
                document.write("A");

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'E'
            if (a == '*' && b == '*'
                && c == '*' && a1 == '*'
                && b1 == '*' && c1 == '*'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If true, print E
                document.write("E");

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'I'
            if (a == '*' && b == '*'
                && c == '*' && a1 == '.'
                && b1 == '*' && c1 == '.'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If true, print I
                document.write("I");

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'O'
            if (a == '*' && b == '*'
                && c == '*' && a1 == '*'
                && b1 == '.' && c1 == '*'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If true, print O
                document.write("O");

                // Increment column number
                i = i + 2;
            }

            // Check if the arrangement
            // of '.' and '*' forms
            // character 'U'
            if (a == '*' && b == '.'
                && c == '*' && a1 == '*'
                && b1 == '.' && c1 == '*'
                && a2 == '*' && b2 == '*'
                && c2 == '*') {

                // If True, print U
                document.write("U");

                // Increment column number
                i = i + 2;
            }
        }
    }
}

// Driver Code

    // Given n, number of columns
    let N = 18;

    // Given matrix
    let mat
        = [ [ '*', '.', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '.', '*', '.' ],
            [ '*', '.', '*', '#', '*', '.', '*', '#', '.',
              '*', '.', '#', '*', '*', '*', '*', '*', '*' ],
            [ '*', '*', '*', '#', '*', '*', '*', '#', '*',
              '*', '*', '#', '*', '*', '*', '*', '.',
              '*' ] ];

    // Function Call
    printGalaxy(mat, N);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
U#O#I#EA
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)