# 通过给定操作从最小转换成本为 1 的范围[L，R]中的数字

> 原文:[https://www . geeksforgeeks . org/number-from-a-range-l-r-having-kth-按给定操作转换为 1 的最小成本/](https://www.geeksforgeeks.org/number-from-a-range-l-r-having-kth-minimum-cost-of-conversion-to-1-by-given-operations/)

给定三个整数 **L** 、 **R** 和 **K** ，其中**【L，R】**表示元素的范围，任务是在范围**【L，R】**中找到元素，要求 K <sup>th</sup> 转换为 **1** 的最小成本。如果两个或多个元素具有相同的成本，则打印其中的最小值。

> 使用给定操作将元素 **X** 转换为 1 的成本是使用的操作计数:
> 
> 1.  如果 X 是偶数，那么把 X 转换成 X/2
> 2.  如果 X 是奇数，则将 X 转换为 3*X + 1

**示例:**

> **输入:** L = 12，R = 15， K = 2
> **产量:** 13
> **解释:**
> 与 12 相关的成本为 9(12–>6–>3–>10–>5–>16–>8–>4–>2–>1)
> 与 13 相关的成本为 9(13–>40–>20–>10–>5–>16–>8–>4–>2–>1)
> 与 14 相关的成本为 17(14–>7–>22–>11–>34–>17–>52–>26–>13–>40–>20–>10–>5–>16–>8–>4–>2–>
> 与 15 相关的成本为 17(15–>46–>23–>70–>35–>106–>53–>160–>80–>40–>20–>10–>5–>16–>8–>4–>
> 对于 K = 2，输出为 13。
> 
> **输入:** L = 1，R = 1，K = 1
> T3】输出: 1

**天真方法:**最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)计算 **L** 和 **R** 之间每个元素的相关成本。以下是步骤:

1.  定义一个递归计算成本的函数**函数**。
2.  将元素的所有成本存储在一对数组中。
3.  根据成本对数组进行排序。
4.  然后从数组中返回第(K-1) <sup>个</sup>索引处的元素。

下面是上述方法的实现:

## C++14

```
// C++14 implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

//Function to calculate the cost
int func(int n)
{
    int count = 0;

    // Base case
    if (n == 2 or n == 1)
        return 1;

    // Even condition
    if (n % 2 == 0)
        count = 1 + func(n / 2);

    // Odd condition
    if (n % 2 != 0)
        count = 1 + func(n * 3 + 1);

    // Return cost
    return count;
}

// Function to find Kth element
void findKthElement(int l, int r, int k)
{
    vector<int> arr;

    for(int i = l; i <= r; i++)
        arr.push_back(i);

    // Array to store the costs
    vector<vector<int>> result;

    for(int i : arr)
        result.push_back({i, func(i)});

    // Sort the array based on cost
    sort(result.begin(), result.end());

    cout << (result[k - 1][0]);
}

// Driver Code
int main()
{

    // Given range and6 K
    int l = 12;
    int r = 15;
    int k = 2;

    // Function call
    findKthElement(l, r, k);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function to calculate the cost
static int func(int n)
{
    int count = 0;

    // Base case
    if (n == 2 || n == 1)
        return 1;

    // Even condition
    if (n % 2 == 0)
        count = 1 + func(n / 2);

    // Odd condition
    if (n % 2 != 0)
        count = 1 + func(n * 3 + 1);

    // Return cost
    return count;
}

// Function to find Kth element
static void findKthElement(int l, int r, int k)
{
    ArrayList<Integer> arr = new ArrayList<>();

    for(int i = l; i <= r; i++)
        arr.add(i);

    // Array to store the costs
    ArrayList<List<Integer>> result = new ArrayList<>();

    for(int i : arr)
        result.add(Arrays.asList(i, func(i)));

    // Sort the array based on cost
    Collections.sort(result, (s1, s2) -> s1.get(1) -
                                         s2.get(1));

    System.out.println(result.get(k - 1).get(0));
}

// Driver code
public static void main (String[] args)
{

    // Given range and6 K
    int l = 12;
    int r = 15;
    int k = 2;

    // Function call
    findKthElement(l, r, k);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to calculate the cost
def func(n):
    count = 0

    # Base case
    if n == 2 or n == 1:
        return 1

    # Even condition
    if n % 2 == 0:  
        count = 1 + func(n//2)

    # Odd condition
    if n % 2 != 0: 
        count = 1 + func(n * 3 + 1)

    # Return cost 
    return count

# Function to find Kth element
def findKthElement(l, r, k):
    arr = list(range(l, r + 1))

    # Array to store the costs
    result = []
    for i in arr:
        result.append([i, func(i)])

    # Sort the array based on cost
    result.sort()
    print(result[k-1][0])

# Driver Code

# Given range and K
l = 12
r = 15
k = 2

# Function Call
findKthElement(l, r, k)
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Function to calculate the cost
static int func(int n)
{
    int count = 0;

    // Base case
    if (n == 2 || n == 1)
        return 1;

    // Even condition
    if (n % 2 == 0)
        count = 1 + func(n / 2);

    // Odd condition
    if (n % 2 != 0)
        count = 1 + func(n * 3 + 1);

    // Return cost
    return count;
}

// Function to find Kth element
static void findKthElement(int l, int r, int k)
{
    List<int> arr = new List<int>();

    for(int i = l; i <= r; i++)
        arr.Add(i);

    // Array to store the costs
    Dictionary<int,
               int> result = new Dictionary<int,
                                            int>();
    foreach(int i in arr)
    {
        result.Add(i, func(i));
    }

    // Sort the array based on cost
    var myList = result.ToList();

    myList.Sort((pair1, pair2) => pair1.Value.CompareTo(
        pair2.Value));

    Console.WriteLine(myList[1].Key);
}

// Driver code
public static void Main(String[] args)
{

    // Given range and6 K
    int l = 12;
    int r = 15;
    int k = 2;

    // Function call
    findKthElement(l, r, k);
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

//Function to calculate the cost
function func(n)
{
    var count = 0;

    // Base case
    if (n == 2 || n == 1)
        return 1;

    // Even condition
    if (n % 2 == 0)
        count = 1 + func(n / 2);

    // Odd condition
    if (n % 2 != 0)
        count = 1 + func(n * 3 + 1);

    // Return cost
    return count;
}

// Function to find Kth element
function findKthElement( l, r, k)
{
    var arr = [];

    for(var i = l; i <= r; i++)
        arr.push(i);

    // Array to store the costs
    var result = [];

    arr.forEach(i => {

        result.push([i, func(i)]);
    });

    // Sort the array based on cost
    result.sort();

    document.write( result[k - 1][0]);
}

// Driver Code
// Given range and6 K
var l = 12;
var r = 15;
var k = 2;

// Function call
findKthElement(l, r, k);

</script>
```

**Output:** 

```
13
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效途径:**上述途径可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。以下是步骤:

*   为了避免重新计算[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，初始化一个 **dp[]** 数组来存储最小成本，使每个遇到的子问题达到 1。
*   更新 dp[]表的重复关系是:

> 偶数元素的 DP[n]= 1+func(n/2)
> 奇数元素的 dp[n] = 1 + func(3 * n + 1)

*   将所有计算出的成本存储在一对数组中
*   [根据成本对成对的数组](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序。
*   然后从数组中返回**(K–1)<sup>第</sup>索引**处的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the cost
int func(int n, int dp[])
{
    int count = 0;

    // Base case
    if (n == 2 || n == 1)
        return 1;

    if (dp[n] != -1)
        return dp[n];

    // Even condition
    if (n % 2 == 0)
        count = 1 + func(n / 2, dp);

    // Odd condition
    if (n % 2 != 0)
        count = 1 + func(n * 3 + 1, dp);

    // Store the result
    dp[n] = count;
    return dp[n];
}

// Function to find Kth element
void findKthElement(int l, int r, int k)
{

    // Array to store the results
    vector<pair<int, int> > result;

    // Define DP array
    int dp[r + 1] = {0};
    dp[1] = 1;
    dp[2] = 1;

    for(int i = l; i <= r; i++)
        result.push_back({i, func(i, dp)});

    // Sort the array based on cost
    sort(result.begin(), result.end());

    cout << (result[k - 1].first);
}

// Driver code
int main()
{

    // Given range and K
    int l = 12;
    int r = 15;
    int k = 2;

    // Function call
    findKthElement(l, r, k);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

static class Pair implements Comparable<Pair>
{
  int start,end;

  Pair(int s, int e)
  {
    start = s;
    end = e;
  }

  public int compareTo(Pair p)
  {
    return this.start - p.start;
  }
}

// Function to calculate
// the cost
static int func(int n,
                int dp[])
{
  int count = 0;

  // Base case
  if (n == 2 ||
      n == 1)
    return 1;

  if (dp[n] != -1)
    return dp[n];

  // Even condition
  if (n % 2 == 0)
    count = 1 + func(n / 2, dp);

  // Odd condition
  if (n % 2 != 0)
    count = 1 + func(n * 3 +
                     1, dp);

  // Store the result
  dp[n] = count;
  return dp[n];
}

// Function to find Kth element
static void findKthElement(int l,
                           int r,
                           int k)
{
  // Array to store the
  // results
  Vector<Pair> result =
         new Vector<>();

  // Define DP array
  int []dp = new int[r + 1];
  dp[1] = 1;
  dp[2] = 1;

  for(int i = l; i <= r; i++)
    result.add(new Pair(i,
               func(i, dp)));

  // Sort the array based
  // on cost
  Collections.sort(result);

  System.out.print(
  result.get(k - 1).start);
}

// Driver code
public static void main(String[] args)
{   
  // Given range and K
  int l = 12;
  int r = 15;
  int k = 2;

  // Function call
  findKthElement(l, r, k);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
# Function to calculate the cost
def func(n, dp):
    count = 0

    # Base case
    if n == 2 or n == 1:
        return 1
    if n in dp:
      return dp[n] 

    # Even condition
    if n % 2 == 0: 
        count = 1 + func(n//2, dp)

    # Odd condition
    if n % 2 != 0:  
        count = 1 + func(n * 3 + 1, dp)

    # Store the result
    dp[n]= count
    return dp[n]

# Function to find Kth element
def findKthElement(l, r, k):
    arr = list(range(l, r + 1))

    # Array to store the results
    result = []

    # Define DP array
    dp ={1:1, 2:1}

    for i in arr:
        result.append([i, func(i, dp)])

    # Sort the array based on cost
    result.sort()
    print(result[k-1][0])

# Given range and K
l = 12
r = 15
k = 2

# Function Call
findKthElement(l, r, k)
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections;

class GFG{

class Pair
{
   public int start,end;

  public Pair(int s, int e)
  {
    start = s;
    end = e;
  }
}

class sortHelper : IComparer
{
   int IComparer.Compare(object a, object b)
   {
      Pair first=(Pair)a;
      Pair second=(Pair)b;

      return first.start - second.start;
   }
}

// Function to calculate
// the cost
static int func(int n, int []dp)
{
  int count = 0;

  // Base case
  if (n == 2 || n == 1)
    return 1;

  if (dp[n] != -1)
    return dp[n];

  // Even condition
  if (n % 2 == 0)
    count = 1 + func(n / 2, dp);

  // Odd condition
  if (n % 2 != 0)
    count = 1 + func(n * 3 +
                     1, dp);

  // Store the result
  dp[n] = count;
  return dp[n];
}

// Function to find Kth element
static void findKthElement(int l,
                           int r,
                           int k)
{
  // Array to store the
  // results
  ArrayList result =
         new ArrayList();

  // Define DP array
  int []dp = new int[r + 1];
  dp[1] = 1;
  dp[2] = 1;

  for(int i = l; i <= r; i++)
    result.Add(new Pair(i,
               func(i, dp)));

  // Sort the array based
  // on cost
  result.Sort(new sortHelper());

  Console.Write(((Pair)result[k - 1]).start);
}

// Driver code
public static void Main(string[] args)
{   
  // Given range and K
  int l = 12;
  int r = 15;
  int k = 2;

  // Function call
  findKthElement(l, r, k);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Function to calculate
// the cost
function func(n,dp)
{
    let count = 0;

  // Base case
  if (n == 2 ||
      n == 1)
    return 1;

  if (dp[n] != -1)
    return dp[n];

  // Even condition
  if (n % 2 == 0)
    count = 1 + func(Math.floor(n / 2), dp);

  // Odd condition
  if (n % 2 != 0)
    count = 1 + func(n * 3 +
                     1, dp);

  // Store the result
  dp[n] = count;
  return dp[n];
}

// Function to find Kth element
function findKthElement(l,r,k)
{
    // Array to store the
  // results
  let result = [];

  // Define DP array
  let dp = new Array(r + 1);
  dp[1] = 1;
  dp[2] = 1;

  for(let i = l; i <= r; i++)
    result.push([i,
               func(i, dp)]);

  // Sort the array based
  // on cost
  result.sort(function(a,b){return a[0]-b[0];});

  document.write(
  result[k-1][0]);
}

// Driver code
// Given range and K
let l = 12;
let r = 15;
let k = 2;

// Function call
findKthElement(l, r, k);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*