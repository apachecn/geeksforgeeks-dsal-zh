# 给定一个数组 A[]和一个数字 x，检查 A[]中的对，其和为 x |集合 2

> 原文:[https://www . geesforgeks . org/给定一个数组和一个数字-x-检查一对和作为 x-set-2/](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x-set-2/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从数组 **arr[]** 中找到两个具有和 **X** 的元素。如果不存在这样的数字，则打印**-1”**。

**示例:**

> **输入:** arr[] = {0，-1，2，-3，1}，X = -2
> **输出:** -3，1
> **解释:**
> 从给定数组中-3 和 1 的和等于-2 (= X)。
> 
> **输入:** arr[] = {1，-2，1，0，5}，X = 0
> T3】输出: -1

**方法:**给定的问题可以通过使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决，思路是[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序**A【】**，对于每个数组元素 **A[i]** ，搜索数组中是否存在另一个值**(X–A[I])**。按照以下步骤解决问题:

*   [按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对给定数组 **arr[]** 进行排序。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**对于每个数组元素**A【I】**，将两个变量**低**和**高**分别初始化为 **0** 和**(N–1)**。现在，按照以下步骤执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/):
    *   如果数组**arr【】**中索引**中间**处的值为**(X–A[I])**，则打印该当前对并[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   更新**中间**为**(低+高)/2** 。
    *   如果 **A【中】**的值小于 **X** ，则将**低**更新为**(中+ 1)** 。否则，将**高电平**更新为**(中-1)**。
*   完成上述步骤后，如果没有找到这样的配对，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the array has
// 2 elements whose sum is equal to
// the given value
void hasArrayTwoPairs(int nums[],
                      int n, int target)
{
    // Sort the array in increasing order
    sort(nums, nums + n);

    // Traverse the array, nums[]
    for (int i = 0; i < n; i++) {

        // Store the required number
        // to be found
        int x = target - nums[i];

        // Perform binary search
        int low = 0, high = n - 1;
        while (low <= high) {

            // Store the mid value
            int mid = low
                      + ((high - low) / 2);

            // If nums[mid] is greater
            // than x, then update
            // high to mid - 1
            if (nums[mid] > x) {
                high = mid - 1;
            }

            // If nums[mid] is less
            // than x, then update
            // low to mid + 1
            else if (nums[mid] < x) {
                low = mid + 1;
            }

            // Otherwise
            else {

                // If mid is equal i,
                // check mid-1 and mid+1
                if (mid == i) {
                    if ((mid - 1 >= 0)
                        && nums[mid - 1] == x) {
                        cout << nums[i] << ", ";
                        cout << nums[mid - 1];
                        return;
                    }
                    if ((mid + 1 < n)
                        && nums[mid + 1] == x) {
                        cout << nums[i] << ", ";
                        cout << nums[mid + 1];
                        return;
                    }
                    break;
                }

                // Otherwise, print the
                // pair and return
                else {
                    cout << nums[i] << ", ";
                    cout << nums[mid];
                    return;
                }
            }
        }
    }

    // If no such pair is found,
    // then print -1
    cout << -1;
}

// Driver Code
int main()
{
    int A[] = { 0, -1, 2, -3, 1 };
    int X = -2;
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    hasArrayTwoPairs(A, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to check if the array has
  // 2 elements whose sum is equal to
  // the given value
  static void hasArrayTwoPairs(int nums[],
                               int n, int target)
  {

    // Sort the array in increasing order
    Arrays.sort(nums);

    // Traverse the array, nums[]
    for (int i = 0; i < n; i++) {

      // Store the required number
      // to be found
      int x = target - nums[i];

      // Perform binary search
      int low = 0, high = n - 1;
      while (low <= high) {

        // Store the mid value
        int mid = low
          + ((high - low) / 2);

        // If nums[mid] is greater
        // than x, then update
        // high to mid - 1
        if (nums[mid] > x) {
          high = mid - 1;
        }

        // If nums[mid] is less
        // than x, then update
        // low to mid + 1
        else if (nums[mid] < x) {
          low = mid + 1;
        }

        // Otherwise
        else {

          // If mid is equal i,
          // check mid-1 and mid+1
          if (mid == i) {
            if ((mid - 1 >= 0)
                && nums[mid - 1] == x) {
              System.out.print(nums[i] + ", ");
              System.out.print( nums[mid - 1]);
              return;
            }
            if ((mid + 1 < n)
                && nums[mid + 1] == x) {
              System.out.print( nums[i] + ", ");
              System.out.print( nums[mid + 1]);
              return;
            }
            break;
          }

          // Otherwise, print the
          // pair and return
          else {
            System.out.print( nums[i] + ", ");
            System.out.print(nums[mid]);
            return;
          }
        }
      }
    }

    // If no such pair is found,
    // then print -1
    System.out.print(-1);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int A[] = { 0, -1, 2, -3, 1 };
    int X = -2;
    int N = A.length;

    // Function Call
    hasArrayTwoPairs(A, N, X);
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the array has
# 2 elements whose sum is equal to
# the given value
def hasArrayTwoPairs(nums, n, target):

    # Sort the array in increasing order
    nums = sorted(nums)

    # Traverse the array, nums[]
    for i in range(n):

        # Store the required number
        # to be found
        x = target - nums[i]

        # Perform binary search
        low, high = 0, n - 1
        while (low <= high):

            # Store the mid value
            mid = low + ((high - low) // 2)

            # If nums[mid] is greater
            # than x, then update
            # high to mid - 1
            if (nums[mid] > x):
                high = mid - 1

            # If nums[mid] is less
            # than x, then update
            # low to mid + 1
            elif (nums[mid] < x):
                low = mid + 1

            # Otherwise
            else:

                # If mid is equal i,
                # check mid-1 and mid+1
                if (mid == i):
                    if ((mid - 1 >= 0) and nums[mid - 1] == x):
                        print(nums[i], end = ", ")
                        print(nums[mid - 1])
                        return
                    if ((mid + 1 < n) and nums[mid + 1] == x):
                        print(nums[i], end = ", ")
                        print(nums[mid + 1])
                        return
                    break

                # Otherwise, print the
                # pair and return
                else:
                    print(nums[i], end = ", ")
                    print(nums[mid])
                    return

    # If no such pair is found,
    # then print -1
    print (-1)

# Driver Code
if __name__ == '__main__':

    A = [0, -1, 2, -3, 1]
    X = -2
    N = len(A)

    # Function Call
    hasArrayTwoPairs(A, N, X)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to check if the array has
    // 2 elements whose sum is equal to
    // the given value
    static void hasArrayTwoPairs(int[] nums, int n, int target)
    {

        // Sort the array in increasing order
        Array.Sort(nums);

        // Traverse the array, nums[]
        for (int i = 0; i < n; i++)
        {

            // Store the required number
            // to be found
            int x = target - nums[i];

            // Perform binary search
            int low = 0, high = n - 1;
            while (low <= high)
            {

                // Store the mid value
                int mid = low + ((high - low) / 2);

                // If nums[mid] is greater
                // than x, then update
                // high to mid - 1
                if (nums[mid] > x) {
                    high = mid - 1;
                }

                // If nums[mid] is less
                // than x, then update
                // low to mid + 1
                else if (nums[mid] < x) {
                    low = mid + 1;
                }

                // Otherwise
                else {

                    // If mid is equal i,
                    // check mid-1 and mid+1
                    if (mid == i) {
                        if ((mid - 1 >= 0) && nums[mid - 1] == x) {
                            Console.Write(nums[i] + ", ");
                            Console.Write( nums[mid - 1]);
                            return;
                        }
                        if ((mid + 1 < n) && nums[mid + 1] == x) {
                            Console.Write( nums[i] + ", ");
                            Console.Write( nums[mid + 1]);
                            return;
                        }
                        break;
                    }

                    // Otherwise, print the
                    // pair and return
                    else {
                        Console.Write( nums[i] + ", ");
                        Console.Write(nums[mid]);
                        return;
                    }
                }
            }
        }

        // If no such pair is found,
        // then print -1
        Console.Write(-1);
    }

    // Driver Code
    static public void Main (){
        int[] A = { 0, -1, 2, -3, 1 };
        int X = -2;
        int N = A.Length;

        // Function Call
        hasArrayTwoPairs(A, N, X);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the array has
// 2 elements whose sum is equal to
// the given value
function hasArrayTwoPairs(nums, n, target)
{
    // Sort the array in increasing order
    nums.sort();
    var i;
    // Traverse the array, nums[]
    for (i = 0; i < n; i++) {

        // Store the required number
        // to be found
        var x = target - nums[i];

        // Perform binary search
        var low = 0, high = n - 1;
        while (low <= high) {

            // Store the mid value
            var mid = low
                      + (Math.floor((high - low) / 2));

            // If nums[mid] is greater
            // than x, then update
            // high to mid - 1
            if (nums[mid] > x) {
                high = mid - 1;
            }

            // If nums[mid] is less
            // than x, then update
            // low to mid + 1
            else if (nums[mid] < x) {
                low = mid + 1;
            }

            // Otherwise
            else {

                // If mid is equal i,
                // check mid-1 and mid+1
                if (mid == i) {
                    if ((mid - 1 >= 0)
                        && nums[mid - 1] == x) {
                        document.write(nums[i] + ", ");
                        document.write(nums[mid - 1]);
                        return;
                    }
                    if ((mid + 1 < n) && nums[mid + 1] == x) {
                        document.write(nums[i] + ", ");
                        document.write(nums[mid + 1]);
                        return;
                    }
                    break;
                }

                // Otherwise, print the
                // pair and return
                else {
                    document.write(nums[i] +", ");
                    document.write(nums[mid]);
                    return;
                }
            }
        }
    }

    // If no such pair is found,
    // then print -1
    document.write(-1);
}

// Driver Code
    var A =  [0, -1, 2, -3, 1];
    var X = -2;
    var N = A.length;

    // Function Call
    hasArrayTwoPairs(A, N, X);

</script>
```

**Output:** 

```
-3, 1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*

**替代方法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/)了解更多解决这个问题的方法。