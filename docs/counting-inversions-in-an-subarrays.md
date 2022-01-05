# 计算子阵列中的反转

> 原文:[https://www . geesforgeks . org/counting-inversion-in-an-subarrays/](https://www.geeksforgeeks.org/counting-inversions-in-an-subarrays/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，目标是计算所有子数组中的逆序数。反转是一对指数 **i** 和 **j** ，使得 **i > j** 和**arr【I】<arr【j】**。从索引 **x** 到 **y ( x < = y)** 的子数组由元素的 **arr[x]、arr[x+1]、…、arr[y]** 组成。数组 **arr[]** 也可以包含重复的元素。

**示例:**

> **输入** : arr[] = {3，6，1，6，5，3， 9}
> **输出**:
> 0 0 2 2 4 7 7
> 0 0 1 3 6 6
> 0 0 0 1 3
> 0 0 0 1 3 3
> 0 0 0 0 1 1 1
> 0 0 0 0 0 0 0
> 0 0 0 0 0 0 0 0
> **解释** :
> 输出的第 I 行和第 j 列中的元素表示从 考虑 i = 1 和 j = 4(假设基于 0 的索引)，子阵列{6，1，6，5}中的反转数为 3。元素对是(6，1)、(6，5)和(6，5)(从第二个 6 开始)。
> 
> **输入** : arr[] = {3，2，1}
> **输出**:
> 0 1 3
> 0 0 1
> 0 0
> T9】解释 :
> 从索引 0 到 1 有 1 个反转，从索引 2 到 3 有 1 个反转，从索引 0 到 2 有 3 个反转。如果 i > = j，输出的第 I 行和第 j 列为 0。

**天真方法:**天真方法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并计算每个子阵列中的反转次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// inversions in all the sub-arrays
void findSubarrayInversions(int arr[], int n)
{

    int inversions[n][n];

    // Initializing the inversion count
    // of each subarray to 0
    // inversions[i][j] will denote
    // the number of inversions
    // from index i to index j inclusive
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            inversions[i][j] = 0;
        }
    }

    // Generating all subarray
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int ans = 0;
            // counting the number of inversions
            // for a subarray
            for (int x = i; x <= j; x++) {
                for (int y = x; y <= j; y++) {
                    if (arr[x] > arr[y])
                        ans++;
                }
            }

            inversions[i][j] = ans;
        }
    }

    // Printing the number of inversions
    // of all subarrays
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << inversions[i][j] << " ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{

    // Given Input
    int n = 7;
    int arr[n] = { 3, 6, 1, 6, 5, 3, 9 };

    // Function Call
    findSubarrayInversions(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the number of
// inversions in all the sub-arrays
static void findSubarrayInversions(int arr[], int n)
{
    int [][]inversions = new int[n][n];

    // Initializing the inversion count
    // of each subarray to 0
    // inversions[i][j] will denote
    // the number of inversions
    // from index i to index j inclusive
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            inversions[i][j] = 0;
        }
    }

    // Generating all subarray
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {
            int ans = 0;

            // Counting the number of inversions
            // for a subarray
            for(int x = i; x <= j; x++)
            {
                for(int y = x; y <= j; y++)
                {
                    if (arr[x] > arr[y])
                        ans++;
                }
            }
            inversions[i][j] = ans;
        }
    }

    // Printing the number of inversions
    // of all subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            System.out.print(inversions[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int n = 7;
    int []arr = { 3, 6, 1, 6, 5, 3, 9 };

    // Function Call
    findSubarrayInversions(arr, n);
}
}

// This code is contributed by SoumikMondal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# inversions in all the sub-arrays
def findSubarrayInversions(arr, n):

    inversions = [[0 for i in range(n)]
                     for j in range(n)]

    # Initializing the inversion count
    # of each subarray to 0
    # inversions[i][j] will denote
    # the number of inversions
    # from index i to index j inclusive
    # Generating all subarray
    for i in range(0, n):
        for j in range(0, n):
            ans = 0

            # Counting the number of inversions
            # for a subarray
            for x in range(i, j + 1):
                for y in range(x, j + 1):
                    if (arr[x] > arr[y]):
                        ans += 1

            # Print(ans)
            inversions[i][j] = ans

    # Printing the number of inversions
    # of all subarrays
    for i in range(0, n):
        for j in range(0, n):
            print(inversions[i][j], end = " ")

        print()

# Driver Code

# Given Input
n = 7
arr = [ 3, 6, 1, 6, 5, 3, 9 ]

