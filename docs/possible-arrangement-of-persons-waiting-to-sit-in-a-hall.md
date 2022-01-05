# 大厅内等候就座人员的可能安排

> 原文:[https://www . geeksforgeeks . org/可能的人员安排-等待入座大厅/](https://www.geeksforgeeks.org/possible-arrangement-of-persons-waiting-to-sit-in-a-hall/)

给定一个整数 **N** 、一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个数组 **W[]** 。 **S** 表示 **N * 2** 人进入大厅的顺序，其中 **0** 表示男生， **1** 表示女生。 **W[]** 表示每排座椅的宽度，其中每排正好由 **2** 个座椅组成。任务是找到进入大厅的人员的可能安排，以满足以下条件:

*   一个男孩选了一排两个座位都是空的。在所有这些行中，他选择宽度最小的一行。
*   女孩选择一排，其中一个座位被男孩占据。在所有这些行中，她选择宽度最大的一行。

**示例:**

> **输入:** N = 3，W[] = {2，1，3}，S = "001011"
> **输出:**2 1 3 3 2
> T6】说明:
> 人进入大厅的方式如下:
> **人 1:** 第一个人是男生，此时所有座位都空着。所以，他可以选择任何一排坐下。在所有行中，座位宽度最小的一行是第二行。所以，第一个人坐在第二排的座位上。
> **第二个人:**第二个人也是男生，现在 2 个座位空着，座位宽度 2 & 3。所以，他坐在第一排，因为它的座位宽度最小。
> **人 3:** 第三个是女生，她可以坐一排已经有人的座位，即第一排和第二排。在这些排中，女孩选择坐在宽度最大的一排，所以她坐在第一排。
> **人 4:** 第四个是男生，只能坐第三排，因为现在只有第三排空着。
> **人 5:** 第五个是女生，可以坐 2 排或者 3 排，有一个座位有人。所以她选择了第三排，因为它的座位比第二排的座位宽。
> **人 6:** 终于来了一个女生，只能坐 2 排。
> 
> **输入:** N = 3，W[] = {1，3，2}，S = "010011"
> **输出:** 1 1 3 2 2 3

**天真的方法:**最简单的方法是取一个大小为 **N** 的数组，如果两个对值都被标记为空，并且宽度最小，则在每个男孩进入公共汽车时将其标记为已占用。同样，只有当单个值被标记为已占用并具有最大宽度时，才能在女孩的条目上标记已占用。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，思路是使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。按照以下步骤解决问题:

*   [按升序排列座位宽度的给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。
*   创建一个优先级队列并保留一个索引变量，以跟踪男孩在**arr【】**中占据的行数。
*   创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**ans【】**来存储结果。
*   遍历字符串 **s** 的每个字符，如果**s【I】**是 **0** ，则在向量中推送**arr【ind】**的索引，并将**arr【ind】**推入队列。
*   否则，弹出队列的顶部元素，然后在向量中推这个元素的索引。
*   经过以上步骤。打印存储在**ans【】**中的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the arrangement
// of seating
void findTheOrder(int arr[], string s,
                  int N)
{
    // Stores the row in which the
    // ith person sits
    vector<int> ans;

    // Stores the width of seats along
    // with their index or row number
    pair<int, int> A[N];

    for (int i = 0; i < N; i++)
        A[i] = { arr[i], i + 1 };

    // Sort the array
    sort(A, A + N);

    // Store the seats and row for
    // boy's seat
    priority_queue<pair<int, int> > q;

    // Stores the index of row upto
    // which boys have taken seat
    int index = 0;

    // Iterate the string
    for (int i = 0; i < 2 * N; i++) {
        if (s[i] == '0') {

            // Push the row number at
            // index in vector and heap
            ans.push_back(A[index].second);
            q.push(A[index]);

            // Increment the index to let
            // the next boy in the next
            // minimum width vacant row
            index++;
        }

        // Otherwise
        else {

            // If girl then take top of
            // element of the max heap
            ans.push_back(q.top().second);

            // Pop from queue
            q.pop();
        }
    }

    // Print the values
    for (auto i : ans) {
        cout << i << " ";
    }
}

// Driver Code
int main()
{
    // Given N
    int N = 3;

    // Given arr[]
    int arr[] = { 2, 1, 3 };

    // Given string
    string s = "001011";

    // Function Call
    findTheOrder(arr, s, N);

    return 0;
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

// Function to find the arrangement
// of seating
static void findTheOrder(int arr[], String s,
                         int N)
{

    // Stores the row in which the
    // ith person sits
    List<Integer> ans = new ArrayList<Integer>();

    // Stores the width of seats along
    // with their index or row number
    List<Pair> A = new ArrayList<Pair>();

    for(int i = 0; i < N; i++)
    {
        Pair p = new Pair(arr[i], i + 1);
        A.add(p);
    }

    // Sort the array
    Collections.sort(A, (p1, p2) -> p1.first -
                                    p2.first);

    // Store the seats and row for
    // boy's seat
    PriorityQueue<Pair> q = new PriorityQueue<Pair>(
        N, (p1, p2) -> p2.first - p1.first);

    // Stores the index of row upto
    // which boys have taken seat
    int index = 0;

    // Iterate the string
    for(int i = 0; i < 2 * N; i++)
    {
        if (s.charAt(i) == '0')
        {

            // Push the row number at
            // index in vector and heap
            ans.add(A.get(index).second);
            q.add(A.get(index));

            // Increment the index to let
            // the next boy in the next
            // minimum width vacant row
            index++;
        }

        // Otherwise
        else
        {

            // If girl then take top of
            // element of the max heap
            ans.add(q.peek().second);

            // Pop from queue
            q.poll();
        }
    }

    // Print the values
    for(int i : ans)
    {
        System.out.print(i + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given N
    int N = 3;

    // Given arr[]
    int arr[] = { 2, 1, 3 };

    // Given string
    String s = "001011";

    // Function Call
    findTheOrder(arr, s, N);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the arrangement
# of seating
def findTheOrder(arr, s, N):

    # Stores the row in which the
    # ith person sits
    ans = []

    # Stores the width of seats along
    # with their index or row number
    A = [[] for i in range(N)]

    for i in range(N):
        A[i] = [arr[i], i + 1]

    # Sort the array
    A = sorted(A)

    # Store the seats and row for
    # boy's seat
    q = []

    # Stores the index of row upto
    # which boys have taken seat
    index = 0

    # Iterate the string
    for i in range(2 * N):
        if (s[i] == '0'):

            # Push the row number at
            # index in vector and heap
            ans.append(A[index][1])
            q.append(A[index])

            # Increment the index to let
            # the next boy in the next
            # minimum width vacant row
            index += 1

        # Otherwise
        else:

            # If girl then take top of
            # element of the max heap
            ans.append(q[-1][1])

            # Pop from queue
            del q[-1]

        q = sorted(q)

    # Print the values
    for i in ans:
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given N
    N = 3

    # Given arr[]
    arr = [ 2, 1, 3 ]

    # Given string
    s = "001011"

    # Function Call
    findTheOrder(arr, s, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the arrangement
    // of seating
    static void findTheOrder(int[] arr, string s, int N)
    {

        // Stores the row in which the
        // ith person sits
        List<int> ans = new List<int>();

        // Stores the width of seats along
        // with their index or row number
        Tuple<int, int>[] A = new Tuple<int,int>[N];

        for (int i = 0; i < N; i++)
            A[i] = new Tuple<int,int>(arr[i], i + 1);

        // Sort the array
        Array.Sort(A);

        // Store the seats and row for
        // boy's seat
        List<Tuple<int, int>> q = new List<Tuple<int,int>>();

        // Stores the index of row upto
        // which boys have taken seat
        int index = 0;

        // Iterate the string
        for (int i = 0; i < 2 * N; i++)
        {
            if (s[i] == '0')
            {

                // Push the row number at
                // index in vector and heap
                ans.Add(A[index].Item2);
                q.Add(A[index]);
                q.Sort();
                q.Reverse();

                // Increment the index to let
                // the next boy in the next
                // minimum width vacant row
                index++;
            }

            // Otherwise
            else
            {

                // If girl then take top of
                // element of the max heap
                ans.Add(q[0].Item2);

                // Pop from queue
                q.RemoveAt(0);
            }
        }

        // Print the values
        foreach(int i in ans)
        {
            Console.Write(i + " ");
        }
    }

  // Driver code
  static void Main()
  {
    // Given N
    int N = 3;

    // Given arr[]
    int[] arr = { 2, 1, 3 };

    // Given string
    string s = "001011";

    // Function Call
    findTheOrder(arr, s, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the arrangement
// of seating
function findTheOrder(arr, s, N)
{

    // Stores the row in which the
    // ith person sits
    let ans = [];

    // Stores the width of seats along
    // with their index or row number
    let A = [];

    for(let i = 0; i < N; i++)
    {
        let p = [arr[i], i + 1];
        A.push(p);
    }

    // Sort the array
    A.sort(function(p1, p2){return p1[0]-p2[0];});

    // Store the seats and row for
    // boy's seat
    let q = [];

    // Stores the index of row upto
    // which boys have taken seat
    let index = 0;

    // Iterate the string
    for(let i = 0; i < 2 * N; i++)
    {
        if (s[i] == '0')
        {

            // Push the row number at
            // index in vector and heap
            ans.push(A[index][1]);
            q.push(A[index]);

            // Increment the index to let
            // the next boy in the next
            // minimum width vacant row
            index++;
        }

        // Otherwise
        else
        {

            // If girl then take top of
            // element of the max heap
            ans.push(q[0][1]);

            // Pop from queue
            q.shift();
        }
        q.sort(function(a,b){return b[0]-a[0];});
    }

    // Print the values
    for(let i=0;i< ans.length;i++)
    {
        document.write(ans[i] + " ");
    }
}

// Driver Code
// Given N
let N = 3;

// Given arr[]
let arr = [ 2, 1, 3 ];

// Given string
let s = "001011";

// Function Call
findTheOrder(arr, s, N);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2 1 1 3 3 2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*