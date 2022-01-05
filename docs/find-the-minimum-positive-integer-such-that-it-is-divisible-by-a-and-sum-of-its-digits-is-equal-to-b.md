# 求最小正整数，使其可被 A 整除，其位数之和等于 B

> 原文:[https://www . geesforgeks . org/find-最小正整数，这样它就可以被 a 整除，并且它的位数之和等于 b/](https://www.geeksforgeeks.org/find-the-minimum-positive-integer-such-that-it-is-divisible-by-a-and-sum-of-its-digits-is-equal-to-b/)

给定两个整数 **A** 和 **B** ，任务是找到最小正整数 **N** ，使得 **N** 可被 **A** 整除， **N** 的位数之和等于 **B** 。如果找不到号码，则打印 **-1** 。
**举例:**

> **输入:** A = 20，B = 30
> **输出:** 49980
> 49980 可被 20 整除，其位数之和= 4 + 9 + 9 + 8 + 0 = 30
> **输入:** A = 5，B = 2
> **输出:** 20

**进场:**

*   创建空队列 **q** ，存储 **A** 和 **B** 的值，并将数字输出为字符串，并创建整数类型 2-D 数组**visited【】【】**存储被访问的数字。
*   将节点插入队列，并检查队列是否为非空。
*   当队列非空时，从队列中弹出一个元素，对于从 **1** 到 **9** 的每一个数字，在字符串 num 之后连接该数字，并检查所形成的数字是否是所需的数字。
*   如果找到所需的号码，打印该号码。
*   否则，当号码小于 **B** 且队列为非空时，重复上述步骤，同时将非访问号码推送到队列中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Array that stores visited digits
int visited[501][5001];

// Structure for queue Node.
struct Node {
    int a, b;
    string str;
};

// Function to return the minimum number such that it is
// divisible by 'a' and sum of its digits is equals to 'b'
int findNumber(int a, int b)
{
    // Create queue
    queue<Node> q;

    // Initially queue is empty
    Node temp = Node{ 0, 0, "" };

    // Initialize visited to 1
    visited[0][0] = 1;

    // Push temp in queue
    q.push(temp);

    // While queue is not empty
    while (!q.empty()) {

        // Get the front of the queue and pop it
        Node u = q.front();
        q.pop();

        // If popped element is the required number
        if (u.a == 0 && u.b == b)

            // Parse int from string and return it
            return std::stoi(u.str);

        // Loop for each digit and check the sum
        // If not visited then push it to the queue
        for (int i = 0; i < 10; i++) {
            int dd = (u.a * 10 + i) % a;
            int ss = u.b + i;
            if (ss <= b && !visited[dd][ss]) {
                visited[dd][ss] = 1;
                q.push(Node{ dd, ss, u.str + char('0' + i) });
            }
        }
    }

    // Required number not found return -1.
    return -1;
}

// Driver code.
int main()
{
    int a = 25, b = 1;
    cout << findNumber(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class Solution
{

// Array that stores visited digits
static int visited[][]= new int[501][5001];

// Structure for queue Node.
static class Node {
    int a, b;
    String str;
    Node(int a1,int b1,String s)
    {
        a=a1;
        b=b1;
        str=s;
    }
}

// Function to return the minimum number such that it is
// divisible by 'a' and sum of its digits is equals to 'b'
static int findNumber(int a, int b)
{
    // Create queue
    Queue<Node> q= new LinkedList<Node>();

    // Initially queue is empty
    Node temp =new  Node( 0, 0, "" );

    // Initialize visited to 1
    visited[0][0] = 1;

    // Push temp in queue
    q.add(temp);

    // While queue is not empty
    while (q.size()!=0) {

        // Get the front of the queue and pop it
        Node u = q.peek();
        q.remove();

        // If popped element is the required number
        if (u.a == 0 && u.b == b)

            // Parse int from string and return it
            return Integer.parseInt(u.str);

        // Loop for each digit and check the sum
        // If not visited then push it to the queue
        for (int i = 0; i < 10; i++) {
            int dd = (u.a * 10 + i) % a;
            int ss = u.b + i;
            if (ss <= b && visited[dd][ss]==0) {
                visited[dd][ss] = 1;
                q.add(new Node( dd, ss, u.str + (char)('0' + i) ));
            }
        }
    }

    // Required number not found return -1.
    return -1;
}

// Driver code.
public static void  main(String args[])
{
    //initialize visited
    for(int i=0;i<500;i++)
        for(int j=0;j<500;j++)
            visited[i][j]=0;

    int a = 25, b = 1;
    System.out.println(findNumber(a, b));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Array that stores visited digits
visited = [[0 for x in range(501)]
              for y in range(5001)]

# Structure for queue Node.
class Node:

    def __init__(self, a, b, string):
        self.a = a
        self.b = b
        self.string = string

# Function to return the minimum number
# such that it is divisible by 'a' and
# sum of its digits is equals to 'b'
def findNumber(a, b):

    # Use list as queue
    q = []

    # Initially queue is empty
    temp = Node(0, 0, "")

    # Initialize visited to 1
    visited[0][0] = 1

    # Push temp in queue
    q.append(temp)

    # While queue is not empty
    while len(q) > 0:

        # Get the front of the queue
        # and pop it
        u = q.pop(0)

        # If popped element is the
        # required number
        if u.a == 0 and u.b == b:

            # Parse int from string
            # and return it
            return int(u.string)

        # Loop for each digit and check the sum
        # If not visited then push it to the queue
        for i in range(0, 10):
            dd = (u.a * 10 + i) % a
            ss = u.b + i

            if ss <= b and visited[dd][ss] == False:
                visited[dd][ss] = 1
                q.append(Node(dd, ss, u.string + str(i)))

    # Required number not found return -1.
    return -1

# Driver code.
if __name__ == "__main__":

    a, b = 25, 1
    print(findNumber(a, b))

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Array that stores visited digits
let visited=new Array(501);
for(let i = 0; i < 501; i++)
{
    visited[i] = new Array(5001);
    for(let j = 0; j < 5001; j++)
        visited[i][j] = 0;
}

// Structure for queue Node.
class Node
{
    constructor(a1, b1, s)
    {
        this.a = a1;
        this.b = b1;
        this.str = s;
    }
}

// Function to return the minimum number such that it is
// divisible by 'a' and sum of its digits is equals to 'b'
function findNumber(a,b)
{
    // Create queue
    let q= [];

    // Initially queue is empty
    let temp = new  Node( 0, 0, "" );

    // Initialize visited to 1
    visited[0][0] = 1;

    // Push temp in queue
    q.push(temp);

    // While queue is not empty
    while (q.length != 0) {

        // Get the front of the queue and pop it
        let u = q[0];
        q.shift();

        // If popped element is the required number
        if (u.a == 0 && u.b == b)

            // Parse int from string and return it
            return parseInt(u.str);

        // Loop for each digit and check the sum
        // If not visited then push it to the queue
        for (let i = 0; i < 10; i++) {
            let dd = (u.a * 10 + i) % a;
            let ss = u.b + i;
            if (ss <= b && visited[dd][ss] == 0) {
                visited[dd][ss] = 1;
                q.push(new Node( dd, ss, u.str + String.fromCharCode('0'.charCodeAt(0) + i) ));
            }
        }
    }

    // Required number not found return -1.
    return -1;
}

// Driver code.
let a = 25, b = 1;
document.write(findNumber(a, b));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
100
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*