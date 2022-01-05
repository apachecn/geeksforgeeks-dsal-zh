# 一种排列，其中每个元素表示其前后的元素数量

> 原文:[https://www . geeksforgeeks . org/a-arrangement-其中每个元素表示它之前或之后的元素数量/](https://www.geeksforgeeks.org/a-permutation-where-each-element-indicates-either-number-of-elements-before-or-after-it/)

给定一组 **n 个**元素。任务是检查给定数组的置换是否存在，使得每个元素指示它之前或之后存在的元素的数量。如果存在，则打印“是”，否则打印“否”。
**例:**

```
Input : arr[] = {1, 3, 3, 2}
Output : Yes
{3, 1, 2, 3} is a permutation in which each element 
indicate number of element present before or after it.
There is one more permutation {3, 2, 1, 3}

Input : arr[] = {4, 1, 2, 3, 0}
Output : Yes
There are two permutations {0, 1, 2, 3, 4} or
{4, 3, 2, 1, 0}
```

想法是使用散列法。注意，对于数组中的每个索引 I，arr[i]可以有值 I 或 n–I。我们遍历给定的数组，找到数组中每个元素出现的频率。现在，对于每个索引 I，检查值 I 和 n-i 的可用性，并相应地降低频率。请注意，值为 I 的项目可以转到索引 I 或 n-i-1。同样，值为 n-i-1 的项目可以转到索引 I 或 n-i-1。
以下是该方法的实现:

## C++

```
// C++ program to check if array permutation
// exists such that each element indicates
// either number of elements before or after
// it.
#include <bits/stdc++.h>
using namespace std;

// Check if array permutation exist such that
// each element indicate either number of
// elements before or after it.
bool check(int arr[], int n)
{
    map<int, int> freq;

    // Finding the frequency of each number.
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    for (int i = 0; i < n; i++)
    {
        // Try to find number of element before
        // the current index.
        if (freq[i])
            freq[i]--;

        // Try to find number of element after
        // the current index.
        else if (freq[n-i-1])
            freq[n-i-1]--;

        // If no such number find, return false.
        else
            return false;
    }

    return true;
}

// Driven Program
int main()
{
    int arr[] = {1, 3, 3, 2};
    int n = sizeof(arr)/sizeof(arr[0]);

    check(arr, n)? (cout << "Yes" << endl) :
                   (cout << "No" << endl);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if array permutation
// exists such that each element indicates
// either number of elements before or after
// it.
import java.io.*;
class GFG
{
    // Check if array permutation exist such that
    // each element indicate either number of
    // elements before or after it.
    public static boolean check(int arr[])
    {
        int n = arr.length;
        int[] freq = new int[n];

        // Finding the frequency of each number.
        for (int i = 0; i < n; i++)
            freq[arr[i]]++;

        for (int i = 0; i < n; i++)
        {
            // Try to find number of element before
            // the current index.
            if (freq[i]!= 0)
                 freq[i]--;

            // Try to find number of element after
            // the current index.
            else if (freq[n-i-1]!= 0)
                    freq[n-i-1]--;

            // If no such number find, return false.
            else
                return false;
        }

    return true;
    }

    //Driver program
    public static void main (String[] args)
    {

        int arr[] = {1, 3, 3, 2};
        boolean bool = check(arr);
        if(bool)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python program to check if array permutation
# exists such that each element indicates
# either number of elements before or after
# it.

# Check if array permutation exist such that
# each element indicate either number of
# elements before or after it.
def check(arr):

    n = len(arr);
    freq = [0] * n;

    # Finding the frequency of each number.
    for i in range(n):
        freq[arr[i]] += 1;

    for i in range(n):

        # Try to find number of element before
        # the current index.
        if (freq[i] != 0):
            freq[i] -= 1;

        # Try to find number of element after
        # the current index.
        elif (freq[n - i - 1] != 0):
                freq[n - i - 1] -= 1;

        # If no such number find, return false.
        else:
            return False;

    return True;

# Driver program
if __name__ == '__main__':

    arr = [1, 3, 3, 2];
    bool = check(arr);
    if(bool):
        print("Yes");
    else:
        print("No");

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to check if array permutation
// exists such that each element indicates
// either number of elements before or after it.
using System;

class GFG
{
    // Check if array permutation exist such that
    // each element indicate either number of
    // elements before or after it.
    public static bool check(int []arr)
    {
        int n = arr.Length;
        int []freq = new int[n];

        // Finding the frequency of each number.
        for (int i = 0; i < n; i++)
            freq[arr[i]]++;

        for (int i = 0; i < n; i++)
        {
            // Try to find number of element
            // before the current index.
            if (freq[i]!= 0)
                freq[i]--;

            // Try to find number of element
            // after the current index.
            else if (freq[n-i-1] != 0)
                    freq[n-i-1]--;

            // If no such number find, return false.
            else
                return false;
        }

    return true;
    }

    //Driver program
    public static void Main ()
    {
        int []arr = {1, 3, 3, 2};
        bool boo = check(arr);
        if(boo)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>
      // JavaScript program to check if array permutation
      // exists such that each element indicates
      // either number of elements before or after it.
      // Check if array permutation exist such that
      // each element indicate either number of
      // elements before or after it.
      function check(arr)
      {
        var n = arr.length;
        var freq = new Array(n).fill(0);

        // Finding the frequency of each number.
        for (var i = 0; i < n; i++) freq[arr[i]]++;

        for (var i = 0; i < n; i++)
        {

          // Try to find number of element
          // before the current index.
          if (freq[i] !== 0) freq[i]--;

          // Try to find number of element
          // after the current index.
          else if (freq[n - i - 1] !== 0) freq[n - i - 1]--;

          // If no such number find, return false.
          else return false;
        }

        return true;
      }

      // Driver program
      var arr = [1, 3, 3, 2];
      var boo = check(arr);
      if (boo) document.write("Yes");
      else document.write("No");

      // This code is contributed by rdtank.
    </script>
```

输出:

```
Yes
```

**时间复杂度:** O(n)。
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。