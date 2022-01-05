# 通过用最大值重复替换相邻的不等对，将数组简化为单个元素

> 原文:[https://www . geeksforgeeks . org/通过用它们的最大值重复替换相邻的不等对来将数组减少为单个元素/](https://www.geeksforgeeks.org/reduce-array-to-a-single-element-by-repeatedly-replacing-adjacent-unequal-pairs-with-their-maximum/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过重复替换任意一对连续的不相等元素，将给定数组简化为单个元素，比如说 **arr[i]** 和 **arr[i+1]** 替换为 **max(arr[i]，arr[i + 1]) + 1** 。如果可能，打印可以开始操作的元素的索引。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = {5，3，4，4，5}
> **输出:** 1
> **解释:**
> 第一步:将 arr[1]和 arr[2]替换为 max(arr[1]，arr[2])+1 = max(5，3) + 1 = 6。因此，arr[] = {6，4，4，5}。
> 第二步:将 arr[1]和 arr[2]替换为 max(arr[1]，arr[2]) + 1 = max(6，4) + 1 = 7。因此，arr[] = {7，4，5}。
> 第三步:将 arr[1]和 arr[2]替换为 max(arr[1]，arr[2])+1 = max(7，4) + 1 = 8。因此，arr[] = {8，5}。
> 第四步:将 arr[1]和 arr[2]替换为 max(arr[1]，arr[2]) + 1 = max(8，5)+1 = 9。因此，arr[] = {9}。
> 
> **输入:** arr[] ={1，1}
> **输出:** -1

**简单方法:**最简单的方法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素**arr【I】**，根据给定的约束开始连续执行给定的操作。如果对于任何元素，数组变成单个元素，打印索引 **i** 否则，打印 **-1** 。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**想法是使用[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)。请注意，如果所有元素都相同，答案将始终是 **-1** 。否则，[可以选择具有最大元素的索引](https://www.geeksforgeeks.org/python-maximum-minimum-elements-position-list/)来开始执行操作。按照以下步骤解决问题:

*   创建与给定数组相同的另一个数组 **B[]** ，并创建一个变量**保存**用**初始化-1** 来存储答案。
*   [排序阵](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)T2【B】。
*   [使用变量 **i** 在**【N–1】**到**0】**的范围内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果发现两个连续的不等元素，即 **B[i]** 不等于**B[I–1]**，则更新**将**保存为**保存= i** 。
*   t 遍历数组后:
    *   如果**保存**是 **-1** ，打印 **-1** 返回。
    *   否则如果**保存**等于**arr【0】****保存**不等于**arr【1】**，则更新保存为 **1** 。
    *   否则如果**保存**等于**arr【N–1】****保存**不等于**arr【N–2】**，则更新保存为 **N** 。
    *   否则，在范围**【1，N–1】**内循环，检查 save 是否等于**arr【I】**，使得**arr【I】**不等于**arr【I–1】**和**arr【I+1】**，然后将 **save** 更新为 **save = i+1** 。
*   完成上述步骤后，打印变量**中存储的索引并保存**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the index from
// where the operation can be started
void printIndex(int arr[], int N)
{
    // Initialize B[]
    int B[N];

    // Initialize save
    int save = -1;

    // Make B[] equals to arr[]
    for (int i = 0; i < N; i++) {
        B[i] = arr[i];
    }

    // Sort the array B[]
    sort(B, B + N);

    // Traverse from N-1 to 1
    for (int i = N - 1; i >= 1; i--) {

        // If B[i] & B[i-1] are unequal
        if (B[i] != B[i - 1]) {
            save = B[i];
            break;
        }
    }

    // If all elements are same
    if (save == -1) {
        cout << -1 << endl;
        return;
    }

    // If arr[1] is maximum element
    if (save == arr[0]
        && save != arr[1]) {
        cout << 1;
    }

    // If arr[N-1] is maximum element
    else if (save == arr[N - 1]
             && save != arr[N - 2]) {
        cout << N;
    }

    // Find the maximum element
    for (int i = 1; i < N - 1; i++) {

        if (save == arr[i]
            && (save != arr[i - 1]
                || save != arr[i + 1])) {
            cout << i + 1;
            break;
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 5, 3, 4, 4, 5 };

    // Length of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printIndex(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to print the index
// from where the operation can
// be started
static void printIndex(int arr[],
                       int N)
{
  // Initialize B[]
  int []B = new int[N];

  // Initialize save
  int save = -1;

  // Make B[] equals to arr[]
  for (int i = 0; i < N; i++)
  {
    B[i] = arr[i];
  }

  // Sort the array B[]
  Arrays.sort(B);

  // Traverse from N-1 to 1
  for (int i = N - 1; i >= 1; i--)
  {
    // If B[i] & B[i-1] are
    // unequal
    if (B[i] != B[i - 1])
    {
      save = B[i];
      break;
    }
  }

  // If all elements are same
  if (save == -1)
  {
    System.out.print(-1 + "\n");
    return;
  }

  // If arr[1] is maximum
  // element
  if (save == arr[0] &&
      save != arr[1])
  {
    System.out.print(1);
  }

  // If arr[N-1] is maximum
  // element
  else if (save == arr[N - 1] &&
           save != arr[N - 2])
  {
    System.out.print(N);
  }

  // Find the maximum element
  for (int i = 1; i < N - 1; i++)
  {
    if (save == arr[i] &&
       (save != arr[i - 1] ||
        save != arr[i + 1]))
    {
      System.out.print(i + 1);
      break;
    }
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {5, 3, 4, 4, 5};

  // Length of array
  int N = arr.length;

  // Function Call
  printIndex(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to print the index
# from where the operation can
# be started
def printIndex(arr, N):

    # Initialize B
    B = [0] * (N)

    # Initialize save
    save = -1

    # Make B equals to arr
    for i in range(N):
        B[i] = arr[i]

    # Sort the array B
    B = sorted(B)

    # Traverse from N-1 to 1
    for i in range(N - 1, 1, -1):

        # If B[i] & B[i-1] are
        # unequal
        if (B[i] != B[i - 1]):
            save = B[i]
            break

    # If all elements are same
    if (save == -1):
        print(-1 + "")
        return

    # If arr[1] is maximum
    # element
    if (save == arr[0] and
        save != arr[1]):
        print(1)

    # If arr[N-1] is maximum
    # element
    elif (save == arr[N - 1] and
          save != arr[N - 2]):
        print(N)

    # Find the maximum element
    for i in range(1, N - 1):
        if (save == arr[i] and
           (save != arr[i - 1] or
            save != arr[i + 1])):
            print(i + 1)
            break

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 5, 3, 4, 4, 5 ]

    # Length of array
    N = len(arr)

    # Function Call
    printIndex(arr, N)

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to print the index
// from where the operation can
// be started
static void printIndex(int []arr,
                       int N)
{

  // Initialize []B
  int []B = new int[N];

  // Initialize save
  int save = -1;

  // Make []B equals to []arr
  for(int i = 0; i < N; i++)
  {
    B[i] = arr[i];
  }

  // Sort the array []B
  Array.Sort(B);

  // Traverse from N-1 to 1
  for(int i = N - 1; i >= 1; i--)
  {

    // If B[i] & B[i-1] are
    // unequal
    if (B[i] != B[i - 1])
    {
      save = B[i];
      break;
    }
  }

  // If all elements are same
  if (save == -1)
  {
    Console.Write(-1 + "\n");
    return;
  }

  // If arr[1] is maximum
  // element
  if (save == arr[0] &&
      save != arr[1])
  {
    Console.Write(1);
  }

  // If arr[N-1] is maximum
  // element
  else if (save == arr[N - 1] &&
           save != arr[N - 2])
  {
    Console.Write(N);
  }

  // Find the maximum element
  for(int i = 1; i < N - 1; i++)
  {
    if (save == arr[i] &&
       (save != arr[i - 1] ||
        save != arr[i + 1]))
    {
      Console.Write(i + 1);
      break;
    }
  }
}

// Driver Code
public static void Main(String[] args)
{

  // Given array []arr
  int []arr = { 5, 3, 4, 4, 5 };

  // Length of array
  int N = arr.Length;

  // Function Call
  printIndex(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the index
// from where the operation can
// be started
function printIndex(arr, N)
{

    // Initialize B[]
    let B = [];

    // Initialize save
    let save = -1;

    // Make B[] equals to arr[]
    for(let i = 0; i < N; i++)
    {
        B[i] = arr[i];
    }

    // Sort the array B[]
    B.sort();

    // Traverse from N-1 to 1
    for(let i = N - 1; i >= 1; i--)
    {

        // If B[i] & B[i-1] are
        // unequal
        if (B[i] != B[i - 1])
        {
            save = B[i];
            break;
        }
    }

    // If all elements are same
    if (save == -1)
    {
        document.write(-1 + "<br/>");
        return;
    }

    // If arr[1] is maximum
    // element
    if (save == arr[0] &&
        save != arr[1])
    {
        document.write(1);
    }

    // If arr[N-1] is maximum
    // element
    else if (save == arr[N - 1] &&
            save != arr[N - 2])
    {
        document.write(N);
    }

    // Find the maximum element
    for (let i = 1; i < N - 1; i++)
    {
        if (save == arr[i] &&
           (save != arr[i - 1] ||
            save != arr[i + 1]))
        {
            document.write(i + 1);
            break;
        }
    }
}

// Driver Code

// Given array arr[]
let arr = [5, 3, 4, 4, 5];

// Length of array
let N = arr.length;

// Function Call
printIndex(arr, N);

// This code is contribute by target_2

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)