# 对设置位等于 K 的数组元素进行排序

> 原文:[https://www . geesforgeks . org/sorting-array-elements-with-set-bits-equal-k/](https://www.geeksforgeeks.org/sorting-array-elements-with-set-bits-equal-to-k/)

给定一个整数数组和一个数字![K ](img/d1076226796ec4213a670c66e7103da1.png "Rendered by QuickLaTeX.com")。任务是只对数组中总设置位等于 k 的那些元素进行排序。排序必须只在它们的相对位置进行，而不影响任何其他元素。
**示例** :

```
Input : arr[] = {32, 1, 9, 4, 64, 2}, K = 1 
Output : 1 2 9 4 32 64
All of the elements except 9 has exactly 1 bit set.
So, all elements except 9 are sorted without affecting
the position of 9 in the input array.

Input : arr[] = {2, 15, 12, 1, 3, 9}, K = 2 
Output : 2 15 3 1 9 12
```

**进场:**

*   初始化两个空向量。
*   从左到右遍历数组，检查每个元素的设置位。
*   这里，C++内置函数 [__builtin_popcount()来计数设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。
*   在第一个向量中，插入设置位等于 k 的所有元素的索引
*   在第二个向量中，插入设置位等于 k 的元素
*   对第二个向量进行排序。
*   现在，我们在排序顺序中有所有设置位等于 K 的元素的索引，也有所有设置位为 K 的元素的索引。
*   因此，将第二个向量的元素逐个插入数组中第一个向量的索引处。

以下是上述方法的实现:

## C++

```
// C++ program for sorting array elements
// with set bits equal to K

#include <bits/stdc++.h>
using namespace std;

// Function to sort elements with
// set bits equal to k
void sortWithSetbits(int arr[], int n, int k)
{
    // initialise two vectors
    vector<int> v1, v2;

    for (int i = 0; i < n; i++) {
        if (__builtin_popcount(arr[i]) == k) {

            // first vector contains indices of
            // required element
            v1.push_back(i);

            // second vector contains
            // required elements
            v2.push_back(arr[i]);
        }
    }

    // sorting the elements in second vector
    sort(v2.begin(), v2.end());

    // replacing the elements with k set bits
    // with the sorted elements
    for (int i = 0; i < v1.size(); i++)
        arr[v1[i]] = v2[i];

    // printing the new sorted array elements
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 14, 255, 1, 7, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    sortWithSetbits(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for sorting array elements
// with set bits equal to K
import java.util.*;

// Represents node of a doubly linked list
class Node
{

    // Function to sort elements with
    // set bits equal to k
    static void sortWithSetbits(int arr[], int n, int k)
    {
        // initialise two vectors
        Vector<Integer> v1 = new Vector<>(), v2 = new Vector<>();

        for (int i = 0; i < n; i++) {
            if (Integer.bitCount(arr[i]) == k)
            {

                // first vector contains indices of
                // required element
                v1.add(i);

                // second vector contains
                // required elements
                v2.add(arr[i]);
            }
        }

        // sorting the elements in second vector
        Collections.sort(v2);

        // replacing the elements with k set bits
        // with the sorted elements
        for (int i = 0; i < v1.size(); i++)
        {
            arr[v1.get(i)] = v2.get(i);
        }

        // printing the new sorted array elements
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {14, 255, 1, 7, 13};
        int n = arr.length;
        int k = 3;

        sortWithSetbits(arr, n, k);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program for sorting array
# elements with set bits equal to K

# Function to sort elements with
# set bits equal to k
def sortWithSetbits(arr, n, k):

    # initialise two vectors
    v1 = []
    v2 = []

    for i in range(0, n, 1):
        if (bin(arr[i]).count('1') == k):

            # first vector contains indices
            # of required element
            v1.append(i)

            # second vector contains
            # required elements
            v2.append(arr[i])

    # sorting the elements in second vector
    v2.sort(reverse = False)

    # replacing the elements with k set
    # bits with the sorted elements
    for i in range(0, len(v1), 1):
        arr[v1[i]] = v2[i]

    # printing the new sorted array elements
    for i in range(0, n, 1):
        print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [14, 255, 1, 7, 13]
    n = len(arr)
    k = 3

    sortWithSetbits(arr, n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program for sorting array elements
// with set bits equal to K
using System;
using System.Collections.Generic;

// Represents node of a doubly linked list
public class Node
{

    // Function to sort elements with
    // set bits equal to k
    static void sortWithSetbits(int []arr, int n, int k)
    {
        // initialise two vectors
        List<int> v1 = new List<int>();
        List<int> v2 = new List<int>();

        for (int i = 0; i < n; i++)
        {
            if (bitCount(arr[i]) == k)
            {

                // first vector contains indices of
                // required element
                v1.Add(i);

                // second vector contains
                // required elements
                v2.Add(arr[i]);
            }
        }

        // sorting the elements in second vector
        v2.Sort();

        // replacing the elements with k set bits
        // with the sorted elements
        for (int i = 0; i < v1.Count; i++)
        {
            arr[v1[i]] = v2[i];
        }

        // printing the new sorted array elements
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }

static int bitCount(long x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
public static void Main(String[] args)
{
        int []arr = {14, 255, 1, 7, 13};
        int n = arr.Length;
        int k = 3;

        sortWithSetbits(arr, n, k);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program for sorting array elements
// with set bits equal to K

function bitCount(x)
{
    var setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Function to sort elements with
// set bits equal to k
function sortWithSetbits(arr, n, k)
{
    // initialise two vectors
    var v1 = [], v2 = [];

    for (var i = 0; i < n; i++) {
        if (bitCount(arr[i]) == k) {

            // first vector contains indices of
            // required element
            v1.push(i);

            // second vector contains
            // required elements
            v2.push(arr[i]);
        }
    }

    // sorting the elements in second vector
    v2.sort((a,b)=> a-b);

    // replacing the elements with k set bits
    // with the sorted elements
    for (var i = 0; i < v1.length; i++)
        arr[v1[i]] = v2[i];

    // printing the new sorted array elements
    for (var i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Driver code
var arr = [14, 255, 1, 7, 13 ];
var n = arr.length;
var k = 3;
sortWithSetbits(arr, n, k);

</script>
```

**Output:** 

```
7 255 1 13 14
```