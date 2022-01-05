# 查询给定范围内的所有元素是否出现偶数次

> 原文:[https://www . geesforgeks . org/query-to-check-给定索引范围内的所有元素是否出现偶数次/](https://www.geeksforgeeks.org/queries-to-check-whether-all-the-elements-in-the-given-index-range-occur-even-number-of-times/)

给定一个包含 **N** 整数的数组**arr【】**，并且存在 **Q** 查询，其中每个查询由一个范围**【L，R】**组成。任务是找出给定索引范围内的所有元素是否具有偶数频率。
**举例:**

> **输入:** arr[] = {1，1，2，2，1}，Q[][] = {{1，5}，{1，4}，{3，4}}
> **输出:**
> 否
> 是
> 是
> **输入:** arr[] = {100，100，200，100}，Q[]= { {1，4}，{ 1，2}}
> **输出**

**天真的方法:**一个简单的方法是从索引范围**【L，R】**为每个查询进行迭代，并计算该范围内每个元素的频率，检查每个元素是否出现偶数次。这种方法最差的时间复杂度是 **O(Q * N)** ，其中 **Q** 是查询的数量， **N** 是数组中元素的数量。
**有效方法:**由于两个相等数的异或为 **0** ，即如果数组的所有元素出现偶数次，那么整个数组的异或为 **0** 。给定范围内的元素**【L，R】**也是如此。现在，为了检查给定范围内所有元素的异或是否为 **0** ，可以创建前缀异或数组，其中 **preXor[i]** 将存储元素的异或 **arr[0…i]** 。并且元素**arr【I…j】**的异或可以容易地计算为**prexor【j】^ prexor【I–1】**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the given queries
void performQueries(vector<int>& A,
                    vector<pair<int, int> >& q)
{

    int n = (int)A.size();

    // Making array 1-indexed
    A.insert(A.begin(), 0);

    // To store the cumulative xor
    vector<int> pref_xor(n + 1, 0);

    // Taking cumulative Xor
    for (int i = 1; i <= n; ++i) {
        pref_xor[i]
            = pref_xor[i - 1] ^ A[i];
    }

    // Iterating over the queries
    for (auto i : q) {
        int L = i.first, R = i.second;
        if (L > R)
            swap(L, R);

        // If both indices are different and xor
        // in the range [L, R] is 0
        if (L != R and pref_xor[R] == pref_xor[L - 1])
            cout << "Yes\n";
        else
            cout << "No\n";
    }
}

// Driver code
int main()
{

    vector<int> Arr = { 1, 1, 2, 2, 1 };

    vector<pair<int, int> > q = {
        { 1, 5 },
        { 1, 4 },
        { 3, 4 }

    };

    performQueries(Arr, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to perform the given queries
static void performQueries(int []A,
                           pair[] q)
{
    int n = A.length;

    // To store the cumulative xor
    int []pref_xor = new int[n + 1];

    // Taking cumulative Xor
    for (int i = 1; i <=n; ++i)
    {
        pref_xor[i] = pref_xor[i - 1] ^
                             A[i - 1];
    }

    // Iterating over the queries
    for (pair i : q)
    {
        int L = i.first, R = i.second;
        if (L > R)
        {
            int temp = L;
            L = R;
            R = temp;
        }

        // If both indices are different and xor
        // in the range [L, R] is 0
        if (L != R && pref_xor[R] == pref_xor[L - 1])
            System.out.println("Yes");
    else
        System.out.println("No");
    }
}

// Driver code
static public void main (String []arg)
{
    int []Arr = { 1, 1, 2, 2, 1 };
    pair[] q = { new pair(1, 5 ),
                 new pair(1, 4 ),
                 new pair(3, 4 ) };

    performQueries(Arr, q);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to perform the given queries
def performQueries(A, q):

    n = len(A)

    # To store the cumulative xor
    pref_xor = [0 for i in range(n + 1)]

    # Taking cumulative Xor
    for i in range(1, n + 1):
        pref_xor[i] = pref_xor[i - 1] ^ A[i - 1]

    # Iterating over the queries
    for i in q:
        L = i[0]
        R = i[1]
        if (L > R):
            L, R = R, L

        # If both indices are different and
        # xor in the range [L, R] is 0
        if (L != R and
            pref_xor[R] == pref_xor[L - 1]):
            print("Yes")
        else:
            print("No")

# Driver code
Arr = [1, 1, 2, 2, 1]

q = [[ 1, 5 ],
     [ 1, 4 ],
     [ 3, 4 ]]

performQueries(Arr, q);

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to perform the given queries
static void performQueries(int []A,
                           pair[] q)
{
    int n = A.Length;

    // To store the cumulative xor
    int []pref_xor = new int[n + 1];

    // Taking cumulative Xor
    for (int i = 1; i <= n; ++i)
    {
        pref_xor[i] = pref_xor[i - 1] ^
                             A[i - 1];
    }

    // Iterating over the queries
    foreach (pair k in q)
    {
        int L = k.first, R = k.second;
        if (L > R)
        {
            int temp = L;
            L = R;
            R = temp;
        }

        // If both indices are different and xor
        // in the range [L, R] is 0
        if (L != R && pref_xor[R] == pref_xor[L - 1])
            Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
    }
}

// Driver code
static public void Main (String []arg)
{
    int []Arr = { 1, 1, 2, 2, 1 };
    pair[] q = {new pair(1, 5 ),
                new pair(1, 4 ),
                new pair(3, 4 )};

    performQueries(Arr, q);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to perform the given queries
function performQueries(A, q) {

    let n = A.length

    // To store the cumulative xor
    let pref_xor = new Array(n + 1).fill(0)

    // Taking cumulative Xor
    for (let i = 1; i < n + 1; i++) {
        pref_xor[i] = pref_xor[i - 1] ^ A[i - 1]
    }

    // Iterating over the queries
    for (let i in q) {
        let L = i[0]
        let R = i[1];
        if (L > R) {
            let temp = R;
            R = L;
            L = temp
        }

        // If both indices are different and
        // xor in the range [L, R] is 0
        if ((L != R) && (pref_xor[R] == pref_xor[L - 1]))
            document.write("No<br>")
        else
            document.write("Yes<br>")
    }
}
// Driver code
let Arr = [1, 1, 2, 2, 1]

let q = [[1, 5],
[1, 4],
[3, 4]]

performQueries(Arr, q);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
No
Yes
Yes
```

**时间复杂度:** O(N)

**辅助空间:** O(N)