# 同一数组中每个元素的楼层

> 原文:[https://www . geeksforgeeks . org/同阵列中每个元素的楼层/](https://www.geeksforgeeks.org/floor-of-every-element-in-same-array/)

给定一个整数数组，为每个元素找到最接近的较小或相同的元素。如果一个元素的所有元素都大于 1，则打印-1。我们可以假设数组至少有两个元素。
**例:**

> 输入:arr[] = {10，5，11，10，20，12}
> 输出:10 -1 10 10 12 11
> 注意 10 有多次出现，所以 10 的楼层就是 10 本身。
> 输入:arr[] = {6，11，7，8，20，12}
> 输出:-1 8 6 7 12 11

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每个拾取的元素，我们遍历剩余的数组并找到最近的较大元素。这个解决方案的时间复杂度是 O(n*n)
一个**更好的解决方案**是对[排序](https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/)的数组并创建一个排序后的副本，然后做二分搜索法为地板。我们遍历数组，对于每个元素，我们搜索大于或等于给定元素的元素的第一次出现。一旦我们找到这样一个元素，我们就检查它的下一个是否也是相同的，如果是，那么这个元素会出现多次，所以我们打印相同的元素作为输出。否则，我们打印排序数组中的前一个元素。在 C++中，[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)返回排序数组中第一个大于或等于元素的迭代器。

## C++

```
// C++ implementation of efficient algorithm to find
// floor of every element
#include <bits/stdc++.h>
using namespace std;

// Prints greater elements on left side of every element
void printPrevGreater(int arr[], int n)
{
    // Create a sorted copy of arr[]
    vector<int> v(arr, arr + n);
    sort(v.begin(), v.end());

    // Traverse through arr[] and do binary search for
    // every element.
    for (int i = 0; i < n; i++) {

        // Floor of first element is -1 if there is only
        // one occurrence of it.
        if (arr[i] == v[0]) {
            (arr[i] == v[1]) ? cout << arr[i] : cout << -1;
            cout << " ";
            continue;
        }

        // Find the first element that is greater than or
        // or equal to given element
        auto it = lower_bound(v.begin(), v.end(), arr[i]);

        // If next element is also same, then there
        // are multiple occurrences, so print it
        if (it != v.end() && *(it + 1) == arr[i])
            cout << arr[i] << " ";

        // Otherwise print previous element
        else
            cout << *(it - 1) << " ";
    }
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = { 6, 11, 7, 8, 20, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printPrevGreater(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of efficient
# algorithm to find floor of every element

# Prints greater elements on left
# side of every element
def printPrevGreater(arr, n) :

    # Create a sorted copy of arr
    v = arr.copy()
    v.sort()

    # Traverse through arr[] and do
    # binary search for every element.
    for i in range(n) :

        # Floor of first element is -1 if
        # there is only one occurrence of it.
        if (arr[i] == v[0]) :
            if (arr[i] == v[1]) :
                print(arr[i], end = " ")

            else :
                print(-1, end = " ")

            continue

        # Find the first element that is greater
        # than or or equal to given element
        if v.count(arr[i]) > 0:
            it = v[v.index(arr[i])]
        else :
            it = v[n - 1]

        # If next element is also same, then there
        # are multiple occurrences, so print it
        if (it != v[n - 1] and
                  v[v.index(it) + 1] == arr[i]) :
            print(arr[i], end = " ")

        # Otherwise print previous element
        else :
            print(v[v.index(it) - 1], end = " ")

# Driver Code
if __name__ == "__main__" :

    arr = [ 6, 11, 7, 8, 20, 12 ]
    n = len(arr)
    printPrevGreater(arr, n)

# This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript implementation of efficient algorithm to find
// floor of every element

// Prints greater elements on left side of every element
function printPrevGreater(arr, n)
{
    // Create a sorted copy of arr[]
    let v = [...arr]
    v.sort((a, b) => a - b);

    // Traverse through arr[] and do binary search for
    // every element.
    for (let i = 0; i < n; i++) {

        // Floor of first element is -1 if there is only
        // one occurrence of it.
        if (arr[i] == v[0]) {
            (arr[i] == v[1]) ?
            document.write(arr[i]) : document.write(-1);
            document.write(" ");
            continue;
        }

        // Find the first element that is greater than or
        // or equal to given element
        if (v.includes(arr[i]))
            it = v[v.indexOf(arr[i])]
        else
            it = v[n - 1]

        // If next element is also same, then there
        // are multiple occurrences, so print it
        if (it != v[n - 1] && (v[v.indexOf(it) + 1] == arr[i]))
            document.write(arr[i] + " ");

        // Otherwise print previous element
        else
            document.write(v[v.indexOf(it) - 1] + " ");
    }
}

function lower_bound(arr, val){

}

/* Driver program to test insertion sort */

    let arr = [ 6, 11, 7, 8, 20, 12 ];
    let n = arr.length;
    printPrevGreater(arr, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
-1 8 6 7 12 11
```

时间复杂度:O(n Log n)
辅助空间:O(n)