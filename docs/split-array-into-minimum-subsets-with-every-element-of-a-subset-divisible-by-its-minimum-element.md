# 将数组拆分成最小数量的子集，子集的每个元素都可以被其最小值

整除

> 原文:[https://www . geeksforgeeks . org/将数组拆分为最小子集，子集的每个元素都可以被其最小元素除尽/](https://www.geeksforgeeks.org/split-array-into-minimum-subsets-with-every-element-of-a-subset-divisible-by-its-minimum-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是将数组拆分为最小数量的子集，使得每个元素恰好属于一个子集，并且可以被每个子集中存在的最小元素整除。

**示例:**

> **输入:** arr[] = {10，2，3，5，4，2}
> **输出:** 3
> **解释:**
> 三种可能的组是:
> 
> *   {5，10}，其中所有元素都可以被 5 整除(最小元素)。
> *   {2，2，4}，其中所有元素都可以被 2 整除(最小元素)。
> *   {3}，其中所有元素都可以被 3 整除(最小元素)。
> 
> **输入:** arr[] = {50，50，50，50，50 }
> T3】输出: 1

**方法:**通过使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)并找到每个子集的最小值，可以解决这个问题。按照以下步骤解决问题:

*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化一个变量，比如说**和**，用 **0** 和一个数组 **vis[]** ，用于存储被访问的数组元素。
*   用 **0** 标记**vis【】**数组的所有位置，表示尚未访问的位置。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   如果元素 **arr[i]** 未被访问，则:
        *   将其视为新子集的最小值，并通过 **1** 增加**和**。
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N–1】**，如果元素**arr【j】**未被访问且可被**arr【I】**整除，则设置**vis【j】= 1**。
    *   对每个索引重复上述步骤。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define LL long long
#define MM 1000000007
using namespace std;

// Function to find the minimum number
// of subsets into which given array
// can be split such that the given
// conditions are satisfied
void groupDivision(int arr[], int n)
{
    LL z, i, j, ans;

    // Sort the given array arr[]
    sort(arr, arr + n);

    // Initialize answer
    ans = 0;
    LL vis[n + 5] = { 0 };

    // Iterate for the smaller value
    // which has not been visited
    for (i = 0; i < n; i++) {

        if (!vis[i]) {

            // Mark all elements that
            // are divisible by arr[i]
            for (j = i + 1; j < n; j++) {

                // If jth index has already
                // been visited
                if (vis[j] == 1)
                    continue;

                if (arr[j] % arr[i] == 0)

                    // Mark the jth index
                    // as visisted
                    vis[j] = 1;
            }

            // Increment ans by 1
            ans++;
        }
    }

    // Print the value of ans
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 10, 2, 3, 5, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    groupDivision(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{
static int MM = 1000000007;

// Function to find the minimum number
// of subsets into which given array
// can be split such that the given
// conditions are satisfied
static void groupDivision(int arr[], int n)
{
    int z, i, j, ans;

    // Sort the given array arr[]
    Arrays.sort(arr);

    // Initialize answer
    ans = 0;
    int[] vis = new int[n + 5];
    Arrays.fill(vis, 0);

    // Iterate for the smaller value
    // which has not been visited
    for (i = 0; i < n; i++) {

        if (vis[i] == 0) {

            // Mark all elements that
            // are divisible by arr[i]
            for (j = i + 1; j < n; j++) {

                // If jth index has already
                // been visited
                if (vis[j] == 1)
                    continue;

                if (arr[j] % arr[i] == 0)

                    // Mark the jth index
                    // as visisted
                    vis[j] = 1;
            }

            // Increment ans by 1
            ans++;
        }
    }

    // Print the value of ans
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 10, 2, 3, 5, 4, 2 };
    int N = arr.length;
    groupDivision(arr, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach
MM = 1000000007

# Function to find the minimum number
# of subsets into which given array
# can be split such that the given
# conditions are satisfied
def groupDivision(arr, n):
    global MM
    ans = 0

    # Sort the given array arr[]
    arr = sorted(arr)
    vis = [0]*(n + 5)

    # Iterate for the smaller value
    # which has not been visited
    for i in range(n):
        if (not vis[i]):

            # Mark all elements that
            # are divisible by arr[i]
            for j in range(i + 1, n):

                # If jth index has already
                # been visited
                if (vis[j] == 1):
                    continue
                if (arr[j] % arr[i] == 0):

                    # Mark the jth index
                    # as visisted
                    vis[j] = 1

            # Increment ans by 1
            ans += 1

    # Print the value of ans
    print (ans)

# Driver Code
if __name__ == '__main__':
    arr =[10, 2, 3, 5, 4, 2]
    N = len(arr)
    groupDivision(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

static int MM = 1000000007;

// Function to find the minimum number
// of subsets into which given array
// can be split such that the given
// conditions are satisfied
static void groupDivision(int[] arr, int n)
{
    int z, i, j, ans;

    // Sort the given array arr[]
    Array.Sort(arr);

    // Initialize answer
    ans = 0;
    int[] vis = new int[n + 5];
    for (i = 0; i < n; i++) {
        vis[i] = 0;
    }

    // Iterate for the smaller value
    // which has not been visited
    for (i = 0; i < n; i++) {

        if (vis[i] == 0) {

            // Mark all elements that
            // are divisible by arr[i]
            for (j = i + 1; j < n; j++) {

                // If jth index has already
                // been visited
                if (vis[j] == 1)
                    continue;

                if (arr[j] % arr[i] == 0)

                    // Mark the jth index
                    // as visisted
                    vis[j] = 1;
            }

            // Increment ans by 1
            ans++;
        }
    }

    // Print the value of ans
    Console.Write(ans);
}

// Driver Code
static public void Main ()
{
    int[] arr = { 10, 2, 3, 5, 4, 2 };
    int N = arr.Length;
    groupDivision(arr, N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach
var MM = 1000000007;

// Creating the bblSort function
function bblSort(arr)
{
    for(var i = 0; i < arr.length; i++)
    {

        // Last i elements are already in place 
        for(var j = 0;
                j < (arr.length - i - 1);
                j++)
        {

            // Checking if the item at present iteration
            // is greater than the next iteration
            if (arr[j] > arr[j + 1])
            {

                // If the condition is true
                // then swap them
                var temp = arr[j]
                arr[j] = arr[j + 1]
                arr[j + 1] = temp
            }
        }
    }

    // Return the sorted array
    return (arr);
}

// Function to find the minimum number
// of subsets into which given array
// can be split such that the given
// conditions are satisfied
function groupDivision(arr, n)
{
    var z, i, j, ans;

    // Sort the given array arr
    arr = bblSort(arr);

    // Initialize answer
    ans = 0;
    var vis = Array(n + 5).fill(0);

    // Iterate for the smaller value
    // which has not been visited
    for(i = 0; i < n; i++)
    {
        if (vis[i] == 0)
        {

            // Mark all elements that
            // are divisible by arr[i]
            for(j = i + 1; j < n; j++)
            {

                // If jth index has already
                // been visited
                if (vis[j] == 1)
                    continue;

                if (arr[j] % arr[i] == 0)

                    // Mark the jth index
                    // as visisted
                    vis[j] = 1;
            }

            // Increment ans by 1
            ans++;
        }
    }

    // Print the value of ans
    document.write(ans);
}

// Driver Code
var arr = [ 10, 2, 3, 5, 4, 2 ];
var N = arr.length;

groupDivision(arr, N);

// This code is contributed by gauravrajput1

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*