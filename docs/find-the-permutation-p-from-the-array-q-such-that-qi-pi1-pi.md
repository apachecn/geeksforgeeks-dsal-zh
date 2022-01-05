# 从数组 q 中找出排列 p，使得 q[I]= p[I+1]–p[I]

> 原文:[https://www . geesforgeks . org/find-the-array-p-from-q-so-qi-pi1-pi/](https://www.geeksforgeeks.org/find-the-permutation-p-from-the-array-q-such-that-qi-pi1-pi/)

给定一个长度为 **N** 的数组 **Q[]** ，任务是从范围**【1，N+1】**中找到整数的排列 **P[]** ，使得**Q[I]= P[I+1]–P[I]**对于所有有效的 **i** 。如果不可能，则打印 **-1** 。

**示例:**

> **输入:** Q[] = {-2，1 }
> T3】输出:3 1 2
> Q[0]= p[1]–p[0]= 1–3 =-2
> Q[1]= p[2]–p[1]= 2–1 = 1
> 
> **输入:** Q[] = {1，1，1，1}
> **输出:** 1 2 3 4 5
> 
> **输入:** Q[] = {-1，2，2 }
> T3】输出: -1

**进场:**
让，

> **P[0] = x** 然后**P[1]= P[0]+(P[1]–P[0])= x+Q[0]**
> ，以及**P[2]= P[0]+(P[1]–P[0])+(P[2]–P[1])= x+Q[0]+Q[1]**。

同样的，

> **P[n] = x + Q[0] + Q[1] + Q[2 ] + …..+Q[N–1]**。

意思是序列 **p' = 0，Q[1]，Q[1] + Q[2]，…..，+ Q[1] + Q[2] + Q[3] + …..+Q[N–1]**是每个元素加上 **x** 后所需的排列。
要找到 **x** 的值，请找到一个 **i** ，使得**p【I】**最小。
As， **p'[i] + x** 是系列中的最小值，那么它必须等于 **1** ，因为系列可以具有来自**【1，N】**的值。
所以**x = 1–p '[I]**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>

using namespace std;

// Function to return the minimum
// value of x from the given array q
int Get_Minimum(vector<int> q)
{
    int minimum = 0;
    int sum = 0;
    for(int i = 0; i < q.size() - 1; i++)
    {
        sum += q[i];
        if (sum < minimum)
            minimum = sum;
    }
    return minimum;
}

// Function to return the required permutation
vector<int> Find_Permutation(vector<int> q, int n)
{
    vector<int> p(n, 0);
    int min_value = Get_Minimum(q);

    // Set the value of p[0] i.e. x = p[0]
    p[0] = 1 - min_value;

    // Iterate over array q[]
    for (int i = 0; i < n - 1; i++)
        p[i + 1] = p[i] + q[i];

    bool okay = true;

    // Check if formed permutation
    // is correct or not
    for (int i = 0; i < n; i++)
    {
        if (p[i] < 1 or p[i] > n)
            okay = false;
        set<int> w(p.begin(), p.end());
        if (w.size() != n)
            okay = false;
    }

    // Return the permutation p
    if (okay)
        return p;
    else
        return {-1};
}

// Driver code
int main()
{
    vector<int> q = {-2, 1};
    int n = q.size() + 1;
    cout << "[ ";
    for (int i:Find_Permutation(q, n))
        cout << i << " ";
    cout << "]";    
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum
// value of x from the given array q
static int Get_Minimum(int [] q)
{
    int minimum = 0;
    int sum = 0;
    for(int i = 0; i < q.length - 1; i++)
    {
        sum += q[i];
        if (sum < minimum)
            minimum = sum;
    }
    return minimum;
}

// Function to return the required permutation
static int [] Find_Permutation(int [] q, int n)
{
    int [] p = new int[n];
    int min_value = Get_Minimum(q);

    // Set the value of p[0] i.e. x = p[0]
    p[0] = 1 - min_value;

    // Iterate over array q[]
    for (int i = 0; i < n - 1; i++)
        p[i + 1] = p[i] + q[i];

    boolean okay = true;

    // Check if formed permutation
    // is correct or not
    for (int i = 0; i < n; i++)
    {
        if (p[i] < 1 || p[i] > n)
            okay = false;
        Set<Integer> w = new HashSet<>();
        if (w.size() != n)
            okay = true;
    }

    // Return the permutation p
    if (okay)
        return p;
    else
        return new int []{-1};
}

// Driver code
public static void main(String args[])
{
    int []q = {-2, 1};
    int n = q.length + 1;
    System.out.print("[ ");
    for (int i:Find_Permutation(q, n))
        System.out.print(i + " ");
    System.out.print("]");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# value of x from the given array q
def Get_Minimum(q):
    minimum = 0
    sum = 0
    for i in range(n - 1):
        sum += q[i]
        if sum < minimum:
            minimum = sum
    return minimum

# Function to return the
# required permutation
def Find_Permutation(q):
    p = [0] * n
    min_value = Get_Minimum(q)

    # Set the value of p[0]
    # i.e. x = p[0]
    p[0]= 1 - min_value

    # Iterate over array q[]
    for i in range(n - 1):
        p[i + 1] = p[i] + q[i]

    okay = True

    # Check if formed permutation
    # is correct or not
    for i in range(n):
        if p[i] < 1 or p[i] > n:
            okay = False
    if len(set(p)) != n:
        okay = False

    # Return the permutation p
    if okay:
        return p
    else:
        return -1

# Driver code
if __name__=="__main__":
    q = [-2, 1]
    n = len(q) + 1
    print(Find_Permutation(q))
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the minimum
// value of x from the given array q
static int Get_Minimum(int [] q)
{
    int minimum = 0;
    int sum = 0;
    for(int i = 0; i < q.Length - 1; i++)
    {
        sum += q[i];
        if (sum < minimum)
            minimum = sum;
    }
    return minimum;
}

// Function to return the required permutation
static int [] Find_Permutation(int [] q, int n)
{
    int [] p = new int[n];
    int min_value = Get_Minimum(q);

    // Set the value of p[0] i.e. x = p[0]
    p[0] = 1 - min_value;

    // Iterate over array q[]
    for (int i = 0; i < n - 1; i++)
        p[i + 1] = p[i] + q[i];

    bool okay = true;

    // Check if formed permutation
    // is correct or not
    for (int i = 0; i < n; i++)
    {
        if (p[i] < 1 || p[i] > n)
            okay = false;
        HashSet<int> w = new HashSet<int>();
        if (w.Count != n)
            okay = true;
    }

    // Return the permutation p
    if (okay)
        return p;
    else
        return new int []{-1};
}

// Driver code
public static void Main(String []args)
{
    int []q = {-2, 1};
    int n = q.Length + 1;
    Console.Write("[ ");
    foreach (int i in Find_Permutation(q, n))
        Console.Write(i + " ");
    Console.Write("]");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// value of x from the given array q
function Get_Minimum(q)
{
    let minimum = 0;
    let sum = 0;
    for(let i = 0; i < q.length - 1; i++)
    {
        sum += q[i];
        if (sum < minimum)
            minimum = sum;
    }
    return minimum;
}

// Function to return the required permutation   
function Find_Permutation(q, n)
{
    let p = new Array(n);
    let min_value = Get_Minimum(q);

    // Set the value of p[0] i.e. x = p[0]
    p[0] = 1 - min_value;

    // Iterate over array q[]
    for(let i = 0; i < n - 1; i++)
        p[i + 1] = p[i] + q[i];

    let okay = true;

    // Check if formed permutation
    // is correct or not
    for(let i = 0; i < n; i++)
    {
        if (p[i] < 1 || p[i] > n)
            okay = false;

        let w = new Set();
        if (w.size != n)
            okay = true;
    }

    // Return the permutation p
    if (okay)
        return p;
    else
        return new [-1];
}

// Driver code
let q = [ -2, 1 ];
let n = q.length + 1;
document.write("[ ");

let temp = Find_Permutation(q, n);
for(let i = 0; i < temp.length; i++)
    document.write(temp[i] + " ");

document.write("]");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
[3, 1, 2]
```