# Function Call
findSubarrayInversions(arr, n)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// inversions in all the sub-arrays
static void findSubarrayInversions(int []arr, int n)
{

    int [,]inversions = new int[n,n];

    // Initializing the inversion count
    // of each subarray to 0
    // inversions[i][j] will denote
    // the number of inversions
    // from index i to index j inclusive
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            inversions[i,j] = 0;
        }
    }

    // Generating all subarray
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {
            int ans = 0;

            // counting the number of inversions
            // for a subarray
            for (int x = i; x <= j; x++) {
                for (int y = x; y <= j; y++) {
                    if (arr[x] > arr[y])
                        ans++;
                }
            }

            inversions[i,j] = ans;
        }
    }

    // Printing the number of inversions
    // of all subarrays
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            Console.Write(inversions[i,j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int n = 7;
    int []arr = { 3, 6, 1, 6, 5, 3, 9 };

    // Function Call
    findSubarrayInversions(arr, n);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of
// inversions in all the sub-arrays
function findSubarrayInversions(arr, n) {

    let inversions = new Array(n).fill(0).map(() => new Array(n));

    // Initializing the inversion count
    // of each subarray to 0
    // inversions[i][j] will denote
    // the number of inversions
    // from index i to index j inclusive
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            inversions[i][j] = 0;
        }
    }

    // Generating all subarray
    for (let i = 0; i < n; i++) {
        for (let j = i; j < n; j++) {
            let ans = 0;
            // counting the number of inversions
            // for a subarray
            for (let x = i; x <= j; x++) {
                for (let y = x; y <= j; y++) {
                    if (arr[x] > arr[y])
                        ans++;
                }
            }

            inversions[i][j] = ans;
        }
    }

    // Printing the number of inversions
    // of all subarrays
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            document.write(inversions[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code

// Given Input
let n = 7;
let arr = [3, 6, 1, 6, 5, 3, 9];

// Function Call

findSubarrayInversions(arr, n);

</script>
```

**Output:** 

```
0 0 2 2 4 7 7 
0 0 1 1 3 6 6 
0 0 0 0 1 3 3 
0 0 0 0 1 3 3 
0 0 0 0 0 1 1 
0 0 0 0 0 0 0 
0 0 0 0 0 0 0
```

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**使用这里给出的方法可以稍微优化一下上面的方法，找到一个子数组中的逆序数。首先看一些解决这个问题的观察:

> 首先创建一个 **2d** 数组**大[][]** ，其中**大[i][j]** 表示范围 **i** 到 **j** 中大于 **arr[i]的元素数量。**迭代数组，对于每个元素，找出其右边小于该元素的元素数。这可以在 O(N^2).用一种天真的方法来实现现在要找出 x 到 y 范围内的倒数，答案将是**大于[x][y] +大于[x+1][y] + … +大于[y-1][y] +大于[y][y]。**
> 
> 使用**大于【】【】**的表格，可以在 **O(n)** 中为每个子阵列计算该值，从而得到复杂度为 **O(n^3)** 的值。(有 **O(n^2)** 子阵，需要 **O(n)** 时间来计算每个子阵中的逆序数)。要在 **O(1)** 中找到该值，请每次从 **greater[][]** 表构建前缀和表，其中**前缀[i][j]** 表示**greater[0][j]+greater[1][j]+…+greater[I][j]的值。**此表也可建在 **O(N^2)** 时间。现在，从 **x** 到 **y** (含)的每个子数组的答案将变成**前缀[y][y]–如果 **x > = 1** 则前缀[x-1][y]** ，如果 x = 0 则前缀[y][y]。

请按照以下步骤解决此问题:

*   初始化数组**大于[][]** 以存储，其中**大于【I】【j】**表示范围 **i** 到 **j** 中大于**arr【I】的元素数量，前缀【】【】**存储子数组的前缀和，**逆矩阵【】[]** 存储逆矩阵的数量。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代:
    *   [使用变量 **j:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N-1】**内迭代
        *   将**大[i][j]** 更新为**大[i][j-1]**
        *   如果 **arr[i]** 大于 **arr[j]，**，那么将**arr[I][j]**增加 **1。**
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代:
    *   将**前缀【0】【j】**更新为**大【0】【j】**
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N-1】**内迭代，并将**前缀【I】【j】**更新为**前缀【I-1】【j】+大于【I】【j】。**
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代:
    *   [使用变量 **j:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I，N-1】**中迭代
        *   如果 **i = 0，**则更新**逆项【I】【j】**为**前缀【j】【j】**
        *   否则，将**倒位[i][j]** 更新为**前缀[j][j] +前缀[i-1][j]。**
*   完成以上步骤后，打印**倒排[][]** 数组作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// inversions in all the sub-arrays
void findSubarrayInversions(int arr[], int n)
{

    int greater[n][n];
    int prefix[n][n];
    int inversions[n][n];

    // Initializing the arrays to 0
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            greater[i][j] = 0;
            prefix[i][j] = 0;
            inversions[i][j] = 0;
        }
    }

    // For each pair of indices i and j
    // calculating the number of elements
    // from i to j inclusive which are
    // greater than arr[i]
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            greater[i][j] = greater[i][j - 1];
            if (arr[i] > arr[j])
                greater[i][j]++;
        }
    }

    // Building the prefix table.
    // Prefix[i][j] denotes the sum of
    // greater[0][j], greater[1][j] ... greater[i][j]
    for (int j = 0; j < n; j++) {
        prefix[0][j] = greater[0][j];
        for (int i = 1; i < n; i++) {
            prefix[i][j] = prefix[i - 1][j] + greater[i][j];
        }
    }

    // Calculating the inversion count for
    // each subarray using the prefix table
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            if (i == 0)
                inversions[i][j] = prefix[j][j];
            else
                inversions[i][j] = prefix[j][j]
                                   - prefix[i - 1][j];
        }
    }

    // Printing the values of the number
    // of inversions in each subarray
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << inversions[i][j] << " ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{

    // Given Input
    int n = 7;
    int arr[n] = { 3, 6, 1, 6, 5, 3, 9 };

    // Function Call
    findSubarrayInversions(arr, n);
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# inversions in all the sub-arrays
def findSubarrayInversions(arr, n):

    # Initializing the arrays to 0
    greater = [[0 for i in range(n)]
                  for j in range(n)]
    prefix = [[0 for i in range(n)]
                 for j in range(n)]
    inversions = [[0 for i in range(n)]
                     for j in range(n)]

    # For each pair of indices i and j
    # calculating the number of elements
    # from i to j inclusive which are
    # greater than arr[i]
    for i in range(0, n):
        for j in range(i + 1, n):
            greater[i][j] = greater[i][j - 1]

            if (arr[i] > arr[j]):
                greater[i][j] += 1

    # Building the prefix table.
    # Prefix[i][j] denotes the sum of
    # greater[0][j], greater[1][j] ... greater[i][j]
    for j in range(0, n):
        prefix[0][j] = greater[0][j]
        for i in range(1, n):
            prefix[i][j] = (prefix[i - 1][j] +
                            greater[i][j])

    # Calculating the inversion count for
    # each subarray using the prefix table
    for i in range(0, n):
        for j in range(i, n):
            if (i == 0):
                inversions[i][j] = prefix[j][j]
            else:
                inversions[i][j] = (prefix[j][j] -
                                    prefix[i - 1][j])

    # Printing the values of the number
    # of inversions in each subarray
    for i in range(0, n):
        for j in range(0, n):
            print(inversions[i][j], end = " ")

        print()

# Driver Code
# Given Input
n = 7
arr = [ 3, 6, 1, 6, 5, 3, 9 ]

# Function Call
findSubarrayInversions(arr, n)

# This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number of
// inversions in all the sub-arrays
function findSubarrayInversions(arr, n) {
  let greater = new Array(n).fill(0).map(() => new Array(n).fill(0));
  let prefix = new Array(n).fill(0).map(() => new Array(n).fill(0));
  let inversions = new Array(n).fill(0).map(() => new Array(n).fill(0));

  // Initializing the arrays to 0
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      greater[i][j] = 0;
      prefix[i][j] = 0;
      inversions[i][j] = 0;
    }
  }

  // For each pair of indices i and j
  // calculating the number of elements
  // from i to j inclusive which are
  // greater than arr[i]
  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j < n; j++) {
      greater[i][j] = greater[i][j - 1];
      if (arr[i] > arr[j]) greater[i][j]++;
    }
  }

  // Building the prefix table.
  // Prefix[i][j] denotes the sum of
  // greater[0][j], greater[1][j] ... greater[i][j]
  for (let j = 0; j < n; j++) {
    prefix[0][j] = greater[0][j];
    for (let i = 1; i < n; i++) {
      prefix[i][j] = prefix[i - 1][j] + greater[i][j];
    }
  }

  // Calculating the inversion count for
  // each subarray using the prefix table
  for (let i = 0; i < n; i++) {
    for (let j = i; j < n; j++) {
      if (i == 0) inversions[i][j] = prefix[j][j];
      else inversions[i][j] = prefix[j][j] - prefix[i - 1][j];
    }
  }

  // Printing the values of the number
  // of inversions in each subarray
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      document.write(inversions[i][j] + " ");
    }
    document.write("<br>");
  }
}

// Driver Code

// Given Input
let n = 7;
let arr = [3, 6, 1, 6, 5, 3, 9];

// Function Call
findSubarrayInversions(arr, n);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
0 0 2 2 4 7 7 
0 0 1 1 3 6 6 
0 0 0 0 1 3 3 
0 0 0 0 1 3 3 
0 0 0 0 0 1 1 
0 0 0 0 0 0 0 
0 0 0 0 0 0 0
```

时间复杂度: **O(N <sup>2</sup> )**
空间复杂度: **O(N <sup>2</sup> )**

**<u>笔记-</u>**

*   通过在大[][]表的顶部构建前缀[][]表，可以节省一些空间，但顺序仍然保持不变。
*   如果你想找到所有子阵列中反转的确切计数，因为子阵列的数量总是 O(N^2).，那么不可能比 O(N^2 表现得更好)