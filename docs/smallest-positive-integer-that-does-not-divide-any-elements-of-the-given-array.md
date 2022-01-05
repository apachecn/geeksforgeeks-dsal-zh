# 不划分给定数组任何元素的最小正整数

> 原文:[https://www . geeksforgeeks . org/给定数组中不除任何元素的最小正整数/](https://www.geeksforgeeks.org/smallest-positive-integer-that-does-not-divide-any-elements-of-the-given-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是确定最小的正整数 **K** ，使得数组元素都不能被 **K** 整除。如果没有这样的整数

**示例:**

> **输入:** arr[] = {3，2，6，9，2}
> **输出:** 4
> **解释:**没有一个数组元素可以被 4 整除(最小的正数)。
> 
> **输入:** arr[] = {3，5，1，19，11 }
> T3】输出: 2

**方法:**按照以下步骤解决问题:

*   [找到给定数组的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，说 **maxE** 。
*   使用变量 **i** 迭代范围**【1，MaxE+1】**，检查给定数组中是否有可被 **i** 整除的整数。如果发现为真，则检查该范围内的下一个整数。
*   否则，打印当前编号 **i** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the smallest number
// which doesn't divides any integer in
// the given array arr[]
void smallestNumber(int arr[], int len)
{
    int maxi = 0;

    // Traverse the array arr[]
    for (int i = 0; i < len; i++) {

        // Maximum array element
        maxi = std::max(maxi, arr[i]);
    }

    // Initialize variable
    int ans = -1;

    // Traverse from 2 to max
    for (int i = 2; i < maxi + 2; i++) {

        // Stores if any such
        // integer is found or not
        bool flag = true;

        for (int j = 0; j < len; j++) {

            // If any array element
            // is divisible by j
            if (arr[j] % i == 0) {

                flag = false;
                break;
            }
        }

        if (flag) {

            // Smallest integer
            ans = i;
            break;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 6, 9, 2 };
    int N = sizeof(arr)
/ sizeof(arr[0]);

    // Function Call
    smallestNumber(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the smallest number
// which doesn't divides any integer in
// the given array arr[]
static void smallestNumber(int arr[], int len)
{
    int maxi = 0;

    // Traverse the array arr[]
    for (int i = 0; i < len; i++)
    {

        // Maximum array element
        maxi = Math.max(maxi, arr[i]);
    }

    // Initialize variable
    int ans = -1;

    // Traverse from 2 to max
    for (int i = 2; i < maxi + 2; i++)
    {

        // Stores if any such
        // integer is found or not
        boolean flag = true;
        for (int j = 0; j < len; j++)
        {

            // If any array element
            // is divisible by j
            if (arr[j] % i == 0)
            {
                flag = false;
                break;
            }
        }

        if (flag)
        {

            // Smallest integer
            ans = i;
            break;
        }
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 6, 9, 2 };
    int N = arr.length;

    // Function Call
    smallestNumber(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest number
# which doesn't divides any integer in
# the given array arr[]
def smallestNumber(arr, lenn):
    maxi = 0

    # Traverse the array arr[]
    for i in range(lenn):

        # Maximum array element
        maxi = max(maxi, arr[i])

    # Initialize variable
    ans = -1

    # Traverse from 2 to max
    for i in range(2, maxi + 2):

        # Stores if any such
        # integer is found or not
        flag = True
        for j in range(lenn):

            # If any array element
            # is divisible by j
            if (arr[j] % i == 0):
                flag = False
                break
        if (flag):

            # Smallest integer
            ans = i
            break

    # Prthe answer
    print (ans)

# Driver Code
if __name__ == '__main__':
    arr = [3, 2, 6, 9, 2]
    N = len(arr)

    #Function Call
    smallestNumber(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the smallest number
  // which doesn't divides any integer in
  // the given array arr[]
  static void smallestNumber(int []arr, int len)
  {
    int maxi = 0;

    // Traverse the array arr[]
    for (int i = 0; i < len; i++)
    {

      // Maximum array element
      maxi = Math.Max(maxi, arr[i]);
    }

    // Initialize variable
    int ans = -1;

    // Traverse from 2 to max
    for (int i = 2; i < maxi + 2; i++)
    {

      // Stores if any such
      // integer is found or not
      bool flag = true;
      for (int j = 0; j < len; j++)
      {

        // If any array element
        // is divisible by j
        if (arr[j] % i == 0)
        {
          flag = false;
          break;
        }
      }
      if (flag)
      {

        // Smallest integer
        ans = i;
        break;
      }
    }

    // Print the answer
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int []arr = { 3, 2, 6, 9, 2 };
    int N = arr.Length;

    // Function Call
    smallestNumber(arr, N);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to find the smallest number
// which doesn't divides any integer in
// the given array arr[]
function smallestNumber(arr, len)
{
    let maxi = 0;

    // Traverse the array arr[]
    for (let i = 0; i < len; i++)
    {

        // Maximum array element
        maxi = Math.max(maxi, arr[i]);
    }

    // Initialize variable
    let ans = -1;

    // Traverse from 2 to max
    for (let i = 2; i < maxi + 2; i++)
    {

        // Stores if any such
        // integer is found or not
        let flag = true;
        for (let j = 0; j < len; j++)
        {

            // If any array element
            // is divisible by j
            if (arr[j] % i == 0)
            {
                flag = false;
                break;
            }
        }

        if (flag)
        {

            // Smallest integer
            ans = i;
            break;
        }
    }

    // Print the answer
    document.write(ans);
}

    // Driver Code

    let arr = [ 3, 2, 6, 9, 2 ];
    let N = arr.length;

    // Function Call
    smallestNumber(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * max)**max**是给定数组中最大的元素*
***辅助空间:** O(N)*