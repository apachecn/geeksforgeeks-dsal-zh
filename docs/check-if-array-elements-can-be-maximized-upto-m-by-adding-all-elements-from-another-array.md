# 通过添加另一个数组中的所有元素，检查数组元素是否可以最大化到 M

> 原文:[https://www . geeksforgeeks . org/check-if-array-elements-可以通过添加另一个数组中的所有元素来最大化最多 m 个元素/](https://www.geeksforgeeks.org/check-if-array-elements-can-be-maximized-upto-m-by-adding-all-elements-from-another-array/)

给定一个正整数 **M** 和两个分别为正整数的 **N** 和 **K** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和**值【】**，任务是将**值【】**中的每个元素添加到**arr【】**中的一个元素中，这样在执行所有添加后，数组中的最大元素最多为 **M** 。如果可以，则打印**“是”**。否则，打印**“否”**。
**举例:**

> **输入:** arr[] = {5，9，3，8，7}，值[] = {1，2，3，4}，M = 9
> **输出:**是
> **说明:**
> 加 1 & 3 使其最大化为 9。
> 加 2 & 4 到 arr[2]最大化到 9。
> 因此，最终 arr 变为{9，9，9，8，7}。
> **输入:** arr[] = {5，8，3，8，7}，值[] = {1，2，3，4}，M = 8
> **输出:**否
> **说明:**
> 将 1 加到 arr[4]，3 加到 arr[0]和 4 加到 arr[2]，数组修改为{8，8，7，8，8}。
> arr[]中当前最大元素为 8。
> 因此，从 value[]到 arr[]的任何元素只需要添加 2。
> 但是，在 arr[]中的任何元素上添加 2 时，数组中的最大元素超过了 8。

**天真方法:**
最简单的方法是从给定数组**arr【】**中选择任意 **K** 元素，并将**值【】**数组中的 **K** 值与这些选择的 **K** 值相加。这些 **K** 值可以加到 **K 中**arr【】**数组的 **K** 选择的数字上！方式**(最坏的情况下)。
***时间复杂度:**O(<sup>N</sup>P<sub>K</sub>)*
**高效途径:**
按照以下步骤解决问题:

1.  按降序对**值[]** 数组中的元素进行排序。
2.  将 **arr[]** 的所有元素存储在[最小优先级队列](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)中。
3.  现在从[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中提取最小元素(比如 **X** ，并将数组**值【】**中的元素添加到 **X** 中。
4.  当数组**值[]** 到 **X** 的值超过 **M** 时，将元素 **X** 插入优先级队列，并对优先级队列中的下一个最小值重复上述步骤。
5.  如果**值【】**中的所有元素被添加到**arr【】**中的某些元素，则**“是”**，否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function which checks if all
// additions are possible
void solve(int ar[], int values[],
        int N, int K, int M)
{

    // Sorting values[] in
    // decreasing order
    sort(values, values + K,
        greater<int>());

    // Minimum priority queue which
    // contains all the elements
    // of array arr[]
    priority_queue<int, vector<int>,
                greater<int> >
        pq;

    for (int x = 0; x < N; x++) {
        pq.push(ar[x]);
    }

    // poss stores whether all the
    // additions are possible
    bool poss = true;
    for (int x = 0; x < K; x++) {

        // Minimum value in the
        // priority queue
        int mini = pq.top();
        pq.pop();
        int val = mini + values[x];

        // If on addition it exceeds
        // M then not possible
        if (val > M) {
            poss = false;
            break;
        }
        pq.push(val);
    }

    // If all elements are added
    if (poss) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    int ar[] = { 5, 9, 3, 8, 7 };
    int N = 5;

    int values[] = { 1, 2, 3, 4 };
    int K = 4;

    int M = 9;

    solve(ar, values, N, K, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.io.*;
import java.util.*;

class GFG{

// Function which checks if all
// additions are possible
static void solve(Integer ar[], Integer values[],
                  int N, int K, int M)
{

    // Sorting values[] in
    // decreasing order
    Arrays.sort(values, (a, b) -> b - a);

    // Minimum priority queue which
    // contains all the elements
    // of array arr[]
    PriorityQueue<Integer> pq = new PriorityQueue<>();

    for(int x = 0; x < N; x++)
    {
        pq.add(ar[x]);
    }

    // poss stores whether all the
    // additions are possible
    boolean poss = true;
    for(int x = 0; x < K; x++)
    {

        // Minimum value in the
        // priority queue
        int mini = pq.peek();
        pq.poll();

        int val = mini + values[x];

        // If on addition it exceeds
        // M then not possible
        if (val > M)
        {
            poss = false;
            break;
        }
        pq.add(val);
    }

    // If all elements are added
    if (poss)
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}

// Driver Code
public static void main(String args[])
{
    Integer ar[] = { 5, 9, 3, 8, 7 };
    int N = 5;

    Integer values[] = { 1, 2, 3, 4 };
    int K = 4;

    int M = 9;

    solve(ar, values, N, K, M);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach
from queue import PriorityQueue

# Function which checks if all
# additions are possible
def solve(ar, values, N, K, M):

    # Sorting values[] in
    # decreasing order
    values.sort(reverse = True)

    # Minimum priority queue which
    # contains all the elements
    # of array arr[]
    pq = PriorityQueue()

    for x in range(N):

        pq.put(ar[x]);

    # poss stores whether all the
    # additions are possible
    poss = True;

    for x in range(K):

        # Minimum value in the
        # priority queue
        mini = pq.get();

        val = mini + values[x];

        # If on addition it exceeds
        # M then not possible
        if (val > M):
          poss = False;
          break;

        pq.put(val);

    # If all elements are added
    if (poss):
        print("Yes");
    else:
        print("No");

# Driver Code
if __name__=='__main__':

    ar = [ 5, 9, 3, 8, 7 ]
    N = 5;

    values = [ 1, 2, 3, 4 ]

    K = 4;

    M = 9;

    solve(ar, values, N, K, M);

# This code is contributed by rutvik_56
```

## C#

```
// C# Program to implement the
// above approach 
using System;
using System.Collections.Generic;
class GFG
{

    // Function which checks if all
    // additions are possible
    static void solve(int[] ar, int[] values,
            int N, int K, int M)
    {

        // Sorting values[] in
        // decreasing order
        Array.Sort(values);
        Array.Reverse(values);

        // Minimum priority queue which
        // contains all the elements
        // of array arr[]
        List<int> pq = new List<int>();

        for (int x = 0; x < N; x++)
        {
            pq.Add(ar[x]);
        }

        pq.Sort();

        // poss stores whether all the
        // additions are possible
        bool poss = true;
        for (int x = 0; x < K; x++)
        {

            // Minimum value in the
            // priority queue
            int mini = pq[0];
            pq.RemoveAt(0);
            int val = mini + values[x];

            // If on addition it exceeds
            // M then not possible
            if (val > M)
            {
                poss = false;
                break;
            }
            pq.Add(val);
            pq.Sort();
        }

        // If all elements are added
        if (poss)
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }

  // Driver code
  static void Main()
  {
    int[] ar = { 5, 9, 3, 8, 7 };
    int N = 5;

    int[] values = { 1, 2, 3, 4 };
    int K = 4;

    int M = 9;

    solve(ar, values, N, K, M);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript Program to implement the
// above approach

    // Function which checks if all
    // additions are possible
    function solve(ar, values, N, K, M)
    {

        // Sorting values[] in
        // decreasing order
        values.sort((a, b) =>  a - b);
        values.reverse();

        // Minimum priority queue which
        // contains all the elements
        // of array arr[]
        let pq = new Array();

        for (let x = 0; x < N; x++)
        {
            pq.push(ar[x]);
        }

        pq.sort((a, b) =>  a -b);

        // poss stores whether all the
        // additions are possible
        let poss = true;
        for (let x = 0; x < K; x++)
        {

            // Minimum value in the
            // priority queue
            let mini = pq[0];
            pq.shift();
            let val = mini + values[x];

            // If on addition it exceeds
            // M then not possible
            if (val > M)
            {
                poss = false;
                break;
            }
            pq.push(val);
            pq.sort((a, b) =>  a - b);
        }

        // If all elements are added
        if (poss)
        {
            document.write("Yes");
        }
        else
        {
            document.write("No");
        }
    }

// Driver code

    let ar = [ 5, 9, 3, 8, 7 ];
    let N = 5;

    let values = [ 1, 2, 3, 4 ];
    let K = 4;

    let M = 9;

    solve(ar, values, N, K, M);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O((N+K)* log(N))*
T5】辅助空间: *O(N)*