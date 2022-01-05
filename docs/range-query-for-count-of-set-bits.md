# 设定位数范围查询

> 原文:[https://www . geesforgeks . org/range-query-for-count-of-set-bits/](https://www.geeksforgeeks.org/range-query-for-count-of-set-bits/)

给定一个正整数数组和一个包含两个整数的 q 查询，L & R 的任务是找到给定范围的集合位数。
**先决条件:** [逐位黑客攻击](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/)

示例:

```
Input :  Arr[] = { 1, 5, 6, 10, 9, 4 }
         Query : 2 
         L  &  R
         1     5
         2     4
Output : 9
         6

Input : Arr[] = { 1, 10, 5, 2, 8, 11, 15 }
        Query : 2
        L  &  R
        2     4
        1     5
Output :  4
          9
```

**这个问题的简单解决方案**是运行一个从 L 到 R 的循环，计算一个范围内的设置位数。该解决方案对每个查询取 0(nlog)(其中 s 是位大小)。

**高效的解决方案**是基于这样一个事实:如果我们在一个数组“位计数”中存储数字的所有设置位的计数，那么我们在 O(1)时间内回答每个查询。因此，开始遍历数组的元素，计算每个元素的设置位并存储在数组中。现在，求这个数组的累计和。这个数组将有助于回答查询。

```
BitCount[] that will store the count of set bits
in a number. 

Run a Loop from 0 to 31 "for 32 bits size integer "       
-> mark elements with i'th bit set     

Run an inner Loop from 0 to size of Array "Arr"  
     -> Check whether the current bit is set or not 
     -> if it's set then mark it.
          long  temp = arr[j] >> i;
             if (temp %2 != 0)
                 BitCount[j] += 1
```

下面是上述想法的实现。

## C++

```
// C++ program to Range query for
// Count number of set bits
#include <bits/stdc++.h>
using namespace std;

// 2-D array that will stored the count
// of bits set in element of array
int BitCount[10000] = { 0 };

// Function store the set bit
// count in BitCount Array
void fillSetBitsMatrix(int arr[], int n)
{

    // traverse over all bits
    for (int i = 0; i < 32; i++) {

        // mark elements with i'th bit set
        for (int j = 0; j < n; j++) {

            // Check whether the current bit is
            // set or not if it's set then mark it.
            long temp = arr[j] >> i;
            if (temp % 2 != 0)
                BitCount[j] += 1;
        }
    }

    // store cumulative sum of bits
    for (int i = 1; i < n; i++)
        BitCount[i] += BitCount[i - 1];
}

// Function to process queries
void Query(int Q[][2], int q)
{
    for (int i = 0; i < q; i++)
        cout << (BitCount[Q[i][1]] -
                 BitCount[Q[i][0] - 1]) << endl;
}

// Driver Code
int main()
{
    int Arr[] = { 1, 5, 6, 10, 9, 4, 67 };
    int n = sizeof(Arr) / sizeof(Arr[0]);

    fillSetBitsMatrix(Arr, n);

    int q = 2;
    int Q[2][2] = { { 1, 5 }, { 2, 6 } };

    Query(Q, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Range query for
// Count number of set bits
import java.io.*;

class GFG {

    // 2-D array that will stored the count
    // of bits set in element of array
    static int BitCount[] = new int[10000];

    // Function store the set bit
    // count in BitCount Array
    static void fillSetBitsMatrix(int arr[], int n)
    {

        // traverse over all bits
        for (int i = 0; i < 32; i++) {

            // mark elements with i'th bit set
            for (int j = 0; j < n; j++) {

                // Check whether the current
                // bit is set or not if it's
                // set then mark it.
                long temp = arr[j] >> i;
                if (temp % 2 != 0)
                    BitCount[j] += 1;
            }
        }

        // store cumulative sum of bits
        for (int i = 1; i < n; i++)
            BitCount[i] += BitCount[i - 1];
    }

    // Function to process queries
    static void Query(int Q[][], int q)
    {
        for (int i = 0; i < q; i++)
            System.out.println( (BitCount[Q[i][1]]
                        - BitCount[Q[i][0] - 1]));
    }

    // Driver Code
    public static void main (String[] args)
    {
        int Arr[] = { 1, 5, 6, 10, 9, 4, 67 };
        int n = Arr.length;

        fillSetBitsMatrix(Arr, n);

        int q = 2;
        int Q[][] = { { 1, 5 }, { 2, 6 } };

        Query(Q, q);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to Range query for
# Count number of set bits

# 2-D array that will stored the count
# of bits set in element of array
BitCount = [0] * 10000

# Function store the set bit
# count in BitCount Array
def fillSetBitsmatrix(arr: list, n: int):
    global BitCount

    # traverse over all bits
    for i in range(32):

        # mark elements with i'th bit set
        for j in range(n):

            # Check whether the current bit is
            # set or not if it's set then mark it.
            temp = arr[j] >> i
            if temp % 2 != 0:
                BitCount[j] += 1

    # store cumulative sum of bits
    for i in range(1, n):
        BitCount[i] += BitCount[i - 1]

# Function to process queries
def Query(Q: list, q: int):
    for i in range(q):
        print(BitCount[Q[i][1]] - BitCount[Q[i][0] - 1])

# Driver Code
if __name__ == "__main__":

    Arr = [1, 5, 6, 10, 9, 4, 67]
    n = len(Arr)

    fillSetBitsmatrix(Arr, n)

    q = 2
    Q = [(1, 5), (2, 6)]
    Query(Q, q)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to Range query for
// Count number of set bits
using System;

class GFG {

    // 2-D array that will stored the count
    // of bits set in element of array
    static int []BitCount = new int[10000];

    // Function store the set bit
    // count in BitCount Array
    static void fillSetBitsMatrix(int []arr, int n)
    {

        // traverse over all bits
        for (int i = 0; i < 32; i++) {

            // mark elements with i'th bit set
            for (int j = 0; j < n; j++) {

                // Check whether the current
                // bit is set or not if it's
                // set then mark it.
                long temp = arr[j] >> i;
                if (temp % 2 != 0)
                    BitCount[j] += 1;
            }
        }

        // store cumulative sum of bits
        for (int i = 1; i < n; i++)
            BitCount[i] += BitCount[i - 1];
    }

    // Function to process queries
    static void Query(int [,]Q, int q)
    {
        for (int i = 0; i < q; i++)
            Console.WriteLine( (BitCount[Q[i,1]]
                        - BitCount[Q[i,0] - 1]));
    }

    // Driver Code
    public static void Main ()
    {
        int []Arr = { 1, 5, 6, 10, 9, 4, 67 };
        int n = Arr.Length;

        fillSetBitsMatrix(Arr, n);

        int q = 2;
        int [,]Q = { { 1, 5 }, { 2, 6 } };

        Query(Q, q);
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>

// Javascript program to Range query for
// Count number of set bits

// 2-D array that will stored the count
// of bits set in element of array
var BitCount = Array.from({length: 10000}, (_, i) => 0);

// Function store the set bit
// count in BitCount Array
function fillSetBitsMatrix(arr, n)
{

    // traverse over all bits
    for(i = 0; i < 32; i++)
    {

        // mark elements with i'th bit set
        for(j = 0; j < n; j++)
        {

            // Check whether the current
            // bit is set or not if it's
            // set then mark it.
            var temp = arr[j] >> i;
            if (temp % 2 != 0)
                BitCount[j] += 1;
        }
    }

    // store cumulative sum of bits
    for(i = 1; i < n; i++)
        BitCount[i] += BitCount[i - 1];
}

// Function to process queries
function Query(Q, q)
{
    for(i = 0; i < q; i++)
        document.write((BitCount[Q[i][1]] -
                        BitCount[Q[i][0] - 1]) + "<br>");
}

// Driver Code
var Arr = [ 1, 5, 6, 10, 9, 4, 67 ];
var n = Arr.length;

fillSetBitsMatrix(Arr, n);

var q = 2;
var Q = [ [ 1, 5 ], [ 2, 6 ] ];

Query(Q, q);

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
9
10
```

**时间复杂度:**每个查询 O(1)。