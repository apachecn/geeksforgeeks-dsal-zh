# 范围 LCM 查询

> 原文： [https://www.geeksforgeeks.org/range-lcm-queries/](https://www.geeksforgeeks.org/range-lcm-queries/)

给定一个整数数组，请评估形式为`LCM(l, r)`的查询。 可能有很多查询，因此可以有效地评估查询。

```
LCM (l, r) denotes the LCM of array elements
           that lie between the index l and r
           (inclusive of both indices) 

Mathematically, 
LCM(l, r) = LCM(arr[l],  arr[l+1] , ......... ,
                                  arr[r-1], arr[r])

```

**示例**：

```
Inputs : Array = {5, 7, 5, 2, 10, 12 ,11, 17, 14, 1, 44}
         Queries: LCM(2, 5), LCM(5, 10), LCM(0, 10)
Outputs: 60 15708 78540
Explanation : In the first query LCM(5, 2, 10, 12) = 60, 
              similarly in other queries.

```



一个简单的解决方案是遍历每个查询的数组，并使用`LCM(a, b) = (a * b) / GCD(a, b)`计算答案。

但是，由于查询的数量可能很大，因此这种解决方案是不切实际的。

一种有效的解决方案是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。 回想一下，在这种情况下，不需要更新，我们可以构建一次树，然后可以重复使用它来回答查询。 树中的每个节点都应存储该特定段的 LCM 值，我们可以使用与上述相同的公式来组合这些段。 因此，我们可以有效地回答每个查询！

下面是相同的解决方案。

## C++

```
// LCM of given range queries using Segment Tree 
#include <bits/stdc++.h> 
using namespace std; 
  
#define MAX 1000 
  
// allocate space for tree 
int tree[4*MAX]; 
  
// declaring the array globally 
int arr[MAX]; 
  
// Function to return gcd of a and b 
int gcd(int a, int b) 
{ 
    if (a == 0) 
        return b; 
    return gcd(b%a, a); 
} 
  
//utility function to find lcm 
int lcm(int a, int b) 
{ 
    return a*b/gcd(a,b); 
} 
  
// Function to build the segment tree 
// Node starts beginning index of current subtree. 
// start and end are indexes in arr[] which is global 
void build(int node, int start, int end) 
{ 
    // If there is only one element in current subarray 
    if (start==end) 
    { 
        tree[node] = arr[start]; 
        return; 
    } 
  
    int mid = (start+end)/2; 
  
    // build left and right segments 
    build(2*node, start, mid); 
    build(2*node+1, mid+1, end); 
  
    // build the parent 
    int left_lcm = tree[2*node]; 
    int right_lcm = tree[2*node+1]; 
  
    tree[node] = lcm(left_lcm, right_lcm); 
} 
  
// Function to make queries for array range )l, r). 
// Node is index of root of current segment in segment 
// tree (Note that indexes in segment tree begin with 1 
// for simplicity). 
// start and end are indexes of subarray covered by root 
// of current segment. 
int query(int node, int start, int end, int l, int r) 
{ 
    // Completely outside the segment, returning 
    // 1 will not affect the lcm; 
    if (end<l || start>r) 
        return 1; 
  
    // completely inside the segment 
    if (l<=start && r>=end) 
        return tree[node]; 
  
    // partially inside 
    int mid = (start+end)/2; 
    int left_lcm = query(2*node, start, mid, l, r); 
    int right_lcm = query(2*node+1, mid+1, end, l, r); 
    return lcm(left_lcm, right_lcm); 
} 
  
//driver function to check the above program 
int main() 
{ 
    //initialize the array 
    arr[0] = 5; 
    arr[1] = 7; 
    arr[2] = 5; 
    arr[3] = 2; 
    arr[4] = 10; 
    arr[5] = 12; 
    arr[6] = 11; 
    arr[7] = 17; 
    arr[8] = 14; 
    arr[9] = 1; 
    arr[10] = 44; 
  
    // build the segment tree 
    build(1, 0, 10); 
  
    // Now we can answer each query efficiently 
  
    // Print LCM of (2, 5) 
    cout << query(1, 0, 10, 2, 5) << endl; 
  
    // Print LCM of (5, 10) 
    cout << query(1, 0, 10, 5, 10) << endl; 
  
    // Print LCM of (0, 10) 
    cout << query(1, 0, 10, 0, 10) << endl; 
  
    return 0; 
}
```

## Java

```
// LCM of given range queries  
// using Segment Tree  
  
class GFG  
{ 
  
    static final int MAX = 1000; 
  
    // allocate space for tree  
    static int tree[] = new int[4 * MAX]; 
  
    // declaring the array globally  
    static int arr[] = new int[MAX]; 
  
    // Function to return gcd of a and b  
    static int gcd(int a, int b) { 
        if (a == 0) { 
            return b; 
        } 
        return gcd(b % a, a); 
    } 
  
    // utility function to find lcm  
    static int lcm(int a, int b)  
    { 
        return a * b / gcd(a, b); 
    } 
  
    // Function to build the segment tree  
    // Node starts beginning index  
    // of current subtree. start and end 
    // are indexes in arr[] which is global  
    static void build(int node, int start, int end)  
    { 
          
        // If there is only one element 
        // in current subarray  
        if (start == end)  
        { 
            tree[node] = arr[start]; 
            return; 
        } 
  
        int mid = (start + end) / 2; 
  
        // build left and right segments  
        build(2 * node, start, mid); 
        build(2 * node + 1, mid + 1, end); 
  
        // build the parent  
        int left_lcm = tree[2 * node]; 
        int right_lcm = tree[2 * node + 1]; 
  
        tree[node] = lcm(left_lcm, right_lcm); 
    } 
  
    // Function to make queries for  
    // array range )l, r). Node is index 
    // of root of current segment in segment  
    // tree (Note that indexes in segment   
    // tree begin with 1 for simplicity).  
    // start and end are indexes of subarray  
    // covered by root of current segment.  
    static int query(int node, int start, 
                    int end, int l, int r)  
    { 
          
        // Completely outside the segment, returning  
        // 1 will not affect the lcm;  
        if (end < l || start > r)  
        { 
            return 1; 
        } 
  
        // completely inside the segment  
        if (l <= start && r >= end) 
        { 
            return tree[node]; 
        } 
  
        // partially inside  
        int mid = (start + end) / 2; 
        int left_lcm = query(2 * node, start, mid, l, r); 
        int right_lcm = query(2 * node + 1, mid + 1, end, l, r); 
        return lcm(left_lcm, right_lcm); 
    } 
  
    // Driver code 
    public static void main(String[] args)  
    { 
  
        //initialize the array  
        arr[0] = 5; 
        arr[1] = 7; 
        arr[2] = 5; 
        arr[3] = 2; 
        arr[4] = 10; 
        arr[5] = 12; 
        arr[6] = 11; 
        arr[7] = 17; 
        arr[8] = 14; 
        arr[9] = 1; 
        arr[10] = 44; 
  
        // build the segment tree  
        build(1, 0, 10); 
  
        // Now we can answer each query efficiently  
        // Print LCM of (2, 5)  
        System.out.println(query(1, 0, 10, 2, 5)); 
  
        // Print LCM of (5, 10)  
        System.out.println(query(1, 0, 10, 5, 10)); 
  
        // Print LCM of (0, 10)  
        System.out.println(query(1, 0, 10, 0, 10)); 
  
    } 
} 
  
// This code is contributed by 29AjayKumar
```

## Python3

```
# LCM of given range queries using Segment Tree 
MAX = 1000
  
# allocate space for tree 
tree = [0] * (4 * MAX) 
  
# declaring the array globally 
arr = [0] * MAX
  
# Function to return gcd of a and b 
def gcd(a: int, b: int): 
    if a == 0: 
        return b 
    return gcd(b % a, a) 
  
# utility function to find lcm 
def lcm(a: int, b: int): 
    return (a * b) // gcd(a, b) 
  
# Function to build the segment tree 
# Node starts beginning index of current subtree. 
# start and end are indexes in arr[] which is global 
def build(node: int, start: int, end: int): 
  
    # If there is only one element  
    # in current subarray 
    if start == end: 
        tree[node] = arr[start] 
        return
  
    mid = (start + end) // 2
  
    # build left and right segments 
    build(2 * node, start, mid) 
    build(2 * node + 1, mid + 1, end) 
  
    # build the parent 
    left_lcm = tree[2 * node] 
    right_lcm = tree[2 * node + 1] 
  
    tree[node] = lcm(left_lcm, right_lcm) 
  
# Function to make queries for array range )l, r). 
# Node is index of root of current segment in segment 
# tree (Note that indexes in segment tree begin with 1 
# for simplicity). 
# start and end are indexes of subarray covered by root 
# of current segment. 
def query(node: int, start: int,  
           end: int, l: int, r: int): 
  
    # Completely outside the segment,  
    # returning 1 will not affect the lcm; 
    if end < l or start > r: 
        return 1
  
    # completely inside the segment 
    if l <= start and r >= end: 
        return tree[node] 
  
    # partially inside 
    mid = (start + end) // 2
    left_lcm = query(2 * node, start, mid, l, r) 
    right_lcm = query(2 * node + 1,  
                      mid + 1, end, l, r) 
    return lcm(left_lcm, right_lcm) 
  
# Driver Code 
if __name__ == "__main__": 
  
    # initialize the array 
    arr[0] = 5
    arr[1] = 7
    arr[2] = 5
    arr[3] = 2
    arr[4] = 10
    arr[5] = 12
    arr[6] = 11
    arr[7] = 17
    arr[8] = 14
    arr[9] = 1
    arr[10] = 44
  
    # build the segment tree 
    build(1, 0, 10) 
  
    # Now we can answer each query efficiently 
  
    # Print LCM of (2, 5) 
    print(query(1, 0, 10, 2, 5)) 
  
    # Print LCM of (5, 10) 
    print(query(1, 0, 10, 5, 10)) 
  
    # Print LCM of (0, 10) 
    print(query(1, 0, 10, 0, 10)) 
  
# This code is contributed by 
# sanjeev2552
```

## C#

```
// LCM of given range queries  
// using Segment Tree  
using System; 
using System.Collections.Generic; 
  
class GFG  
{ 
    static readonly int MAX = 1000; 
  
    // allocate space for tree  
    static int []tree = new int[4 * MAX]; 
  
    // declaring the array globally  
    static int []arr = new int[MAX]; 
  
    // Function to return gcd of a and b  
    static int gcd(int a, int b)  
    { 
        if (a == 0)  
        { 
            return b; 
        } 
        return gcd(b % a, a); 
    } 
  
    // utility function to find lcm  
    static int lcm(int a, int b)  
    { 
        return a * b / gcd(a, b); 
    } 
  
    // Function to build the segment tree  
    // Node starts beginning index  
    // of current subtree. start and end 
    // are indexes in []arr which is global  
    static void build(int node, int start, int end)  
    { 
          
        // If there is only one element 
        // in current subarray  
        if (start == end)  
        { 
            tree[node] = arr[start]; 
            return; 
        } 
  
        int mid = (start + end) / 2; 
  
        // build left and right segments  
        build(2 * node, start, mid); 
        build(2 * node + 1, mid + 1, end); 
  
        // build the parent  
        int left_lcm = tree[2 * node]; 
        int right_lcm = tree[2 * node + 1]; 
  
        tree[node] = lcm(left_lcm, right_lcm); 
    } 
  
    // Function to make queries for  
    // array range )l, r). Node is index 
    // of root of current segment in segment  
    // tree (Note that indexes in segment  
    // tree begin with 1 for simplicity).  
    // start and end are indexes of subarray  
    // covered by root of current segment.  
    static int query(int node, int start, 
                     int end, int l, int r)  
    { 
          
        // Completely outside the segment,  
        // returning 1 will not affect the lcm;  
        if (end < l || start > r)  
        { 
            return 1; 
        } 
  
        // completely inside the segment  
        if (l <= start && r >= end) 
        { 
            return tree[node]; 
        } 
  
        // partially inside  
        int mid = (start + end) / 2; 
        int left_lcm = query(2 * node, start, mid, l, r); 
        int right_lcm = query(2 * node + 1,  
                              mid + 1, end, l, r); 
        return lcm(left_lcm, right_lcm); 
    } 
  
    // Driver code 
    public static void Main(String[] args)  
    { 
  
        // initialize the array  
        arr[0] = 5; 
        arr[1] = 7; 
        arr[2] = 5; 
        arr[3] = 2; 
        arr[4] = 10; 
        arr[5] = 12; 
        arr[6] = 11; 
        arr[7] = 17; 
        arr[8] = 14; 
        arr[9] = 1; 
        arr[10] = 44; 
  
        // build the segment tree  
        build(1, 0, 10); 
  
        // Now we can answer each query efficiently  
        // Print LCM of (2, 5)  
        Console.WriteLine(query(1, 0, 10, 2, 5)); 
  
        // Print LCM of (5, 10)  
        Console.WriteLine(query(1, 0, 10, 5, 10)); 
  
        // Print LCM of (0, 10)  
        Console.WriteLine(query(1, 0, 10, 0, 10)); 
    } 
} 
  
// This code is contributed by Rajput-Ji
```

输出：

```
60
15708
78540
```

