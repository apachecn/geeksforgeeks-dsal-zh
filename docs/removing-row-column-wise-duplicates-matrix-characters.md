# 从字符矩阵中删除行或列重复

> 原文:[https://www . geesforgeks . org/remove-row-column-wise-duplicates-matrix-characters/](https://www.geeksforgeeks.org/removing-row-column-wise-duplicates-matrix-characters/)

给定一个只包含小写字母的字符矩阵，从矩阵中形成一个新的字符串，该字符串在删除每行和每列的重复字符后仍然存在。剩余的字符按行连接形成字符串。
**例:**

```
Input : Matrix of characters (Or array
        of strings)
        aabcd
        effgh
        iijkk
        lmnoo
        pqqrs
        ttuvw
        xxyyz
Output : bcdeghjlmnprsuvwz
The characters that appear more than once
in their row or column are removed.

Input : zx
        xz
Output :zxxz
```

**方法:**遍历整个矩阵，对于每个元素，检查其对应的行和列。如果有重复项，则将另一个矩阵中的特定单元格标记为 true。最后，将另一个矩阵中有假值的所有字符连接起来形成字符串。

## C++

```
// CPP code to form string after removing
// duplicates from rows and columns.
#include <bits/stdc++.h>
using namespace std;

// Function to check duplicates
// in row and column
void findDuplciates(string a[], int n, int m)
{
    // Create an array isPresent and initialize
    // all entries of it as false. The value of
    // isPresent[i][j] is going to be true if
    // s[i][j] is present in its row or column.
    bool isPresent[n][m];
    memset(isPresent, 0, sizeof(isPresent));

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // Checking every row for
            // duplicates of a[i][j]
            for (int k = 0; k < n; k++) {
                if (a[i][j] == a[k][j] && i != k) {
                    isPresent[i][j] = true;
                    isPresent[k][j] = true;
                }
            }

            // Checking every column for
            // duplicate characters
            for (int k = 0; k < m; k++) {
                if (a[i][j] == a[i][k] && j != k) {
                    isPresent[i][j] = true;
                    isPresent[i][k] = true;
                }
            }
        }
    }

    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)

            // If the character is unique
            // in its row and column
            if (!isPresent[i][j])
                printf("%c", a[i][j]);
}

// Driver code
int main()
{
    int n = 2, m = 5;

    // character array
    string a[] = { "zx", "xz" };

    // Calling function
    findDuplciates(a, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to form string
// after removing duplicates
// from rows and columns.

class GFG
{
    // Function to check
    // duplicates in row
    // and column
    static void findDuplciates(String []a,
                            int n, int m)
    {
        // Create an array isPresent
        // and initialize all entries
        // of it as false. The value
        // of isPresent[i,j] is going
        // to be true if s[i,j] is
        // present in its row or column.
        boolean [][]isPresent = new boolean[n] [m];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                isPresent[i][j]=false;
            }
        }

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Checking every row for
                // duplicates of a[i,j]
                for (int k = 0; k < n; k++)
                {
                    if (a[i].charAt(j)== a[k].charAt(j) &&
                                i != k)
                    {
                        isPresent[i][j] = true;
                        isPresent[k][j] = true;
                    }
                }

                // Checking every column for
                // duplicate characters
                for (int k = 0; k < m; k++)
                {
                    if (a[i].charAt(j)== a[i].charAt(k) &&
                                j != k)
                    {
                        isPresent[i][j] = true;
                        isPresent[i][k] = true;
                    }
                }
            }
        }

        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)

                // If the character is
                // unique in its row
                // and column
                if (isPresent[i][j]==false)
                    System.out.print(a[i].charAt(j));
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 2, m = 2;

        // character array
        String []a = new String[]{"zx",
                                "xz"};

        // Calling function
        findDuplciates(a, n, m);
    }
}

// This code is contributed by
// Hritik Raj( ihritik)
```

## 蟒蛇 3

```
# Python3 code to form string after removing
# duplicates from rows and columns.

# Function to check duplicates
# in row and column
def findDuplicates(a, n, m):

    # Create an array isPresent and initialize
    # all entries of it as false. The value of
    # isPresent[i][j] is going to be true if
    # s[i][j] is present in its row or column.
    isPresent = [[False for i in range(n)]
                        for j in range(m)]

    for i in range(n):
        for j in range(m):

            # Checking every row for
            # duplicates of a[i][j]
            for k in range(n):
                if i != k and a[i][j] == a[k][j]:
                    isPresent[i][j] = True
                    isPresent[k][j] = True

            # Checking every row for
            # duplicates of a[i][j]
            for k in range(m):
                if j != k and a[i][j] == a[i][k]:
                    isPresent[i][j] = True
                    isPresent[i][k] = True

    for i in range(n):
        for j in range(m):

            # If the character is unique
            # in its row and column
            if not isPresent[i][j]:
                print(a[i][j], end = "")

# Driver Code
if __name__ == "__main__":

    n = 2
    m = 2

    # character array
    a = ["zx", "xz"]

    # Calling function
    findDuplicates(a, n, m)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# code to form string
// after removing duplicates
// from rows and columns.
using System;

class GFG
{
    // Function to check
    // duplicates in row
    // and column
    static void findDuplciates(string []a,
                               int n, int m)
    {
        // Create an array isPresent
        // and initialize all entries
        // of it as false. The value
        // of isPresent[i,j] is going
        // to be true if s[i,j] is
        // present in its row or column.
        bool [,]isPresent = new bool[n, m];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Checking every row for
                // duplicates of a[i,j]
                for (int k = 0; k < n; k++)
                {
                    if (a[i][j] == a[k][j] &&
                                   i != k)
                    {
                        isPresent[i, j] = true;
                        isPresent[k, j] = true;
                    }
                }

                // Checking every column for
                // duplicate characters
                for (int k = 0; k < m; k++)
                {
                    if (a[i][j] == a[i][k] &&
                                   j != k)
                    {
                        isPresent[i, j] = true;
                        isPresent[i, k] = true;
                    }
                }
            }
        }

        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)

                // If the character is
                // unique in its row
                // and column
                if (!isPresent[i, j])
                    Console.Write(a[i][j]);
    }

    // Driver code
    static void Main()
    {
        int n = 2, m = 2;

        // character array
        string []a = new string[]{"zx",
                                  "xz"};

        // Calling function
        findDuplciates(a, n, m);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>
// javascript code to form string
// after removing duplicates
// from rows and columns.    // Function to check
    // duplicates in row
    // and column
    function findDuplciates( a , n , m) {
        // Create an array isPresent
        // and initialize all entries
        // of it as false. The value
        // of isPresent[i,j] is going
        // to be true if s[i,j] is
        // present in its row or column.
        var isPresent = Array(n).fill().map(() => Array(m).fill(0));

        for (var i = 0; i < n; i++) {
            for (var j = 0; j < m; j++) {

                isPresent[i][j] = false;
            }
        }

        for (var i = 0; i < n; i++) {
            for (var j = 0; j < m; j++) {

                // Checking every row for
                // duplicates of a[i,j]
                for (var k = 0; k < n; k++) {
                    if (a[i].charAt(j) == a[k].charAt(j) && i != k) {
                        isPresent[i][j] = true;
                        isPresent[k][j] = true;
                    }
                }

                // Checking every column for
                // duplicate characters
                for (k = 0; k < m; k++) {
                    if (a[i].charAt(j) == a[i].charAt(k) && j != k) {
                        isPresent[i][j] = true;
                        isPresent[i][k] = true;
                    }
                }
            }
        }

        for (var i = 0; i < n; i++)
            for (var j = 0; j < m; j++)

                // If the character is
                // unique in its row
                // and column
                if (isPresent[i][j] == false)
                    document.write(a[i].charAt(j));
    }

    // Driver code

        var n = 2, m = 2;

        // character array
        var a = [ "zx", "xz" ];

        // Calling function
        findDuplciates(a, n, m);

// This code contributed by umadevi9616
</script>
```

**输出:**

```
zxxz
```