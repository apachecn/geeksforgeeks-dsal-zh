# 所有其他给定对位于其最小值和最大值之间的对

> 原文:[https://www . geesforgeks . org/pair-having-all-other-given-pair-介于其最小值和最大值之间/](https://www.geeksforgeeks.org/pair-having-all-other-given-pairs-lying-between-its-minimum-and-maximum/)

给定一个 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**由 **N** 对整数组成，任务是找到覆盖给定数组所有其他对的整数对。如果找不到这样的一对，那么打印 **-1** 。

> 如果条件 **(a ≤ c ≤ d ≤ b)** 成立，一对{ **a，b}** 将覆盖另一对 **{c，d}** 。

**示例:**

> **输入:** arr[][2] = {{2，2}、{3，3}、{3，5}、{4，5}、{1，1}、{1，5}}
> **输出:** 6
> **解释:**
> 存在一对(1，5)覆盖所有其他对，因为所有其他对都位于对{1，5}中。
> 因此，对{1，5}的位置为 6。所以，输出是 6。
> 
> **输入:** arr[][] = {{1，20}，{2，22}，{3，18}}
> **输出:** -1
> **解释:**
> 不存在覆盖所有剩余对的这样的对。
> 因此，输出为-1

**天真方法:**最简单的方法是将每一对与所有其他对进行比较，并检查任何一对是否覆盖所有对。以下是步骤:

1.  初始化变量**计数= 0** ，该变量存储当前对之间的对的数量。
2.  [遍历对的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每对，检查**计数**是否等于对的总数。
3.  如果发现是真的，则意味着该对可以覆盖所有其他对。把这一对打印出来。
4.  否则，设置**计数= 0** 并对下一对重复上述步骤。
5.  如果不存在这样的配对，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the position of
// the pair that covers every pair
// in the array arr[][]
void position(int arr[][2], int N)
{
    // Stores the index of the
    // resultant pair
    int pos = -1;

    // To count the occurences
    int count;

    // Iterate to check every pair
    for (int i = 0; i < N; i++) {

        // Set count to 0
        count = 0;

        for (int j = 0; j < N; j++) {

            // Condition to checked for
            // overlapping of pairs
            if (arr[i][0] <= arr[j][0]
                && arr[i][1] >= arr[j][1]) {
                count++;
            }
        }

        // If that pair can cover all other
        // pairs then store its position
        if (count == N) {
            pos = i;
        }
    }

    // If position not found
    if (pos == -1) {

        cout << pos;
    }

    // Otherwise
    else {

        cout << pos + 1;
    }
}

// Driver Code
int main()
{
    // Given array of pairs
    int arr[][2] = {{ 3, 3 }, { 1, 3 },
                    { 2, 2 }, { 2, 3 },
                    { 1, 2 }};

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    position(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find the position of
// the pair that covers every pair
// in the array arr[][]
static void position(int arr[][],
                     int N)
{
  // Stores the index of the
  // resultant pair
  int pos = -1;

  // To count the occurences
  int count;

  // Iterate to check every pair
  for (int i = 0; i < N; i++)
  {
    // Set count to 0
    count = 0;

    for (int j = 0; j < N; j++)
    {
      // Condition to checked for
      // overlapping of pairs
      if (arr[i][0] <= arr[j][0] &&
          arr[i][1] >= arr[j][1])
      {
        count++;
      }
    }

    // If that pair can cover all other
    // pairs then store its position
    if (count == N)
    {
      pos = i;
    }
  }

  // If position not found
  if (pos == -1)
  {
    System.out.print(pos);
  }

  // Otherwise
  else
  {
    System.out.print(pos + 1);
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array of pairs
  int arr[][] = {{3, 3}, {1, 3},
                 {2, 2}, {2, 3},
                 {1, 2}};

  int N = arr.length;

  // Function Call
  position(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the position of
# the pair that covers every pair
# in the array arr
def position(arr, N):

    # Stores the index of the
    # resultant pair
    pos = -1;

    # To count the occurences
    count = 0;

    # Iterate to check every pair
    for i in range(N):

        # Set count to 0
        count = 0;

        for j in range(N):
            # Condition to checked for
            # overlapping of pairs
            if (arr[i][0] <= arr[j][0] and
                arr[i][1] >= arr[j][1]):
                count += 1;

        # If that pair can cover
        # all other pairs then
        # store its position
        if (count == N):
            pos = i;

    # If position not found
    if (pos == -1):
        print(pos);

    # Otherwise
    else:
        print(pos + 1);

# Driver Code
if __name__ == '__main__':

    # Given array of pairs
    arr = [[3, 3], [1, 3],
           [2, 2], [2, 3],
           [1, 2]];

    N = len(arr);

    # Function Call
    position(arr, N);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the position of
// the pair that covers every pair
// in the array arr[][]
static void position(int[,] arr,
                     int N)
{
  // Stores the index of the
  // resultant pair
  int pos = -1;

  // To count the occurences
  int count;

  // Iterate to check every pair
  for(int i = 0; i < N; i++)
  {
    // Set count to 0
    count = 0;

    for(int j = 0; j < N; j++)
    {
      // Condition to checked for
      // overlapping of pairs
      if (arr[i, 0] <= arr[j, 0] &&
          arr[i, 1] >= arr[j, 1])
      {
        count++;
      }
    }

    // If that pair can cover
    // all other pairs then
    // store its position
    if (count == N)
    {
      pos = i;
    }
  }

  // If position not found
  if (pos == -1)
  {
    Console.Write(pos);
  }

  // Otherwise
  else
  {
    Console.Write(pos + 1);
  }
}

// Driver Code
public static void Main()
{ 
  // Give array of pairs
  int[,] arr = {{3, 3}, {1, 3},
                {2, 2}, {2, 3},
                {1, 2}};

  int N = arr.GetLength(0);

  // Function Call
  position(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to find the position of
// the pair that covers every pair
// in the array arr[][]
function position(arr, N)
{
  // Stores the index of the
  // resultant pair
  let pos = -1;

  // To count the occurences
  let count;

  // Iterate to check every pair
  for (let i = 0; i < N; i++)
  {
    // Set count to 0
    count = 0;

    for (let j = 0; j < N; j++)
    {
      // Condition to checked for
      // overlapping of pairs
      if (arr[i][0] <= arr[j][0] &&
          arr[i][1] >= arr[j][1])
      {
        count++;
      }
    }

    // If that pair can cover all other
    // pairs then store its position
    if (count == N)
    {
      pos = i;
    }
  }

  // If position not found
  if (pos == -1)
  {
    document.write(pos);
  }

  // Otherwise
  else
  {
    document.write(pos + 1);
  }
}

// Driver Code

    // Given array of pairs
  let arr = [[3, 3], [1, 3],
                 [2, 2], [2, 3],
                 [1, 2]];

  let N = arr.length;

  // Function Call
  position(arr, N);

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是观察到答案总是唯一的，因为总是有一个包含最小值和最大值的唯一对。以下是步骤:

1.  [迭代给定的配对数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，从 **arr[][]** 中的所有配对中找到最小的第一对和最大的第二对。
2.  在上述步骤中找到最大值和最小值后，必须存在任何一对 **arr[i][0]** =最小值和 **arr[i][1]** =最大值。
3.  遍历每一对数组，检查是否有一对的 **arr[i][0]** 等于最小值， **arr[i][1]** 等于最大值。
4.  如果上述步骤中存在任何位置，则打印该位置。
5.  否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the position of
// the pair that covers every pair
// in the array arr[][]
void position(int arr[][2], int N)
{
    // Position to store the index
    int pos = -1;

    // Stores the maximum second value
    int right = INT_MIN;

    // Stores the minimum first value
    int left = INT_MAX;

    // Iterate over the array of pairs
    for (int i = 0; i < N; i++) {

        // Update right maximum
        if (arr[i][1] > right) {
            right = arr[i][1];
        }

        // Update left minimum
        if (arr[i][0] < left) {

            left = arr[i][0];
        }
    }

    // Iterate over the array of pairs
    for (int i = 0; i < N; i++) {

        // If any pair exists with value
        // {left, right} then store it
        if (arr[i][0] == left
            && arr[i][1] == right) {

            pos = i + 1;
        }
    }

    // Print the answer
    cout << pos << endl;
}

// Driver Code
int main()
{
    // Given array of pairs
    int arr[][2] = {{ 3, 3 }, { 1, 3 },
                    { 2, 2 }, { 2, 3 },
                    { 1, 2 }};

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    position(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to find the position
// of the pair that covers
// every pair in the array arr[][]
static void position(int arr[][],
                     int N)
{
  // Position to store
  // the index
  int pos = -1;

  // Stores the maximum
  // second value
  int right = Integer.MIN_VALUE;

  // Stores the minimum
  // first value
  int left = Integer.MAX_VALUE;

  // Iterate over the array
  // of pairs
  for (int i = 0; i < N; i++)
  {
    // Update right maximum
    if (arr[i][1] > right)
    {
      right = arr[i][1];
    }

    // Update left minimum
    if (arr[i][0] < left)
    {
      left = arr[i][0];
    }
  }

  // Iterate over the array
  // of pairs
  for (int i = 0; i < N; i++)
  {
    // If any pair exists
    // with value {left,
    // right} then store it
    if (arr[i][0] == left &&
        arr[i][1] == right)
    {
      pos = i + 1;
    }
  }

  // Print the answer
  System.out.print(pos + "\n");
}

// Driver Code
public static void main(String[] args)
{
  // Given array of pairs
  int arr[][] = {{3, 3}, {1, 3},
                 {2, 2}, {2, 3},
                 {1, 2}};

  int N = arr.length;

  // Function Call
  position(arr, N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the position of
# the pair that covers every pair
# in the array arr[][]
def position(arr, N):

    # Position to store the index
    pos = -1

    # Stores the minimum second value
    right = -sys.maxsize - 1

    # Stores the maximum first value
    left = sys.maxsize

    # Iterate over the array of pairs
    for i in range(N):

        # Update right maximum
        if (arr[i][1] > right):
            right = arr[i][1]

        # Update left minimum
        if (arr[i][0] < left):
            left = arr[i][0]

    # Iterate over the array of pairs
    for i in range(N):

        # If any pair exists with value
        # {left, right then store it
        if (arr[i][0] == left and
            arr[i][1] == right):
            pos = i + 1

    # Print the answer
    print(pos)

# Driver Code
if __name__ == '__main__':

    # Given array of pairs
    arr = [ [ 3, 3 ], [ 1, 3 ],
            [ 2, 2 ], [ 2, 3 ],
            [ 1, 2 ] ]

    N = len(arr)

    # Function call
    position(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the position
// of the pair that covers
// every pair in the array [,]arr
static void position(int [,]arr,
                     int N)
{
  // Position to store
  // the index
  int pos = -1;

  // Stores the maximum
  // second value
  int right = int.MinValue;

  // Stores the minimum
  // first value
  int left = int.MaxValue;

  // Iterate over the array
  // of pairs
  for (int i = 0; i < N; i++)
  {
    // Update right maximum
    if (arr[i, 1] > right)
    {
      right = arr[i, 1];
    }

    // Update left minimum
    if (arr[i, 0] < left)
    {
      left = arr[i, 0];
    }
  }

  // Iterate over the array
  // of pairs
  for (int i = 0; i < N; i++)
  {
    // If any pair exists
    // with value {left,
    // right} then store it
    if (arr[i, 0] == left &&
        arr[i, 1] == right)
    {
      pos = i + 1;
    }
  }

  // Print the answer
  Console.Write(pos + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Given array of pairs
  int [,]arr = {{3, 3}, {1, 3},
                {2, 2}, {2, 3},
                {1, 2}};

  int N = arr.GetLength(0);

  // Function Call
  position(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)