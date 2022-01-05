# 用下一个 K 个元素的和替换圆形数组中的每个元素

> 原文:[https://www . geesforgeks . org/按下一个 k 元素的和替换循环数组中的每个元素/](https://www.geeksforgeeks.org/replace-every-element-in-a-circular-array-by-sum-of-next-k-elements/)

给定一个 **N** 整数的[圆形数组](https://www.geeksforgeeks.org/circular-array/)**arr【】**和一个整数 **K** ，任务是在以下操作后打印数组:

*   如果 **K** 非负，则用下一个 **K** 元素的和替换**A【I】**。
*   如果 **K** 为负，则替换为之前的 **K** 元素之和。

> 循环数组意味着数组最后一个元素的下一个元素是第一个元素，第一个元素的前一个元素是最后一个元素。

**示例:**

> **输入** : arr[] = {4，2，-5，11}，K = 3
> **输出:** 8 10 17 1
> **解释:**
> 步骤 1:对于索引 0，替换 arr[0]= arr[1]+arr[2]+arr[3]= 2+(-5)+11 = 8
> 步骤 2:对于索引 1，替换 arr[1] = arr[2] + arr[3] + arr[0] =() 替换 arr[2]= arr[3]+arr[0]+arr[1]= 11+4+2 = 17
> 步骤 4:对于索引 3，替换 arr[3]= arr[0]+arr[1]+arr[2]= 4+2+-5 = 1
> 因此，结果数组为{8，10，17，1}
> 
> **输入:** arr[] = {2，5，7，9}，K = -2
> **输出:** 16 11 7 12
> **解释:**
> 步骤 1:对于索引 0，替换 arr[0] = arr[3] + arr[2] = 9 + 7 = 16
> 步骤 2:对于索引 1，替换 arr[1]= arr[0]+arr[3]= 2+9 = 11
> 步骤 3:对于索引 替换 arr[2] = arr[1] + arr[0] = 5 + 2 = 7
> 步骤 4:对于索引 3，替换 arr[3]= arr[2]+arr[1]= 7+5 = 12
> 因此，结果数组为{16，11，7，12}

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并遍历下一个或上一个 **K 元素**，基于 **K** 的值，对每个数组元素进行遍历并打印它们的和。按照以下步骤解决问题:

*   如果 **K** 的值为负，则[反阵](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)求下一个 **K** 元素的和。
*   如果 **K** 的值非负，那么只需求每个元素的下一个 **K** 元素的和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define pb push_back

// Function to find the sum of next
// or previous k array elements
vector<int> sumOfKelementsUtil(
    vector<int>& a, int x)
{
    // Size of the array
    int n = a.size();

    int count, k, temp;

    // Stores the result
    vector<int> ans;

    // Iterate the given array
    for (int i = 0; i < n; i++) {

        count = 0;
        k = i + 1;
        temp = 0;

        // Traverse the k elements
        while (count < x) {

            temp += a[k % n];
            count++;
            k++;
        }

        // Push the K elements sum
        ans.pb(temp);
    }

    // Return the resultant vector
    return ans;
}

// Function that prints the sum of next
// K element for each index in the array
void sumOfKelements(vector<int>& arr,
                    int K)
{
    // Size of the array
    int N = (int)arr.size();

    // Stores the result
    vector<int> ans;

    // If key is negative,
    // reverse the array
    if (K < 0) {
        K = K * (-1);

        // Reverse the array
        reverse(arr.begin(),
                arr.end());

        // Find the resultant vector
        ans = sumOfKelementsUtil(arr, K);

        // Reverse the array again to
        // get the original sequence
        reverse(ans.begin(), ans.end());
    }

    // If K is positive
    else {
        ans = sumOfKelementsUtil(arr, K);
    }

    // Print the answer
    for (int i = 0; i < N; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 4, 2, -5, 11 };
    int K = 3;

    // Function Call
    sumOfKelements(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

//reverse array
static Vector<Integer> reverse(Vector<Integer> a)
{
  int i, n = a.size(), t;
  for (i = 0; i < n / 2; i++)
  {
    t = a.elementAt(i);
    a.set(i, a.elementAt(n - i - 1));
    a.set(n - i - 1, t);
  }
  return a;
}

// Function to find the sum of next
// or previous k array elements
static Vector<Integer> sumOfKelementsUtil(
       Vector<Integer>a, int x)
{
  // Size of the array
  int n = a.size();

  int count, k, temp;

  // Stores the result
  Vector<Integer> ans = new Vector<>();

  // Iterate the given array
  for (int i = 0; i < n; i++)
  {
    count = 0;
    k = i + 1;
    temp = 0;

    // Traverse the k elements
    while (count < x)
    {
      temp += a.elementAt(k % n);
      count++;
      k++;
    }

    // Push the K elements sum
    ans.add(temp);
  }

  // Return the resultant vector
  return ans;
}

// Function that prints the sum of next
// K element for each index in the array
static void sumOfKelements(Vector<Integer> arr,
                           int K)
{
  // Size of the array
  int N = (int)arr.size();

  // Stores the result
  Vector<Integer> ans = new Vector<>();

  // If key is negative,
  // reverse the array
  if (K < 0)
  {
    K = K * (-1);

    // Reverse the array
    arr =  reverse(arr);

    // Find the resultant vector
    ans = sumOfKelementsUtil(arr, K);

    // Reverse the array again to
    // get the original sequence
    ans = reverse(ans);
  }

  // If K is positive
  else
  {
    ans = sumOfKelementsUtil(arr, K);
  }

  // Print the answer
  for (int i = 0; i < N; i++)
  {
    System.out.print(ans.elementAt(i) + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    Vector<Integer> arr = new Vector<>();
    arr.add(4);
    arr.add(2);
    arr.add(-5);
    arr.add(11);
    int K = 3;

    // Function Call
    sumOfKelements(arr, K);

}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the sum of next
# or previous k array elements
def sumOfKelementsUtil(a, x):

    # Size of the array
    n = len(a)

    # Stores the result
    ans = []

    # Iterate the given array
    for i in range(n):
        count = 0
        k = i + 1
        temp = 0

        # Traverse the k elements
        while (count < x):
            temp += a[k % n]
            count += 1
            k += 1

        # Push the K elements sum
        ans.append(temp)

    # Return the resultant vector
    return ans

# Function that prints the
# sum of next K element for
# each index in the array
def sumOfKelements(arr, K):

    # Size of the array
    N = len(arr)

    #Stores the result
    ans = []

    # If key is negative,
    # reverse the array
    if (K < 0):
        K = K * (-1)

        # Reverse the array
        arr.reverse()

        # Find the resultant vector
        ans = sumOfKelementsUtil(arr, K)

        #Reverse the array again to
        # get the original sequence
        ans.reverse()

    # If K is positive
    else:
        ans = sumOfKelementsUtil(arr, K)

    # Print the answer
    for i in range(N):
        print (ans[i], end = " ")

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [4, 2, -5, 11]
    K = 3

    # Function Call
    sumOfKelements(arr, K)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Reverse array
static List<int> reverse(List<int> a)
{
  int i, n = a.Count, t;
  for (i = 0; i < n / 2; i++)
  {
    t = a[i];
    a[i] = a[n - i - 1];
    a[n - i - 1] = t;
  }
  return a;
}

// Function to find the sum of next
// or previous k array elements
static List<int> sumOfKelementsUtil(
       List<int>a, int x)
{
  // Size of the array
  int n = a.Count;

  int count, k, temp;

  // Stores the result
  List<int> ans = new List<int>();

  // Iterate the given array
  for (int i = 0; i < n; i++)
  {
    count = 0;
    k = i + 1;
    temp = 0;

    // Traverse the k elements
    while (count < x)
    {
      temp += a[k % n];
      count++;
      k++;
    }

    // Push the K elements sum
    ans.Add(temp);
  }

  // Return the resultant vector
  return ans;
}

// Function that prints the sum of next
// K element for each index in the array
static void sumOfKelements(List<int> arr,
                           int K)
{
  // Size of the array
  int N = (int)arr.Count;

  // Stores the result
  List<int> ans = new List<int>();

  // If key is negative,
  // reverse the array
  if (K < 0)
  {
    K = K * (-1);

    // Reverse the array
    arr =  reverse(arr);

    // Find the resultant vector
    ans = sumOfKelementsUtil(arr, K);

    // Reverse the array again to
    // get the original sequence
    ans = reverse(ans);
  }

  // If K is positive
  else
  {
    ans = sumOfKelementsUtil(arr, K);
  }

  // Print the answer
  for (int i = 0; i < N; i++)
  {
    Console.Write(ans[i] + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  List<int> arr = new List<int>();
  arr.Add(4);
  arr.Add(2);
  arr.Add(-5);
  arr.Add(11);
  int K = 3;

  // Function Call
  sumOfKelements(arr, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

   // Function to print the
    // required resultant array
    function sumOfKElements(
        arr, n, k)
    {

        // Reverse the array
        let rev = false;

        if (k < 0) {

            rev = true;
            k *= -1;
            let l = 0, r = n - 1;

            // Traverse the range
            while (l < r) {

                let tmp = arr[l];
                arr[l] = arr[r];
                arr[r] = tmp;
                l++;
                r--;
            }
        }

        // Store prefix sum
        let dp = Array.from({length: n}, (_, i) => 0);
        dp[0] = arr[0];

        // Find the prefix sum
        for (let i = 1; i < n; i++) {

            dp[i] += dp[i - 1] + arr[i];
        }

        // Store the answer
        let ans = Array.from({length: n}, (_, i) => 0);

        // Calculate the answers
        for (let i = 0; i < n; i++) {

            if (i + k < n)
                ans[i] = dp[i + k] - dp[i];
            else {

                // Count of remaining elements
                let x = k - (n - 1 - i);

                // Add the sum of all elements
                // y times
                let y = Math.floor(x / n);

                // Add the remaining elements
                let rem = x % n;

                // Update ans[i]
                ans[i] = dp[n - 1]
                         - dp[i]
                         + y * dp[n - 1]
                         + (rem - 1 >= 0 ? dp[rem - 1] : 0);
            }
        }

        // If array is reversed print
        // ans[] in reverse
        if (rev) {
            for (let i = n - 1; i >= 0; i--) {
                document.write(ans[i] + " ");
            }
        }
        else {
            for (let i = 0; i < n; i++) {
                document.write(ans[i] + " ");
            }
        }
    }

// Driver Code

   // Given array arr[]
        let arr = [ 4, 2, -5, 11 ];

        let N = arr.length;

        // Given K
        let K = 3;

        // Function
        sumOfKElements(arr, N, K);

// This code is contributed by souravghosh0416.
</script>
```

**Output**

```
8 10 17 1 
```

***时间复杂度:** O(N*K)，其中 N 为给定数组的长度，K 为给定整数。*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。按照以下步骤解决问题:

1.  如果 **K** 为负，[反转给定数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)，将 **K** 乘以 **-1** 。
2.  在 **pre[]** 中计算并存储给定数组的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
3.  创建数组 **ans[]** 来存储每个元素的答案。
4.  对于每个索引 **i** ，如果 **i + K** 小于 **N** ，则更新**ans[I]= pre[I+K]–pre[I]**
5.  否则，将从索引 **i** 到**N–1**的所有元素的总和相加，找到剩余的**K –( N–1–I)**元素，因为**(N–1–I)**元素已经在上述步骤中添加。
6.  将所有元素的总和**floor((K–N–1–I)/N)**乘以给定数组中从 **0** 到**((K –( N–1–I))% N)–1**的剩余元素的总和。
7.  计算完数组中每个元素的答案后，检查数组之前是否反转过。如果是，反转 **ans[]** 阵列。
8.  完成上述步骤后，打印数组**和**中存储的所有元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print the
// required resultant array
void sumOfKElements(int arr[], int n,
                    int k)
{

    // Reverse the array
    bool rev = false;

    if (k < 0)
    {
        rev = true;
        k *= -1;
        int l = 0, r = n - 1;

        // Traverse the range
        while (l < r)
        {
            int tmp = arr[l];
            arr[l] = arr[r];
            arr[r] = tmp;
            l++;
            r--;
        }
    }

    // Store prefix sum
    int dp[n] = {0};
    dp[0] = arr[0];

    // Find the prefix sum
    for(int i = 1; i < n; i++)
    {
        dp[i] += dp[i - 1] + arr[i];
    }

    // Store the answer
    int ans[n] = {0};

    // Calculate the answers
    for(int i = 0; i < n; i++)
    {
        if (i + k < n)
            ans[i] = dp[i + k] - dp[i];
        else
        {

            // Count of remaining elements
            int x = k - (n - 1 - i);

            // Add the sum of all elements
            // y times
            int y = x / n;

            // Add the remaining elements
            int rem = x % n;

            // Update ans[i]
            ans[i] = dp[n - 1] - dp[i] +
                 y * dp[n - 1] + (rem - 1 >= 0 ?
                   dp[rem - 1] : 0);
        }
    }

    // If array is reversed print
    // ans[] in reverse
    if (rev)
    {
        for(int i = n - 1; i >= 0; i--)
        {
            cout << ans[i] << " ";
        }
    }
    else
    {
        for(int i = 0; i < n; i++)
        {
            cout << ans[i] << " ";
        }
    }
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 4, 2, -5, 11 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 3;

    // Function
    sumOfKElements(arr, N, K);
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to print the
    // required resultant array
    static void sumOfKElements(
        int arr[], int n, int k)
    {

        // Reverse the array
        boolean rev = false;

        if (k < 0) {

            rev = true;
            k *= -1;
            int l = 0, r = n - 1;

            // Traverse the range
            while (l < r) {

                int tmp = arr[l];
                arr[l] = arr[r];
                arr[r] = tmp;
                l++;
                r--;
            }
        }

        // Store prefix sum
        int dp[] = new int[n];
        dp[0] = arr[0];

        // Find the prefix sum
        for (int i = 1; i < n; i++) {

            dp[i] += dp[i - 1] + arr[i];
        }

        // Store the answer
        int ans[] = new int[n];

        // Calculate the answers
        for (int i = 0; i < n; i++) {

            if (i + k < n)
                ans[i] = dp[i + k] - dp[i];
            else {

                // Count of remaining elements
                int x = k - (n - 1 - i);

                // Add the sum of all elements
                // y times
                int y = x / n;

                // Add the remaining elements
                int rem = x % n;

                // Update ans[i]
                ans[i] = dp[n - 1]
                         - dp[i]
                         + y * dp[n - 1]
                         + (rem - 1 >= 0 ? dp[rem - 1] : 0);
            }
        }

        // If array is reversed print
        // ans[] in reverse
        if (rev) {
            for (int i = n - 1; i >= 0; i--) {
                System.out.print(ans[i] + " ");
            }
        }
        else {
            for (int i = 0; i < n; i++) {
                System.out.print(ans[i] + " ");
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 4, 2, -5, 11 };

        int N = arr.length;

        // Given K
        int K = 3;

        // Function
        sumOfKElements(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to print
# required resultant array
def sumOfKElements(arr, n, k):

    # Reverse the array
    rev = False;

    if (k < 0):

        rev = True;
        k *= -1;
        l = 0;
        r = n - 1;

        # Traverse the range
        while (l < r):
            tmp = arr[l];
            arr[l] = arr[r];
            arr[r] = tmp;
            l += 1;
            r -= 1;

    # Store prefix sum
    dp = [0] * n;
    dp[0] = arr[0];

    # Find the prefix sum
    for i in range(1, n):
        dp[i] += dp[i - 1] + arr[i];

    # Store the answer
    ans = [0] * n;

    # Calculate the answers
    for i in range(n):
        if (i + k < n):
            ans[i] = dp[i + k] - dp[i];
        else:

            # Count of remaining
            # elements
            x = k - (n - 1 - i);

            # Add the sum of
            # all elements y times
            y = x // n;

            # Add the remaining
            # elements
            rem = x % n;

            # Update ans[i]
            ans[i] = (dp[n - 1] - dp[i] +
                      y * dp[n - 1] +
                      (dp[rem - 1]
                      if rem - 1 >= 0
                      else 0));

    # If array is reversed
    # print ans in reverse
    if (rev):
        for i in range(n - 1, -1, -1):
            print(ans[i], end = " ");

    else:
        for i in range(n):
            print(ans[i], end = " ");

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [4, 2, -5, 11];

    N = len(arr);

    # Given K
    K = 3;

    # Function
    sumOfKElements(arr, N, K);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for
// the above approach
using System;
class GFG {

// Function to print the
// required resultant array
static void sumOfKElements(int []arr,
                           int n, int k)
{
  // Reverse the array
  bool rev = false;

  if (k < 0)
  {
    rev = true;
    k *= -1;
    int l = 0, r = n - 1;

    // Traverse the range
    while (l < r)
    {
      int tmp = arr[l];
      arr[l] = arr[r];
      arr[r] = tmp;
      l++;
      r--;
    }
  }

  // Store prefix sum
  int []dp = new int[n];
  dp[0] = arr[0];

  // Find the prefix sum
  for (int i = 1; i < n; i++)
  {
    dp[i] += dp[i - 1] + arr[i];
  }

  // Store the answer
  int []ans = new int[n];

  // Calculate the answers
  for (int i = 0; i < n; i++)
  {
    if (i + k < n)
      ans[i] = dp[i + k] - dp[i];
    else
    {
      // Count of remaining elements
      int x = k - (n - 1 - i);

      // Add the sum of all elements
      // y times
      int y = x / n;

      // Add the remaining elements
      int rem = x % n;

      // Update ans[i]
      ans[i] = dp[n - 1] - dp[i] +
               y * dp[n - 1] +
               (rem - 1 >= 0 ?
                dp[rem - 1] : 0);
    }
  }

  // If array is reversed print
  // ans[] in reverse
  if (rev)
  {
    for (int i = n - 1; i >= 0; i--)
    {
      Console.Write(ans[i] + " ");
    }
  }
  else
  {
    for (int i = 0; i < n; i++)
    {
      Console.Write(ans[i] + " ");
    }
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {4, 2, -5, 11};

  int N = arr.Length;

  // Given K
  int K = 3;

  // Function
  sumOfKElements(arr, N, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the
// required resultant array
function sumOfKElements(arr, n,
                    k)
{

    // Reverse the array
    let rev = false;

    if (k < 0)
    {
        rev = true;
        k *= -1;
        let l = 0, r = n - 1;

        // Traverse the range
        while (l < r)
        {
            let tmp = arr[l];
            arr[l] = arr[r];
            arr[r] = tmp;
            l++;
            r--;
        }
    }

    // Store prefix sum
    let dp = new Uint8Array(n);
    dp[0] = arr[0];

    // Find the prefix sum
    for(let i = 1; i < n; i++)
    {
        dp[i] += dp[i - 1] + arr[i];
    }

    // Store the answer
    let ans = new Uint8Array(n);

    // Calculate the answers
    for(let i = 0; i < n; i++)
    {
        if (i + k < n)
            ans[i] = dp[i + k] - dp[i];
        else
        {

            // Count of remaining elements
            let x = k - (n - 1 - i);

            // Add the sum of all elements
            // y times
            let y = Math.floor(x / n);

            // Add the remaining elements
            let rem = x % n;

            // Update ans[i]
            ans[i] = dp[n - 1] - dp[i] +
                y * dp[n - 1] + (rem - 1 >= 0 ?
                dp[rem - 1] : 0);
        }
    }

    // If array is reversed print
    // ans[] in reverse
    if (rev)
    {
        for(let i = n - 1; i >= 0; i--)
        {
            document.write(ans[i] + " ");
        }
    }
    else
    {
        for(let i = 0; i < n; i++)
        {
            document.write(ans[i] + " ");
        }
    }
}

// Driver Code

    // Given array arr[]
    let arr = [ 4, 2, -5, 11 ];

    let N = arr.length;

    // Given K
    let K = 3;

    // Function
    sumOfKElements(arr, N, K);

//This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
8 10 17 1 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)