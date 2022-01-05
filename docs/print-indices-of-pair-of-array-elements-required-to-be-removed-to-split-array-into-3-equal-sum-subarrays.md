# 打印需要移除的阵列元素对的索引，以将阵列分割成 3 个相等和的子阵列

> 原文:[https://www . geesforgeks . org/print-indexs-数组元素对-需要移除-将数组拆分为 3 个等和子数组/](https://www.geeksforgeeks.org/print-indices-of-pair-of-array-elements-required-to-be-removed-to-split-array-into-3-equal-sum-subarrays/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是打印需要移除的两个数组元素的索引，这样给定的[数组可以被分成三个相等和的子数组](https://www.geeksforgeeks.org/split-array-three-equal-sum-subarrays/)。如果不可能，则打印**-1”**。

**示例:**

> **输入:** arr[] = {2，5，12，7，19，4，3}
> **输出:** 2 4
> **解释:**
> 移除 arr[2]和 arr[4]将 arr[]修改为{2，5，7，4，3}。
> 子阵{arr[0]，arr[1]}之和= 7。
> arr[2] = 7。
> 子阵{arr[3]，arr[4]}之和= 7。
> 
> **输入:** arr[] = {2，1，13，5，14}
> **输出:** -1

**天真方法:**最简单的方法是[生成所有可能的阵列元素对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每一对，检查移除这些对是否可以从给定阵列生成三个相等和的子阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if array can
// be split into three equal sum
// subarrays by removing two elements
void findSplit(int arr[], int N)
{
    for (int l = 1; l <= N - 4; l++) {

        for (int r = l + 2; r <= N - 2; r++) {

            // Stores sum of all three subarrays
            int lsum = 0, rsum = 0, msum = 0;

            // Sum of left subarray
            for (int i = 0; i <= l - 1; i++) {
                lsum += arr[i];
            }

            // Sum of middle subarray
            for (int i = l + 1; i <= r - 1; i++) {
                msum += arr[i];
            }

            // Sum of right subarray
            for (int i = r + 1; i < N; i++) {
                rsum += arr[i];
            }

            // Check if sum of subarrays are equal
            if (lsum == rsum && rsum == msum) {

                // Print the possible pair
                cout << l << " " << r << endl;
                return;
            }
        }
    }

    // If no pair exists, print -1
    cout << -1 << endl;
}

// Driver code
int main()
{
    // Given array
    int arr[] = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    findSplit(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to check if array can
// be split into three equal sum
// subarrays by removing two elements
static void findSplit(int arr[], int N)
{
    for (int l = 1; l <= N - 4; l++)
    {
        for (int r = l + 2; r <= N - 2; r++)
        {

            // Stores sum of all three subarrays
            int lsum = 0, rsum = 0, msum = 0;

            // Sum of left subarray
            for (int i = 0; i <= l - 1; i++) {
                lsum += arr[i];
            }

            // Sum of middle subarray
            for (int i = l + 1; i <= r - 1; i++) {
                msum += arr[i];
            }

            // Sum of right subarray
            for (int i = r + 1; i < N; i++) {
                rsum += arr[i];
            }

            // Check if sum of subarrays are equal
            if (lsum == rsum && rsum == msum) {

                // Print the possible pair
                System.out.println( l + " " + r );
                return;
            }
        }
    }

    // If no pair exists, print -1
    System.out.print(-1 );
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = arr.length;
    findSplit(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Pyhton 3 program for the above approach

# Function to check if array can
# be split into three equal sum
# subarrays by removing two elements
def findSplit(arr, N):
    for l in range(1, N - 3, 1):
        for r in range(l + 2, N - 1, 1):

            # Stores sum of all three subarrays
            lsum = 0
            rsum = 0
            msum = 0

            # Sum of left subarray
            for i in range(0, l, 1):
                lsum += arr[i]

            # Sum of middle subarray
            for i in range(l + 1, r, 1):
                msum += arr[i]

            # Sum of right subarray
            for i in range(r + 1, N, 1):
                rsum += arr[i]

            # Check if sum of subarrays are equal
            if (lsum == rsum and rsum == msum):

                # Print the possible pair
                print(l, r)
                return

    # If no pair exists, print -1
    print(-1)

# Driver code
if __name__ == '__main__':

    # Given array
    arr =  [2, 5, 12, 7, 19, 4, 3]

    # Size of the array
    N = len(arr)
    findSplit(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to check if array can
  // be split into three equal sum
  // subarrays by removing two elements
  static void findSplit(int []arr, int N)
  {
    for (int l = 1; l <= N - 4; l++)
    {
      for (int r = l + 2; r <= N - 2; r++)
      {

        // Stores sum of all three subarrays
        int lsum = 0, rsum = 0, msum = 0;

        // Sum of left subarray
        for (int i = 0; i <= l - 1; i++) {
          lsum += arr[i];
        }

        // Sum of middle subarray
        for (int i = l + 1; i <= r - 1; i++) {
          msum += arr[i];
        }

        // Sum of right subarray
        for (int i = r + 1; i < N; i++) {
          rsum += arr[i];
        }

        // Check if sum of subarrays are equal
        if (lsum == rsum && rsum == msum) {

          // Print the possible pair
          Console.WriteLine( l + " " + r );
          return;
        }
      }
    }

    // If no pair exists, print -1
    Console.Write(-1 );
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given array
    int []arr = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = arr.Length;
    findSplit(arr, N);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if array can
    // be split into three equal sum
    // subarrays by removing two elements
    function findSplit(arr, N)
    {
      for (let l = 1; l <= N - 4; l++)
      {
        for (let r = l + 2; r <= N - 2; r++)
        {

          // Stores sum of all three subarrays
          let lsum = 0, rsum = 0, msum = 0;

          // Sum of left subarray
          for (let i = 0; i <= l - 1; i++) {
            lsum += arr[i];
          }

          // Sum of middle subarray
          for (let i = l + 1; i <= r - 1; i++) {
            msum += arr[i];
          }

          // Sum of right subarray
          for (let i = r + 1; i < N; i++) {
            rsum += arr[i];
          }

          // Check if sum of subarrays are equal
          if (lsum == rsum && rsum == msum) {

            // Print the possible pair
            document.write( l + " " + r + "</br>");
            return;
          }
        }
      }

      // If no pair exists, print -1
      document.write(-1 );
    }

    // Given array
    let arr = [ 2, 5, 12, 7, 19, 4, 3 ];

    // Size of the array
    let N = arr.length;
    findSplit(arr, N);

</script>
```

**Output:** 

```
2 4
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是利用[前缀和数组技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)在恒定时间内找到所有子阵和。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **和**来存储数组的前缀和。
*   初始化两个变量，比如说 **l** & **r、**来存储两个要删除的索引，以便将数组拆分成 3 个相等和的子数组。
*   三个子阵列的总和将是**总和【l–1】**、**总和【r–1】–总和【l】**和**总和【N–1】–总和【r】**。
*   使用变量 **l:** 迭代范围**【1，N–4】**
    *   使用变量 **r** 迭代范围**【l+2，N–2】**，并检查在任何一点，左子阵和是否等于中子阵和和右子阵和，然后打印 **l** & **r** 的值并返回。
*   如果不存在这样的配对，打印 **-1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if array can
// be split into three equal sum
// subarrays by removing a pair
void findSplit(int arr[], int N)
{
    // Stores prefix sum array
    vector<int> sum(N);

    // Copy array elements
    for (int i = 0; i < N; i++) {
        sum[i] = arr[i];
    }

    // Traverse the array
    for (int i = 1; i < N; i++) {
        sum[i] += sum[i - 1];
    }

    for (int l = 1; l <= N - 4; l++) {

        for (int r = l + 2; r <= N - 2; r++) {

            // Stores sums of all three subarrays
            int lsum = 0, rsum = 0, msum = 0;

            // Sum of left subarray
            lsum = sum[l - 1];

            // Sum of middle subarray
            msum = sum[r - 1] - sum[l];

            // Sum of right subarray
            rsum = sum[N - 1] - sum[r];

            // Check if sum of subarrays are equal
            if (lsum == rsum && rsum == msum) {

                // Print the possible pair
                cout << l << " " << r << endl;
                return;
            }
        }
    }

    // If no such pair exists, print -1
    cout << -1 << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    findSplit(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to check if array can
// be split into three equal sum
// subarrays by removing a pair
static void findSplit(int arr[], int N)
{

    // Stores prefix sum array
    int []sum = new int[N];

    // Copy array elements
    for (int i = 0; i < N; i++)
    {
        sum[i] = arr[i];
    }

    // Traverse the array
    for (int i = 1; i < N; i++)
    {
        sum[i] += sum[i - 1];
    }

    for (int l = 1; l <= N - 4; l++) {

        for (int r = l + 2; r <= N - 2; r++) {

            // Stores sums of all three subarrays
            int lsum = 0, rsum = 0, msum = 0;

            // Sum of left subarray
            lsum = sum[l - 1];

            // Sum of middle subarray
            msum = sum[r - 1] - sum[l];

            // Sum of right subarray
            rsum = sum[N - 1] - sum[r];

            // Check if sum of subarrays are equal
            if (lsum == rsum && rsum == msum) {

                // Print the possible pair
                System.out.print(l+ " " +  r +"\n");
                return;
            }
        }
    }

    // If no such pair exists, print -1
    System.out.print(-1 +"\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = arr.length;
    findSplit(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if array can
# be split into three equal sum
# subarrays by removing a pair
def findSplit(arr, N):

    # Stores prefix sum array
    sum = [i for i in arr]

    # Traverse the array
    for i in range(1, N):
        sum[i] += sum[i - 1]

    for l in range(1, N - 3):
        for r in range(l + 2, N - 1):

            # Stores sums of all three subarrays
            lsum , rsum , msum =0, 0, 0

            # Sum of left subarray
            lsum = sum[l - 1]

            # Sum of middle subarray
            msum = sum[r - 1] - sum[l]

            # Sum of right subarray
            rsum = sum[N - 1] - sum[r]

            # Check if sum of subarrays are equal
            if (lsum == rsum and rsum == msum):

                # Print possible pair
                print(l, r)
                return

    # If no such pair exists, print -1
    print (-1)

# Driver Code
if __name__ == '__main__':
    # Given array
    arr = [2, 5, 12, 7, 19, 4, 3 ]

    # Size of the array
    N = len(arr)

    findSplit(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to check if array can
// be split into three equal sum
// subarrays by removing a pair
static void findSplit(int []arr, int N)
{

    // Stores prefix sum array
    int []sum = new int[N];

    // Copy array elements
    for (int i = 0; i < N; i++)
    {
        sum[i] = arr[i];
    }

    // Traverse the array
    for (int i = 1; i < N; i++)
    {
        sum[i] += sum[i - 1];
    }

    for (int l = 1; l <= N - 4; l++) {
        for (int r = l + 2; r <= N - 2; r++) {

            // Stores sums of all three subarrays
            int lsum = 0, rsum = 0, msum = 0;

            // Sum of left subarray
            lsum = sum[l - 1];

            // Sum of middle subarray
            msum = sum[r - 1] - sum[l];

            // Sum of right subarray
            rsum = sum[N - 1] - sum[r];

            // Check if sum of subarrays are equal
            if (lsum == rsum && rsum == msum) {

                // Print the possible pair
                Console.Write(l+ " " +  r +"\n");
                return;
            }
        }
    }

    // If no such pair exists, print -1
    Console.Write(-1 +"\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = arr.Length;
    findSplit(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if array can
    // be split into three equal sum
    // subarrays by removing a pair
    function findSplit(arr, N)
    {

        // Stores prefix sum array
        let sum = new Array(N);

        // Copy array elements
        for (let i = 0; i < N; i++)
        {
            sum[i] = arr[i];
        }

        // Traverse the array
        for (let i = 1; i < N; i++)
        {
            sum[i] += sum[i - 1];
        }

        for (let l = 1; l <= N - 4; l++) {
            for (let r = l + 2; r <= N - 2; r++) {

                // Stores sums of all three subarrays
                let lsum = 0, rsum = 0, msum = 0;

                // Sum of left subarray
                lsum = sum[l - 1];

                // Sum of middle subarray
                msum = sum[r - 1] - sum[l];

                // Sum of right subarray
                rsum = sum[N - 1] - sum[r];

                // Check if sum of subarrays are equal
                if (lsum == rsum && rsum == msum) {

                    // Print the possible pair
                    document.write(l+ " " +  r +"</br>");
                    return;
                }
            }
        }

        // If no such pair exists, print -1
        document.write(-1 +"</br>");
    }

    // Given array
    let arr = [ 2, 5, 12, 7, 19, 4, 3 ];

    // Size of the array
    let N = arr.length;
    findSplit(arr, N);

</script>
```

**Output:** 

```
2 4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**最佳方案:**最佳方案是在使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的同时，使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的向量来存储数组的前缀和。
*   初始化两个变量，比如说 **l** & **r** ，使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)遍历数组。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)直到 **l < r** 或者直到所有三个和都相等:
    *   如果左子阵列的总和大于右子阵列的总和，则在右子阵列上增加一个额外的元素。因此，将 **r** 的值减少 **1** 。
    *   如果右子阵列的总和大于左子阵列的总和，则在左子阵列上添加一个元素。因此，用 **1** 增加 **l** 。
    *   如果左右子阵列之和相等，但不等于中间子阵列之和，则增加 **1** 的 **l** ，减少 **r** 的 **1** 。
*   如果不存在这样的配对，打印 **-1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if array can
// be split into three equal sum
// subarrays by removing a pair
void findSplit(int arr[], int N)
{
    // Two pointers l and r
    int l = 1, r = N - 2;
    int lsum, msum, rsum;

    // Stores prefix sum array
    vector<int> sum(N);
    sum[0] = arr[0];

    // Traverse the array
    for (int i = 1; i < N; i++) {
        sum[i] = sum[i - 1] + arr[i];
    }

    // Two pointer approach
    while (l < r) {

        // Sum of left subarray
        lsum = sum[l - 1];

        // Sum of middle subarray
        msum = sum[r - 1] - sum[l];

        // Sum of right subarray
        rsum = sum[N - 1] - sum[r];

        // Print split indices if sum is equal
        if (lsum == msum and msum == rsum) {
            cout << l << " " << r << endl;
            return;
        }

        // Move left pointer if lsum < rsum
        if (lsum < rsum)
            l++;

        // Move right pointer if rsum > lsum
        else if (lsum > rsum)
            r--;

        // Move both pointers if lsum = rsum
        // but they are not equal to msum
        else {
            l++;
            r--;
        }
    }

    // If no possible pair exists, print -1
    cout << -1 << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    findSplit(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

  // Function to check if array can
  // be split into three equal sum
  // subarrays by removing a pair
  static void findSplit(int []arr, int N)
  {

    // Two pointers l and r
    int l = 1, r = N - 2;
    int lsum, msum, rsum;

    // Stores prefix sum array
    int sum[] = new int[N];

    sum[0] = arr[0];

    // Traverse the array
    for (int i = 1; i < N; i++) {
      sum[i] = sum[i - 1] + arr[i];
    }

    // Two pointer approach
    while (l < r) {

      // Sum of left subarray
      lsum = sum[l - 1];

      // Sum of middle subarray
      msum = sum[r - 1] - sum[l];

      // Sum of right subarray
      rsum = sum[N - 1] - sum[r];

      // Print split indices if sum is equal
      if (lsum == msum && msum == rsum) {
        System.out.println(l + " " + r);
        return;
      }

      // Move left pointer if lsum < rsum
      if (lsum < rsum)
        l++;

      // Move right pointer if rsum > lsum
      else if (lsum > rsum)
        r--;

      // Move both pointers if lsum = rsum
      // but they are not equal to msum
      else {
        l++;
        r--;
      }
    }

    // If no possible pair exists, print -1
    System.out.println(-1);
  }

  // Driver Code
  public static void main (String[] args)
  {
    // Given array
    int []arr = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = arr.length;

    findSplit(arr, N);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if array can
# be split into three equal sum
# subarrays by removing a pair
def findSplit(arr, N) :

    # Two pointers l and r
    l = 1; r = N - 2;

    # Stores prefix sum array
    sum = [0]*N;
    sum[0] = arr[0];

    # Traverse the array
    for i in range(1, N) :
        sum[i] = sum[i - 1] + arr[i];

    # Two pointer approach
    while (l < r) :

        # Sum of left subarray
        lsum = sum[l - 1];

        # Sum of middle subarray
        msum = sum[r - 1] - sum[l];

        # Sum of right subarray
        rsum = sum[N - 1] - sum[r];

        # Print split indices if sum is equal
        if (lsum == msum and msum == rsum) :
            print(l,r);
            return;

        # Move left pointer if lsum < rsum
        if (lsum < rsum) :
            l += 1;

        # Move right pointer if rsum > lsum
        elif (lsum > rsum) :
            r -= 1;

        # Move both pointers if lsum = rsum
        # but they are not equal to msum
        else :
            l += 1;
            r -= 1;

    # If no possible pair exists, print -1
    print(-1);

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 2, 5, 12, 7, 19, 4, 3 ];

    # Size of the array
    N = len(arr);

    findSplit(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to check if array can
    // be split into three equal sum
    // subarrays by removing a pair
    static void findSplit(int[] arr, int N)
    {

      // Two pointers l and r
      int l = 1, r = N - 2;
      int lsum, msum, rsum;

      // Stores prefix sum array
      int[] sum = new int[N];

      sum[0] = arr[0];

      // Traverse the array
      for (int i = 1; i < N; i++) {
        sum[i] = sum[i - 1] + arr[i];
      }

      // Two pointer approach
      while (l < r) {

        // Sum of left subarray
        lsum = sum[l - 1];

        // Sum of middle subarray
        msum = sum[r - 1] - sum[l];

        // Sum of right subarray
        rsum = sum[N - 1] - sum[r];

        // Print split indices if sum is equal
        if (lsum == msum && msum == rsum) {
          Console.Write(l + " " + r);
          return;
        }

        // Move left pointer if lsum < rsum
        if (lsum < rsum)
          l++;

        // Move right pointer if rsum > lsum
        else if (lsum > rsum)
          r--;

        // Move both pointers if lsum = rsum
        // but they are not equal to msum
        else {
          l++;
          r--;
        }
      }

      // If no possible pair exists, print -1
      Console.Write(-1);
    }

  static void Main()
  {

    // Given array
    int[] arr = { 2, 5, 12, 7, 19, 4, 3 };

    // Size of the array
    int N = arr.Length;

    findSplit(arr, N);
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if array can
    // be split into three equal sum
    // subarrays by removing a pair
    function findSplit(arr, N)
    {

      // Two pointers l and r
      let l = 1, r = N - 2;
      let lsum, msum, rsum;

      // Stores prefix sum array
      let sum = new Array(N);

      sum[0] = arr[0];

      // Traverse the array
      for (let i = 1; i < N; i++) {
        sum[i] = sum[i - 1] + arr[i];
      }

      // Two pointer approach
      while (l < r) {

        // Sum of left subarray
        lsum = sum[l - 1];

        // Sum of middle subarray
        msum = sum[r - 1] - sum[l];

        // Sum of right subarray
        rsum = sum[N - 1] - sum[r];

        // Print split indices if sum is equal
        if (lsum == msum && msum == rsum) {
          document.write(l + " " + r);
          return;
        }

        // Move left pointer if lsum < rsum
        if (lsum < rsum)
          l++;

        // Move right pointer if rsum > lsum
        else if (lsum > rsum)
          r--;

        // Move both pointers if lsum = rsum
        // but they are not equal to msum
        else {
          l++;
          r--;
        }
      }

      // If no possible pair exists, print -1
      document.write(-1);
    }

    // Given array
    let arr = [ 2, 5, 12, 7, 19, 4, 3 ];

    // Size of the array
    let N = arr.length;

    findSplit(arr, N);

</script>
```

**Output:** 

```
2 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)