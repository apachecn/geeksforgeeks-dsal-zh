# 检查一个数组是否可以排列成左或右定位的数组

> 原文:[https://www . geesforgeks . org/check-if-给定-array-can-in-left-or-right-positioned-array/](https://www.geeksforgeeks.org/check-if-given-array-can-be-arranged-in-left-or-right-positioned-array/)

给定一个大小 n>4 的数组 arr【】，任务是检查给定的数组是否可以**以左定位数组或右定位数组的形式排列**？
**左或右定位数组**表示数组中的每个元素等于其左边的元素数或右边的元素数。
**例:**

```
Input  : arr[] = {1, 3, 3, 2}
Output : "YES"  
This array has one such arrangement {3, 1, 2, 3}. 
In this arrangement, first element '3' indicates 
that three numbers are after it, the 2nd element 
'1' indicates that one number is before it, the 
3rd element '2' indicates that two elements are 
before it.

Input : arr[] = {1, 6, 5, 4, 3, 2, 1}
Output: "NO"
// No such arrangement is possible

Input : arr[] = {2, 0, 1, 3}
Output: "YES"
// Possible arrangement is {0, 1, 2, 3}

Input : arr[] = {2, 1, 5, 2, 1, 5}
Output: "YES"
// Possible arrangement is {5, 1, 2, 2, 1, 5}
```

一个**简单的解决方案**是生成所有可能的排列(参见[这篇](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)文章)，并检查左或右定位数组条件，如果数组中的每个元素都满足条件，那么“是”或“否”。这种方法的时间复杂度是 O(n*n！+ n)，n*n！使用临时数组生成用于检查条件的所有排列和 n。
针对这个问题的一个**高效解决方案**需要一点观察和纸笔工作。为了满足左或右定位数组条件，数组中的所有数字应该等于 index，I 或(n-1-i)和 arr[i] < n。因此，我们创建了一个大小为 n 的访问[]数组，并用 0 初始化它的元素。然后我们遍历数组并遵循给定的步骤:

*   如果 visited[arr[i]] = 0，那么将它设为 1，这将检查数组 arr[0]…arr[i-1]左侧的元素数是否等于 arr[i]的条件。
*   否则，使 visited[n-arr[i]-1] = 1，检查数组 arr[i+1]右侧的元素数量是否等于 arr[i]。
*   现在遍历访问过的[]数组，如果访问过的[]数组的所有元素都变成 1，这意味着排列是可能的“是”或者“否”。

## C++

```
// C++ program to check if an array can be arranged
// to left or right positioned array.
#include<bits/stdc++.h>
using namespace std;

// Function to check Left or Right Positioned
// Array.
// arr[] is array of n elements
// visited[] is boolean array of size n
bool leftRight(int arr[],int n)
{
    // Initially no element is placed at any position
    int visited[n] = {0};

    // Traverse each element of array
    for (int i=0; i<n; i++)
    {
        // Element must be smaller than n.
        if (arr[i] < n)
        {
            // Place "arr[i]" at position "i"
            // or at position n-arr[i]-1
            if (visited[arr[i]] == 0)
                visited[arr[i]] = 1;
            else
                visited[n-arr[i]-1] = 1;
        }
    }

    // All positions must be occupied
    for (int i=0; i<n; i++)
        if (visited[i] == 0)
            return false;

    return true;
}

// Driver program to test the case
int main()
{
    int arr[] = {2, 1, 5, 2, 1, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    if (leftRight(arr, n) == true)
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if an array
// can be arranged to left or
// right positioned array.

class GFG {

    // Function to check Left or
    // Right Positioned Array.
    // arr[] is array of n elements
    // visited[] is boolean array of size n
    static boolean leftRight(int arr[], int n) {

    // Initially no element is
    // placed at any position
    int visited[] = new int[n];

    // Traverse each element of array
    for (int i = 0; i < n; i++) {

    // Element must be smaller than n.
    if (arr[i] < n) {

        // Place "arr[i]" at position "i"
        // or at position n-arr[i]-1
        if (visited[arr[i]] == 0)
        visited[arr[i]] = 1;
        else
        visited[n - arr[i] - 1] = 1;
    }
    }

    // All positions must be occupied
    for (int i = 0; i < n; i++)
    if (visited[i] == 0)
        return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {2, 1, 5, 2, 1, 5};
    int n = arr.length;
    if (leftRight(arr, n) == true)
    System.out.print("YES");
    else
    System.out.print("NO");
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check
# if an array can be arranged
# to left or right positioned array.

# Function to check Left
# or Right Positioned
# Array.
# arr[] is array of n elements
# visited[] is boolean array of size n
def leftRight(arr,n):

    # Initially no element
    # is placed at any position
    visited=[]
    for i in range(n+1):
        visited.append(0)

    # Traverse each element of array
    for i in range(n):

        # Element must be smaller than n.
        if (arr[i] < n):

            # Place "arr[i]" at position "i"
            # or at position n-arr[i]-1
            if (visited[arr[i]] == 0):
                visited[arr[i]] = 1
            else:
                visited[n-arr[i]-1] = 1

    # All positions must be occupied
    for i in range(n):
        if (visited[i] == 0):
            return False

    return True

# Driver code

arr = [2, 1, 5, 2, 1, 5]
n = len(arr)

if (leftRight(arr, n) == True):
    print("YES")
else:
    print("NO")

# This code is contributed
# by Anant Agarwal.
```

## C#

```

// C# program to check if an array
// can be arranged to left or
// right positioned array.
using System;
public class GFG {

        // Function to check Left or
        // Right Positioned Array.
        // arr[] is array of n elements
        // visited[] is boolean array of size n
        static bool leftRight(int []arr, int n) {

        // Initially no element is
        // placed at any position
        int []visited = new int[n];

        // Traverse each element of array
        for (int i = 0; i < n; i++) {

        // Element must be smaller than n.
        if (arr[i] < n) {

            // Place "arr[i]" at position "i"
            // or at position n-arr[i]-1
            if (visited[arr[i]] == 0)
            visited[arr[i]] = 1;
            else
            visited[n - arr[i] - 1] = 1;
        }
        }

        // All positions must be occupied
        for (int i = 0; i < n; i++)
        if (visited[i] == 0)
            return false;

        return true;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, 1, 5, 2, 1, 5};
        int n = arr.Length;
        if (leftRight(arr, n) == true)
        Console.WriteLine("YES");
        else
        Console.WriteLine("NO");
    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if an
// array can be arranged to
// left or right positioned array.

// Function to check Left or
// Right Positioned Array.
// arr[] is array of n elements
// visited[] is boolean array of size n
function leftRight($arr, $n)
{
    // Initially no element is
    // placed at any position
    $visited[$n] = array(0);

    // Traverse each element of array
    for ($i = 0; $i < $n; $i++)
    {
        // Element must be smaller than n.
        if ($arr[$i] < $n)
        {
            // Place "arr[i]" at position "i"
            // or at position n-arr[i]-1
                $visited[$arr[$i]] = 1;
                $visited[$n - $arr[$i] - 1] = 1;
        }
    }

    // All positions must be occupied
    for ($i = 0; $i < $n; $i++)
        if ($visited[$i] == 0)
            return false;

    return true;
}

// Driver Code
$arr = array(2, 1, 5, 2, 1, 5);
$n = sizeof($arr);
if (leftRight($arr, $n) == true)
    echo "YES";
else
    echo "NO";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to check if an array
    // can be arranged to left or
    // right positioned array.

    // Function to check Left or
    // Right Positioned Array.
    // arr[] is array of n elements
    // visited[] is boolean array of size n
    function leftRight(arr, n) {

        // Initially no element is
        // placed at any position
        let visited = new Array(n);

        // Traverse each element of array
        for (let i = 0; i < n; i++) {

          // Element must be smaller than n.
          if (arr[i] < n) {

              // Place "arr[i]" at position "i"
              // or at position n-arr[i]-1
              if (visited[arr[i]] == 0)
                  visited[arr[i]] = 1;
              else
                  visited[n - arr[i] - 1] = 1;
          }
        }

        // All positions must be occupied
        for (let i = 0; i < n; i++)
          if (visited[i] == 0)
              return false;

        return true;
    }

    let arr = [2, 1, 5, 2, 1, 5];
    let n = arr.length;
    if (leftRight(arr, n) == true)
      document.write("YES");
    else
      document.write("NO");

</script>
```

**输出:**

```
"YES"
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由 [**沙莎克·米什拉(古鲁)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。