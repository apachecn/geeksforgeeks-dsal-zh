# 2D 阵列(矩阵)的搜索算法

> 原文:[https://www . geeksforgeeks . org/search-algorithms-for-a-2d-arrays-matrix/](https://www.geeksforgeeks.org/searching-algorithms-for-a-2d-arrays-matrix/)

**<u>线性搜索 2D 阵</u>**

[线性搜索](https://www.geeksforgeeks.org/linear-search/)是一种简单的顺序搜索算法。它用于通过遍历数组中的每个元素来查找数组中是否存在特定元素。虽然在 2D 数组中搜索完全相同，但这里所有的单元都需要遍历，这样，任何元素都在 2D 数组中搜索。

下面是 2D 阵列中线性搜索的实现

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;
vector<int> linearSearch(vector<vector<int>> arr, int target)
{
  for (int i = 0; i < arr.size(); i++) {
    for (int j = 0; j < arr[i].size(); j++) {
      if (arr[i][j] == target) {
        return {i, j};
      }
    }
  }
  return {-1, -1};
}

// Driver code
int main()
{

  vector<vector<int>> arr = { { 3, 12, 9 },
                             { 5, 2, 89 },
                             { 90, 45, 22 } };
  int target = 89;
  vector<int> ans = linearSearch(arr, target);
  cout << "Element found at index: [" << ans[0] << " " <<ans[1] <<"]";

  return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Linear Search in 2D arrays
import java.util.Arrays;

public class GFG {
    public static void main(String[] args)
    {
        int arr[][] = { { 3, 12, 9 },
                        { 5, 2, 89 },
                        { 90, 45, 22 } };
        int target = 89;
        int ans[] = linearSearch(arr, target);
        System.out.println("Element found at index: "
                           + Arrays.toString(ans));
    }

    static int[] linearSearch(int[][] arr, int target)
    {
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                if (arr[i][j] == target) {
                    return new int[] { i, j };
                }
            }
        }
        return new int[] { -1, -1 };
    }
}
```

## 蟒蛇 3

```
# Python code for the above approach
def linearSearch (arr, target):
    for i in range(len(arr)):
        for j in range(len(arr[i])):
            if (arr[i][j] == target):
                return [i, j]
    return [-1, -1]

# Driver code
arr = [[3, 12, 9], [5, 2, 89], [90, 45, 22]]
target = 89
ans = linearSearch(arr, target)
print(f"Element found at index: [{ans[0]} {ans[1]}]")

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// Linear Search in 2D arrays
using System;

public class GFG {
    public static void Main(string[] args)
    {
        int[, ] arr = { { 3, 12, 9 },
                        { 5, 2, 89 },
                        { 90, 45, 22 } };
        int target = 89;
        int[] ans = linearSearch(arr, target);
        Console.WriteLine("Element found at index: ["
                          + ans[0] + "," + ans[1]+"]");
    }

    static int[] linearSearch(int[, ] arr, int target)
    {
        for (int i = 0; i < arr.GetLength(0); i++) {
            for (int j = 0; j < arr.GetLength(1); j++) {
                if (arr[i, j] == target) {
                    return new int[] { i, j };
                }
            }
        }
        return new int[] { -1, -1 };
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach
    const linearSearch = (arr, target) => {
        for (let i = 0; i < arr.length; i++) {
            for (let j = 0; j < arr[i].length; j++) {
                if (arr[i][j] == target) {
                    return [i, j];
                }
            }
        }
        return [-1, -1];
    }

    // Driver code
    let arr = [[3, 12, 9],
    [5, 2, 89],
    [90, 45, 22]];
    let target = 89;
    let ans = linearSearch(arr, target);
    document.write(`Element found at index: [${ans[0]} ${ans[1]}]`);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
Element found at index: [1, 2]
```

2D 数组中线性搜索的时间复杂度为 0(N * M),其中 **N** 是行数， **M** 是列数。

**<u>二分搜索法中一</u>** **<u>2D 阵</u>**

[二分搜索法](https://www.geeksforgeeks.org/binary-search/)是一种有效的数组搜索方法。二分搜索法研究排序数组。在每次迭代中，搜索空间被分成两半，这就是为什么二分搜索法比线性搜索更有效的原因。

**为什么二分搜索法对于在未排序的数组中搜索没有用？**

在任何算法中的任何地方应用二分搜索法的基本条件是搜索空间应该被排序。要在 2D 数组中执行二分搜索法操作，需要对数组进行排序。这里给出了一个未排序的 2D 数组，所以在未排序的数组中应用二分搜索法是不可能的。要首先应用二分搜索法，2D 数组需要以任何顺序进行排序，其本身需要 **(M*N)log(M*N)** 时间。所以在这里搜索任何元素的总时间复杂度是 **O((M * N) log(M * N)) + O(N + M)** ，这和线性搜索的时间复杂度相比非常差，线性搜索的时间复杂度只是 **O(N*M)** 。因此，线性搜索用于在未排序的数组中搜索，而不是二分搜索法。

以下是二分搜索法在 2D 阵列中的实施

## C++

```
// Binary Search on sorted 2D array
#include <bits/stdc++.h>
using namespace std;

vector<int> findAns(vector<vector<int>> arr, int target)
{
  int r = 0;
  int c = arr[r].size() - 1;
  while (r < arr.size() && c >= 0) {
    if (arr[r] == target) {
      return { r, c };
    }

    // Target lies in further row
    if (arr[r] < target) {
      r++;
    }
    // Target lies in previous column
    else {
      c--;
    }
  }
  return { -1, -1 };
}

// Driver Code
int main()
{

  // Binary search in sorted matrix
  vector<vector<int>> arr = { { 1, 2, 3, 4 },
                             { 5, 6, 7, 8 },
                             { 9, 10, 11, 12 } };

  vector<int> ans = findAns(arr, 12);

  cout << "Element found at index: [";
  for(int i = 0; i < ans.size(); i++){
    if(i == ans.size() - 1)
      cout << ans[i];
    else
      cout << ans[i] << ", ";
  }
  cout << "]";

}

// This code is contributed by Samim Hossain Mondal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Binary Search on sorted 2D array
import java.util.Arrays;

class GFG {

    static int[] findAns(int[][] arr, int target)
    {
        int r = 0;
        int c = arr[r].length - 1;
        while (r < arr.length && c >= 0) {
            if (arr[r] == target) {
                return new int[] { r, c };
            }

            // Target lies in further row
            if (arr[r] < target) {
                r++;
            }
            // Target lies in previous column
            else {
                c--;
            }
        }
        return new int[] { -1, -1 };
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Binary search in sorted matrix
        int arr[][] = { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 9, 10, 11, 12 } };
        int[] ans = findAns(arr, 12);
        System.out.println("Element found at index: "
                           + Arrays.toString(ans));
    }
}
```

## 蟒蛇 3

```
# Binary Search on sorted 2D array
def findAns(arr, target):
    r = 0;
    c = len(arr[r]) - 1;
    while (r < len(arr) and c >= 0):
        if (arr[r] == target):
            return [r, c];

        # Target lies in further row
        if (arr[r] < target):
            r += 1;

        # Target lies in previous column
        else:
            c -=1;

    return [ -1, -1];

# Driver Code
if __name__ == '__main__':
    # Binary search in sorted matrix
    arr = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]];
    ans = findAns(arr, 12);
    print("Element found at index: ", ans);

    # This code contributed by shikhasingrajput
