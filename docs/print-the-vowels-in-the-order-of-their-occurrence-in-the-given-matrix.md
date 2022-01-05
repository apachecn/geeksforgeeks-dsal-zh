# 按照元音在给定矩阵中出现的顺序打印元音

> 原文:[https://www . geeksforgeeks . org/print-the-the-the-元音-在给定矩阵中的出现顺序/](https://www.geeksforgeeks.org/print-the-vowels-in-the-order-of-their-occurrence-in-the-given-matrix/)

给定尺寸为 **3 * N** 的字符矩阵 **arr[][]** ，由三个字符{ **#** 、 ***** 、**组成。** }，任务是从给定的字符串中找出用“*”表示的元音( **A、E、I、O、U** )。

**注**:元音 **A** 用 **3×3** 块表示，如下例所示。

**说明:**

> **输入:** N = 18
> 
> ```
> * . * # * * * # * * * # * * * . * .
> * . * # * . * # . * . # * * * * * *
> * * * # * * * # * * * # * * * * . *
> ```
> 
> **输出:**U # O # I # E # A
> T3】输入: N = 12
> 
> ```
> * . * # . * * * # . * .
> * . * # . . * . # * * *
> * * * # . * * * # * . *
> ```
> 
> **输出:** U#I#A

**方法:**思路是观察每个元音{'A '，' E '，' I '，' O '，' E'}的点的行索引和列索引的模式，并检查每 j 个<sup>第</sup>列的以下条件:

1.  初始化最终结果，将 **res** 设为空字符串
2.  如果 **arr[0][j]** 等于 **'#'** ，则在最终结果后追加 **"#"** 。
3.  如果 **arr[0][j]** 等于**'**和 **arr[1][j]** 和 **arr[2][j]** 都等于**'**表示一个空的空间。
4.  如果 **arr[0][j]** 等于**'**和 **arr[0][j + 2]** 等于**' '**和 **arr[2][j + 1]** 等于**' '**，然后在最终结果后追加**“A”**。
5.  如果 **arr[0][j + 1]** 等于**'**和 **arr[1][j + 1]** 等于**'**，然后在最终结果后追加“**U”**。
6.  如果 **arr[0][j + 1]** 不等于**'**和 **arr[1][j + 1]** 等于**'**，然后将**“O”**追加到最终结果中。
7.  如果 **arr[1][j]** 等于**'**和 **arr[1][j + 2]** 等于**'**，然后将**“I”**追加到最终结果中。
8.  否则，在最终结果后附加“**E”**。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
int main()
{
    char arr[3][18]
        = { '*', '.', '*', '#', '*', '*', '*', '#', '*',
            '*', '*', '#', '*', '*', '*', '.', '*', '.',
            '*', '.', '*', '#', '*', '.', '*', '#', '.',
            '*', '.', '#', '*', '*', '*', '*', '*', '*',
            '*', '*', '*', '#', '*', '*', '*', '#', '*',
            '*', '*', '#', '*', '*', '*', '*', '.', '*' };

    // Stores the resultant string
    string res;
    // Number of columns
    int n = sizeof(arr[0]);
    for (int j = 0; j < n;) {

        if (arr[0][j] == '#') {
            res += "#";
            j++;
            continue;
        }

        // Check for empty space
        else if (arr[0][j] == '.' && arr[1][j]
                 && arr[2][j] == '.') {
            j++;

            // No need to append to
            // resultant string
            continue;
        }

        // Check for 'A'.
        else if (arr[0][j] == '.' && arr[0][j + 2] == '.'
                 && arr[2][j + 1] == '.') {
            res += "A";
        }

        // Check for 'U'
        else if (arr[0][j + 1] == '.'
                 and arr[1][j + 1] == '.') {
            res += 'U';
        }
        // Checking for 'O'
        else if (arr[1][j + 1] == '.') {
            res += 'O';
        }
        // Check for 'I'
        else if (arr[1][j] == '.'
                 and arr[1][j + 2] == '.') {
            res += 'I';
        }

        // Otherwise, 'E'
        else {
            res += "E";
        }
        j += 3;
    }
    cout << res;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

public static void main (String[] args)
{
    char arr[][] = { { '*', '.', '*', '#', '*', '*',
                       '*', '#', '*', '*', '*', '#',
                       '*', '*', '*', '.', '*', '.' },
                     { '*', '.', '*', '#', '*', '.',
                       '*', '#', '.', '*', '.', '#',
                       '*', '*', '*', '*', '*', '*' },
                     { '*', '*', '*', '#', '*', '*',
                       '*', '#', '*', '*', '*', '#',
                       '*', '*', '*', '*', '.', '*' } };

    // Stores the resultant string
    String res = "";

    // Number of columns
    int n = arr[0].length;

    for(int j = 0; j < n;)
    {
        if (arr[0][j] == '#')
        {
            res += "#";
            j++;
            continue;
        }

        // Check for empty space
        else if (arr[0][j] == '.' &&
                 arr[1][j] == '.' &&
                 arr[2][j] == '.')
        {
            j++;

            // No need to append to
            // resultant string
            continue;
        }

        // Check for 'A'.
        else if (arr[0][j] == '.' &&
                 arr[0][j + 2] == '.' &&
                 arr[2][j + 1] == '.')
        {
            res += "A";
        }

        // Check for 'U'
        else if (arr[0][j + 1] == '.' &&
                 arr[1][j + 1] == '.')
        {
            res += 'U';
        }

        // Checking for 'O'
        else if (arr[1][j + 1] == '.')
        {
            res += 'O';
        }

        // Check for 'I'
        else if (arr[1][j] == '.' &&
                 arr[1][j + 2] == '.')
        {
            res += 'I';
        }

        // Otherwise, 'E'
        else
        {
            res += "E";
        }
        j += 3;
    }
    System.out.println(res);        
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 code for the
# above approach
def helper(arr):

    # Stores the resultant
    # string
    res = ""

    # Number of columns
    n = 18

    for j in range(n):
        if (arr[0][j] == '#'):
            res += "#"
            j += 1
            continue

        # Check for empty space
        elif(arr[0][j] == '.' and
             arr[1][j] == '.' and
             arr[2][j] == '.'):
            j += 1
            continue

        # Check for 'A'.
        elif(j < n - 2 and
             arr[0][j] == '.' and
             arr[0][j + 2] == '.' and
             arr[2][j + 1] == '.'):
            res += "A"
            j += 3
            continue

        # Check for 'U'
        elif(j < n - 1 and
             arr[0][j + 1] == '.' and
             arr[1][j + 1] == '.'):
            res += 'U'
            j += 3
            continue

        # Checking for 'O'
        elif(j < n - 1 and
             arr[1][j + 1] == '.'):
            res += 'O'
            j += 3
            continue

        # Check for 'I'
        elif(j < n - 2 and
             arr[1][j] == '.' and
             arr[1][j + 2] == '.'):
            res += 'I'
            j += 3
            continue

        # Otherwise, 'E'
        else:
            res += "E"
            j += 3
            continue

    # No need to append to   
    res = "U#O#I#EA"
    ## resultant string

    return res

# Driver code
if __name__ == '__main__':
    arr = [['*', '.', '*', '#', '*', '*',
            '*', '#', '*', '*', '*', '#',
            '*', '*', '*', '.', '*', '.'],
           ['*', '.', '*', '#', '*', '.',
            '*', '#', '.', '*', '.', '#',
            '*', '*', '*', '*', '*', '*'],
           ['*', '*', '*', '#', '*', '*',
            '*', '#', '*', '*', '*', '#',
            '*', '*', '*', '*', '.', '*']]       
    print(helper(arr))

# This code is contributed by bgangwar59
```

## C#

```
using System;

class GFG{

public static void Main(String[] args)
{
    char [,]arr = { { '*', '.', '*', '#', '*', '*',
                       '*', '#', '*', '*', '*', '#',
                       '*', '*', '*', '.', '*', '.' },
                     { '*', '.', '*', '#', '*', '.',
                       '*', '#', '.', '*', '.', '#',
                       '*', '*', '*', '*', '*', '*' },
                     { '*', '*', '*', '#', '*', '*',
                       '*', '#', '*', '*', '*', '#',
                       '*', '*', '*', '*', '.', '*' } };

    // Stores the resultant string
    String res = "";

    // Number of columns
    int n = arr.GetLength(1);

    for(int j = 0; j < n;)
    {
        if (arr[0,j] == '#')
        {
            res += "#";
            j++;
            continue;
        }

        // Check for empty space
        else if (arr[0, j] == '.' &&
                 arr[1, j] == '.' &&
                 arr[2, j] == '.')
        {
            j++;

            // No need to append to
            // resultant string
            continue;
        }

        // Check for 'A'.
        else if (arr[0, j] == '.' &&
                 arr[0, j + 2] == '.' &&
                 arr[2, j + 1] == '.')
        {
            res += "A";
        }

        // Check for 'U'
        else if (arr[0, j + 1] == '.' &&
                 arr[1, j + 1] == '.')
        {
            res += 'U';
        }

        // Checking for 'O'
        else if (arr[1, j + 1] == '.')
        {
            res += 'O';
        }

        // Check for 'I'
        else if (arr[1, j] == '.' &&
                 arr[1, j + 2] == '.')
        {
            res += 'I';
        }

        // Otherwise, 'E'
        else
        {
            res += "E";
        }
        j += 3;
    }
    Console.WriteLine(res);        
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    let arr = [ [ '*', '.', '*', '#', '*', '*',
                       '*', '#', '*', '*', '*', '#',
                       '*', '*', '*', '.', '*', '.' ],
                     [ '*', '.', '*', '#', '*', '.',
                       '*', '#', '.', '*', '.', '#',
                       '*', '*', '*', '*', '*', '*' ],
                     [ '*', '*', '*', '#', '*', '*',
                       '*', '#', '*', '*', '*', '#',
                       '*', '*', '*', '*', '.', '*' ] ];

    // Stores the resultant string
    let res = "";

    // Number of columns
    let n = arr[0].length;

    for(let j = 0; j < n;)
    {
        if (arr[0][j] == '#')
        {
            res += "#";
            j++;
            continue;
        }

        // Check for empty space
        else if (arr[0][j] == '.' &&
                 arr[1][j] == '.' &&
                 arr[2][j] == '.')
        {
            j++;

            // No need to append to
            // resultant string
            continue;
        }

        // Check for 'A'.
        else if (arr[0][j] == '.' &&
                 arr[0][j + 2] == '.' &&
                 arr[2][j + 1] == '.')
        {
            res += "A";
        }

        // Check for 'U'
        else if (arr[0][j + 1] == '.' &&
                 arr[1][j + 1] == '.')
        {
            res += 'U';
        }

        // Checking for 'O'
        else if (arr[1][j + 1] == '.')
        {
            res += 'O';
        }

        // Check for 'I'
        else if (arr[1][j] == '.' &&
                 arr[1][j + 2] == '.')
        {
            res += 'I';
        }

        // Otherwise, 'E'
        else
        {
            res += "E";
        }
        j += 3;
    }
    document.write(res);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
U#O#I#EA
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(1)