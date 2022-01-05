# 基于给定条件的范围和查询

> 原文:[https://www . geesforgeks . org/range-sum-query-基于给定条件/](https://www.geeksforgeeks.org/range-sum-queries-based-on-given-conditions/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和由 **Q** 个查询组成的矩阵**查询的形式为 **{m，a，b}** 。对于每个查询，任务是根据以下条件找到数组元素的总和:**

*   **如果 m = 1:** 求范围内数组元素的和**【a，b】**。
*   **如果 m = 2:** 按照递增的顺序重新排列数组元素，找到新数组中**【a，b】**范围内的元素之和。

**示例:**

> **输入** : arr[] = {6，4，2，7，2，7}，Q = 3，*查询[][3] = {{2，3，6}，{1，3，4}，{1，1，6}}*
> **输出** : 24 9 28
> **解释:
> 对于查询 1:
> m 为 2，则排序后的数组为 arr[] = {2，2，4，6，7
> 对于查询 2:
> m 为 1，则原始数组为 arr[] = {6，4，2，7，2，7}，范围[3，4]内的元素之和为 2 + 7 = 9。
> 对于查询 3:
> m 为 1，则原始数组为 arr[] = {6，4，2，7，2，7}，范围[1，6]内元素之和为 6 + 4 + 2 + 7 + 2 + 7 = 28。**
> 
> **输入** : arr[] = {5，5，2，3}，Q = 3，*查询[][10] = {{1，2，4}，{2，1，4}，{1，1，1}，{2，1，4}，{2，1，2}，{1，1，1}，{1，3，3}，{1，1，3}，{1，4，4}，{1，2，2 } }*
> T5】输出【T6

**朴素方法:**思想是遍历给定的查询，根据给定的条件找到所有元素的和:

1.  根据给定的 m 选择数组，如果 **m 等于 1** 则选择原始数组，否则选择另一个数组，在该数组中所有元素 **arr[]** 被排序。
2.  现在计算范围**【a，b】**之间的数组之和。
3.  在该范围内循环迭代以找到总和。
4.  打印每个查询的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// between the given range as per
// value of m
int range_sum(vector<int> v, int a,
              int b)
{
    // Stores the sum
    int sum = 0;

    // Loop to calculate the sum
    for (int i = a - 1; i < b; i++) {
        sum += v[i];
    }

    // Return sum
    return sum;
}

// Function to find the sum of elements
// for each query
void findSum(vector<int>& v1, int q,
             int Queries[][3])
{
    // Take a dummy vector
    vector<int> v2;

    // Size of vector
    int n = sizeof(v1) / sizeof(int);

    // Copying the elements into
    // dummy vector
    for (int i = 0; i < n; i++) {
        v2.push_back(v1[i]);
    }

    // Sort the dummy vector
    sort(v2.begin(), v2.end());

    // Performs operations
    for (int i = 0; i < q; i++) {

        int m = Queries[i][0];
        int a = Queries[i][1];
        int b = Queries[i][2];

        if (m == 1) {

            // Function Call to find sum
            cout << range_sum(v1, a, b)
                 << ' ';
        }
        else if (m == 2) {

            // Function Call to find sum
            cout << range_sum(v2, a, b)
                 << ' ';
        }
    }
}

// Driver Code
int main()
{
    // Given arr[]
    vector<int> arr = { 6, 4, 2, 7, 2, 7 };

    int Q = 1;

    // Given Queries
    int Queries[][3] = { { 2, 3, 6 } };

    // Function Call
    findSum(arr, Q, Queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate the sum
// between the given range as per
// value of m
static int range_sum(Vector<Integer> v, int a,
                                        int b)
{

    // Stores the sum
    int sum = 0;

    // Loop to calculate the sum
    for(int i = a - 1; i < b; i++)
    {
        sum += v.get(i);
    }

    // Return sum
    return sum;
}

static int range_sum(int []v, int a,
                     int b)
{

    // Stores the sum
    int sum = 0;

    // Loop to calculate the sum
    for(int i = a - 1; i < b; i++)
    {
        sum += v[i];
    }

    // Return sum
    return sum;
}

// Function to find the sum of elements
// for each query
static void findSum(int []v1, int q,
                    int Queries[][])
{

    // Take a dummy vector
    Vector<Integer> v2 = new Vector<Integer>();

    // Size of vector
    int n = v1.length;

    // Copying the elements into
    // dummy vector
    for(int i = 0; i < n; i++)
    {
        v2.add(v1[i]);
    }

    // Sort the dummy vector
    Collections.sort(v2);

    // Performs operations
    for(int i = 0; i < q; i++)
    {
        int m = Queries[i][0];
        int a = Queries[i][1];
        int b = Queries[i][2];

        if (m == 1)
        {

            // Function call to find sum
            System.out.print(range_sum(
                v1, a, b) + " ");
        }
        else if (m == 2)
        {

            // Function call to find sum
            System.out.print(range_sum(
                v2, a, b) + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given arr[]
    int []arr = { 6, 4, 2, 7, 2, 7 };

    int Q = 1;

    // Given Queries
    int Queries[][] = { { 2, 3, 6 } };

    // Function call
    findSum(arr, Q, Queries);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the sum
# between the given range as per
# value of m
def range_sum(v, a, b):

    # Stores the sum
    Sum = 0

    # Loop to calculate the sum
    for i in range(a - 1, b):
        Sum += v[i]

    # Return sum
    return Sum

# Function to find the sum of elements
# for each query
def findSum(v1, q, Queries):

    # Take a dummy vector
    v2 = []

    # Size of vector
    n = len(v1)

    # Copying the elements into
    # dummy vector
    for i in range(n):
        v2.append(v1[i])

    # Sort the dummy vector
    v2.sort()

    # Performs operations
    for i in range(q):
        m = Queries[i][0]
        a = Queries[i][1]
        b = Queries[i][2]

        if (m == 1):

            # Function call to find sum
            print(range_sum(v1, a, b), end = " ")

        elif (m == 2):

            # Function call to find sum
            print(range_sum(v2, a, b), end = " ")

# Driver code

# Given arr[]
arr = [ 6, 4, 2, 7, 2, 7 ]

Q = 1

# Given Queries
Queries = [ [ 2, 3, 6 ] ]

# Function call
findSum(arr, Q, Queries)

# This code is contributed divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;
using System.Text;

class GFG{

// Function to calculate the sum
// between the given range as per
// value of m
static int range_sum(ArrayList v, int a,
                                  int b)
{

    // Stores the sum
    int sum = 0;

    // Loop to calculate the sum
    for(int i = a - 1; i < b; i++)
    {
        sum += (int)v[i];
    }

    // Return sum
    return sum;
}

// Function to find the sum of elements
// for each query
static void findSum(ArrayList v1, int q,
                    int [,]Queries)
{

    // Take a dummy vector
    ArrayList v2 = new ArrayList();

    // Size of vector
    int n = v1.Count;

    // Copying the elements into
    // dummy vector
    for(int i = 0; i < n; i++)
    {
        v2.Add(v1[i]);
    }

    // Sort the dummy vector
    v2.Sort();

    // Performs operations
    for(int i = 0; i < q; i++)
    {
        int m = Queries[i, 0];
        int a = Queries[i, 1];
        int b = Queries[i, 2];

        if (m == 1)
        {

            // Function call to find sum
            Console.Write(range_sum(v1, a, b));
            Console.Write(' ');
        }
        else if (m == 2)
        {

            // Function call to find sum
            Console.Write(range_sum(v2, a, b));
            Console.Write(' ');
        }
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given arr[]
    ArrayList arr=new ArrayList(){ 6, 4, 2,
                                   7, 2, 7 };

    int Q = 1;

    // Given Queries
    int [,]Queries = { { 2, 3, 6 } };

    // Function call
    findSum(arr, Q, Queries);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the sum
// between the given range as per
// value of m
function range_sum(v, a, b)
{

    // Stores the sum
    let sum = 0;

    // Loop to calculate the sum
    for(let i = a - 1; i < b; i++)
    {
        sum += v[i];
    }

    // Return sum
    return sum;
}

// Function to find the sum of elements
// for each query
function findSum(v1, q, Queries)
{

    // Take a dummy vector
    let v2 = [];

    // Size of vector
    let n = v1.length;

    // Copying the elements into
    // dummy vector
    for(let i = 0; i < n; i++)
    {
        v2.push(v1[i]);
    }

    // Sort the dummy vector
    v2.sort(function(a, b){return a - b;});

    // Performs operations
    for(let i = 0; i < q; i++)
    {
        let m = Queries[i][0];
        let a = Queries[i][1];
        let b = Queries[i][2];

        if (m == 1)
        {

            // Function call to find sum
            document.write(range_sum(
                v1, a, b) + " ");
        }
        else if (m == 2)
        {

            // Function call to find sum
            document.write(range_sum(
                v2, a, b) + " ");
        }
    }
}

// Driver Code

// Given arr[]
let arr = [ 6, 4, 2, 7, 2, 7 ];
let Q = 1;

// Given Queries
let Queries = [ [ 2, 3, 6 ] ];

// Function call
findSum(arr, Q, Queries);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
24
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以通过使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)减少一个循环来优化。以下是步骤:

*   创建另一个数组 **brr[]** 以按排序顺序存储给定数组 **arr[]** 的元素。
*   求数组 **arr[]** 和 **brr[]** 的前缀和。
*   遍历给定的查询，如果查询类型为 1，则范围[a，b]内元素的总和由下式给出:

> arr[b–1]–arr[a–2]

*   如果查询类型为 2，则范围[a，b]内元素的总和由下式给出:

> brr[B- 1]-arr[a-2]

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// between the given range as per
// value of m
int range_sum(vector<int>& arr, int a,
              int b)
{
    // Stores the sum
    int sum = 0;

    // Condition for a to print the
    // sum between ranges [a, b]
    if (a - 2 < 0)
        sum = arr[b - 1];
    else
        sum = arr[b - 1] - arr[a - 2];

    // Return sum
    return sum;
}

// Function to precalculate the sum
// of both the vectors
void precompute_sum(vector<int>& arr,
                    vector<int>& brr)
{
    int N = (int)arr.size();

    // Make Prefix sum array
    for (int i = 1; i <= N; i++) {
        arr[i] = arr[i] + arr[i - 1];
        brr[i] = brr[i] + brr[i - 1];
    }
}

// Function to compute the result
// for each query
void find_sum(vector<int>& arr, int q,
              int Queries[][3])
{
    // Take a dummy vector and copy
    // the element of arr in brr
    vector<int> brr(arr);

    int N = (int)arr.size();

    // Sort the dummy vector
    sort(brr.begin(), brr.end());

    // Compute prefix sum of both vectors
    precompute_sum(arr, brr);

    // Performs operations
    for (int i = 0; i < q; i++) {

        int m = Queries[i][0];
        int a = Queries[i][1];
        int b = Queries[i][2];

        if (m == 1) {

            // Function Call to find sum
            cout << range_sum(arr, a, b)
                 << ' ';
        }
        else if (m == 2) {

            // Function Call to find sum
            cout << range_sum(brr, a, b)
                 << ' ';
        }
    }
}

// Driver Code
int main()
{
    // Given arr[]
    vector<int> arr = { 0, 6, 4, 2, 7, 2, 7 };

    // Number of queries
    int Q = 1;

    // Given queries
    int Queries[][3] = { { 2, 3, 6 } };

    // Function Call
    find_sum(arr, Q, Queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate the sum
// between the given range as per
// value of m
static int range_sum(int []arr, int a,
                     int b)
{

    // Stores the sum
    int sum = 0;

    // Condition for a to print the
    // sum between ranges [a, b]
    if (a - 2 < 0)
        sum = arr[b - 1];
    else
        sum = arr[b - 1] - arr[a - 2];

    // Return sum
    return sum;
}

// Function to precalculate the sum
// of both the vectors
static void precompute_sum(int []arr,
                           int []brr)
{
    int N = (int)arr.length;

    // Make Prefix sum array
    for(int i = 1; i < N; i++)
    {
        arr[i] = arr[i] + arr[i - 1];
        brr[i] = brr[i] + brr[i - 1];
    }
}

// Function to compute the result
// for each query
static void find_sum(int []arr, int q,
                     int Queries[][])
{

    // Take a dummy vector and copy
    // the element of arr in brr
    int []brr = arr.clone();

    int N = (int)arr.length;

    // Sort the dummy vector
    Arrays.sort(brr);

    // Compute prefix sum of both vectors
    precompute_sum(arr, brr);

    // Performs operations
    for(int i = 0; i < q; i++)
    {
        int m = Queries[i][0];
        int a = Queries[i][1];
        int b = Queries[i][2];

        if (m == 1)
        {

            // Function call to find sum
            System.out.print(range_sum(
                arr, a, b) + " ");
        }
        else if (m == 2)
        {

            // Function call to find sum
            System.out.print(range_sum(
                brr, a, b) + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given arr[]
    int []arr = { 0, 6, 4, 2, 7, 2, 7 };

    // Number of queries
    int Q = 1;

    // Given queries
    int Queries[][] = { { 2, 3, 6 } };

    // Function call
    find_sum(arr, Q, Queries);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to calculate
# the sum between the
# given range as per value
# of m
def range_sum(arr, a, b):

    # Stores the sum
    sum = 0

    # Condition for a to
    # print the sum between
    # ranges [a, b]
    if (a - 2 < 0):
        sum = arr[b - 1]
    else:
        sum = (arr[b - 1] -
               arr[a - 2])

    # Return sum
    return sum

# Function to precalculate
# the sum of both the vectors
def precompute_sum(arr, brr):

    N = len(arr)

    # Make Prefix sum array
    for i in range(1, N):
        arr[i] = arr[i] + arr[i - 1]
        brr[i] = brr[i] + brr[i - 1]

# Function to compute
# the result for each query
def find_sum(arr, q, Queries):

    # Take a dummy vector
    # and copy the element
    # of arr in brr
    brr = arr.copy()

    N = len(arr)

    # Sort the dummy vector
    brr.sort()

    # Compute prefix sum of
    # both vectors
    precompute_sum(arr, brr)

    # Performs operations
    for i in range(q):

        m = Queries[i][0]
        a = Queries[i][1]
        b = Queries[i][2]

        if (m == 1):

            # Function Call to
            # find sum
            print (range_sum(arr,
                             a, b),
                   end = ' ')

        elif (m == 2):

            # Function Call to
            # find sum
            print (range_sum(brr,
                             a, b),
                   end = ' ')

# Driver Code
if __name__ == "__main__":

    # Given arr[]
    arr = [0, 6, 4,
           2, 7, 2, 7]

    # Number of queries
    Q = 1

    # Given queries
    Queries = [[2, 3, 6]]

    # Function Call
    find_sum(arr, Q, Queries)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to calculate the sum
// between the given range as per
// value of m
static int range_sum(int []arr,
                     int a,
                     int b)
{
  // Stores the sum
  int sum = 0;

  // Condition for a to print the
  // sum between ranges [a, b]
  if (a - 2 < 0)
    sum = arr[b - 1];
  else
    sum = arr[b - 1] - arr[a - 2];

  // Return sum
  return sum;
}

// Function to precalculate the sum
// of both the vectors
static void precompute_sum(int []arr,
                           int []brr)
{
  int N = (int)arr.Length;

  // Make Prefix sum array
  for(int i = 1; i < N; i++)
  {
    arr[i] = arr[i] + arr[i - 1];
    brr[i] = brr[i] + brr[i - 1];
  }
}

// Function to compute the result
// for each query
static void find_sum(int []arr, int q,
                     int [,]Queries)
{   
  // Take a dummy vector and copy
  // the element of arr in brr
  int []brr = new int[arr.Length];
  arr.CopyTo(brr, 0);

  int N = (int)arr.Length;

  // Sort the dummy vector
  Array.Sort(brr);

  // Compute prefix sum of both vectors
  precompute_sum(arr, brr);

  // Performs operations
  for(int i = 0; i < q; i++)
  {
    int m = Queries[i, 0];
    int a = Queries[i, 1];
    int b = Queries[i, 2];

    if (m == 1)
    {
      // Function call to find sum
      Console.Write(range_sum(
                    arr, a, b) + " ");
    }
    else if (m == 2)
    {
      // Function call to find sum
      Console.Write(range_sum(
                    brr, a, b) + " ");
    }
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given []arr
  int []arr = {0, 6, 4, 2, 7, 2, 7};

  // Number of queries
  int Q = 1;

  // Given queries
  int [,]Queries = {{2, 3, 6}};

  // Function call
  find_sum(arr, Q, Queries);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate the sum
// between the given range as per
// value of m
function range_sum(arr,a,b)
{
    // Stores the sum
    let sum = 0;

    // Condition for a to print the
    // sum between ranges [a, b]
    if (a - 2 < 0)
        sum = arr[b - 1];
    else
        sum = arr[b - 1] - arr[a - 2];

    // Return sum
    return sum;
}

// Function to precalculate the sum
// of both the vectors
function precompute_sum(arr,brr)
{
    let N = arr.length;

    // Make Prefix sum array
    for(let i = 1; i < N; i++)
    {
        arr[i] = arr[i] + arr[i - 1];
        brr[i] = brr[i] + brr[i - 1];
    }
}

// Function to compute the result
// for each query
function find_sum(arr,q,Queries)
{
    // Take a dummy vector and copy
    // the element of arr in brr
    let brr = [...arr];

    let N = arr.length;

    // Sort the dummy vector
    brr.sort(function(a,b){return a-b;});

    // Compute prefix sum of both vectors
    precompute_sum(arr, brr);

    // Performs operations
    for(let i = 0; i < q; i++)
    {
        let m = Queries[i][0];
        let a = Queries[i][1];
        let b = Queries[i][2];

        if (m == 1)
        {

            // Function call to find sum
            document.write(range_sum(
                arr, a, b) + " ");
        }
        else if (m == 2)
        {

            // Function call to find sum
            document.write(range_sum(
                brr, a, b) + " ");
        }
    }
}

// Driver Code
let arr=[0, 6, 4, 2, 7, 2, 7];
// Number of queries
let Q = 1;

// Given queries
let Queries = [[ 2, 3, 6 ]];

// Function call
find_sum(arr, Q, Queries);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*