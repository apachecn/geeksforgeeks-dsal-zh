# 计算通过添加前 N 个自然数的任意排列可以最大化的数组元素

> 原文:[https://www . geesforgeks . org/count-array-elements-可以通过添加第一个 n 个自然数的任意排列来最大化的元素/](https://www.geeksforgeeks.org/count-array-elements-that-can-be-maximized-by-adding-any-permutation-of-first-n-natural-numbers/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过将**【1，N】**的任意排列与给定数组中的相应值相加来确定可以成为数组中最大值的数组元素的总数。

**示例:**

> **输入:** N = 3，arr[] = {8，9，6}
> **输出:** 2
> **说明:**
> 可加入以下排列得到最大值:
> 指数 0 为最大，加入{3，1，2}。因此，arr[] = {8 + 3，9 + 1，6 + 2} = {11，10，8}
> 要使索引 1 最大，请添加{1，3，2}。因此，arr[] = {8 + 1，9 + 3，6 + 2} = {9，12，8}
> 要使索引 2 最大，就不存在 arr[2]变得最大的可能排列。
> 
> **输入:** N = 5 arr[] = {15，14，15，12，14}
> **输出:** 4
> **解释:**
> 可以添加以下排列以获得最大值:
> 要使索引 0 最大，请添加{5，4，3，2，1}。因此，arr[] = {15+5，14+4，15+3，12+2，14+1} = {20，18，18，14，15}
> 要使索引 1 最大，请添加{1，5，4，3，2}。因此，arr[] = {15+1，14+5，15+4，12+3，14+2} = {16，19，19，15，16}
> 要使索引 2 最大，请添加{1，5，4，3，2}。因此，arr[] = {15+1，14+5，15+4，12+3，14+2} = {16，19，19，15，16}
> 要使索引 3 最大，就不存在 arr[3]最大的可能排列。
> 要使索引 4 最大，请添加{1，2，3，4，5}。因此，arr[] = {15+1，14+2，15+3，12+4，14+5} = {16，16，18，16，19}

**天真方法:**最简单的方法是[生成第一个 **N** 自然数的所有可能排列](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)。现在，对于给定数组的每个元素，检查通过添加任何排列是否使当前元素成为结果数组的最大元素。如果发现为真，则增加**计数**并检查下一个元素。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*

**有效方法:**可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来优化上述方法，以检查数组元素是否可以通过添加任何排列而变得最大。按照以下步骤解决上述问题:

1.  [按降序排列给定数组 **arr[]** 。](https://www.geeksforgeeks.org/sorting-algorithms/)
2.  初始化变量**计数****并用 **0** 标记**。
3.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的方法是将最小值即 1 加到最大值，将第二小值加到第二大值，以此类推。
4.  此外，用找到的最大值更新**标记**，直到上述步骤中的每个索引。
5.  在更新变量**标记**之前，通过与**标记**进行比较，检查在其中添加 **N** 时**arr【I】**是否可以变为最大值。如果是，将计数器**计数**增加 **1** 。
6.  完成以上所有步骤后，打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort the
// given array
bool cmp(int x, int y) { return x > y; }

// Function to get the count of values
// that can have the maximum value
void countMaximum(int* a, int n)
{

    // Sort array in decreasing order
    sort(a, a + n, cmp);

    // Stores the answer
    int count = 0;

    // mark stores the maximum value
    // till each index i
    int mark = 0;

    for (int i = 0; i < n; ++i) {

        // Check if arr[i] can be maximum
        if ((a[i] + n >= mark)) {
            count += 1;
        }

        // Update the mark
        mark = max(mark, a[i] + i + 1);
    }

    // Print the total count
    cout << count;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 8, 9, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countMaximum(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to get the count of values
// that can have the maximum value
static void countMaximum(Integer []a, int n)
{

    // Sort array in decreasing order
    Arrays.sort(a, Collections.reverseOrder());

    // Stores the answer
    int count = 0;

    // mark stores the maximum value
    // till each index i
    int mark = 0;

    for(int i = 0; i < n; ++i)
    {

        // Check if arr[i] can be maximum
        if ((a[i] + n >= mark))
        {
            count += 1;
        }

        // Update the mark
        mark = Math.max(mark, a[i] + i + 1);
    }

    // Print the total count
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    Integer arr[] = { 8, 9, 6 };

    int N = arr.length;

    // Function call
    countMaximum(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to get the count of values
# that can have the maximum value
def countMaximum(a, n):

    # Sort array in decreasing order
    a.sort(reverse = True);

    # Stores the answer
    count = 0;

    # mark stores the maximum value
    # till each index i
    mark = 0;

    for i in range(n):

        # Check if arr[i] can be maximum
        if ((a[i] + n >= mark)):
            count += 1;

        # Update the mark
        mark = max(mark, a[i] + i + 1);

    # Print the total count
    print(count);

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 8, 9, 6 ];

    N = len(arr);

    # Function call
    countMaximum(arr, N);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Linq;
using System.Collections.Generic; 

class GFG{

// Function to get the count of values
// that can have the maximum value
static void countMaximum(int []a, int n)
{

    // Sort array in decreasing order
    a.OrderByDescending(c => c).ToArray();

    // Stores the answer
    int count = 0;

    // mark stores the maximum value
    // till each index i
    int mark = 0;

    for(int i = 0; i < n; ++i)
    {

        // Check if arr[i] can be maximum
        if ((a[i] + n >= mark))
        {
            count += 1;
        }

        // Update the mark
        mark = Math.Max(mark, a[i] + i + 1);
    }

    // Print the total count
    Console.Write(count);
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 8, 9, 6 };

    int N = arr.Length;

    // Function call
    countMaximum(arr, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to get the count of values
// that can have the maximum value
function countMaximum(a, n)
{

    // Sort array in decreasing order
    a.sort();
    a.reverse();

    // Stores the answer
    let count = 0;

    // mark stores the maximum value
    // till each index i
    let mark = 0;

    for(let i = 0; i < n; ++i)
    {

        // Check if arr[i] can be maximum
        if ((a[i] + n >= mark))
        {
            count += 1;
        }

        // Update the mark
        mark = Math.max(mark, a[i] + i + 1);
    }

    // Prlet the total count
    document.write(count);
}

// Driver Code

     // Given array arr[]
    let arr = [ 8, 9, 6 ];

    let N = arr.length;

    // Function call
    countMaximum(arr, N);

 // This code is contributed by avijitmonal1998.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*