```

## C#

```
// Binary Search on sorted 2D array
using System;
class GFG {

  static int[] findAns(int[, ] arr, int target)
  {
    int r = 0;
    int c = arr.GetLength(1) - 1;
    while (r < arr.GetLength(0) && c >= 0) {
      if (arr[r, c] == target) {
        return new int[] { r, c };
      }

      // Target lies in further row
      if (arr[r, c] < target) {
        r++;
      }

      // Target lies in previous column
      else {
        c--;
      }
    }
    return new int[] { -1, -1 };
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Binary search in sorted matrix
    int[, ] arr = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 } };
    int[] ans = findAns(arr, 12);
    Console.Write("Element found at index: [");
    int i = 0;
    for (i = 0; i < ans.Length - 1; i++)
      Console.Write(ans[i] + " ,");
    Console.Write(ans[i] + "]");
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Binary Search on sorted 2D array
   function findAns(arr , target)
    {
        var r = 0;
        var c = arr[r].length - 1;
        while (r < arr.length && c >= 0) {
            if (arr[r] == target) {
                return [ r, c ];
            }

            // Target lies in further row
            if (arr[r] < target) {
                r++;
            }

            // Target lies in previous column
            else {
                c--;
            }
        }
        return [ -1, -1 ];
    }

    // Driver Code
    // Binary search in sorted matrix
        var arr = [ [ 1, 2, 3, 4 ],
                        [ 5, 6, 7, 8 ],
                        [ 9, 10, 11, 12 ] ];
        var ans = findAns(arr, 12);
        document.write("Element found at index: "
                           + (ans));

// This code is contributed by shikhasingrajput
</script>
```

**Output**

```
Element found at index: [2, 3]
```

在已经排序的 2D 数组中，二分搜索法的时间复杂度为 0(N+M)，其中 **N** 是行数， **M** 是列数。