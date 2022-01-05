# 检查给定数组是否按螺旋方式排序

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数组是以螺旋方式排序的，则不排序/](https://www.geeksforgeeks.org/check-if-a-given-array-is-sorted-in-spiral-manner-or-not/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是检查该数组是否是螺旋排序的。如果发现属实，则打印**“是”**。否则，打印**“否”**。

**注意:**如果**arr[0]≤arr[N–1]≤arr[1]≤arr[N–2]…**则数组是螺旋排序的

**示例:**

> **输入:** arr[] = { 1，10，14，20，18，12，5 }
> **输出:** YES
> **解释:**T8】arr[0]<arr[6]
> arr[1]<arr[5]
> arr[2]<arr[4]
> 因此，需要的输出为 YES。
> 
> **输入:** arr[] = { 1，2，4，3 }
> **输出:**否

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，比如**arr【I】**，检查**arr【I】**是否小于等于**arr【N–I–1】**和**arr【N–I–1】**是否小于等于**arr【I+1】**。如果发现是假的，则打印**“否”**。否则，如果所有数组元素都满足条件，则打印**“是”**。按照以下步骤解决问题:

*   初始化两个变量，比如说**开始**和**结束**，来存储给定数组的开始和结束索引。
*   当**开始**小于**结束**时，迭代一个[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，检查 **arr【开始】**是否小于或等于 **arr【结束】****arr【结束】**是否小于或等于 **arr【开始+1】**。如果发现是假的，则打印**“否”**。
*   否则，打印**“是”**。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to check if the array is
// spirally sorted or not
bool isSpiralSorted(int arr[], int n)
{

    // Stores start index
    // of the array
    int start = 0;

    // Stores end index
    // of an array
    int end = n - 1;

    while (start < end) {

        // If arr[start]
        // greater than arr[end]
        if (arr[start] > arr[end]) {
            return false;
        }

        // Update start
        start++;

        // If arr[end]
        // greater than arr[start]
        if (arr[end] > arr[start]) {
            return false;
        }

        // Update end
        end--;
    }

    return true;
}

// Driver Code
int main()
{
    int arr[] = { 1, 10, 14, 20, 18, 12, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    if (isSpiralSorted(arr, N))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

  // Function to check if the array is
  // spirally sorted or not
  static boolean isSpiralSorted(int[] arr, int n)
  {

    // Stores start index
    // of the array
    int start = 0;

    // Stores end index
    // of an array
    int end = n - 1;

    while (start < end)
    {

      // If arr[start]
      // greater than arr[end]
      if (arr[start] > arr[end])
      {
        return false;
      }

      // Update start
      start++;

      // If arr[end]
      // greater than arr[start]
      if (arr[end] > arr[start])
      {
        return false;
      }

      // Update end
      end--;
    }       
    return true;
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 1, 10, 14, 20, 18, 12, 5 };  
    int N = arr.length;

    // Function Call
    if (isSpiralSorted(arr, N) != false)
      System.out.print("YES");
    else
      System.out.print("NO");
  }
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if the array is
# spirally sorted or not
def isSpiralSorted(arr, n) :

    # Stores start index
    # of the array
    start = 0;

    # Stores end index
    # of an array
    end = n - 1;
    while (start < end) :

        # If arr[start]
        # greater than arr[end]
        if (arr[start] > arr[end]) :
            return False;

        # Update start
        start += 1;

        # If arr[end]
        # greater than arr[start]
        if (arr[end] > arr[start]) :
            return False;

        # Update end
        end -= 1;
    return True;

# Driver Code
if __name__ ==  "__main__" :
    arr = [ 1, 10, 14, 20, 18, 12, 5 ];
    N = len(arr);

    # Function Call
    if (isSpiralSorted(arr, N)) :
        print("YES");
    else :
        print("NO");

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to check if the array is
    // spirally sorted or not
    static bool isSpiralSorted(int[] arr, int n)
    {

        // Stores start index
        // of the array
        int start = 0;

        // Stores end index
        // of an array
        int end = n - 1;

        while (start < end)
        {

            // If arr[start]
            // greater than arr[end]
            if (arr[start] > arr[end])
            {
                return false;
            }

            // Update start
            start++;

            // If arr[end]
            // greater than arr[start]
            if (arr[end] > arr[start])
            {
                return false;
            }

            // Update end
            end--;
        }

        return true;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 10, 14, 20, 18, 12, 5 };  
    int N = arr.Length;

    // Function Call
    if (isSpiralSorted(arr, N))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
  }
}

// This code is contributed bydivyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to implement
    // the above approach

    // Function to check if the array is
    // spirally sorted or not
    function isSpiralSorted(arr, n)
    {

        // Stores start index
        // of the array
        let start = 0;

        // Stores end index
        // of an array
        let end = n - 1;

        while (start < end)
        {

            // If arr[start]
            // greater than arr[end]
            if (arr[start] > arr[end])
            {
                return false;
            }

            // Update start
            start++;

            // If arr[end]
            // greater than arr[start]
            if (arr[end] > arr[start])
            {
                return false;
            }

            // Update end
            end--;
        }

        return true;
    }

    let arr = [ 1, 10, 14, 20, 18, 12, 5 ]; 
    let N = arr.length;

    // Function Call
    if (isSpiralSorted(arr, N))
        document.write("YES");
    else
        document.write("NO");

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)