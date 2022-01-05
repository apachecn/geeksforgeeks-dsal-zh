# 等级等于或小于给定截止等级的玩家数量

> 原文:[https://www . geesforgeks . org/排名等于或低于给定截止排名的玩家数量/](https://www.geeksforgeeks.org/number-of-players-whose-rank-is-equal-to-or-less-than-a-given-cutoff-rank/)

给定一个由 **N** 个整数和一个表示截止秩的整数 **R** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算秩为**的数组元素的数量，最多 R** 个，使得相等的数组元素被排序相同，并且不同的数组元素根据它们在数组**arr【】**中的位置进行排序。

**示例:**

> **输入:** arr[] = {100，50，50，25}，R = 3
> **输出:** 3
> **说明:**
> 玩家排名如下:{1，2，2，4}。排名最多的玩家是{1，2，2}。因此，总数为 3。
> 
> **输入:** arr[] = {2，2，3，4，5}，R = 4
> T3】输出: 5

**方法:**利用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)的概念可以解决给定的问题。请按照以下步骤解决此问题:

*   [按降序排列给定数组**arr[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   初始化两个变量，说**将**排序为 **1** 存储数组元素的排序，说**将**计数为 **0** 存储需要的结果。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **arr[]** ，并执行以下步骤:
    *   如果 **arr[i]** 等于前一个元素，则将与前一个等级相同的等级分配给当前元素。
    *   否则，将**(计数+1)**等级的值赋给当前元素。
    *   如果**等级**大于**等级**，则破。否则，将**计数**增加 **1** 。
*   完成以上步骤后，打印**的数值，计**作为答案。

下面是上述方法的实现:

## C++

```
// C++  program for above approach
#include <algorithm>
#include <iostream>
using namespace std;

// Function to find the count of array
// elements having rank at most R
int countElements(int R, int N, int arr[])
{

  // Sort the array arr[] in the
  // decreasing order
  sort(arr, arr + N, greater<int>());

  // Stores the rank and required
  // count of array elements
  int rank = 1, count = 0;

  // store the previou element
  int prevScore = arr[0], score;

  // Traverse the array
  for (int i = 0; i < N; i++) {
    score = arr[i];

    // If score is less than the
    // prevScore
    if (score < prevScore) {
      rank = count + 1;
    }

    // If the rank is greater than R
    if (rank > R) {
      break;
    }

    // Increment count by 1
    count++;

    // update prevscore
    prevScore = score;
  }

  // return count
  return count;
}

// Driver code
int main()
{
  int arr[] = { 100, 50, 50, 25 };
  int R = 2;
  int N = sizeof(arr) / sizeof(arr[0]);
  cout << countElements(R, N, arr);
  return 0;
}

// This code is contributed by Parth Manchanda
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{
  static void reverse(int a[])
  {
    int n = a.length;
    int[] b = new int[n];
    int j = n;
    for (int i = 0; i < n; i++) {
      b[j - 1] = a[i];
      j = j - 1;
    }
  }

  // Function to find the count of array
  // elements having rank at most R
  static int countElements(int R, int N, int[] arr)
  {

    // Sort the array arr[] in the
    // decreasing order
    Arrays.sort(arr);
    reverse(arr);

    // Stores the rank and required
    // count of array elements
    int rank = 1;
    int count = -1;

    // Stores the previous element
    int prevScore = arr[0];

    // Traverse the array
    for(int score : arr)
    {

      // If score is less than the
      // prevScore
      if (score < prevScore)
        rank = count + 1;

      // If the rank is greater than R
      if (rank > R)
        break;

      // Increment count by 1
      count = count + 1;

      // Update prevScore
      prevScore = score;
    }

    // Return the result
    return count;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 100, 50, 50, 25 };
    int R = 2;
    int N = arr.length;

    // Function Call
    System.out.println(countElements(R, N, arr));
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the count of array
# elements having rank at most R
def countElements(R, N, arr):

    # Sort the array arr[] in the
    # decreasing order
    arr.sort(reverse = True)

    # Stores the rank and required
    # count of array elements
    rank = 1
    count = 0

    # Stores the previous element
    prevScore = arr[0]

    # Traverse the array
    for score in arr:

        # If score is less than the
        # prevScore
        if score < prevScore:
            rank = count + 1

        # If the rank is greater than R
        if rank > R:
            break

        # Increment count by 1
        count += 1

        # Update prevScore
        prevScore = score

    # Return the result
    return count

# Driver Code
arr = [100, 50, 50, 25]
R = 2
N = len(arr)

# Function Call
print(countElements(R, N, arr))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the count of array
// elements having rank at most R
static int countElements(int R, int N, int[] arr)
{

    // Sort the array arr[] in the
    // decreasing order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Stores the rank and required
    // count of array elements
    int rank = 1;
    int count = 0;

    // Stores the previous element
    int prevScore = arr[0];

    // Traverse the array
    foreach(int score in arr)
    {

        // If score is less than the
        // prevScore
        if (score < prevScore)
            rank = count + 1;

        // If the rank is greater than R
        if (rank > R)
            break;

        // Increment count by 1
        count = count + 1;

        // Update prevScore
        prevScore = score;
    }

    // Return the result
    return count;
}

// Driver code
static public void Main()
{
    int[] arr = { 100, 50, 50, 25 };
    int R = 2;
    int N = arr.Length;

    // Function Call
    Console.WriteLine(countElements(R, N, arr));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the count of array
// elements having rank at most R
function countElements(R, N, arr)
{

    // Sort the array arr[] in the
    // decreasing order
    arr.sort(function(a, b){ return b - a; });

    // Stores the rank and required
    // count of array elements
    let rank = 1;
    let count = 0;

    // Stores the previous element
    let prevScore = arr[0];

    // Traverse the array
    for(let score of arr)
    {

        // If score is less than the
        // prevScore
        if (score < prevScore)
            rank = count + 1;

        // If the rank is greater than R
        if (rank > R)
            break;

        // Increment count by 1
        count = count + 1;

        // Update prevScore
        prevScore = score;
    }

    // Return the result
    return count;
}

// Driver Code
let arr = [ 100, 50, 50, 25 ];
let R = 2;
let N = arr.length;

// Function Call
document.write(countElements(R, N, arr));

// This code is contributed by lokeshpotta20

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*