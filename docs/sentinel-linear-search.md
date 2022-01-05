# 哨点线性搜索

> 原文:[https://www.geeksforgeeks.org/sentinel-linear-search/](https://www.geeksforgeeks.org/sentinel-linear-search/)

哨兵线性搜索顾名思义是一种[线性搜索](https://www.geeksforgeeks.org/linear-search/)的类型，与传统的线性搜索相比，比较的次数减少了。当对大小为 N 的数组执行线性搜索时，在最坏的情况下，当要搜索的元素与数组的所有元素进行比较时，进行总共 N 次比较，并且对要比较的元素的索引进行(N + 1)次比较，使得索引不超出数组的边界，这可以在哨兵线性搜索中减少。
在此搜索中，数组的最后一个元素被替换为要搜索的元素，然后对数组执行线性搜索，而不检查当前索引是否在数组的索引范围内，因为要搜索的元素肯定会在数组内找到，即使它在最后一个元素被替换后不在原始数组中。因此，要检查的索引永远不会超出数组的界限。这里最坏情况下的比较次数将是(N + 2)。
**示例:**

> **输入:** arr[] = {10，20，180，30，60，50，110，100，70}，x = 180
> **输出:** 180 出现在索引 2
> **输入:** arr[] = {10，20，180，30，60，50，110，100，70}，x = 90
> **输出:【t100**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to search x in the given array
void sentinelSearch(int arr[], int n, int key)
{

    // Last element of the array
    int last = arr[n - 1];

    // Element to be searched is
    // placed at the last index
    arr[n - 1] = key;
    int i = 0;

    while (arr[i] != key)
        i++;

    // Put the last element back
    arr[n - 1] = last;

    if ((i < n - 1) || (arr[n - 1] == key))
        cout << key << " is present at index " << i;
    else
        cout << "Element Not found";
}

// Driver code
int main()
{
    int arr[] = { 10, 20, 180, 30, 60, 50, 110, 100, 70 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 180;

    sentinelSearch(arr, n, key);

    return 0;
}
// This code is contributed by Mandeep Dalavi
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to search x in the given array
    static void sentinelSearch(int arr[], int n, int key)
    {

        // Last element of the array
        int last = arr[n - 1];

        // Element to be searched is
        // placed at the last index
        arr[n - 1] = key;
        int i = 0;

        while (arr[i] != key)
            i++;

        // Put the last element back
        arr[n - 1] = last;

        if ((i < n - 1) || (arr[n - 1] == key))
            System.out.println(key + " is present at index "
                               + i);
        else
            System.out.println("Element Not found");
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[]
            = { 10, 20, 180, 30, 60, 50, 110, 100, 70 };
        int n = arr.length;
        int key = 180;

        sentinelSearch(arr, n, key);
    }
}

// This code is contributed by Ankit Rai, Mandeep Dalavi
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to search key in the given array

def sentinelSearch(arr, n, key):

    # Last element of the array
    last = arr[n - 1]

    # Element to be searched is
    # placed at the last index
    arr[n - 1] = key
    i = 0

    while (arr[i] != key):
        i += 1

    # Put the last element back
    arr[n - 1] = last

    if ((i < n - 1) or (arr[n - 1] == key)):
        print(key, "is present at index", i)
    else:
        print("Element Not found")

# Driver code
arr = [10, 20, 180, 30, 60, 50, 110, 100, 70]
n = len(arr)
key = 180

sentinelSearch(arr, n, key)

# This code is contributed by divyamohan123, Mandeep Dalavi
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to search x in the given array
    static void sentinelSearch(int[] arr, int n, int key)
    {

        // Last element of the array
        int last = arr[n - 1];

        // Element to be searched is
        // placed at the last index
        arr[n - 1] = key;
        int i = 0;

        while (arr[i] != key)
            i++;

        // Put the last element back
        arr[n - 1] = last;

        if ((i < n - 1) || (arr[n - 1] == key))
            Console.WriteLine(key + " is present"
                              + " at index " + i);
        else
            Console.WriteLine("Element Not found");
    }

    // Driver code
    public static void Main()
    {
        int[] arr
            = { 10, 20, 180, 30, 60, 50, 110, 100, 70 };
        int n = arr.Length;
        int key = 180;

        sentinelSearch(arr, n, key);
    }
}

// This code is contributed by Mohit kumar, Mandeep Dalavi
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to search x in the given array
    function sentinelSearch(arr , n , key) {

        // Last element of the array
        var last = arr[n - 1];

        // Element to be searched is
        // placed at the last index
        arr[n - 1] = key;
        var i = 0;

        while (arr[i] != key)
            i++;

        // Put the last element back
        arr[n - 1] = last;

        if ((i < n - 1) || (arr[n - 1] == key))
            document.write(key + " is present at index " + i);
        else
            document.write("Element Not found");
    }

    // Driver code

        var arr = [ 10, 20, 180, 30, 60, 50, 110, 100, 70 ];
        var n = arr.length;
        var key = 180;

        sentinelSearch(arr, n, key);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
180 is present at index 2
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)