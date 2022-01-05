# 求两个不相交的子阵，所有元素的和等于 2 的幂

> 原文:[https://www . geeksforgeeks . org/find-两个不相交的子阵列-所有元素的和相等-提升到 2 的幂/](https://www.geeksforgeeks.org/find-two-non-intersecting-subarrays-having-equal-sum-of-all-elements-raised-to-the-power-of-2/)

给定一个大小为 **N** 的正整数[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查 **arr[]** 中是否存在两个不相交的子数组，使得所有可能的 **2 <sup>(子数组【I】)</sup>**之和与所有可能的 **2 <sup>(子数组【j】)</sup>**之和相等。

**示例:**

> **输入:** arr[] = {4，3，0，1，2，0}
> **输出:** YES
> **解释:**用 2 <sup>arr[i]</sup> 的形式表示每个数组元素，数组修改为{ 16，8，1，2，4，1 }。
> 因此，两个有效的子阵是{ 16 }和{ 8，1，2，4，1 }，它们的和相等。
> 
> **输入:** arr[]={ 3，4 }
> T3】输出:否

**方法:**由于 2 的所有[次幂的二进制表示是唯一的，因此只有在该数组](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) y 中存在任何重复元素时，才能获得两个这样的子数组[，否则是不可能的。](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/?ref=rp)

按照以下步骤解决问题:

*   [给定数组按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查任意一对相邻元素是否相等。
*   如果发现任何这样的配对，打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if two non-intersecting
// subarrays with equal sum exists or not
void findSubarrays(int arr[], int N)
{
    // Sort the given array
    sort(arr, arr + N);
    int i = 0;

    // Traverse the array
    for (i = 0; i < N - 1; i++) {

        // Check for duplicate elements
        if (arr[i] == arr[i + 1]) {

            cout << "YES" << endl;
            return;
        }
    }

    // If no duplicate element is
    // present in the array
    cout << "NO" << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, 3, 0, 1, 2, 0 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    findSubarrays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if two non-intersecting
// subarrays with equal sum exists or not
static void findSubarrays(int arr[], int N)
{

    // Sort the given array
    Arrays.sort(arr);
    int i = 0;

    // Traverse the array
    for(i = 0; i < N - 1; i++)
    {

        // Check for duplicate elements
        if (arr[i] == arr[i + 1])
        {
            System.out.println("YES");
            return;
        }
    }

    // If no duplicate element is
    // present in the array
    System.out.println("NO");
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int[] arr = { 4, 3, 0, 1, 2, 0 };

    // Size of array
    int N = arr.length;

    findSubarrays(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if two non-intersecting
# subarrays with equal sum exists or not
def findSubarrays(arr, N):

    # Sort the given array
    arr.sort();
    i = 0;

    # Traverse the array
    for i in range(N - 1):

        # Check for duplicate elements
        if (arr[i] == arr[i + 1]):
            print("YES");
            return;

    # If no duplicate element is
    # present in the array
    print("NO");

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [4, 3, 0, 1, 2, 0];

    # Size of array
    N = len(arr);

    findSubarrays(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if two non-intersecting
// subarrays with equal sum exists or not
static void findSubarrays(int[] arr, int N)
{

    // Sort the given array
    Array.Sort(arr);
    int i = 0;

    // Traverse the array
    for(i = 0; i < N - 1; i++)
    {

        // Check for duplicate elements
        if (arr[i] == arr[i + 1])
        {
            Console.WriteLine("YES");
            return;
        }
    }

    // If no duplicate element is
    // present in the array
    Console.WriteLine("NO");
}

// Driver code
public static void Main()
{

    // Given array
    int[] arr = { 4, 3, 0, 1, 2, 0 };

    // Size of array
    int N = arr.Length;

    findSubarrays(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to check if two non-intersecting
    // subarrays with equal sum exists or not
    function findSubarrays(arr , N) {

        // Sort the given array
        arr.sort();
        var i = 0;

        // Traverse the array
        for (i = 0; i < N - 1; i++) {

            // Check for duplicate elements
            if (arr[i] == arr[i + 1]) {
                document.write("YES");
                return;
            }
        }

        // If no duplicate element is
        // present in the array
        document.write("NO");
    }

    // Driver code

        // Given array
        var arr = [ 4, 3, 0, 1, 2, 0 ];

        // Size of array
        var N = arr.length;

        findSubarrays(arr, N);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(NLogN)*
***辅助空间:** O(1)*