# 查询用等长数组替换子数组，对于任何数组元素最多允许 P 个替换

> 原文:[https://www . geeksforgeeks . org/query-用最多 p 个替换的等长数组替换子数组-允许任何数组元素/](https://www.geeksforgeeks.org/queries-to-replace-subarrays-by-equal-length-arrays-with-at-most-p-replacements-allowed-for-any-array-element/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，整数 **P** 和由以下类型的查询组成的 2D 数组 **Q[][]** :

*   **1 L R B[R–L+1]:**此查询的任务是将子阵列 **{arr[L]，… arr[R]** 替换为数组 **B[]** b，假设任何数组元素最多可以替换 **P** 次。
*   **2 X:** 该查询的任务是打印**arr【X】**。

**示例:**

> **输入:** arr[] = {3，10，4，2，8，7}，P = 1，Q[][] = {{1，0，3，3，2，1，11}，{2，3，5，7}，{2，2 } }
> T3】输出:11
> T6】解释:
> 查询 1:将子数组{arr[0]，…，arr[3]}替换为数组{ T0
> 查询 3:由于 P = 1，因此子数组{arr[2]，…，arr[3]}不能被替换多次。
> 查询 4:打印 arr[2]。
> 
> **输入:** arr[] = {1，2，3，4，5}，P = 2，Q[][] = {{2，0}，{1，1，3，6，7，8}，{1，3，4，10，12}，{2，4}}
> **输出:** 1 12

**方法:**问题可以使用[联合-查找](https://www.geeksforgeeks.org/union-find/)算法解决。思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** ，检查 **Q[0]** 是否等于 **1** 。如果发现为真，则用新阵列替换子阵列，并且每当任何阵列元素被替换 P 次时，则使用[联合-查找](https://www.geeksforgeeks.org/union-find/)创建新子集。按照以下步骤解决问题:

*   初始化一个数组，比如**访问了[]** ，其中**访问了【I】**检查索引 **i** 是否存在于任何不相交的子集中。
*   初始化一个数组，比如 **count[]** ，其中**count【I】**存储**arr【I】**被替换的次数。
*   初始化一个数组，比如说**最后一个[]** ，来存储每个不相交子集的最大元素。
*   初始化一个数组，比如**父[]** ，来存储每个不相交子集的最小元素。
*   遍历 **Q[][]** 数组，对于每个查询，检查 **Q[i][0] == 1** 是否存在。如果发现为真，则执行以下操作:
    *   使用变量**低**迭代范围**【Q[I][1]、Q[I][2]】**，检查**访问的【低】**是否为真。如果发现为真，则找到存在**低**的子集的父元素，找到该子集中存在的最大元素。
    *   否则，检查**计数【低】**是否小于 **P** 。如果发现为真，则用相应的值替换 **arr【低】**的值。
    *   否则，检查**计数【低】**是否等于 **P** 。如果发现为真，则创建当前索引的新的不相交子集。
*   否则，打印**arr[Q[I][1]]**。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // visited[i]: Check index i is present
    // in any disjoint subset or not.
    static boolean[] visited;

    // Store the smallest element
    // of each disjoint subset
    static int[] parent;

    // count[i]: Stores the count
    // of replacements of arr[i]
    static int[] last;

    // Store the largest element
    // of each disjoint subset
    static int[] count;

    // Function to process all the given Queries
    static void processQueries(int[] arr, int P,
                               List<List<Integer> > Q)
    {
        // Traverse the queries[][] array
        for (int i = 0; i < Q.size(); i++) {

            // Stores the current query
            List<Integer> query = Q.get(i);

            // If query of type is 1
            if (query.get(0) == 1) {

                // Perform the query of type 1
                processTypeOneQuery(query, arr, P);
            }

            // If query of type is 2
            else {

                // Stores 2nd element of
                // current query
                int index = query.get(1);

                // Print arr[index]
                System.out.println(arr[index]);
            }
        }
    }

    // Function to perform the query of type 1
    static void processTypeOneQuery(
        List<Integer> query, int[] arr, int P)
    {
        // Stores the value of L
        int low = query.get(1);

        // Stores the value of R
        int high = query.get(2);

        // Stores leftmost index of the
        // subarray for which a new
        // subset can be generated
        int left = -1;

        // Stores index of
        // the query[] array
        int j = 3;

        // Iterate over the
        // range [low, high]
        while (low <= high) {

            // If low is present in
            // any of the subset
            if (visited[low]) {

                // If no subset created for
                // the subarray arr[left...low - 1]
                if (left != -1) {

                    // Create a new subset
                    newUnion(left, low - 1,
                             arr.length);

                    // Update left
                    left = -1;
                }

                // Stores next index to be
                // processed
                int jump = findJumpLength(low);

                // Update low
                low += jump;

                // Update j
                j += jump;
            }

            // If arr[low] has been
            // already replaced P times
            else if (count[low] == P) {

                // If already subset
                // created for left
                if (left == -1) {

                    // Update left
                    left = low;
                }

                // Mark low as an element
                // of any subset
                visited[low] = true;

                // Update low
                low++;

                // Update j
                j++;
            }

            // If arr[low] has been replaced
            // less than P times
            else {

                // If no subset created for
                // the subarray arr[left...low - 1]
                if (left != -1) {

                    // Create a new subset
                    newUnion(left, low - 1, arr.length);

                    // Update left
                    left = -1;
                }

                // Replace arr[low] with
                // the corresponding value
                arr[low] = query.get(j);

                // Update count[low]
                count[low]++;

                // Update low
                low++;

                // Update j
                j++;
            }
        }

        // If no subset has been created for
        // the subarray arr[left...low - 1]
        if (left != -1) {

            // Create a new subset
            newUnion(left, high, arr.length);
        }
    }

    // Function to find the next index
    // to be processed after visiting low
    static int findJumpLength(int low)
    {

        // Stores smallest index of
        // the subset where low present
        int p = findParent(low);

        // Stores next index
        // to be processed
        int nextIndex = last[p] + 1;

        // Stores difference between
        // low and nextIndex
        int jump = (nextIndex - low);

        // Return jump
        return jump;
    }

    // Function to create a new subset
    static void newUnion(int low, int high,
                         int N)
    {

        // Iterate over
        // the range [low + 1, high]
        for (int i = low + 1; i <= high;
             i++) {

            // Perform union operation
            // on low
            union(low, i);
        }

        // If just smaller element of low
        // is present in any of the subset
        if (low > 0 && visited[low - 1]) {

            // Perform union on (low - 1)
            union(low - 1, low);
        }

        // If just greater element of high
        // is present in any of the subset
        if (high < N - 1 && visited[high + 1]) {

            // Perform union on high
            union(high, high + 1);
        }
    }

    // Function to find the smallest
    // element of the subset
    static int findParent(int u)
    {

        // Base Case
        if (parent[u] == u)
            return u;

        // Stores smallest element
        // of parent[u
        return parent[u]
            = findParent(parent[u]);
    }

    // Function to perform union operation
    static void union(int u, int v)
    {
        // Stores smallest element
        // of subset containing u
        int p1 = findParent(u);

        // Stores smallest element
        // of subset containing u
        int p2 = findParent(v);

        // Update parent[p2]
        parent[p2] = p1;

        // Update last[p1]
        last[p1] = last[p2];
    }

    // Function to find all the queries
    static List<List<Integer> > getQueries()
    {

        // Stores all the queries
        List<List<Integer> > Q
            = new ArrayList<List<Integer> >();

        // Initialize all queries
        Integer[] query1 = { 1, 0, 3, 3, 2,
                             1, 11 };
        Integer[] query2 = { 2, 3 };
        Integer[] query3 = { 1, 2, 3, 5, 7 };
        Integer[] query4 = { 2, 2 };

        // Insert all queries
        Q.add(Arrays.asList(query1));
        Q.add(Arrays.asList(query2));
        Q.add(Arrays.asList(query3));
        Q.add(Arrays.asList(query4));

        // Return all queries
        return Q;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 3, 10, 4, 2, 8, 7 };
        int N = arr.length;
        int P = 1;

        parent = new int[N];
        last = new int[N];
        count = new int[N];
        visited = new boolean[N];

        // Initialize parent[] and
        // last[] array
        for (int i = 0; i < parent.length;
             i++) {

            // Update parent[i]
            parent[i] = i;

            // Update last[i]
            last[i] = i;
        }

        List<List<Integer> > Q = getQueries();
        processQueries(arr, P, Q);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# visited[i]: Check index i is present
# in any disjoint subset or not.
visited = []

# Store the smallest element
# of each disjoint subset
parent = []

# count[i]: Stores the count
# of replacements of arr[i]
last = []

# Store the largest element
# of each disjoint subset
count = []

# Function to process all the given Queries
def processQueries(arr, P, Q):

    # Traverse the [,]queries array
    for i in range(len(Q)):

        # Stores the current query
        query = Q[i];

        # If query of type is 1
        if (query[0] == 1):

            # Perform the query of type 1
            processTypeOneQuery(query, arr, P);

        # If query of type is 2
        else:

            # Stores 2nd element of
            # current query
            index = query[1];

            # Print arr[index]
            print(arr[index]);

# Function to perform the query of type 1
def processTypeOneQuery(query, arr, P):

    # Stores the value of L
    low = query[1];

    # Stores the value of R
    high = query[2];

    # Stores leftmost index of the
    # subarray for which a new
    # subset can be generated
    left = -1;

    # Stores index of
    # the query[] array
    j = 3;

    # Iterate over the
    # range [low, high]
    while (low <= high):

        # If low is present in
        # any of the subset
        if (visited[low]):

            # If no subset created for
            # the subarray arr[left...low - 1]
            if (left != -1):

                # Create a new subset
                newUnion(left, low - 1,len(arr));

                # Update left
                left = -1;

            # Stores next index to be
            # processed
            jump = findJumpLength(low);

            # Update low
            low += jump;

            # Update j
            j += jump;

        # If arr[low] has been
        # already replaced P times
        elif (count[low] == P):

            # If already subset
            # created for left
            if (left == -1):

                # Update left
                left = low;

            # Mark low as an element
            # of any subset
            visited[low] = True;

            # Update low
            low += 1

            # Update j
            j += 1

        # If arr[low] has been replaced
        # less than P times
        else:

            # If no subset created for
            # the subarray arr[left...low - 1]
            if (left != -1):

                # Create a new subset
                newUnion(left, low - 1, len(arr));

                # Update left
                left = -1;

            # Replace arr[low] with
            # the corresponding value
            arr[low] = query[j];

            # Update count[low]
            count[low] += 1

            # Update low
            low += 1

            # Update j
            j += 1

    # If no subset has been created for
    # the subarray arr[left...low - 1]
    if (left != -1):

        # Create a new subset
        newUnion(left, high, len(arr));

# Function to find the next index
# to be processed after visiting low
def findJumpLength(low):

    # Stores smallest index of
    # the subset where low present
    p = findParent(low);

    # Stores next index
    # to be processed
    nextIndex = last[p] + 1;

    # Stores difference between
    # low and nextIndex
    jump = (nextIndex - low);

    # Return jump
    return jump;

# Function to create a new subset
def newUnion(low, high,N):

    # Iterate over
    # the range [low + 1, high]
    for i in range(low+1,high+1):

        # Perform union operation
        # on low
        union(low, i);

    # If just smaller element of low
    # is present in any of the subset
    if (low > 0 and visited[low - 1]):

        # Perform union on (low - 1)
        union(low - 1, low);

    # If just greater element of high
    # is present in any of the subset
    if (high < N - 1 and visited[high + 1]):

        # Perform union on high
        union(high, high + 1);

# Function to find the smallest
# element of the subset
def findParent(u):

    # Base Case
    if (parent[u] == u):
        return u;

    # Stores smallest element
    # of parent[u
    parent[u]= findParent(parent[u]);
    return parent[u]

# Function to perform union operation
def union(u, v):

    # Stores smallest element
    # of subset containing u
    p1 = findParent(u);

    # Stores smallest element
    # of subset containing u
    p2 = findParent(v);

    # Update parent[p2]
    parent[p2] = p1;

    # Update last[p1]
    last[p1] = last[p2];

# Function to find all the queries
def getQueries():

    # Stores all the queries
    Q = []

    # Initialize all queries
    query1 = [ 1, 0, 3, 3, 2,1, 11 ]
    query2 = [ 2, 3 ]
    query3 = [ 1, 2, 3, 5, 7 ]
    query4 = [ 2, 2 ]

    # Insert all queries        
    Q.append(query1)
    Q.append(query2)
    Q.append(query3)
    Q.append(query4)

    # Return all queries
    return Q;

# Driver Code
if __name__=='__main__':

    arr = [ 3, 10, 4, 2, 8, 7 ]
    N = len(arr)
    P = 1;
    parent = [i for i in range(N)]
    last = [i for i in range(N)]
    count = [0 for i in range(N)]
    visited = [False for i in range(N)]

    Q = getQueries();
    processQueries(arr, P, Q);

    # This code is contributed by rutvik_56.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // visited[i]: Check index i is present
    // in any disjoint subset or not.
    static bool[] visited;

    // Store the smallest element
    // of each disjoint subset
    static int[] parent;

    // count[i]: Stores the count
    // of replacements of arr[i]
    static int[] last;

    // Store the largest element
    // of each disjoint subset
    static int[] count;

    // Function to process all the given Queries
    static void processQueries(int[] arr, int P,
                               List<List<int> > Q)
    {

        // Traverse the [,]queries array
        for (int i = 0; i < Q.Count; i++) {

            // Stores the current query
            List<int> query = Q[i];

            // If query of type is 1
            if (query[0] == 1) {

                // Perform the query of type 1
                processTypeOneQuery(query, arr, P);
            }

            // If query of type is 2
            else {

                // Stores 2nd element of
                // current query
                int index = query[1];

                // Print arr[index]
                Console.WriteLine(arr[index]);
            }
        }
    }

    // Function to perform the query of type 1
    static void processTypeOneQuery(
        List<int> query, int[] arr, int P)
    {
        // Stores the value of L
        int low = query[1];

        // Stores the value of R
        int high = query[2];

        // Stores leftmost index of the
        // subarray for which a new
        // subset can be generated
        int left = -1;

        // Stores index of
        // the query[] array
        int j = 3;

        // Iterate over the
        // range [low, high]
        while (low <= high) {

            // If low is present in
            // any of the subset
            if (visited[low]) {

                // If no subset created for
                // the subarray arr[left...low - 1]
                if (left != -1) {

                    // Create a new subset
                    newUnion(left, low - 1,
                             arr.Length);

                    // Update left
                    left = -1;
                }

                // Stores next index to be
                // processed
                int jump = findJumpLength(low);

                // Update low
                low += jump;

                // Update j
                j += jump;
            }

            // If arr[low] has been
            // already replaced P times
            else if (count[low] == P) {

                // If already subset
                // created for left
                if (left == -1) {

                    // Update left
                    left = low;
                }

                // Mark low as an element
                // of any subset
                visited[low] = true;

                // Update low
                low++;

                // Update j
                j++;
            }

            // If arr[low] has been replaced
            // less than P times
            else {

                // If no subset created for
                // the subarray arr[left...low - 1]
                if (left != -1) {

                    // Create a new subset
                    newUnion(left, low - 1, arr.Length);

                    // Update left
                    left = -1;
                }

                // Replace arr[low] with
                // the corresponding value
                arr[low] = query[j];

                // Update count[low]
                count[low]++;

                // Update low
                low++;

                // Update j
                j++;
            }
        }

        // If no subset has been created for
        // the subarray arr[left...low - 1]
        if (left != -1) {

            // Create a new subset
            newUnion(left, high, arr.Length);
        }
    }

    // Function to find the next index
    // to be processed after visiting low
    static int findJumpLength(int low)
    {

        // Stores smallest index of
        // the subset where low present
        int p = findParent(low);

        // Stores next index
        // to be processed
        int nextIndex = last[p] + 1;

        // Stores difference between
        // low and nextIndex
        int jump = (nextIndex - low);

        // Return jump
        return jump;
    }

    // Function to create a new subset
    static void newUnion(int low, int high,
                         int N)
    {

        // Iterate over
        // the range [low + 1, high]
        for (int i = low + 1; i <= high;
             i++) {

            // Perform union operation
            // on low
            union(low, i);
        }

        // If just smaller element of low
        // is present in any of the subset
        if (low > 0 && visited[low - 1]) {

            // Perform union on (low - 1)
            union(low - 1, low);
        }

        // If just greater element of high
        // is present in any of the subset
        if (high < N - 1 && visited[high + 1]) {

            // Perform union on high
            union(high, high + 1);
        }
    }

    // Function to find the smallest
    // element of the subset
    static int findParent(int u)
    {

        // Base Case
        if (parent[u] == u)
            return u;

        // Stores smallest element
        // of parent[u
        return parent[u]
            = findParent(parent[u]);
    }

    // Function to perform union operation
    static void union(int u, int v)
    {
        // Stores smallest element
        // of subset containing u
        int p1 = findParent(u);

        // Stores smallest element
        // of subset containing u
        int p2 = findParent(v);

        // Update parent[p2]
        parent[p2] = p1;

        // Update last[p1]
        last[p1] = last[p2];
    }

    // Function to find all the queries
    static List<List<int> > getQueries()
    {

        // Stores all the queries
        List<List<int> > Q
            = new List<List<int> >();

        // Initialize all queries
        int[] query1 = { 1, 0, 3, 3, 2,
                             1, 11 };
        int[] query2 = { 2, 3 };
        int[] query3 = { 1, 2, 3, 5, 7 };
        int[] query4 = { 2, 2 };

        // Insert all queries        
        Q.Add(new List<int>(query1));
        Q.Add(new List<int>(query2));
        Q.Add(new List<int>(query3));
        Q.Add(new List<int>(query4));

        // Return all queries
        return Q;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        int[] arr = { 3, 10, 4, 2, 8, 7 };
        int N = arr.Length;
        int P = 1;

        parent = new int[N];
        last = new int[N];
        count = new int[N];
        visited = new bool[N];

        // Initialize parent[] and
        // last[] array
        for (int i = 0; i < parent.Length;
             i++) {

            // Update parent[i]
            parent[i] = i;

            // Update last[i]
            last[i] = i;
        }

        List<List<int> > Q = getQueries();
        processQueries(arr, P, Q);
    }
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
11
1
```

***时间复杂度:**O(N+| Q | * P)*
T5**辅助空间:** O(N)