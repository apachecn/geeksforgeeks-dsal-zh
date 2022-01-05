# 按照给定查询的指定重新排列和更新数组元素

> 原文:[https://www . geeksforgeeks . org/重排并更新由给定查询指定的数组元素/](https://www.geeksforgeeks.org/rearrange-and-update-array-elements-as-specified-by-the-given-queries/)

给定一个大小为 **N** 的数组 **arr[]** ，并查询 **Q[][]** ，任务是对给定的数组执行以下类型的查询。 **0:** 将数组左移一个位置。

*   **1:** 将数组右移一个位置。
*   **2 X Y:** 更新**arr【X】= Y**的值。
*   **3 X:** 打印**arr【X】**。

**示例:**

> **输入:** arr[]={1，2，3，4，5}，Q[][]={{0}，{1}，{3，1}，{2，2，54}，{3，2}}。
> **输出:** 4 54
> **说明:**
> 查询 1:数组 arr[]修改为{2，3，4，5，1}
> 查询 2:数组 arr[]修改为{1，2，3，4，5}
> 查询 3:打印 arr[1]的值，即 2
> 查询 4:数组 arr[]修改为{1，54，3，4，5}
> 查询 5:打印
> 
> **输入:** arr[]={1}，Q[][]={{0}，{1}，{2，0，54}，{3，0}}
> **输出:** 54

**处理方法:**使用[德克尔(双端队列)](https://www.geeksforgeeks.org/deque-cpp-stl/)在 O(1)中的队列前后执行插入和删除操作，可以解决这个问题。按照以下步骤解决问题。

1.  创建双端[队列](https://www.geeksforgeeks.org/queue-data-structure/)、 **dq** 。
2.  将数组的所有元素 **arr[]** 推送到 **dq** 。
3.  对于类型为 **0** (左移)的查询，从 **dq** 的前面弹出一个元素，将该元素推到 **dq** 的后面。
4.  对于类型为 **1(** 右移)的查询，从 **dq** 的后面弹出一个元素，将该元素推到 **dq** 的前面。
5.  对于类型 **2** 的查询，更新 **dq[X] = Y** 。
6.  类型 **3** 的查询，打印**dq【X】**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the
// given operations
void Queries(int arr[], int N,
             vector<vector<int> >& Q)
{

    // Dequeue to store the
    // array elements
    deque<int> dq;

    // Insert all element of
    // the array into the dequeue
    for (int i = 0; i < N; i++) {
        dq.push_back(arr[i]);
    }

    // Stores the size of the queue
    int sz = Q.size();

    // Traverse each query
    for (int i = 0; i < sz; i++) {

        // Query for left shift.
        if (Q[i][0] == 0) {

            // Extract the element at
            // the front of the queue
            int front = dq[0];

            // Pop the element at
            // the front of the queue
            dq.pop_front();

            // Push the element at
            // the back of the queue
            dq.push_back(front);
        }

        // Query for right shift
        else if (Q[i][0] == 1) {

            // Extract the element at
            // the back of the queue
            int back = dq[N - 1];

            // Pop the element at
            // the back of the queue
            dq.pop_back();

            // Push the element at
            // the front of the queue
            dq.push_front(back);
        }

        // Query for update
        else if (Q[i][0] == 2) {

            dq[Q[i][1]] = Q[i][2];
        }

        // Query to get the value
        else {
            cout << dq[Q[i][1]] << " ";
        }
    }
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    vector<vector<int> > Q;

    // All possible Queries
    Q = { { 0 }, { 1 }, { 3, 1 },
          { 2, 2, 54 }, { 3, 2 } };

    Queries(arr, N, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to perform the
// given operations
static void Queries(int arr[], int N,
                    int [][]Q)
{
  // Dequeue to store the
  // array elements
  Vector<Integer> dq = new Vector<>();

  // Insert all element of
  // the array into the dequeue
  for (int i = 0; i < N; i++)
  {
    dq.add(arr[i]);
  }

  // Stores the size of the queue
  int sz = Q.length;

  // Traverse each query
  for (int i = 0; i < sz; i++)
  {
    // Query for left shift.
    if (Q[i][0] == 0)
    {
      // Extract the element at
      // the front of the queue
      int front = dq.get(0);

      // Pop the element at
      // the front of the queue
      dq.remove(0);

      // Push the element at
      // the back of the queue
      dq.add(front);
    }

    // Query for right shift
    else if (Q[i][0] == 1)
    {
      // Extract the element at
      // the back of the queue
      int back = dq.elementAt(dq.size() - 1);

      // Pop the element at
      // the back of the queue
      dq.remove(dq.size() - 1);

      // Push the element at
      // the front of the queue
      dq.add(0, back);
    }

    // Query for update
    else if (Q[i][0] == 2)
    {
      dq.set(Q[i][1], Q[i][2]);
    }

    // Query to get the value
    else
    {
      System.out.print(dq.get(Q[i][1]) + " ");
    }
  }
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 2, 3, 4, 5};
  int N = arr.length;

  // Vector<Vector<Integer>
  // > Q = new Vector<>();

  // All possible Queries
  int [][]Q = {{0}, {1}, {3, 1},
               {2, 2, 54}, {3, 2}};
  Queries(arr, N, Q);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import deque

# Function to perform the
# given operations
def Queries(arr, N, Q):

    # Dequeue to store the
    # array elements
    dq = deque()

    # Insert all element of
    # the array into the dequeue
    for i in range(N):
        dq.append(arr[i])

    # Stores the size of the queue
    sz = len(Q)

    # Traverse each query
    for i in range(sz):

        # Query for left shift.
        if (Q[i][0] == 0):

            # Extract the element at
            # the front of the queue
            front = dq[0]

            # Pop the element at
            # the front of the queue
            dq.popleft()

            # Push the element at
            # the back of the queue
            dq.appendleft(front)

        # Query for right shift
        elif (Q[i][0] == 1):

            # Extract the element at
            # the back of the queue
            back = dq[N - 1]

            # Pop the element at
            # the back of the queue
            dq.popleft()

            # Push the element at
            # the front of the queue
            dq.appendleft(back)

        # Query for update
        elif (Q[i][0] == 2):
            dq[Q[i][1]] = Q[i][2]

        # Query to get the value
        else:
            print(dq[Q[i][1]], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5 ]
    N = len(arr)

    # All possible Queries
    Q = [ [ 0 ], [ 1 ], [ 3, 1 ],
          [ 2, 2, 54 ], [ 3, 2 ] ]

    Queries(arr, N, Q)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to perform the
// given operations
function Queries(arr,N,Q)
{
  // Dequeue to store the
  // array elements
  let dq = [];

  // Insert all element of
  // the array into the dequeue
  for (let i = 0; i < N; i++)
  {
    dq.push(arr[i]);
  }

  // Stores the size of the queue
  let sz = Q.length;

  // Traverse each query
  for (let i = 0; i < sz; i++)
  {
    // Query for left shift.
    if (Q[i][0] == 0)
    {
      // Extract the element at
      // the front of the queue
      let front = dq[0];

      // Pop the element at
      // the front of the queue
      dq.shift();

      // Push the element at
      // the back of the queue
      dq.push(front);
    }

    // Query for right shift
    else if (Q[i][0] == 1)
    {
      // Extract the element at
      // the back of the queue
      let back = dq[dq.length - 1];

      // Pop the element at
      // the back of the queue
      dq.pop();

      // Push the element at
      // the front of the queue
      dq.unshift( back);
    }

    // Query for update
    else if (Q[i][0] == 2)
    {
      dq[Q[i][1]] = Q[i][2];
    }

    // Query to get the value
    else
    {
      document.write(dq[Q[i][1]] + " ");
    }
  }
}

// Driver Code
let arr=[1, 2, 3, 4, 5];
let N = arr.length;

// Vector<Vector<Integer>
// > Q = new Vector<>();

// All possible Queries
let Q = [[0], [1], [3, 1],
[2, 2, 54], [3, 2]];
Queries(arr, N, Q);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
2 54
```

***时间复杂度** : O(N+|Q|)*
***辅助空间:** O(N)*