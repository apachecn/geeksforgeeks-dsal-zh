# 查询给定字符串在恒定时间内的旋转和第 k 个字符

> 原文:[https://www . geeksforgeeks . org/查询给定字符串的旋转和固定字符数/](https://www.geeksforgeeks.org/queries-for-rotation-and-kth-character-of-the-given-string-in-constant-time/)

给定一个字符串 **str** ，任务是对给定的字符串执行以下类型的查询:

1.  **(1，K):** 向左旋转 **K** 字符。
2.  **(2，K):** 打印字符串的 **K <sup>第</sup>个**字符。

**例:**

> **输入:** str = "abcdefgh "，q[][] = {{1，2}，{2，2}，{1，4}，{2，7}}
> **输出:**
> d
> e
> 查询 1: str = "cdefghab"
> 查询 2: 2 <sup>nd</sup> 字符为 d
> 查询 3: str = "ghabcdef"
> 查询 4: 7 <sup>th</sup>

**方法:**这里的主要观察是字符串不需要在每个查询中旋转，相反我们可以创建一个指针 **ptr** 指向字符串的第一个字符，并且可以为每个旋转更新为 **ptr = (ptr + K) % N** ，其中 **K** 是字符串需要旋转的整数，而 **N** 是字符串的长度。现在对于第二种类型的每一个查询， **K <sup>第</sup>** 个字符可以通过**str[(ptr+K–1)% N]**找到。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define size 2

// Function to perform the required
// queries on the given string
void performQueries(string str, int n,
                    int queries[][size], int q)
{

    // Pointer pointing to the current starting
    // character of the string
    int ptr = 0;

    // For every query
    for (int i = 0; i < q; i++) {

        // If the query is to rotate the string
        if (queries[i][0] == 1) {

            // Update the pointer pointing to the
            // starting character of the string
            ptr = (ptr + queries[i][1]) % n;
        }
        else {

            int k = queries[i][1];

            // Index of the kth character in the
            // current rotation of the string
            int index = (ptr + k - 1) % n;

            // Print the kth character
            cout << str[index] << "\n";
        }
    }
}

// Driver code
int main()
{
    string str = "abcdefgh";
    int n = str.length();

    int queries[][size] = { { 1, 2 }, { 2, 2 },
                            { 1, 4 }, { 2, 7 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    performQueries(str, n, queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{
static int size = 2;

// Function to perform the required
// queries on the given string
static void performQueries(String str, int n,
                           int queries[][], int q)
{

    // Pointer pointing to the current
    // starting character of the string
    int ptr = 0;

    // For every query
    for (int i = 0; i < q; i++)
    {

        // If the query is to rotate the string
        if (queries[i][0] == 1)
        {

            // Update the pointer pointing to the
            // starting character of the string
            ptr = (ptr + queries[i][1]) % n;
        }
        else
        {
            int k = queries[i][1];

            // Index of the kth character in the
            // current rotation of the string
            int index = (ptr + k - 1) % n;

            // Print the kth character
            System.out.println(str.charAt(index));
        }
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "abcdefgh";
    int n = str.length();

    int queries[][] = { { 1, 2 }, { 2, 2 },
                        { 1, 4 }, { 2, 7 } };
    int q = queries.length;

    performQueries(str, n, queries, q);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
size = 2

# Function to perform the required
# queries on the given string
def performQueries(string, n, queries, q) :

    # Pointer pointing to the current starting
    # character of the string
    ptr = 0;

    # For every query
    for i in range(q) :

        # If the query is to rotate the string
        if (queries[i][0] == 1) :

            # Update the pointer pointing to the
            # starting character of the string
            ptr = (ptr + queries[i][1]) % n;

        else :

            k = queries[i][1];

            # Index of the kth character in the
            # current rotation of the string
            index = (ptr + k - 1) % n;

            # Print the kth character
            print(string[index]);

# Driver code
if __name__ == "__main__" :

    string = "abcdefgh";
    n = len(string);

    queries = [[ 1, 2 ], [ 2, 2 ],
               [ 1, 4 ], [ 2, 7 ]];
    q = len(queries);

    performQueries(string, n, queries, q);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int size = 2;

// Function to perform the required
// queries on the given string
static void performQueries(String str, int n,
                           int [,]queries, int q)
{

    // Pointer pointing to the current
    // starting character of the string
    int ptr = 0;

    // For every query
    for (int i = 0; i < q; i++)
    {

        // If the query is to rotate the string
        if (queries[i, 0] == 1)
        {

            // Update the pointer pointing to the
            // starting character of the string
            ptr = (ptr + queries[i, 1]) % n;
        }
        else
        {
            int k = queries[i, 1];

            // Index of the kth character in the
            // current rotation of the string
            int index = (ptr + k - 1) % n;

            // Print the kth character
            Console.WriteLine(str[index]);
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "abcdefgh";
    int n = str.Length;

    int [,]queries = { { 1, 2 }, { 2, 2 },
                       { 1, 4 }, { 2, 7 } };
    int q = queries.GetLength(0);

    performQueries(str, n, queries, q);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var size = 2;

// Function to perform the required
// queries on the given string
function performQueries(str, n, queries, q)
{

    // Pointer pointing to the current starting
    // character of the string
    var ptr = 0;

    // For every query
    for (var i = 0; i < q; i++) {

        // If the query is to rotate the string
        if (queries[i][0] == 1) {

            // Update the pointer pointing to the
            // starting character of the string
            ptr = (ptr + queries[i][1]) % n;
        }
        else {

            var k = queries[i][1];

            // Index of the kth character in the
            // current rotation of the string
            var index = (ptr + k - 1) % n;

            // Print the kth character
            document.write( str[index] + "<br>");
        }
    }
}

// Driver code
var str = "abcdefgh";
var n = str.length;
var queries = [ [ 1, 2 ], [ 2, 2 ],
                        [ 1, 4 ], [ 2, 7 ] ];
var q = queries.length;
performQueries(str, n, queries, q);

</script>
```

**Output:** 

```
d
e
```