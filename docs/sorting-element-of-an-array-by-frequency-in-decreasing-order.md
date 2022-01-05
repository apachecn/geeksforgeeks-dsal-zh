# 按频率降序排列数组元素

> 原文:[https://www . geeksforgeeks . org/按频率降序排列数组元素/](https://www.geeksforgeeks.org/sorting-element-of-an-array-by-frequency-in-decreasing-order/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是将数组**arr【】**按照元素出现的频率降序排序。
**注:**如果两个元素的频率相同，那么应该以较小的元素为先。

**示例:**

> **输入:** arr[] = { 4，4，5，6，4，2，2，8，5 }
> **输出:**4 4 2 5 6 8
> 
> **输入:** arr[] = { 9，9，5，8，5 }
> 输出: 5 5 9 9 8

**进场:**

*   将所有元素的频率存储在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中。
*   对于 arr[] = { 4，4，5，6，4，2，2，8，5 }
    上述数组的频率数组为:
    freq[] = { 0，0，2，0，3，2，0，1，0，1}
*   遍历频率[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，对于频率大于 **1** 的所有元素，更新数组**arr【】**中的值如下:

> freq[2]= 2
> arr[0]= 100000 * freq[2]+(100000–2)= 299998
> freq[4]= 3
> arr[1]= 100000 * freq[2]+(100000–4)= 39996
> freq[5]= 2
> arr[2]= 100000 * freq[2]+(110

*   按降序排列数组 **arr[]** 。
*   遍历[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**并根据步骤 2 中[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素的更新获得该元素的元素和频率，执行以下操作:

> 得到当前元素的频率:
> 频率= arr[I]/100000；
> 获取值:
> 值= 100000–arr[I]% 100000

例如:

> 如果 arr[i] = 399996
> 频率= arr[I]/100000 = 399996/100000 = 3
> 值= 100000–arr[I]% 100000 = 100000–99996 = 4
> 元素 **4** 具有频率 **3** 。

*   对于**arr【】**中的每个元素，在每个索引处找到**值**和频率(比如说 **f** ，并打印出数值 **f** 的次数。

下面是上述方法的实现:

## C++

```
// C++ program to sort an array in
// decreasing order of their frequency
#include "bits/stdc++.h"
using namespace std;

// Function that return the index
// upto all the array elements are
// updated.
int sortByFreq(int* arr, int n)
{

    // Initialise maxE = -1
    int maxE = -1;

    // Find the maximum element of
    // arr[]
    for (int i = 0; i < n; i++) {
        maxE = max(maxE, arr[i]);
    }

    // Create frequency array freq[]
    int freq[maxE + 1] = { 0 };

    // Update the frequency array as
    // per the occurrence of element in
    // arr[]
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Initialise cnt to 0
    int cnt = 0;

    // Traversing freq[]
    for (int i = 0; i <= maxE; i++) {

        // If freq of an element is
        // greater than 0 update the
        // value of arr[] at index cnt
        // & increment cnt
        if (freq[i] > 0) {

            int value = 100000 - i;
            arr[cnt] = 100000 * freq[i] + value;
            cnt++;
        }
    }

    // Return cnt
    return cnt;
}

// Function that print array arr[]
// elements in sorted order
void printSortedArray(int* arr, int cnt)
{

    // Traversing arr[] till index cnt
    for (int i = 0; i < cnt; i++) {

        // Find frequency of elements
        int frequency = arr[i] / 100000;

        // Find value at index i
        int value = 100000 - (arr[i] % 100000);

        // Traversing till frequency
        // to print value at index i
        for (int j = 0; j < frequency; j++) {
            cout << value << ' ';
        }
    }
}

// Driver code
int main()
{

    int arr[] = { 4, 4, 5, 6, 4, 2, 2, 8, 5 };

    // Size of array arr[]
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to get cnt
    int cnt = sortByFreq(arr, n);

    // Sort the arr[] in decreasing order
    sort(arr, arr + cnt, greater<int>());

    // Function that prints elements
    // in decreasing order
    printSortedArray(arr, cnt);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array in
// decreasing order of their frequency
import java.util.*;

class GFG{

// Function that return the index
// upto all the array elements are
// updated.
static int sortByFreq(Integer []arr, int n)
{

    // Initialise maxE = -1
    int maxE = -1;

    // Find the maximum element of
    // arr[]
    for (int i = 0; i < n; i++) {
        maxE = Math.max(maxE, arr[i]);
    }

    // Create frequency array freq[]
    int freq[] = new int[maxE + 1];

    // Update the frequency array as
    // per the occurrence of element in
    // arr[]
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Initialise cnt to 0
    int cnt = 0;

    // Traversing freq[]
    for (int i = 0; i <= maxE; i++) {

        // If freq of an element is
        // greater than 0 update the
        // value of arr[] at index cnt
        // & increment cnt
        if (freq[i] > 0) {

            int value = 100000 - i;
            arr[cnt] = 100000 * freq[i] + value;
            cnt++;
        }
    }

    // Return cnt
    return cnt;
}

// Function that print array arr[]
// elements in sorted order
static void printSortedArray(Integer []arr, int cnt)
{

    // Traversing arr[] till index cnt
    for (int i = 0; i < cnt; i++) {

        // Find frequency of elements
        int frequency = arr[i] / 100000;

        // Find value at index i
        int value = 100000 - (arr[i] % 100000);

        // Traversing till frequency
        // to print value at index i
        for (int j = 0; j < frequency; j++) {
            System.out.print(value + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

    Integer arr[] = { 4, 4, 5, 6, 4, 2, 2, 8, 5 };

    // Size of array arr[]
    int n = arr.length;

    // Function call to get cnt
    int cnt = sortByFreq(arr, n);

    // Sort the arr[] in decreasing order
    Arrays.sort(arr, Collections.reverseOrder());

    // Function that prints elements
    // in decreasing order
    printSortedArray(arr, cnt);

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python program to sort an array in
# decreasing order of their frequency

# Function that return the index
# upto all the array elements are
# updated.
def sortByFreq(arr, n):

    # Initialise maxE = -1
    maxE = -1;

    # Find the maximum element of
    # arr[]
    for i in range(n):
        maxE = max(maxE, arr[i])

    # Create frequency array freq[]
    freq = [0]*(maxE + 1);

    # Update the frequency array as
    # per the occurrence of element in
    # arr[]
    for i in range(n):
        freq[arr[i]] += 1;

    # Initialise cnt to 0
    cnt = 0;

    # Traversing freq[]
    for i in range(maxE+1):

        # If freq of an element is
        # greater than 0 update the
        # value of arr[] at index cnt
        # & increment cnt
        if (freq[i] > 0):

            value = 100000 - i;
            arr[cnt] = 100000 * freq[i] + value;
            cnt += 1;

    # Return cnt
    return cnt;

# Function that print array arr[]
# elements in sorted order
def printSortedArray(arr, cnt):

    # Traversing arr[] till index cnt
    for i in range(cnt):

        # Find frequency of elements
        frequency = arr[i] / 100000;

        # Find value at index i
        value = 100000 - (arr[i] % 100000);

        # Traversing till frequency
        # to print value at index i
        for j in range(int(frequency)):
            print(value, end=" ")

# Driver code
if __name__=='__main__':

    arr = [ 4, 4, 5, 6, 4, 2, 2, 8, 5 ]

    # Size of array arr[]
    n = len(arr)

    # Function call to get cnt
    cnt = sortByFreq(arr, n);

    # Sort the arr[] in decreasing order
    arr.sort(reverse = True)

    # Function that prints elements
    # in decreasing order
    printSortedArray(arr, cnt);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to sort an array in
// decreasing order of their frequency
using System;

class GFG {

  // Function that return the index
  // upto all the array elements are
  // updated.
  static int sortByFreq(int[] arr, int n)
  {

    // Initialise maxE = -1
    int maxE = -1;

    // Find the maximum element of
    // arr[]
    for (int i = 0; i < n; i++)
    {
      maxE = Math.Max(maxE, arr[i]);
    }

    // Create frequency array freq[]
    int[] freq = new int[maxE + 1];

    // Update the frequency array as
    // per the occurrence of element in
    // arr[]
    for (int i = 0; i < n; i++)
    {
      freq[arr[i]]++;
    }

    // Initialise cnt to 0
    int cnt = 0;

    // Traversing freq[]
    for (int i = 0; i <= maxE; i++)
    {

      // If freq of an element is
      // greater than 0 update the
      // value of arr[] at index cnt
      // & increment cnt
      if (freq[i] > 0)
      {
        int value = 100000 - i;
        arr[cnt] = 100000 * freq[i] + value;
        cnt++;
      }
    }

    // Return cnt
    return cnt;
  }

  // Function that print array arr[]
  // elements in sorted order
  static void printSortedArray(int[] arr, int cnt)
  {

    // Traversing arr[] till index cnt
    for (int i = 0; i < cnt; i++)
    {

      // Find frequency of elements
      int frequency = arr[i] / 100000;

      // Find value at index i
      int value = 100000 - (arr[i] % 100000);

      // Traversing till frequency
      // to print value at index i
      for (int j = 0; j < frequency; j++)
      {
        Console.Write(value + " ");
      }
    }
  }

  // Driver code
  public static void Main()
  {
    int[] arr = { 4, 4, 5, 6, 4, 2, 2, 8, 5 };

    // Size of array arr[]
    int n = arr.Length;

    // Function call to get cnt
    int cnt = sortByFreq(arr, n);

    // Sort the arr[] in decreasing order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Function that prints elements
    // in decreasing order
    printSortedArray(arr, cnt);
  }
}

// This code is contributed by subhamahato348
```

## java 描述语言

```
<script>

      // JavaScript program to sort an array in
      // decreasing order of their frequency

      // Function that return the index
      // upto all the array elements are
      // updated.
      function sortByFreq(arr, n) {
        // Initialise maxE = -1
        var maxE = -1;

        // Find the maximum element of
        // arr[]
        for (var i = 0; i < n; i++) {
          maxE = Math.max(maxE, arr[i]);
        }

        // Create frequency array freq[]
        var freq = new Array(maxE + 1).fill(0);

        // Update the frequency array as
        // per the occurrence of element in
        // arr[]
        for (var i = 0; i < n; i++) {
          freq[arr[i]]++;
        }

        // Initialise cnt to 0
        var cnt = 0;

        // Traversing freq[]
        for (var i = 0; i <= maxE; i++) {
          // If freq of an element is
          // greater than 0 update the
          // value of arr[] at index cnt
          // & increment cnt
          if (freq[i] > 0) {
            var value = 100000 - i;
            arr[cnt] = 100000 * freq[i] + value;
            cnt++;
          }
        }

        // Return cnt
        return cnt;
      }

      // Function that print array arr[]
      // elements in sorted order
      function printSortedArray(arr, cnt) {
        // Traversing arr[] till index cnt
        for (var i = 0; i < cnt; i++) {
          // Find frequency of elements
          var frequency = parseInt(arr[i] / 100000);

          // Find value at index i
          var value = 100000 - (arr[i] % 100000);

          // Traversing till frequency
          // to print value at index i
          for (var j = 0; j < frequency; j++) {
            document.write(value + " ");
          }
        }
      }

      // Driver code
      var arr = [4, 4, 5, 6, 4, 2, 2, 8, 5];

      // Size of array arr[]
      var n = arr.length;

      // Function call to get cnt
      var cnt = sortByFreq(arr, n);

      // Sort the arr[] in decreasing order
      arr.sort((a, b) => b - a);

      // Function that prints elements
      // in decreasing order
      printSortedArray(arr, cnt);

</script>
```

**Output:** 

```
4 4 4 2 2 5 5 6 8
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)

基于 STL [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)和[比较器](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)的方法:

方法:

1.在地图中存储每个元素的频率。

2.迭代地图并将每个元素及其频率存储在一对向量中。

3.传递一个比较器，如果频率相等，该比较器按照频率的降序和元素值对元素进行排序。

4.在最终数组中多次按下元素的频率。

## C++

```
#include<bits/stdc++.h>
using namespace std;
bool compare(pair<int,int>p1,pair<int,int>p2)
{
    if(p1.second==p2.second) //if frequency is equal
    {
        return p1.first<p2.first; //return the smaller value
    }
    return p1.second>p2.second; //return the element with greater frequency
}
int main()
{
    vector<int>arr={4,4,5,6,4,2,2,8,5};
    int n=arr.size();
    map<int,int>m;
    for(int i=0;i<n;i++)
    {
        m[arr[i]]+=1;
    }
    vector<pair<int,int>>a;
    for(auto it=m.begin();it!=m.end();it++)
    {
        a.push_back(make_pair(it->first,it->second)); //making pair of element and it's frequency
    }
    sort(a.begin(),a.end(),compare);
    vector<int>ans;
    for(auto x:a)
    {
        while(x.second--)
        {
        ans.push_back(x.first);
        }
    }
    for(auto x:ans)
    {
        cout<<x<<" ";
    }
    return 0;
}
```

**Output**

```
4 4 4 2 2 5 5 6 8 
```