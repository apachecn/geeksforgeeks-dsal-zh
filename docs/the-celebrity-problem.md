# 名人问题

> 原文:[https://www.geeksforgeeks.org/the-celebrity-problem/](https://www.geeksforgeeks.org/the-celebrity-problem/)

*N 个人的聚会，每个人只认识一个人。这样的人**可能在党内**在场，如果是的话，(s)他在党内不认识任何人。我们只能问类似**A 认识 B 吗？**”。在最少数量的问题中找到陌生人(名人)。*
我们可以把输入的问题描述为代表聚会中人物的数字/字符数组。我们还有一个假设函数*有一个 quantity(A，B)* ，如果 A 知道 B，则返回 *true* ，否则返回 *false* 。我们如何解决这个问题。

**示例:**

```
Input:
MATRIX = { {0, 0, 1, 0},
           {0, 0, 1, 0},
           {0, 0, 0, 0},
           {0, 0, 1, 0} }
Output:id = 2
Explanation: The person with ID 2 does not 
know anyone but everyone knows him

Input:
MATRIX = { {0, 0, 1, 0},
           {0, 0, 1, 0},
           {0, 1, 0, 0},
           {0, 0, 1, 0} }
Output: No celebrity
Explanation: There is no celebrity.
```

我们根据对*的呼叫来衡量复杂性。*

**<u>方法 1:</u>** 这使用 Graph 来得出特定的解。

**方法:**
使用图形建模解决方案。将每个顶点的内倾角和外倾角初始化为 0。如果甲知道乙，画一条从甲到乙的有向边，把乙的度数和甲的度数增加 1。为每个可能的对[i，j]构造图的所有可能的边。有 N <sub>C2</sub> 对。如果聚会中有一个名人，图中会有一个外倾角为零、内倾角为 N-1 的汇聚节点。

**算法:**

1.  创建两个数组*增量*和*增量*，以存储增量和增量
2.  运行嵌套循环，外环从 0 到 n，内环从 0 到 n。
3.  对于每一对 I，j 检查我是否知道 j，然后增加 I 的外倾角和 j 的内倾角
4.  对于每一对 I，j 检查 j 是否知道 I，然后增加 j 的外倾角和 I 的内倾角
5.  运行一个从 0 到 n 的循环，找到索引为 n-1 且外倾角为 0 的 id

**实施:**

## C++

```
// C++ program to find celebrity
#include <bits/stdc++.h>
#include <list>
using namespace std;

// Max # of persons in the party
#define N 8

// Person with 2 is celebrity
bool MATRIX[N][N] = {{0, 0, 1, 0},
                    {0, 0, 1, 0},
                    {0, 0, 0, 0},
                    {0, 0, 1, 0}};

bool knows(int a, int b)
{
    return MATRIX[a][b];
}

// Returns -1 if celebrity
// is not present. If present,
// returns id (value from 0 to n-1).
int findCelebrity(int n)
{
    //the graph needs not be constructed
    //as the edges can be found by
    //using knows function

    //degree array;
    int indegree[n]={0},outdegree[n]={0};

    //query for all edges
    for(int i=0; i<n; i++)
    {
        for(int j=0; j<n; j++)
        {
            int x = knows(i,j);

            //set the degrees
            outdegree[i]+=x;
            indegree[j]+=x;
        }
    }

    //find a person with indegree n-1
    //and out degree 0
    for(int i=0; i<n; i++)
    if(indegree[i] == n-1 && outdegree[i] == 0)
        return i;

    return -1;
}

// Driver code
int main()
{
    int n = 4;
    int id = findCelebrity(n);
    id == -1 ? cout << "No celebrity" :
               cout << "Celebrity ID " << id;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find celebrity
import java.util.*;
class GFG {

  // Max # of persons in the party
  static final int N = 8;

  // Person with 2 is celebrity
  static int MATRIX[][] = { { 0, 0, 1, 0 },
                           { 0, 0, 1, 0 },
                           { 0, 0, 0, 0 },
                           { 0, 0, 1, 0 } };

  static int knows(int a, int b) { return MATRIX[a][b]; }

  // Returns -1 if celebrity
  // is not present. If present,
  // returns id (value from 0 to n-1).
  static int findCelebrity(int n)
  {

    // the graph needs not be constructed
    // as the edges can be found by
    // using knows function

    // degree array;
    int[] indegree = new int[n];
    int[] outdegree = new int[n];

    // query for all edges
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < n; j++)
      {
        int x = knows(i, j);

        // set the degrees
        outdegree[i] += x;
        indegree[j] += x;
      }
    }

    // find a person with indegree n-1
    // and out degree 0
    for (int i = 0; i < n; i++)
      if (indegree[i] == n - 1 && outdegree[i] == 0)
        return i;

    return -1;
  }

  // Driver code
  public static void main(String[] args)
  {
    int n = 4;
    int id = findCelebrity(n);
    if (id == -1)
      System.out.print("No celebrity");
    else
      System.out.print("Celebrity ID " + id);
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find celebrity

# Max # of persons in the party
N = 8

# Person with 2 is celebrity
MATRIX = [ [ 0, 0, 1, 0 ],
           [ 0, 0, 1, 0 ],
           [ 0, 0, 0, 0 ],
           [ 0, 0, 1, 0 ] ]

def knows(a, b):

  return MATRIX[a][b]

def findCelebrity(n):

    # The graph needs not be constructed
    # as the edges can be found by
    # using knows function

    # degree array;
    indegree = [0 for x in range(n)]
    outdegree = [0 for x in range(n)]

    # Query for all edges
    for i in range(n):
        for j in range(n):
            x = knows(i, j)

            # Set the degrees
            outdegree[i] += x
            indegree[j] += x

    # Find a person with indegree n-1
    # and out degree 0
    for i in range(n):
        if (indegree[i] == n - 1 and
           outdegree[i] == 0):
            return i

    return -1

# Driver code   
if __name__ == '__main__':

    n = 4
    id_ = findCelebrity(n)

    if id_ == -1:
        print("No celebrity")
    else:
        print("Celebrity ID", id_)

# This code is contributed by UnworthyProgrammer
```

## C#

```
// C# program to find celebrity
using System;
public class GFG
{

  // Max # of persons in the party
  static readonly int N = 8;

  // Person with 2 is celebrity
  static int[,] MATRIX = { { 0, 0, 1, 0 },
                           { 0, 0, 1, 0 },
                           { 0, 0, 0, 0 },
                           { 0, 0, 1, 0 } };

  static int knows(int a, int b) { return MATRIX[a,b]; }

  // Returns -1 if celebrity
  // is not present. If present,
  // returns id (value from 0 to n-1).
  static int findCelebrity(int n)
  {

    // the graph needs not be constructed
    // as the edges can be found by
    // using knows function

    // degree array;
    int[] indegree = new int[n];
    int[] outdegree = new int[n];

    // query for all edges
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < n; j++)
      {
        int x = knows(i, j);

        // set the degrees
        outdegree[i] += x;
        indegree[j] += x;
      }
    }

    // find a person with indegree n-1
    // and out degree 0
    for (int i = 0; i < n; i++)
      if (indegree[i] == n - 1 && outdegree[i] == 0)
        return i;

    return -1;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int n = 4;
    int id = findCelebrity(n);
    if (id == -1)
      Console.Write("No celebrity");
    else
      Console.Write("Celebrity ID " + id);
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to find celebrity

    // Max # of persons in the party
      var N = 8;

    // Person with 2 is celebrity
    var MATRIX = [ [ 0, 0, 1, 0 ],
                   [ 0, 0, 1, 0 ],
                   [ 0, 0, 0, 0 ],
                   [ 0, 0, 1, 0 ] ];

    function knows(a , b) {
        return MATRIX[a][b];
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    function findCelebrity(n) {

        // the graph needs not be constructed
        // as the edges can be found by
        // using knows function

        // degree array;
        var indegree = Array(n).fill(0);
        var outdegree = Array(n).fill(0);

        // query for all edges
        for (var i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                var x = knows(i, j);

                // set the degrees
                outdegree[i] += x;
                indegree[j] += x;
            }
        }

        // find a person with indegree n-1
        // and out degree 0
        for (i = 0; i < n; i++)
            if (indegree[i] == n - 1 && outdegree[i] == 0)
                return i;

        return -1;
    }

    // Driver code

        var n = 4;
        var id = findCelebrity(n);
        if (id == -1)
            document.write("No celebrity");
        else
            document.write("Celebrity ID " + id);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Celebrity ID 2
```

**复杂度分析:**

*   **时间复杂度:** O(n <sup>2</sup> )。
    运行嵌套循环遍历数组，因此时间复杂度为 0(n<sup>2</sup>
*   **空间复杂度:** O(n)。
    因为需要 n 号的额外空间。

**方法:**
这个问题可以用递归来解决。比如说，如果知道了 N-1 个人的“潜在名人”，能从中找到 N 的解决方案吗？一个潜在的名人是在消灭 n-1 个人后剩下的唯一一个人。n-1 人通过以下策略被淘汰:

*   如果 A 认识 B，那么 A 就不可能是名人。但是 B 可能是。
*   否则如果 B 认识 A，那么 B 不可能是名人。但是 A 可能是。

上述方法使用**递归**在 n 个人中寻找潜在名人，递归调用 n-1 个人，直到达到 0 个人的基本情况。对于 0 个人-返回 1，表示没有可能的名人，因为有 0 个人。在递归的第 I 阶段，比较第 I 个人和第(i-1)个人，以检查他们中是否有人知道对方。使用上面的逻辑(在要点中)，潜在的名人回到第(i+1)阶段。

一旦递归函数返回一个 id。我们检查这个 id 是否不认识其他人，但是所有其他人都知道这个 id。如果这是真的，那么这个 id 将是名人。

**算法:**

1.  创建一个接受整数 n 的递归函数。
2.  检查基本情况，如果 n 值为 0，则返回-1。
3.  调用递归函数，从前 n-1 个元素中获取潜在名人的 ID。
4.  如果 id 是-1，那么将 n 指定为潜在名人并返回值。
5.  如果前 n-1 个元素的潜在名人知道 n-1，则返回 n-1(基于 0 的索引)
6.  如果前 n-1 个元素的名人不知道 n-1，则返回 n-1 个元素的名人的 id(基于 0 的索引)
7.  否则返回-1
8.  创建一个包装函数，检查函数返回的 id 是否真的是名人。

**实施:**

## C++

```
// C++ program to find celebrity
#include <bits/stdc++.h>
#include <list>
using namespace std;

// Max # of persons in the party
#define N 8

// Person with 2 is celebrity
bool MATRIX[N][N] = { { 0, 0, 1, 0 },
                      { 0, 0, 1, 0 },
                      { 0, 0, 0, 0 },
                      { 0, 0, 1, 0 } };

bool knows(int a, int b) { return MATRIX[a][b]; }

// Returns -1 if a 'potential celebrity'
// is not present. If present,
// returns id (value from 0 to n-1).
int findPotentialCelebrity(int n)
{
    // base case - when n reaches 0 , returns -1
    // since n represents the number of people,
    // 0 people implies no celebrity(= -1)
    if (n == 0)
        return -1;

    // find the celebrity with n-1
    // persons
    int id = findPotentialCelebrity(n - 1);

    // if there are no celebrities
    if (id == -1)
        return n - 1;

    // if the id knows the nth person
    // then the id cannot be a celebrity, but nth person
    // could be one
    else if (knows(id, n - 1)) {
        return n - 1;
    }
    // if the nth person knows the id,
    // then the nth person cannot be a celebrity and the id
    // could be one
    else if (knows(n - 1, id)) {
        return id;
    }

    // if there is no celebrity
    return -1;
}

// Returns -1 if celebrity
// is not present. If present,
// returns id (value from 0 to n-1).
// a wrapper over findCelebrity
int Celebrity(int n)
{
    // find the celebrity
    int id = findPotentialCelebrity(n);

    // check if the celebrity found
    // is really the celebrity
    if (id == -1)
        return id;
    else {
        int c1 = 0, c2 = 0;

        // check the id is really the
        // celebrity
        for (int i = 0; i < n; i++)
            if (i != id) {
                c1 += knows(id, i);
                c2 += knows(i, id);
            }

        // if the person is known to
        // everyone.
        if (c1 == 0 && c2 == n - 1)
            return id;

        return -1;
    }
}

// Driver code
int main()
{
    int n = 4;
    int id = Celebrity(n);
    id == -1 ? cout << "No celebrity"
             : cout << "Celebrity ID " << id;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Max # of persons in the party
    static int N = 8;

    // Person with 2 is celebrity
    static int MATRIX[][] = { { 0, 0, 1, 0 },
                              { 0, 0, 1, 0 },
                              { 0, 0, 0, 0 },
                              { 0, 0, 1, 0 } };

    static int knows(int a, int b) { return MATRIX[a][b]; }

    // Returns -1 if a 'potential celebrity'
    // is not present. If present,
    // returns id (value from 0 to n-1).
    static int findPotentialCelebrity(int n)
    {
        // base case - when n reaches 0 , returns -1
        // since n represents the number of people,
        // 0 people implies no celebrity(= -1)
        if (n == 0)
            return -1;

        // find the celebrity with n-1
        // persons
        int id = findPotentialCelebrity(n - 1);

        // if there are no celebrities
        if (id == -1)
            return n - 1;

        // if the id knows the nth person
        // then the id cannot be a celebrity, but nth person
        // could be one
        else if (knows(id, n - 1) == 1) {
            return n - 1;
        }
        // if the nth person knows the id,
        // then the nth person cannot be a celebrity and the
        // id could be one
        else if (knows(n - 1, id) == 1) {
            return id;
        }

        // if there is no celebrity
        return -1;
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    // a wrapper over findCelebrity
    static int Celebrity(int n)
    {
        // find the celebrity
        int id = findPotentialCelebrity(n);

        // check if the celebrity found
        // is really the celebrity
        if (id == -1)
            return id;
        else {
            int c1 = 0, c2 = 0;

            // check the id is really the
            // celebrity
            for (int i = 0; i < n; i++)
                if (i != id) {
                    c1 += knows(id, i);
                    c2 += knows(i, id);
                }

            // if the person is known to
            // everyone.
            if (c1 == 0 && c2 == n - 1)
                return id;

            return -1;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        int id = Celebrity(n);
        if (id == -1) {
            System.out.println("No celebrity");
        }
        else {
            System.out.println("Celebrity ID " + id);
        }
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program to find celebrity

# Max # of persons in the party
N = 8

# Person with 2 is celebrity
MATRIX = [[0, 0, 1, 0],
           [0, 0, 1, 0],
           [0, 0, 0, 0],
           [0, 0, 1, 0]]

def knows(a, b):

    return MATRIX[a][b]

# Returns -1 if a potential celebrity
# is not present. If present,
# returns id (value from 0 to n-1).

def findPotentialCelebrity(n):

    # Base case
    if (n == 0):
        return 0;

    # Find the celebrity with n-1
    # persons
    id_ = findPotentialCelebrity(n - 1)

    # If there are no celebrities
    if (id_ == -1):
        return n - 1
    # if the id knows the nth person
    # then the id cannot be a celebrity, but nth person
    # could be on
    elif knows(id_, n - 1):
          return n - 1
    # if the id knows the nth person
    # then the id cannot be a celebrity, but nth person
    # could be one
    elif knows(n - 1, id_):
          return id_
    # If there is no celebrity
    return - 1

# Returns -1 if celebrity
# is not present. If present,
# returns id (value from 0 to n-1).
# a wrapper over findCelebrity
def Celebrity(n):

    # Find the celebrity
    id_=findPotentialCelebrity(n)

    # Check if the celebrity found
    # is really the celebrity
    if (id_ == -1):
        return id_
    else:
        c1=0
        c2=0

        # Check the id is really the
        # celebrity
        for i in range(n):
            if (i != id_):
                c1 += knows(id_, i)
                c2 += knows(i, id_)

        # If the person is known to
        # everyone.
        if (c1 == 0 and c2 == n - 1):
            return id_

        return -1

# Driver code
if __name__ == '__main__':

    n=4
    id_=Celebrity(n)

    if id_ == -1:
        print("No celebrity")
    else:
        print("Celebrity ID", id_)

# This code is contributed by UnworthyProgrammer
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    // Max # of persons in the party
    static int N = 8;

    // Person with 2 is celebrity
    static int [,]MATRIX = { { 0, 0, 1, 0 },
                              { 0, 0, 1, 0 },
                              { 0, 0, 0, 0 },
                              { 0, 0, 1, 0 } };

    static int knows(int a, int b) { return MATRIX[a,b]; }

    // Returns -1 if a 'potential celebrity'
    // is not present. If present,
    // returns id (value from 0 to n-1).
    static int findPotentialCelebrity(int n)
    {

        // base case - when n reaches 0 , returns -1
        // since n represents the number of people,
        // 0 people implies no celebrity(= -1)
        if (n == 0)
            return -1;

        // find the celebrity with n-1
        // persons
        int id = findPotentialCelebrity(n - 1);

        // if there are no celebrities
        if (id == -1)
            return n - 1;

        // if the id knows the nth person
        // then the id cannot be a celebrity, but nth person
        // could be one
        else if (knows(id, n - 1) == 1) {
            return n - 1;
        }

        // if the nth person knows the id,
        // then the nth person cannot be a celebrity and the
        // id could be one
        else if (knows(n - 1, id) == 1) {
            return id;
        }

        // if there is no celebrity
        return -1;
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    // a wrapper over findCelebrity
    static int Celebrity(int n)
    {

        // find the celebrity
        int id = findPotentialCelebrity(n);

        // check if the celebrity found
        // is really the celebrity
        if (id == -1)
            return id;
        else {
            int c1 = 0, c2 = 0;

            // check the id is really the
            // celebrity
            for (int i = 0; i < n; i++)
                if (i != id) {
                    c1 += knows(id, i);
                    c2 += knows(i, id);
                }

            // if the person is known to
            // everyone.
            if (c1 == 0 && c2 == n - 1)
                return id;

            return -1;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 4;
        int id = Celebrity(n);
        if (id == -1) {
            Console.WriteLine("No celebrity");
        }
        else {
            Console.WriteLine("Celebrity ID " + id);
        }
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Max # of persons in the party
var N = 8;

    // Person with 2 is celebrity
    var MATRIX = [ [ 0, 0, 1, 0 ],
                              [ 0, 0, 1, 0 ],
                              [ 0, 0, 0, 0 ],
                              [ 0, 0, 1, 0 ] ];

    function knows(a, b)
    {
        return MATRIX[a][b];

    }

    // Returns -1 if a 'potential celebrity'
    // is not present. If present,
    // returns id (value from 0 to n-1).
    function findPotentialCelebrity(n)
    {
        // base case - when n reaches 0 , returns -1
        // since n represents the number of people,
        // 0 people implies no celebrity(= -1)
        if (n == 0)
            return -1;

        // find the celebrity with n-1
        // persons
        var id = findPotentialCelebrity(n - 1);

        // if there are no celebrities
        if (id == -1)
            return n - 1;

        // if the id knows the nth person
        // then the id cannot be a celebrity, but nth person
        // could be one
        else if (knows(id, n - 1) == 1) {
            return n - 1;
        }
        // if the nth person knows the id,
        // then the nth person cannot be a celebrity and the
        // id could be one
        else if (knows(n - 1, id) == 1) {
            return id;
        }

        // if there is no celebrity
        return -1;
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    // a wrapper over findCelebrity
    function Celebrity(n)
    {
        // find the celebrity
        var id = findPotentialCelebrity(n);

        // check if the celebrity found
        // is really the celebrity
        if (id == -1)
            return id;
        else {
            var c1 = 0, c2 = 0;

            // check the id is really the
            // celebrity
            for (var i = 0; i < n; i++)
                if (i != id) {
                    c1 += knows(id, i);
                    c2 += knows(i, id);
                }

            // if the person is known to
            // everyone.
            if (c1 == 0 && c2 == n - 1)
                return id;

            return -1;
        }
    }

    // Driver code
        var n = 4;
        var id = Celebrity(n);
        if (id == -1) {
            document.write("No celebrity");
        }
        else {
            document.write("Celebrity ID " + id);
        }

// This code is contributed by shivanisinghss2110
</script>
```

**输出:**

```
Celebrity ID 2
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    递归函数被调用 n 次，所以时间复杂度为 O(n)。
*   **空间复杂度:** O(1)。
    因为不需要额外的空间。

**方法:**有一些基于消去法的观察(参考*波利亚的《如何求解》*一书)。

*   如果 A 认识 B，那么 A 不可能是名人。弃甲，*乙可能是名人*。
*   如果 A 不认识 B，那么 B 就不可能是名人。弃 B， *A 可能是名人*。
*   重复以上两个步骤，直到只有一个人。
*   确保留下的人是名人。(这一步的需要是什么？)

**算法:**

1.  创建一个堆栈并推送堆栈中的所有 id。
2.  当堆栈中有 1 个以上的元素时运行循环。
3.  从堆栈中弹出前两个元素(将它们表示为 A 和 B)
4.  如果 A 认识 B，那么 A 就不能成为名人，把 B 推上栈。否则如果 A 不认识 B，那么 B 也不可能是堆里的名人推 A。
5.  将堆栈中的剩余元素指定为名人。
6.  运行一个从 0 到 n-1 的循环，找出认识名人的人数和名人认识的人数。如果知道名人的人数是 n-1，而知道名人的人数是 0，那么返回名人的 id，否则返回-1。

**实施:**

## C++

```
// C++ program to find celebrity
#include <bits/stdc++.h>
#include <list>
using namespace std;

// Max # of persons in the party
#define N 8

// Person with 2 is celebrity
bool MATRIX[N][N] = {{0, 0, 1, 0},
                    {0, 0, 1, 0},
                    {0, 0, 0, 0},
                    {0, 0, 1, 0}};

bool knows(int a, int b)
{
    return MATRIX[a][b];
}

// Returns -1 if celebrity
// is not present. If present,
// returns id (value from 0 to n-1).
int findCelebrity(int n)
{
    // Handle trivial
    // case of size = 2
    stack<int> s;

    // Celebrity
    int C;

    // Push everybody to stack
    for (int i = 0; i < n; i++)
        s.push(i);

    // Extract top 2

    // Find a potential celebrity
    while (s.size() > 1)
    {   int A = s.top();
        s.pop();
        int B = s.top();
        s.pop();
        if (knows(A, B))
        {
          s.push(B);
        }
        else
        {
          s.push(A);
        }
    }
    // If there are only two people
    // and there is no
    // potential candicate
    if(s.empty())
        return -1;

    // Potential candidate?
    C = s.top();
    s.pop();

    // Check if C is actually
    // a celebrity or not
    for (int i = 0; i < n; i++)
    {
        // If any person doesn't
        // know 'C' or 'C' doesn't
        // know any person, return -1
        if ( (i != C) &&
                (knows(C, i) ||
                 !knows(i, C)) )
            return -1;
    }

    return C;
}

// Driver code
int main()
{
    int n = 4;
    int id = findCelebrity(n);
    id == -1 ? cout << "No celebrity" :
               cout << "Celebrity ID " << id;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find celebrity using
// stack data structure
import java.util.Stack;

class GFG
{
    // Person with 2 is celebrity
    static int MATRIX[][] = { { 0, 0, 1, 0 },
                            { 0, 0, 1, 0 },
                            { 0, 0, 0, 0 },
                            { 0, 0, 1, 0 } };

    // Returns true if a knows
    // b, false otherwise
    static boolean knows(int a, int b)
    {
        boolean res = (MATRIX[a][b] == 1) ?
                                     true :
                                     false;
        return res;
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    static int findCelebrity(int n)
    {
        Stack<Integer> st = new Stack<>();
        int c;

        // Step 1 :Push everybody
        // onto stack
        for (int i = 0; i < n; i++)
        {
            st.push(i);
        }

        while (st.size() > 1)
        {
            // Step 2 :Pop off top
            // two persons from the
            // stack, discard one
            // person based on return
            // status of knows(A, B).
            int a = st.pop();
            int b = st.pop();

            // Step 3 : Push the
            // remained person onto stack.
            if (knows(a, b))
            {
                st.push(b);
            }

            else
                st.push(a);
        }

        // If there are only two people
        // and there is no
        // potential candicate
        if(st.empty())
            return -1;

        c = st.pop();

        // Step 5 : Check if the last
        // person is celebrity or not
        for (int i = 0; i < n; i++)
        {
            // If any person doesn't
            //  know 'c' or 'a' doesn't
            // know any person, return -1
            if (i != c && (knows(c, i) ||
                          !knows(i, c)))
                return -1;
        }
        return c;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        int result = findCelebrity(n);
        if (result == -1)
        {
            System.out.println("No Celebrity");
        }
        else
            System.out.println("Celebrity ID " +
                                        result);
    }
}

// This code is contributed
// by Rishabh Mahrsee
```

## 蟒蛇 3

```
# Python3 program to find celebrity
# using stack data structure

# Max # of persons in the party
N = 8

# Person with 2 is celebrity
MATRIX = [ [ 0, 0, 1, 0 ],
           [ 0, 0, 1, 0 ],
           [ 0, 0, 0, 0 ],
           [ 0, 0, 1, 0 ] ]

def knows(a, b):

    return MATRIX[a][b]

# Returns -1 if celebrity
# is not present. If present,
# returns id (value from 0 to n-1).
def findCelebrity(n):

    # Handle trivial
    # case of size = 2
    s = []

    # Push everybody to stack
    for i in range(n):
        s.append(i)

    # Extract top 2
    A = s.pop()
    B = s.pop()

    # Find a potential celebrity
    while (len(s) > 1):
        if (knows(A, B)):
            A = s.pop()
        else:
            B = s.pop()

    # If there are only two people
    # and there is no
    # potential candicate
    if(len(s) == 0):
        return -1

    # Potential candidate?
    C = s.pop();

    # Last candidate was not
    # examined, it leads one
    # excess comparison (optimize)
    if (knows(C, B)):
        C = B

    if (knows(C, A)):
        C = A

    # Check if C is actually
    # a celebrity or not
    for i in range(n):

        # If any person doesn't
        # know 'a' or 'a' doesn't
        # know any person, return -1
        if ((i != C) and
           (knows(C, i) or
           not(knows(i, C)))):
            return -1

    return C

# Driver code
if __name__ == '__main__':

    n = 4
    id_ = findCelebrity(n)

    if id_ == -1:
        print("No celebrity")
    else:
      print("Celebrity ID ", id_)

# This code is contributed by UnworthyProgrammer
```

## C#

```
// C# program to find celebrity using
// stack data structure
using System;
using System.Collections.Generic;

public class GFG
{
    // Person with 2 is celebrity
    static int [,]MATRIX = { { 0, 0, 1, 0 },
                            { 0, 0, 1, 0 },
                            { 0, 0, 0, 0 },
                            { 0, 0, 1, 0 } };

    // Returns true if a knows
    // b, false otherwise
    static bool knows(int a, int b)
    {
        bool res = (MATRIX[a,b] == 1) ?
                                     true :
                                     false;
        return res;
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    static int findCelebrity(int n)
    {
        Stack<int> st = new Stack<int>();
        int c;

        // Step 1 :Push everybody
        // onto stack
        for (int i = 0; i < n; i++)
        {
            st.Push(i);
        }

        while (st.Count > 1)
        {
            // Step 2 :Pop off top
            // two persons from the
            // stack, discard one
            // person based on return
            // status of knows(A, B).
            int a = st.Pop();
            int b = st.Pop();

            // Step 3 : Push the
            // remained person onto stack.
            if (knows(a, b))
            {
                st.Push(b);
            }

            else
                st.Push(a);
        }

        // If there are only two people
        // and there is no
        // potential candicate
        if(st.Count==0)
            return -1;

        c = st.Pop();

        // Step 5 : Check if the last
        // person is celebrity or not
        for (int i = 0; i < n; i++)
        {
            // If any person doesn't
            //  know 'c' or 'a' doesn't
            // know any person, return -1
            if (i != c && (knows(c, i) ||
                          !knows(i, c)))
                return -1;
        }
        return c;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;
        int result = findCelebrity(n);
        if (result == -1)
        {
            Console.WriteLine("No Celebrity");
        }
        else
            Console.WriteLine("Celebrity ID " +
                                        result);
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript program to find celebrity using
// stack data structure
    // Person with 2 is celebrity
    var MATRIX = [ [ 0, 0, 1, 0 ],
    [ 0, 0, 1, 0 ],
    [ 0, 0, 0, 0 ],
    [ 0, 0, 1, 0 ] ];

    // Returns true if a knows
    // b, false otherwise
    function knows(a , b) {
        var res = (MATRIX[a][b] == 1) ? true : false;
        return res;
    }

    // Returns -1 if celebrity
    // is not present. If present,
    // returns id (value from 0 to n-1).
    function findCelebrity(n) {
        var st = new Array();
        var c;

        // Step 1 :Push everybody
        // onto stack
        for (var i = 0; i < n; i++) {
            st.push(i);
        }

        while (st.length > 1)
        {

            // Step 2 :Pop off top
            // two persons from the
            // stack, discard one
            // person based on return
            // status of knows(A, B).
            var a = st.pop();
            var b = st.pop();

            // Step 3 : Push the
            // remained person onto stack.
            if (knows(a, b)) {
                st.push(b);
            }

            else
                st.push(a);
        }

        // If there are only two people
        // and there is no
        // potential candicate
        if (st.length==0)
            return -1;

        c = st.pop();

        // Step 5 : Check if the last
        // person is celebrity or not
        for (i = 0; i < n; i++)
        {

            // If any person doesn't
            // know 'c' or 'a' doesn't
            // know any person, return -1
            if (i != c && (knows(c, i) || !knows(i, c)))
                return -1;
        }
        return c;
    }

    // Driver Code   
        var n = 4;
        var result = findCelebrity(n);
        if (result == -1) {
            document.write("No Celebrity");
        } else
            document.write("Celebrity ID " + result);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Celebrity ID 2
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    比较总数为 3(N-1)，所以时间复杂度为 O(n)。
*   **空间复杂度:** O(n)。
    需要 n 个额外空间来存储堆栈。

**最优方法:**思路是用两个指针，一个从开始，一个从结束。假设开始的人是 A，结束的人是 B，如果 A 认识 B，那么 A 一定不是名人。否则，B 一定不是名人。在循环结束时，只有一个索引将作为名人留下。把每个人都检查一遍，看看这是不是名人。
可以使用**双指针方法**，其中可以分配两个指针，一个在开始，另一个在结束，并且可以比较元素并减少搜索空间。

**算法:**

1.  创建两个索引 I 和 j，其中 i = 0，j = n-1
2.  运行一个循环，直到我小于 j。
3.  如果我认识 j，我就不能成为名人。所以增量 I，也就是 i++
4.  否则 j 不能成为名人，所以减量 j，即 j–
5.  指定我为名人候选人
6.  现在，通过重新运行从 0 到 n-1 的循环，并不断检查候选人是否认识某个人或是否有候选人不认识该候选人，最后检查候选人是否真的是名人，然后我们应该返回-1。否则在循环的最后，我们可以确定候选人实际上是一个名人。

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find celebrity
// in the given Matrix of people
// Code by Sparsh_cbs

import java.io.*;

class GFG {
    public static void main(String[] args)
    {
        int[][] M = { { 0, 0, 1, 0 },
                      { 0, 0, 1, 0 },
                      { 0, 0, 0, 0 },
                      { 0, 0, 1, 0 } };

        int celebIdx = celebrity(M, 4);

        if (celebIdx == -1)
            System.out.println("No celebrity found!");
        else {
            System.out.println(
                "0-based celebrity index is : " + celebIdx);
        }
    }
    public static int celebrity(int M[][], int n)
    {
        // This function returns the celebrity
        // index 0-based (if any)

        int i = 0, j = n - 1;
        while (i < j) {
            if (M[j][i] == 1) // j knows i
                j--;
            else // j doesnt know i so i cant be celebrity
                i++;
        }
        // i points to our celebrity candidate
        int candidate = i;

        // Now, all that is left is to check that whether
        // the candidate is actually a celebrity i.e: he is
        // known by everyone but he knows no one
        for (i = 0; i < n; i++) {
            if (i != candidate) {
                if (M[i][candidate] == 0
                    || M[candidate][i] == 1)
                    return -1;
            }
        }
        // if we reach here this means that the candidate
        // is really a celebrity
        return candidate;
    }
}
```

## 蟒蛇 3

```
# Python3 code
class Solution:

    # Function to find if there is a celebrity in the party or not.
    # return index if celebrity else return -1
    def celebrity(self, M, n):
        # code here
        i = 0
        j = n-1
        candidate = -1
        while(i < j):
            if M[j][i] == 1:
                j -= 1
            else:
                i += 1

        candidate = i
        for k in range(n):
            if candidate != k:
                if M[candidate][k] == 1 or M[k][candidate] == 0:
                    return -1

        return candidate

n = 4
m = [[0, 0, 1, 0],
     [0, 0, 1, 0],
     [0, 0, 0, 0],
     [0, 0, 1, 0]]
ob = Solution()
print("Celebrity at index "+str(ob.celebrity(m, n)))
```

## C#

```
// C# program to find celebrity
// in the given Matrix of people
// Code by Sparsh_cbs
using System;

class GFG {
    public static void Main(String[] args)
    {
        int[,] M = { { 0, 0, 1, 0 },
                      { 0, 0, 1, 0 },
                      { 0, 0, 0, 0 },
                      { 0, 0, 1, 0 } };

        int celebIdx = celebrity(M, 4);

        if (celebIdx == -1)
            Console.Write("No celebrity found!");
        else {
            Console.Write(
                "0-based celebrity index is : " + celebIdx);
        }
    }
    public static int celebrity(int [,]M, int n)
    {
        // This function returns the celebrity
        // index 0-based (if any)

        int i = 0, j = n - 1;
        while (i < j) {
            if (M[j,i] == 1) // j knows i
                j--;
            else // i knows j
                i++;
        }

        // i points to our celebrity candidate
        int candidate = i;

        // Now, all that is left is to check that whether
        // the candidate is actually a celebrity i.e: he is
        // known by everyone but he knows no one
        for (i = 0; i < n; i++) {
            if (i != candidate) {
                if (M[i,candidate] == 0
                    || M[candidate,i] == 1)
                    return -1;
            }
        }

        // if we reach here this means that the candidate
        // is really a celebrity
        return candidate;
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program to find celebrity
// in the given Matrix of people
// Code by Sparsh_cbs
var M = [ [ 0, 0, 1, 0 ],
                      [ 0, 0, 1, 0 ],
                      [ 0, 0, 0, 0 ],
                      [ 0, 0, 1, 0 ] ];

        var celebIdx = celebrity(M, 4);

        if (celebIdx == -1)
            document.write("No celebrity found!");
        else {
            document.write(
                "0-based celebrity index is : " + celebIdx);
        }

function celebrity( M, n)
    {

        // This function returns the celebrity
        // index 0-based (if any)
        var i = 0, j = n - 1;
        while (i < j) {
            if (M[j][i] == 1) // j knows i
                j--;
            else // i knows j
                i++;
        }

        // i points to our celebrity candidate
        var candidate = i;

        // Now, all that is left is to check that whether
        // the candidate is actually a celebrity i.e: he is
        // known by everyone but he knows no one
        for (i = 0; i < n; i++) {
            if (i != candidate) {
                if (M[i][candidate] == 0
                    || M[candidate][i] == 1)
                    return -1;
            }
        }

        // if we reach here this means that the candidate
        // is really a celebrity
        return candidate;
  } 

 // This code is contributed by shivanisinghss2110
</script>
```

## C++

```
// C++ program to find celebrity
// in the given Matrix of people
#include<bits/stdc++.h>
using namespace std;
#define N 4
  int celebrity(int M[N][N], int n)
    {
        // This function returns the celebrity
        // index 0-based (if any)

        int i = 0, j = n - 1;
        while (i < j) {
            if (M[j][i] == 1) // j knows i
                j--;
            else // j doesnt know i so i cant be celebrity
                i++;
        }
        // i points to our celebrity candidate
        int candidate = i;

        // Now, all that is left is to check that whether
        // the candidate is actually a celebrity i.e: he is
        // known by everyone but he knows no one
        for (i = 0; i < n; i++) {
            if (i != candidate) {
                if (M[i][candidate] == 0
                    || M[candidate][i] == 1)
                    return -1;
            }
        }
        // if we reach here this means that the candidate
        // is really a celebrity
        return candidate;

}

int main()
    {
        int M[N][N] = { { 0, 0, 1, 0 },
                      { 0, 0, 1, 0 },
                      { 0, 0, 0, 0 },
                      { 0, 0, 1, 0 } };

        int celebIdx = celebrity(M, 4);

        if (celebIdx == -1)
            cout<<("No celebrity found!");
        else {
            cout<<
                "0-based celebrity index is : " << celebIdx;
        }
        return 0;
    }

// This code contributed by gauravrajput1
```

**输出:**

```
0-based celebrity index is : 2
```

**复杂度分析:**

*   **时间复杂度:** O(n)
*   **空间复杂度:** O(1)不需要额外空间。

1.  写代码找名人。不要使用任何数据结构，如图形、堆栈等……您只能访问 *N* 和*具有质量(int，int)* 。
2.  使用队列实现算法。你的观察是什么？将您的解决方案与[在数组中查找最大值和最小值](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)和[锦标赛树](https://www.geeksforgeeks.org/tournament-tree-and-binary-heap/)进行比较。我们需要的最少比较次数是多少(打给*的最佳电话数是多少？*