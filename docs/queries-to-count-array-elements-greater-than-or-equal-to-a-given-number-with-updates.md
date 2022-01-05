# 通过更新对大于或等于给定数量的数组元素进行计数的查询

> 原文:[https://www . geeksforgeeks . org/query-to-count-array-elements-大于或等于给定的数字-带更新/](https://www.geeksforgeeks.org/queries-to-count-array-elements-greater-than-or-equal-to-a-given-number-with-updates/)

给定两个大小分别为 **N** 和 **Q** 的数组**arr【】**和**query【】**和一个整数 **M** ，每个查询的任务是计算大于或等于**查询【I】**的数组元素的数量，并将所有这些数量减少 **M** ，并对更新后的数组执行其余查询。
**示例:**

> **输入:** arr[] = {1，2，3，4}，查询[] = {4，3，1}，M = 1
> **输出:** 1 2 4
> **解释:**
> 查询[0]:大于或等于**arr[**中的 **4** 的数组元素个数为 1，将数组减 M 将数组修改为{1，2，3，3}。
> 查询[1]:大于或等于 **arr[]** 中的 **3** 的数组元素个数为 2，将所有这些个数减 M 会将数组修改为{1，2，2，2}。
> 查询[2]:在**arr【】**中大于或等于 **1** 的数组元素个数为 4，将所有这些数字减 M 会将数组修改为{0，1，1，1}。
> 
> **输入:** arr[] = {1，2，3}，查询= {3，3}，M = 2
> **输出:** 1 0
> **解释:**
> 查询[0]:在 **arr[]** 中大于或等于的数组元素的计数为 1，将该数字减 M 会将数组修改为 arr[] = {1，2，1}。
> 查询[1]:在**arr【】**中大于等于 **3** 的数组元素个数为 0。所以数组保持不变。

**天真方法:**最简单的方法是对每个查询迭代整个数组，并检查当前数组元素是否大于或等于**查询【I】**。对于上述条件成立的元素，用 **M** 减去该元素并增加计数。最后打印每个查询的计数。
***时间复杂度:** O(Q * N)*
***辅助空间:** O(1)*

**高效方法:**使用[分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)可以解决问题。

1.  首先，[按照非递减顺序对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 进行排序。
2.  现在，找到元素的第一个位置，说 **l** ，其中包含一个元素**>= query【I】**。
3.  如果不存在这样的元素，那么该查询的答案将是 **0** 。否则答案将是**N–l**。
4.  最后将给定范围内的线段树 **l** 更新为**N–1**，并从给定范围内的所有元素中减去 **M** 。

> **图解:**
> 考虑以下例子:arr[] = {1，2，3，4}，query[] = {4，3，1}，M = 1
> 排序后 arr[] = {1，2，3，4}。
> 查询[0]: K = 4 和 arr[3] > = 4 so l = 3 和结果= 4–3 = 1 和更新的 arr[] = {1，2，3，3}
> 查询[1]: K = 3 和 arr[2] > =3 so l = 2 和结果= 4–2 = 2 和更新的 arr[] = {1，2，2，2}
> 查询[2]: K = 1 和 arr[0] > =1 so l = 0 和结果= 4–0 = 4

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to build a segment tree
void build(vector<int>& sum,
           vector<int>& a,
           int l, int r, int rt)
{
    // Check for base case
    if (l == r) {
        sum[rt] = a[l - 1];
        return;
    }

    // Find mid point
    int m = (l + r) >> 1;

    // Recursively build the
    // segment tree
    build(sum, a, l, m, rt << 1);
    build(sum, a, m + 1, r, rt << 1 | 1);
}

// Function for push down operation
// on the segment tree
void pushDown(vector<int>& sum,
              vector<int>& add,
              int rt, int ln, int rn)
{
    if (add[rt]) {
        add[rt << 1] += add[rt];
        add[rt << 1 | 1] += add[rt];
        sum[rt << 1] += add[rt] * ln;
        sum[rt << 1 | 1] += add[rt] * rn;
        add[rt] = 0;
    }
}

// Function to update the segment tree
void update(vector<int>& sum,
            vector<int>& add,
            int L, int R, int C, int l,
            int r, int rt)
{
    // Complete overlap
    if (L <= l && r <= R) {
        sum[rt] += C * (r - l + 1);
        add[rt] += C;
        return;
    }

    // Find mid
    int m = (l + r) >> 1;

    // Perform push down operation
    // on segment tree
    pushDown(sum, add, rt, m - l + 1,
             r - m);

    // Recursively update the segment tree
    if (L <= m)
        update(sum, add, L, R, C, l, m,
               rt << 1);

    if (R > m)
        update(sum, add, L, R, C, m + 1, r,
               rt << 1 | 1);
}

// Function to process the query
int query(vector<int>& sum,
          vector<int>& add,
          int L, int R, int l,
          int r, int rt)
{
    // Base case
    if (L <= l && r <= R) {
        return sum[rt];
    }

    // Find mid
    int m = (l + r) >> 1;

    // Perform push down operation
    // on segment tree
    pushDown(sum, add, rt, m - l + 1,
             r - m);

    int ans = 0;

    // Recursively calculate the result
    // of the query
    if (L <= m)
        ans += query(sum, add, L, R, l, m,
                     rt << 1);
    if (R > m)
        ans += query(sum, add, L, R, m + 1, r,
                     rt << 1 | 1);

    // Return the result
    return ans;
}

// Function to count the numbers
// which are greater than the given query
void sequenceMaintenance(int n, int q,
                         vector<int>& a,
                         vector<int>& b,
                         int m)
{
    // Sort the input array
    sort(a.begin(), a.end());

    // Create segment tree of size 4*n
    vector<int> sum, add, ans;
    sum.assign(n << 2, 0);
    add.assign(n << 2, 0);

    // Build the segment tree
    build(sum, a, 1, n, 1);

    // Iterate over the queries
    for (int i = 0; i < q; i++) {
        int l = 1, r = n, pos = -1;
        while (l <= r) {
            int m = (l + r) >> 1;
            if (query(sum, add, m, m, 1, n, 1)
                >= b[i]) {
                r = m - 1;
                pos = m;
            }
            else {
                l = m + 1;
            }
        }
        if (pos == -1)
            ans.push_back(0);
        else {
            // Store result in array
            ans.push_back(n - pos + 1);

            // Update the elements in
            // the given range
            update(sum, add, pos, n, -m,
                   1, n, 1);
        }
    }

    // Print the result of queries
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    int N = 4;
    int Q = 3;
    int M = 1;
    vector<int> arr = { 1, 2, 3, 4 };
    vector<int> query = { 4, 3, 1 };

    // Function Call
    sequenceMaintenance(N, Q, arr, query, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to build a segment tree
    static void build(Vector<Integer> sum,Vector<Integer> a,
                      int l, int r, int rt)
    {

        // Check for base case
        if(l == r)
        {
            sum.set(rt, a.get(l - 1));
            return;
        }

        // Find mid point
        int m = (l + r) >> 1;

        // Recursively build the
        // segment tree
        build(sum, a, l, m, rt << 1);
        build(sum, a, m + 1, r, rt << 1 | 1);

    }

    // Function for push down operation
    // on the segment tree
    static void pushDown(Vector<Integer> sum,
                         Vector<Integer> add,
                         int rt, int ln, int rn)
    {
        if(add.get(rt) != 0)
        {
            add.set(rt << 1, add.get(rt));
            add.set(rt << 1 | 1, add.get(rt));
            sum.set(rt << 1, sum.get(rt << 1) + add.get(rt) * ln);
            sum.set(rt << 1 | 1, sum.get(rt << 1 | 1) + add.get(rt) * rn);
            add.set(rt, 0);
        }
    }

    // Function to update the segment tree
    static void update(Vector<Integer> sum,
                       Vector<Integer> add,int L,
                       int R, int C, int l, int r, int rt)
    {

        // Complete overlap
        if(L <= l && r <= R)
        {
            sum.set(rt,sum.get(rt) + C * (r - l + 1));
            add.set(rt,add.get(rt) + C);
            return;
        }

        // Find mid
        int m = (l + r) >> 1;

        // Perform push down operation
        // on segment tree
        pushDown(sum, add, rt, m - l + 1, r - m);

        // Recursively update the segment tree
        if(L <= m)
        {
            update(sum, add, L, R, C, l, m, rt << 1);

        }
        if(R > m)
        {
            update(sum, add, L, R, C, m + 1, r, rt << 1 | 1);
        }
    }
    // Function to process the query
    static int query(Vector<Integer> sum,Vector<Integer> add,
                     int L, int R, int l,int r, int rt)
    {
        // Base case
        if (L <= l && r <= R)
        {
            return sum.get(rt);
        }

        // Find mid
        int m = (l + r) >> 1;

        // Perform push down operation
        // on segment tree
        pushDown(sum, add, rt, m - l + 1, r - m);
        int ans = 0;

        // Recursively calculate the result
        // of the query
        if(L <= m)
        {
            ans += query(sum, add, L, R, l, m, rt << 1);

        }
        if(R > m)
        {
            ans += query(sum, add, L, R, m + 1, r,rt << 1 | 1);
        }

        // Return the result
        return ans;
    }

    // Function to count the numbers
    // which are greater than the given query
    static void sequenceMaintenance(int n, int q,
                                    Vector<Integer> a,
                                    Vector<Integer> b,int m)
    {
        // Sort the input array
        Collections.sort(a);

        // Create segment tree of size 4*n
        Vector<Integer> sum = new Vector<Integer>();
        Vector<Integer> ad = new Vector<Integer>();
        Vector<Integer> ans = new Vector<Integer>();
        for(int i = 0; i < (n << 2); i++)
        {
            sum.add(0);
            ad.add(0);
        }

        // Build the segment tree
        build(sum, a, 1, n, 1);

        // Iterate over the queries
        for(int i = 0; i < q; i++)
        {
            int l = 1, r = n, pos = -1;
            while(l <= r)
            {
                m = (l + r) >> 1;
                if(query(sum, ad, m, m, 1, n, 1) >= b.get(i))
                {
                    r = m - 1;
                    pos = m;
                }
                else
                {
                    l = m + 1;
                }
            }
            if(pos == -1)
            {
                ans.add(0);
            }
            else
            {

                // Store result in array
                ans.add(n - pos + 1);

                // Update the elements in
                // the given range
                update(sum, ad, pos, n, -m, 1, n, 1);
            }
        }

         // Print the result of queries
        for(int i = 0; i < ans.size(); i++)
        {
            System.out.print(ans.get(i) + " ");
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int N = 4;
        int Q = 3;
        int M = 1;
        Vector<Integer> arr = new Vector<Integer>();
        arr.add(1);
        arr.add(2);
        arr.add(3);
        arr.add(4);
        Vector<Integer> query = new Vector<Integer>();
        query.add(4);
        query.add(3);
        query.add(1);

        // Function call
        sequenceMaintenance(N, Q, arr, query, M);
    }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to build a segment tree
def build(sum, a, l, r, rt):

    # Check for base case
    if (l == r):
        sum[rt] = a[l - 1]
        return

    # Find mid point
    m = (l + r) >> 1

    # Recursively build the
    # segment tree
    build(sum, a, l, m, rt << 1)
    build(sum, a, m + 1, r, rt << 1 | 1)

# Function for push down operation
# on the segment tree
def pushDown(sum, add, rt, ln, rn):

    if (add[rt]):
        add[rt << 1] += add[rt]
        add[rt << 1 | 1] += add[rt]
        sum[rt << 1] += add[rt] * ln
        sum[rt << 1 | 1] += add[rt] * rn
        add[rt] = 0

# Function to update the segment tree
def update(sum, add, L, R, C, l, r, rt):

    # Complete overlap
    if (L <= l and r <= R):
        sum[rt] += C * (r - l + 1)
        add[rt] += C
        return

    # Find mid
    m = (l + r) >> 1

    # Perform push down operation
    # on segment tree
    pushDown(sum, add, rt, m - l + 1, r - m)

    # Recursively update the segment tree
    if (L <= m):
        update(sum, add, L, R, C, l,
               m, rt << 1)

    if (R > m):
        update(sum, add, L, R, C, m + 1,
               r, rt << 1 | 1)

# Function to process the queryy
def queryy(sum, add, L, R, l, r, rt):

    # Base case
    if (L <= l and r <= R):
        return sum[rt]

    # Find mid
    m = (l + r) >> 1

    # Perform push down operation
    # on segment tree
    pushDown(sum, add, rt, m - l + 1, r - m)

    ans = 0

    # Recursively calculate the result
    # of the queryy
    if (L <= m):
        ans += queryy(sum, add, L, R, l,
                      m, rt << 1)
    if (R > m):
        ans += queryy(sum, add, L, R, m + 1,
                      r, (rt << 1 | 1))

    # Return the result
    return ans

# Function to count the numbers
# which are greater than the given queryy
def sequenceMaintenance(n, q, a, b, m):

    # Sort the input array
    a = sorted(a)

    # Create segment tree of size 4*n
    # vector<int> sum, add, ans
    sum = [0] * (4 * n)
    add = [0] * (4 * n)
    ans = []

    # Build the segment tree
    build(sum, a, 1, n, 1)

    #print(sum)

    # Iterate over the queries
    for i in range(q):
        l = 1
        r = n
        pos = -1

        while (l <= r):
            m = (l + r) >> 1
            if (queryy(sum, add, m, m,
                       1, n, 1) >= b[i]):
                r = m - 1
                pos = m

            else:
                l = m + 1

        if (pos == -1):
            ans.append(0)
        else:

            # Store result in array
            ans.append(n - pos + 1)

            # Update the elements in
            # the given range
            update(sum, add, pos, n,
                   -m, 1, n, 1)

    # Print the result of queries
    for i in ans:
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':

    N = 4
    Q = 3
    M = 1

    arr = [ 1, 2, 3, 4 ]
    query = [ 4, 3, 1 ]

    # Function call
    sequenceMaintenance(N, Q, arr, query, M)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic; 

class GFG{

// Function to build a segment tree
static void build(ArrayList sum,
                  ArrayList a,
                  int l, int r,
                  int rt)
{

    // Check for base case
    if (l == r)
    {
        sum[rt] = a[l - 1];
        return;
    }

    // Find mid point
    int m = (l + r) >> 1;

    // Recursively build the
    // segment tree
    build(sum, a, l, m, rt << 1);
    build(sum, a, m + 1, r, rt << 1 | 1);
}

// Function for push down operation
// on the segment tree
static void pushDown(ArrayList sum,
                     ArrayList add,
                     int rt, int ln,
                     int rn)
{
    if ((int)add[rt] != 0)
    {
        add[rt << 1] = (int)add[rt << 1] +
                       (int)add[rt];
        add[rt << 1 | 1] = (int)add[rt << 1 | 1] +
                           (int)add[rt];
        sum[rt << 1] = (int)sum[rt << 1] +
                       (int)add[rt] * ln;
        sum[rt << 1 | 1] = (int)sum[rt << 1 | 1] +
                           (int)add[rt] * rn;
        add[rt] = 0;
    }
}

// Function to update the segment tree
static void update(ArrayList sum,
                   ArrayList add,
                   int L, int R, int C,
                   int l, int r, int rt)
{

    // Complete overlap
    if (L <= l && r <= R)
    {
        sum[rt] = (int)sum[rt] +
                    C * (r - l + 1);
        add[rt] = (int)add[rt] + C;
        return;
    }

    // Find mid
    int m = (l + r) >> 1;

    // Perform push down operation
    // on segment tree
    pushDown(sum, add, rt, m - l + 1,
                           r - m);

    // Recursively update the segment tree
    if (L <= m)
        update(sum, add, L, R, C, l, m,
               rt << 1);
    if (R > m)
        update(sum, add, L, R, C, m + 1, r,
               rt << 1 | 1);
}

// Function to process the query
static int query(ArrayList sum,
                 ArrayList add,
                 int L, int R, int l,
                 int r, int rt)
{

    // Base case
    if (L <= l && r <= R)
    {
        return (int)sum[rt];
    }

    // Find mid
    int m = (l + r) >> 1;

    // Perform push down operation
    // on segment tree
    pushDown(sum, add, rt, m - l + 1,
                           r - m);

    int ans = 0;

    // Recursively calculate the result
    // of the query
    if (L <= m)
        ans += query(sum, add, L, R, l, m,
                     rt << 1);
    if (R > m)
        ans += query(sum, add, L, R, m + 1, r,
                     rt << 1 | 1);

    // Return the result
    return ans;
}

// Function to count the numbers
// which are greater than the given query
static void sequenceMaintenance(int n, int q,
                                ArrayList a,
                                ArrayList b,
                                int m)
{

    // Sort the input array
    a.Sort();

    // Create segment tree of size 4*n
    ArrayList sum = new ArrayList();
    ArrayList add = new ArrayList();
    ArrayList ans = new ArrayList();

    for(int i = 0; i < (n << 2); i++)
    {
        sum.Add(0);
        add.Add(0);
    }

    // Build the segment tree
    build(sum, a, 1, n, 1);

    // Iterate over the queries
    for(int i = 0; i < q; i++)
    {
        int l = 1, r = n, pos = -1;
        while (l <= r)
        {
            m = (l + r) >> 1;
            if (query(sum, add, m, m,
                      1, n, 1) >= (int)b[i])
            {
                r = m - 1;
                pos = m;
            }
            else
            {
                l = m + 1;
            }
        }
        if (pos == -1)
            ans.Add(0);
        else
        {

            // Store result in array
            ans.Add(n - pos + 1);

            // Update the elements in
            // the given range
            update(sum, add, pos, n, -m,
                   1, n, 1);
        }
    }

    // Print the result of queries
    for(int i = 0; i < ans.Count; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Driver Code
public static void Main(string[] args)
{
    int N = 4;
    int Q = 3;
    int M = 1;

    ArrayList arr = new ArrayList(){ 1, 2, 3, 4 };
    ArrayList query = new ArrayList(){ 4, 3, 1 };

    // Function call
    sequenceMaintenance(N, Q, arr, query, M);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to build a segment tree
function build(sum, a, l, r, rt)
{

    // Check for base case
        if(l == r)
        {
            sum[rt] =  a[l - 1];
            return;
        }

        // Find mid point
        let m = (l + r) >> 1;

        // Recursively build the
        // segment tree
        build(sum, a, l, m, rt << 1);
        build(sum, a, m + 1, r, rt << 1 | 1);
}

// Function for push down operation
    // on the segment tree
function pushDown(sum,add,rt,ln,rn)
{
    if(add[rt] != 0)
        {
            add[rt << 1] = add[rt];
            add[rt << 1 | 1] = add[rt];
            sum[rt << 1] = sum[rt << 1] + add[rt] * ln;
            sum[rt << 1 | 1] = sum[rt << 1 | 1] + add[rt] * rn;
            add[rt]= 0;
        }
}

// Function to update the segment tree
function update(sum,add,L,R,C,l,r,rt)
{
    // Complete overlap
        if(L <= l && r <= R)
        {
            sum[rt] = sum[rt] + C * (r - l + 1);
            add[rt] = add[rt] + C;
            return;
        }

        // Find mid
        let m = (l + r) >> 1;

        // Perform push down operation
        // on segment tree
        pushDown(sum, add, rt, m - l + 1, r - m);

        // Recursively update the segment tree
        if(L <= m)
        {
            update(sum, add, L, R, C, l, m, rt << 1);

        }
        if(R > m)
        {
            update(sum, add, L, R, C, m + 1, r, rt << 1 | 1);
        }
}

// Function to process the query
function query(sum,add,L,R,l,r,rt)
{
    // Base case
        if (L <= l && r <= R)
        {
            return sum[rt];
        }

        // Find mid
        let m = (l + r) >> 1;

        // Perform push down operation
        // on segment tree
        pushDown(sum, add, rt, m - l + 1, r - m);
        let ans = 0;

        // Recursively calculate the result
        // of the query
        if(L <= m)
        {
            ans += query(sum, add, L, R, l, m, rt << 1);

        }
        if(R > m)
        {
            ans += query(sum, add, L, R, m + 1, r,rt << 1 | 1);
        }

        // Return the result
        return ans;
}

// Function to count the numbers
    // which are greater than the given query
function sequenceMaintenance(n,q,a,b,m)
{
    // Sort the input array
        a.sort(function(a,b){return a-b;});

        // Create segment tree of size 4*n
        let sum = [];
        let ad = [];
        let ans = [];
        for(let i = 0; i < (n << 2); i++)
        {
            sum.push(0);
            ad.push(0);
        }

        // Build the segment tree
        build(sum, a, 1, n, 1);

        // Iterate over the queries
        for(let i = 0; i < q; i++)
        {
            let l = 1, r = n, pos = -1;
            while(l <= r)
            {
                m = (l + r) >> 1;
                if(query(sum, ad, m, m, 1, n, 1) >= b[i])
                {
                    r = m - 1;
                    pos = m;
                }
                else
                {
                    l = m + 1;
                }
            }
            if(pos == -1)
            {
                ans.push(0);
            }
            else
            {

                // Store result in array
                ans.push(n - pos + 1);

                // Update the elements in
                // the given range
                update(sum, ad, pos, n, -m, 1, n, 1);
            }
        }

         // Print the result of queries
        for(let i = 0; i < ans.length; i++)
        {
            document.write(ans[i] + " ");
        }
}

// Driver Code
let N = 4;
let Q = 3;
let M = 1;

let arr=[1, 2, 3, 4];
let Query = [4, 3, 1];

// Function call
sequenceMaintenance(N, Q, arr, Query, M);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
1 2 4
```

***时间复杂度:**O(N+(Q * logN))*
***辅助空间:** O (N)*