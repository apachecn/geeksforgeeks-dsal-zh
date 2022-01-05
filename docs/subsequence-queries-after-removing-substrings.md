# 删除子字符串后的子序列查询

> 原文:[https://www . geeksforgeeks . org/subsequence-查询-删除后-子字符串/](https://www.geeksforgeeks.org/subsequence-queries-after-removing-substrings/)

给定两个字符串 A 和 B，问题是如果我们去掉子字符串[A[i]，那么字符串 B 是否会是字符串 A 的子序列..假设有 Q 个查询给出了索引 I 和 j，并且每个查询都是相互独立的。
**例:**

```
Input : A = abcabcxy, B = acy
        Q = 2
        i = 2, j = 5
        i = 3, j = 6
Output :
Yes
No
Explanation :
In the first query we remove A[2]..A[5], 
getting acxy and acy is its subsequence.

In the second query we remove A[3]..A[6], 
getting abxy but acy is not its subsequence.
```

一种**蛮力**的方法是，对于每个查询，从 A 中移除所需的子串，并且[检查 B 是否是 A 的子序列](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)，但是这是低效的，因为我们必须为每个查询修改字符串 A，并且还要检查字符串 B 是否是它的子序列。
更有效的方法**是对字符串进行预处理，因为我们必须遇到多个查询。我们可以将字符串 B 中匹配的字符数存储在两个独立的数组中，直到字符串 A 的前向和后向的每个索引。最后我们可以说答案是肯定的，如果下面的等式成立，否则就是否定的:
向前[i-1] +向后[j+1] > =长度(B)。
这很有效，因为我们正在移除 A[i]..A[j]来自 A，想知道 A 中匹配的 B 的字符数之和
来自 A[1]..A[i-1]和 A[j+1]..A[len]，如果这个和至少是字符串 b 的长度，它就是一个子序列。
下面是上述方法的实现:** 

## C++

```
// CPP program for answering queries to check
// whether a string subsequence or not after
// removing a substring.
#include <bits/stdc++.h>
using namespace std;

// arrays to store results of preprocessing
int *fwd, *bwd;

// function to preprocess the strings
void preProcess(string a, string b)
{
    int n = a.size();

    // Allocate memory for fwd and bwd, and
    // initialize it as 0.
    fwd = new int[n]();
    bwd = new int[n]();

    int j = 0;

    // store subsequence count in forward direction
    for (int i = 1; i <= a.size(); i++) {
        if (j < b.size() && a[i - 1] == b[j])
            j++;

        // store number of matches till now
        fwd[i] = j;
    }

    j = 0;

    // store subsequence count in backward direction
    for (int i = a.size(); i >= 1; i--) {
        if (j < b.size() &&
            a[i - 1] == b[b.size() - j - 1])
            j++;

        // store number of matches till now
        bwd[i] = j;
    }
}

// function that gives the output
void query(string a, string b, int x, int y)
{
    // length of remaining string A is less
    // than B's length
    if ((x - 1 + a.size() - y) < b.size()) {
        cout << "No\n";
        return;
    }

    if (fwd[x - 1] + bwd[y + 1] >= b.size())
        cout << "Yes\n";
    else
        cout << "No\n";
}

// driver function
int main()
{
    string a = "abcabcxy", b = "acy";
    preProcess(a, b);

    // two queries
    int x = 2, y = 5;
    query(a, b, x, y);

    x = 3, y = 6;
    query(a, b, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for answering
// queries to check whether
// a String subsequence or
// not after removing a substring.

class GFG
{
    // arrays to store results
    // of preprocessing

    static int[] fwd = new int[100];
    static int[] bwd = new int[100];

    // function to preprocess
    // the strings
    static void preProcess(String a,
                            String b)
    {
        int n = a.length();

        // initialize it as 0.
        int j = 0;

        // store subsequence count
        // in forward direction
        for (int i = 1;
                i <= a.length(); i++)
        {
            if (j < b.length() &&
                a.charAt(i - 1) == b.charAt(j))
            {
                j++;
            }

            // store number of
            // matches till now
            fwd[i] = j;
        }

        j = 0;

        // store subsequence count
        // in backward direction
        for (int i = a.length(); i >= 1; i--)
        {
            if (j < b.length() && a.charAt(i - 1) ==
                    b.charAt(b.length() - j - 1))
            {
                j++;
            }

            // store number of
            // matches till now
            bwd[i] = j;
        }
    }

    // function that gives
    // the output
    static void query(String a, String b,
                            int x, int y)
    {
        // length of remaining
        // String A is less
        // than B's length
        if ((x - 1 + a.length() - y) < b.length())
        {
            System.out.print("No\n");
            return;
        }

        if (fwd[x - 1] + bwd[y + 1] >= b.length())
        {
            System.out.print("Yes\n");
        }
        else
        {
            System.out.print("No\n");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        String a = "abcabcxy", b = "acy";
        preProcess(a, b);

        // two queries
        int x = 2, y = 5;
        query(a, b, x, y);

        x = 3;
        y = 6;
        query(a, b, x, y);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for answering
# queries to check whether
# a String subsequence or
# not after removing a substring.

# arrays to store results
# of preprocessing
fwd = [0] * 100
bwd = [0] * 100

# function to preprocess
# the strings
def preProcess(a, b):
    n = len(a)

    # initialize it as 0.
    j = 0

    # store subsequence count
    # in forward direction
    for i in range(1, len(a) + 1):
        if j < len(b) and a[i - 1] == b[j]:
            j += 1

        # store number of
        # matches till now
        fwd[i] = j

    j = 0

    # store subsequence count
    # in backward direction
    for i in range(len(a), 0, -1):
        if (j < len(b) and
            a[i - 1] == b[len(b) - j - 1]):
            j += 1

        # store number of
        # matches till now
        bwd[i] = j

# function that gives
# the output
def query(a, b, x, y):

    # length of remaining
    # String A is less
    # than B's length
    if (x - 1 + len(a) - y) < len(b):
        print("No")
        return

    if (fwd[x - 1] + bwd[y + 1]) >= len(b):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == "__main__":
    a = "abcabcxy"
    b = "acy"
    preProcess(a, b)

    x = 2
    y = 5

    query(a, b, x, y)

    x = 3
    y = 6
    query(a, b, x, y)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for answering
// queries to check whether
// a string subsequence or
// not after removing a substring.
using System;

class GFG
{
    // arrays to store results
    // of preprocessing
    static int []fwd = new int[100];
    static int []bwd = new int[100];

    // function to preprocess
    // the strings
    static void preProcess(string a,
                           string b)
    {
        int n = a.Length;

        // initialize it as 0.
        int j = 0;

        // store subsequence count
        // in forward direction
        for (int i = 1;
                 i <= a.Length; i++)
        {
            if (j < b.Length &&
                    a[i - 1] == b[j])
                j++;

            // store number of
            // matches till now
            fwd[i] = j;
        }

        j = 0;

        // store subsequence count
        // in backward direction
        for (int i = a.Length;
                 i >= 1; i--)
        {
            if (j < b.Length &&
                a[i - 1] == b[b.Length - j - 1])
                j++;

            // store number of
            // matches till now
            bwd[i] = j;
        }
    }

    // function that gives
    // the output
    static void query(string a, string b,
                      int x, int y)
    {
        // length of remaining
        // string A is less
        // than B's length
        if ((x - 1 + a.Length - y) < b.Length)
        {
            Console.Write("No\n");
            return;
        }

        if (fwd[x - 1] +
            bwd[y + 1] >= b.Length)
            Console.Write("Yes\n");
        else
            Console.Write("No\n");
    }

    // Driver Code
    static void Main()
    {
        string a = "abcabcxy", b = "acy";
        preProcess(a, b);

        // two queries
        int x = 2, y = 5;
        query(a, b, x, y);

        x = 3; y = 6;
        query(a, b, x, y);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>
// Javascript program for answering
// queries to check whether
// a String subsequence or
// not after removing a substring.

// arrays to store results
// of preprocessing
let fwd = new Array(100);
let bwd = new Array(100);

// function to preprocess
// the strings
function preProcess(a,b)
{
    let n = a.length;

        // initialize it as 0.
        let j = 0;

        // store subsequence count
        // in forward direction
        for (let i = 1;
                i <= a.length; i++)
        {
            if (j < b.length &&
                a[i - 1] == b[j])
            {
                j++;
            }

            // store number of
            // matches till now
            fwd[i] = j;
        }

        j = 0;

        // store subsequence count
        // in backward direction
        for (let i = a.length; i >= 1; i--)
        {
            if (j < b.length && a[i-1] ==
                    b[b.length - j - 1])
            {
                j++;
            }

            // store number of
            // matches till now
            bwd[i] = j;
        }
}

// function that gives
// the output
function query(a,b,x,y)
{
    // length of remaining
        // String A is less
        // than B's length
        if ((x - 1 + a.length - y) < b.length)
        {
            document.write("No<br>");
            return;
        }

        if (fwd[x - 1] + bwd[y + 1] >= b.length)
        {
            document.write("Yes<br>");
        }
        else
        {
            document.write("No<br>");
        }
}

// Driver Code
let a = "abcabcxy", b = "acy";
preProcess(a, b);

// two queries
let x = 2, y = 5;
query(a, b, x, y);

x = 3;
y = 6;
query(a, b, x, y);

// This code is contributed by rag2127
</script>
```

**输出:**

```
Yes
No
```

上述方法的**时间复杂度**为 O(n + q)，其中 q 为查询数，n 为字符串 a 的长度