# 检查一个数组是否可以拆分成 3 个和相等的子序列

> 原文:[https://www . geesforgeks . org/check-if-a-array-can-split-in-3-subseries-of-equal-sum-or-not/](https://www.geeksforgeeks.org/check-if-an-array-can-be-split-into-3-subsequences-of-equal-sum-or-not/)

给定一个具有 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是确定数组是否可以被分成 3 个子序列，它们的和是否相等。如果是，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {1，1，1}
> **输出:**是
> **说明:**
> 这里的数组可以分割成 3 等份和。{1}
> 
> **输入:** arr[] = {40}
> **输出:**否
> **说明:**
> 此处数组不能分割成 3 等份和。

**递归方式:**这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)解决。以下是步骤:

1.  将三个变量 **sum1** 、 **sum2** 和 **sum3** 初始化为值 0。
2.  然后将数组**arr【】**的每个元素添加到这 3 个变量中的任何一个，给出所有可能的组合。
3.  在这种情况下，任何具有 3 个相等和的子序列都可以对数组进行划分。
4.  如果阵列可以分区，则打印“**是”**否则打印“**否”**。

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to check array can
// be partition to 3 subsequences of
// equal sum or not
int checkEqualSumUtil(int arr[], int N,
                      int sm1, int sm2,
                      int sm3, int j)
{   
  // Base Case
  if (j == N)
  {
    if (sm1 == sm2 && sm2 == sm3)
      return 1;
    else
      return 0;
  }

  else
  {
    // When element at index
    // j is added to sm1
    int l = checkEqualSumUtil(arr, N,
                              sm1 + arr[j],
                              sm2, sm3, j + 1);

    // When element at index
    // j is added to sm2
    int m = checkEqualSumUtil(arr, N, sm1,
                              sm2 + arr[j],
                              sm3, j + 1);

    // When element at index
    // j is added to sm3
    int r = checkEqualSumUtil(arr, N, sm1, sm2,
                              sm3 + arr[j], j + 1);

    // Return maximum value among
    // all above 3 recursive call
    return max(max(l, m), r);
  }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
void checkEqualSum(int arr[], int N)
{
  // Initialise 3 sums to 0
  int sum1, sum2, sum3;

  sum1 = sum2 = sum3 = 0;

  // Function Call
  if (checkEqualSumUtil(arr, N, sum1,
                        sum2, sum3, 0)== 1)
  {
    cout << "Yes";
  }
  else
  {
    cout << "No";
  }
}

// Driver Code
int main()
{
  // Given array arr[]
  int arr[] = {17, 34, 59, 23, 17, 67,
               57, 2, 18, 59, 1 };

  int N = sizeof(arr) / sizeof(arr[0]);

  // Function Call
  checkEqualSum(arr, N);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Utility function to check array can
// be partition to 3 subsequences of
// equal sum or not
static int checkEqualSumUtil(int arr[], int N,
                             int sm1, int sm2,
                             int sm3, int j)
{
  // Base Case
  if (j == N)
  {
    if (sm1 == sm2 && sm2 == sm3)
      return 1;
    else
      return 0;
  }
  else
  {
    // When element at index
    // j is added to sm1
    int l = checkEqualSumUtil(arr, N,
                              sm1 + arr[j],
                              sm2, sm3, j + 1);

    // When element at index
    // j is added to sm2
    int m = checkEqualSumUtil(arr, N, sm1,
                              sm2 + arr[j],
                              sm3, j + 1);

    // When element at index
    // j is added to sm3
    int r = checkEqualSumUtil(arr, N, sm1, sm2,
                              sm3 + arr[j], j + 1);

    // Return maximum value among
    // all above 3 recursive call
    return Math.max(Math.max(l, m), r);
  }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
static void checkEqualSum(int arr[], int N)
{
  // Initialise 3 sums to 0
  int sum1, sum2, sum3;

  sum1 = sum2 = sum3 = 0;

  // Function Call
  if (checkEqualSumUtil(arr, N, sum1,
                        sum2, sum3, 0) == 1)
  {
    System.out.print("Yes");
  }
  else
  {
    System.out.print("No");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {17, 34, 59, 23, 17,
               67, 57, 2, 18, 59, 1};       

  int N = arr.length;

  // Function Call
  checkEqualSum(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Utility function to check array can
# be partition to 3 subsequences of
# equal sum or not
def checkEqualSumUtil(arr, N, sm1, sm2, sm3, j):

    # Base case
    if j == N:
        if sm1 == sm2 and sm2 == sm3:
            return 1
        else:
            return 0
    else:

        # When element at index
        # j is added to sm1
        l = checkEqualSumUtil(arr, N, sm1 + arr[j],
                              sm2, sm3, j + 1)

        # When element at index
        # j is added to sm2
        m = checkEqualSumUtil(arr, N, sm1,
                              sm2 + arr[j],
                              sm3, j + 1)

        # When element at index
        # j is added to sm3
        r = checkEqualSumUtil(arr, N, sm1,
                              sm2, sm3 + arr[j],
                                     j + 1)

        # Return maximum value among
        # all above 3 recursive call
        return max(l, m, r)

# Function to check array can be
# partition to 3 subsequences of
# equal sum or not
def checkEqualSum(arr, N):

    # Initialise 3 sums to 0
    sum1 = sum2 = sum3 = 0

    # Function call
    if checkEqualSumUtil(arr, N, sum1,
                         sum2, sum3, 0) == 1:
        print("Yes")
    else:
        print("No")

# Driver code

# Given array arr[]
arr = [ 17, 34, 59, 23, 17,
        67, 57, 2, 18, 59, 1 ]
N = len(arr)

# Function call
checkEqualSum(arr, N)

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Utility function to check array can
// be partition to 3 subsequences of
// equal sum or not
static int checkEqualSumUtil(int[] arr, int N,
                             int sm1, int sm2,
                             int sm3, int j)
{
  // Base Case
  if (j == N)
  {
    if (sm1 == sm2 && sm2 == sm3)
      return 1;
    else
      return 0;
  }
  else
  {
    // When element at index
    // j is added to sm1
    int l = checkEqualSumUtil(arr, N,
                              sm1 + arr[j],
                              sm2, sm3, j + 1);

    // When element at index
    // j is added to sm2
    int m = checkEqualSumUtil(arr, N, sm1,
                              sm2 + arr[j],
                              sm3, j + 1);

    // When element at index
    // j is added to sm3
    int r = checkEqualSumUtil(arr, N,
                              sm1, sm2,
                              sm3 + arr[j],
                              j + 1);

    // Return maximum value among
    // all above 3 recursive call
    return Math.Max(Math.Max(l, m), r);
  }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
static void checkEqualSum(int[] arr, int N)
{

  // Initialise 3 sums to 0
  int sum1, sum2, sum3;
  sum1 = sum2 = sum3 = 0;

  // Function Call
  if (checkEqualSumUtil(arr, N, sum1,
                        sum2, sum3, 0) == 1)
  {
    Console.Write("Yes");
  }
  else
  {
    Console.Write("No");
  }
}

// Driver Code
public static void Main()
{
  // Given array arr[]
  int[] arr = {17, 34, 59, 23, 17,
               67, 57, 2, 18, 59, 1};
  int N = arr.Length;

  // Function Call
  checkEqualSum(arr, N);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Java script program for
// the above approach

// Utility function to check array can
// be partition to 3 subsequences of
// equal sum or not
function checkEqualSumUtil( arr,  N,
                             sm1,  sm2,
                             sm3,  j)
{
// Base Case
if (j == N)
{
    if (sm1 == sm2 && sm2 == sm3)
    return 1;
    else
    return 0;
}
else
{
    // When element at index
    // j is added to sm1
    let l = checkEqualSumUtil(arr, N,
                            sm1 + arr[j],
                            sm2, sm3, j + 1);

    // When element at index
    // j is added to sm2
    let m = checkEqualSumUtil(arr, N, sm1,
                            sm2 + arr[j],
                            sm3, j + 1);

    // When element at index
    // j is added to sm3
    let r = checkEqualSumUtil(arr, N, sm1, sm2,
                            sm3 + arr[j], j + 1);

    // Return maximum value among
    // all above 3 recursive call
    return Math.max(Math.max(l, m), r);
}
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
function checkEqualSum(arr,N)
{
// Initialise 3 sums to 0
let sum1, sum2, sum3;

sum1 = sum2 = sum3 = 0;

// Function Call
if (checkEqualSumUtil(arr, N, sum1,
                        sum2, sum3, 0) == 1)
{
    document.write("Yes");
}
else
{
    document.write("No");
}
}

// Driver Code

// Given array arr[]
let arr = [17, 34, 59, 23, 17,
            67, 57, 2, 18, 59, 1];   

let N = arr.length;

// Function Call
checkEqualSum(arr, N);

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(3<sup>N</sup>)*
***辅助空间:** O(1)*

[**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) **方法:**这个问题可以使用动态规划来解决，其思想是将所有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)的值存储在一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，并使用[重叠子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)的值来减少递归调用的次数。以下是步骤:

*   让 **sum1** 、 **sum2** 、 **sum3** 为三个相等的和进行分割。
*   创建一个有钥匙的地图 **dp** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   **基本情况:**在遍历数组时，如果我们到达数组的末尾，那么检查 **sum1** 、 **sum2** 和 **sum3** 的值是否相等，然后返回 1，这将确保我们能够将给定的数组分解成具有相等和值的子序列。否则，返回 0。
    *   **递归调用:**对于数组中的每个元素，逐个包含 **sum1** 、 **sum2** 和 **sum3** 中的每个元素，并返回这些递归调用的最大值。

> a =递归 _ 函数(arr，N，sum1 + arr[j]，sum2，sum3，j + 1)
> b =递归 _ 函数(arr，N，sum1，sum2 + arr[j]，sum3，j + 1)
> c =递归 _ 函数(arr，N，sum1，sum2，sum3 + arr[j]，j + 1)

*   **Return 语句:**在上面的递归调用中，三个值的最大值将给出当前递归调用的结果。将 [dp 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)中的当前状态更新为:

> 字符串 s = to _ string(sum 1)+' _ '+to _ string(sum 2)+to _ string(j)
> 返回 dp[s] = max(a，max(b，c))

*   如果有分区可能，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
map<string, int> dp;

// Function to check array can be
// partition into sum of 3 equal
int checkEqualSumUtil(int arr[], int N,
                      int sm1,
                      int sm2,
                      int sm3, int j)
{
    string s = to_string(sm1)
               + "_" + to_string(sm2)
               + to_string(j);

    // Base Case
    if (j == N) {
        if (sm1 == sm2 && sm2 == sm3)
            return 1;
        else
            return 0;
    }

    // If value at particular index is not
    // -1 then return value at that index
    // which ensure no more further calls
    if (dp.find(s) != dp.end())
        return dp[s];

    else {

        // When element at index
        // j is added to sm1
        int l = checkEqualSumUtil(
            arr, N, sm1 + arr[j],
            sm2, sm3, j + 1);

        // When element at index
        // j is added to sm2
        int m = checkEqualSumUtil(
            arr, N, sm1, sm2 + arr[j],
            sm3, j + 1);

        // When element at index
        // j is added to sm3
        int r = checkEqualSumUtil(
            arr, N, sm1, sm2,
            sm3 + arr[j], j + 1);

        // Update the current state and
        // return that value
        return dp[s] = max(max(l, m), r);
    }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
void checkEqualSum(int arr[], int N)
{
    // Initialise 3 sums to 0
    int sum1, sum2, sum3;

    sum1 = sum2 = sum3 = 0;

    // Function Call
    if (checkEqualSumUtil(
            arr, N, sum1,
            sum2, sum3, 0)
        == 1) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[]
        = { 17, 34, 59, 23, 17, 67,
            57, 2, 18, 59, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    checkEqualSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{
static HashMap<String,
               Integer> dp = new HashMap<String,
                                         Integer>();

// Function to check array can be
// partition into sum of 3 equal
static int checkEqualSumUtil(int arr[], int N,
                             int sm1, int sm2,
                             int sm3, int j)
{
  String s = String.valueOf(sm1) + "_" +
  String.valueOf(sm2) + String.valueOf(j);

  // Base Case
  if (j == N)
  {
    if (sm1 == sm2 && sm2 == sm3)
      return 1;
    else
      return 0;
  }

  // If value at particular index is not
  // -1 then return value at that index
  // which ensure no more further calls
  if (dp.containsKey(s))
    return dp.get(s);

  else
  {
    // When element at index
    // j is added to sm1
    int l = checkEqualSumUtil(arr, N, sm1 + arr[j],
                              sm2, sm3, j + 1);

    // When element at index
    // j is added to sm2
    int m = checkEqualSumUtil(arr, N, sm1,
                              sm2 + arr[j],
                              sm3, j + 1);

    // When element at index
    // j is added to sm3
    int r = checkEqualSumUtil(arr, N, sm1, sm2,
                              sm3 + arr[j], j + 1);

    // Update the current state and
    // return that value
    dp.put(s, Math.max(Math.max(l, m), r));
    return dp.get(s);
  }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
static void checkEqualSum(int arr[], int N)
{
  // Initialise 3 sums to 0
  int sum1, sum2, sum3;

  sum1 = sum2 = sum3 = 0;

  // Function Call
  if (checkEqualSumUtil(arr, N, sum1,
                        sum2, sum3, 0) == 1)
  {
    System.out.print("Yes");
  }
  else
  {
    System.out.print("No");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {17, 34, 59, 23, 17,
               67, 57, 2, 18, 59, 1};

  int N = arr.length;

  // Function Call
  checkEqualSum(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
dp = {}

# Function to check array can be
# partition into sum of 3 equal
def checkEqualSumUtil(arr, N, sm1, sm2, sm3, j):

    s = str(sm1) + "_" + str(sm2) + str(j)

    # Base Case
    if j == N:
        if sm1 == sm2 and sm2 == sm3:
            return 1
        else:
            return 0

    # If value at particular index is not
    # -1 then return value at that index
    # which ensure no more further calls
    if s in dp:
        return dp[s]

    # When element at index
    # j is added to sm1
    l = checkEqualSumUtil(arr, N, sm1 + arr[j],
                          sm2, sm3, j + 1)

    # When element at index
    # j is added to sm2
    m = checkEqualSumUtil(arr, N, sm1,
                          sm2 + arr[j], sm3,
                            j + 1)

    # When element at index
    # j is added to sm3
    r = checkEqualSumUtil(arr, N, sm1,
                          sm2, sm3 + arr[j],
                                 j + 1)

    # Update the current state and
    # return that value
    dp[s] = max(l, m, r)

    return dp[s]

# Function to check array can be
# partition to 3 subsequences of
# equal sum or not
def checkEqualSum(arr, N):

    # Initialise 3 sums to 0
    sum1 = sum2 = sum3 = 0

    # Function Call
    if checkEqualSumUtil(arr, N, sum1,
                         sum2, sum3, 0) == 1:
        print("Yes")
    else:
        print("No")

# Driver code

# Given array arr[]
arr = [ 17, 34, 59, 23, 17,
        67, 57, 2, 18, 59, 1 ]
N = len(arr)

# Function call
checkEqualSum(arr, N)

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static Dictionary<string,
                  int> dp = new Dictionary<string,
                                           int>();

// Function to check array can be
// partition into sum of 3 equal
static int checkEqualSumUtil(int []arr, int N,
                             int sm1, int sm2,
                             int sm3, int j)
{
    string s = sm1.ToString() + "_" +
               sm2.ToString() + j.ToString();

    // Base Case
    if (j == N)
    {
        if (sm1 == sm2 && sm2 == sm3)
            return 1;
        else
            return 0;
    }

    // If value at particular index is not
    // -1 then return value at that index
    // which ensure no more further calls
    if (dp.ContainsKey(s))
        return dp[s];

    else
    {

        // When element at index
        // j is added to sm1
        int l = checkEqualSumUtil(arr, N, sm1 + arr[j],
                                  sm2, sm3, j + 1);

        // When element at index
        // j is added to sm2
        int m = checkEqualSumUtil(arr, N, sm1,
                                  sm2 + arr[j],
                                  sm3, j + 1);

        // When element at index
        // j is added to sm3
        int r = checkEqualSumUtil(arr, N, sm1, sm2,
                                  sm3 + arr[j], j + 1);

        // Update the current state and
        // return that value
        dp[s] = Math.Max(Math.Max(l, m), r);

        return dp[s];
    }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
static void checkEqualSum(int []arr, int N)
{

    // Initialise 3 sums to 0
    int sum1, sum2, sum3;

    sum1 = sum2 = sum3 = 0;

    // Function call
    if (checkEqualSumUtil(arr, N, sum1,
                          sum2, sum3, 0) == 1)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 17, 34, 59, 23, 17,
                  67, 57, 2, 18, 59, 1 };

    int N = arr.Length;

    // Function call
    checkEqualSum(arr, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
var dp = new Map();

// Function to check array can be
// partition into sum of 3 equal
function checkEqualSumUtil(arr, N, sm1, sm2, sm3, j)
{
    var s = (sm1.toString())
               + "_" + (sm2.toString())
               + (j.toString());

    // Base Case
    if (j == N) {
        if (sm1 == sm2 && sm2 == sm3)
            return 1;
        else
            return 0;
    }

    // If value at particular index is not
    // -1 then return value at that index
    // which ensure no more further calls
    if (dp.has(s))
        return dp[s];

    else {

        // When element at index
        // j is added to sm1
        var l = checkEqualSumUtil(
            arr, N, sm1 + arr[j],
            sm2, sm3, j + 1);

        // When element at index
        // j is added to sm2
        var m = checkEqualSumUtil(
            arr, N, sm1, sm2 + arr[j],
            sm3, j + 1);

        // When element at index
        // j is added to sm3
        var r = checkEqualSumUtil(
            arr, N, sm1, sm2,
            sm3 + arr[j], j + 1);

        // Update the current state and
        // return that value
        return dp[s] = Math.max(Math.max(l, m), r);
    }
}

// Function to check array can be
// partition to 3 subsequences of
// equal sum or not
function checkEqualSum(arr, N)
{
    // Initialise 3 sums to 0
    var sum1, sum2, sum3;

    sum1 = sum2 = sum3 = 0;

    // Function Call
    if (checkEqualSumUtil(
            arr, N, sum1,
            sum2, sum3, 0)
        == 1) {
        document.write( "Yes");
    }
    else {
        document.write( "No");
    }
}

// Driver Code

// Given array arr[]
var arr
    = [17, 34, 59, 23, 17, 67,
        57, 2, 18, 59, 1];
var N = arr.length;

// Function Call
checkEqualSum(arr, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N * K<sup>2</sup>)*
***辅助空间:** O(N*K <sup>2</sup> )其中 K 为数组的和。*

> (**to _ string**(sum 1)+“_”+**to _ string**(sum 2)+“_”+**to _ string**(sum 3))

*   如果找到 3 个相等的子集，则值为 **1** ，否则值为 **0** 。