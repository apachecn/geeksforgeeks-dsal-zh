# 根据设置的位数对数组进行排序|设置 2

> 原文:[https://www . geeksforgeeks . org/sort-a-array-on-count-set-bit-set-2/](https://www.geeksforgeeks.org/sort-an-array-according-to-count-of-set-bits-set-2/)

给定一个正整数数组 **arr[]** ，任务是按照数组元素二进制表示中设置位的计数递减顺序对数组进行排序。
对于二进制表示中具有相同位数的整数，根据它们在原始数组中的位置进行排序，即稳定排序。例如，如果输入数组是{3，5}，那么输出数组也应该是{3，5}。请注意，3 和 5 具有相同数量的设置位。
**示例:**

> **输入:** arr[] = {5，2，3，9，4，6，7，15，32}
> **输出:** 15 7 5 3 9 6 2 4 32
> 整数的二进制表示为:
> 15–1111
> 7–0111
> 5–0101
> 3–0011
> 9–1001
> 6–0110【T12
> **产量:** 3 5 6 1 2 4

**方法:**上一节我们已经用各种方法讨论了基于集合比特计数的排序方法。本文包含使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)的实现。
众所周知，地图/多地图以有序的方式存储数据。因此，如果我们在 map 中为 arr[i]存储(32–countsetbits(arr[I])，那么输出将按照设置位计数的递减顺序输出，这就是所需的输出。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// function to sort the array according
// to the number of set bits in elements
void sortArr(int arr[], int n)
{
    multimap<int, int> map;

    for (int i = 0; i < n; i++) {
        int count = 0;
        int k = arr[i];

        // Counting no of setBits in arr[i]
        while (k) {
            k = k & k - 1;
            count++;
        }

        // The count is subtracted from 32
        // because the result needs
        // to be in descending order
        map.insert(make_pair(32 - count, arr[i]));
    }

    // Printing the numbers in descending
    // order of set bit count
    for (auto it = map.begin(); it != map.end(); it++) {
        cout << (*it).second << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 2, 3, 9, 4, 6, 7, 15, 32 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# function to sort the array according
# to the number of set bits in elements
def sortArr(arr, n):

    mp = []

    for i in range( n):
        count = 0
        k = arr[i]

        # Counting no of setBits in arr[i]
        while (k):
            k = k & k - 1
            count += 1

        # The count is subtracted from 32
        # because the result needs
        # to be in descending order
        mp.append((32 - count, arr[i]))

    # Printing the numbers in descending
    # order of set bit count
    mp.sort(key = lambda x: x[0])
    for it in mp:
        print(it[1], end= " ")

# Driver code
if __name__ == "__main__":

    arr = [ 5, 2, 3, 9, 4, 6, 7, 15, 32 ]
    n = len(arr)

    sortArr(arr, n)

# This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// function to sort the array according
// to the number of set bits in elements
function sortArr(arr,n)
{
    let map=[];

    for (let i = 0; i < n; i++) {
        let count = 0;
        let k = arr[i];

        // Counting no of setBits in arr[i]
        while (k) {
            k = k & k - 1;
            count++;
        }

        // The count is subtracted from 32
        // because the result needs
        // to be in descending order
        map.push([32 - count, arr[i]]);
    }

      map.sort(function(a,b){return a[0]-b[0];});
    // Printing the numbers in descending
    // order of set bit count
    for (let i=0;i<map.length;i++) {
        document.write(map[i][1]+" ");
    }
}

// Driver code
let arr=[5, 2, 3, 9, 4, 6, 7, 15, 32 ];
let n=arr.length;
sortArr(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
15 7 5 3 9 6 2 4 32
```

时间复杂度:O(n * log n)

辅助空间:O(n)