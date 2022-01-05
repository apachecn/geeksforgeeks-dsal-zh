# 检查给定数组是否为 k 排序数组

> 原文:[https://www . geesforgeks . org/check-是否-给定-数组-k-排序-数组-not/](https://www.geeksforgeeks.org/check-whether-given-array-k-sorted-array-not/)

给定一组不同的元素。检查给定数组是否为 **k** 排序数组。一个 **k** 排序数组是一个数组，其中每个元素在排序数组中距离其目标位置最多 **k** 个距离。
例如，让我们考虑 **k** 是 2，排序数组中索引 7 处的元素，可以在给定数组中的索引 5、6、7、8、9 处。

**示例:**

```
Input : arr[] = {3, 2, 1, 5, 6, 4}, k = 2
Output : Yes
Every element is at most 2 distance away
from its target position in the sorted array.

Input : arr[] = {13, 8, 10, 7, 15, 14, 12}, k = 3
Output : No
13 is more than k = 3 distance away
from its target position in the sorted array. 
```

将原始数组 **arr[]** 的元素复制到辅助数组 **aux[]** 。
排序**辅助[]** 。现在，对于**arr【】**中索引 **i** 处的每个元素，使用二分搜索法查找其在**aux【】**中的索引 **j** 。如果对于任何元素 **k < abs(i-j)** ，则 **arr[]** 不是 **k** 排序数组。否则就是一个 **k** 排序数组。这里 **abs** 是绝对值。

## C++

```
// C++ implementation to check whether the given array
// is a k sorted array or not
#include <bits / stdc++.h>
using namespace std;

// function to find index of element 'x' in sorted 'arr'
// uses binary search technique
int binarySearch(int arr[], int low, int high, int x)
{
    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (arr[mid] == x)
            return mid;
        else if (arr[mid] > x)
            high = mid - 1;
        else   
            low = mid + 1;   
    }
}

// function to check whether the given array is
// a 'k' sorted array or not
string isKSortedArray(int arr[], int n, int k)
{
    // auxiliary array 'aux'
    int aux[n];

    // copy elements of 'arr' to 'aux'
    for (int i = 0; i<n; i++)
        aux[i] = arr[i];

    // sort 'aux'   
    sort(aux, aux + n);

    // for every element of 'arr' at index 'i',
    // find its index 'j' in 'aux'
    for (int i = 0; i<n; i++)
    {
        // index of arr[i] in sorted array 'aux'
        int j = binarySearch(aux, 0, n-1, arr[i]);

        // if abs(i-j) > k, then that element is
        // not at-most k distance away from its
        // target position. Thus,  'arr' is not a
        // k sorted array
        if (abs(i - j) > k)
            return "No";
    }

    // 'arr' is a k sorted array
    return "Yes";   
}

// Driver program to test above
int main()
{
    int arr[] = {3, 2, 1, 5, 6, 4};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << "Is it a k sorted array?: "
         << isKSortedArray(arr, n, k);
    return 0;    
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether the given array
// is a k sorted array or not

import java.util.Arrays;

class Test
{
    // Method to check whether the given array is
    // a 'k' sorted array or not
    static String isKSortedArray(int arr[], int n, int k)
    {
        // auxiliary array 'aux'
        int aux[] = new int[n];

        // copy elements of 'arr' to 'aux'
        for (int i = 0; i<n; i++)
            aux[i] = arr[i];

        // sort 'aux'   
        Arrays.sort(aux);

        // for every element of 'arr' at index 'i',
        // find its index 'j' in 'aux'
        for (int i = 0; i<n; i++)
        {
            // index of arr[i] in sorted array 'aux'
            int j = Arrays.binarySearch(aux,arr[i]);

            // if abs(i-j) > k, then that element is
            // not at-most k distance away from its
            // target position. Thus,  'arr' is not a
            // k sorted array
            if (Math.abs(i - j) > k)
                return "No";
        }

        // 'arr' is a k sorted array
        return "Yes";   
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = {3, 2, 1, 5, 6, 4};
        int k = 2;

        System.out.println("Is it a k sorted array ?: " +
                            isKSortedArray(arr, arr.length, k));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to check
# whether the given array is a k
# sorted array or not

# function to find index of element
# 'x' in sorted 'arr' uses binary
# search technique
def binarySearch(arr, low, high, x):
    while (low <= high):
        mid = int((low + high) / 2)

        if (arr[mid] == x):
            return mid
        elif(arr[mid] > x):
            high = mid - 1
        else:
            low = mid + 1

# function to check whether the given
# array is a 'k' sorted array or not
def isKSortedArray(arr, n, k):

    # auxiliary array 'aux'
    aux = [0 for i in range(n)]

    # copy elements of 'arr' to 'aux'
    for i in range(0, n, 1):
        aux[i] = arr[i]

    # sort 'aux'
    aux.sort(reverse = False)

    # for every element of 'arr' at
    # index 'i', find its index 'j' in 'aux'
    for i in range(0, n, 1):

        # index of arr[i] in sorted
        # array 'aux'
        j = binarySearch(aux, 0, n - 1, arr[i])

        # if abs(i-j) > k, then that element is
        # not at-most k distance away from its
        # target position. Thus, 'arr' is not a
        # k sorted array
        if (abs(i - j) > k):
            return "No"

    # 'arr' is a k sorted array
    return "Yes"

# Driver Code
if __name__ == '__main__':
    arr = [3, 2, 1, 5, 6, 4]
    n = len(arr)
    k = 2
    print("Is it a k sorted array?:",
           isKSortedArray(arr, n, k))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation to check
// whether the given array is a
// k sorted array or not
using System;
using System.Collections;

class GFG {

    // Method to check whether the given
    // array is a 'k' sorted array or not
    static String isKSortedArray(int []arr, int n, int k)
    {
        // auxiliary array 'aux'
        int []aux = new int[n];

        // copy elements of 'arr' to 'aux'
        for (int i = 0; i<n; i++)
            aux[i] = arr[i];

        // sort 'aux'
        Array.Sort(aux);

        // for every element of 'arr' at index
        // 'i', find its index 'j' in 'aux'
        for (int i = 0; i<n; i++)
        {
            // index of arr[i] in sorted array 'aux'
            int j = Array.BinarySearch(aux,arr[i]);

            // if abs(i-j) > k, then that element is
            // not at-most k distance away from its
            // target position. Thus, 'arr' is not a
            // k sorted array
            if (Math.Abs(i - j) > k)
                return "No";
        }

        // 'arr' is a k sorted array
        return "Yes";
    }

    // Driver method
    public static void Main()
    {
        int []arr = {3, 2, 1, 5, 6, 4};
        int k = 2;

        Console.WriteLine("Is it a k sorted array ?: " +
                           isKSortedArray(arr, arr.Length, k));
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// Javascript implementation to check whether the given array
// is a k sorted array or not

// function to find index of element 'x' in sorted 'arr'
// uses binary search technique
function binarySearch(arr, low, high, x)
{
    while (low <= high)
    {
        var mid = parseInt((low + high) / 2);

        if (arr[mid] == x)
            return mid;
        else if (arr[mid] > x)
            high = mid - 1;
        else   
            low = mid + 1;   
    }
}

// function to check whether the given array is
// a 'k' sorted array or not
function isKSortedArray(arr, n, k)
{
    // auxiliary array 'aux'
    var aux = Array(n);

    // copy elements of 'arr' to 'aux'
    for (var i = 0; i<n; i++)
        aux[i] = arr[i];

    // sort 'aux'   
    aux.sort((a,b)=> a-b)

    // for every element of 'arr' at index 'i',
    // find its index 'j' in 'aux'
    for (var i = 0; i<n; i++)
    {
        // index of arr[i] in sorted array 'aux'
        var j = binarySearch(aux, 0, n-1, arr[i]);

        // if abs(i-j) > k, then that element is
        // not at-most k distance away from its
        // target position. Thus,  'arr' is not a
        // k sorted array
        if (Math.abs(i - j) > k)
            return "No";
    }

    // 'arr' is a k sorted array
    return "Yes";   
}

// Driver program to test above
var arr = [3, 2, 1, 5, 6, 4];
var n = arr.length;
var k = 2;
document.write( "Is it a k sorted array?: "
      + isKSortedArray(arr, n, k));

</script>
```

**输出:**

```
Is it a k sorted array?: Yes
```

**时间复杂度:**O(nlogn)
T3】辅助空间: O(n)

**另一种方法**可以是**将相应的元素索引存储到辅助数组**中。然后简单检查一下**腹肌(I–aux[I]。第二)< = k，不满足条件**返回“否”。它比上面提到的方法稍快，因为**我们不必执行二分搜索法来检查与原始索引的距离，**虽然“0”符号保持不变。

## C++

```
#include <bits/stdc++.h>
using namespace std;

string isKSortedArray(int arr[], int n, int k)
{
  // creating an array to store value, index of the original array
  vector<pair<int, int>> aux;

  for(int i=0;i<n;i++){
    aux.push_back({arr[i], i}); //  pushing the elements and index of arr to aux
  }

  // sorting the aux array
  sort(aux.begin(), aux.end());

  //  for every element, check if the absolute value of (currIndex-originalIndex) <= k
  //  if not, then return "NO"
  for(auto i=0;i<n;i++){
    if(abs(i-aux[i].second)>k) return "No";

  }

  // If all elements satisfy the condition, the loop will terminate and
  // "Yes" will be returned.
  return "Yes";
}

int main() {
    int arr[] = {3, 2, 1, 5, 6, 4}; //  input array
      int n = sizeof(arr)/sizeof(int); // number of elements in array(arr)
      int k = 2; // value to check is array is "k" sorted

    cout<<isKSortedArray(arr, n, k); // prints "Yes" since the input array is k-sorted

    return 0;
}
```

**输出:**

```
Yes
```

**时间复杂度:O(nlogn)**

**空间复杂度:O(n)**

本文由**阿育什·乔哈里和那曼·蒙加**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。