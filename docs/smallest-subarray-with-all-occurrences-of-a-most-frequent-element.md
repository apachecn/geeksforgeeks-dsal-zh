# 具有最频繁元素所有出现的最小子阵列

> 原文:[https://www . geeksforgeeks . org/最小子数组-出现次数最多的元素/](https://www.geeksforgeeks.org/smallest-subarray-with-all-occurrences-of-a-most-frequent-element/)

给定一个数组，设 x 是数组中的一个元素。x 在数组中具有最大频率。找出数组中最小的子段，它也有 x 作为最大频率元素。
**例:**

```
Input :  arr[] = {4, 1, 1, 2, 2, 1, 3, 3} 
Output :   1, 1, 2, 2, 1
The most frequent element is 1\. The smallest
subarray that has all occurrences of it is
1 1 2 2 1

Input :  A[] = {1, 2, 2, 3, 1}
Output : 2, 2
Note that there are two elements that appear
two times, 1 and 2\. The smallest window for
1 is whole array and smallest window for 2 is
{2, 2}. Since window for 2 is smaller, this is
our output.
```

**方法:**观察如果 X 是我们的子片段的最大重复元素，那么日落应该是这样的[X，…..，X]，因为如果子片段以另一个元素结束或开始，我们可以删除它，这不会改变我们的答案。
为了解决这个问题，让我们为数组中的每个不同元素存储三个值，元素第一次出现的索引和最后一次出现的索引元素和元素的频率。在每一步中，对于最大的重复元素，最小化子片段的大小。

## C++

```
// C++ implementation to find smallest
// subarray with all occurrences of
// a most frequent element
#include <bits/stdc++.h>
using namespace std;

void smallestSubsegment(int a[], int n)
{
    // To store left most occurrence of elements
    unordered_map<int, int> left;

    // To store counts of elements
    unordered_map<int, int> count;

    // To store maximum frequency
    int mx = 0;

    // To store length and starting index of
    // smallest result window
    int mn, strindex;

    for (int i = 0; i < n; i++) {

        int x = a[i];

        // First occurrence of an element,
        // store the index
        if (count[x] == 0) {
            left[x] = i;
            count[x] = 1;
        }

        // increase the frequency of elements
        else
            count[x]++;

        // Find maximum repeated element and
        // store its last occurrence and first
        // occurrence
        if (count[x] > mx) {
            mx = count[x];
            mn = i - left[x] + 1; // length of subsegment
            strindex = left[x];
        }

        // select subsegment of smallest size
        else if (count[x] == mx && i - left[x] + 1 < mn) {
            mn = i - left[x] + 1;
            strindex = left[x];
        }
    }

    // Print the subsegment with all occurrences of
    // a most frequent element
    for (int i = strindex; i < strindex + mn; i++)
        cout << a[i] << " ";
}

// Driver code
int main()
{
    int A[] = { 1, 2, 2, 2, 1 };
    int n = sizeof(A) / sizeof(A[0]);
    smallestSubsegment(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find smallest
// subarray with all occurrences of
// a most frequent element
import java.io.*;
import java.util.*;
class GfG {

    static void smallestSubsegment(int a[], int n)
    {
        // To store left most occurrence of elements
        HashMap<Integer, Integer> left= new HashMap<Integer, Integer>();

        // To store counts of elements
        HashMap<Integer, Integer> count= new HashMap<Integer, Integer>();

        // To store maximum frequency
        int mx = 0;

        // To store length and starting index of
        // smallest result window
        int mn = -1, strindex = -1;

        for (int i = 0; i < n; i++)
        {

            int x = a[i];

            // First occurrence of an element,
            // store the index
            if (count.get(x) == null)
            {
                left.put(x, i) ;
                count.put(x, 1);
            }

            // increase the frequency of elements
            else
                count.put(x, count.get(x) + 1);

            // Find maximum repeated element and
            // store its last occurrence and first
            // occurrence
            if (count.get(x) > mx)
            {
                mx = count.get(x);

                // length of subsegment
                mn = i - left.get(x) + 1;
                strindex = left.get(x);
            }

            // select subsegment of smallest size
            else if ((count.get(x) == mx) &&
                    (i - left.get(x) + 1 < mn))
            {
                mn = i - left.get(x) + 1;
                strindex = left.get(x);
            }
        }

        // Print the subsegment with all occurrences of
        // a most frequent element
        for (int i = strindex; i < strindex + mn; i++)
            System.out.print(a[i] + " ");
    }

    // Driver program
    public static void main (String[] args)
    {
        int A[] = { 1, 2, 2, 2, 1 };
        int n = A.length;
        smallestSubsegment(A, n);
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 implementation to find smallest
# subarray with all occurrences of
# a most frequent element
def smallestSubsegment(a, n):

    # To store left most occurrence of elements
    left = dict()

    # To store counts of elements
    count = dict()

    # To store maximum frequency
    mx = 0

    # To store length and starting index of
    # smallest result window
    mn, strindex = 0, 0

    for i in range(n):

        x = a[i]

        # First occurrence of an element,
        # store the index
        if (x not in count.keys()):
            left[x] = i
            count[x] = 1

        # increase the frequency of elements
        else:
            count[x] += 1

        # Find maximum repeated element and
        # store its last occurrence and first
        # occurrence
        if (count[x] > mx):
            mx = count[x]
            mn = i - left[x] + 1 # length of subsegment
            strindex = left[x]

        # select subsegment of smallest size
        elif (count[x] == mx and
              i - left[x] + 1 < mn):
            mn = i - left[x] + 1
            strindex = left[x]

    # Print the subsegment with all occurrences of
    # a most frequent element
    for i in range(strindex, strindex + mn):
        print(a[i], end = " ")

# Driver code
A = [1, 2, 2, 2, 1]
n = len(A)
smallestSubsegment(A, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation to find smallest
// subarray with all occurrences of
// a most frequent element
using System;
using System.Collections.Generic;

class GfG
{

    static void smallestSubsegment(int []a, int n)
    {
        // To store left most occurrence of elements
        Dictionary<int, int> left = new Dictionary<int, int>();

        // To store counts of elements
        Dictionary<int, int> count = new Dictionary<int, int>();

        // To store maximum frequency
        int mx = 0;

        // To store length and starting index of
        // smallest result window
        int mn = -1, strindex = -1;

        for (int i = 0; i < n; i++)
        {

            int x = a[i];

            // First occurrence of an element,
            // store the index
            if (!count.ContainsKey(x))
            {
                left.Add(x, i) ;
                count.Add(x, 1);
            }

            // increase the frequency of elements
            else
                count[x] = count[x] + 1;

            // Find maximum repeated element and
            // store its last occurrence and first
            // occurrence
            if (count[x] > mx)
            {
                mx = count[x];

                // length of subsegment
                mn = i - left[x] + 1;
                strindex = left[x];
            }

            // select subsegment of smallest size
            else if ((count[x] == mx) &&
                    (i - left[x] + 1 < mn))
            {
                mn = i - left[x] + 1;
                strindex = left[x];
            }
        }

        // Print the subsegment with all occurrences of
        // a most frequent element
        for (int i = strindex; i < strindex + mn; i++)
            Console.Write(a[i] + " ");
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []A = { 1, 2, 2, 2, 1 };
        int n = A.Length;
        smallestSubsegment(A, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation to find smallest
// subarray with all occurrences of
// a most frequent element

    function smallestSubsegment(a,n)
    {
        // To store left most occurrence of elements
        let left= new Map();

        // To store counts of elements
        let count= new Map();

        // To store maximum frequency
        let mx = 0;

        // To store length and starting index of
        // smallest result window
        let mn = -1, strindex = -1;

        for (let i = 0; i < n; i++)
        {

            let x = a[i];

            // First occurrence of an element,
            // store the index
            if (count.get(x) == null)
            {
                left.set(x, i) ;
                count.set(x, 1);
            }

            // increase the frequency of elements
            else
                count.set(x, count.get(x) + 1);

            // Find maximum repeated element and
            // store its last occurrence and first
            // occurrence
            if (count.get(x) > mx)
            {
                mx = count.get(x);

                // length of subsegment
                mn = i - left.get(x) + 1;
                strindex = left.get(x);
            }

            // select subsegment of smallest size
            else if ((count.get(x) == mx) &&
                    (i - left.get(x) + 1 < mn))
            {
                mn = i - left.get(x) + 1;
                strindex = left.get(x);
            }
        }

        // Print the subsegment with all occurrences of
        // a most frequent element
        for (let i = strindex; i < strindex + mn; i++)
            document.write(a[i] + " ");
    }

    // Driver program
    let A=[1, 2, 2, 2, 1];
    let n = A.length;
    smallestSubsegment(A, n);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
2 2 2 
```

**时间复杂度:** O(n)