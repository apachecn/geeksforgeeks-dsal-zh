# 字符串中取决于频率计数的字符索引

> 原文:[https://www . geeksforgeeks . org/字符串中基于频率的字符索引/](https://www.geeksforgeeks.org/index-of-character-depending-on-frequency-count-in-string/)

给定一个只包含小写字符的字符串 **str** ，任务是回答以下类型的 **Q** 查询:

1.  **1 C X:** 找到最大的 **i** 使得**str【0…I】**正好有 **X** 字符 **C** 的出现。
2.  **2 C X:** 找到最小的 **i** ，这样**str【0…I】**正好有 **X** 字符 **C** 的出现。

**例:**

> **输入:** str = "geeksforgeeks "，query[] = {{1，' e '，2}，{2，' k '，2}}
> **输出:**
> 8
> 11
> 查询 1:“geeks org”是从 str[0]开始的最大子串，其中' e '恰好出现了两次，最后一个字符的索引为 8。
> 查询 2:“geeksforgeek”是从 str[0]开始的最小子串，其中‘k’恰好出现两次，最后一个字符的索引为 11。
> **输入:** str = "abcdabcd "，查询[] = {{1，' a '，1}，{2，' a '，2}}
> **输出:**
> 3
> 4

**方法:**创建两个二维数组 **L[][]** 和 **F[][]** ，使得 **L[i][j]** 存储最大的 **i** ，使得 **i <sup>第</sup>T13】字符在 **str[0…i]** 和 **F[i][j]中精确出现 **j <sup>第</sup>T17】次为此，遍历整个字符串并保持一个频率数组，以便对于每个迭代/字符，更新其计数，然后开始从 **0** 到 **26** 的另一个循环(每个字母 a-z)。在内循环中，如果迭代器等于字符值，则使用外循环迭代器用当前索引位置更新 **L[][]** 和 **F[][]** 数组，否则只需将其他字符的 **L[][]** 数组值增加 **1** ，因为只有索引增加了，字符没有出现。现在，类型 1 查询可以回答为 **L【给定字符】【频率计数】**，类型 2 查询可以回答为 **F【给定字符】【频率计数】**。
以下是上述办法的实施情况。****** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to perform the queries
void performQueries(string str, int q, int type[],
                    char ch[], int freq[])
{

    int n = str.length();

    // L[i][j] stores the largest i
    // such that ith character appears
    // exactly jth times in str[0...i]
    int L[MAX][n];

    // F[i][j] stores the smallest i
    // such that ith character appears
    // exactly jth times in str[0...i]
    int F[MAX][n];

    // To store the frequency of each
    // of the character of str
    int cnt[MAX] = { 0 };
    for (int i = 0; i < n; i++) {

        // Current character of str
        int k = str[i] - 'a';

        // Update its frequency
        cnt[k]++;

        // For every lowercase character
        // of the English alphabet
        for (int j = 0; j < MAX; j++) {

            // If it is equal to the character
            // under consideration then update
            // L[][] and R[][] as it is cnt[j]th
            // occurrence of character k
            if (k == j) {
                L[j][cnt[j]] = i;
                F[j][cnt[j]] = i;
            }

            // Only update L[][] as k has not
            // been occurred so only index
            // has to be incremented
            else
                L[j][cnt[j]] = L[j][cnt[j]] + 1;
        }
    }

    // Perform the queries
    for (int i = 0; i < q; i++) {

        // Type 1 query
        if (type[i] == 1) {
            cout << L[ch[i] - 'a'][freq[i]];
        }

        // Type 2 query
        else {
            cout << F[ch[i] - 'a'][freq[i]];
        }

        cout << "\n";
    }
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    // Queries
    int type[] = { 1, 2 };
    char ch[] = { 'e', 'k' };
    int freq[] = { 2, 2 };
    int q = sizeof(type) / sizeof(int);

    // Perform the queries
    performQueries(str, q, type, ch, freq);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MAX = 26;

// Function to perform the queries
static void performQueries(String str, int q, int type[],
                                   char ch[], int freq[])
{
    int n = str.length();

    // L[i][j] stores the largest i
    // such that ith character appears
    // exactly jth times in str[0...i]
    int [][]L = new int[MAX][n];

    // F[i][j] stores the smallest i
    // such that ith character appears
    // exactly jth times in str[0...i]
    int [][]F = new int[MAX][n];

    // To store the frequency of each
    // of the character of str
    int []cnt = new int[MAX];
    for (int i = 0; i < n; i++)
    {

        // Current character of str
        int k = str.charAt(i) - 'a';

        // Update its frequency
        cnt[k]++;

        // For every lowercase character
        // of the English alphabet
        for (int j = 0; j < MAX; j++)
        {

            // If it is equal to the character
            // under consideration then update
            // L[][] and R[][] as it is cnt[j]th
            // occurrence of character k
            if (k == j)
            {
                L[j][cnt[j]] = i;
                F[j][cnt[j]] = i;
            }

            // Only update L[][] as k has not
            // been occurred so only index
            // has to be incremented
            else
                L[j][cnt[j]] = L[j][cnt[j]] + 1;
        }
    }

    // Perform the queries
    for (int i = 0; i < q; i++)
    {

        // Type 1 query
        if (type[i] == 1)
        {
            System.out.print(L[ch[i] - 'a'][freq[i]]);
        }

        // Type 2 query
        else
        {
            System.out.print(F[ch[i] - 'a'][freq[i]]);
        }
        System.out.print("\n");
    }
}

// Driver code
public static void main(String []args)
{
    String str = "geeksforgeeks";

    // Queries
    int type[] = { 1, 2 };
    char ch[] = { 'e', 'k' };
    int freq[] = { 2, 2 };
    int q = type.length;

    // Perform the queries
    performQueries(str, q, type, ch, freq);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

MAX = 26;

# Function to perform the queries
def performQueries(string , q, type_arr, ch, freq) :

    n = len(string);

    # L[i][j] stores the largest i
    # such that ith character appears
    # exactly jth times in str[0...i]
    L = np.zeros((MAX, n));

    # F[i][j] stores the smallest i
    # such that ith character appears
    # exactly jth times in str[0...i]
    F = np.zeros((MAX, n));

    # To store the frequency of each
    # of the character of str
    cnt = [ 0 ] * MAX;
    for i in range(n) :

        # Current character of str
        k = ord(string[i]) - ord('a');

        # Update its frequency
        cnt[k] += 1;

        # For every lowercase character
        # of the English alphabet
        for j in range(MAX) :

            # If it is equal to the character
            # under consideration then update
            # L[][] and R[][] as it is cnt[j]th
            # occurrence of character k
            if (k == j) :
                L[j][cnt[j]] = i;
                F[j][cnt[j]] = i;

            # Only update L[][] as k has not
            # been occurred so only index
            # has to be incremented
            else :
                L[j][cnt[j]] = L[j][cnt[j]] + 1;

    # Perform the queries
    for i in range(q) :

        # Type 1 query
        if (type_arr[i] == 1) :
            print(L[ord(ch[i]) -
                    ord('a')][freq[i]], end = "");

        # Type 2 query
        else :
            print(F[ord(ch[i]) -
                    ord('a')][freq[i]], end = "");

        print()

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";

    # Queries
    type_arr = [ 1, 2 ];
    ch = [ 'e', 'k' ];
    freq = [ 2, 2 ];
    q = len(type_arr);

    # Perform the queries
    performQueries(string, q, type_arr, ch, freq);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 26;

// Function to perform the queries
static void performQueries(String str, int q, int []type,
                                     char []ch, int []freq)
{
    int n = str.Length;

    // L[i,j] stores the largest i
    // such that ith character appears
    // exactly jth times in str[0...i]
    int [,]L = new int[MAX, n];

    // F[i,j] stores the smallest i
    // such that ith character appears
    // exactly jth times in str[0...i]
    int [,]F = new int[MAX, n];

    // To store the frequency of each
    // of the character of str
    int []cnt = new int[MAX];
    for (int i = 0; i < n; i++)
    {

        // Current character of str
        int k = str[i] - 'a';

        // Update its frequency
        cnt[k]++;

        // For every lowercase character
        // of the English alphabet
        for (int j = 0; j < MAX; j++)
        {

            // If it is equal to the character
            // under consideration then update
            // L[,] and R[,] as it is cnt[j]th
            // occurrence of character k
            if (k == j)
            {
                L[j, cnt[j]] = i;
                F[j, cnt[j]] = i;
            }

            // Only update L[,] as k has not
            // been occurred so only index
            // has to be incremented
            else
                L[j, cnt[j]] = L[j, cnt[j]] + 1;
        }
    }

    // Perform the queries
    for (int i = 0; i < q; i++)
    {

        // Type 1 query
        if (type[i] == 1)
        {
            Console.Write(L[ch[i] - 'a', freq[i]]);
        }

        // Type 2 query
        else
        {
            Console.Write(F[ch[i] - 'a', freq[i]]);
        }
        Console.Write("\n");
    }
}

// Driver code
public static void Main(String []args)
{
    String str = "geeksforgeeks";

    // Queries
    int []type = { 1, 2 };
    char []ch = { 'e', 'k' };
    int []freq = { 2, 2 };
    int q = type.Length;

    // Perform the queries
    performQueries(str, q, type, ch, freq);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MAX = 26;

    // Function to perform the queries
    function performQueries(str, q, type, ch, freq)
    {
        let n = str.length;

        // L[i][j] stores the largest i
        // such that ith character appears
        // exactly jth times in str[0...i]
        let L = new Array(MAX);

        // F[i][j] stores the smallest i
        // such that ith character appears
        // exactly jth times in str[0...i]
        let F = new Array(MAX);

        // To store the frequency of each
        // of the character of str
        let cnt = new Array(MAX);

        for (let i = 0; i < MAX; i++)
        {
            L[i] = new Array(n);
            F[i] = new Array(n);
            cnt[i] = 0;
            for (let j = 0; j < n; j++)
            {
                L[i][j] = 0;
                F[i][j] = 0;
            }
        }

        for (let i = 0; i < n; i++)
        {

            // Current character of str
            let k = str[i].charCodeAt() - 'a'.charCodeAt();

            // Update its frequency
            cnt[k]++;

            // For every lowercase character
            // of the English alphabet
            for (let j = 0; j < MAX; j++)
            {

                // If it is equal to the character
                // under consideration then update
                // L[][] and R[][] as it is cnt[j]th
                // occurrence of character k
                if (k == j)
                {
                    L[j][cnt[j]] = i;
                    F[j][cnt[j]] = i;
                }

                // Only update L[][] as k has not
                // been occurred so only index
                // has to be incremented
                else
                    L[j][cnt[j]] = L[j][cnt[j]] + 1;
            }
        }

        // Perform the queries
        for (let i = 0; i < q; i++)
        {

            // Type 1 query
            if (type[i] == 1)
            {
                document.write(L[ch[i].charCodeAt() -
                'a'.charCodeAt()][freq[i]]);
            }

            // Type 2 query
            else
            {
                document.write(F[ch[i].charCodeAt() -
                'a'.charCodeAt()][freq[i]]);
            }
            document.write("</br>");
        }
    }

    let str = "geeksforgeeks";

    // Queries
    let type = [ 1, 2 ];
    let ch = [ 'e', 'k' ];
    let freq = [ 2, 2 ];
    let q = type.length;

    // Perform the queries
    performQueries(str, q, type, ch, freq);

</script>
```

**Output:** 

```
8
11
```

**时间复杂度:** O(n)其中 n 是字符串的长度。