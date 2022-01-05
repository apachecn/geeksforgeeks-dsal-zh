# 在数组中搜索一个元素的查询，并在每次查询后将其移到前面

> 原文:[https://www . geeksforgeeks . org/query-to-search-in-a-element-in-a-array-and-move-to-front-after-the-after-query/](https://www.geeksforgeeks.org/queries-to-search-an-element-in-an-array-and-move-it-to-front-after-every-query/)

给定一个整数 **M** ，它表示一个最初具有数字 1 到 M 的数组。还给定了一个**查询**数组。对于每个查询，搜索初始数组中的数字，并将其放在数组的前面。任务是为每个查询返回给定数组中搜索到的元素的索引。
**例:**

> **输入:** Q[] = {3，1，2，1}，M = 5
> **输出:**【2，1，2，1】
> **解释:**
> 由于 M = 5，初始数组为[1，2，3，4，5]。
> 查询 1:在[1，2，3，4，5]中搜索 3，并在开头移动它。移动后，数组看起来像[3，1，2，4，5]。3 在指数 2。
> 查询 2:将 1 从[3，1，2，4，5]移动到数组的开头，使数组看起来像[1，3，2，4，5]。索引 1 中有 1。
> 查询 3:将 2 从[1，3，2，4，5]移动到数组的开头，使数组看起来像[2，1，3，2，4，5]。索引 2 中有 2。
> 查询 4:将 1 从[2，1，3，4，5]移动到数组的开头，使数组看起来像[1，2，3，4，5]。索引 1 中有 1。
> **输入:** Q[] = {4，1，2，2}，M = 4
> **输出:** 3，1，2，0

**天真的方法:****天真的方法是使用哈希表来搜索元素，并通过执行交换来线性地执行移位。对于这种方法，时间复杂度本质上是二次的。
下面是上述方法的天真实现:**

## C++

```
// C++ program to search the element
// in an array for every query and
// move the searched element to
// the front after every query
#include <bits/stdc++.h>
using namespace std;

// Function to find the indices
vector<int> processQueries(int Q[], int m, int n)
{
    int a[m + 1], pos[m + 1];

    for (int i = 1; i <= m; i++) {
        a[i - 1] = i;
        pos[i] = i - 1;
    }

    vector<int> ans;

    // iterate in the query array
    for (int i = 0; i < n; i++) {
        int q = Q[i];

        // store current element
        int p = pos[q];

        ans.push_back(p);

        for (int i = p; i > 0; i--) {

            // swap positions of the element
            swap(a[i], a[i - 1]);

            pos[a[i]] = i;
        }

        pos[a[0]] = 0;
    }

    // return the result
    return ans;
}

// Driver code
int main()
{
    // initialise array
    int Q[] = { 3, 1, 2, 1 };
    int n = sizeof(Q) / sizeof(Q[0]);

    int m = 5;

    vector<int> ans;

    // Function call
    ans = processQueries(Q, m, n);

    // Print answers to queries
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to search the element
// in an array for every query and
// move the searched element to
// the front after every query
import java.util.*;

class GFG{

// Function to find the indices
static Vector<Integer> processQueries(int Q[], int m, int n)
{
    int []a = new int[m + 1];
    int []pos = new int[m + 1];

    for (int i = 1; i <= m; i++) {
        a[i - 1] = i;
        pos[i] = i - 1;
    }

    Vector<Integer> ans = new Vector<Integer>();

    // iterate in the query array
    for (int i = 0; i < n; i++) {
        int q = Q[i];

        // store current element
        int p = pos[q];

        ans.add(p);

        for (int j = p; j > 0; j--) {

            // swap positions of the element
            a[j] = a[j] + a[j - 1];
            a[j - 1] = a[j] - a[j - 1];
            a[j] = a[j] - a[j - 1];

            pos[a[j]] = j;
        }

        pos[a[0]] = 0;
    }

    // return the result
    return ans;
}

// Driver code
public static void main(String[] args)
{
    // initialise array
    int Q[] = { 3, 1, 2, 1 };
    int n = Q.length;

    int m = 5;

    Vector<Integer> ans = new Vector<Integer>();

    // Function call
    ans = processQueries(Q, m, n);

    // Print answers to queries
    for (int i = 0; i < ans.size(); i++)
        System.out.print(ans.get(i)+ " ");

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to search the element
# in an array for every query and
# move the searched element to
# the front after every query

# Function to find the indices
def processQueries(Q, m, n) :

    a = [0]*(m + 1); pos = [0]*(m + 1);

    for i in range(1, m + 1) :
        a[i - 1] = i;
        pos[i] = i - 1;

    ans = [];

    # iterate in the query array
    for i in range(n) :
        q = Q[i];

        # store current element
        p = pos[q];

        ans.append(p);

        for i in range(p,0,-1) :

            # swap positions of the element
            a[i], a[i - 1] = a[i - 1],a[i];
            pos[a[i]] = i;

        pos[a[0]] = 0;

    # return the result
    return ans;

# Driver code
if __name__ == "__main__" :

    # initialise array
    Q = [ 3, 1, 2, 1 ];
    n = len(Q);

    m = 5;

    ans = [];

    # Function call
    ans = processQueries(Q, m, n);

    # Print answers to queries
    for i in range(len(ans)) :
        print(ans[i],end=" ");

# This code is contributed by Yash_R
```

## C#

```
// C# program to search the element
// in an array for every query and
// move the searched element to
// the front after every query
using System;
using System.Collections.Generic;

public class GFG{

// Function to find the indices
static List<int> processQueries(int []Q, int m, int n)
{
    int []a = new int[m + 1];
    int []pos = new int[m + 1];

    for(int i = 1; i <= m; i++)
    {
       a[i - 1] = i;
       pos[i] = i - 1;
    }

    List<int> ans = new List<int>();

    // Iterate in the query array
    for(int i = 0; i < n; i++)
    {
       int q = Q[i];

       // Store current element
       int p = pos[q];
       ans.Add(p);

       for(int j = p; j > 0; j--)
       {

          // Swap positions of the element
          a[j] = a[j] + a[j - 1];
          a[j - 1] = a[j] - a[j - 1];
          a[j] = a[j] - a[j - 1];

          pos[a[j]] = j;
       }
       pos[a[0]] = 0;
    }

    // Return the result
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    // Initialise array
    int []Q = { 3, 1, 2, 1 };
    int n = Q.Length;
    int m = 5;

    List<int> ans = new List<int>();

    // Function call
    ans = processQueries(Q, m, n);

    // Print answers to queries
    for(int i = 0; i < ans.Count; i++)
       Console.Write(ans[i] + " ");

}
}
// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program to search the element
// in an array for every query and
// move the searched element to
// the front after every query

// Function to find the indices
function processQueries(Q,m,n)
{
    let a = new Array(m + 1);
    let pos = new Array(m + 1);

    for (let i = 1; i <= m; i++) {
        a[i - 1] = i;
        pos[i] = i - 1;
    }

    let ans = [];

    // iterate in the query array
    for (let i = 0; i < n; i++) {
        let q = Q[i];

        // store current element
        let p = pos[q];

        ans.push(p);

        for (let j = p; j > 0; j--) {

            // swap positions of the element
            a[j] = a[j] + a[j - 1];
            a[j - 1] = a[j] - a[j - 1];
            a[j] = a[j] - a[j - 1];

            pos[a[j]] = j;
        }

        pos[a[0]] = 0;
    }

    // return the result
    return ans;
}

// Driver code

// initialise array
let Q=[3, 1, 2, 1];
let n = Q.length;
let m = 5;
let ans=[];
// Function call
ans = processQueries(Q, m, n);

// Print answers to queries
for (let i = 0; i < ans.length; i++)
    document.write(ans[i]+ " ");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2 1 2 1
```