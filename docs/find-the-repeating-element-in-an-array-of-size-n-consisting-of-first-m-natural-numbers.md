# 在由前 M 个自然数组成的 N 大小数组中找到重复元素

> 原文:[https://www . geesforgeks . org/find-由第一个 m 个自然数组成的 n 大小数组中的重复元素/](https://www.geeksforgeeks.org/find-the-repeating-element-in-an-array-of-size-n-consisting-of-first-m-natural-numbers/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，其中包含从 **1 到 M** 的数字[排列，以及一个重复的元素(一次或多次)，任务是找到重复的元素。](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)

**示例:**

> **输入:** arr[]={2，6，4，3，1，5，2}，N=7
> **输出:**
> 2
> **说明:**在 arr[]中，从 0 到 6 的所有元素都出现一次，除了 2 重复一次。
> 
> **输入:** arr[]={2，1，3，1，1，1}，N = 6
> T3】输出:T5】1

**天真方法:**天真方法是对数组进行排序，并检查相邻的元素是否相等。

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*

**方法:**按照以下步骤解决问题:

1.  初始化两个变量 **M** 和**和**分别存储数组的最大元素和[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr** 并执行以下操作:
    1.  将当前元素添加到**和**中
    2.  将当前元素与 **M** 进行比较，计算出[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。
3.  将从 **1 到 M** 的排列总和存储在一个变量中，例如 **sum1** ，使用公式:

```
Sum of elements from 1 to X= X*(X+1)/2
```

1.  计算答案为**总和**和**总和**除以额外字符数，即**(总和-总和 1)/(N-M)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the repeating character in a given
// permutation
int repeatingElement(int arr[], int N)
{
    // variables to store maximum element and sum of the
    // array respectively.
    int M = 0, sum = 0;
    for (int i = 0; i < N; i++) {

        // calculate sum of array
        sum += arr[i];

        // calculate maximum element in the array
        M = max(M, arr[i]);
    }

    // calculating sum of permutation
    int sum1 = M * (M + 1) / 2;

    // calculate required answer
    int ans = (sum - sum1) / (N - M);
    return ans;
}
// Driver code
int main()
{
    // Input
    int arr[] = { 2, 6, 4, 3, 1, 5, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << repeatingElement(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG
{

  // Function to calculate the repeating character in a given
  // permutation
  public static int repeatingElement(int arr[], int N)
  {

    // variables to store maximum element and sum of the
    // array respectively.
    int M = 0, sum = 0;
    for (int i = 0; i < N; i++) {

      // calculate sum of array
      sum += arr[i];

      // calculate maximum element in the array
      M = Math.max(M, arr[i]);
    }

    // calculating sum of permutation
    int sum1 = M * (M + 1) / 2;

    // calculate required answer
    int ans = (sum - sum1) / (N - M);
    return ans;
  }

  // Driver code
  public static void main (String[] args)
  {

    // Input
    int arr[] = { 2, 6, 4, 3, 1, 5, 2 };
    int N = arr.length;

    // Function call
    System.out.println(repeatingElement(arr, N));
  }
}

// This code is contributed by lokeshpotta20
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate the repeating character in a given
# permutation
def repeatingElement(arr, N):

    # variables to store maximum element and sum of the
    # array respectively.
    M = 0
    sum = 0
    for i in range(N):

        # calculate sum of array
        sum += arr[i]

        # calculate maximum element in the array
        M = max(M, arr[i])

    # calculating sum of permutation
    sum1 = M * (M + 1) // 2

    # calculate required answer
    ans = (sum - sum1) // (N - M)
    return ans

# Driver code
if __name__ == '__main__':

    # Input
    arr = [2, 6, 4, 3, 1, 5, 2]
    N = len(arr)

    # Function call
    print(repeatingElement(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C++ program for the above approach
using System;

// Function to calculate the repeating character in a given
// permutation
public class GFG
{
    public static int repeatingElement(int[] arr, int N)
    {

        // variables to store maximum element and sum of the
        // array respectively.
        int M = 0, sum = 0;
        for (int i = 0; i < N; i++) {

            // calculate sum of array
            sum += arr[i];

            // calculate maximum element in the array
            M = Math.Max(M, arr[i]);
        }

        // calculating sum of permutation
        int sum1 = M * (M + 1) / 2;

        // calculate required answer
        int ans = (sum - sum1) / (N - M);
        return ans;
    }

    // Driver code
    public static void Main()
    {
        // Input
        int[] arr = { 2, 6, 4, 3, 1, 5, 2 };
        int N = 7;

        // Function call
        Console.WriteLine(repeatingElement(arr, N));
    }
}

// This code is contributed by Sohom Das
```

## java 描述语言

```
// JavaScript program for the above approach

        // Function to calculate the repeating character in a given
        // permutation
        function repeatingElement(arr, N)
        {

            // variables to store maximum element and sum of the
            // array respectively.
            let M = 0, sum = 0;
            for (let i = 0; i < N; i++) {

                // calculate sum of array
                sum += arr[i];

                // calculate maximum element in the array
                M = Math.max(M, arr[i]);
            }

            // calculating sum of permutation
            let sum1 = parseInt(M * (M + 1) / 2);

            // calculate required answer
            let ans = parseInt((sum - sum1) / (N - M));
            return ans;
        }
        // Driver code

        // Input
        let arr = [2, 6, 4, 3, 1, 5, 2];
        let N = arr.length;

        // Function call
        document.write(repeatingElement(arr, N));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)