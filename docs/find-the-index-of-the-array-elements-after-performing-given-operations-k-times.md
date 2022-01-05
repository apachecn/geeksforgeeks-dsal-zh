# 执行给定的 K 次运算后求数组元素的索引

> 原文:[https://www . geeksforgeeks . org/find-执行给定操作后的数组元素索引-k-times/](https://www.geeksforgeeks.org/find-the-index-of-the-array-elements-after-performing-given-operations-k-times/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是打印数组元素的位置，其中结果中的**I<sup>th</sup>T9】值是在精确地应用以下操作 **K** 次后原始数组中 i <sup>th</sup> 元素的索引:**

*   移除第一个数组元素，并将其递减 **1** 。
*   如果递减后大于 **0** ，将其放在数组的末尾，并将元素的位置向左移动。

**示例:**

> **输入:** arr[] = {3，1，3，2}，K = 4
> **输出:** {0，2，3}
> **解释:**
> 操作 1 - > arr[] = {3，1，3，2}(位置{0，1，2，3}) - > {1，3，2，2}(位置{1，2，3，0})。
> 操作 2 - > arr[] = {1，3，2，2}(位置{1，2，3，0})- > {3，2，2}(位置{2，3，0})，因为第一个元素变成了零。
> 操作 3 - > arr[] = {3，2，2}(位置{2，3，0}) - > {2，2，2}(位置{3，0，2})。
> 操作 4 - > ar[] = {2，2，2}(位置{3，0，2}) - > {2，2，1}(位置{0，2，3})。
> 
> **输入:** arr[] = {1，2，3}，K = 3
> **输出:** {1，2}
> **解释:**
> 操作 1 - > arr[] = {1，2，3}(位置{0，1，2}) - > {2，3}(位置{1，2})。
> 操作 2 - > arr[] = {2，3}(位置{1，2}) - > {3，1}(位置{2，1})，因为第一个元素变成了零。
> 操作 3 - > arr[] = {3，1}(位置{2，1}) - > {1，2}(位置{1，2})。

**方式:**思路是用一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)来模拟 **K** 的操作。按照以下步骤解决问题:

1.  初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)来存储这对 **{arr[i]，i}** 。
2.  迭代范围**【0，K–1】并执行以下操作:**
    1.  [弹出队列的前元素](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)并将其值减少 **1** 。
    2.  [将更新后的元素推回到队列中。](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)
3.  使用该对中的第二个成员，通过弹出元素直到队列为空来打印元素的位置。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print position of array
// elements after performing given
// operations exactly K times
void findElementPositions(int arr[], int N, int K)
{

    // make the queue of pairs
    queue<pair<int, int> > que;

    // Convert the array
    // to queue of pairs
    for (int i = 0; i < N; i++) {
        que.push({ arr[i], i });
    }

    // Perform the operations
    // for K units of time
    for (int i = 0; i < K; i++) {

        // get the front pair
        pair<int, int> value = que.front();

        // If the first element
        // value is one
        if (value.first == 1) {
            que.pop();
        }

        // Otherwise
        else {
            que.pop();
            value.first -= 1;
            que.push(value);
        }
    }

    // Print all the positions
    // after K operations
    while (!que.empty()) {

        pair<int, int> value = que.front();
        que.pop();

        cout << value.second << " ";
    }
}

