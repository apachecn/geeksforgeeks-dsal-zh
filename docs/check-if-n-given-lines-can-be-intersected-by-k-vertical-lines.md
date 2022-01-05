# 检查 N 条给定的线是否可以被 K 条垂直线相交

> 原文:[https://www . geesforgeks . org/check-if-n-给定行-可被 k-垂直线相交/](https://www.geeksforgeeks.org/check-if-n-given-lines-can-be-intersected-by-k-vertical-lines/)

给定由大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **位置【】【】**表示的 **N** 水平线，其中**位置【I】**表示**I<sup>th</sup>T13】水平线，该水平线具有**x**-从**位置【I】【0】**到**位置【I】【1】**的坐标和整数 **K，【T21****

**示例:**

> **输入:** N = 4，K = 2，位置[][] = [[1，4]，[6，8]，[7，9]，[10，15]]
> T3】输出: NO
> **说明:**在给定的例子中，在[1，7，10]处画线。在 1 处绘制的线将与第一条线相交，在位置 7 处的线将与第二条线和第三条线相交，在 10 处绘制的线将与第四条线相交。因此，至少需要 3 根杆。因此，这是不可能的
> 
> **输入:** N = 5，K = 3，位置[][] = [[1，6]，[3，5]，[2，4]，[8，12]，[10，24]]
> **输出:**是

**方法:**思路是用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)通过[排序](https://www.geeksforgeeks.org/sorting-algorithms/)把**位置[][]** [排列](https://www.geeksforgeeks.org/array-data-structure/)来解决这个问题，用 1 条线，相交尽可能多的线，以此类推。按照以下步骤解决问题:

*   [按升序排列](https://www.geeksforgeeks.org/sorting-algorithms/)[阵](https://www.geeksforgeeks.org/array-data-structure/)T4【位置】[] 。
*   将变量**和**初始化为 **1** 以存储答案，将 **r** 初始化为**位置【0】【1】**以存储终点，直到其他水平线可以与给定的考虑垂直线相交的特定点。
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，说我**、**并执行以下步骤:
    *   如果**位置[i][0]** 小于 **r，**则将 **r** 的值设置为 **r** 或**位置[i][1]的最小值。**
    *   否则，用 **1** 加上**和**的值，将 **r** 的值设置为**位置[i][1]。**
*   如果 **k** 大于等于 **ans，**则打印**“是”**，否则打印**“否”**。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to intersect n lines using k vertical lines
void findIfPossible(int n, int k,
                    vector<vector<int> > position)
{

    sort(position.begin(), position.end());

    int ans = 1;

    // Track the point till a particular
    // vertical line can intersect
    int r = position[0][1];

    // Iterate over the range
    for (int i = 1; i < n; i++) {

        if (position[i][0] <= r) {

            r = min(r, position[i][1]);
        }

        else {

            ans++;

            r = position[i][1];
        }
    }
    if (k >= ans)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

// Driver Code
int main()
{

    int n = 5;
    int k = 2;
    vector<vector<int> > position = {
        { 2, 5 }, { 4, 6 }, { 7, 16 }, { 9, 10 }, { 10, 17 }
    };

    findIfPossible(n, k, position);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to check if it is possible
  // to intersect n lines using k vertical lines
  static void findIfPossible(int n, int k,
                             int[][] position)
  {

    Arrays.sort(position, Comparator.comparingDouble(o -> o[0]));

    int ans = 1;

    // Track the point till a particular
    // vertical line can intersect
    int r = position[0][1];

    // Iterate over the range
    for (int i = 1; i < n; i++) {

      if (position[i][0] <= r) {

        r = Math.min(r, position[i][1]);
      }

      else {

        ans++;

        r = position[i][1];
      }
    }
    if (k >= ans)
      System.out.println("YES");
    else
      System.out.println("NO");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int n = 5;
    int k = 2;
    int[][] position = {
      { 2, 5 }, { 4, 6 }, { 7, 16 }, { 9, 10 }, { 10, 17 }
    };

    findIfPossible(n, k, position);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to check if it is possible
# to intersect n lines using k vertical lines
def findIfPossible(n, k, position):
    position.sort()
    ans = 1

    # Track the point till a particular
    # vertical line can intersect
    r = position[0][1]

    # Iterate over the range
    for i in range(1, n):
        if (position[i][0] <= r):
            r = min(r, position[i][1])
        else:
            ans += 1
            r = position[i][1]
    if (k >= ans):
        print("YES")
    else:
        print("NO")

# Driver Code
n = 5
k = 2
position = [[2, 5], [4, 6], [7, 16], [9, 10], [10, 17]]
findIfPossible(n, k, position)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static void Sort(int[,] arr)
{
    for(int i = 0; i < arr.GetLength(0); i++)
    {
        for(int j = arr.GetLength(1) - 1; j > 0; j--)
        {
            for(int k = 0; k < j; k++)
            {
                if (arr[i, k] > arr[i, k + 1])
                {
                    int myTemp = arr[i, k];
                    arr[i, k] = arr[i, k + 1];
                    arr[i, k + 1] = myTemp;
                }
            }
        }
    } 
}

// Function to check if it is possible
// to intersect n lines using k vertical lines
static void findIfPossible(int n, int k,
                           int[,] position)
{
    Sort(position);

    int ans = 1;

    // Track the point till a particular
    // vertical line can intersect
    int r = position[0, 1];

    // Iterate over the range
    for(int i = 1; i < n; i++)
    {
        if (position[i, 0] <= r)
        {
            r = Math.Min(r, position[i, 1]);
        }
        else
        {
            ans++;
            r = position[i, 1];
        }
    }
    if (k >= ans)
        Console.Write("YES");
    else
        Console.Write("NO");
}

// Driver Code
public static void Main(string[] args)
{
    int n = 5;
    int k = 2;
    int[,] position = { { 2, 5 }, { 4, 6 },
                        { 7, 16 }, { 9, 10 },
                        { 10, 17 } };

    findIfPossible(n, k, position);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if it is possible
// to intersect n lines using k vertical lines
function findIfPossible(n, k, position)
{
     position = position.sort(function(a, b)
     {
    return a[0]-b[0]
    });

    var i;
    var ans = 1;

    // Track the point till a particular
    // vertical line can intersect
    var r = position[0][1];

    // Iterate over the range
    for (i = 1; i < n; i++) {

        if (position[i][0] <= r) {

            r = Math.min(r, position[i][1]);
        }

        else {

            ans++;

            r = position[i][1];
        }
    }

    if (k >= ans)
        document.write("YES");
    else
        document.write("NO");
}

// Driver Code

    var n = 5;
    var k = 2;
    var position = [[2, 5],[4, 6], [7, 16],[9, 10],[10, 17]];

    findIfPossible(n, k, position);

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*