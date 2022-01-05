# 移除元素使数组排序

> 原文:[https://www . geesforgeks . org/remove-elements-to-make-array-sorted/](https://www.geeksforgeeks.org/remove-elements-to-make-array-sorted/)

给定一个整数数组，任务是从数组中移除元素，使数组排序。也就是说，移除不遵循递增顺序的元素。

**示例:**

> **输入:** arr[] = {1，2，4，3，5，7，8，6，9，10}
> **输出:** 1 2 4 5 7 8 9 10
> 
> **输入:** arr[] = {10，12，9，5，2，13，14}
> 输出: 10 12 13 14

**方法:**遍历给定的数组，对于每个大于或等于前一个元素的元素，将这个元素添加到另一个数组中，否则跳到下一个元素。最后新创建的数组会按照斯大林排序进行排序。

1.  对于每个元素，检查该元素是否大于前一个元素。
    *   如果是，则检查下一个元素。
    *   否则移除该元素。
2.  遍历完所有元素后，我们将得到一个排序的数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the array
// by removing misplaced elements
void removeElements(int arr[], int n)
{

    // brr[] is used to store
    // the sorted array elements
    int brr[n], l = 1;

    brr[0] = arr[0];
    for (int i = 1; i < n; i++) {
        if (brr[l - 1] <= arr[i]) {
            brr[l] = arr[i];
            l++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < l; i++)
        cout << brr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 10, 12, 9, 10, 2, 13, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    removeElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to sort the array
// by removing misplaced elements
static void removeElements(int []arr, int n)
{

    // brr[] is used to store
    // the sorted array elements
    int []brr = new int[n];
    int l = 1;

    brr[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        if (brr[l - 1] <= arr[i])
        {
            brr[l] = arr[i];
            l++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < l; i++)
        System.out.print(brr[i] + " ");
}

// Driver code
static public void main (String[] args)
{
    int []arr = { 10, 12, 9, 10, 2, 13, 14 };
    int n = arr.length;
    removeElements(arr, n);
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to sort the array
# by removing misplaced elements
def removeElements(arr,  n) :

    # brr[] is used to store
    # the sorted array elements
    brr = [0]*n; l = 1;

    brr[0] = arr[0];
    for i in range(1,n) :
        if (brr[l - 1] <= arr[i]) :
            brr[l] = arr[i];
            l += 1;

    # Print the sorted array
    for i in range(l) :
        print(brr[i],end=" ");

# Driver code
if __name__ == "__main__" :

    arr = [ 10, 12, 9, 10, 2, 13, 14 ];
    n = len(arr);
    removeElements(arr, n);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to sort the array
// by removing misplaced elements
static void removeElements(int []arr, int n)
{

    // brr[] is used to store
    // the sorted array elements
    int []brr = new int[n];
    int l = 1;

    brr[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        if (brr[l - 1] <= arr[i])
        {
            brr[l] = arr[i];
            l++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < l; i++)
        Console.Write(brr[i] + " ");
}

// Driver code
static public void Main ()
{
    int []arr = { 10, 12, 9, 10, 2, 13, 14 };
    int n = arr.Length;
    removeElements(arr, n);
}
}

// This code is contributed by jit_t
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to sort the array
    // by removing misplaced elements
    function removeElements(arr, n)
    {

        // brr[] is used to store
        // the sorted array elements
        let brr = new Array(n);
        brr.fill(0);
        let l = 1;

        brr[0] = arr[0];
        for (let i = 1; i < n; i++)
        {
            if (brr[l - 1] <= arr[i])
            {
                brr[l] = arr[i];
                l++;
            }
        }

        // Print the sorted array
        for (let i = 0; i < l; i++)
            document.write(brr[i] + " ");
    }

    let arr = [ 10, 12, 9, 10, 2, 13, 14 ];
    let n = arr.length;
    removeElements(arr, n);

</script>
```

**Output:** 

```
10 12 13 14
```

**方法 2:** 不要使用额外的数组，而是将它们存储在同一个数组中

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the array
// by removing misplaced elements
void removeElements(int arr[], int n)
{

    // l stores the index
    int l = 1;
    for (int i = 1; i < n; i++) {
        if (arr[l - 1] <= arr[i]) {
            arr[l] = arr[i];
            l++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < l; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 10, 12, 9, 10, 2, 13, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    removeElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Function to sort the array
// by removing misplaced elements
static void removeElements(int arr[], int n)
{

    // l stores the index
    int l = 1;
    for(int i = 1; i < n; i++)
    {
        if (arr[l - 1] <= arr[i])
        {
            arr[l] = arr[i];
            l++;
        }
    }

    // Print the sorted array
    for(int i = 0; i < l; i++)
        System.out.print(arr[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 10, 12, 9, 10, 2, 13, 14 };
    int n = arr.length;

    removeElements(arr, n);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to sort the array
# by removing misplaced elements
def removeElements(arr, n):

    # l stores the index
    l = 1
    for i in range(1, n):
        if (arr[l - 1] <= arr[i]):
            arr[l] = arr[i]
            l += 1

    # Print the sorted array
    for i in range(l):
        print(arr[i], end = " ")

# Driver code
if __name__ == "__main__" :

    arr = [ 10, 12, 9, 10, 2, 13, 14 ]
    n = len(arr)

    removeElements(arr, n)

# This code is contributed by Surbhi Tyagi.
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to sort the array
// by removing misplaced elements
public static void removeElements(int []arr, int n)
{

    // l stores the index
    int l = 1;
    for(int i = 1; i < n; i++)
    {
        if (arr[l - 1] <= arr[i])
        {
            arr[l] = arr[i];
            l++;
        }
    }

    // Print the sorted array
    for(int i = 0; i < l; i++)
        Console.Write( arr[i] + " ");
}

// Driver code
public static void Main(string []args)
{
    int []arr = { 10, 12, 9, 10, 2, 13, 14 };
    int n = arr.Length;

    removeElements(arr, n);
}
}

// This code is contributed by importantly
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to sort the array
    // by removing misplaced elements
    function removeElements(arr, n)
    {

        // l stores the index
        let l = 1;
        for (let i = 1; i < n; i++) {
            if (arr[l - 1] <= arr[i]) {
                arr[l] = arr[i];
                l++;
            }
        }

        // Print the sorted array
        for (let i = 0; i < l; i++)
            document.write(arr[i] + " ");
    }

    let arr = [ 10, 12, 9, 10, 2, 13, 14 ];
    let n = arr.length;
    removeElements(arr, n);

</script>
```

**Output:** 

```
10 12 13 14
```