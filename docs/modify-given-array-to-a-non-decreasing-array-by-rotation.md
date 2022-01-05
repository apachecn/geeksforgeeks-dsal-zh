# 通过旋转

将给定数组修改为非递减数组

> 原文:[https://www . geesforgeks . org/modify-given-array-to-a-non-reduced-array-by-rotation/](https://www.geeksforgeeks.org/modify-given-array-to-a-non-decreasing-array-by-rotation/)

给定一个大小为***(由副本组成)的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，*任务是检查给定数组是否可以通过旋转将其转换为非递减数组。如果无法做到，则打印“**否**”。否则，打印“**是**”。**

****示例:****

> ****输入:** arr[] = {3，4，5，1，2}
> **输出:**是
> **解释:**向右旋转 2 圈后，数组 arr[]修改为{1，2，3，4，5}**
> 
> ****输入:** arr[] = {1，2，4，3}
> **输出:**否**

****方法:**这个想法是基于这样一个事实，即通过旋转给定的阵列，并检查每个单独的旋转阵列，无论其是否为非递减的，可以获得最大数量的 **N** 个不同的阵列。按照以下步骤解决问题:**

*   **初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，说 **v，**，把原数组的所有元素都复制进去。**
*   **[排序向量 **v**](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) 。**
*   **[遍历原始数组](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)并执行以下步骤:

    *   每次迭代旋转 1。
    *   如果数组等于向量 **v** ，则打印“**是**”。否则，打印“ **No** ”。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// non-decreasing array can be obtained
// by rotating the original array
void rotateArray(vector<int>& arr, int N)
{
    // Stores copy of original array
    vector<int> v = arr;

    // Sort the given vector
    sort(v.begin(), v.end());

    // Traverse the array
    for (int i = 1; i <= N; ++i) {

        // Rotate the array by 1
        rotate(arr.begin(),
               arr.begin() + 1, arr.end());

        // If array is sorted
        if (arr == v) {

            cout << "YES" << endl;
            return;
        }
    }

    // If it is not possible to
    // sort the array
    cout << "NO" << endl;
}

// Driver Code
int main()
{
    // Given array
    vector<int> arr = { 3, 4, 5, 1, 2 };

    // Size of the array
    int N = arr.size();

    // Function call to check if it is possible
    // to make array non-decreasing by rotating
    rotateArray(arr, N);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

  // Function to check if a
  // non-decreasing array can be obtained
  // by rotating the original array
  static void rotateArray(int[] arr, int N)
  {
    // Stores copy of original array
    int[] v = arr;

    // Sort the given vector
    Arrays.sort(v);

    // Traverse the array
    for (int i = 1; i <= N; ++i) {

      // Rotate the array by 1
      int x = arr[N - 1];
      i = N - 1;
      while(i > 0){
        arr[i] = arr[i - 1];
        arr[0] = x;
        i -= 1;
      }

      // If array is sorted
      if (arr == v) {

        System.out.print("YES");
        return;
      }
    }

    // If it is not possible to
    // sort the array
    System.out.print("NO");
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int[] arr = { 3, 4, 5, 1, 2 };

    // Size of the array
    int N = arr.length;

    // Function call to check if it is possible
    // to make array non-decreasing by rotating
    rotateArray(arr, N);
  }
}

// This code is contributed by splevel62.
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to check if a
# non-decreasing array can be obtained
# by rotating the original array
def rotateArray(arr, N):

    # Stores copy of original array
    v = arr

    # Sort the given vector
    v.sort(reverse = False)

    # Traverse the array
    for i in range(1, N + 1, 1):

        # Rotate the array by 1
        x = arr[N - 1]
        i = N - 1
        while(i > 0):
            arr[i] = arr[i - 1]
            arr[0] = x
            i -= 1

        # If array is sorted
        if (arr == v):
            print("YES")
            return

    # If it is not possible to
    # sort the array
    print("NO")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr =  [3, 4, 5, 1, 2]

    # Size of the array
    N = len(arr)

    # Function call to check if it is possible
    # to make array non-decreasing by rotating
    rotateArray(arr, N)

    # This code is contributed by ipg2016107.
```

## **C#**

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to check if a
  // non-decreasing array can be obtained
  // by rotating the original array
  static void rotateArray(int[] arr, int N)
  {

    // Stores copy of original array
    int[] v = arr;

    // Sort the given vector
    Array.Sort(v);

    // Traverse the array
    for (int i = 1; i <= N; ++i) {

      // Rotate the array by 1
      int x = arr[N - 1];
      i = N - 1;
      while(i > 0){
        arr[i] = arr[i - 1];
        arr[0] = x;
        i -= 1;
      }

      // If array is sorted
      if (arr == v) {

        Console.Write("YES");
        return;
      }
    }

    // If it is not possible to
    // sort the array
    Console.Write("NO");
  }

// Driver code
public static void Main()
{
    // Given array
    int[] arr = { 3, 4, 5, 1, 2 };

    // Size of the array
    int N = arr.Length;

    // Function call to check if it is possible
    // to make array non-decreasing by rotating
    rotateArray(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if a
// non-decreasing array can be obtained
// by rotating the original array
function rotateArray(arr, N) {

    // Stores copy of original array
    let v = arr;

    // Sort the given vector
    v.sort((a, b) => a - b);

    // Traverse the array
    for (let i = 1; i <= N; ++i) {

        // Rotate the array by 1
        let x = arr[N - 1];
        i = N - 1;
        while (i--) {
            arr[i] = arr[i - 1];
            arr[0] = x;
        }

        // If array is sorted

        let isEqual = arr.every((e, i) => {
            return arr[i] == v[i]
        })

        if (isEqual) {
            document.write("YES");
            return;
        }
    }

    // If it is not possible to
    // sort the array
    document.write("NO");
}

// Driver code

// Given array
let arr = [3, 4, 5, 1, 2];

// Size of the array
let N = arr.length;

// Function call to check if it is possible
// to make array non-decreasing by rotating
rotateArray(arr, N);

// This code is contributed by _saurabh_jaiswal

</script>
```

****Output**

```
YES
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)***