// Driven Program
int main()
{

    // Given array
    int arr[] = { 3, 1, 3, 2 };

    // Stores the length of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 4;

    // Function call
    findElementPositions(arr, N, K);

    return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to print position of array
  // elements after performing given
  // operations exactly K times
  static void findElementPositions(int arr[], int N,
                                   int K)
  {

    // make the queue of pairs
    ArrayDeque<int[]> que = new ArrayDeque<>();

    // Convert the array
    // to queue of pairs
    for (int i = 0; i < N; i++) {
      que.addLast(new int[] { arr[i], i });
    }

    // Perform the operations
    // for K units of time
    for (int i = 0; i < K; i++) {

      // get the front pair
      int value[] = que.peekFirst();

      // If the first element
      // value is one
      if (value[0] == 1) {
        que.pollFirst();
      }

      // Otherwise
      else {
        que.pollFirst();
        value[0] -= 1;
        que.addLast(value);
      }
    }

    // Print all the positions
    // after K operations
    while (!que.isEmpty())
    {

      int value[] = que.pollFirst();
      System.out.print(value[1] + " ");
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 3, 1, 3, 2 };

    // length of the array
    int N = arr.length;

    // Given value of K
    int K = 4;

    // Function call
    findElementPositions(arr, N, K);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print position of array
# elements after performing given
# operations exactly K times
def findElementPositions(que, K):

    # Convert the queue
    # to queue of pairs
    for i in range(len(que)):
        que[i] = [que[i], i]

    # Perform the operations
    # for K units of time
    for i in range(K):

        # If the first element
        # value is one
        if que[0][0] == 1:
            que.pop(0)

        # Otherwise
        else:
            temp = que.pop(0)
            temp[0] -= 1
            que.append(temp)

    # All the positions
    # after K operations
    ans = [i[1] for i in que]

    # Print the answer
    print(ans)

# Given array
arr = [3, 1, 3, 2]

# Given value of K
K = 4

findElementPositions(arr, K)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Function to print position of array
    // elements after performing given
    // operations exactly K times
    static void findElementPositions(int[] arr, int N, int K)
    {

        // make the queue of pairs
        Queue que = new Queue();

        // Convert the array
        // to queue of pairs
        for (int i = 0; i < N; i++) {
            que.Enqueue(new Tuple<int,int>(arr[i], i));
        }

        // Perform the operations
        // for K units of time
        for (int i = 0; i < K; i++) {

            // get the front pair
            Tuple<int,int> value = (Tuple<int,int>)que.Peek();

            // If the first element
            // value is one
            if (value.Item1 == 1) {
                que.Dequeue();
            }

            // Otherwise
            else {
                que.Dequeue();
                value = new Tuple<int,int>(value.Item1-1, value.Item2);
                que.Enqueue(value);
            }
        }

        // Print all the positions
        // after K operations
        Console.Write("[");
        while (que.Count > 0) {

            Tuple<int,int> value = (Tuple<int,int>)que.Peek();
            que.Dequeue();

            if(que.Count > 0)
            {
                Console.Write(value.Item2 + ", ");
            }
            else{
                Console.Write(value.Item2);
            }
        }
        Console.Write("]");
    }

  // Driver code
  static void Main()
  {

    // Given array
    int[] arr = { 3, 1, 3, 2 };

    // Stores the length of array
    int N = arr.Length;

    // Given value of K
    int K = 4;

    // Function call
    findElementPositions(arr, N, K);
  }
}

// This code is contributed by rameshtravel07
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to print position of array
    // elements after performing given
    // operations exactly K times
    function findElementPositions(arr, N, K)
    {

        // make the queue of pairs
        let que = [];

        // Convert the array
        // to queue of pairs
        for (let i = 0; i < N; i++) {
            que.push([ arr[i], i ]);
        }

        // Perform the operations
        // for K units of time
        for (let i = 0; i < K; i++) {

            // get the front pair
            let value = que[0];

            // If the first element
            // value is one
            if (value[0] == 1) {
                que.shift();
            }

            // Otherwise
            else {
                que.shift();
                value[0] -= 1;
                que.push(value);
            }
        }

        // Print all the positions
        // after K operations
        document.write("[");
        while (que.length > 0) {

            let value = que[0];
            que.shift();
            if(que.length > 0)
            {
                document.write(value[1] + ", ");
            }
            else{
                document.write(value[1]);
            }

        }
        document.write("]");
    }

    // Given array
    let arr = [ 3, 1, 3, 2 ];

    // Stores the length of array
    let N = arr.length;

    // Given value of K
    let K = 4;

    // Function call
    findElementPositions(arr, N, K);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
[0, 2, 3]
```

***时间复杂度:** O(max(N，K))*
***辅助空间:** O(N)*