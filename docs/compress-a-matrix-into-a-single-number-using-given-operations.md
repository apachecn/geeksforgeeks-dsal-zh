# 使用给定的操作将矩阵压缩成一个数字

> 原文:[https://www . geeksforgeeks . org/compress-a-matrix-to-a-single-number-use-given-operations/](https://www.geeksforgeeks.org/compress-a-matrix-into-a-single-number-using-given-operations/)

给定维度为 **M * N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**，任务是首先压缩它以获得一个数组，然后使用以下操作再次压缩它以获得单个整数:

*   当矩阵被压缩时，其值的二进制表示被压缩。
*   因此，考虑每个比特，如果一个比特的位置具有 **S** 设置比特和 **NS** 未设置比特，则如果 **S > NS** 则该比特被设置为该位置，否则不被设置。
*   每一列被压缩，把矩阵变成一个数组，然后这个数组被进一步压缩成一个数字。

> 例如，如果 **5、2、3、**和 **1** 被压缩，那么它们的二进制表示 **(101) <sub>2</sub> 、(010) <sub>2</sub> 、(011) <sub>2</sub> 、**和 **(001) <sub>2</sub>** 被压缩，那么对于 **0 <sup>th</sup>** 和

**示例:**

> **输入:** arr[][] ={{ 3，2，4}，{5，6，1}，{8，1，3}}
> **输出:** 1
> **说明:**从上往下压缩给定矩阵后得到的数组为{1，2，1 }。然后，将获得的数组压缩为 1。
> 
> **输入:** arr[][] = {{ 5，3}，{6，7 } }
> T3】输出: 0

**方法:**思路是[统计每个位置的设置位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。按照以下步骤解决问题:

*   遍历矩阵每一列的每个元素，并将每一列压缩为一个数字。
*   [统计每个位置的设定位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。
*   为设置位数超过未设置位数的位置设置位。
*   在决定是否为每个位置设置位后，计算该值。
*   获取数组后，应用相同的步骤获取所需的整数。

下面是上述方法的实现:

## C++

```
// c++ Program for the above approach
#include<bits/stdc++.h>
using namespace std;

  // Function to compress an
  // array to a single number
  vector<int> append(vector<int> arr, int x)
  {

    // create a new ArrayList
    arr.push_back(x);
    return arr;
  }

  int compress(vector<int> arr)
  {

    // Stores the required integer
    int ans = 0;
    int getBit = 1;

    // Checking for each position
    for (int i = 0; i < 32; i++)
    {
      int S = 0;
      int NS = 0;
      for (int j = 0; j < arr.size(); j++)
      {

        // Count set and unset bit
        int temp = getBit & arr[j];
        if (temp == 1) {
          S += 1;
        }
        else {
          NS += 1;
        }

        // If count of set bits exceeds
        // count of unset bits
        if (S > NS) {

          // Add value of set bits to ans
          ans += pow(2, i);
        }
        getBit <<= 1;
      }
    }

    return ans;
  }

  // Function to compress
  // matrix to a single number
 int getResult(vector<vector<int>> mat)
  {

    // Stores compressed array
    vector<int> compressedArr;
    int len = mat.size();
    int len2 = mat[0].size();
    for (int i = 0; i < len; i++)
    {
      vector<int> col;

      for (int j = 0; j < len2; j++)
      {
        col = append(col, mat[j][i]);
      }

      // Compress all columns
      // to a single number
      compressedArr = append(compressedArr, compress(col));
    }
    return compress(compressedArr);
  }

  // Driver Code
  int main()
  {
    vector<vector<int>> mat{{3, 2, 4 },{5, 6, 1},{8, 1, 3}};
    cout<<(getResult(mat));
  }

// THIS CODE IS CONTRIBUTED BY SURENDRA_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;
import java.lang.*;
import java.lang.Math;
import java.util.*;
class GFG {

  // Function to compress an
  // array to a single number
  static Integer[] append(Integer arr[], int x)
  {
    // create a new ArrayList
    List<Integer> arrlist
      = new ArrayList<Integer>(Arrays.asList(arr));

    // Add the new element
    arrlist.add(x);

    // Convert the Arraylist to array
    arr = arrlist.toArray(arr);

    // return the array
    return arr;
  }
  static int compress(Integer[] arr)
  {

    // Stores the required integer
    int ans = 0;
    int getBit = 1;

    // Checking for each position
    for (int i = 0; i < 32; i++) {

      int S = 0;
      int NS = 0;

      for (int j = 0; j < arr.length; j++) {

        // Count set and unset bit
        int and = getBit & arr[j];
        if (and == 1) {
          S += 1;
        }
        else {
          NS += 1;
        }

        // If count of set bits exceeds
        // count of unset bits
        if (S > NS) {

          // Add value of set bits to ans
          ans += Math.pow(2, i);
        }
        getBit <<= 1;
      }
    }

    return ans;
  }

  // Function to compress
  // matrix to a single number
  static int getResult(Integer[][] mat)
  {

    // Stores compressed array
    Integer[] compressedArr = {};
    int len = mat.length;
    int len2 = mat[0].length;
    for (int i = 0; i < len; i++)
    {
      Integer[] col = {};

      for (int j = 0; j < len2; j++)
      {
        col = append(col, mat[j][i]);
      }

      // Compress all columns
      // to a single number
      compressedArr
        = append(compressedArr, compress(col));
    }
    return compress(compressedArr);
  }

  // Driver Code
  public static void main(String[] args)
  {
    Integer[][] mat = { { 3, 2, 4 },
                       { 5, 6, 1 },
                       { 8, 1, 3 } };
    System.out.println(getResult(mat));
  }
}

// This code is contributed by rohitsingh07052.
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to compress an
# array to a single number
def compress(arr):

  # Stores the required integer
  ans = 0
  getBit = 1

  # Checking for each position
  for i in range(32):

    S = 0
    NS = 0

    for j in arr:

      # Count set and unset bits
      if getBit&j:
        S += 1
      else:
        NS += 1

    # If count of set bits exceeds
    # count of unset bits
    if S > NS:

      # Add value of set bits to ans
      ans += 2**i
    getBit <<= 1

  return ans

# Function to compress
# matrix to a single number
def getResult(mat):

  # Stores compressed array
  compressedArr = []

  for i in range(len(mat)):
    col = []
    for j in range(len(mat[0])):
      col.append(mat[j][i])

    # Compress all columns
    # to a single number 
    compressedArr.append(compress(col))

  return compress(compressedArr)

# Driver Code
mat = [ [ 3, 2, 4], [5, 6, 1], [8, 1, 3] ]

print( getResult(mat) )
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to compress an
// array to a single number
static int[] append(int []arr, int x)
{

    // create a new List
    List<int> arrlist = new List<int>(arr);

    // Add the new element
    arrlist.Add(x);

    // Convert the Arraylist to array
    arr = arrlist.ToArray();

    // return the array
    return arr;
}

static int compress(int[] arr)
{

    // Stores the required integer
    int ans = 0;
    int getBit = 1;

    // Checking for each position
    for(int i = 0; i < 32; i++)
    {

        int S = 0;
        int NS = 0;

        for(int j = 0; j < arr.Length; j++)
        {

            // Count set and unset bit
            int and = getBit & arr[j];
            if (and == 1)
            {
                S += 1;
            }
            else
            {
                NS += 1;
            }

            // If count of set bits exceeds
            // count of unset bits
            if (S > NS)
            {

                // Add value of set bits to ans
                ans += (int)Math.Pow(2, i);
            }
            getBit <<= 1;
        }
    }

    return ans;
}

// Function to compress
// matrix to a single number
static int getResult(int[,] mat)
{

    // Stores compressed array
    int[] compressedArr = {};
    int len = mat.GetLength(0);
    int len2 = mat.GetLength(1);

    for(int i = 0; i < len; i++)
    {
        int[] col = {};

        for (int j = 0; j < len2; j++)
        {
            col = append(col, mat[j,i]);
        }

        // Compress all columns
        // to a single number
        compressedArr = append(compressedArr,
                               compress(col));
    }
    return compress(compressedArr);
}

// Driver Code
public static void Main(String[] args)
{
    int[,] mat = { { 3, 2, 4 },
                   { 5, 6, 1 },
                   { 8, 1, 3 } };

    Console.WriteLine(getResult(mat));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript Program for the above approach

    // Function to compress an
    // array to a single number
    function append(arr, x)
    {

      // create a new ArrayList
      arr.push(x);
      return arr;
    }

    function compress(arr)
    {

      // Stores the required integer
      let ans = 0;
      let getBit = 1;

      // Checking for each position
      for (let i = 0; i < 32; i++)
      {
        let S = 0;
        let NS = 0;
        for (let j = 0; j < arr.length; j++)
        {

          // Count set and unset bit
          let temp = getBit & arr[j];
          if (temp == 1) {
            S += 1;
          }
          else {
            NS += 1;
          }

          // If count of set bits exceeds
          // count of unset bits
          if (S > NS) {

            // Add value of set bits to ans
            ans += Math.pow(2, i);
          }
          getBit <<= 1;
        }
      }

      return ans;
    }

    // Function to compress
    // matrix to a single number
    function getResult(mat)
    {

      // Stores compressed array
      let compressedArr = [];
      let len = mat.length;
      let len2 = mat[0].length;
      for (let i = 0; i < len; i++)
      {
        let col = [];

        for (let j = 0; j < len2; j++)
        {
          col = append(col, mat[j][i]);
        }

        // Compress all columns
        // to a single number
        compressedArr = append(compressedArr, compress(col));
      }
      return compress(compressedArr);
    }

    let mat = [[3, 2, 4 ],[5, 6, 1],[8, 1, 3]];
    document.write(getResult(mat));

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*