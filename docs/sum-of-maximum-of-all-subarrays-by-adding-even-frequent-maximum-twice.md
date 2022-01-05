# 所有子阵的最大值之和，加两次偶频数最大值

> 原文:[https://www . geeksforgeeks . org/所有子阵的最大值之和加偶频最大值两次/](https://www.geeksforgeeks.org/sum-of-maximum-of-all-subarrays-by-adding-even-frequent-maximum-twice/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**(*所有数组元素都是 2* 的 [*完美幂)，任务是计算所有*](https://www.geeksforgeeks.org/calculate-sum-of-all-integers-from-1-to-n-excluding-perfect-power-of-2/)*[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中最大元素的和。*

***注:**如果子阵中最大元素的频率为偶数，则将该元素的值的两倍加到和上。*

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 5
> **解释:**所有可能的子阵都是{1}、{1，2}、{2}。
> 斯巴莱 1: {1}。最大值= 1。总和= 1。
> 斯巴莱 2: {1，2}。最大值= 2。总和= 3。
> 斯巴莱 3: {2}。最大值= 2。总和= 5。
> 因此，要求输出为 5。
> 
> **输入:** arr[] = {4，4}
> **输出:** 16
> **解释:**所有可能的子阵都是{4}、{4，4}、{4}。
> 斯巴莱 1: {4}。最大值= 4。总和= 1。
> 斯巴莱 2: {4，4}。最大值= 4。由于最大值在子阵列中出现两次，Sum = 4 + 8 = 12。
> 斯巴莱 3: {4}。最大值= 4。总和= 16。
> 因此，要求输出为 16。

**天真方法:**解决这个问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能的子数组，并找到所有子数组中的最大元素及其出现的次数。最后，打印获得的所有最大元素的总和。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，以存储所有子阵列的最大值的所需[和。](https://www.geeksforgeeks.org/sum-of-maximum-of-all-subarrays-divide-and-conquer/)
*   生成给定阵列的所有可能子阵列 **arr[]** 。
*   对于生成的每个子阵，找到最大元素的[频率，](https://www.geeksforgeeks.org/python-find-frequency-of-largest-element-in-list/)[检查频率是否均匀](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现是真的，将 **2 *最大值**加到**和**上。否则，将**最大值**加到**和**上。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate sum of
// maximum of all subarrays
void findSum(vector<int>a)
{
    // Storeas the sum of maximums
    int ans = 0;

    // Traverse the array
    for(int low = 0;
            low < a.size();
            low++)
    {
        for(int high = low;
                high < a.size();
                high++)
        {

            // Store the frequency of the
            // maximum element in subarray
            int count = 0;
            int maxNumber = 0;

            // Finding maximum
            for(int i = low;
                    i <= high; i++)
            {

                // Increment frequency by 1
                if (a[i] == maxNumber)
                    count++;

                // If new maximum is obtained
                else if (a[i] > maxNumber)
                {
                    maxNumber = a[i];
                    count = 1;
                }
            }

            // If frequency of maximum
            // is even, then add 2*maxNumber.
            // Otherwise, add maxNumber
            ans += maxNumber * ((count % 2 == 0) ? 2 : 1);
        }
    }

    // Print the sum obtained
    cout << (ans);
}

// Driver Code
int main()
{
    vector<int>arr = { 2, 1, 4, 4, 2 };

    // Function Call
    findSum(arr);
}

// This code is contributed by amreshkumar3
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to calculate sum of
    // maximum of all subarrays
    public static void findSum(int a[])
    {
        // Stores the sum of maximums
        int ans = 0;

        // Traverse the array
        for (int low = 0;
             low < a.length; low++) {

            for (int high = low;
                 high < a.length;
                 high++) {

                // Store the frequency of the
                // maximum element in subarray
                int count = 0;
                int maxNumber = 0;

                // Finding maximum
                for (int i = low;
                     i <= high; i++) {

                    // Increment frequency by 1
                    if (a[i] == maxNumber)
                        count++;

                    // If new maximum is obtained
                    else if (a[i] > maxNumber) {
                        maxNumber = a[i];
                        count = 1;
                    }
                }

                // If frequency of maximum
                // is even, then add 2*maxNumber.
                // Otherwise, add maxNumber
                ans += maxNumber
                       * ((count % 2 == 0) ? 2 : 1);
            }
        }

        // Print the sum obtained
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 1, 4, 4, 2 };

        // Function Call
        findSum(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of
# maximum of all subarrays
def findSum(a):

  # Stores the sum of maximums
  ans = 0

  # Traverse the array
  for low in range(0, len(a)):
    for high in range(low,len(a)):

      # Store the frequency of the
      # maximum element in subarray
      count = 0
      maxNumber = 0

      # Finding maximum
      for i in range(low, high + 1):

        # Increment frequency by 1
        if (a[i] == maxNumber):
          count += 1

        # If new maximum is obtained
        elif (a[i] > maxNumber):
          maxNumber = a[i]
          count = 1

      # If frequency of maximum
      # is even, then add 2*maxNumber.
      # Otherwise, add maxNumber
      if count % 2:
        ans += maxNumber
      else:
        ans += maxNumber * 2

  # Print the sum obtained
  print(ans)

# Driver Code
arr = [ 2, 1, 4, 4, 2 ]

# Function Call
findSum(arr)

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program for the above approach
using System;

class GFG {

  // Function to calculate sum of
  // maximum of all subarrays
  public static void findSum(int[] a)
  {

    // Stores the sum of maximums
    int ans = 0;

    // Traverse the array
    for (int low = 0; low < a.Length; low++) {

      for (int high = low; high < a.Length; high++) {

        // Store the frequency of the
        // maximum element in subarray
        int count = 0;
        int maxNumber = 0;

        // Finding maximum
        for (int i = low; i <= high; i++) {

          // Increment frequency by 1
          if (a[i] == maxNumber)
            count++;

          // If new maximum is obtained
          else if (a[i] > maxNumber) {
            maxNumber = a[i];
            count = 1;
          }
        }

        // If frequency of maximum
        // is even, then add 2*maxNumber.
        // Otherwise, add maxNumber
        ans += maxNumber
          * ((count % 2 == 0) ? 2 : 1);
      }
    }

    // Print the sum obtained
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { 2, 1, 4, 4, 2 };

    // Function Call
    findSum(arr);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to calculate sum of
      // maximum of all subarrays
      function findSum(a) {
      // Stores the sum of maximums
        var ans = 0;

        // Traverse the array
        for (var low = 0; low < a.length; low++) {
          for (var high = low; high < a.length; high++) {
            // Store the frequency of the
            // maximum element in subarray
            var count = 0;
            var maxNumber = 0;

            // Finding maximum
            for (var i = low; i <= high; i++) {
              // Increment frequency by 1
              if (a[i] === maxNumber) count++;
              // If new maximum is obtained
              else if (a[i] > maxNumber) {
                maxNumber = a[i];
                count = 1;
              }
            }

            // If frequency of maximum
            // is even, then add 2*maxNumber.
            // Otherwise, add maxNumber
            ans += maxNumber * (count % 2 === 0 ? 2 : 1);
          }
        }

        // Print the sum obtained
        document.write(ans);
      }

      // Driver Code
      var arr = [2, 1, 4, 4, 2];

      // Function Call
      findSum(arr);

</script>
```

**Output:** 

```
75
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**优化方法:**对上述方法进行优化，思路是存储数组元素每一位的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，在 **O(1)** 计算复杂度中找到一个子阵中最大元素的频率。这种方法的工作原理是所有的数组元素都是 2 的**次方**。

下面是上述方法的实现:

## C++

```
// c++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum
// in subarray {arr[low], ..., arr[high]}
int getCountLargestNumber(
  int low, int high, int i,
  vector<vector<int>> prefixSums);

// Function to calculate the prefix
// sum array
vector<vector<int>> getPrefixSums(
  vector<int> a);

// Function to calculate sum of
// maximum of all subarrays
void findSum(vector<int> a)
{
  // Calculate prefix sum array
  vector<vector<int>> prefixSums
    = getPrefixSums(a);

  // Store the sum of maximums
  int ans = 0;

  // Traverse the array
  for (int low = 0;
       low < a.size();
       low++) {

    for (int high = low;
         high < a.size();
         high++) {

      // Store the frequency of the
      // maximum element in subarray
      int count = 0;
      int maxNumber = 0;

      // Store prefix sum of every bit
      for (int i = 30; i >= 0; i--) {

        // Get the frequency of the
        // largest element in subarray
        count = getCountLargestNumber(
          low, high, i, prefixSums);

        if (count > 0) {
          maxNumber = (1 << i);

          // If frequency of the largest
          // element is even, add 2 * maxNumber
          // Otherwise, add maxNumber
          ans += maxNumber
            * ((count % 2 == 0) ? 2 : 1);
          break;
        }
      }
    }
  }

  // Print the required answer
  cout << ans;
}

// Function to calculate the prefix
// sum array
vector<vector<int>> getPrefixSums(
  vector<int> a)
{

  // Initialize prefix array
  vector<vector<int>> prefix(32, vector<int>(a.size() + 1, 0));

  // Start traversing the array
  for (int j = 0; j < a.size(); j++) {

    // Update the prefix array for
    // each element in the array
    for (int i = 0; i <= 30; i++) {

      // To check which bit is set
      int mask = (1 << i);
      prefix[i][j + 1] += prefix[i][j];
      if ((a[j] & mask) > 0)
        prefix[i][j + 1]++;
    }
  }

  // Return prefix array
  return prefix;
}

// Function to find the maximum
// in subarray {arr[low], ..., arr[high]}
int getCountLargestNumber(
  int low, int high, int i,
  vector<vector<int>> prefixSums)
{
  return prefixSums[i][high + 1]
    - prefixSums[i][low];
}

// Driver Code
int main()
{
  vector<int> arr = { 2, 1, 4, 4, 2 };

  // Function Call
  findSum(arr);
  return 0;
}

// This code is contributed
// by Shubham Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to calculate sum of
    // maximum of all subarrays
    public static void findSum(int a[])
    {
        // Calculate prefix sum array
        int[][] prefixSums
            = getPrefixSums(a);

        // Store the sum of maximums
        int ans = 0;

        // Traverse the array
        for (int low = 0;
             low < a.length;
             low++) {

            for (int high = low;
                 high < a.length;
                 high++) {

                // Store the frequency of the
                // maximum element in subarray
                int count = 0;
                int maxNumber = 0;

                // Store prefix sum of every bit
                for (int i = 30; i >= 0; i--) {

                    // Get the frequency of the
                    // largest element in subarray
                    count = getCountLargestNumber(
                        low, high, i, prefixSums);

                    if (count > 0) {
                        maxNumber = (1 << i);

                        // If frequency of the largest
                        // element is even, add 2 * maxNumber
                        // Otherwise, add maxNumber
                        ans += maxNumber
                               * ((count % 2 == 0) ? 2 : 1);
                        break;
                    }
                }
            }
        }

        // Print the required answer
        System.out.println(ans);
    }

    // Function to calculate the prefix
    // sum array
    public static int[][] getPrefixSums(
        int[] a)
    {

        // Initialize prefix array
        int[][] prefix = new int[32][a.length + 1];

        // Start traversing the array
        for (int j = 0; j < a.length; j++) {

            // Update the prefix array for
            // each element in the array
            for (int i = 0; i <= 30; i++) {

                // To check which bit is set
                int mask = (1 << i);
                prefix[i][j + 1] += prefix[i][j];
                if ((a[j] & mask) > 0)
                    prefix[i][j + 1]++;
            }
        }

        // Return prefix array
        return prefix;
    }

    // Function to find the maximum
    // in subarray {arr[low], ..., arr[high]}
    public static int
    getCountLargestNumber(
        int low, int high, int i,
        int[][] prefixSums)
    {
        return prefixSums[i][high + 1]
            - prefixSums[i][low];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 1, 4, 4, 2 };

        // Function Call
        findSum(arr);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate sum of
# maximum of all subarrays
def findSum(a):

    # Calculate prefix sum array
    prefixSums = getPrefixSums(a);

    # Store the sum of maximums
    ans = 1;

    # Traverse the array
    for low in range(len(a)):

        for high in range(len(a)):

            # Store the frequency of the
            # maximum element in subarray
            count = 0;
            maxNumber = 0;

            # Store prefix sum of every bit
            for i in range(30,0,-1):

                # Get the frequency of the
                # largest element in subarray
                count = getCountLargestNumber(low, high, i, prefixSums);

                if (count > 0):
                    maxNumber = (1 << i);

                    # If frequency of the largest
                    # element is even, add 2 * maxNumber
                    # Otherwise, add maxNumber
                    if(count % 2 == 0):
                        ans += maxNumber * 2;
                    else:
                        ans += maxNumber *  1;
                    break;

    # Prthe required answer
    print(ans);

# Function to calculate the prefix
# sum array
def getPrefixSums(a):

    # Initialize prefix array
    prefix = [[0 for i in range(len(a)+1)] for j in range(32)];

    # Start traversing the array
    for j in range(len(a)):

        # Update the prefix array for
        # each element in the array
        for i in range(31):

            # To check which bit is set
            mask = (1 << i);
            prefix[i][j + 1] += prefix[i][j];
            if ((a[j] & mask) > 0):
                prefix[i][j + 1]+=1;

    # Return prefix array
    return prefix;

# Function to find the maximum
# in subarray:arr[low], ..., arr[high]
def getCountLargestNumber(low, high, i, prefixSums):
    return prefixSums[i][high + 1] - prefixSums[i][low];

# Driver Code
if __name__ == '__main__':
    arr = [ 2, 1, 4, 4, 2 ];

    # Function Call
    findSum(arr);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach

using System;
public class GFG {

    // Function to calculate sum of
    // maximum of all subarrays
    public static void findSum(int []a) {
        // Calculate prefix sum array
        int[,] prefixSums = getPrefixSums(a);

        // Store the sum of maximums
        int ans = 0;

        // Traverse the array
        for (int low = 0; low < a.Length; low++) {

            for (int high = low; high < a.Length; high++) {

                // Store the frequency of the
                // maximum element in subarray
                int count = 0;
                int maxNumber = 0;

                // Store prefix sum of every bit
                for (int i = 30; i >= 0; i--) {

                    // Get the frequency of the
                    // largest element in subarray
                    count = getCountLargestNumber(low, high, i, prefixSums);

                    if (count > 0) {
                        maxNumber = (1 << i);

                        // If frequency of the largest
                        // element is even, add 2 * maxNumber
                        // Otherwise, add maxNumber
                        ans += maxNumber * ((count % 2 == 0) ? 2 : 1);
                        break;
                    }
                }
            }
        }

        // Print the required answer
        Console.WriteLine(ans);
    }

    // Function to calculate the prefix
    // sum array
    public static int[,] getPrefixSums(int[] a) {

        // Initialize prefix array
        int[,] prefix = new int[32,a.Length + 1];

        // Start traversing the array
        for (int j = 0; j < a.Length; j++) {

            // Update the prefix array for
            // each element in the array
            for (int i = 0; i <= 30; i++) {

                // To check which bit is set
                int mask = (1 << i);
                prefix[i, j + 1] += prefix[i,j];
                if ((a[j] & mask) > 0)
                    prefix[i, j + 1]++;
            }
        }

        // Return prefix array
        return prefix;
    }

    // Function to find the maximum
    // in subarray {arr[low], ..., arr[high]}
    public static int getCountLargestNumber(int low, int high, int i, int[,] prefixSums) {
        return prefixSums[i,high + 1] - prefixSums[i,low];
    }

    // Driver Code
    public static void Main(String[] args) {
        int[] arr = { 2, 1, 4, 4, 2 };

        // Function Call
        findSum(arr);
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to calculate sum of
    // maximum of all subarrays
    function findSum(a)
    {

        // Calculate prefix sum array
        var prefixSums = getPrefixSums(a);

        // Store the sum of maximums
        var ans = 0;

        // Traverse the array
        for (var low = 0; low < a.length; low++) {

            for (var high = low; high < a.length; high++) {

                // Store the frequency of the
                // maximum element in subarray
                var count = 0;
                var maxNumber = 0;

                // Store prefix sum of every bit
                for (var i = 30; i >= 0; i--) {

                    // Get the frequency of the
                    // largest element in subarray
                    count = getCountLargestNumber(low, high, i, prefixSums);

                    if (count > 0) {
                        maxNumber = (1 << i);

                        // If frequency of the largest
                        // element is even, add 2 * maxNumber
                        // Otherwise, add maxNumber
                        ans += maxNumber * ((count % 2 == 0) ? 2 : 1);
                        break;
                    }
                }
            }
        }

        // Print the required answer
        document.write(ans);
    }

    // Function to calculate the prefix
    // sum array
      function getPrefixSums(a) {

        // Initialize prefix array
        var prefix = Array(32).fill().map(()=>Array(a.length + 1).fill(0));

        // Start traversing the array
        for (var j = 0; j < a.length; j++) {

            // Update the prefix array for
            // each element in the array
            for (var i = 0; i <= 30; i++) {

                // To check which bit is set
                var mask = (1 << i);
                prefix[i][j + 1] += prefix[i][j];
                if ((a[j] & mask) > 0)
                    prefix[i][j + 1]++;
            }
        }

        // Return prefix array
        return prefix;
    }

    // Function to find the maximum
    // in subarray {arr[low], ..., arr[high]}
    function getCountLargestNumber(low , high , i, prefixSums) {
        return prefixSums[i][high + 1] - prefixSums[i][low];
    }

    // Driver Code
        var arr = [ 2, 1, 4, 4, 2 ];

        // Function Call
        findSum(arr);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
75
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(32 * N)*

**高效方法:**优化上述方法，思路是利用所有数组元素都是 2 的[次方的属性，利用该属性解决问题。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

*   按照**降序**遍历 2 的所有 [**次幂。将任意 2 次方视为**掩码**。**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)
*   将数组分成子数组，这样就不会有子数组包含 **arr[index] = -1** ，其中 index 是数组中的任何有效位置。
*   让上述步骤得到的子阵列为 **S** 。遍历 **S** 和**从外环添加**值，该值仅由 **S** 中具有当前掩码的子阵列贡献。同时将相应的位置 **arr[index] =屏蔽**设置为 **arr[index] = -1** 。
*   计算包含**掩码**的 **S** 中所有子阵列贡献的值，并将三个计数器维护为**奇数**、**事件计数**，以及**掩码**的频率。
*   指针 **prev** 指向前一个索引，这样**arr【prev】=屏蔽**。
*   在任何**索引**处，其中 **arr【索引】=掩码**，通过从索引中减去 **prev** 获得掩码的最后一次出现**和当前出现**之间的整数的**计数**。使用此**计数**和掩码频率的奇偶校验，使用公式**计数=(index–prev)**获得包含掩码的所有连续子阵列贡献的值，并将计数添加到答案中。****
*   如果最大频率为偶数或奇数，并且如果**奇偶校验为奇数**:
    *   掩码的**频率**为奇数的所有相邻子阵列贡献的值为**(计数–1)*偶数计数+奇数计数**。
    *   由所有相邻子阵列贡献的值，这些子阵列具有与 T2 2 *(计数–1)*奇数计数+2 *偶数计数相同的掩码频率**。**
*   **否则，如果**奇偶为偶数**:

    *   掩码的**频率**为奇数的所有相邻子阵列贡献的值为**(计数–1)*奇数计数+偶数计数**。
    *   由所有相邻子阵列贡献的值，这些子阵列具有与 T2 2 *(计数–1)*偶数计数+ 2 *奇数计数相同的掩码频率**。**** 
*   ****将所有相应的值添加到答案中。如果奇偶校验为偶数，也将计数加到偶数。否则，将**计数**加到**奇数**上。****

****下面是上述方法的实现:****

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.io.*;

class GFG {

    // Function to calculate sum of
    // maximum of all subarrays
    public static void findSum(int a[])
    {
        int ans = 0;
        int prev = -1;

        // Iterate over the range [30, 0]
        for (int i = 30; i >= 0; i--) {
            int mask = (1 << i);

            // Inner loop through the
            // length of the array
            for (int j = 0;
                 j < a.length; j++) {

                // Divide the array such
                // that no subarray will
                // have any index set to -1
                if (a[j] == -1) {
                    ans += findSumOfValuesOfRange(
                        a, prev + 1, j - 1, mask);
                    prev = j;
                }
            }

            // Find the sum of subarray
            ans += findSumOfValuesOfRange(
                a, prev + 1, a.length - 1, mask);
        }

        // Print the sum obtained
        System.out.println(ans);
    }

    // Function that takes any subarray
    // S and return values contributed
    // by only the subarrays in S containing mask
    public static int findSumOfValuesOfRange(
        int[] a, int low, int high, int mask)
    {
        if (low > high)
            return 0;

        // Stores count even, odd count of
        // occurrences and maximum element
        int evenCount = 0, oddCount = 0,
            countLargestNumber = 0;
        int prev = low - 1, ans = 0;

        // Traverse from low to high
        for (int i = low; i <= high; i++) {

            // Checking if this position
            // in the array is mask
            if ((mask & a[i]) > 0) {

                // Mask is the largest
                // number in subarray.
                // Increment count by 1
                countLargestNumber++;

                // Store parity as 0 or 1
                int parity = countLargestNumber % 2;

                // Setting a[i]=-1, this
                // will help in splitting
                // array into subarrays
                a[i] = -1;
                int count = i - prev;
                ans += count;

                // Add values contributed
                // by those subarrays that
                // have an odd frequency
                ans += (count - 1)
                       * ((parity == 1) ? evenCount
                                        : oddCount);
                ans += ((parity == 1) ? oddCount
                                      : evenCount);

                // Adding values contributed
                // by those subarrays that
                // have an even frequency
                ans += 2 * (count - 1)
                       * ((parity == 1) ? oddCount
                                        : evenCount);
                ans += 2
                       * ((parity == 1) ? evenCount
                                        : oddCount);

                // Set the prev pointer
                // to this position
                prev = i;

                if (parity == 1)
                    oddCount += count;
                else
                    evenCount += count;
            }
        }

        if (prev != low - 1) {
            int count = high - prev;
            int parity = countLargestNumber % 2;

            ans += count
                   * ((parity == 1)
                          ? oddCount
                          : evenCount);
            ans += 2 * count
                   * ((parity == 1)
                          ? evenCount
                          : oddCount);
            ans *= mask;
        }

        // Return the final sum
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 1, 4, 4, 2 };

        // Function call
        findSum(arr);
    }
}**
```

## ****C#****

```
**// C# program for the above approach
using System;
public class GFG {

    // Function to calculate sum of
    // maximum of all subarrays
    public static void findSum(int []a) {
        int ans = 0;
        int prev = -1;

        // Iterate over the range [30, 0]
        for (int i = 30; i >= 0; i--) {
            int mask = (1 << i);

            // Inner loop through the
            // length of the array
            for (int j = 0; j < a.Length; j++) {

                // Divide the array such
                // that no subarray will
                // have any index set to -1
                if (a[j] == -1) {
                    ans += findSumOfValuesOfRange(a, prev + 1, j - 1, mask);
                    prev = j;
                }
            }

            // Find the sum of subarray
            ans += findSumOfValuesOfRange(a, prev + 1, a.Length - 1, mask);
        }

        // Print the sum obtained
        Console.WriteLine(ans);
    }

    // Function that takes any subarray
    // S and return values contributed
    // by only the subarrays in S containing mask
    public static int findSumOfValuesOfRange(int[] a, int low,
                                             int high, int mask)
    {
        if (low > high)
            return 0;

        // Stores count even, odd count of
        // occurrences and maximum element
        int evenCount = 0, oddCount = 0, countLargestNumber = 0;
        int prev = low - 1, ans = 0;

        // Traverse from low to high
        for (int i = low; i <= high; i++) {

            // Checking if this position
            // in the array is mask
            if ((mask & a[i]) > 0) {

                // Mask is the largest
                // number in subarray.
                // Increment count by 1
                countLargestNumber++;

                // Store parity as 0 or 1
                int parity = countLargestNumber % 2;

                // Setting a[i]=-1, this
                // will help in splitting
                // array into subarrays
                a[i] = -1;
                int count = i - prev;
                ans += count;

                // Add values contributed
                // by those subarrays that
                // have an odd frequency
                ans += (count - 1) * ((parity == 1) ? evenCount : oddCount);
                ans += ((parity == 1) ? oddCount : evenCount);

                // Adding values contributed
                // by those subarrays that
                // have an even frequency
                ans += 2 * (count - 1) * ((parity == 1) ? oddCount : evenCount);
                ans += 2 * ((parity == 1) ? evenCount : oddCount);

                // Set the prev pointer
                // to this position
                prev = i;

                if (parity == 1)
                    oddCount += count;
                else
                    evenCount += count;
            }
        }

        if (prev != low - 1) {
            int count = high - prev;
            int parity = countLargestNumber % 2;

            ans += count * ((parity == 1) ? oddCount : evenCount);
            ans += 2 * count * ((parity == 1) ? evenCount : oddCount);
            ans *= mask;
        }

        // Return the readonly sum
        return ans;
    }

    // Driver Code
    public static void Main(String[] args) {
        int[] arr = { 2, 1, 4, 4, 2 };

        // Function call
        findSum(arr);
    }
}

// This code is contributed by gauravrajput1**
```

## ****java 描述语言****

```
**<script>
// javascript program for the above approach

    // Function to calculate sum of
    // maximum of all subarrays
    function findSum(a) {
        var ans = 0;
        var prev = -1;

        // Iterate over the range [30, 0]
        for (var i = 30; i >= 0; i--) {
            var mask = (1 << i);

            // Inner loop through the
            // length of the array
            for (var j = 0; j < a.length; j++) {

                // Divide the array such
                // that no subarray will
                // have any index set to -1
                if (a[j] == -1) {
                    ans += findSumOfValuesOfRange(a, prev + 1, j - 1, mask);
                    prev = j;
                }
            }

            // Find the sum of subarray
            ans += findSumOfValuesOfRange(a, prev + 1, a.length - 1, mask);
        }

        // Print the sum obtained
        document.write(ans);
    }

    // Function that takes any subarray
    // S and return values contributed
    // by only the subarrays in S containing mask
    function findSumOfValuesOfRange(a , low , high , mask) {
        if (low > high)
            return 0;

        // Stores count even, odd count of
        // occurrences and maximum element
        var evenCount = 0, oddCount = 0, countLargestNumber = 0;
        var prev = low - 1, ans = 0;

        // Traverse from low to high
        for (var i = low; i <= high; i++) {

            // Checking if this position
            // in the array is mask
            if ((mask & a[i]) > 0) {

                // Mask is the largest
                // number in subarray.
                // Increment count by 1
                countLargestNumber++;

                // Store parity as 0 or 1
                var parity = countLargestNumber % 2;

                // Setting a[i]=-1, this
                // will help in splitting
                // array into subarrays
                a[i] = -1;
                var count = i - prev;
                ans += count;

                // Add values contributed
                // by those subarrays that
                // have an odd frequency
                ans += (count - 1) * ((parity == 1) ? evenCount : oddCount);
                ans += ((parity == 1) ? oddCount : evenCount);

                // Adding values contributed
                // by those subarrays that
                // have an even frequency
                ans += 2 * (count - 1) * ((parity == 1) ? oddCount : evenCount);
                ans += 2 * ((parity == 1) ? evenCount : oddCount);

                // Set the prev pointer
                // to this position
                prev = i;

                if (parity == 1)
                    oddCount += count;
                else
                    evenCount += count;
            }
        }

        if (prev != low - 1) {
            var count = high - prev;
            var parity = countLargestNumber % 2;

            ans += count * ((parity == 1) ? oddCount : evenCount);
            ans += 2 * count * ((parity == 1) ? evenCount : oddCount);
            ans *= mask;
        }

        // Return the final sum
        return ans;
    }

    // Driver Code
        var arr = [ 2, 1, 4, 4, 2 ];

        // Function call
        findSum(arr);

// This code is contributed by gauravrajput1
</script>**
```

******Output:** 

```
75
```**** 

*******时间复杂度:** O(30*N)*
***辅助空间:** O(1)*****