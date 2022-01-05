# 对在范围[L，R]

内具有奇数频率的字符进行计数的查询

> 原文:[https://www . geesforgeks . org/query-to-count-characters-with-奇数频率范围-l-r/](https://www.geeksforgeeks.org/queries-to-count-characters-having-odd-frequency-in-a-range-l-r/)

给定长度为 **N** 的字符串 **S** ，由小写字母组成，并查询形式为**【L，R】**的 **Q[][]** ，任务是计算在范围【L，R】内出现奇数次的字符数。

**示例:**

> **输入:** S = "geeksforgeeks "，Q[][] = {{2，4}，{0，3}，{0，12}}
> **输出:** 3 2 3
> **解释:**
> 字符在[2，4]中出现奇数次:{'e '，' k '，' s'}。
> 在[0，3]中出现奇数次的字符:{'g '，' k'}。
> 在[0，12 ]中出现奇数次的字符:{'f '，' o '，' r'}。
> 
> **输入:** S = "hello "，Q[][] = {{0，4}}
> **输出:** 3
> **说明:**字符在[0，4]中出现奇数次:{'h '，' e '，' o'}。

**进场:**

按照以下步骤解决问题:

*   每个字符可以用唯一的 2 的幂来表示(按升序)。例如**2<sup>0</sup>T3 为**a '**，**2<sup>1</sup>T9 为**b '**以此类推，直至**2<sup>25</sup>T15 为**z '**。******
*   初始化一个大小为 **N** 的数组 **arr[]** ，其中 **arr[i]** 是 **S[i]** 的相应整数值。
*   构建大小为 **N** 的前缀数组**前缀[]** ，其中**前缀【I】**是对从**arr【0】**到**arr【I】**的所有数字执行的**异或**运算的值。
*   **{arr[L]，arr[L + 1]，…，arr[R–1]，arr[R]}** 的异或值中的[设定位数给出了给定范围 **[L，R]** 所需的答案。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to print the number
// of characters having odd
// frequencies for each query
void queryResult(int prefix[],
                 pair<int, int> Q)
{
    int l = Q.first;
    int r = Q.second;

    if (l == 0) {
        int xorval = prefix[r];
        cout << __builtin_popcount(xorval)
             << endl;
    }
    else {
        int xorval = prefix[r]
                     ^ prefix[l - 1];
        cout << __builtin_popcount(xorval)
             << endl;
    }
}

// A function to construct
// the arr[] and prefix[]
void calculateCount(string S,
                    pair<int, int> Q[],
                    int m)
{
    // Stores array length
    int n = S.length();

    // Stores the unique powers of 2
    // associated to each character
    int arr[n];
    for (int i = 0; i < n; i++) {
        arr[i] = (1 << (S[i] - 'a'));
    }

    // Prefix array to store the
    // XOR values from array elements
    int prefix[n];
    int x = 0;
    for (int i = 0; i < n; i++) {
        x ^= arr[i];
        prefix[i] = x;
    }

    for (int i = 0; i < m; i++) {
        queryResult(prefix, Q[i]);
    }
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    pair<int, int> Q[] = { { 2, 4 },
                           { 0, 3 },
                           { 0, 12 } };

    calculateCount(S, Q, 3);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above problem
import java.util.*;
class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to print the number
    // of characters having odd
    // frequencies for each query
    static void queryResult(int prefix[], pair Q)
    {
        int l = Q.first;
        int r = Q.second;
        if (l == 0)
        {
            int xorval = prefix[r];
            System.out.print(Integer.bitCount(xorval) + "\n");
        }
        else
        {
            int xorval = prefix[r] ^ prefix[l - 1];
            System.out.print(Integer.bitCount(xorval) + "\n");
        }
    }

    // A function to construct
    // the arr[] and prefix[]
    static void calculateCount(String S, pair Q[], int m)
    {

        // Stores array length
        int n = S.length();

        // Stores the unique powers of 2
        // associated to each character
        int[] arr = new int[n];
        for (int i = 0; i < n; i++)
        {
            arr[i] = (1 << (S.charAt(i) - 'a'));
        }

        // Prefix array to store the
        // XOR values from array elements
        int[] prefix = new int[n];
        int x = 0;
        for (int i = 0; i < n; i++)
        {
            x ^= arr[i];
            prefix[i] = x;
        }

        for (int i = 0; i < m; i++)
        {
            queryResult(prefix, Q[i]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "geeksforgeeks";
        pair Q[] = {new pair(2, 4),
                    new pair(0, 3), new pair(0, 12)};
        calculateCount(S, Q, 3);
    }
}
// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the number
# of characters having odd
# frequencies for each query
def queryResult(prefix, Q):

    l = Q[0]
    r = Q[1]

    if(l == 0):
        xorval = prefix[r]
        print(bin(xorval).count('1'))

    else:
        xorval = prefix[r] ^ prefix[l - 1]
        print(bin(xorval).count('1'))

# A function to construct
# the arr[] and prefix[]
def calculateCount(S, Q, m):

    # Stores array length
    n = len(S)

    # Stores the unique powers of 2
    # associated to each character
    arr = [0] * n
    for i in range(n):
        arr[i] = (1 << (ord(S[i]) - ord('a')))

    # Prefix array to store the
    # XOR values from array elements
    prefix = [0] * n
    x = 0

    for i in range(n):
        x ^= arr[i]
        prefix[i] = x

    for i in range(m):
        queryResult(prefix, Q[i])

# Driver Code
if __name__ == '__main__':

    S = "geeksforgeeks"

    # Function call
    Q = [ [ 2, 4 ],
          [ 0, 3 ],
          [ 0, 12 ] ]

    calculateCount(S, Q, 3)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above problem
using System;

class GFG{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to print the number
// of characters having odd
// frequencies for each query
static void queryResult(int []prefix, pair Q)
{
    int l = Q.first;
    int r = Q.second;

    if (l == 0)
    {
        int xorval = prefix[r];
        Console.Write(countSetBits(xorval) + "\n");
    }
    else
    {
        int xorval = prefix[r] ^ prefix[l - 1];
        Console.Write(countSetBits(xorval) + "\n");
    }
}

// A function to construct
// the []arr and prefix[]
static void calculateCount(String S, pair []Q,
                           int m)
{

    // Stores array length
    int n = S.Length;

    // Stores the unique powers of 2
    // associated to each character
    int[] arr = new int[n];
    for(int i = 0; i < n; i++)
    {
        arr[i] = (1 << (S[i] - 'a'));
    }

    // Prefix array to store the
    // XOR values from array elements
    int[] prefix = new int[n];
    int x = 0;

    for(int i = 0; i < n; i++)
    {
        x ^= arr[i];
        prefix[i] = x;
    }

    for(int i = 0; i < m; i++)
    {
        queryResult(prefix, Q[i]);
    }
}

static int countSetBits(long x)
{
    int setBits = 0;

    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "geeksforgeeks";
    pair []Q = { new pair(2, 4),
                 new pair(0, 3),
                 new pair(0, 12) };

    calculateCount(S, Q, 3);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript program to implement the above problem

    // Function to print the number
    // of characters having odd
    // frequencies for each query
    function queryResult(prefix, Q)
    {
        let l = Q[0];
        let r = Q[1];

        if (l == 0)
        {
            let xorval = prefix[r];
            document.write(countSetBits(xorval) + "</br>");
        }
        else
        {
            let xorval = prefix[r] ^ prefix[l - 1];
            document.write(countSetBits(xorval) + "</br>");
        }
    }

    // A function to construct
    // the []arr and prefix[]
    function calculateCount(S, Q, m)
    {

        // Stores array length
        let n = S.length;

        // Stores the unique powers of 2
        // associated to each character
        let arr = new Array(n);
        for(let i = 0; i < n; i++)
        {
            arr[i] = (1 << (S[i].charCodeAt() - 'a'.charCodeAt()));
        }

        // Prefix array to store the
        // XOR values from array elements
        let prefix = new Array(n);
        let x = 0;

        for(let i = 0; i < n; i++)
        {
            x ^= arr[i];
            prefix[i] = x;
        }

        for(let i = 0; i < m; i++)
        {
            queryResult(prefix, Q[i]);
        }
    }

    function countSetBits(x)
    {
        let setBits = 0;

        while (x != 0)
        {
            x = x & (x - 1);
            setBits++;
        }
        return setBits;
    }

    let S = "geeksforgeeks";
    let Q = [ [2, 4], [0, 3], [0, 12] ];

    calculateCount(S, Q, 3);

</script>
```

**Output:** 

```
3
2
3
```

***时间复杂度:** O(N + Q)*
***辅助空间:** O(N)*