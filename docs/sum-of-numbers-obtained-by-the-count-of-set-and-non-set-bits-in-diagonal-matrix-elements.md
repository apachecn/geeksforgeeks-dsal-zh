# 对角矩阵元素中集合位和非集合位计数得到的数之和

> 原文:[https://www . geeksforgeeks . org/通过矩阵元素的集合和非集合对角位计数获得的数字总和/](https://www.geeksforgeeks.org/sum-of-numbers-obtained-by-the-count-of-set-and-non-set-bits-in-diagonal-matrix-elements/)

给定尺寸为 **N*N** 的[正方形矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **mat[][]** ，将两条对角线中的元素转换为它们各自的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)，并执行以下操作:

*   对于每个位的位置，计算那些[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中的设置位和未设置位的数量。
*   如果设置位的计数超过未设置位的计数，则将 **0** 放在该位置以获得新的数字。否则，将 **1** 置于该位置。
*   最后，打印两个生成数字的总和。

**示例:**

> **输入:** mat[][] = [[1，2，3]，[4，5，6]，[7，8，9]]
> **输出:** 8
> **解释:**
> 对于主对角线，每个元素的二进制表示为:
> 1 =(0001)<sub>2</sub>
> 5 =(0101)<sub>2</sub>
> 9 =(1001) **设置比特数(=0) <未设置比特数(=3)
> 在比特位置 2，设置比特数(=1) <未设置比特数(=2)
> 在比特位置 3，设置比特数(=1) <未设置比特数(=2)
> 因此，在处理主对角线之后，生成的数字是(0001) <sub>2</sub> = 1。
> 对于次对角线，每个元素的二进制表示为:
> 3 =(011)<sub>2</sub>
> 5 =(101)<sub>2</sub>
> 7 =(111)<sub>2</sub>
> 在比特位置 0，设置比特数(=3) >非设置比特数(=0)
> 在比特位置 1，设置比特数(=2) >非
> 因此，所需的总和= 1 + 7 = 8。**
> 
> **输入:** mat[][] = [[2，3]，[3，9]]
> **输出:** 3

**天真方法:**最简单的方法是[遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，将主对角线元素存储在一个数组中，将次对角线元素存储在另一个数组中。然后，通过迭代两个数组中元素的集合位，找到生成的数字的总和。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过[使用单个循环](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix/)找到对角元素来优化。按照以下步骤解决问题:

*   **对于主对角线元素:** [迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)直到 **N** ，其中 **N** 是列数，存储**mat【I】【I】**，其中 **i** 是索引变量。
*   **对于次对角线元素:** [迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)直到 **N** ，其中 **N** 是列数，存储**mat【I】【K】**，其中 **i** 是索引变量，**K = N–1**。降低 **K** 直到 **i < N** 。

要查找每组对角线元素的数字，请执行以下步骤:

*   初始化一个变量，说 **ans** 为 **0** ，存储结果数。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，31】**，并执行以下操作:
    *   将 **S** 和 **NS** 初始化为 **0** ，在 **i** 位置分别存储设定位和非设定位的个数。
    *   使用变量 **j** 遍历对角线元素，如果**arr【j】**设置在位置 **i** ，则将 **S** 增加 **1** ，否则将 **NS** 增加 **1** 。
    *   如果 **S** 的值大于 **NS** ，将该位设置在 **ans** 的 **i** 位置。
*   完成上述步骤后，**和**的值是为每组对角元素生成的数字。
*   对其他组对角元素重复上述步骤，并打印生成的两个数之和。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the number after
// processing the diagonal elements
int processDiagonal(vector<int>arr)
{

  // Store the required number
  int ans = 0;

  int getBit = 1;

  // Checking for each position
  for (int i = 0; i < 32; i++)
  {

   // Store the number of set bits
    // & non-set bits at position i
    int S = 0;
    int NS = 0;

    // Traverse the diagonal elements
    for(auto j: arr)
    {

         // Update count of S if current
      // element is set at position i
      if (getBit&j)
        S += 1;

      // Else update NS
      else
        NS += 1;
    }
    // If number of set bits is >
    // number of non-set bits, add
    // set bits value to the ans
    if(S > NS)
      ans += pow(2,i);
    getBit <<= 1;

  }

  // Return the answer
  return ans;
}

// Function to find the sum of the
// numbers generated after processing
// both the diagonals of the matrix
int findSum(vector<vector<int>>mat)
{

  int i = 0;
  int j = 0;

  // Store the primary diagonal elements
  vector<int> priDiag;

  while(i<mat.size()){
    priDiag.push_back(mat[i][j]);
    i += 1;
    j += 1;
  }

  i = 0;
  j = mat.size()-1;

  // Store the secondary diagonal elements
  vector<int> secDiag;
  while(i<mat.size()){
    secDiag.push_back(mat[i][j]);
    i += 1;
    j -= 1;
  }

  // Function Call to get the required
  // numbers and return their sum
  return processDiagonal(priDiag) + processDiagonal(secDiag);

}

// Driver Code
int main(){
vector<vector<int>>mat{{1, 2, 3},{4, 5, 6},{7, 8, 9}};

// Function Call
cout<<findSum(mat)<<endl;
}

// This code is contributed by bgangwar59.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Functino to find the number after
  // processing the diagonal elements
  static int processDiagonal(ArrayList<Integer> arr)
  {

    // Store the required number
    int ans = 0;

    int getBit = 1;

    // Checking for each position
    for (int i = 0; i < 32; i++)
    {

      // Store the number of set bits
      // & non-set bits at position i
      int S = 0;
      int NS = 0;

      // Traverse the diagonal elements
      for(int j: arr)
      {

        // Update count of S if current
        // element is set at position i
        if ((getBit&j) != 0)
          S += 1;

        // Else update NS
        else
          NS += 1;
      }
      // If number of set bits is >
      // number of non-set bits, add
      // set bits value to the ans
      if(S > NS)
        ans += Math.pow(2,i);
      getBit <<= 1;

    }

    // Return the answer
    return ans;
  }

  // Function to find the sum of the
  // numbers generated after processing
  // both the diagonals of the matrix
  static int findSum(int[][] mat)
  {

    int i = 0;
    int j = 0;

    // Store the primary diagonal elements
    ArrayList<Integer> priDiag
      = new ArrayList<Integer>();

    while(i<mat.length){
      priDiag.add(mat[i][j]);
      i += 1;
      j += 1;
    }

    i = 0;
    j = mat.length - 1;

    // Store the secondary diagonal elements
    ArrayList<Integer> secDiag
      = new ArrayList<Integer>();
    while(i<mat.length){
      secDiag.add(mat[i][j]);
      i += 1;
      j -= 1;
    }

    // Function Call to get the required
    // numbers and return their sum
    return (processDiagonal(priDiag) + processDiagonal(secDiag));

  }

  // Driver Code
  public static void main(String[] args)
  {
    int[][] mat= {{1, 2, 3},{4, 5, 6},{7, 8, 9}};

    // Function Call
    System.out.print(findSum(mat));
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Functino to find the number after
# processing the diagonal elements
def processDiagonal(arr):

  # Store the required number
  ans = 0

  getBit = 1

  # Checking for each position
  for i in range(32):

    # Store the number of set bits
    # & non-set bits at position i
    S = 0
    NS = 0

    # Traverse the diagonal elements
    for j in arr:

      # Update count of S if current
      # element is set at position i
      if getBit&j:
        S += 1

      # Else update NS
      else:
        NS += 1

    # If number of set bits is >
    # number of non-set bits, add
    # set bits value to the ans
    if S > NS:
      ans += 2**i
    getBit <<= 1

  # Return the answer
  return ans

# Function to find the sum of the
# numbers generated after processing
# both the diagonals of the matrix
def findSum(mat):
  i = 0
  j = 0

  # Store the primary diagonal elements
  priDiag = []

  while i<len(mat):
    priDiag.append(mat[i][j])
    i += 1
    j += 1

  i = 0
  j = len(mat)-1

  # Store the secondary diagonal elements
  secDiag = []
  while i<len(mat):
    secDiag.append(mat[i][j])
    i += 1
    j -= 1

  # Function Call to get the required
  # numbers and return their sum
  return processDiagonal(priDiag) + processDiagonal(secDiag)

# Driver Code
mat = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Function Call
print(findSum(mat))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

  // Functino to find the number after
  // processing the diagonal elements
  static int processDiagonal(List<int> arr)
  {

    // Store the required number
    int ans = 0;

    int getBit = 1;

    // Checking for each position
    for (int i = 0; i < 32; i++) {

      // Store the number of set bits
      // & non-set bits at position i
      int S = 0;
      int NS = 0;

      // Traverse the diagonal elements
      foreach(int j in arr)
      {

        // Update count of S if current
        // element is set at position i
        if ((getBit & j) != 0)
          S += 1;

        // Else update NS
        else
          NS += 1;
      }
      // If number of set bits is >
      // number of non-set bits, add
      // set bits value to the ans
      if (S > NS)
        ans += (int)Math.Pow(2, i);
      getBit <<= 1;
    }

    // Return the answer
    return ans;
  }

  // Function to find the sum of the
  // numbers generated after processing
  // both the diagonals of the matrix
  static int findSum(int[, ] mat)
  {

    int i = 0;
    int j = 0;

    // Store the primary diagonal elements
    List<int> priDiag = new List<int>();

    while (i < mat.GetLength(0)) {
      priDiag.Add(mat[i, j]);
      i += 1;
      j += 1;
    }

    i = 0;
    j = mat.GetLength(0) - 1;

    // Store the secondary diagonal elements
    List<int> secDiag = new List<int>();
    while (i < mat.GetLength(0)) {
      secDiag.Add(mat[i, j]);
      i += 1;
      j -= 1;
    }

    // Function Call to get the required
    // numbers and return their sum
    return (processDiagonal(priDiag)
            + processDiagonal(secDiag));
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[, ] mat
      = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

    // Function Call
    Console.Write(findSum(mat));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Functino to find the number after
// processing the diagonal elements
function processDiagonal(arr)
{

  // Store the required number
  let ans = 0;

  let getBit = 1;

  // Checking for each position
  for (let i = 0; i < 32; i++)
  {

   // Store the number of set bits
    // & non-set bits at position i
    let S = 0;
    let NS = 0;

    // Traverse the diagonal elements
    for(let j = 0; j < arr.length; j++)
    {

         // Update count of S if current
      // element is set at position i
      if (getBit & arr[j])
        S += 1;

      // Else update NS
      else
        NS += 1;
    }
    // If number of set bits is >
    // number of non-set bits, add
    // set bits value to the ans
    if(S > NS)
      ans += Math.pow(2,i);
    getBit <<= 1;

  }

  // Return the answer
  return ans;
}

// Function to find the sum of the
// numbers generated after processing
// both the diagonals of the matrix
function findSum(mat)
{

  let i = 0;
  let j = 0;

  // Store the primary diagonal elements
  let priDiag = [];

  while(i<mat.length){
    priDiag.push(mat[i][j]);
    i += 1;
    j += 1;
  }

  i = 0;
  j = mat.length - 1;

  // Store the secondary diagonal elements
  let secDiag = [];
  while(i<mat.length){
    secDiag.push(mat[i][j]);
    i += 1;
    j -= 1;
  }

  // Function Call to get the required
  // numbers and return their sum
  return processDiagonal(priDiag) + processDiagonal(secDiag);

}

// Driver Code
let mat = [[1, 2, 3],[4, 5, 6],[7, 8, 9]];

// Function Call
document.write(findSum(mat));

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)