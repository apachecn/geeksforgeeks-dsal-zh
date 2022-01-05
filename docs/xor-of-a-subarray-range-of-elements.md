# 子阵列(元素范围)的异或运算

> 原文:[https://www . geeksforgeeks . org/子数组元素范围异或/](https://www.geeksforgeeks.org/xor-of-a-subarray-range-of-elements/)

给定 n 个整数的数组 arr[]和一些查询。每个查询的形式都是(L，R)，其中 L 和 R 是数组的索引。求子阵 arr[L…R]的异或值，即当[L，R]范围内的所有元素都异或时得到的值。假设从 0 开始索引，并且每个数组元素都是 32 位无符号整数。
**例:**

```
Input : arr[] = {2, 5, 1, 6, 1, 2, 5}
        L =  1, R = 4
Output : 3
The XOR value of arr[1...4] is 3.

Input : arr[] = {2, 5, 1, 6, 1, 2, 5}
        L = 0, R = 6
Output : 6
The XOR value of arr[0...6] is 6.
```

**方法:**
一个**简单的**解决方案是为每个查询遍历给定数组从索引 L 到索引 R。这导致处理每个查询的时间复杂度为 O(n)。如果有 q 个查询，那么需要的总时间将是 O(q*n)。对于大量查询和大型数组，这种解决方案并不是最优的。
一种有效的**解决方案是首先预处理阵列。两个观察会有帮助:** 

1.  问题陈述中提到，每个数组元素都是一个 32 位无符号数。因此，结果也将是一个 32 位无符号数。
2.  当多个位被异或时，如果有奇数个 1，结果为 1，否则结果为 0。

使用观察 1，创建一个大小为 32*n 的二维数组 cnt。该数组将用于存储 1 的计数。元素 cnt[i][j]表示到索引 j 为止的第 I 位的 1 的计数，即子阵列 arr[0]中存在多少个 1..j]在第一位位置。
根据观察 2 得到异或值，需要找到子阵列 arr[L…R]中所有 32 位位置的 1 个数。这可以在碳纳米管阵列的帮助下完成。子数组 arr[L…R]中第个位位置的位数是 CNT[I][R]–CNT[I][L-1]。如果第 I 位的 1 个数为奇数，则第 I 位将在结果中置 1。如果置位，则可以通过将对应于第 I 位的 2 的幂相加来获得结果。
根据该算法处理每个查询将花费 O(32)即恒定时间。创建 cnt 阵列的预处理阶段将花费 O(n)个时间。因此，这个 q 查询解决方案的总时间复杂度是 O(n+q)。
**实施:**

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to preprocess the array and find count of
// number of ones upto jth index for ith bit.
void preprocess(int arr[], int n, vector<vector<int> >& cnt)
{
    int i, j;

    // Run a loop for each bit position from
    // 0 to 32.
    for (i = 0; i < 32; i++) {
        cnt[i][0] = 0;
        for (j = 0; j < n; j++) {
            if (j > 0) {

                // store previous count of 1s
                // for ith bit position.
                cnt[i][j] = cnt[i][j - 1];
            }

            // Check if ith bit for jth element
            // of array is set or not. If it is
            // set then increase count of 1 for
            // ith bit by 1.
            if (arr[j] & (1 << i))
                cnt[i][j]++;
        }
    }
}

// Function to find XOR value for a range of array elements.
int findXOR(int L, int R, const vector<vector<int> > cnt)
{

    // variable to store final answer.
    int ans = 0;

    // variable to store number of 1s for ith bit
    // in the range L to R.
    int noOfOnes;

    int i, j;

    // Find number of 1s for each bit position from 0
    // to 32.
    for (i = 0; i < 32; i++) {
        noOfOnes = cnt[i][R] - ((L > 0) ? cnt[i][L - 1] : 0);

        // If number of 1s are odd then in the result
        // ith bit will be set, i.e., 2^i will be present in
        // the result. Add 2^i in ans variable.
        if (noOfOnes & 1) {
            ans += (1 << i);
        }
    }

    return ans;
}

