# 将数量 x 转换为 y 所需的最小操作数

> 原文： [https://www.geeksforgeeks.org/minimum-number-operation-required-convert-number-x-y/](https://www.geeksforgeeks.org/minimum-number-operation-required-convert-number-x-y/)

给定一个初始数 x 和下面给出的两个操作：

1.  将数字乘以 2。
2.  从数字中减去 1。

任务是找出仅使用以上两个运算将 x 转换为 y 所需的最小运算数。 我们可以多次应用这些操作。

限制条件：
1 < = x，y < = 10000

**示例**：

```
Input : x = 4, y = 7
Output : 2
We can transform x into y using following
two operations.
1\. 4*2  = 8
2\. 8-1  = 7

Input  : x = 2, y = 5
Output : 4
We can transform x into y using following
four operations.
1\. 2*2  = 4
2\. 4-1   = 3
3\. 3*2  = 6
4\. 6-1   = 5
Answer = 4
Note that other sequences of two operations 
would take more operations.

```

想法是为此使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。 我们运行一个 BFS 并通过乘以 2 并乘以 1 来创建节点，因此我们可以从起始编号获得所有可能的编号。
要点：
1）当我们从数字中减去 1 且如果其变为< 0（即负数）时，则没有理由从其创建下一个节点（根据输入约束，数字 x 和 y 为 正）。
2）另外，如果我们已经创建了号码，则没有理由再次创建它。 即我们维护一个访问数组。

## C++

```cpp

// C++ program to find minimum number of steps needed 
// to convert a number x into y with two operations 
// allowed : (1) multiplication with 2 (2) subtraction 
// with 1\. 
#include<bits/stdc++.h> 
using namespace std; 

// A node of BFS traversal 
struct node 
{ 
    int val; 
    int level; 
}; 

// Returns minimum number of operations 
// needed to convert x into y using BFS 
int minOperations(int x, int y) 
{ 
    // To keep track of visited numbers 
    // in BFS. 
    set<int> visit; 

    // Create a queue and enqueue x into it. 
    queue<node> q; 
    node n = {x, 0}; 
    q.push(n); 

    // Do BFS starting from x 
    while (!q.empty()) 
    { 
        // Remove an item from queue 
        node t = q.front(); 
        q.pop(); 

        // If the removed item is target 
        // number y, return its level 
        if (t.val == y) 
            return t.level; 

        // Mark dequeued number as visited 
        visit.insert(t.val); 

        // If we can reach y in one more step 
        if (t.val*2 == y || t.val-1 == y) 
            return t.level+1; 

        // Insert children of t if not visited 
        // already 
        if (visit.find(t.val*2) == visit.end()) 
        { 
            n.val = t.val*2; 
            n.level = t.level+1; 
            q.push(n); 
        } 
        if (t.val-1>=0 && visit.find(t.val-1) == visit.end()) 
        { 
            n.val = t.val-1; 
            n.level = t.level+1; 
            q.push(n); 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int x = 4, y = 7; 
    cout << minOperations(x, y); 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum  
// number of steps needed to 
// convert a number x into y  
// with two operations allowed :  
// (1) multiplication with 2  
// (2) subtraction with 1\. 

import java.util.HashSet; 
import java.util.LinkedList; 
import java.util.Set; 

class GFG  
{ 
    int val; 
    int steps; 

    public GFG(int val, int steps)  
    { 
        this.val = val; 
        this.steps = steps; 
    } 
} 

public class GeeksForGeeks 
{ 
    private static int minOperations(int src,  
                                     int target)  
    { 

        Set<GFG> visited = new HashSet<>(1000); 
        LinkedList<GFG> queue = new LinkedList<GFG>(); 

        GFG node = new GFG(src, 0); 

        queue.offer(node); 
        visited.add(node); 

        while (!queue.isEmpty())  
        { 
            GFG temp = queue.poll(); 
            visited.add(temp); 

            if (temp.val == target) 
            { 
                return temp.steps; 
            } 

            int mul = temp.val * 2; 
            int sub = temp.val - 1; 

            // given constraints 
            if (mul > 0 && mul < 1000)  
            { 
                GFG nodeMul = new GFG(mul, temp.steps + 1); 
                queue.offer(nodeMul); 
            } 
            if (sub > 0 && sub < 1000)  
            { 
                GFG nodeSub = new GFG(sub, temp.steps + 1); 
                queue.offer(nodeSub); 
            } 
        } 
        return -1; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        // int x = 2, y = 5; 
        int x = 4, y = 7; 
        GFG src = new GFG(x, y); 
        System.out.println(minOperations(x, y)); 
    } 
} 

// This code is contributed by Rahul 

```

## Python

```py

# Python3 program to find minimum number of  
# steps needed to convert a number x into y  
# with two operations allowed :  
# (1) multiplication with 2  
# (2) subtraction with 1.  
import queue 

# A node of BFS traversal  
class node: 
    def __init__(self, val, level): 
        self.val = val  
        self.level = level 

# Returns minimum number of operations  
# needed to convert x into y using BFS  
def minOperations(x, y): 

    # To keep track of visited numbers  
    # in BFS.  
    visit = set()  

    # Create a queue and enqueue x into it.  
    q = queue.Queue() 
    n = node(x, 0)  
    q.put(n)  

    # Do BFS starting from x  
    while (not q.empty()): 

        # Remove an item from queue  
        t = q.get()  

        # If the removed item is target  
        # number y, return its level  
        if (t.val == y): 
            return t.level  

        # Mark dequeued number as visited  
        visit.add(t.val)  

        # If we can reach y in one more step  
        if (t.val * 2 == y or t.val - 1 == y):  
            return t.level+1

        # Insert children of t if not visited  
        # already  
        if (t.val * 2 not in visit): 
            n.val = t.val * 2
            n.level = t.level + 1
            q.put(n) 
        if (t.val - 1 >= 0 and t.val - 1 not in visit): 
            n.val = t.val - 1
            n.level = t.level + 1
            q.put(n) 

# Driver code  
if __name__ == '__main__': 

    x = 4
    y = 7
    print(minOperations(x, y)) 

# This code is contributed by PranchalK 

```

**Output :**

```
2
```

本文由 **Vipin Khushu** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

