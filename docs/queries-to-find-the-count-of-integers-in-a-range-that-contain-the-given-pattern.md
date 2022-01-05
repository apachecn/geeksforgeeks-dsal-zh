# 查询包含给定模式的范围内的整数个数

> 原文:[https://www . geeksforgeeks . org/查询查找包含给定模式的范围内整数的计数/](https://www.geeksforgeeks.org/queries-to-find-the-count-of-integers-in-a-range-that-contain-the-given-pattern/)

给定二进制模式**模式**和 **Q** 查询，其中每个查询由范围**【L，R】**组成，对于每个查询，任务是从给定的范围中找到整数的计数，使得它们在其二进制表示中包含给定的模式。
**示例:**

> **输入:** q[][] = {{2，10}}，patt = "101"
> **输出:**
> 2
> 5(101)和 10(1010)是唯一有效的整数。
> **输入:** q[][] = {{122，150}，{18，1000}}，patt = "1111"
> **输出:**
> 7
> 227

**进场:**

*   创建一个数组 **res[]** ，其中 **res[i]** 将存储范围**【0，I】**中的有效整数计数。
*   从 **0** 开始，找到所有整数的二进制表示，检查其中是否出现给定的模式。
*   根据上一步中找到的值更新 **res[]** 数组。
*   现在每个查询都可以在 O(1)中回答为**RES[R]–RES[L–1]**。

以下是上述方法的实现:

## C++

```
#include<bits/stdc++.h>
using namespace std;

// Function to return the
// pre-calculate array such
// that arr[i] stores the count of
// valid numbers in the range [0, i]
string DecimalToBinaryString(int a)
{
  string binary = "";
  int mask = 1;
  for (int i = 0; i < 31; i++)
  {
    if(mask&a)
      binary = "1" + binary;
    else
      binary = "0" + binary;
    mask <<= 1;
  }

  return binary;
}

vector<int> preCalculate(int max,
                         string pattern)
{
  vector<int> arr(max + 1, 0);

  // If 0 is a valid number
  if (pattern == "0")
    arr[0] = 1;
  else
    arr[0] = 0;

  // For every element i
  for (int i = 1; i <= max; i++)
  {
    // If i is avalid number
    if (DecimalToBinaryString(i).find(pattern) !=
        std::string :: npos)
    {
      arr[i] = 1 + arr[i - 1];
    }
    else
    {
      arr[i] = arr[i - 1];
    }
  }
  return arr;
}

// Function to perform the queries
void performQueries(vector<vector<int> > queries,
                    int q, string pattern)
{
  // Maximum value for the
  // end of any range
  int ma = INT_MIN;

  for (int i = 0; i < q; i++)
    ma = max(ma, queries[i][1]);

  // res[i] stores the count of valid
  // integers from the range [0, i]
  vector<int> res = preCalculate(ma,
                                 pattern);

  for (int i = 0; i < q; i++)
  {
    int l = queries[i][0];
    int r = queries[i][1];

    if (l == 0)
      cout << (res[r]) << endl;
    else
      cout << (res[r] -
               res[l - 1]) << endl;
  }
}

// Driver code
int main()
{
  vector<vector<int>> queries = {{2, 10},
                                 {8, 120}};
  int q = queries.size();
  string pattern = "101";
  performQueries(queries, q, pattern);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    // Function to return the pre-calculate array
    // such that arr[i] stores the count of
    // valid numbers in the range [0, i]
    static int[] preCalculate(int max, String pattern)
    {
        int arr[] = new int[max + 1];

        // If 0 is a valid number
        if (pattern == "0")
            arr[0] = 1;
        else
            arr[0] = 0;

        // For every element i
        for (int i = 1; i <= max; i++) {

            // If i is avalid number
            if (Integer.toBinaryString(i).contains(pattern)) {
                arr[i] = 1 + arr[i - 1];
            }
            else {
                arr[i] = arr[i - 1];
            }
        }
        return arr;
    }

    // Function to perform the queries
    static void performQueries(int queries[][],
                               int q, String pattern)
    {

        // Maximum value for the end of any range
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < q; i++)
            max = Math.max(max, queries[i][1]);

        // res[i] stores the count of valid
        // integers from the range [0, i]
        int res[] = preCalculate(max, pattern);

        for (int i = 0; i < q; i++) {
            int l = queries[i][0];
            int r = queries[i][1];

            if (l == 0)
                System.out.println(res[r]);
            else
                System.out.println(res[r] - res[l - 1]);
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int queries[][] = { { 2, 10 }, { 8, 120 } };
        int q = queries.length;
        String pattern = "101";

        performQueries(queries, q, pattern);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the pre-calculate array
# such that arr[i] stores the count of
# valid numbers in the range [0, i]
def preCalculate(maX, pattern) :
    arr = [0] * (maX + 1);

    # If 0 is a valid number
    if (pattern == "0") :
        arr[0] = 1;

    else :
        arr[0] = 0;

    # For every element i
    for i in range(1, maX + 1) :

        # If i is avalid number
        if (pattern in bin(i)) :
            arr[i] = 1 + arr[i - 1];

        else :
            arr[i] = arr[i - 1];

    return arr;

# Function to perform the queries
def performQueries(queries,q, pattern) :

    # Maximum value for the end of any range
    maX = -(sys.maxsize + 1);

    for i in range(q) :

        maX = max(maX, queries[i][1]);

    # res[i] stores the count of valid
    # integers from the range [0, i]
    res = preCalculate(maX, pattern);

    for i in range(q) :
        l = queries[i][0];
        r = queries[i][1];

        if (l == 0) :
            print(res[r]);
        else :
            print(res[r] - res[l - 1]);

# Driver code
if __name__ == "__main__" :

    queries = [ [ 2, 10 ], [ 8, 120 ] ];
    q = len(queries);
    pattern = "101";
    performQueries(queries, q, pattern);

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;
using System.Numerics;

class GFG
{

    //integer to binary string
    public static string toBinaryString(int x)
    {
        char[] bits = new char[32];
        int i = 0;

        while (x != 0)
        {
            bits[i++] = (x & 1) == 1 ? '1' : '0';
            x >>= 1;
        }

        Array.Reverse(bits, 0, i);
        return new string(bits);
    }

    // Function to return the pre-calculate array
    // such that arr[i] stores the count of
    // valid numbers in the range [0, i]
    static int[] preCalculate(int max, string pattern)
    {
        int []arr = new int[max + 1];

        // If 0 is a valid number
        if (pattern == "0")
            arr[0] = 1;
        else
            arr[0] = 0;

        // For every element i
        for (int i = 1; i <= max; i++)
        {
            // If i is avalid number
            if (toBinaryString(i).Contains(pattern))
            {
                arr[i] = 1 + arr[i - 1];
            }
            else
            {
                arr[i] = arr[i - 1];
            }
        }
        return arr;
    }

    // Function to perform the queries
    static void performQueries(int [,]queries,
                               int q, string pattern)
    {

        // Maximum value for the end of any range
        int max = int.MinValue;
        for (int i = 0; i < q; i++)
            max = Math.Max(max, queries[i, 1]);

        // res[i] stores the count of valid
        // integers from the range [0, i]
        int []res = preCalculate(max, pattern);

        for (int i = 0; i < q; i++)
        {
            int l = queries[i, 0];
            int r = queries[i, 1];

            if (l == 0)
                Console.WriteLine(res[r]);
            else
                Console.WriteLine(res[r] - res[l - 1]);
        }
    }

    // Driver code
    public static void Main(string []args)
    {
        int [,]queries = { { 2, 10 }, { 8, 120 } };
        int q = queries.GetLength(0) ;
        string pattern = "101";

        performQueries(queries, q, pattern);
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the pre-calculate array
    // such that arr[i] stores the count of
    // valid numbers in the range [0, i]
function preCalculate(max,pattern)
{
    let arr = new Array(max + 1);

        // If 0 is a valid number
        if (pattern == "0")
            arr[0] = 1;
        else
            arr[0] = 0;

        // For every element i
        for (let i = 1; i <= max; i++) {

            // If i is avalid number
            if ((i >>> 0).toString(2).includes(pattern)) {
                arr[i] = 1 + arr[i - 1];
            }
            else {
                arr[i] = arr[i - 1];
            }
        }
        return arr;
}

 // Function to perform the queries
function performQueries(queries,q,pattern)
{
    // Maximum value for the end of any range
        let max = Number.MIN_VALUE;
        for (let i = 0; i < q; i++)
            max = Math.max(max, queries[i][1]);

        // res[i] stores the count of valid
        // integers from the range [0, i]
        let res = preCalculate(max, pattern);

        for (let i = 0; i < q; i++) {
            let l = queries[i][0];
            let r = queries[i][1];

            if (l == 0)
                document.write(res[r]+"<br>");
            else
                document.write(res[r] - res[l - 1]+"<br>");
        }
}

// Driver code
let queries=[[ 2, 10 ], [ 8, 120 ]];
let q = queries.length;
let pattern = "101";

performQueries(queries, q, pattern);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
59
```