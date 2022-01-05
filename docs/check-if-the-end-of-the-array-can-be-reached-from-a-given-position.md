# 检查是否可以从给定位置到达阵列的末端

> 原文:[https://www . geesforgeks . org/check-如果可以从给定位置到达阵列末端/](https://www.geeksforgeeks.org/check-if-the-end-of-the-array-can-be-reached-from-a-given-position/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数 **S** ，任务是[从索引 **S** 到达数组](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/)的末尾。我们只能从当前索引 **i** 移动到索引 **(i + arr[i])** 或**(I–arr[I])**。如果有办法到达数组末尾，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:** arr[] = {4，1，3，2，5}，S = 1
> **输出:**是
> **说明:**
> 初始位置:arr[S] = arr[1] = 1。
> 跳跃到达终点:1 - > 4 - > 5
> 因此到达终点。
> 
> **输入:** arr[] = {2，1，4，5}，S = 2
> **输出:**否
> **说明:**
> 初始位置:arr[S] = arr[2] = 2。
> 到达终点的可能跳跃:4 - >(指数 7)或 4 - >(指数 2)
> 由于两者都在界内，因此无法到达终点。

**方法 1:** 这个问题可以使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)解决。以下是步骤:

*   将起始索引 **S** 视为源节点，并将其插入到[队列](https://www.geeksforgeeks.org/queue-data-structure/)中。
*   当队列不为空时，请执行以下操作:
    1.  从队列顶部弹出元素，说 **temp** 。
    2.  如果已经访问了 **temp** 或者它超出了数组界限索引，则转到步骤 1。
    3.  否则将其标记为已访问。
    4.  现在如果 **temp** 是数组的最后一个索引，那么打印**“是”**。
    5.  否则，从 temp 到 **(temp + arr[temp])** 、**(temp–arr[temp])**取两个可能的目的地，并将其推入队列。
*   如果在上述步骤后没有到达数组的末尾，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if we can reach to
// the end of the arr[] with possible moves
void solve(int arr[], int n, int start)
{

    // Queue to perform BFS
    queue<int> q;

    // Initially all nodes(index)
    // are not visited.
    bool visited[n] = { false };

    // Initially the end of
    // the array is not reached
    bool reached = false;

    // Push start index in queue
    q.push(start);

    // Until queue becomes empty
    while (!q.empty()) {

        // Get the top element
        int temp = q.front();

        // Delete popped element
        q.pop();

        // If the index is already
        // visited. No need to
        // traverse it again.
        if (visited[temp] == true)
            continue;

        // Mark temp as visited
        // if not
        visited[temp] = true;
        if (temp == n - 1) {

            // If reached at the end
            // of the array then break
            reached = true;
            break;
        }

        // If temp + arr[temp] and
        // temp - arr[temp] are in
        // the index of array
        if (temp + arr[temp] < n) {
            q.push(temp + arr[temp]);
        }

        if (temp - arr[temp] >= 0) {
            q.push(temp - arr[temp]);
        }
    }

    // If reaches the end of the array,
    // Print "Yes"
    if (reached == true) {
        cout << "Yes";
    }

    // Else print "No"
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 1, 3, 2, 5 };

    // Starting index
    int S = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    solve(arr, N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if we can reach to
// the end of the arr[] with possible moves
static void solve(int arr[], int n, int start)
{

    // Queue to perform BFS
    Queue<Integer> q = new LinkedList<>();

    // Initially all nodes(index)
    // are not visited.
    boolean []visited = new boolean[n];

    // Initially the end of
    // the array is not reached
    boolean reached = false;

    // Push start index in queue
    q.add(start);

    // Until queue becomes empty
    while (!q.isEmpty())
    {

        // Get the top element
        int temp = q.peek();

        // Delete popped element
        q.remove();

        // If the index is already
        // visited. No need to
        // traverse it again.
        if (visited[temp] == true)
            continue;

        // Mark temp as visited
        // if not
        visited[temp] = true;

        if (temp == n - 1)
        {

            // If reached at the end
            // of the array then break
            reached = true;
            break;
        }

        // If temp + arr[temp] and
        // temp - arr[temp] are in
        // the index of array
        if (temp + arr[temp] < n)
        {
            q.add(temp + arr[temp]);
        }

        if (temp - arr[temp] >= 0)
        {
            q.add(temp - arr[temp]);
        }
    }

    // If reaches the end of the array,
    // Print "Yes"
    if (reached == true)
    {
        System.out.print("Yes");
    }

    // Else print "No"
    else
    {
        System.out.print("No");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 1, 3, 2, 5 };

    // Starting index
    int S = 1;
    int N = arr.length;

    // Function call
    solve(arr, N, S);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
from queue import Queue

# Function to check if we can reach to
# the end of the arr[] with possible moves
def solve(arr, n, start):

    # Queue to perform BFS
    q = Queue()

    # Initially all nodes(index)
    # are not visited.
    visited = [False] * n

    # Initially the end of
    # the array is not reached
    reached = False

    # Push start index in queue
    q.put(start);

    # Until queue becomes empty
    while (not q.empty()):

        # Get the top element
        temp = q.get()

        # If the index is already
        # visited. No need to
        # traverse it again.
        if (visited[temp] == True):
            continue

        # Mark temp as visited, if not
        visited[temp] = True
        if (temp == n - 1):

            # If reached at the end
            # of the array then break
            reached = True
            break

        # If temp + arr[temp] and
        # temp - arr[temp] are in
        # the index of array
        if (temp + arr[temp] < n):
            q.put(temp + arr[temp])

        if (temp - arr[temp] >= 0):
            q.put(temp - arr[temp])

    # If reaches the end of the array,
    # Print "Yes"
    if (reached == True):
        print("Yes")

    # Else print "No"
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 4, 1, 3, 2, 5 ]

    # starting index
    S = 1
    N = len(arr)

    # Function call
    solve(arr, N, S)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if we can reach to
// the end of the []arr with possible moves
static void solve(int []arr, int n,
                  int start)
{

    // Queue to perform BFS
    Queue<int> q = new Queue<int>();

    // Initially all nodes(index)
    // are not visited.
    bool []visited = new bool[n];

    // Initially the end of
    // the array is not reached
    bool reached = false;

    // Push start index in queue
    q.Enqueue(start);

    // Until queue becomes empty
    while (q.Count != 0)
    {

        // Get the top element
        int temp = q.Peek();

        // Delete popped element
        q.Dequeue();

        // If the index is already
        // visited. No need to
        // traverse it again.
        if (visited[temp] == true)
            continue;

        // Mark temp as visited
        // if not
        visited[temp] = true;

        if (temp == n - 1)
        {

            // If reached at the end
            // of the array then break
            reached = true;
            break;
        }

        // If temp + arr[temp] and
        // temp - arr[temp] are in
        // the index of array
        if (temp + arr[temp] < n)
        {
            q.Enqueue(temp + arr[temp]);
        }

        if (temp - arr[temp] >= 0)
        {
            q.Enqueue(temp - arr[temp]);
        }
    }

    // If reaches the end of the array,
    // Print "Yes"
    if (reached == true)
    {
        Console.Write("Yes");
    }

    // Else print "No"
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 4, 1, 3, 2, 5 };

    // Starting index
    int S = 1;
    int N = arr.Length;

    // Function call
    solve(arr, N, S);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if we can reach to
// the end of the arr[] with possible moves
function solve(arr, n, start)
{

    // Queue to perform BFS
    let q = [];

    // Initially all nodes(index)
    // are not visited.
    let visited = new Array(n);
    visited.fill(false);

    // Initially the end of
    // the array is not reached
    let reached = false;

    // Push start index in queue
    q.push(start);

    // Until queue becomes empty
    while (q.length > 0)
    {

        // Get the top element
        let temp = q[0];

        // Delete popped element
        q.shift();

        // If the index is already
        // visited. No need to
        // traverse it again.
        if (visited[temp] == true)
            continue;

        // Mark temp as visited
        // if not
        visited[temp] = true;
        if (temp == n - 1)
        {

            // If reached at the end
            // of the array then break
            reached = true;
            break;
        }

        // If temp + arr[temp] and
        // temp - arr[temp] are in
        // the index of array
        if (temp + arr[temp] < n)
        {
            q.push(temp + arr[temp]);
        }

        if (temp - arr[temp] >= 0)
        {
            q.push(temp - arr[temp]);
        }
    }

    // If reaches the end of the array,
    // Print "Yes"
    if (reached == true)
    {
        document.write("Yes");
    }

    // Else print "No"
    else
    {
        document.write("No");
    }
}

// Driver code

// Given array arr[]
let arr = [ 4, 1, 3, 2, 5 ];

// Starting index
let S = 1;
let N = arr.length;

// Function Call
solve(arr, N, S);

// This code is contributed by divyeshrabadiya07 

</script>
```

**Output:** 

```
Yes
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*

**方法 2:**

1.  另一种方法是使用递归。
2.  使用递归跳转到数组的 **i + arr[i]** 和**I–arr[I]**位置，检查我们是否已经到达终点。
3.  使用递归方法的优点是它大大简化了代码。下面是实现。

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;
bool check_the_end(int arr[], int n, int i)
{

    // If we have reached out of bounds
    // of the array then return False
    if (i < 0 or i >= n)
        return false;

    // If we have reached the end then return True
    if (i == n - 1)
        return true;

    // Either of the condition return true solved the
    // problem
    return check_the_end(arr, n, i - arr[i])
           or check_the_end(arr, n, i + arr[i]);
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 3, 2, 5 };
    int S = 1;
    int n = sizeof(arr) / sizeof(arr[0]);
    bool result = check_the_end(arr, n, S);
    cout << result;

}

    // This Code is Contributed by Harshit Srivastava
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    static boolean check_the_end(int arr[], int n, int i)
    {

        // If we have reached out of bounds
        // of the array then return False
        if (i < 0 || i >= n)
            return false;

        // If we have reached the end then return True
        if (i == n - 1)
            return true;

        // Either of the condition return true solved the
        // problem
        return check_the_end(arr, n, i - arr[i])
               || check_the_end(arr, n, i + arr[i]);
    }

    // Driver Code
    public static void main (String[] args) {
        int arr[] = { 4, 1, 3, 2, 5 };
        int S = 1;
        int n = arr.length;
        boolean result = check_the_end(arr, n, S);
        System.out.println(result);

    }
}

