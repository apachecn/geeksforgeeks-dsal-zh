# 查找数组中的第二大元素|集合 2

> 原文:[https://www . geesforgeks . org/find-第二大数组元素集-2/](https://www.geeksforgeeks.org/find-second-largest-element-in-an-array-set-2/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是使用**N+log<sub>2</sub>(N)–2**个比较找到给定数组中的第二大元素。

**示例:**

> **输入** : arr[] = {22，33，14，55，100，12}
> **输出** : 55
> 
> **输入** : arr[] = {35，23，12，35，19，100}
> **输出** : 35

**排序和两次遍历方法:**参考[找到数组中的第二大元素](https://www.geeksforgeeks.org/find-second-largest-element-array/)了解使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)以及遍历数组两次的解决方案。

**高效方法:**
按照以下步骤解决问题:

*   从给定的数组中找到**最大的**元素，并跟踪所有元素**将**与最大的元素进行比较。
    *   将当前阵列分成两个等长的子阵列。
    *   对于每个子阵列，**递归地**找到**最大元素**，并返回一个数组，其中**第一个索引**包含该数组的长度，**第二个索引**元素包含**最大元素**，其余数组包含与最大元素相比较的元素。
    *   现在，从两个子阵列返回的两个阵列中，比较两个子阵列的最大元素，并返回包含两个子阵列中最大元素的阵列。
*   由**FindMaggest()**返回的最终数组包含其在第一个索引中的大小、在第二个索引中数组的最大元素以及与剩余索引中最大元素相比较的元素。使用**find maximum()**重复上述步骤，从比较元素列表中找到数组的第二大**元素**。

> **算法分析:**
> 从算法中可以清楚地看到**find maximum()**算法的时间复杂度为**O(N)**【N:数组大小】
> 因此，进行 **(N-1)** **比较**。
> 现在**find maximum()**返回的数组大小为 **log <sub>2</sub> (N) + 2、**其中 **log <sub>2</sub> (N)元素**是与**最大元素**进行比较的元素。
> 因此，为了找到第二大元素，使用**log<sub>2</sub>(N)–1**比较来计算这些 **log <sub>2</sub> (N)元素**中最大的元素。
> 
> 因此，**比较总数**= N–1+log<sub>2</sub>(N)–1 =**N+log<sub>2</sub>(N)–2**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// element in the array arr[]
vector<int> findLargest(int beg, int end,
                vector<int> arr, int n)
{

    // Base Condition
    if (beg == end)
    {

        // Initialize an empty list
        vector<int> compared(n, 0);
        compared[0] = 1;
        compared[1] = arr[beg];
        return compared;
    }

    // Divide the array into two equal
    // length subarrays and recursively
    // find the largest among the two
    vector<int> compared1 = findLargest(
                            beg, (beg + end) / 2,
                            arr, n);

    vector<int> compared2 = findLargest(
                            (beg + end) / 2 + 1,
                            end, arr, n);

    if (compared1[1] > compared2[1])
    {
        int k = compared1[0] + 1;

        // Store length of compared1[]
        // in the first index
        compared1[0] = k;

        // Store the maximum element
        compared1[k] = compared2[1];

        // Return compared1 which
        // contains the maximum element
        return compared1;
    }
    else
    {
        int k = compared2[0] + 1;

        // Store length of compared2[]
        // in the first index
        compared2[0] = k;

        // Store the maximum element
        compared2[k] = compared1[1];

        // Return compared2[] which
        // contains the maximum element
        return compared2;
    }
}

// Function to print the second largest
// element in the array arr[]
void findSecondLargest(int end, vector<int> arr)
{

    // Find the largest element in arr[]
    vector<int> compared1 = findLargest(
                            0, end - 1, arr, end);

    // Find the second largest element
    // in arr[]
    vector<int> compared2 = findLargest(
                            2, compared1[0] + 2,
                            compared1,
                            compared1[0]);

    // Print the second largest element
    cout << compared2[1];
}

// Driver code
int main()
{
    int N = 10;

    vector<int> arr{ 20, 1990, 12, 1110, 1,
                    59, 12, 15, 120, 1110};

    findSecondLargest(N, arr);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the largest
// element in the array arr[]
static int[] findLargest(int beg, int end,
                        int []arr, int n)
{
// Base Condition
if (beg == end)
{
    // Initialize an empty list
    int []compared = new int[n];
    compared[0] = 1;
    compared[1] = arr[beg];
    return compared;
}

// Divide the array into two equal
// length subarrays and recursively
// find the largest among the two
int []compared1 = findLargest(beg,
                            (beg + end) /
                                2, arr, n);

int []compared2 = findLargest((beg + end) /
                                2 + 1,
                                end, arr, n);

if (compared1[1] > compared2[1])
{
    int k = compared1[0] + 1;

    // Store length of compared1[]
    // in the first index
    compared1[0] = k;

    // Store the maximum element
    compared1[k] = compared2[1];

    // Return compared1 which
    // contains the maximum element
    return compared1;
}
else
{
    int k = compared2[0] + 1;

    // Store length of compared2[]
    // in the first index
    compared2[0] = k;

    // Store the maximum element
    compared2[k] = compared1[1];

    // Return compared2[] which
    // contains the maximum element
    return compared2;
}
}

// Function to print the second largest
// element in the array arr[]
static void findSecondLargest(int end,
                            int []arr)
{
    // Find the largest element in arr[]
    int []compared1 = findLargest(0, end - 1,
                                arr, end);

    // Find the second largest element
    // in arr[]
    int []compared2 = findLargest(2, compared1[0] + 2,
                                compared1,
                                compared1[0]);

    // Print the second largest element
    System.out.print(compared2[1]);
}

// Driver code
public static void main(String[] args)
{
  int N = 10;
  int []arr ={20, 1990, 12, 1110, 1,
              59, 12, 15, 120, 1110};
  findSecondLargest(N, arr);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find the largest
# element in the array arr[]
def findLargest(beg, end, arr, n):

    # Base Condition
    if(beg == end):

        # Initialize an empty list
        compared = [0]*n
        compared[0] = 1
        compared[1] = arr[beg]
        return compared

    # Divide the array into two equal
    # length subarrays and recursively
    # find the largest among the two
    compared1 = findLargest(beg, (beg+end)//2,
                            arr, n)

    compared2 = findLargest((beg+end)//2+1, end,
                            arr, n)

    if(compared1[1] > compared2[1]):
        k = compared1[0]+1

    # Store length of compared1[]
    # in the first index
        compared1[0] = k

    # Store the maximum element
        compared1[k] = compared2[1]

        # Return compared1 which
        # contains the maximum element
        return compared1

    else:
        k = compared2[0]+1

    # Store length of compared2[]
    # in the first index
        compared2[0] = k

    # Store the maximum element
        compared2[k] = compared1[1]

        # Return compared2[] which
        # contains the maximum element
        return compared2

# Function to print the second largest
# element in the array arr[]
def findSecondLargest(end, arr):

    # Find the largest element in arr[]
    compared1 = findLargest(0, end-1, arr, end)

    # Find the second largest element
    # in arr[]
    compared2 = findLargest(2, compared1[0]+2,
                            compared1,
                            compared1[0])

    # Print the second largest element
    print(compared2[1])

# Driver Code
N = 10

arr = [20, 1990, 12, 1110, 1, 59, 12, 15, 120, 1110]

findSecondLargest(N, arr)
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the largest
// element in the array arr[]
static int[] findLargest(int beg, int end,
                         int []arr, int n)
{

    // Base Condition
    if (beg == end)
    {

        // Initialize an empty list
        int []compared = new int[n];
        compared[0] = 1;
        compared[1] = arr[beg];
        return compared;
    }

    // Divide the array into two equal
    // length subarrays and recursively
    // find the largest among the two
    int []compared1 = findLargest(beg,
                                 (beg + end) /
                                  2, arr, n);

    int []compared2 = findLargest((beg + end) /
                                     2 + 1,
                                  end, arr, n);

    if (compared1[1] > compared2[1])
    {
        int k = compared1[0] + 1;

        // Store length of compared1[]
        // in the first index
        compared1[0] = k;

        // Store the maximum element
        compared1[k] = compared2[1];

        // Return compared1 which
        // contains the maximum element
        return compared1;
    }
    else
    {
        int k = compared2[0] + 1;

        // Store length of compared2[]
        // in the first index
        compared2[0] = k;

        // Store the maximum element
        compared2[k] = compared1[1];

        // Return compared2[] which
        // contains the maximum element
        return compared2;
    }
}

// Function to print the second largest
// element in the array arr[]
static void findSecondLargest(int end,
                              int []arr)
{

    // Find the largest element in arr[]
    int []compared1 = findLargest(0, end - 1,
                                  arr, end);

    // Find the second largest element
    // in arr[]
    int []compared2 = findLargest(2, compared1[0] + 2,
                                     compared1,
                                     compared1[0]);

    // Print the second largest element
   Console.WriteLine(compared2[1]);
}

// Driver code
static public void Main ()
{
    int N = 10;
    int []arr = { 20, 1990, 12, 1110, 1,
                  59, 12, 15, 120, 1110 };

    findSecondLargest(N, arr);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the largest
// element in the array arr[]
function findLargest(beg,end,arr,n)
{
    // Base Condition
if (beg == end)
{
    // Initialize an empty list
    let compared = new Array(n);
    for(let i=0;i<n;i++)
        compared[i]=0;
    compared[0] = 1;
    compared[1] = arr[beg];
    return compared;
}

// Divide the array into two equal
// length subarrays and recursively
// find the largest among the two
let compared1 = findLargest(beg,
                            Math.floor((beg + end) /
                                2), arr, n);

let compared2 = findLargest(Math.floor((beg + end) /
                                2 )+ 1,
                                end, arr, n);

if (compared1[1] > compared2[1])
{
    let k = compared1[0] + 1;

    // Store length of compared1[]
    // in the first index
    compared1[0] = k;

    // Store the maximum element
    compared1[k] = compared2[1];

    // Return compared1 which
    // contains the maximum element
    return compared1;
}
else
{
    let k = compared2[0] + 1;

    // Store length of compared2[]
    // in the first index
    compared2[0] = k;

    // Store the maximum element
    compared2[k] = compared1[1];

    // Return compared2[] which
    // contains the maximum element
    return compared2;
}
}

// Function to print the second largest
// element in the array arr[]
function findSecondLargest(end,arr)
{
    // Find the largest element in arr[]
    let compared1 = findLargest(0, end - 1,
                                arr, end);

    // Find the second largest element
    // in arr[]
    let compared2 = findLargest(2, compared1[0] + 2,
                                compared1,
                                compared1[0]);

    // Print the second largest element
    document.write(compared2[1]);
}

// Driver code
let N = 10;
let arr=[20, 1990, 12, 1110, 1,
              59, 12, 15, 120, 1110];
findSecondLargest(N, arr);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1110
```

***时间复杂度:** O(N)*
***辅助空间:** O(logN)*