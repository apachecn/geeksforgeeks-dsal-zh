# 如果 N≤2 | X–Y |

，通过交换 X 和 Y 位置的元素，对前 N 个自然数的排列进行排序

> 原文:[https://www . geeksforgeeks . org/sort-a-通过交换位置元素对第一个 n 个自然数进行排列-x-和-y-if-n-2x-y/](https://www.geeksforgeeks.org/sort-a-permutation-of-first-n-natural-numbers-by-swapping-elements-at-positions-x-and-y-if-n-2x-y/)

给定一个由第一个 **N** 自然数( **N** 为偶数)组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找到一个交换序列，该序列可以[通过交换位置 **X** 和 **Y** 的元素对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，如果
**N≤2 | X–Y |**
***注意:**考虑基于 1 的索引*

**示例:**

> **输入:** N = 2，arr[] = { 2，1 }
> **输出:** 1 2
> **解释:**交换位置 1 和 2 的元素对数组进行排序。
> 
> **输入:** N = 4，arr[] = { 3，4，1，2 }
> **输出:**
> 1 3
> 2 4
> **解释:**
> 在位置 1 3 交换元素。数组 arr[]修改为{1，4，3，2}。
> 交换位置 2 和 4 的元素。数组 arr[]修改为{1，2，3，4}。

**方法:**解决这个问题的思路是使用一个数组**位置[]** 来维护数组 arr[]中元素的位置，**T5】执行 arr[x] an arr[y]以及**位置【arr[x]】**和**位置【arr[y]】的互换。**按照以下步骤解决问题:**

*   初始化一个数组 **newArr[]** 直接按位置引用元素。
*   初始化一个向量**位置**存储原始数组元素的位置，向量**回答**存储执行的交换。
*   从 i=1 到 N 进行遍历，并检查以下条件:
    *   **如果位置[i] = i :** 继续下一个整数，因为这个整数已经在它的右边位置。
    *   **如果|位置[I]–I |>= N/2**:呼叫**执行 _ 交换(I，位置[i])**
    *   **否则:**保持变量**初始 _ 位置**保持整数当前位置即**位置【I】**
        *   **如果|位置[i]-1| > = N/2 :** 呼叫**执行 _ 交换(位置[i]，1)**
            *   **如果|i-1| > = N/2 :** 调用**执行 _swap(i，1)** 和**执行 _swap(初始 _ 位置，1)**
            *   **否则:**调用**执行 _swap(1，N)** 、**执行 _swap(N，i)** 和**执行 _swap(1，初始 _ 位置)**。
        *   否则:调用**执行 _swap(位置[i]，N)** 、**执行 _swap(N，I)**；

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

// Function to swap values in arr and position
void perform_swap(vector<int>& arr, vector<int>& position,
                  vector<pair<int, int> >& answer, int x,
                  int y)
{

    // Swap position[arr[x]] and position[arr[y]]
    swap(position[arr[x]], position[arr[y]]);

    // Swap arr[x] and arr[y]
    swap(arr[x], arr[y]);

    // Push x and y to the answer vector
    answer.push_back({ x, y });
}

// Function to find the sequence of swaps
// that can sort the array
void sortBySwap(int N, int arr[])
{

    // Shifted vector of Array arr
    vector<int> newArr(N + 1, 0);

    for (int i = 0; i < N; i++)
        newArr[i + 1] = arr[i];

    // Keep an vector to maintain positions
    vector<int> position(N + 1, 0);

    // Vector to maintain the swaps performed
    vector<pair<int, int> > answer;

    // Assign position of elements in position array
    for (int i = 1; i <= N; i++)
        position[newArr[i]] = i;

    // Traverse from 1 to N
    for (int i = 1; i <= N; i++) {

        // If element is already at it's right position
        if (i == position[i])
            continue;

        // If current and right place can be directly
        // swapped
        if (abs(i - position[i]) >= N / 2) {
            perform_swap(newArr, position, answer, i,
                         position[i]);
        }
        else {

            // Initial position of integer i
            int initial_position = position[i];

            // If |position[i]-1| >= N/2 :
            // Call perform_swap(position[i], 1)
            if (abs(position[i] - 1) >= N / 2) {
                perform_swap(newArr, position, answer,
                             position[i], 1);

                // If |i-1| >= N/2 : Call perform_swap(i, 1)
                // and perform_swap(initial_position, 1)
                if (abs(i - 1) >= N / 2) {
                    perform_swap(newArr, position, answer,
                                 i, 1);
                    perform_swap(newArr, position, answer,
                                 initial_position, 1);
                }

                // Otherwise: Call perform_swap(1, N),
                // perform_swap(N, i) and
                // perform_swap(1, initial_position).
                else {
                    perform_swap(newArr, position, answer,
                                 1, N);
                    perform_swap(newArr, position, answer,
                                 N, i);
                    perform_swap(newArr, position, answer,
                                 1, initial_position);
                }
            }

            // Otherwise: Call perform_swap(position[i], N)
            // and perform_swap(N, i);
            else {
                perform_swap(newArr, position, answer,
                             position[i], N);
                perform_swap(newArr, position, answer, N,
                             i);
            }
        }
    }

    // Print the sequences which sorts
    // the given array
    for (int i = 0; i < (int)answer.size(); i++)
        printf("%d %d\n", answer[i].first,
               answer[i].second);
}

// Driver Code
int main()
{
    // Input Array
    int arr[] = { 3, 4, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortBySwap(N, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class Pair
{
    int first, second;

    Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

class GFG{

static void swap(int[] a, int i, int j)
{
    int temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}

// Function to swap values in arr and position
static void perform_swap(int[] arr, int[] position,
                         List<Pair> answer, int x,
                         int y)
{

    // Swap position[arr[x]] and position[arr[y]]
    swap(position, arr[x], arr[y]);

    // Swap arr[x] and arr[y]
    swap(arr, x, y);

    // Push x and y to the answer vector
    answer.add(new Pair(x, y));
}

// Function to find the sequence of swaps
// that can sort the array
static void sortBySwap(int N, int arr[])
{

    // Shifted vector of Array arr
    int[] newArr = new int[N + 1];

    for(int i = 0; i < N; i++)
        newArr[i + 1] = arr[i];

    // Keep an vector to maintain positions
    int[] position = new int[N + 1];

    // Vector to maintain the swaps performed
    @SuppressWarnings("unchecked")
    List<Pair> answer = new ArrayList();

    // Assign position of elements in position array
    for(int i = 1; i <= N; i++)
        position[newArr[i]] = i;

    // Traverse from 1 to N
    for(int i = 1; i <= N; i++)
    {

        // If element is already at it's
        // right position
        if (i == position[i])
            continue;

        // If current and right place can
        // be directly swapped
        if (Math.abs(i - position[i]) >= N / 2)
        {
            perform_swap(newArr, position, answer, i,
                         position[i]);
        }
        else
        {

            // Initial position of integer i
            int initial_position = position[i];

            // If |position[i]-1| >= N/2 :
            // Call perform_swap(position[i], 1)
            if (Math.abs(position[i] - 1) >= N / 2)
            {
                perform_swap(newArr, position, answer,
                             position[i], 1);

                // If |i-1| >= N/2 : Call
                // perform_swap(i, 1) and
                // perform_swap(initial_position, 1)
                if (Math.abs(i - 1) >= N / 2)
                {
                    perform_swap(newArr, position,
                                 answer, i, 1);
                    perform_swap(newArr, position,
                                 answer,
                                 initial_position, 1);
                }

                // Otherwise: Call perform_swap(1, N),
                // perform_swap(N, i) and
                // perform_swap(1, initial_position).
                else
                {
                    perform_swap(newArr, position,
                                 answer, 1, N);
                    perform_swap(newArr, position,
                                 answer, N, i);
                    perform_swap(newArr, position,
                                 answer, 1,
                                 initial_position);
                }
            }

            // Otherwise: Call perform_swap(position[i],
            // N) and perform_swap(N, i);
            else
            {
                perform_swap(newArr, position, answer,
                             position[i], N);
                perform_swap(newArr, position, answer,
                             N, i);
            }
        }
    }

    // Print the sequences which sorts
    // the given array
    for(int i = 0; i < answer.size(); i++)
        System.out.println(answer.get(i).first + " " +
                           answer.get(i).second);
}

// Driver code
public static void main(String[] args)
{

    // Input Array
    int arr[] = { 3, 4, 1, 2 };
    int N = arr.length;

    // Function Call
    sortBySwap(N, arr);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to swap values in arr and position
def perform_swap(x, y):
    global arr, position, answer

    # Swap position[arr[x]] and position[arr[y]]
    position[arr[x - 1]], position[arr[y - 1]] = position[arr[y - 1]], position[arr[x - 1]]
    arr[x - 1], arr[y - 1] = arr[y - 1], arr[x - 1]

    # Push x and y to the answer vector
    answer.append([x, y])

# Function to find the sequence of swaps
# that can sort the array
def sortBySwap(N, arr):
    global newArr, position, answer

    for i in range(N):
        newArr[i + 1] = arr[i]

    # Assign position of elements in position array
    for i in range(1, N + 1):
        position[newArr[i]] = i

    # Traverse from 1 to N
    for i in range(N + 1):

        # If element is already at it's right position
        if (i == position[i]):
            continue

        # If current and right place can be directly
        # swapped
        if (abs(i - position[i]) >= N // 2):
            perform_swap(i, position[i])
        else:
            # Initial position of integer i
            initial_position = position[i]

            # If |position[i]-1| >= N/2 :
            # Call perform_swap(position[i], 1)
            if (abs(position[i] - 1) >= N // 2):
                perform_swap(position[i], 1)

                # If |i-1| >= N/2 : Call perform_swap(i, 1)
                # and perform_swap(initial_position, 1)
                if (abs(i - 1) >= N // 2):
                    perform_swap(i, 1)
                    perform_swap(initial_position, 1)

                # Otherwise: Call perform_swap(1, N),
                # perform_swap(N, i) and
                # perform_swap(1, initial_position).
                else:
                    perform_swap(1, N)
                    perform_swap(N, i)
                    perform_swap(1, initial_position)

            # Otherwise: Call perform_swap(position[i], N)
            # and perform_swap(N, i)
            else:
                perform_swap(position[i], N)
                perform_swap(N, i)

    # Print the sequences which sorts
    # the given array
    for i in answer:
        print(i[0], i[1])

# Driver Code
if __name__ == '__main__':

    # Input Array
    arr = [3, 4, 1, 2]
    N = len(arr)

    newArr = [0 for i in range(N+1)]
    position = [i for i in range(N+1)]

    answer = []

    # Function Call
    sortBySwap(N, arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class Pair
{
  public int first, second;

  public Pair(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}
public class GFG
{
  static void swap(int[] a, int i, int j)
  {
    int temp = a[i];
    a[i] = a[j];
    a[j] = temp;
  }

  // Function to swap values in arr and position
  static void perform_swap(int[] arr, int[] position,
                           List<Pair> answer, int x,
                           int y)
  {

    // Swap position[arr[x]] and position[arr[y]]
    swap(position, arr[x], arr[y]);

    // Swap arr[x] and arr[y]
    swap(arr, x, y);

    // Push x and y to the answer vector
    answer.Add(new Pair(x, y));
  }

  // Function to find the sequence of swaps
  // that can sort the array
  static void sortBySwap(int N, int[] arr)
  {

    // Shifted vector of Array arr
    int[] newArr = new int[N + 1];

    for(int i = 0; i < N; i++)
      newArr[i + 1] = arr[i];

    // Keep an vector to maintain positions
    int[] position = new int[N + 1];

    // Vector to maintain the swaps performed

    List<Pair> answer = new List<Pair>();

    // Assign position of elements in position array
    for(int i = 1; i <= N; i++)
      position[newArr[i]] = i;

    // Traverse from 1 to N
    for(int i = 1; i <= N; i++)
    {

      // If element is already at it's
      // right position
      if (i == position[i])
        continue;

      // If current and right place can
      // be directly swapped
      if (Math.Abs(i - position[i]) >= N / 2)
      {
        perform_swap(newArr, position, answer, i,
                     position[i]);
      }
      else
      {

        // Initial position of integer i
        int initial_position = position[i];

        // If |position[i]-1| >= N/2 :
        // Call perform_swap(position[i], 1)
        if (Math.Abs(position[i] - 1) >= N / 2)
        {
          perform_swap(newArr, position, answer,
                       position[i], 1);

          // If |i-1| >= N/2 : Call
          // perform_swap(i, 1) and
          // perform_swap(initial_position, 1)
          if (Math.Abs(i - 1) >= N / 2)
          {
            perform_swap(newArr, position,
                         answer, i, 1);
            perform_swap(newArr, position,
                         answer,
                         initial_position, 1);
          }

          // Otherwise: Call perform_swap(1, N),
          // perform_swap(N, i) and
          // perform_swap(1, initial_position).
          else
          {
            perform_swap(newArr, position,
                         answer, 1, N);
            perform_swap(newArr, position,
                         answer, N, i);
            perform_swap(newArr, position,
                         answer, 1,
                         initial_position);
          }
        }

        // Otherwise: Call perform_swap(position[i],
        // N) and perform_swap(N, i);
        else
        {
          perform_swap(newArr, position, answer,
                       position[i], N);
          perform_swap(newArr, position, answer,
                       N, i);
        }
      }
    }

    // Print the sequences which sorts
    // the given array
    for(int i = 0; i < answer.Count; i++)
      Console.WriteLine(answer[i].first + " " +
                        answer[i].second);
  }

  // Driver code
  static public void Main ()
  {

    // Input Array
    int[] arr = { 3, 4, 1, 2 };
    int N = arr.Length;

    // Function Call
    sortBySwap(N, arr);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach
class Pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

function swap(a, i, j)
{
    let temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}

// Function to swap values in arr and position
function perform_swap(arr, position, answer, x, y)
{

    // Swap position[arr[x]] and position[arr[y]]
    swap(position, arr[x], arr[y]);

    // Swap arr[x] and arr[y]
    swap(arr, x, y);

    // Push x and y to the answer vector
    answer.push(new Pair(x, y));
}

// Function to find the sequence of swaps
// that can sort the array
function sortBySwap(N, arr)
{

    // Shifted vector of Array arr
    let newArr = new Array(N + 1);

    for(let i = 0; i < N; i++)
        newArr[i + 1] = arr[i];

    // Keep an vector to maintain positions
    let position = new Array(N + 1);

    // Vector to maintain the swaps performed
    let answer = [];

    // Assign position of elements
    // in position array
    for(let i = 1; i <= N; i++)
        position[newArr[i]] = i;

    // Traverse from 1 to N
    for(let i = 1; i <= N; i++)
    {

        // If element is already at it's
        // right position
        if (i == position[i])
            continue;

        // If current and right place can
        // be directly swapped
        if (Math.abs(i - position[i]) >= N / 2)
        {
            perform_swap(newArr, position, answer, i,
                         position[i]);
        }
        else
        {

            // Initial position of integer i
            let initial_position = position[i];

            // If |position[i]-1| >= N/2 :
            // Call perform_swap(position[i], 1)
            if (Math.abs(position[i] - 1) >= N / 2)
            {
                perform_swap(newArr, position, answer,
                             position[i], 1);

                // If |i-1| >= N/2 : Call
                // perform_swap(i, 1) and
                // perform_swap(initial_position, 1)
                if (Math.abs(i - 1) >= N / 2)
                {
                    perform_swap(newArr, position,
                                 answer, i, 1);
                    perform_swap(newArr, position,
                                 answer,
                                 initial_position, 1);
                }

                // Otherwise: Call perform_swap(1, N),
                // perform_swap(N, i) and
                // perform_swap(1, initial_position).
                else
                {
                    perform_swap(newArr, position,
                                 answer, 1, N);
                    perform_swap(newArr, position,
                                 answer, N, i);
                    perform_swap(newArr, position,
                                 answer, 1,
                                 initial_position);
                }
            }

            // Otherwise: Call perform_swap(position[i],
            // N) and perform_swap(N, i);
            else
            {
                perform_swap(newArr, position, answer,
                             position[i], N);
                perform_swap(newArr, position, answer,
                             N, i);
            }
        }
    }

    // Print the sequences which sorts
    // the given array
    for(let i = 0; i < answer.length; i++)
        document.write(answer[i].first + " " +
                       answer[i].second + "<br>");
}

// Driver code

// Input Array
let arr = [ 3, 4, 1, 2 ];
let N = arr.length;

// Function Call
sortBySwap(N, arr);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1 3
2 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)