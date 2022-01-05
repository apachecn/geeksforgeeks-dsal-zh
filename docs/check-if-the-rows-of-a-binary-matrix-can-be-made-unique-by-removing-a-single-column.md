# 通过删除一列

检查二进制矩阵的行是否可以唯一

> 原文:[https://www . geeksforgeeks . org/check-如果可以通过移除单个列来使二进制矩阵的行变得唯一/](https://www.geeksforgeeks.org/check-if-the-rows-of-a-binary-matrix-can-be-made-unique-by-removing-a-single-column/)

给定大小为 **M * N** 的二元矩阵 **mat[][]** 。任务是检查从矩阵中删除一列后矩阵的行是否唯一。

**示例:**

> **输入:** mat[][] = {
> {1 0 1}，
> { 0 0 }，
> {1 0 0}
> }
> **输出:**是
> 删除第 2 列后，矩阵每行变得唯一。
> 
> **输入:** mat[][] = {
> {1 0}，
> {1 0}
> }
> **输出:** No

**进场:**

*   将矩阵视为一个字符串数组，每行视为一个字符串。
*   初始化变量**计数= 0** 以计数矩阵中的重复行。
*   现在从 **i = 0 到 str.length()** 取两个嵌套循环外循环，从 **j = 0 到 i** 取两个嵌套循环内循环，对于每个索引，检查 **str[i] == str[j]** 是否递增计数 1 并断开循环。
*   现在检查**是否计数> = 1** 然后打印**否**否则打印**是**。

以下是上述方法的实施:

## C++

```
// C++ program to check whether the
// Rows of Binary Matrix become unique
// After Deleting a column.
#include <bits/stdc++.h>
using namespace std;

// Function to check whether rows of
// Binary matrix become unique after
// Deleting a column of from matrix.
int uniqueRows(string s[], int m, int n)
{
    // Initialize variable count that
    // stores the count of duplicate rows.
    int i, j, count = 0;

    // Take two nested loop and
    // check weather rows already
    // get seen then increment
    // count by 1 then break the loop.
    for (i = 0; i < n; i++) {
        for (j = 0; j < i; j++) {
            if (s[i] == s[j]) {
                count++;
                break;
            }
        }
    }

    // Check if count>=1 then print No
    // Else print Yes.
    if (count >= 1) {
        cout << "No" << endl;
    }
    else {
        cout << "Yes" << endl;
    }
    return 0;
}

// Driver code.
int main()
{
    int m = 3, n = 3;
    string s[] = {
        { 1, 0, 1 },
        { 0, 0, 0 },
        { 1, 0, 0 }
    };

    // Function calling
    uniqueRows(s, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the
// Rows of Binary Matrix become unique
// After Deleting a column.
class GFG
{

// Function to check whether rows of
// Binary matrix become unique after
// Deleting a column of from matrix.
static int uniqueRows(int [][]s,
                      int m, int n)
{
    // Initialize variable count that
    // stores the count of duplicate rows.
    int i, j, count = 0;

    // Take two nested loop and
    // check weather rows already
    // get seen then increment
    // count by 1 then break the loop.
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < i; j++)
        {
            if (s[i] == s[j])
            {
                count++;
                break;
            }
        }
    }

    // Check if count>=1 then print No
    // Else print Yes.
    if (count >= 1)
        System.out.println("No");
    else
        System.out.println("Yes");
    return 0;
}

// Driver code.
public static void main(String[] args)
{
    int m = 3, n = 3;
    int s[][] = { { 1, 0, 1 },
                  { 0, 0, 0 },
                  { 1, 0, 0 } };

    // Function calling
    uniqueRows(s, m, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to check whether the
# Rows of Binary Matrix become unique
# After Deleting a column.

# Function to check whether rows of
# Binary matrix become unique after
# Deleting a column of from matrix.
def uniqueRows(s, m, n):

    # Initialize variable count that
    # stores the count of duplicate rows.
    i, j, count = 0, 0, 0

    # Take two nested loop and
    # check weather rows already
    # get seen then increment
    # count by 1 then break the loop.
    for i in range(n):
        for j in range(i):
            if (s[i] == s[j]):
                count += 1
                break

    # Check if count>=1 then prNo
    # Else prYes.
    if (count >= 1):
        print("No" )
    else:
        print("Yes")

# Driver code.
m = 3
n = 3
s = [[ 1, 0, 1 ],
     [ 0, 0, 0 ],
     [ 1, 0, 0 ]]

uniqueRows(s, m, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# iprogram to check whether the
// Rows of Binary Matrix become unique
// After Deleting a column.
using System;

class GFG
{

// Function to check whether rows of
// Binary matrix become unique after
// Deleting a column of from matrix.
static int uniqueRows(string []s,
                      int m, int n)
{
    // Initialize variable count that
    // stores the count of duplicate rows.
    int i, j, count = 0;

    // Take two nested loop and
    // check weather rows already
    // get seen then increment
    // count by 1 then break the loop.
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < i; j++)
        {
            if (s[i] == s[j])
            {
                count++;
                break;
            }
        }
    }

    // Check if count>=1 then print No
    // Else print Yes.
    if (count >= 1)
        Console.WriteLine("No");
    else
        Console.WriteLine("Yes");
    return 0;
}

// Driver code.
public static void Main(String[] args)
{
    int m = 3, n = 3;
    string []s = { "101","000", "100"};

    // Function calling
    uniqueRows(s, m, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to check whether the
// Rows of Binary Matrix become unique
// After Deleting a column.

// Function to check whether rows of
// Binary matrix become unique after
// Deleting a column of from matrix.
function uniqueRows(s, m, n)
{

    // Initialize variable count that
    // stores the count of duplicate rows.
    var i, j, count = 0;

    // Take two nested loop and
    // check weather rows already
    // get seen then increment
    // count by 1 then break the loop.
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < i; j++)
        {
            if (s[i] == s[j])
            {
                count++;
                break;
            }
        }
    }

    // Check if count>=1 then print No
    // Else print Yes.
    if (count >= 1)
    {
        document.write("No");
    }
    else
    {
        document.write("Yes");
    }
}

// Driver code.
var m = 3, n = 3;
var s = [ [ 1, 0, 1 ],
          [ 0, 0, 0 ],
          [ 1, 0, 0 ] ];

// Function calling
uniqueRows(s, m, n);

// This code is contributed by importantly

</script>
```

**Output:** 

```
Yes
```