// This Code is Contributed by Shubhamsingh10
```

## 蟒蛇 3

```
# Python program for the above approach
def check_the_end(arr, i):

    # If we have reached out of bounds
    # of the array then return False
    if i < 0 or i >= len(arr):
        return False

    # If we have reached the end then return True
    if i == len(arr) - 1:
        return True

    # Either of the condition return true solved the problem
    return check_the_end(arr, i - arr[i]) or
            check_the_end(arr, i + arr[i])

# Driver Code
arr = [4, 1, 3, 2, 5]
S = 1
result = check_the_end(arr, S)
print(result)
```

## C#

```
// C# program for the above approach
using System;

public class GFG{
    static bool check_the_end(int[] arr, int n, int i)
    {

        // If we have reached out of bounds
        // of the array then return False
        if (i < 0 || i >= n)
            return false;

        // If we have reached the end then return True
        if (i == n - 1)
            return true;

        // Either of the condition return true solved the
        // problem
        return check_the_end(arr, n, i - arr[i])
               || check_the_end(arr, n, i + arr[i]);
    }

    // Driver Code
    static public void Main (){
        int[] arr = { 4, 1, 3, 2, 5 };
        int S = 1;
        int n = arr.Length;
        bool result = check_the_end(arr, n, S);
        Console.WriteLine(result);

    }
}

// This Code is Contributed by Shubhamsingh10
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
function check_the_end(arr, n, i)
{
    // If we have reached out of bounds
    // of the array then return False
    if (i < 0 || i >= n)
        return false;

    // If we have reached the end then return True
    if (i == n - 1)
        return true;

    // Either of the condition return true solved the
    // problem
    return check_the_end(arr, n, i - arr[i])
           || check_the_end(arr, n, i + arr[i]);
}

// Driver Code
var arr = [4, 1, 3, 2, 5];
var S = 1
var n = arr.length;
var result = check_the_end(arr,n, S);
document.write(result)

// This code is contributed by Shivani

</script>
```

**输出:**

```
True
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*