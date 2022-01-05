# 同一数组中每个元素的上限

> 原文:[https://www . geeksforgeeks . org/同阵列中每个元素的上限/](https://www.geeksforgeeks.org/ceiling-of-every-element-in-same-array/)

给定一个整数数组，为每个元素找到最接近的较小或相同的元素。如果一个元素的所有元素都大于 1，那么打印-1
**示例:**

> 输入:arr[] = {10，5，11，10，20，12}
> 输出:10 10 12 10 -1 20
> 注意 10 有多次出现，所以 10 的上限就是 10 本身。
> 输入:arr[] = {6，11，7，8，20，12}
> 输出:7 12 8 11 -1 20

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每个拾取的元素，我们遍历剩余的数组并找到最近的较大元素。该方案的时间复杂度为 O(n*n)

**使用哈希的另一种方法:**

解决方案是将每个元素的答案存储在地图中。这可以通过使用第二个映射(比如 m)来实现，它将存储元素的频率，并根据关键字自动对其进行排序。然后遍历地图 m，找到每个键的答案，并将答案存储在地图 res[key]中。

时间复杂度:0(n)

空间复杂度:0(n)

## C++

```
// C++ implementation to find the closest smaller or same
// element for every element.

#include <bits/stdc++.h>
using namespace std;

map<int, int> m; // initialise two maps
map<int, int> res;

void printPrevGreater(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        m[arr[i]]++; // Add elements to map to store count
    }

    int c = 0;
    int prev;
    int f = 0;
    for (auto i = m.begin(); i != m.end(); i++) {

        if (f == 1) {
            res[prev] = i->first;// check if previous element have
                           // no similar element ,store next
                           // element occuring in map in
                           // res[previous_element]
            f = 0;
            c++;
        }

        if (i->second == 1) { // if current element count is
                              // 1 then its greater value
                              // will be map's next element
            f = 1;
            prev = i->first;
        }

        else if (i->second
                 > 1) { // if current element count is
                        // greater than 1, it means there are
                        // similar elements
            res[i->first] = i->first;
            c++;
            f = 0;
        }
    }

    if (c < n) {
        res[prev] = -1; // checks whether the value for the last
                  // element in map m is stores in res or
                  // not. if not set value to -1 as no other
                  // greater element is there.
    }

    for (int i = 0; i < n; i++) { // print the elements
        cout << res[arr[i]] << " ";
    }
}

int main()
{
    int arr[] = { 6, 11, 7, 8, 20, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printPrevGreater(arr, n);
    return 0;
}
```

一个**更好的解决方案**是[排序](https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/)数组并创建一个排序后的副本，然后做二分搜索法为地板。我们遍历数组，为每个元素搜索第一个更大的元素。在 C++中[上限()](https://www.geeksforgeeks.org/stdupper_bound-in-cpp/)就是为了这个目的。
以下是上述方法的实施。

## C++

```
// C++ implementation of efficient algorithm to find
// floor of every element
#include <bits/stdc++.h>
using namespace std;

// Prints greater elements on left side of every element
void printPrevGreater(int arr[], int n)
{
    if (n == 1) {
        cout << "-1";
        return;
    }

    // Create a sorted copy of arr[]
    vector<int> v(arr, arr + n);
    sort(v.begin(), v.end());

    // Traverse through arr[] and do binary search for
    // every element.
    for (int i = 0; i < n; i++) {

        // Find the first element that is greater than
        // the given element
        auto it = upper_bound(v.begin(), v.end(), arr[i]);

        // Since arr[i] also exists in array, *(it-1)
        // will be same as arr[i]. Let us check *(it-2)
        // is also same as arr[i]. If true, then arr[i]
        // exists twice in array, so ceiling is same
        // same as arr[i]
        if ((it - 1) != v.begin() && *(it - 2) == arr[i]) {

            // If next element is also same, then there
            // are multiple occurrences, so print it
            cout << arr[i] << " ";
        }

        else if (it != v.end())
            cout << *it << " ";
        else
            cout << -1 << " ";
    }
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = {10, 5, 11, 10, 20, 12};
    int n = sizeof(arr) / sizeof(arr[0]);
    printPrevGreater(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of efficient algorithm to find
// floor of every element
import java.util.Arrays;

class GFG
{

    // Prints greater elements on left side of every element
    static void printPrevGreater(int arr[], int n)
    {
        if (n == 1)
        {
            System.out.println("-1");
            return;
        }

        // Create a sorted copy of arr[]
        int v[] = Arrays.copyOf(arr, arr.length);
        Arrays.sort(v);

        // Traverse through arr[] and do binary search for
        // every element.
        for (int i = 0; i < n; i++)
        {

            // Find the first element that is greater than
            // the given element
            int it = Arrays.binarySearch(v,arr[i]);
            it++;

            // Since arr[i] also exists in array, *(it-1)
            // will be same as arr[i]. Let us check *(it-2)
            // is also same as arr[i]. If true, then arr[i]
            // exists twice in array, so ceiling is same
            // same as arr[i]
            if ((it - 1) != 0 && v[it - 2] == arr[i])
            {

                // If next element is also same, then there
                // are multiple occurrences, so print it
                System.out.print(arr[i] + " ");
            }
            else if (it != v.length)
                System.out.print(v[it] + " ");
            else
                System.out.print(-1 + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {10, 5, 11, 10, 20, 12};
        int n = arr.length;
        printPrevGreater(arr, n);
    }
}

// This code is contributed by
// Rajnis09
```

## 蟒蛇 3

```
# Python implementation of efficient algorithm
# to find floor of every element
import bisect

# Prints greater elements on left side of every element
def printPrevGreater(arr, n):

    if n == 1:
        print("-1")
        return

    # Create a sorted copy of arr[]
    v = list(arr)
    v.sort()

    # Traverse through arr[] and do binary search for
    # every element
    for i in range(n):

        # Find the location of first element that
        # is greater than the given element
        it = bisect.bisect_right(v, arr[i])

        # Since arr[i] also exists in array, v[it-1]
        # will be same as arr[i]. Let us check v[it-2]
        # is also same as arr[i]. If true, then arr[i]
        # exists twice in array, so ceiling is same
        # same as arr[i]
        if (it-1) != 0 and v[it-2] == arr[i]:

            # If next element is also same, then there
            # are multiple occurrences, so print it
            print(arr[i], end=" ")

        elif it <= n-1:
            print(v[it], end=" ")

        else:
            print(-1, end=" ")

# Driver code
if __name__ == "__main__":
    arr = [10, 5, 11, 10, 20, 12]
    n = len(arr)
    printPrevGreater(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of efficient algorithm
// to find floor of every element
using System;

class GFG
{

    // Prints greater elements on left side
    // of every element
    static void printPrevGreater(int []arr, int n)
    {
        if (n == 1)
        {
            Console.Write("-1");
            return;
        }

        // Create a sorted copy of arr[]
        int []v = new int[arr.GetLength(0)];
        Array.Copy(arr, v, arr.GetLength(0));
        Array.Sort(v);

        // Traverse through arr[] and
        // do binary search for every element.
        for (int i = 0; i < n; i++)
        {

            // Find the first element that is
            // greater than the given element
            int it = Array.BinarySearch(v, arr[i]);
            it++;

            // Since arr[i] also exists in array, *(it-1)
            // will be same as arr[i]. Let us check *(it-2)
            // is also same as arr[i]. If true, then arr[i]
            // exists twice in array, so ceiling is same
            // same as arr[i]
            if ((it - 1) != 0 && v[it - 2] == arr[i])
            {

                // If next element is also same, then there
                // are multiple occurrences, so print it
                Console.Write(arr[i] + " ");
            }
            else if (it != v.Length)
                Console.Write(v[it] + " ");
            else
                Console.Write(-1 + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {10, 5, 11, 10, 20, 12};
        int n = arr.Length;
        printPrevGreater(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
10 10 12 10 -1 20
```

**时间复杂度:**O(n Log n)
T3】辅助空间: O(n)