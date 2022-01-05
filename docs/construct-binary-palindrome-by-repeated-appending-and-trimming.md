# 通过反复追加和修剪

构建二进制回文

> 原文:[https://www . geesforgeks . org/construct-binary-回文-by-repeating-and-trim/](https://www.geeksforgeeks.org/construct-binary-palindrome-by-repeated-appending-and-trimming/)

给定 n 和 k，用一个大小为 k 的二进制数构造一个大小为 n 的回文，重复它自己来包装回文。**回文必须始终以 1 开头，并且包含最大数量的零。**
**例:**

```
Input : n = 5,  k = 3
Output : 11011 
Explanation : the 3 sized substring is
110 combined twice and trimming the extra 
0 in the end to give 11011.

Input : n = 2,  k = 8
Output : 11 
Explanation : the 8 sized substring is 11...... 
wrapped to two places to give 11.
```

天真的方法是尝试从 1 开始的每个大小为 k 的回文，这样就形成了一个大小为 n 的回文。这种方法具有指数级的复杂性。
A **更好的方法**是用索引初始化 k 大小的二进制数，并按照应该的方式连接回文。像回文的最后一个字符应该首先匹配，找到哪些索引将出现在这些位置，并链接它们。将与第 0 个索引链接的每个字符设置为 1，字符串就准备好了。这种方法将具有线性复杂性。
在这种方法中，首先将 k 大小的二进制文件的索引放入一个数组中，例如，如果 n = 7，k = 3 arr 变成[0，1，2，0，1，2，0]。接下来，在 connectchars 图中，通过遍历回文的性质来连接 k 大小的二进制数的索引，该二进制数应该相同，并且第(n–k–1)个变量应该相同，例如 0 链接到 1(反之亦然)，1 链接到 2(反之亦然)等等。之后，检查 connectchars 数组中与 0 链接的内容，并使用 dfs 方法将所有关联的索引都设为 1(因为第一个数字应该是非零)。在 dfs 中，传递 0、最终答案字符串和图表。首先，将父项设为 1，并检查其子项是否为零，如果是，则将父项和子项设为 1。这使得只有 k 大小的字符串的所需索引为 1，其他索引为零。最后，答案包含 0 到 k–1 的索引，对应于 arr 的数字被打印出来。

## C++

```
// CPP code to form binary palindrome
#include <iostream>
#include <vector>
using namespace std;

// function to apply DFS
void dfs(int parent, int ans[], vector<int> connectchars[])
{
    // set the parent marked
    ans[parent] = 1;

    // if the node has not been visited set it and
    // its children marked
    for (int i = 0; i < connectchars[parent].size(); i++) {
        if (!ans[connectchars[parent][i]])
            dfs(connectchars[parent][i], ans, connectchars);
    }
}

void printBinaryPalindrome(int n, int k)
{
    int arr[n], ans[n] = { 0 };

    // link which digits must be equal
    vector<int> connectchars[k];

    for (int i = 0; i < n; i++)
        arr[i] = i % k;

    // connect the two indices
    for (int i = 0; i < n / 2; i++) {
        connectchars[arr[i]].push_back(arr[n - i - 1]);
        connectchars[arr[n - i - 1]].push_back(arr[i]);
    }

    // set everything connected to
    // first character as 1
    dfs(0, ans, connectchars);

    for (int i = 0; i < n; i++)
        cout << ans[arr[i]];
}

// driver code
int main()
{
    int n = 10, k = 4;
    printBinaryPalindrome(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to form binary palindrome
import java.util.*;

class GFG
{

// function to apply DFS
static void dfs(int parent, int ans[],
                Vector<Integer> connectchars[])
{
    // set the parent marked
    ans[parent] = 1;

    // if the node has not been visited set it and
    // its children marked
    for (int i = 0; i < connectchars[parent].size(); i++)
    {
        if (ans[connectchars[parent].get(i)] != 1)
            dfs(connectchars[parent].get(i), ans, connectchars);
    }
}

static void printBinaryPalindrome(int n, int k)
{
    int []arr = new int[n];
    int []ans = new int[n];

    // link which digits must be equal
    Vector<Integer> []connectchars = new Vector[k];
    for (int i = 0; i < k; i++)
        connectchars[i] = new Vector<Integer>();
    for (int i = 0; i < n; i++)
        arr[i] = i % k;

    // connect the two indices
    for (int i = 0; i < n / 2; i++)
    {
        connectchars[arr[i]].add(arr[n - i - 1]);
        connectchars[arr[n - i - 1]].add(arr[i]);
    }

    // set everything connected to
    // first character as 1
    dfs(0, ans, connectchars);

    for (int i = 0; i < n; i++)
        System.out.print(ans[arr[i]]);
}

// Driver code
public static void main(String[] args)
{
    int n = 10, k = 4;
    printBinaryPalindrome(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 code to form binary palindrome

# function to apply DFS
def dfs(parent, ans, connectchars):

    # set the parent marked
    ans[parent] = 1

    # if the node has not been visited
    # set it and its children marked
    for i in range(len(connectchars[parent])):
        if (not ans[connectchars[parent][i]]):
            dfs(connectchars[parent][i], ans,
                             connectchars)

def printBinaryPalindrome(n, k):
    arr = [0] * n
    ans = [0] * n

    # link which digits must be equal
    connectchars = [[] for i in range(k)]

    for i in range(n):
        arr[i] = i % k

    # connect the two indices
    for i in range(int(n / 2)):
        connectchars[arr[i]].append(arr[n - i - 1])
        connectchars[arr[n - i - 1]].append(arr[i])

    # set everything connected to
    # first character as 1
    dfs(0, ans, connectchars)

    for i in range(n):
        print(ans[arr[i]], end = "")

# Driver Code
if __name__ == '__main__':

    n = 10
    k = 4
    printBinaryPalindrome(n, k)

# This code is contributed by PranchalK
```

## C#

```
// C# code to form binary palindrome
using System;
using System.Collections.Generic;

class GFG
{

// function to apply DFS
static void dfs(int parent, int []ans,
                List<int> []connectchars)
{
    // set the parent marked
    ans[parent] = 1;

    // if the node has not been visited set it and
    // its children marked
    for (int i = 0; i < connectchars[parent].Count; i++)
    {
        if (ans[connectchars[parent][i]] != 1)
            dfs(connectchars[parent][i], ans, connectchars);
    }
}

static void printBinaryPalindrome(int n, int k)
{
    int []arr = new int[n];
    int []ans = new int[n];

    // link which digits must be equal
    List<int> []connectchars = new List<int>[k];
    for (int i = 0; i < k; i++)
        connectchars[i] = new List<int>();
    for (int i = 0; i < n; i++)
        arr[i] = i % k;

    // connect the two indices
    for (int i = 0; i < n / 2; i++)
    {
        connectchars[arr[i]].Add(arr[n - i - 1]);
        connectchars[arr[n - i - 1]].Add(arr[i]);
    }

    // set everything connected to
    // first character as 1
    dfs(0, ans, connectchars);

    for (int i = 0; i < n; i++)
        Console.Write(ans[arr[i]]);
}

// Driver code
public static void Main(String[] args)
{
    int n = 10, k = 4;
    printBinaryPalindrome(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript code to form binary palindrome

// function to apply DFS
function dfs(parent, ans, connectchars) {
    // set the parent marked
    ans[parent] = 1;

    // if the node has not been visited set it and
    // its children marked
    for (let i = 0; i < connectchars[parent].length; i++) {
        if (!ans[connectchars[parent][i]])
            dfs(connectchars[parent][i], ans, connectchars);
    }
}

function printBinaryPalindrome(n, k) {
    let arr = new Array(n), ans = new Array(n).fill(0);

    // link which digits must be equal
    let connectchars = new Array(k).fill(0).map(() => new Array(k).fill(0));

    for (let i = 0; i < n; i++)
        arr[i] = i % k;

    // connect the two indices
    for (let i = 0; i < n / 2; i++) {
        connectchars[arr[i]].push(arr[n - i - 1]);
        connectchars[arr[n - i - 1]].push(arr[i]);
    }

    // set everything connected to
    // first character as 1
    dfs(0, ans, connectchars);

    for (let i = 0; i < n; i++)
        document.write(ans[arr[i]]);
}

// driver code

let n = 10, k = 4;
printBinaryPalindrome(n, k);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
1100110011
```

时间复杂度:O(n)