int main()
{
    int arr[] = { 2, 5, 1, 6, 1, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    vector<vector<int> > cnt(32, vector<int>(n));
    preprocess(arr, n, cnt);
    int L = 1;
    int R = 4;
    cout << findXOR(L, R, cnt);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{

    // Function to preprocess the array and find count of
    // number of ones upto jth index for ith bit.
    static void preprocess(int arr[], int n, int[][] cnt)
    {
        int i, j;

        // Run a loop for each bit position from
        // 0 to 32.
        for (i = 0; i < 32; i++)
        {
            cnt[i][0] = 0;
            for (j = 0; j < n; j++)
            {
                if (j > 0)
                {

                    // store previous count of 1s
                    // for ith bit position.
                    cnt[i][j] = cnt[i][j - 1];
                }

                // Check if ith bit for jth element
                // of array is set or not. If it is
                // set then increase count of 1 for
                // ith bit by 1.
                if ((arr[j] & (1 << i)) >= 1)
                    cnt[i][j]++;
            }
        }
    }

    // Function to find XOR value for a range of array elements.
    static int findXOR(int L, int R, int[][] cnt)
    {

        // variable to store final answer.
        int ans = 0;

        // variable to store number of 1s for ith bit
        // in the range L to R.
        int noOfOnes;

        int i, j;

        // Find number of 1s for each bit position from 0
        // to 32.
        for (i = 0; i < 32; i++)
        {
            noOfOnes = cnt[i][R] - ((L > 0) ? cnt[i][L - 1] : 0);

            // If number of 1s are odd then in the result
            // ith bit will be set, i.e., 2^i will be present in
            // the result. Add 2^i in ans variable.
            if (noOfOnes % 2 == 1)
            {
                ans += (1 << i);
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 5, 1, 6, 1, 2, 5 };
        int n = arr.length;
        int[][] cnt = new int[32][n];
        preprocess(arr, n, cnt);
        int L = 1;
        int R = 4;
        System.out.print(findXOR(L, R, cnt));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Function to preprocess the array and
# find count of number of ones upto
# jth index for ith bit.
def preprocess(arr, n, cnt):

    # Run a loop for each bit position
    # from 0 to 32.
    for i in range(32):
        cnt[i][0] = 0
        for j in range(n):
            if (j > 0):

                # store previous count of 1s
                # for ith bit position.
                cnt[i][j] = cnt[i][j - 1]

            # Check if ith bit for jth element
            # of array is set or not. If it is
            # set then increase count of 1 for
            # ith bit by 1.
            if (arr[j] & (1 << i)):
                cnt[i][j] += 1

# Function to find XOR value
# for a range of array elements.
def findXOR(L, R, cnt):

    # variable to store final answer.
    ans = 0

    # variable to store number of 1s
    # for ith bit in the range L to R.
    noOfOnes = 0

    # Find number of 1s for each
    # bit position from 0 to 32.
    for i in range(32):
        if L > 0:
            noOfOnes = cnt[i][R] - cnt[i][L - 1]
        else:
            noOfOnes = cnt[i][R]

        # If number of 1s are odd then in the result
        # ith bit will be set, i.e., 2^i will be
        # present in the result. Add 2^i in ans variable.
        if (noOfOnes & 1):
            ans += (1 << i)

    return ans

# Driver Code
arr = [2, 5, 1, 6, 1, 2, 5]

n = len(arr)

cnt = [[0 for i in range(n)]
          for i in range(32)]

preprocess(arr, n, cnt)

L = 1
R = 4
print(findXOR(L, R, cnt))

# This code is contributed by Mohit Kumar
```

## C#

```
using System;

class GFG
{

    // Function to preprocess the array and find count of
    // number of ones upto jth index for ith bit.
    static void preprocess(int []arr, int n, int[,] cnt)
    {
        int i, j;

        // Run a loop for each bit position from
        // 0 to 32.
        for (i = 0; i < 32; i++)
        {
            cnt[i, 0] = 0;
            for (j = 0; j < n; j++)
            {
                if (j > 0)
                {

                    // store previous count of 1s
                    // for ith bit position.
                    cnt[i, j] = cnt[i, j - 1];
                }

                // Check if ith bit for jth element
                // of array is set or not. If it is
                // set then increase count of 1 for
                // ith bit by 1.
                if ((arr[j] & (1 << i)) >= 1)
                    cnt[i, j]++;
            }
        }
    }

    // Function to find XOR value for a range of array elements.
    static int findXOR(int L, int R, int[,] cnt)
    {

        // variable to store readonly answer.
        int ans = 0;

        // variable to store number of 1s for ith bit
        // in the range L to R.
        int noOfOnes;

        int i;

        // Find number of 1s for each bit position from 0
        // to 32.
        for (i = 0; i < 32; i++)
        {
            noOfOnes = cnt[i, R] - ((L > 0) ? cnt[i, L - 1] : 0);

            // If number of 1s are odd then in the result
            // ith bit will be set, i.e., 2^i will be present in
            // the result. Add 2^i in ans variable.
            if (noOfOnes % 2 == 1)
            {
                ans += (1 << i);
            }
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 5, 1, 6, 1, 2, 5 };
        int n = arr.Length;
        int[,] cnt = new int[32, n];
        preprocess(arr, n, cnt);
        int L = 1;
        int R = 4;
        Console.Write(findXOR(L, R, cnt));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Function to preprocess the array and find count of
// number of ones upto jth index for ith bit.
function preprocess(arr, n, cnt)
{
    var i, j;

    // Run a loop for each bit position from
    // 0 to 32.
    for (i = 0; i < 32; i++) {
        cnt[i][0] = 0;
        for (j = 0; j < n; j++) {
            if (j > 0) {

                // store previous count of 1s
                // for ith bit position.
                cnt[i][j] = cnt[i][j - 1];
            }

            // Check if ith bit for jth element
            // of array is set or not. If it is
            // set then increase count of 1 for
            // ith bit by 1.
            if (arr[j] & (1 << i))
                cnt[i][j]++;
        }
    }
}

// Function to find XOR value for a range of array elements.
function findXOR(L, R, cnt)
{

    // variable to store final answer.
    var ans = 0;

    // variable to store number of 1s for ith bit
    // in the range L to R.
    var noOfOnes;

    var i, j;

    // Find number of 1s for each bit position from 0
    // to 32.
    for (i = 0; i < 32; i++) {
        noOfOnes = cnt[i][R] - ((L > 0) ? cnt[i][L - 1] : 0);

        // If number of 1s are odd then in the result
        // ith bit will be set, i.e., 2^i will be present in
        // the result. Add 2^i in ans variable.
        if (noOfOnes & 1) {
            ans += (1 << i);
        }
    }

    return ans;
}

var arr = [ 2, 5, 1, 6, 1, 2, 5 ];
var n = arr.length;
var cnt = Array.from( Array(32), () => Array(n));
preprocess(arr, n, cnt);
var L = 1;
var R = 4;
document.write( findXOR(L, R, cnt));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(n+q)
T3】辅助空间: O(n)