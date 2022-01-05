# 求所有奇数长度子阵的中值之和

> 原文:[https://www . geeksforgeeks . org/find-全奇数长度子阵的中位数之和/](https://www.geeksforgeeks.org/find-the-sum-of-medians-of-all-odd-length-subarrays/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找出所有**奇数长度子数组**的[中值](https://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes/)之和。

**示例**:

> **输入** : arr[] = {4，2，5，1}
> **输出** : 18
> **解释**:奇数长度的子数组及其中间值为:
> 
> *   **【4】**->中位数为 4
> *   **【4，2，5】**->中位数为 4
> *   **【2】**->中位数为 2
> *   **【2，5，1】**->中位数为 2
> *   **【5】**->中位数为 5
> *   **【1】**->中位数为 1
> 
> 它们的总和= 4 + 4+ 2 + 2 + 5 +1 = 18
> 
> **输入** : arr[] = {1，2}
> **输出** : 3

**使用 STL 预先要求** : [运行整数流的中间值](https://www.geeksforgeeks.org/median-of-stream-of-running-integers-using-stl/)

**天真方法**:生成每个子数组。如果子数组的长度是奇数，那么排序子数组并返回中间元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find sum of medians
// of all odd-length subarrays
int solve(vector<int> arr)
{
    int ans = 0;
    int n = arr.size();

    // Loop to calculate the sum
    for(int i = 0; i < n; i++)
    {
        vector<int> new_arr;
        for(int j = i; j < n; j++)
        {
            new_arr.push_back(arr[j]);

            // Odd length subarray
            if ((new_arr.size() % 2) == 1)
            {
                sort(new_arr.begin(), new_arr.end());
                int mid = new_arr.size() / 2;
                ans += new_arr[mid];
            }
        }
    }
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 2, 5, 1 };
    cout << solve(arr);
}

// This code is contributed by Samim Hossain Mondal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {
    // Function to find sum of medians
    // of all odd-length subarrays
    static int solve(int[] arr) {
        int ans = 0;
        int n = arr.length;

        // Loop to calculate the sum
        for (int i = 0; i < n; i++) {
            List<Integer> new_arr = new LinkedList<Integer>();
            for (int j = i; j < n; j++) {
                new_arr.add(arr[j]);

                // Odd length subarray
                if ((new_arr.size() % 2) == 1) {
                    Collections.sort(new_arr);
                    int mid = new_arr.size() / 2;
                    ans += new_arr.get(mid);
                }
            }
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args) {
        int[] arr = { 4, 2, 5, 1 };
        System.out.println(solve(arr));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find sum of medians
# of all odd-length subarrays
def solve(arr):
        ans = 0
        n = len(arr)

        # Loop to calculate the sum
        for i in range(n):
            new_arr = []
            for j in range(i, n, 1):
                new_arr.append(arr[j])

                # Odd length subarray
                if (len(new_arr)) % 2 == 1:
                    new_arr.sort()
                    mid = len(new_arr)//2
                    ans += new_arr[mid]
        return (ans)

# Driver Code
if __name__ == "__main__":
    arr = [4, 2, 5, 1]
    print(solve(arr))

```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find sum of medians
  // of all odd-length subarrays
  static int solve(int[] arr) {
    int ans = 0;
    int n = arr.Length;

    // Loop to calculate the sum
    for (int i = 0; i < n; i++) {
      List<int> new_arr = new List<int>();
      for (int j = i; j < n; j++) {
        new_arr.Add(arr[j]);

        // Odd length subarray
        if ((new_arr.Count % 2) == 1) {
          new_arr.Sort();
          int mid = new_arr.Count / 2;
          ans += new_arr[mid];
        }
      }
    }
    return ans;
  }

  // Driver Code
  public static void Main() {
    int[] arr = { 4, 2, 5, 1 };
    Console.Write(solve(arr));
  }
}

// This code is contributed by Saurabh Jaiswal
```

**Output**

```
18
```

***时间复杂度*****:**O(N<sup>3</sup>* Log(N)) *****辅助空间*** **:** O(N)**

****注意:**不需要每次排序数组，需要花费( **N*logN)** ，可以应用插入排序。但是，总的来说**时间复杂度**将是 **O(N <sup>3</sup> )。****

****有效方法:**排序数组的中值是将数组中的上半部分和下半部分分开的值。为了找出中间值，我们只需要中间元素，而不是整个排序数组。**运行整数流的中值**的方法可以应用在这里。遵循下面提到的步骤**

1.  **使用最大堆和最小堆来计算运行中值。**
2.  **遍历数组中的每个元素。**
3.  **创建新的子数组时，在堆中添加一个元素，如果大小为奇数，则返回中值，否则返回 0。**
4.  ****Max_heap** 用于存储**下半部分**元素，使得**最大元素**位于顶部， **min_heap** 用于存储**上半部分**元素，使得**最小元素**位于顶部。**
5.  **两堆之间的**差**不应大于 1，**多一个元素**总是放在 **max_heap** 中。**

****<u>注意</u>** :这里 max_heap 是用 min_heap 实现的，只需要否定这些值就可以弹出**最大负元素**。**

**下面是上述方法的实现:**

## **蟒蛇 3**

```
# Python program for the above approach
from heapq import heappush as push, heappop as pop

# Find the sum of medians of odd-length
# subarrays

class find_median():

    # Constructor to declare two heaps
    def __init__(self):

        # Store lower half elments such that
        # maximum element is at top
        self.max_heap = []

        # Store higher half elements such that
        # minimum element is at top
        self.min_heap = []

    def add(self, val):

        # len(max_heap) == 0 or curr_element
        # smaller than max_heap top
        if (len(self.max_heap) == 0 or
            self.max_heap[0] > val):
            push(self.max_heap, -val)

        else:
            push(self.min_heap, val)

        # If size of max_heap + 1 greater
        # than min_heap
        if (len(self.max_heap)+1 >
            len(self.min_heap)):
            val = pop(self.max_heap)
            push(self.min_heap, -val)

        # If size of min_heap
        # greater than max_heap
        if (len(self.min_heap) >
            len(self.max_heap)):
            val = pop(self.min_heap)
            push(self.max_heap, -val)

        # Finally if sum of sizes is odd,
        # return median
        if (len(self.min_heap) +
            len(self.max_heap)) % 2 == 1:
            return (-self.max_heap[0])

        # Else return 0
        else:
            return 0

# Function to calculate the sum
# of all odd length subarrays
def solve(arr):
    ans = 0

    # Size of the array
    n = len(arr)
    for i in range(n):

        # Create an obbject
        # of class find_median
        obj = find_median()
        for j in range(i, n, 1):

            # Add value to the heaps
            # using object
            val = obj.add(arr[j])
            ans += val

    return (ans)

# Driver Code
if __name__ == "__main__":
    arr = [4, 2, 5, 1]
    print(solve(arr))
```

****Output**

```
18
```** 

*****时间复杂度*****:**O(N<sup>2</sup>* Log(N)) *****辅助空间*** **:** O(N)****