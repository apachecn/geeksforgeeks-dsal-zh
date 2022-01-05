# 检查 n 元树中的镜像

> 原文:[https://www.geeksforgeeks.org/check-mirror-n-ary-tree/](https://www.geeksforgeeks.org/check-mirror-n-ary-tree/)

给定两个 n 元树，任务是检查它们是否是彼此的镜像。如果他们是对方的镜子，打印“是”或“否”。

**示例:**

```
Input : Node = 3, Edges = 2
Edge 1 of first N-ary: 1 2
Edge 2 of first N-ary: 1 3
Edge 1 of second N-ary: 1 3
Edge 2 of second N-ary: 1 2
Output : Yes
```

![](img/1064e210a13d60d2ff421f5060d122fb.png)

```
Input : Node = 3, Edges = 2
Edge 1 of first N-ary: 1 2 
Edge 2 of first N-ary: 1 3
Edge 1 of second N-ary: 1 2
Edge 2 of second N-ary: 1 3
Output : No
```

**方法 1:(使用散列法)**

这个想法是使用一个无序的堆栈图来检查给定的 N 元树是否是彼此的镜像。
设第一棵 n 元树为 t1，第二棵 n 元树为 T2。对于 t1 中的每个节点，将其连接的节点推送到映射中相应的堆栈中。现在，对于 t2 中的每个节点，它们连接的节点与栈顶匹配，然后从栈中弹出元素。

否则，如果节点与堆栈顶部不匹配，则意味着两个树互不镜像。
现在，对每个对应的节点执行以下操作:

```
  1\. Iterate over map of stack
      Push all connected nodes of each node of first tree in map of  stack.

  2\. Again iterate over map for each node of second tree
      For example :     

      Let us take one node X of second tree 

      For this node X , check in map which stack is used

      a = Top of that stack for node X present in second tree;
      b = Connected node of X in second tree
      if (a != b)
           return false;
      pop node X from stack.
```

## C++

```
// C++ program to check if two n-ary trees are
// mirror.
#include <bits/stdc++.h>
using namespace std;

// Function to check given two trees are mirror
// of each other or not
int checkMirrorTree(int M, int N, int u1[ ],
                    int v1[ ] , int u2[], int v2[])
    {
        // Map to store nodes of the tree
        unordered_map<int , stack<int>>mp;

        // Traverse first tree nodes
        for (int i = 0 ; i < N ; i++ )
        {
           mp[u1[i]].push(v1[i]);
        }

        // Traverse second tree nodes
        for (int i = 0 ; i < N ; i++)
        {
            if(mp[u2[i]].top() != v2[i])
                  return 0;
            mp[u2[i]].pop();
        }

        return 1;
    }

// Driver code
int main()
{
    int M = 7, N = 6;

    //Tree 1
    int u1[] = { 1, 1, 1, 10, 10, 10 };
    int v1[] = { 10, 7, 3, 4, 5, 6 };

    //Tree 2
    int u2[] = { 1, 1, 1, 10, 10, 10 };
    int v2[] = { 3, 7, 10, 6, 5, 4 };

    if(checkMirrorTree(M, N, u1, v1, u2, v2))
       cout<<"Yes";
    else
       cout<<"No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two n-ary trees are mirror.
import java.util.*;
public class Main
{
    // Function to check given two trees are mirror
    // of each other or not
    static boolean checkMirrorTree(int M, int N, int[] u1, int[] v1, int[] u2, int[] v2)
    {

        // Map to store nodes of the tree
        HashMap<Integer, Stack<Integer>> mp = new HashMap<>();

        // Traverse first tree nodes
        for (int i = 0 ; i < N ; i++ )
        {
           if(!mp.containsKey(u1[i]))
           {
               mp.put(u1[i], new Stack<Integer>());
           }
           else{
               mp.get(u1[i]).push(v1[i]);
           }
        }

        // Traverse second tree nodes
        for (int i = 0 ; i < N ; i++)
        {
            if(mp.containsKey(u2[i]) && mp.get(u2[i]).size() > 0)
            {
                if(mp.get(u2[i]).peek() != v2[i])
                  return false;
                mp.get(u2[i]).pop();
            }
        }

        return true;
    }

  // Driver code
    public static void main(String[] args) {
        int M = 7, N = 6;

        // Tree 1
        int[] u1 = { 1, 1, 1, 10, 10, 10 };
        int[] v1 = { 10, 7, 3, 4, 5, 6 };

        // Tree 2
        int[] u2 = { 1, 1, 1, 10, 10, 10 };
        int[] v2 = { 3, 7, 10, 6, 5, 4 };

        if(checkMirrorTree(M, N, u1, v1, u2, v2))
           System.out.print("Yes");
        else
           System.out.print("No");
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program to check if two n-ary trees are mirror.

# Function to check given two trees are mirror
# of each other or not
def checkMirrorTree(M, N, u1, v1, u2, v2):
    # Map to store nodes of the tree
    mp = {}

    # Traverse first tree nodes
    for i in range(N):
        if u1[i] in mp:
            mp[u1[i]].append(v1[i])
        else:
            mp[u1[i]] = []

    # Traverse second tree nodes
    for i in range(N):
        if u2[i] in mp and len(mp[u2[i]]) > 0:
            if(mp[u2[i]][-1] != v2[i]):
                return 0
            mp[u2[i]].pop()
    return 1

M, N = 7, 6

#Tree 1
u1 = [ 1, 1, 1, 10, 10, 10 ]
v1 = [ 10, 7, 3, 4, 5, 6 ]

#Tree 2
u2 = [ 1, 1, 1, 10, 10, 10 ]
v2 = [ 3, 7, 10, 6, 5, 4 ]

if(checkMirrorTree(M, N, u1, v1, u2, v2)):
   print("Yes")
else:
   print("No")

    # This code is contributed by rameshtravel07.
```

## C#

```
// C# program to check if two n-ary trees are mirror.
using System;
using System.Collections.Generic;
class GFG {

    // Function to check given two trees are mirror
    // of each other or not
    static bool checkMirrorTree(int M, int N, int[] u1, int[] v1, int[] u2, int[] v2)
    {

        // Map to store nodes of the tree
        Dictionary<int, Stack<int>> mp = new Dictionary<int, Stack<int>>();

        // Traverse first tree nodes
        for (int i = 0 ; i < N ; i++ )
        {
           if(!mp.ContainsKey(u1[i]))
           {
               mp[u1[i]] = new Stack<int>();
           }
           else{
               mp[u1[i]].Push(v1[i]);
           }
        }

        // Traverse second tree nodes
        for (int i = 0 ; i < N ; i++)
        {
            if(mp.ContainsKey(u2[i]) && mp[u2[i]].Count > 0)
            {
                if(mp[u2[i]].Peek() != v2[i])
                  return false;
                mp[u2[i]].Pop();
            }
        }

        return true;
    }

  // Driver code
  static void Main()
  {
    int M = 7, N = 6;

    // Tree 1
    int[] u1 = { 1, 1, 1, 10, 10, 10 };
    int[] v1 = { 10, 7, 3, 4, 5, 6 };

    // Tree 2
    int[] u2 = { 1, 1, 1, 10, 10, 10 };
    int[] v2 = { 3, 7, 10, 6, 5, 4 };

    if(checkMirrorTree(M, N, u1, v1, u2, v2))
       Console.Write("Yes");
    else
       Console.Write("No");
  }
}

// This code is contributed by mukesh07.
```

**Output**

```
Yes
```

**方法 2:(使用链接列表):**

主要方法是使用一个堆栈列表和一个队列列表来存储以两个数组形式给出的节点值。

```
1\. Initialize both the lists with empty stack and empty queues respectively.

2\. Now, iterate over the lists
    Push all connected nodes of each node of first tree in list of stack and second tree list of queue.

3\. Now iterate over the array and pop item from both stack and queue and check if they are same, if not same then return 0.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check two n-ary trees are mirror.

import java.io.*;
import java.util.*;

class GFG {

      // Function to check given two trees are mirror
    // of each other or not
      static int checkMirrorTree(int n, int e, int[] A, int[] B) {

          //Lists to store nodes of the tree
        List<Stack<Integer>> s = new ArrayList<>();
        List<Queue<Integer>> q = new ArrayList<>();

        // initializing both list with empty stack and queue
        for (int i = 0; i <= n; i++) {
            s.add(new Stack<>());
            Queue<Integer> queue = new LinkedList<>();
            q.add(queue);
        }

           // add all nodes of tree 1 to list of stack and tree 2 to list of queue
        for (int i = 0; i < 2 * e; i += 2) {
            s.get(A[i]).push(A[i + 1]);
            q.get(B[i]).add(B[i + 1]);
        }

          // now take out the stack and queues
        // for each of the nodes and compare them
        // one by one
        for (int i = 1; i <= n; i++) {
            while (!s.get(i).isEmpty() && !q.get(i).isEmpty()) {
                int a = s.get(i).pop();
                int b = q.get(i).poll();

                if (a != b) {
                    return 0;
                }
            }
        }

        return 1;
    }

    public static void main (String[] args) {
        int n = 3;
        int e = 2;
        int A[] = { 1, 2, 1, 3 };
        int B[] = { 1, 3, 1, 2 };

        if (checkMirrorTree(n, e, A, B) == 1) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }

    }
}
```

## 蟒蛇 3

```
# Python3 program to check two n-ary trees are mirror.

# Function to check given two trees are mirror
# of each other or not
def checkMirrorTree(n, e, A, B):
    # Lists to store nodes of the tree
    s = []
    q = []

    # initializing both list with empty stack and queue
    for i in range(n + 1):
        s.append([])
        queue = []
        q.append(queue)

   # add all nodes of tree 1 to
   # list of stack and tree 2 to list of queue
    for i in range(0, 2 * e, 2):
        s[A[i]].append(A[i + 1])
        q[B[i]].append(B[i + 1])

    # now take out the stack and queues
    # for each of the nodes and compare them
    # one by one
    for i in range(1, n + 1):
        while (len(s[i]) > 0 and len(q[i]) > 0):
            a = s[i][len(s[i]) - 1]
            s[i].pop()
            b = q[i][0]
            q[i].pop(0)

            if (a != b):
                return 0
    return 1

  # Driver code
n = 3
e = 2
A = [ 1, 2, 1, 3 ]
B = [ 1, 3, 1, 2 ]

if (checkMirrorTree(n, e, A, B) == 1):
    print("Yes")
else:
    print("No")

    # This code is contributed by decode2207.
```

## C#

```
// C# program to check two n-ary trees are mirror.
using System;
using System.Collections;
using System.Collections.Generic;
class GFG {

    // Function to check given two trees are mirror
    // of each other or not
    static int checkMirrorTree(int n, int e, int[] A, int[] B)
    {
        //Lists to store nodes of the tree
        List<Stack> s = new List<Stack>();
        List<Queue> q = new List<Queue>();

        // initializing both list with empty stack and queue
        for (int i = 0; i <= n; i++) {
            s.Add(new Stack());
            Queue queue = new Queue();
            q.Add(queue);
        }

           // add all nodes of tree 1 to list of stack and tree 2 to list of queue
        for (int i = 0; i < 2 * e; i += 2) {
            s[A[i]].Push(A[i + 1]);
            q[B[i]].Enqueue(B[i + 1]);
        }

          // now take out the stack and queues
        // for each of the nodes and compare them
        // one by one
        for (int i = 1; i <= n; i++) {
            while (s[i].Count > 0 && q[i].Count > 0) {
                int a = (int)s[i].Pop();
                int b = (int)q[i].Dequeue();

                if (a != b) {
                    return 0;
                }
            }
        }

        return 1;
    }

  static void Main() {
    int n = 3;
    int e = 2;
    int[] A = { 1, 2, 1, 3 };
    int[] B = { 1, 3, 1, 2 };

    if (checkMirrorTree(n, e, A, B) == 1) {
        Console.Write("Yes");
    } else {
        Console.Write("No");
    }
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program to check two n-ary trees are mirror.

    // Function to check given two trees are mirror
    // of each other or not
      function checkMirrorTree(n, e, A, B) {

          //Lists to store nodes of the tree
        let s = [];
        let q = [];

        // initializing both list with empty stack and queue
        for (let i = 0; i <= n; i++) {
            s.push([]);
            let queue = [];
            q.push(queue);
        }

           // add all nodes of tree 1 to
           // list of stack and tree 2 to list of queue
        for (let i = 0; i < 2 * e; i += 2) {
            s[A[i]].push(A[i + 1]);
            q[B[i]].push(B[i + 1]);
        }

          // now take out the stack and queues
        // for each of the nodes and compare them
        // one by one
        for (let i = 1; i <= n; i++) {
            while (s[i].length > 0 && q[i].length > 0) {
                let a = s[i][s[i].length - 1];
                s[i].pop();
                let b = q[i][0];
                q[i].shift();

                if (a != b) {
                    return 0;
                }
            }
        }

        return 1;
    }

    let n = 3;
    let e = 2;
    let A = [ 1, 2, 1, 3 ];
    let B = [ 1, 3, 1, 2 ];

    if (checkMirrorTree(n, e, A, B) == 1) {
      document.write("Yes");
    } else {
      document.write("No");
    }

   // This code is contributed by suresh07.
</script>
```

**Output**

```
Yes
```

参考:[https://practice . geeks forgeks . org/problems/check-镜中月树/0](https://practice.geeksforgeeks.org/problems/check-mirror-in-n-ary-tree/0)
本文由 **Nitin Kumar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。