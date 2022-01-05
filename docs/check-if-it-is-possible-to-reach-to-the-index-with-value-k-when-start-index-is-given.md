# 当给定起始指数时，检查是否有可能到达 K 值的指数

> 原文:[https://www . geeksforgeeks . org/check-如果给定了起始索引，是否有可能到达带值索引 k/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-to-the-index-with-value-k-when-start-index-is-given/)

给定一个由 **N** 个正整数和两个正整数 **S** 和 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是从索引 **S** 到达数组中值为 **K** 的位置。我们只能从当前索引 **i** 移动到索引 **(i + arr[i])** 或**(I–arr[I])**。如果有办法到达值为 **K** 的数组位置，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:** arr[] = {4，2，3，0，3，1，2}，S = 5，K = 0。
> **输出:**是
> **解释:**
> 最初我们站在指数 5，也就是元素 1，因此我们可以向前或向后移动一步。因此，以值 0 到达指数 3 的所有可能方式是:
> 指数 5 - >指数 4 - >指数 1 - >指数 3
> 指数 5 - >指数 6 - >指数 4 - >指数 1 - >指数 3。因为有可能达到指数 3，我们的输出是肯定的。
> 
> **输入:** arr[] = {0，3，2，1，2}，S = 2，K = 3
> **输出:**否
> **说明:**
> 没有办法用值 3 达到指标 1。

**方法 1–使用 BFS**[广度优先搜索(BFS)](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 方法讨论如下:

*   将起始索引 **S** 视为源节点，并将其插入到[队列](https://www.geeksforgeeks.org/queue-data-structure/)中。
*   当队列不为空时，请执行以下操作:
    1.  从队列顶部弹出元素，说 **temp** 。
    2.  如果已经访问了 **temp** 或者它超出了数组界限索引，则转到步骤 1。
    3.  否则将其标记为已访问。
    4.  现在如果 **temp** 是值为 **K** 的数组的索引，那么打印**“是”**。
    5.  否则，从 temp 到 **(temp + arr[temp])** 、**(temp–arr[temp])**取两个可能的目的地，并将其推入队列。
*   如果在上述步骤后没有达到数值为 **K** 的指标，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// BFS approach to check if traversal
// is possible or not
bool check(int arr[], int& s_start,
        int start, bool visited[],
        int size, int K)
{
    queue<int> q;

    // Push start index into queue
    q.push(start);

    // Until queue is not empty
    while (!q.empty()) {

        // Top element of queue
        int front = q.front();

        // Pop the topmost element
        q.pop();

        // mark as visited
        visited[front] = true;

        if (arr[front] == K
            && front != s_start) {
            return true;
        }

        // Check for i + arr[i]
        if (front + arr[front] >= 0
            && front + arr[front] < size
            && visited[front + arr[front]]
                == false) {

            q.push(front + arr[front]);
        }

        // Check for i - arr[i]
        if (front - arr[front] >= 0
            && front - arr[front] < size
            && visited[front - arr[front]]
                == false) {

            q.push(front - arr[front]);
        }
    }

    return false;
}

// Function to check if index with value
// K can be reached or not
void solve(int arr[], int n, int start,
        int K)
{

    // Initialize visited array
    bool visited[n] = { false };

    // BFS Traversal
    bool ans = check(arr, start, start,
                    visited, n, K);

    // Print the result
    if (ans)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    solve(arr, N, start, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // BFS approach to check if traversal
  // is possible or not
  static boolean check(int arr[], int s_start, int start,
                       boolean visited[], int size, int K)
  {
    Queue<Integer> q = new LinkedList<Integer>();

    // Push start index into queue
    q.add(start);

    // Until queue is not empty
    while (!q.isEmpty())
    {

      // Top element of queue
      int front = q.peek();

      // Pop the topmost element
      q.remove();

      // mark as visited
      visited[front] = true;

      if (arr[front] == K && front != s_start)
      {
        return true;
      }

      // Check for i + arr[i]
      if (front + arr[front] >= 0 &&
          front + arr[front] < size &&
          visited[front + arr[front]] == false)
      {

        q.add(front + arr[front]);
      }

      // Check for i - arr[i]
      if (front - arr[front] >= 0 &&
          front - arr[front] < size &&
          visited[front - arr[front]] == false)
      {
        q.add(front - arr[front]);
      }
    }

    return false;
  }

  // Function to check if index with value
  // K can be reached or not
  static void solve(int arr[], int n, int start, int K)
  {

    // Initialize visited array
    boolean visited[] = new boolean[n];

    // BFS Traversal
    boolean ans = check(arr, start, start,
                        visited, n, K);

    // Print the result
    if (ans)
      System.out.print("Yes");
    else
      System.out.print("No");
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given array arr[]
    int arr[] = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = arr.length;

    // Function Call
    solve(arr, N, start, K);
  }
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# BFS approach to check if traversal
# is possible or not
def check(arr, s_start, start,
          visited, size, K):

    q = []

    # Push start index into queue
    q.append(start)

    # Until queue is not empty
    while (len(q) != 0):

        # Top element of queue
        front = q[-1]

        # Pop the topmost element
        q.pop(0)

        # Mark as visited
        visited[front] = True

        if (arr[front] == K and front != s_start):
            return True

        # Check for i + arr[i]
        if (front + arr[front] >= 0 and
            front + arr[front] < size and
            visited[front + arr[front]] == False):
            q.append(front + arr[front])

        # Check for i - arr[i]
        if (front - arr[front] >= 0 and
            front - arr[front] < size and
            visited[front - arr[front]] == False):
            q.append(front - arr[front])

    return False

# Function to check if index with value
# K can be reached or not
def solve(arr, n, start, K):

    # Initialize visited array
    visited = [False for i in range(n)]

    # BFS Traversal
    ans = check(arr, start, start,
                visited, n, K)

    # Print the result
    if (ans):
        print('Yes')
    else:
        print('No')

# Driver Code
if __name__=="__main__":

    # Given array arr[]
    arr = [ 3, 0, 2, 1, 2 ]

    # Given start and end
    start = 2
    K = 0

    N = len(arr)

    # Function Call
    solve(arr, N, start, K)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// BFS approach to check if traversal
// is possible or not
static bool check(int []arr, int s_start, int start,
                  bool []visited, int size, int K)
{
    Queue<int> q = new Queue<int>();

    // Push start index into queue
    q.Enqueue(start);

    // Until queue is not empty
    while (q.Count != 0)
    {

        // Top element of queue
        int front = q.Peek();

        // Pop the topmost element
        q.Dequeue();

        // mark as visited
        visited[front] = true;

        if (arr[front] == K && front != s_start)
        {
            return true;
        }

        // Check for i + arr[i]
        if (front + arr[front] >= 0 &&
            front + arr[front] < size &&
            visited[front + arr[front]] == false)
        {
            q.Enqueue(front + arr[front]);
        }

        // Check for i - arr[i]
        if (front - arr[front] >= 0 &&
            front - arr[front] < size &&
            visited[front - arr[front]] == false)
        {
            q.Enqueue(front - arr[front]);
        }
    }
    return false;
}

// Function to check if index with value
// K can be reached or not
static void solve(int []arr, int n, int start,
                  int K)
{

    // Initialize visited array
    bool []visited = new bool[n];

    // BFS Traversal
    bool ans = check(arr, start, start,
                     visited, n, K);

    // Print the result
    if (ans)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = arr.Length;

    // Function call
    solve(arr, N, start, K);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // BFS approach to check if traversal
    // is possible or not
    function check(arr, s_start, start, visited, size, K)
    {
      let q = [];

      // Push start index into queue
      q.push(start);

      // Until queue is not empty
      while (q.length > 0)
      {

        // Top element of queue
        let front = q[0];

        // Pop the topmost element
        q.shift();

        // mark as visited
        visited[front] = true;

        if (arr[front] == K && front != s_start)
        {
          return true;
        }

        // Check for i + arr[i]
        if (front + arr[front] >= 0 &&
            front + arr[front] < size &&
            visited[front + arr[front]] == false)
        {

          q.push(front + arr[front]);
        }

        // Check for i - arr[i]
        if (front - arr[front] >= 0 &&
            front - arr[front] < size &&
            visited[front - arr[front]] == false)
        {
          q.push(front - arr[front]);
        }
      }

      return false;
    }

    // Function to check if index with value
    // K can be reached or not
    function solve(arr, n, start, K)
    {

      // Initialize visited array
      let visited = new Array(n);

      // BFS Traversal
      let ans = check(arr, start, start,
                          visited, n, K);

      // Print the result
      if (ans)
        document.write("Yes");
      else
        document.write("No");
    }

    // Given array arr[]
    let arr = [ 3, 0, 2, 1, 2 ];

    // Given start and end
    let start = 2;
    let K = 0;

    let N = arr.length;

    // Function Call
    solve(arr, N, start, K);

</script>
```

**Output**

```
No
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*

**方法 2–使用深度优先搜索法:**[深度优先搜索法(DFS)](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 方法讨论如下:

1.  初始化一个数组**访问过的[]** 将访问过的顶点标记为真。
2.  从起始索引 **S** 开始，使用[递归](https://www.geeksforgeeks.org/recursion/)深入探索其他索引。
3.  在每次递归调用中，我们检查该索引是否有效，或者之前是否被访问过。如果不是这样，我们返回 false。
4.  否则，如果该索引值为 **K** ，我们返回 true。
5.  否则将索引标记为已访问，并从当前索引 I 中递归处理 **i + arr[i]** 和**I–arr[I]**
6.  如果任何递归调用返回真，这意味着我们有可能到达具有值 **K** 的索引，并且我们打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// DFS approach to check if traversal
// is possible or not
bool check(int arr[], int& s_start,
        int start, bool visited[],
        int size, int K)
{
    // Base cases
    if (start < 0 || start >= size
        || visited[start]) {
        return false;
    }

    // Check if start index value K
    if (arr[start] == K
        && start != s_start) {
        return true;
    }

    // Mark as visited
    visited[start] = true;

    // Check for both i + arr[i]
    // and i - arr[i] recursively
    return (check(arr, s_start,
                start + arr[start],
                visited, size, K)

            || check(arr, s_start,
                    start - arr[start],
                    visited, size, K));
}

// Function to check if index with value
// K can be reached or not
void solve(int arr[], int n, int start,
        int K)
{

    // Initialize visited array
    bool visited[n] = { false };

    // DFS Traversal
    bool ans = check(arr, start, start,
                    visited, n, K);

    // Print the result
    if (ans)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    solve(arr, N, start, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// DFS approach to check if traversal
// is possible or not
public static boolean check(int[] arr, int s_start,
                            int start, boolean[] visited,
                            int size, int K)
{

    // Base cases
    if (start < 0 || start >= size ||
        visited[start])
    {
        return false;
    }

    // Check if start index value K
    if (arr[start] == K &&
            start != s_start)
    {
        return true;
    }

    // Mark as visited
    visited[start] = true;

    // Check for both i + arr[i]
    // and i - arr[i] recursively
    return (check(arr, s_start,
                start + arr[start],
                visited, size, K) ||
            check(arr, s_start,
                start - arr[start],
                visited, size, K));
}

// Function to check if index with value
// K can be reached or not
public static void solve(int[] arr, int n,
                        int start, int K)
{

    // Initialize visited array
    boolean[] visited = new boolean[n];
    Arrays.fill(visited, false);

    // DFS Traversal
    boolean ans = check(arr, start, start,
                        visited, n, K);

    // Print the result
    if (ans)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = arr.length;

    // Function call
    solve(arr, N, start, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# DFS approach to check if traversal
# is possible or not
def check(arr, s_start, start, visited,
          size, K):

    # Base cases
    if (start < 0 or start >= size or
        visited[start]):
        return False

    # Check if start index value K
    if (arr[start] == K and
            start != s_start):
        return True

    # Mark as visited
    visited[start] = True

    # Check for both i + arr[i]
    # and i - arr[i] recursively
    return (check(arr, s_start,
                  start + arr[start],
                  visited, size, K) or
            check(arr, s_start,
                  start - arr[start],
                  visited, size, K))

# Function to check if index with value
# K can be reached or not
def solve(arr, n, start, K):

    # Initialize visited array
    visited = [False] * n

    # DFS Traversal
    ans = check(arr, start, start,
                visited, n, K)

    # Print the result
    if (ans):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [ 3, 0, 2, 1, 2 ]

    # Given start and end
    start = 2
    K = 0

    N = len(arr)

    # Function call
    solve(arr, N, start, K)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// DFS approach to check if traversal
// is possible or not
public static bool check(int[] arr, int s_start,
                         int start, bool[] visited,
                         int size, int K)
{

    // Base cases
    if (start < 0 || start >= size||
        visited[start])
    {
        return false;
    }

    // Check if start index value K
    if (arr[start] == K &&
            start != s_start)
    {
        return true;
    }

    // Mark as visited
    visited[start] = true;

    // Check for both i + arr[i]
    // and i - arr[i] recursively
    return (check(arr, s_start,
                  start + arr[start],
                  visited, size, K) ||
            check(arr, s_start,
                  start - arr[start],
                  visited, size, K));
}

// Function to check if index with value
// K can be reached or not
public static void solve(int[] arr, int n,
                         int start, int K)
{

    // Initialize visited array
    bool[] visited = new bool[n];

    // DFS Traversal
    bool ans = check(arr, start, start,
                     visited, n, K);

    // Print the result
    if (ans)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = arr.Length;

    // Function call
    solve(arr, N, start, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// DFS approach to check if traversal
// is possible or not
function check(arr, s_start,
        start, visited,
        size, K)
{
    // Base cases
    if (start < 0 || start >= size
        || visited[start]) {
        return false;
    }

    // Check if start index value K
    if (arr[start] == K
        && start != s_start) {
        return true;
    }

    // Mark as visited
    visited[start] = true;

    // Check for both i + arr[i]
    // and i - arr[i] recursively
    return (check(arr, s_start,
                start + arr[start],
                visited, size, K)

            || check(arr, s_start,
                    start - arr[start],
                    visited, size, K));
}

// Function to check if index with value
// K can be reached or not
function solve(arr, n, start, K)
{

    // Initialize visited array
    var visited = Array(n).fill(false);

    // DFS Traversal
    var ans = check(arr, start, start,
                    visited, n, K);

    // Print the result
    if (ans)
        document.write("Yes");
    else
        document.write("No");
}

// Driver Code

// Given array arr[]
var arr = [ 3, 0, 2, 1, 2 ];

// Given start and end
var start = 2;
var K = 0;
var N = arr.length;

// Function Call
solve(arr, N, start, K);

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
No
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*

**方法 3 : DFS(高效方法):**我们将遵循下面提到的步骤:

1.  由于数组只包含正数，所以每次使用 dfs 时，都将该数字乘以-1，这确认我们以前访问过该元素。
2.  检查给定的索引元素是否与 K 相同。
3.  否则，通过增加 **start + arr[start]** 和减少**start–arr[start]**来调用 dfs。
4.  在基本情况下，检查**开始**是否在数组长度范围内，并检查之前是否访问过。

上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// DFS approach to check if traversal
// is possible or not
bool dfs(int arr[], int N, int start, int K)
{
    // Base cases
    if (start < 0 || start >= N || arr[start] < 0)
        return false;

    // Marking visited
    arr[start] *= -1;

    // Checking is that the element we needed or not
    // otherwise making call for dfs again for different
    // positions
    return (abs(arr[start]) == K)
           || dfs(arr, N, start + arr[start], K)
           || dfs(arr, N, start - arr[start], K);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    bool flag = dfs(arr, N, start, K);
    if (flag)
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG {

    // DFS approach to check if traversal
    // is possible or not
    public static boolean dfs(int[] arr, int N, int start,
                              int K)
    {
        // Base Cases
        if (start < 0 || start >= N || arr[start] < 0)
            return false;

        // Marking visited
        arr[start] *= -1;

        // Checking is that the element we needed or not
        // otherwise making call for dfs again for different
        // positions
        return (Math.abs(arr[start]) == K)
            || dfs(arr, N, start + arr[start], K)
            || dfs(arr, N, start - arr[start], K);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given array arr[]
        int arr[] = { 3, 0, 2, 1, 2 };

        // Given start and end
        int start = 2;
        int K = 0;

        int N = arr.length;

        // Function call
        if (dfs(arr, N, start, K))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# DFS approach to check if traversal
# is possible or not
def dfs(arr, N, start, K):
    # Base Cases
    if start < 0 or start >= N or arr[start] < 0:
        return False

    # Marking visited
    arr[start] *= -1

    # Checking is that the element we needed or not
    # otherwise making call for dfs again for different positions
    return abs(arr[start]) == K or dfs(arr, N, start + arr[start], K) or dfs(arr, N, start - arr[start], K)

# Given array arr[]
arr = [ 3, 0, 2, 1, 2 ]

# Given start and end
start = 2
K = 0

N = len(arr)

# Function call
if dfs(arr, N, start, K):
  print("Yes")
else:
  print("No")

  # This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // DFS approach to check if traversal
    // is possible or not
    static bool dfs(int[] arr, int N, int start, int K)
    {

        // Base Cases
        if (start < 0 || start >= N || arr[start] < 0)
            return false;

        // Marking visited
        arr[start] *= -1;

        // Checking is that the element we needed or not
        // otherwise making call for dfs again for different
        // positions
        return (Math.Abs(arr[start]) == K)
            || dfs(arr, N, start + arr[start], K)
            || dfs(arr, N, start - arr[start], K);
    }

  static void Main()
  {

    // Given array arr[]
    int[] arr = { 3, 0, 2, 1, 2 };

    // Given start and end
    int start = 2;
    int K = 0;

    int N = arr.Length;

    // Function call
    if (dfs(arr, N, start, K))
        Console.Write("Yes");
    else
        Console.Write("No");
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // DFS approach to check if traversal
    // is possible or not
    function dfs(arr, N, start, K)
    {
        // Base Cases
        if (start < 0 || start >= N || arr[start] < 0)
            return false;

        // Marking visited
        arr[start] *= -1;

        // Checking is that the element we needed or not
        // otherwise making call for dfs again for different
        // positions
        return (Math.abs(arr[start]) == K)
            || dfs(arr, N, start + arr[start], K)
            || dfs(arr, N, start - arr[start], K);
    }

    // Given array arr[]
    let arr = [ 3, 0, 2, 1, 2 ];

    // Given start and end
    let start = 2;
    let K = 0;

    let N = arr.length;

    // Function call
    if (dfs(arr, N, start, K))
      document.write("Yes");
    else
      document.write("No");

// This code is contributed by mukesh07.
</script>
```

**Output**

```
No
```

**时间复杂度:** O(n)

**辅助空间:** O(n)，(空间只用于递归)