# 找到引爆所有气球所需的最小箭头数量

> 原文:[https://www . geeksforgeeks . org/find-爆爆所有气球所需的最小箭数/](https://www.geeksforgeeks.org/find-minimum-number-of-arrows-needed-to-burst-all-balloons/)

给定大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **点[][]** ，其中**点【I】**代表从**点【I】【0】**到**点【I】【1】**的 X 坐标区域上的气球。Y 坐标不重要。所有的气球都需要爆裂。要爆裂气球，可在 **(x，0)** 点发射一箭，箭垂直向上行进，将满足条件**点【I】【0】<= x<=点【I】【1】**的所有气球爆裂。任务是找到使所有气球爆炸所需的最小箭数。

**示例:**

> **输入:** N = 4，点数= {{10，16}，{2，8}，{1，6}，{7，12}}
> **输出:** 2
> **解释:**一种方法是射出一箭，例如在 x = 6 时(炸开气球[2，8]和[1，6])，在 x = 11 时射出另一箭(炸开另外两个气球)。
> 
> **输入:** N = 1，点数= {{1，6}}
> **输出:** 1
> **说明:**一箭可爆气球。

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)找到彼此重叠的气球来解决，以便箭头可以穿过所有这样的气球并使它们爆裂。为了达到最佳效果，[按照升序相对于 X 坐标对数组进行排序](https://www.geeksforgeeks.org/sort-an-array-of-pairs-using-java-pair-and-comparator/)。所以，现在考虑 2 个气球，如果第二个气球在第一个气球之前开始，那么它一定在第一个气球之后结束，或者在相同的位置。

> 例如**【1，6】、【2，8】**->第二个气球的起始位置即 2 在第一个气球的结束位置即 6 之前，并且由于数组是排序的，所以第二个气球的末端总是大于第一个气球的末端。第二气球端即 8 位于第一气球端即 6 之后。这向我们展示了[2，6]之间的重叠。

按照以下步骤解决问题:

*   [使用比较器/λ表达式**根据气球的结束位置对数组进行排序。排序(点，(a，b)- >整数。比较(a[1]，b[1])**。](https://www.geeksforgeeks.org/sorting-2d-array-according-values-given-column-java/)
*   制作一个变量**箭头**并用 **1** 初始化它(至少需要一个箭头来炸开气球)
*   制作一个变量**结束**并用**点【0】【1】**初始化它，这将存储第一个气球的结束。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【1，N)** ，并执行以下步骤:
    *   检查下一个气球**点【I】【0】**的起点是否小于终点变量**终点**。
    *   如果是，那么继续迭代。
    *   否则，通过 **1** 增加**箭头**的计数，并将**结束**的值设置为**点【I】【1】**。
*   完成上述步骤后，打印**箭头**的值，作为所需箭头的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

bool cmp(vector<int> a, vector<int> b)
{
    return b[1] > a[1];
}

// Function to find the minimum count of
// arrows required to burst all balloons
int minArrows(vector<vector<int>> points)
{

    // To sort our array according
    // to end position of balloons
    sort(points.begin(), points.end(), cmp);

    // Initialize end variable with
    // the end of first balloon
    int end = points[0][1];

    // Initialize arrow with 1
    int arrow = 1;

    // Iterate through the entire
    // arrow of points
    for (int i = 1; i < points.size(); i++)
    {

        // If the start of ith balloon
        // <= end than do nothing
        if (points[i][0] <= end)
        {
            continue;
        }

        // if start of the next balloon
        // >= end of the first balloon
        // then increment the arrow
        else
        {

            // Update the new end
            end = points[i][1];
            arrow++;
        }
    }

    // Return the total count of arrows
    return arrow;
}

// Driver code
int main()
{

    vector<vector<int>> points = {{10, 16}, {2, 8}, {1, 6}, {7, 12}};
    cout << (minArrows(points));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum count of
    // arrows required to burst all balloons
    public static int minArrows(int points[][])
    {
        // To sort our array according
        // to end position of balloons
        Arrays.sort(points,
                    (a, b) -> Integer.compare(a[1], b[1]));

        // Initialize end variable with
        // the end of first balloon
        int end = points[0][1];

        // Initialize arrow with 1
        int arrow = 1;

        // Iterate through the entire
        // arrow of points
        for (int i = 1; i < points.length; i++) {

            // If the start of ith balloon
            // <= end than do nothing
            if (points[i][0] <= end) {
                continue;
            }

            // if start of the next balloon
            // >= end of the first balloon
            // then increment the arrow
            else {

                // Update the new end
                end = points[i][1];
                arrow++;
            }
        }

        // Return the total count of arrows
        return arrow;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] points
            = { { 10, 16 }, { 2, 8 }, { 1, 6 }, { 7, 12 } };

        System.out.println(
            minArrows(points));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum count of
# arrows required to burst all balloons
def minArrows(points):

    # To sort our array according
    # to end position of balloons
    points = sorted(points,  key = lambda x:x[1])

    # Initialize end variable with
    # the end of first balloon
    end = points[0][1];

    # Initialize arrow with 1
    arrow = 1;

    # Iterate through the entire
    # arrow of points
    for i in range (1, len(points)) :

        # If the start of ith balloon
          # <= end than do nothing
        if (points[i][0] <= end) :
            continue;

        # if start of the next balloon
        # >= end of the first balloon
        # then increment the arrow
        else :

            # Update the new end
            end = points[i][1]       
            arrow = arrow + 1

    # Return the total count of arrows
    return arrow;

# Driver Code
points = [[10, 16 ], [ 2, 8 ], [1, 6 ], [ 7, 12 ]]
print(minArrows(points))

# This code is contributed by AR_Gaurav
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the minimum count of
    // arrows required to burst all balloons
    public static int minArrows(int[][] points)
    {
        // To sort our array according
        // to end position of balloons
        // Array.Sort(points, (a, b) => {return a[1] - b[1];});
        Comparer<int> comparer = Comparer<int>.Default;
        Array.Sort<int[]>(points, (x,y) => comparer.Compare(x[1],y[1]));

        // Initialize end variable with
        // the end of first balloon
        int end = points[0][1];

        // Initialize arrow with 1
        int arrow = 1;

        // Iterate through the entire
        // arrow of points
        for (int i = 1; i < points.Length; i++) {

            // If the start of ith balloon
            // <= end than do nothing
            if (points[i][0] <= end) {
                continue;
            }

            // if start of the next balloon
            // >= end of the first balloon
            // then increment the arrow
            else {

                // Update the new end
                end = points[i][1];
                arrow++;
            }
        }

        // Return the total count of arrows
        return arrow;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[][] points
            = { new int[] { 10, 16 }, new int[] { 2, 8 }, new int[]{ 1, 6 }, new int[]{ 7, 12 } };

        Console.Write(minArrows(points));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

function cmp(a, b) {
  return a[1] - b[1];
}

// Function to find the minimum count of
// arrows required to burst all balloons
function minArrows(points)
{

  // To sort our array according
  // to end position of balloons
  points.sort(cmp);

  // Initialize end variable with
  // the end of first balloon
  let end = points[0][1];

  // Initialize arrow with 1
  let arrow = 1;

  // Iterate through the entire
  // arrow of points
  for (let i = 1; i < points.length; i++) {
    // If the start of ith balloon
    // <= end than do nothing
    if (points[i][0] <= end) {
      continue;
    }

    // if start of the next balloon
    // >= end of the first balloon
    // then increment the arrow
    else {
      // Update the new end
      end = points[i][1];
      arrow++;
    }
  }

  // Return the total count of arrows
  return arrow;
}

// Driver code
let points = [
  [10, 16],
  [2, 8],
  [1, 6],
  [7, 12],
];
document.write(minArrows(points));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*