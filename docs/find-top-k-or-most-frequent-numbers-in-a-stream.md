# 查找一个流中的前 k 个(或最频繁的)数字

> 原文:[https://www . geeksforgeeks . org/find-top-k-or-最常出现的流中数字/](https://www.geeksforgeeks.org/find-top-k-or-most-frequent-numbers-in-a-stream/)

给定一组 n 个数字。您的任务是从数组中读取数字，并在每次读取新数字时将最多 K 个数字保持在顶部(根据它们的递减频率)。当输入流包含 k 个不同元素时，我们基本上需要打印按频率排序的前 k 个数字，否则需要打印所有按频率排序的不同元素。
**例:**

> **输入:** arr[] = {5，2，1，3，2}
> k = 4
> **输出:**5 2 5 1 2 5 1 2 3 5 1 3 5
> **解释:**
> 
> 1.  读完 5，只有一个元素 5 的频率到现在为止是最大的。
>     所以打印 5。
> 2.  读完 2，我们会有两个频率相同的元素 2 和 5。
>     As 2，小于 5 但是它们的频率是一样的，所以我们会打印 2 5。
> 3.  读完 1，我们会有 3 个频率相同的元素 1、2、5，
>     所以打印 1 2 5。
> 4.  同样，阅读 3 后，打印 1 2 3 5
> 5.  读取最后一个元素 2 后，因为 2 已经出现，所以我们现在将
>     频率 2 设为 2。所以我们在顶部保留 2，然后在排序顺序中以相同的频率保留元素
>     的其余部分。所以打印，2 1 3 5。
> 
> **输入:** arr[] = {5，2，1，3，4}
> k = 4
> **输出:** 5 2 5 1 2 5 1 2 3 5 1 2 3 4
> **解释:**
> 
> 1.  读完 5，只有一个元素 5 的频率到现在为止是最大的。
>     所以打印 5。
> 2.  读完 2，我们会有两个频率相同的元素 2 和 5。
>     As 2，小于 5 但是它们的频率是一样的，所以我们会打印 2 5。
> 3.  读完 1，我们会有 3 个频率相同的元素 1、2、5，
>     所以打印 1 2 5。
>     同样读完 3，打印 1 2 3 5
> 4.  读取最后一个元素 4 后，所有元素频率相同
>     所以打印，1 2 3 4。

**<u>进场:</u>** 思路是以最大频率存储前 k 个元素。为了存储它们，可以使用向量或数组。为了跟踪元素的频率，创建了一个 HashMap 来存储元素频率对。给定一个数字流，当一个新元素出现在流中时，更新 HashMap 中该元素的频率，并将该元素放在 K 个数字列表的末尾(总共 k+1 个元素)，现在比较列表的相邻元素，如果频率较高的元素存储在它旁边，则进行交换。
**算法:**

1.  创建一个散列表 *hm* ，以及一个长度为 *k + 1* 的数组。
2.  从头到尾遍历输入数组。
3.  在数组的第 k+1 个位置插入元素，更新该元素在 HashMap 中的出现频率。
4.  现在，从头到尾遍历 temp 数组–1
5.  对于每个元素，比较频率，如果频率较高的元素存储在它旁边，则交换，如果频率相同，则交换是下一个较大的元素。
6.  打印原始数组每次遍历的前 k 个元素。

**执行:**

## C++

```
// C++ program to find top k elements in a stream
#include <bits/stdc++.h>
using namespace std;

// Function to print top k numbers
void kTop(int a[], int n, int k)
{
    // vector of size k+1 to store elements
    vector<int> top(k + 1);

    // array to keep track of frequency
    unordered_map<int, int> freq;

    // iterate till the end of stream
    for (int m = 0; m < n; m++) {
        // increase the frequency
        freq[a[m]]++;

        // store that element in top vector
        top[k] = a[m];

        // search in top vector for same element
        auto it = find(top.begin(), top.end() - 1, a[m]);

        // iterate from the position of element to zero
        for (int i = distance(top.begin(), it) - 1; i >= 0; --i) {
            // compare the frequency and swap if higher
            // frequency element is stored next to it
            if (freq[top[i]] < freq[top[i + 1]])
                swap(top[i], top[i + 1]);

            // if frequency is same compare the elements
            // and swap if next element is high
            else if ((freq[top[i]] == freq[top[i + 1]])
                     && (top[i] > top[i + 1]))
                swap(top[i], top[i + 1]);
            else
                break;
        }

        // print top k elements
        for (int i = 0; i < k && top[i] != 0; ++i)
            cout << top[i] << ' ';
    }
    cout << endl;
}

// Driver program to test above function
int main()
{
    int k = 4;
    int arr[] = { 5, 2, 1, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    kTop(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
class GFG {

    // function to search in top vector for element
    static int find(int[] arr, int ele)
    {
        for (int i = 0; i < arr.length; i++)
            if (arr[i] == ele)
                return i;
        return -1;
    }

    // Function to print top k numbers
    static void kTop(int[] a, int n, int k)
    {
        // vector of size k+1 to store elements
        int[] top = new int[k + 1];

        // array to keep track of frequency
        HashMap<Integer, Integer> freq = new HashMap<>();
        for (int i = 0; i < k + 1; i++)
            freq.put(i, 0);

        // iterate till the end of stream
        for (int m = 0; m < n; m++) {
            // increase the frequency
            if (freq.containsKey(a[m]))
                freq.put(a[m], freq.get(a[m]) + 1);
            else
                freq.put(a[m], 1);

            // store that element in top vector
            top[k] = a[m];

            // search in top vector for same element
            int i = find(top, a[m]);
            i -= 1;

            // iterate from the position of element to zero
            while (i >= 0) {
                // compare the frequency and swap if higher
                // frequency element is stored next to it
                if (freq.get(top[i]) < freq.get(top[i + 1])) {
                    int temp = top[i];
                    top[i] = top[i + 1];
                    top[i + 1] = temp;
                }

                // if frequency is same compare the elements
                // and swap if next element is high
                else if ((freq.get(top[i]) == freq.get(top[i + 1])) && (top[i] > top[i + 1])) {
                    int temp = top[i];
                    top[i] = top[i + 1];
                    top[i + 1] = temp;
                }

                else
                    break;
                i -= 1;
            }

            // print top k elements
            for (int j = 0; j < k && top[j] != 0; ++j)
                System.out.print(top[j] + " ");
        }
        System.out.println();
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        int k = 4;
        int[] arr = { 5, 2, 1, 3, 2 };
        int n = arr.length;
        kTop(arr, n, k);
    }
}

// This code is contributed by rachana soma
```

## 计算机编程语言

```
# Python program to find top k elements in a stream

# Function to print top k numbers
def kTop(a, n, k):

    # list of size k + 1 to store elements
    top = [0 for i in range(k + 1)]

    # dictionary to keep track of frequency
    freq = {i:0 for i in range(k + 1)}

    # iterate till the end of stream
    for m in range(n):

        # increase the frequency
        if a[m] in freq.keys():
            freq[a[m]] += 1
        else:
            freq[a[m]] = 1

        # store that element in top vector
        top[k] = a[m]

        i = top.index(a[m])
        i -= 1

        while i >= 0:

            # compare the frequency and swap if higher
            # frequency element is stored next to it
            if (freq[top[i]] < freq[top[i + 1]]):
                t = top[i]
                top[i] = top[i + 1]
                top[i + 1] = t

            # if frequency is same compare the elements
            # and swap if next element is high
            elif ((freq[top[i]] == freq[top[i + 1]]) and (top[i] > top[i + 1])):
                t = top[i]
                top[i] = top[i + 1]
                top[i + 1] = t
            else:
                break
            i -= 1

        # print top k elements
        i = 0
        while i < k and top[i] != 0:
            print top[i],
            i += 1
    print

# Driver program to test above function
k = 4
arr = [ 5, 2, 1, 3, 2 ]
n = len(arr)
kTop(arr, n, k)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find top k elements in a stream
using System;
using System.Collections.Generic;

class GFG {
    // function to search in top vector for element
    static int find(int[] arr, int ele)
    {
        for (int i = 0; i < arr.Length; i++)
            if (arr[i] == ele)
                return i;
        return -1;
    }

    // Function to print top k numbers
    static void kTop(int[] a, int n, int k)
    {
        // vector of size k+1 to store elements
        int[] top = new int[k + 1];

        // array to keep track of frequency
        Dictionary<int,
                   int>
            freq = new Dictionary<int,
                                  int>();
        for (int i = 0; i < k + 1; i++)
            freq.Add(i, 0);

        // iterate till the end of stream
        for (int m = 0; m < n; m++) {
            // increase the frequency
            if (freq.ContainsKey(a[m]))
                freq[a[m]]++;
            else
                freq.Add(a[m], 1);

            // store that element in top vector
            top[k] = a[m];

            // search in top vector for same element
            int i = find(top, a[m]);
            i--;

            // iterate from the position of element to zero
            while (i >= 0) {
                // compare the frequency and swap if higher
                // frequency element is stored next to it
                if (freq[top[i]] < freq[top[i + 1]]) {
                    int temp = top[i];
                    top[i] = top[i + 1];
                    top[i + 1] = temp;
                }

                // if frequency is same compare the elements
                // and swap if next element is high
                else if (freq[top[i]] == freq[top[i + 1]] && top[i] > top[i + 1]) {
                    int temp = top[i];
                    top[i] = top[i + 1];
                    top[i + 1] = temp;
                }
                else
                    break;

                i--;
            }

            // print top k elements
            for (int j = 0; j < k && top[j] != 0; ++j)
                Console.Write(top[j] + " ");
        }
        Console.WriteLine();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int k = 4;
        int[] arr = { 5, 2, 1, 3, 2 };
        int n = arr.Length;
        kTop(arr, n, k);
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

      // JavaScript program to find top k elements in a stream
      // function to search in top vector for element
      function find(arr, ele) {
        for (var i = 0; i < arr.length; i++)
        if (arr[i] === ele) return i;
        return -1;
      }

      // Function to print top k numbers
      function kTop(a, n, k) {
        // vector of size k+1 to store elements
        var top = new Array(k + 1).fill(0);

        // array to keep track of frequency

        var freq = {};
        for (var i = 0; i < k + 1; i++) freq[i] = 0;

        // iterate till the end of stream
        for (var m = 0; m < n; m++) {
          // increase the frequency
          if (freq.hasOwnProperty(a[m])) freq[a[m]]++;
          else freq[a[m]] = 1;

          // store that element in top vector
          top[k] = a[m];

          // search in top vector for same element
          var i = find(top, a[m]);
          i--;

          // iterate from the position of element to zero
          while (i >= 0) {
            // compare the frequency and swap if higher
            // frequency element is stored next to it
            if (freq[top[i]] < freq[top[i + 1]]) {
              var temp = top[i];
              top[i] = top[i + 1];
              top[i + 1] = temp;
            }

            // if frequency is same compare the elements
            // and swap if next element is high
            else if (freq[top[i]] === freq[top[i + 1]] &&
            top[i] > top[i + 1])
            {
              var temp = top[i];
              top[i] = top[i + 1];
              top[i + 1] = temp;
            } else break;

            i--;
          }

          // print top k elements
          for (var j = 0; j < k && top[j] !== 0; ++j)
            document.write(top[j] + " ");
        }
        document.write("<br>");
      }

      // Driver Code
      var k = 4;
      var arr = [5, 2, 1, 3, 2];
      var n = arr.length;
      kTop(arr, n, k);

</script>
```

**Output:** 

```
5 2 5 1 2 5 1 2 3 5 2 1 3 5
```

**复杂度分析:**

*   **时间复杂度:** O( n * k)。
    在每次遍历中，遍历大小为 k 的临时数组，因此时间复杂度为 O( n * k)。
*   **空间复杂度:** O(n)。
    需要在 HashMap O(n)空间中存储元素。

本文由**尼泰什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。