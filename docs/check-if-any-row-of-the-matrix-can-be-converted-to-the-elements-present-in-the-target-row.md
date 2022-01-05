# 检查矩阵的任何一行是否可以转换为目标行中的元素

> 原文:[https://www . geeksforgeeks . org/check-if-no-row-of-the-matrix-can-convert-to-elements-present-in-target-row/](https://www.geeksforgeeks.org/check-if-any-row-of-the-matrix-can-be-converted-to-the-elements-present-in-the-target-row/)

给定维度为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**和整数为 **M** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**target【】**，任务是通过选择矩阵的任意两行来检查矩阵的任意一行是否可以等于数组**target【】**，并将任意一行的每个元素更新为所选两行的相应索引处的元素的最大值。如果可以，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** mat[][] = {{2，5，3}，{2，8，4}，{1，5，7}}，target[] = {2，5，7}
> **输出:** Yes
> **解释:**
> 对第 3 行和第 1 行执行给定操作并修改第 3 行后，变为:
> 【max(1，2)，max(5，5)，max(7，3)】=【2，5，7】等于
> 
> **输入:** mat[][] = {{3，4，5}，{4，5，6}}，target[] = {3，2，5}
> **输出:**否

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，其思想是创建一个辅助的[数组](https://www.geeksforgeeks.org/array-class-c/)**comp【】**和[遍历矩阵](https://www.geeksforgeeks.org/how-to-iterate-through-each-element-in-n-dimensional-matrix-in-matlab/)的每一行，如果这些行的元素小于或等于目标数组中相应的元素，则对该行的每一个元素执行 [Math.max()](https://www.geeksforgeeks.org/java-math-max-method-examples/) 操作，并执行 **comp** 。可以遵循以下步骤:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-class-c/)，说 **comp[]** 大小 **M** 每个元素等于 [**INT_MIN**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 。
*   [遍历矩阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**mat【】【】**并针对每一行检查该行中的所有值是否小于或等于**目标**数组中的相应值。如果发现为真，则更新 **comp[]** 数组，取 **comp[]** 中每个元素与行中相应元素的最大值。
*   经过以上步骤，如果数组 **comp[]** 与数组 **target[]** 相同，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if target array
// can be formed from any row in trio
// with the given operations
int checkPossibleOrNot(vector<vector<int> >& mat,
                       vector<int>& target)
{

    // Initialize comp[] of size M
    vector<int> comp(mat[0].size(), INT_MIN);

    // Traverse the matrix mat[]
    for (auto val : mat) {

        // Check if all values in a row
        // is at most the corresponding
        // values in target[] array
        if (val[0] <= target[0] && val[1] <= target[1]
            && val[2] <= target[2])

            // Update the comp[]
            comp = { max(comp[0], val[0]),
                     max(comp[1], val[1]),
                     max(comp[2], val[2]) };
    }

    // Return the possibility
    return (comp == target);
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 2, 5, 3 }, { 2, 8, 4 }, { 1, 5, 7 } };
    vector<int> target = { 2, 5, 7 };

    string ans
        = checkPossibleOrNot(mat, target) ? "Yes" : "NO";
    cout << ans;

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to check if target array
    // can be formed from any row in trio
    // with the given operations
    public static boolean checkPossibleOrNot(
        int[][] mat, int[] target)
    {

        // Initialize comp[] of size M
        int[] comp = new int[mat[0].length];

        // Fill the array with minimum
        // value of integer
        Arrays.fill(comp, Integer.MIN_VALUE);

        // Traverse the matrix mat[]
        for (int[] val : mat) {

            // Check if all values in a row
            // is at most the corresponding
            // values in target[] array
            if (val[0] <= target[0]
                && val[1] <= target[1]
                && val[2] <= target[2])

                // Update the comp[]
                comp = new int[] { Math.max(
                                       comp[0], val[0]),
                                   Math.max(
                                       comp[1], val[1]),
                                   Math.max(
                                       comp[2], val[2]) };
        }

        // Return the possibility
        return Arrays.equals(comp, target);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] mat
            = { { 2, 5, 3 }, { 2, 8, 4 }, { 1, 5, 7 } };
        int[] target = { 2, 5, 7 };

        String ans = checkPossibleOrNot(
                         mat, target)
                         ? "Yes"
                         : "NO";
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to check if target array
# can be formed from any row in trio
# with the given operations
def checkPossibleOrNot(mat, target) :

    comp = [] ;
    INT_MIN = - (sys.maxsize - 1)

    # Initialize comp[] of size M
    for i in range(len(mat[0])) :
        comp.append(INT_MIN)

    # Traverse the matrix mat[]
    for val in mat :

        # Check if all values in a row
        # is at most the corresponding
        # values in target[] array
        if (val[0] <= target[0] and val[1] <= target[1] and val[2] <= target[2]) :

            # Update the comp[]
            comp = [ max(comp[0], val[0]), max(comp[1], val[1]), max(comp[2], val[2]) ];

    if comp == target :

        # Return the possibility
        return True
    else :

        # Return the possibility
        return False

# Driver Code
if __name__ == "__main__" :

    mat = [ [ 2, 5, 3 ], [ 2, 8, 4 ], [ 1, 5, 7 ] ];
    target = [ 2, 5, 7 ];

    ans = checkPossibleOrNot(mat, target)

    if ans:
        print("Yes")
    else :
        print("NO")

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

public class GFG {

    // Function to check if target array
    // can be formed from any row in trio
    // with the given operations
    public static bool checkPossibleOrNot(
        int [,]mat, int[] target)
    {

        // Initialize comp[] of size M
        int[] comp = new int[mat.GetLength(0)];

        // Fill the array with minimum
        // value of integer
        for (int i = 0; i < mat.GetLength(0); i++)
            comp[i] = int.MinValue;

        // Traverse the matrix mat[]
        for (int i = 0; i < mat.GetLength(0); i++){

            int []val = {mat[i, 0], mat[i, 1], mat[i, 2]};

            // Check if all values in a row
            // is at most the corresponding
            // values in target[] array
            if (val[0] <= target[0]
                && val[1] <= target[1]
                && val[2] <= target[2])

                // Update the comp[]
                comp = new int[] { Math.Max(
                                    comp[0], val[0]),
                                Math.Max(
                                    comp[1], val[1]),
                                Math.Max(
                                    comp[2], val[2]) };
        }

        // Return the possibility
        return comp.SequenceEqual(target);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[,] mat = { { 2, 5, 3 }, { 2, 8, 4 }, { 1, 5, 7 } };
        int[] target = { 2, 5, 7 };

        string ans = checkPossibleOrNot(
                        mat, target)
                        ? "Yes"
                        : "NO";
        Console.WriteLine(ans);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if target array
// can be formed from any row in trio
// with the given operations
function checkPossibleOrNot(mat, target)
{

  // Initialize comp[] of size M
  let comp = new Array(mat[0].length).fill(Number.MIN_SAFE_INTEGER);

  // Traverse the matrix mat[]
  for (let val of mat)
  {

    // Check if all values in a row
    // is at most the corresponding
    // values in target[] array
    if (val[0] <= target[0] && val[1] <= target[1] && val[2] <= target[2])

      // Update the comp[]
      comp = [
        Math.max(comp[0], val[0]),
        Math.max(comp[1], val[1]),
        Math.max(comp[2], val[2]),
      ];
  }

  // Return the possibility
  return comp.join("") == target.join("");
}

// Driver Code

let mat = [
  [2, 5, 3],
  [2, 8, 4],
  [1, 5, 7],
];
let target = [2, 5, 7];

let ans = checkPossibleOrNot(mat, target) ? "Yes" : "NO";
document.write(ans);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*