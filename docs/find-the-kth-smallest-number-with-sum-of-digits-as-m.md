# 求数字和为 m 的第 k 个最小数

> 原文:[https://www . geeksforgeeks . org/find-the-kth-最小数字加数字和-as-m/](https://www.geeksforgeeks.org/find-the-kth-smallest-number-with-sum-of-digits-as-m/)

给定两个整数 **M** 和 **K** ，任务是找到数字和为 **M** 的 **Kth** 最小数。
**举例:**

> **输入:** M = 5，K = 3
> **输出:** 23
> 从 1 开始以数字和为 5 的数字序列如下:
> 5
> 14
> 23
> 32
> 41
> 所以第三个最小的数字是 23
> **输入:** M = 4，K = 1
> **输出:** 4

**方法:**我们需要找到从 1 开始的数字序列，数字之和为 m.

*   写一个递归函数，增加数字，直到数字的位数总和等于我们需要的总和 **M** 。
*   为此，始终从 **0** 开始，并检查将加到 **M** 的一位数
*   让我们举一个 sum = 5 的例子，这样我们就可以从 0 开始，以一位数上升到 5，因为 6 超过了所需的总和
*   现在，从 5 开始，我们将移动到两位数数字 10，我们将上升到 14，因为 14 的位数总和是 5，15 将超过所需的总和，以此类推，然后我们将在 20 秒内移动，这将上升到 50，因为 50 到 99 年后，每个数字的位数总和将大于 5，因此我们将跳过这一步。
*   现在我们将移入三个数字 100，101，102，…类似地，这个操作将继续进行，直到数字的位数之和等于 15。
*   我们将继续把元素插入到数字总和等于 **M** 的集合中。

```
for(int i=0;i<=min(left, 9LL);i++){
  dfs(num*10+i, left-i, ct+1);  
}
```

为了找到最小的 kth，我们需要对序列进行排序，所以如果我们将数字存储在 C++中的[集合中会更好，因为集合中的数字是按排序顺序排列的。
**注意**这种方法不适用于更大的输入值。
以下是上述方法的实施:](https://www.geeksforgeeks.org/set-in-cpp-stl/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define int long long
const int N = 2005;

set<int> ans;

// Recursively moving to add
// all the numbers upto a limit
// with sum of digits as m
void dfs(int num, int left, int ct)
{
    // Max number of digits allowed in
    // a number for this implementation
    if (ct >= 15)
        return;
    if (left == 0)
        ans.insert(num);
    for (int i = 0; i <= min(left, 9LL); i++)
        dfs(num * 10 + i, left - i, ct + 1);
}

// Function to return the kth number
// with sum of digits as m
int getKthNum(int m, int k)
{
    dfs(0, m, 0);

    int ct = 0;
    for (auto it : ans) {
        ct++;

        // The kth smallest number is found
        if (ct == k) {
            return it;
        }
    }
    return -1;
}

// Driver code
int main()
{
    int m = 5, k = 3;

    cout << getKthNum(m, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int N = 2005;

static Set<Integer> ans = new LinkedHashSet<Integer>();

// Recursively moving to add
// all the numbers upto a limit
// with sum of digits as m
static void dfs(int num, int left, int ct)
{
    // Max number of digits allowed in
    // a number for this implementation
    if (ct >= 15)
        return;
    if (left == 0)
        ans.add(num);
    for (int i = 0; i <= Math.min(left, 9); i++)
        dfs(num * 10 + i, left - i, ct + 1);
}

// Function to return the kth number
// with sum of digits as m
static int getKthNum(int m, int k)
{
    dfs(0, m, 0);

    int ct = 0;
    for (int it : ans)
    {
        ct++;

        // The kth smallest number is found
        if (ct == k)
        {
            return it;
        }
    }
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int m = 5, k = 3;

    System.out.println(getKthNum(m, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# define long long
N = 2005

ans = dict()

# Recursively moving to add
# all the numbers upto a limit
# with sum of digits as m
def dfs(n, left, ct):

    # Max nber of digits allowed in
    # a nber for this implementation
    if (ct >= 15):
        return
    if (left == 0):
        ans[n] = 1
    for i in range(min(left, 9) + 1):
        dfs(n * 10 + i, left - i, ct + 1)

# Function to return the kth number
# with sum of digits as m
def getKthNum(m, k):
    dfs(0, m, 0)

    c = 0
    for it in sorted(ans.keys()):
        c += 1

        # The kth smallest number is found
        if (c == k):
            return it
    return -1

# Driver code
m = 5
k = 3

print(getKthNum(m, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{
static int N = 2005;

static HashSet<int> ans = new HashSet<int>();

// Recursively moving to add
// all the numbers upto a limit
// with sum of digits as m
static void dfs(int num, int left, int ct)
{
    // Max number of digits allowed in
    // a number for this implementation
    if (ct >= 15)
        return;
    if (left == 0)
        ans.Add(num);
    for (int i = 0;
             i <= Math.Min(left, 9); i++)
        dfs(num * 10 + i, left - i, ct + 1);
}

// Function to return the kth number
// with sum of digits as m
static int getKthNum(int m, int k)
{
    dfs(0, m, 0);

    int ct = 0;
    foreach (int it in ans)
    {
        ct++;

        // The kth smallest number is found
        if (ct == k)
        {
            return it;
        }
    }
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int m = 5, k = 3;

    Console.WriteLine(getKthNum(m, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let N = 2005;
let  ans = new Set();

// Recursively moving to add
// all the numbers upto a limit
// with sum of digits as m
function dfs(num,left,ct)
{
    // Max number of digits allowed in
    // a number for this implementation
    if (ct >= 15)
        return;
    if (left == 0)
        ans.add(num);
    for (let i = 0; i <= Math.min(left, 9); i++)
        dfs(num * 10 + i, left - i, ct + 1);
}

// Function to return the kth number
// with sum of digits as m
function getKthNum(m,k)
{
    dfs(0, m, 0);

    let ct = 0;
    for (let it of ans.values())
    {
        ct++;

        // The kth smallest number is found
        if (ct == k)
        {
            return it;
        }
    }
    return -1;
}

// Driver code
let m = 5, k = 3;

document.write(getKthNum(m, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
23
```