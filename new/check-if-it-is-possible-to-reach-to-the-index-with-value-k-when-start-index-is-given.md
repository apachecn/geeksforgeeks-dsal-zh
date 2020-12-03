# 检查给定起始索引时是否可以到达值为 K 的索引

> 原文： [https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-to-the-index-with-value-k-when-start-index-is-given/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-to-the-index-with-value-k-when-start-index-is-given/)

给定`N`个正整数和两个正整数`S`和`K`的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务 从索引`S`到达值为`K`的数组的位置。 我们只能从当前索引`i`移至索引**（i + arr [i]）**或**（i – arr [i]）**。 如果有一种方法可以到达值`K`的数组的位置，则打印**“是”** ，否则打印**“否”** 。

**示例**：

> **输入**：arr [] = {4，2，3，0，3，1，2}，S = 5，K =0。
> **输出**：是
> **解释**：
> 最初我们位于元素 5 的索引 5，因此可以向前或向后移动一步。 因此，到达索引 3 的值为 0 的所有可能方法是：
> 索引 5->索引 4->索引 1->索引 3
> 索引 5->索引 6- >索引 4->索引 1->索引 3。由于有可能达到索引 3，因此我们的输出为 yes。
> 
> **输入**：arr [] = {0，3，2，1，2}，S = 2，K = 3
> **输出**：否
> **说明 **：［HTG8］无法通过值 3 到达索引 1。

**方法 1 –使用 BFS** 下面讨论[广度优先搜索（BFS）](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)方法：

*   将起始索引`S`作为源节点，并将其插入[队列](http://www.geeksforgeeks.org/queue-data-structure/)中。

*   当队列不为空时，请执行以下操作：

    1.  从队列顶部弹出 **temp** 元素。

    2.  如果**临时**已被访问或它超出了绑定索引的数组，则转到步骤 1。

    3.  否则将其标记为已访问。

    4.  现在，如果 **temp** 是值为`K`的数组的索引，则打印**为“是”** 。

    5.  否则，从 temp 到**（temp + arr [temp]）**，**（temp – arr [temp]）**两个可能的目的地，并将其推入队列。

*   如果在上述步骤之后未达到具有`K`值的索引，则打印**“否”** 。

下面是上述方法的实现：

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

```cs

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

**Output:** 

```
No

```

**时间复杂度**：*O（N）*；

**辅助空间**：*O（N）*

**方法 2 –使用 DFS**：下面讨论[深度优先搜索（DFS）](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)方法：

1.  初始化数组 **Visited []** ，以将访问顶点标记为 true。

2.  从起始索引`S`开始，然后使用[递归](http://www.geeksforgeeks.org/recursion/)深入探索其他索引。

3.  在每个递归调用中，我们检查该索引是否有效或以前没有访问过。 如果不是这样，则返回 false。

4.  否则，如果该索引值为`K`，则返回 true。

5.  否则，将该索引标记为已访问，并根据当前索引 i 递归处理 **i + arr [i]** 和 **i – arr [i]** 。

6.  如果任何递归调用返回 true，则意味着我们可以到达值`K`的索引，并打印**“是”** 其他打印**“否”** 。

下面是上述方法的实现：

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

```cs

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

**Output:** 

```
No

```

**时间复杂度**：*O（N）*辅助空间： *O（N）*

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。