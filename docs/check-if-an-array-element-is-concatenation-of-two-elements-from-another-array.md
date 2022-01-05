# 检查一个数组元素是否是另一个数组的两个元素的连接

> 原文:[https://www . geesforgeks . org/check-if-a-array-element-is-concation-of-elements-from-other-array/](https://www.geeksforgeeks.org/check-if-an-array-element-is-concatenation-of-two-elements-from-another-array/)

给定两个分别由 **N** 和 **M** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和**brr【】**，任务是找到数组**brr【】**中的所有元素，这些元素等于数组**arr【】**中任意两个元素的串联。如果不存在这样的元素，则打印**-1”**。

**示例:**

> **输入:** arr[] = {2，34，4，5}，brr[] = {26，24，345，4，22}
> **输出:** 24 345 22
> **解释:**
> 数组 brr[]中的元素是数组 arr[]中任意两个元素的串联:
> 
> 1.  24 是 2 和 4 的串联。
> 2.  345 是 34 和 5 的串联。
> 3.  22 是 2 和 2 的串联。
> 
> **输入:** arr[] = {1，2，3}，brr[] = {1，23}
> **输出:** 23

**天真方法:**解决问题最简单的方法是[从给定的数组中生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)和[检查数组 arr[]中的元素对的连接是否存在于数组中](https://www.geeksforgeeks.org/check-if-a-value-is-present-in-an-array-in-java/) **brr[]** 。如果发现是真的，则打印形成的串联数字。

***时间复杂度:**O(M * N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**上述方法可以通过检查数组中的每个元素 **brr[]** 、 **brr[i]** 是否可以分为 2 个部分**左**和**右**，使得这两个部分都存在于数组中 **arr[]** 。

> 考虑一个数字，b[i] = 2365
> 左右所有可能的组合为:
> 左右
> 2 365
> 23 65
> 236 5

按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** 并存储数组**arr【】**中存在的所有元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **brr[]** 并执行以下步骤:
    *   生成**左侧**和**右侧**零件的所有可能组合，以便它们的连接结果为**brr【I】**。
    *   如果在上述组合之一中的[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中同时存在**左侧**和**右侧**零件，则打印 **brr[i]** 的值。否则，[继续下一次迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find elements present in
// the array b[] which are concatenation
// of any pair of elements in the array a[]
void findConcatenatedNumbers(vector<int> a,
                             vector<int> b)
{
    // Stores if there doesn't any such
    // element in the array brr[]
    bool ans = true;

    // Stored the size of both the arrays
    int n1 = a.size();
    int n2 = b.size();

    // Store the presence of an element
    // of array a[]
    unordered_map<int, int> cnt;

    // Traverse the array a[]
    for (int i = 0; i < n1; i++) {
        cnt[a[i]] = 1;
    }

    // Traverse the array b[]
    for (int i = 0; i < n2; i++) {

        int left = b[i];
        int right = 0;
        int mul = 1;

        // Traverse over all possible
        // concatenations of b[i]
        while (left > 9) {

            // Update right and left parts
            right += (left % 10) * mul;
            left /= 10;
            mul *= 10;

            // Check if both left and right
            // parts are present in a[]
            if (cnt[left] == 1
                && cnt[right] == 1) {
                ans = false;
                cout << b[i] << " ";
            }
        }
    }

    if (ans)
        cout << "-1";
}

// Driver Code
int main()
{
    vector<int> a = { 2, 34, 4, 5 };
    vector<int> b = { 26, 24, 345, 4, 22 };
    findConcatenatedNumbers(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to find elements present in
  // the array b[] which are concatenation
  // of any pair of elements in the array a[]
  static void findConcatenatedNumbers(int[] a,
                                      int[] b)
  {
    // Stores if there doesn't any such
    // element in the array brr[]
    boolean ans = true;

    // Stored the size of both the arrays
    int n1 = a.length;
    int n2 = b.length;

    // Store the presence of an element
    // of array a[]
    int cnt[] = new int[100000];

    // Traverse the array
    for (int i = 0; i < n1; i++)
    {
      cnt[a[i]] = 1;
    }

    // Traverse the array b[]
    for (int i = 0; i < n2; i++) {

      int left = b[i];
      int right = 0;
      int mul = 1;

      // Traverse over all possible
      // concatenations of b[i]
      while (left > 9) {

        // Update right and left parts
        right += (left % 10) * mul;
        left /= 10;
        mul *= 10;

        // Check if both left and right
        // parts are present in a[]
        if (cnt[left] == 1
            && cnt[right] == 1) {
          ans = false;
          System.out.print(b[i] + " ");
        }
      }
    }

    if (ans)
      System.out.print("-1");
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] a = { 2, 34, 4, 5 };
    int[] b = { 26, 24, 345, 4, 22 };
    findConcatenatedNumbers(a, b);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find elements present in
# the array b[] which are concatenation
# of any pair of elements in the array a[]
def findConcatenatedNumbers(a, b):

    # Stores if there doesn't any such
    # element in the array brr[]
    ans = True

    # Stored the size of both the arrays
    n1 = len(a)
    n2 = len(b)

    # Store the presence of an element
    # of array a[]
    cnt = defaultdict(int)

    # Traverse the array a[]
    for i in range(n1):
        cnt[a[i]] = 1

    # Traverse the array b[]
    for i in range(n2):
        left = b[i]
        right = 0
        mul = 1

        # Traverse over all possible
        # concatenations of b[i]
        while (left > 9):

            # Update right and left parts
            right += (left % 10) * mul
            left //= 10
            mul *= 10

            # Check if both left and right
            # parts are present in a[]
            if (cnt[left] == 1 and cnt[right] == 1):
                ans = False
                print(b[i], end = " ")

    if (ans):
        print("-1")

# Driver Code
if __name__ == "__main__":

    a = [ 2, 34, 4, 5 ]
    b = [ 26, 24, 345, 4, 22 ]

    findConcatenatedNumbers(a, b)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find elements present in
  // the array b[] which are concatenation
  // of any pair of elements in the array a[]
  static void findConcatenatedNumbers(int[] a,
                                      int[] b)
  {

    // Stores if there doesn't any such
    // element in the array brr[]
    bool ans = true;

    // Stored the size of both the arrays
    int n1 = a.Length;
    int n2 = b.Length;

    // Store the presence of an element
    // of array a[]
    int []cnt = new int[100000];

    // Traverse the array
    for (int i = 0; i < n1; i++)
    {
      cnt[a[i]] = 1;
    }

    // Traverse the array b[]
    for (int i = 0; i < n2; i++) {

      int left = b[i];
      int right = 0;
      int mul = 1;

      // Traverse over all possible
      // concatenations of b[i]
      while (left > 9) {

        // Update right and left parts
        right += (left % 10) * mul;
        left /= 10;
        mul *= 10;

        // Check if both left and right
        // parts are present in a[]
        if (cnt[left] == 1
            && cnt[right] == 1) {
          ans = false;
          Console.Write(b[i] + " ");
        }
      }
    }

    if (ans)
      Console.Write("-1");
  }

  // Driver code
  public static void Main(String[] args)
  {
    int[] a = { 2, 34, 4, 5 };
    int[] b = { 26, 24, 345, 4, 22 };
    findConcatenatedNumbers(a, b);
  }
}

// This code is contributed by shivani
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find elements present in
// the array b[] which are concatenation
// of any pair of elements in the array a[]
function findConcatenatedNumbers(a, b)
{
    // Stores if there doesn't any such
    // element in the array brr[]
    var ans = true;

    // Stored the size of both the arrays
    var n1 = a.length;
    var n2 = b.length;

    // Store the presence of an element
    // of array a[]
    var cnt = new Map();

    // Traverse the array a[]
    for (var i = 0; i < n1; i++) {
        cnt.set(a[i], 1);
    }

    // Traverse the array b[]
    for (var i = 0; i < n2; i++) {

        var left = b[i];
        var right = 0;
        var mul = 1;

        // Traverse over all possible
        // concatenations of b[i]
        while (left > 9) {

            // Update right and left parts
            right += (left % 10) * mul;
            left = parseInt(left/10);
            mul *= 10;

            // Check if both left and right
            // parts are present in a[]
            if (cnt.has(left)
                && cnt.has(right)) {
                ans = false;
                document.write( b[i] + " ");
            }
        }
    }

    if (ans)
        document.write( "-1");
}

// Driver Code
var a = [2, 34, 4, 5 ];
var b = [26, 24, 345, 4, 22 ];
findConcatenatedNumbers(a, b);

</script>
```

**Output:** 

```
24 345 22
```

***时间复杂度:** O(M*log(X))，其中 **X** 是数组中* [*最大的元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *brr[]。*
***辅助空间:** O(N)*