# 检查二进制矩阵的所有行是否都相邻

> 原文:[https://www . geeksforgeeks . org/check-如果一个二进制矩阵的所有行都有一个相邻或不相邻的位置/](https://www.geeksforgeeks.org/check-if-all-rows-of-a-binary-matrix-have-all-ones-placed-adjacently-or-not/)

给定一个维度为 **N*M** 的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/) **mat[][]** ，任务是检查每一行中的[是否所有 **1** s 都相邻于给定矩阵上的](https://www.geeksforgeeks.org/minimum-swaps-required-group-1s-together/)。如果每行的所有 **1** 都相邻，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** mat[][] = {{0，1，1，0}，{1，1，0，0}，{0，0，0，1}，{1，1，1，0}
> **输出:** Yes
> **说明:**
> 第一行的元素为{0，1，1，0}。
> 第二行的元素是{1，1，0，0}。
> 第三行的元素为{0，0，0，1}。
> 第四行的元素是{1，1，1，0}。
> 因此，所有行都将全 1 分组在一起。因此，打印“是”。
> 
> **输入:** mat[][] = {{1，0，1}，{0，0，1}，{0，0，0 } }
> T3】输出:否

**方法:**思路是对矩阵进行[逐行遍历，利用](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)[逐位异或](https://www.geeksforgeeks.org/tag/xor/)的性质，检查一行中的所有 **1** 是否相邻放置。给定的问题可以基于以下观察来解决:

*   计算第 I<sup>行每对相邻元素的[位异或之和，比如 **X** 。如果满足以下任一条件，所有 **1s** 将不在 **i <sup>th</sup>** 行:](https://www.geeksforgeeks.org/find-the-original-array-using-xor-values-of-all-adjacent-elements/)

    *   如果 **X > 2** 和**mat[I][0]+mat[I][M–1]= 0**。
    *   如果 **X > 1** 和**mat[I][0]+mat[I][M–1]= 1**。
    *   如果 **X > 0** 和**mat[I][0]+mat[I][M–1]= 0**。</sup> 

按照以下步骤解决此问题:

*   [遍历给定矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/) **mat[][]** 并执行以下操作:
    *   每行检查 **M** 的值是否小于 **3** ，然后打印**“是”**。
    *   否则，求相邻数组元素的**位异或**的和，并存储在一个变量中，比如 **X** 。
    *   对于 **X** 的每一个值，如果上述任一条件成立**为真**，则打印**“否”**。
*   完成上述步骤后，如果上述任何条件对于 **X** 的任何值都不成立，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if all 1s are
// placed adjacently in an array or not
bool checkGroup(vector<int> arr)
{

    // Base Case
    if (arr.size() <= 2)
        return true;
    int corner = arr[0] + arr[(int)arr.size()-1];

    // Stores the sum of XOR of all
    // pair of adjacent elements
    int xorSum = 0;

    // Calculate sum of XOR of all
    // pair of adjacent elements
    for (int i = 0; i < arr.size() - 1; i++)
        xorSum += (arr[i] ^ arr[i + 1]);

    // Check for corner cases
    if (!corner)
        if (xorSum > 2)
            return false;
    else if (corner == 1)
        if (xorSum > 1)
            return false;
    else
        if (xorSum > 0)
            return false;

    // Return true
    return true;
}

// Function to check if all the rows
// have all 1s grouped together or not
bool isInGroupUtil(vector<vector<int>> mat)
{

    // Traverse each row
    for (auto i:mat)
    {

        // Check if all 1s are placed
        // together in the ith row or not
        if (!checkGroup(i))
            return false;
         }
    return true;
}

// Function to check if all 1s in a row
// are grouped together in a matrix or not
void isInGroup(vector<vector<int>> mat)
{

    bool ans = isInGroupUtil(mat);

    //Print the result
    if (ans)
        printf("Yes");
    else
        printf("No");
}

// Driver Code
int main()
{

  // Given matrix
  vector<vector<int>> mat = {{0, 1, 1, 0},
                            {1, 1, 0, 0},
                            {0, 0, 0, 1},
                            {1, 1, 1, 0}};

  // Function Call
  isInGroup(mat);
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to check if all 1s are
    // placed adjacently in an array or not
    static Boolean checkGroup(Vector<Integer> arr)
    {

        // Base Case
        if (arr.size() <= 2)
            return true;
        int corner = arr.get(0) + arr.get(arr.size()-1);

        // Stores the sum of XOR of all
        // pair of adjacent elements
        int xorSum = 0;

        // Calculate sum of XOR of all
        // pair of adjacent elements
        for (int i = 0; i < arr.size() - 1; i++)
            xorSum += (arr.get(i) ^ arr.get(i + 1));

        // Check for corner cases
        if (corner == 0)
            if (xorSum > 2)
                return false;
        else if (corner == 1)
            if (xorSum > 1)
                return false;
        else
            if (xorSum > 0)
                return false;

        // Return true
        return true;
    }

    // Function to check if all the rows
    // have all 1s grouped together or not
    static Boolean isInGroupUtil(int[][] mat)
    {

        // Traverse each row
        for (int i = 0; i < mat.length; i++)
        {
            Vector<Integer> arr = new Vector<Integer>();
            for(int j = 0; j < mat[i].length; j++)
            {
                arr.add(mat[i][j]);
            }
            // Check if all 1s are placed
            // together in the ith row or not
            if (!checkGroup(arr))
                return false;
             }
        return true;
    }

    // Function to check if all 1s in a row
    // are grouped together in a matrix or not
    static void isInGroup(int[][] mat)
    {

        Boolean ans = isInGroupUtil(mat);

        //Print the result
        if (ans)
            System.out.print("Yes");
        else
            System.out.print("No");
    }

    public static void main(String[] args) {
        // Given matrix
        int[][] mat = {{0, 1, 1, 0},
                   {1, 1, 0, 0},
                   {0, 0, 0, 1},
                   {1, 1, 1, 0}};

        // Function Call
        isInGroup(mat);
    }
}

// This code is contributed by decode2207.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if all 1s are
# placed adjacently in an array or not
def checkGroup(arr):

    # Base Case
    if len(arr) <= 2:
        return True

    corner = arr[0] + arr[-1]

    # Stores the sum of XOR of all
    # pair of adjacent elements
    xorSum = 0

    # Calculate sum of XOR of all
    # pair of adjacent elements
    for i in range(len(arr)-1):
        xorSum += (arr[i] ^ arr[i + 1])

    # Check for corner cases
    if not corner:
        if xorSum > 2:
            return False
    elif corner == 1:
        if xorSum > 1:
            return False
    else:
        if xorSum > 0:
            return False

    # Return true
    return True

# Function to check if all the rows
# have all 1s grouped together or not
def isInGroupUtil(mat):

    # Traverse each row
    for i in mat:

        # Check if all 1s are placed
        # together in the ith row or not
        if not checkGroup(i):
            return False

    return True

# Function to check if all 1s in a row
# are grouped together in a matrix or not
def isInGroup(mat):

    ans = isInGroupUtil(mat)

    # Print the result
    if ans:
        print("Yes")
    else:
        print("No")

# Given matrix
mat = [[0, 1, 1, 0], [1, 1, 0, 0],
       [0, 0, 0, 1], [1, 1, 1, 0]]

# Function Call
isInGroup(mat)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to check if all 1s are
    // placed adjacently in an array or not
    static bool checkGroup(List<int> arr)
    {

        // Base Case
        if (arr.Count <= 2)
            return true;
        int corner = arr[0] + arr[arr.Count-1];

        // Stores the sum of XOR of all
        // pair of adjacent elements
        int xorSum = 0;

        // Calculate sum of XOR of all
        // pair of adjacent elements
        for (int i = 0; i < arr.Count - 1; i++)
            xorSum += (arr[i] ^ arr[i + 1]);

        // Check for corner cases
        if (corner == 0)
            if (xorSum > 2)
                return false;
        else if (corner == 1)
            if (xorSum > 1)
                return false;
        else
            if (xorSum > 0)
                return false;

        // Return true
        return true;
    }

    // Function to check if all the rows
    // have all 1s grouped together or not
    static bool isInGroupUtil(int[,] mat)
    {

        // Traverse each row
        for (int i = 0; i < mat.GetLength(1); i++)
        {
            List<int> arr = new List<int>();
            for(int j = 0; j < mat.GetLength(0); j++)
            {
                arr.Add(mat[i,j]);
            }
            // Check if all 1s are placed
            // together in the ith row or not
            if (!checkGroup(arr))
                return false;
            }
        return true;
    }

    // Function to check if all 1s in a row
    // are grouped together in a matrix or not
    static void isInGroup(int[,] mat)
    {

        bool ans = isInGroupUtil(mat);

        //Print the result
        if (ans)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

  // Driver code
  static void Main()
  {

    // Given matrix
    int[,] mat = {{0, 1, 1, 0},
               {1, 1, 0, 0},
               {0, 0, 0, 1},
               {1, 1, 1, 0}};

    // Function Call
    isInGroup(mat);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if all 1s are
    // placed adjacently in an array or not
    function checkGroup(arr)
    {

        // Base Case
        if (arr.length <= 2)
            return true;
        let corner = arr[0] + arr[arr.length-1];

        // Stores the sum of XOR of all
        // pair of adjacent elements
        let xorSum = 0;

        // Calculate sum of XOR of all
        // pair of adjacent elements
        for (let i = 0; i < arr.length - 1; i++)
            xorSum += (arr[i] ^ arr[i + 1]);

        // Check for corner cases
        if (corner == 0)
            if (xorSum > 2)
                return false;
        else if (corner == 1)
            if (xorSum > 1)
                return false;
        else
            if (xorSum > 0)
                return false;

        // Return true
        return true;
    }

    // Function to check if all the rows
    // have all 1s grouped together or not
    function isInGroupUtil(mat)
    {

        // Traverse each row
        for (let i = 0; i < mat.length; i++)
        {
            let arr = []
            for(let j = 0; j < mat[i].length; j++)
            {
                arr.push(mat[i][j]);
            }
            // Check if all 1s are placed
            // together in the ith row or not
            if (!checkGroup(arr))
                return false;
             }
        return true;
    }

    // Function to check if all 1s in a row
    // are grouped together in a matrix or not
    function isInGroup(mat)
    {

        let ans = isInGroupUtil(mat);

        //Print the result
        if (ans)
            document.write("Yes");
        else
            document.write("No");
    }

    // Given matrix
    let mat = [[0, 1, 1, 0],
               [1, 1, 0, 0],
               [0, 0, 0, 1],
               [1, 1, 1, 0]];

    // Function Call
    isInGroup(mat);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*