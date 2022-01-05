# 从存储右侧较大元素计数的数组生成原始数组

> 原文:[https://www . geesforgeks . org/generate-original-array-array-store-counts-greater-elements-right/](https://www.geeksforgeeks.org/generate-original-array-array-store-counts-greater-elements-right/)

给定一个大于[]的整数数组，其中数组的每个值都表示在未知数组 arr[]中有多少元素大于其右侧的元素。我们的任务是生成原始数组 arr[]。可以假设原始数组包含范围从 1 到 n 的元素，并且所有元素都是唯一的
**示例:**

```
Input  : greater[] = { 6, 3, 2, 1, 0, 0, 0 }
Output : arr[] = [ 1, 4, 5, 6, 7, 3, 2 ]

Input  : greater[] = { 0, 0, 0, 0, 0 }
Output : arr[] = [ 5, 4, 3, 2, 1 ]  
```

我们考虑一个元素数组 temp[] = {1，2，3，4，..n}。我们知道大于[0]的值表示元素计数大于 arr[0]。我们可以观察到温度[]的第**(n–大于[0])个**元素可以放在 arr[0]处。所以我们将它放在 arr[0]处，并从 temp[]中删除它。我们对剩余元素重复上述过程。对于每一个大于[i]的元素，我们将 temp[]的第(n–大于[I]–I)个元素放入 arr[i]中，并将其从 temp[]中移除。
以下是以上想法的实现

## C++

```
// C++ program to generate original array
// from an array that stores counts of
// greater elements on right.
#include <bits/stdc++.h>
using namespace std;

void originalArray(int greater[], int n)
{
    // Array that is used to include every
    // element only once
    vector<int> temp;
    for (int i = 0; i <= n; i++)
        temp.push_back(i);

    // Traverse the array element
    int arr[n];
    for (int i = 0; i < n; i++) {

        // find the K-th (n-greater[i]-i)
        // smallest element in Include_Array
        int k = n - greater[i] - i;

        arr[i] = temp[k];

        // remove current k-th element
        // from Include array
        temp.erase(temp.begin() + k);
    }

    // print resultant array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// driver program to test above function
int main()
{
    int Arr[] = { 6, 3, 2, 1, 0, 1, 0 };
    int n = sizeof(Arr) / sizeof(Arr[0]);
    originalArray(Arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate original array
// from an array that stores counts of
// greater elements on right.
import java.util.Vector;

class GFG
{

static void originalArray(int greater[], int n)
{
    // Array that is used to include every
    // element only once
    Vector<Integer> temp = new Vector<Integer>();
    for (int i = 0; i <= n; i++)
        temp.add(i);

    // Traverse the array element
    int arr[] = new int[n];
    for (int i = 0; i < n; i++)
    {

        // find the K-th (n-greater[i]-i)
        // smallest element in Include_Array
        int k = n - greater[i] - i;

        arr[i] = temp.get(k);

        // remove current k-th element
        // from Include array
        temp.remove(k);
    }

    // print resultant array
    for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int Arr[] = { 6, 3, 2, 1, 0, 1, 0 };
    int n = Arr.length;
    originalArray(Arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program original array from an
# array that stores counts of greater
# elements on right
def originalArray(greater, n):

    # array that is used to include
    # every element only once
    temp = []

    for i in range(n + 1):
        temp.append(i)

    # traverse the array element
    arr = [0 for i in range(n)]

    for i in range(n):

        # find the Kth (n-greater[i]-i)
        # smallest element in Include_array
        k = n - greater[i] - i

        arr[i] = temp[k]

        # remove current kth element
        # from include array
        del temp[k]

    for i in range(n):
        print(arr[i], end = " ")

# Driver code
arr = [6, 3, 2, 1, 0, 1, 0]
n = len(arr)
originalArray(arr, n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to generate original array
// from an array that stores counts of
// greater elements on right.
using System;
using System.Collections.Generic;

class GFG
{

static void originalArray(int []greater, int n)
{
    // Array that is used to include every
    // element only once
    List<int> temp = new List<int>();
    for (int i = 0; i <= n; i++)
        temp.Add(i);

    // Traverse the array element
    int []arr = new int[n];
    for (int i = 0; i < n; i++)
    {

        // find the K-th (n-greater[i]-i)
        // smallest element in Include_Array
        int k = n - greater[i] - i;

        arr[i] = temp[k];

        // remove current k-th element
        // from Include array
        temp.RemoveAt(k);
    }

    // print resultant array
    for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
}

// Driver code
public static void Main()
{
    int []Arr = { 6, 3, 2, 1, 0, 1, 0 };
    int n = Arr.Length;
    originalArray(Arr, n);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to generate original array
// from an array that stores counts of
// greater elements on right.

    function originalArray(greater,n)
    {
        // Array that is used to include every
    // element only once
    let temp = [];
    for (let i = 0; i <= n; i++)
        temp.push(i);

    // Traverse the array element
    let arr = new Array(n);
    for (let i = 0; i < n; i++)
    {

        // find the K-th (n-greater[i]-i)
        // smallest element in Include_Array
        let k = n - greater[i] - i;

        arr[i] = temp[k];

        // remove current k-th element
        // from Include array
        temp.splice(k,1);
    }

    // print resultant array
    for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Driver code
    let Arr=[6, 3, 2, 1, 0, 1, 0 ];
    let n = Arr.length;
    originalArray(Arr, n);

// This code is contributed by patel2127

</script>
```

**输出:**

```
1 4 5 6 7 2 3
```

**时间复杂度:** (n <sup>2</sup> )(擦除操作取向量中的 O(n)