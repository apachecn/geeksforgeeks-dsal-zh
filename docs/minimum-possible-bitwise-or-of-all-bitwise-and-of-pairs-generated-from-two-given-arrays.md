# 从两个给定数组生成的所有对的按位“与”的最小可能按位“或”

> 原文:[https://www . geeksforgeeks . org/从两个给定数组生成的最小可能位或对的位和对/](https://www.geeksforgeeks.org/minimum-possible-bitwise-or-of-all-bitwise-and-of-pairs-generated-from-two-given-arrays/)

给定两个长度分别为 **N** 和 **M** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **brr[]** ，使用以下操作创建一个长度为 **N** 的数组 **res[]** ，使得数组**RES[**中所有元素的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)最小。

*   对于**arr【】**中的每个索引 I，从数组**brr【】**中选择任意索引 **j** ( *允许重复次数*，并更新 **res[i] = arr[i] & brr[j]**

任务是打印数组元素**RES【】**的最小可能位或值。

**示例:**

> **输入:** arr[] = {2，1}，brr[] = {4，6，7}
> **输出:** 0
> **解释:**
> 对于数组 arr[] = {2，1}，从 brr[]中选择值作为{4，4}或{4，6}。
> 因此，结果数组变为{0，0}，结果数组的按位 OR = 0，这是最小可能值。
> 
> **输入:** arr[] = {1，2，3}，brr[] = {7，15}
> **输出:** 3
> **解释:**
> 对于数组 arr[] = {1，2，3}，从 brr[]中选择值作为{7，7，7}。
> 因此，结果数组变为{1，2，3}，结果数组的按位 OR = 3。

**简单方法:**最简单的方法是用**brr【】**生成[所有可能的数组对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)**arr【】**的[位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。完成上述步骤后，只选择按位“或”最小的那些 **N** 元素。打印最小位或。

***时间复杂度:**O(2<sup>(N * M)</sup>)*
***辅助空间:** O(1)*

**高效法:**对上述方法进行优化，思路是从最大可能的答案开始，然后在每一步尽量最小化。以下是步骤:

1.  初始化最大可能答案(比如**和**)，这将是一个所有位都被**设置为**的数字。
2.  遍历从 **31** 到 **0** 的每一位，检查该位是否可以取消设置，因为创建一个特定位(如 **0** 将最小化整体答案。
3.  对于上述步骤中的每个未设置的位，检查结果数组的所有元素是否会给出按位“或”作为当前可能的答案。如果发现为真，则用最小答案更新当前答案。
4.  完成上述步骤后，打印 ans 中存储的 Bitwise 的最小可能值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to check if it is possible
// to make current no as minimum result
// using array a and b
bool check(ll no, vector<int>& a,
        vector<int>& b)
{
    int count = 0;

    // Size of the first array
    int n = a.size();

    // Size of the second array
    int m = b.size();

    for (int i = 0; i < n; ++i) {

        for (int j = 0; j < m; ++j) {

            // Check for the number as
            // ans is possible or not
            if (((a[i] & b[j]) | no) == no) {
                count++;
                break;
            }
        }
    }

    // If all the elements of array
    // gives no as the Bitwise OR
    if (count == n)
        return true;
    else
        return false;
}

// Function to find the minimum bitwise
// OR of all the element in res[]
ll findMinValue(vector<int>& a,
                vector<int>& b)
{
    // Max possible ans
    ll ans = (1LL << 31) - 1;

    for (ll i = 30; i >= 0; --i) {

        // Check for the upper bit that
        // can be make off or not
        if (check(ans ^ (1 << i), a, b)) {
            ans = ans ^ (1 << i);
        }
    }

    return ans;
}

// Driver Code
int main()
{
    // Given array a[] and b[]
    vector<int> a = { 1, 2, 3 };
    vector<int> b = { 7, 15 };

    // Function Call
    cout << findMinValue(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to check if it is possible
// to make current no as minimum result
// using array a and b
static boolean check(int no,
                     int []a, int []b)
{
  int count = 0;

  // Size of the first array
  int n = a.length;

  // Size of the second array
  int m = b.length;

  for (int i = 0; i < n; ++i)
  {
    for (int j = 0; j < m; ++j)
    {
      // Check for the number as
      // ans is possible or not
      if (((a[i] & b[j]) | no) == no)
      {
        count++;
        break;
      }
    }
  }

  // If all the elements of array
  // gives no as the Bitwise OR
  if (count == n)
    return true;
  else
    return false;
}

// Function to find the minimum
// bitwise OR of all the
// element in res[]
static int findMinValue(int []a,
                        int []b)
{
  // Max possible ans
  int ans = (1 << 31) - 1;

  for (int i = 30; i >= 0; --i)
  {
    // Check for the upper bit that
    // can be make off or not
    if (check(ans ^ (1 << i), a, b))
    {
      ans = ans ^ (1 << i);
    }
  }

  return ans;
}

// Driver Code
public static void main(String[] args)
{
  // Given array a[] and b[]
  int []a = {1, 2, 3};
  int []b = {7, 15};

  // Function Call
  System.out.print(findMinValue(a, b));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to make current no as minimum result
# using array a and b
def check(no, a, b):

    count = 0

    # Size of the first array
    n = len(a)

    # Size of the second array
    m = len(b)

    for i in range(n):
        for j in range(m):

            # Check for the number as
            # ans is possible or not
            if (((a[i] & b[j]) | no) == no):
                count += 1
                break

    # If athe elements of array
    # gives no as the Bitwise OR
    if (count == n):
        return True
    else:
        return False

# Function to find the minimum bitwise
# OR of athe element in res[]
def findMinValue(a, b):

    # Max possible ans
    ans = (1 << 31) - 1

    for i in range(30, -1, -1):

        # Check for the upper bit that
        # can be make off or not
        if (check(ans ^ (1 << i), a, b)):
            ans = ans ^ (1 << i)

    return ans

# Driver Code
if __name__ == '__main__':

    # Given array a[] and b[]
    a = [ 1, 2, 3 ]
    b = [ 7, 15 ]

    # Function call
    print(findMinValue(a, b))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if it is possible
// to make current no as minimum result
// using array a and b
static bool check(int no, int []a,
                          int []b)
{
    int count = 0;

    // Size of the first array
    int n = a.Length;

    // Size of the second array
    int m = b.Length;

    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {

            // Check for the number as
            // ans is possible or not
            if (((a[i] & b[j]) | no) == no)
            {
                count++;
                break;
            }
        }
    }

    // If all the elements of array
    // gives no as the Bitwise OR
    if (count == n)
        return true;
    else
        return false;
}

// Function to find the minimum
// bitwise OR of all the
// element in res[]
static int findMinValue(int []a,
                        int []b)
{

    // Max possible ans
    int ans = int.MaxValue;

    for(int i = 30; i >= 0; --i)
    {

        // Check for the upper bit that
        // can be make off or not
        if (check(ans ^ (1 << i), a, b))
        {
            ans = ans ^ (1 << i);
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []a and []b
    int []a = { 1, 2, 3 };
    int []b = { 7, 15 };

    // Function call
    Console.Write(findMinValue(a, b));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if it is possible
// to make current no as minimum result
// using array a and b
function check(no,
                     a, b)
{
  let count = 0;

  // Size of the first array
  let n = a.length;

  // Size of the second array
  let m = b.length;

  for (let i = 0; i < n; ++i)
  {
    for (let j = 0; j < m; ++j)
    {
      // Check for the number as
      // ans is possible or not
      if (((a[i] & b[j]) | no) == no)
      {
        count++;
        break;
      }
    }
  }

  // If all the elements of array
  // gives no as the Bitwise OR
  if (count == n)
    return true;
  else
    return false;
}

// Function to find the minimum
// bitwise OR of all the
// element in res[]
function findMinValue(a,b)
{
  // Max possible ans
  let ans = (1 << 31) - 1;

  for (let i = 30; i >= 0; --i)
  {
    // Check for the upper bit that
    // can be make off or not
    if (check(ans ^ (1 << i), a, b))
    {
      ans = ans ^ (1 << i);
    }
  }

  return ans;
}

// Driver code

    // Given array a[] and b[]
  let a = [1, 2, 3];
  let b = [7, 15];

  // Function Call
  document.write(findMinValue(a, b));

  // This code is contributed by target_2.      
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*