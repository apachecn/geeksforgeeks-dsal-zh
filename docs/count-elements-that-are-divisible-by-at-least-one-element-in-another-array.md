# 计算另一个数组中至少可以被一个元素整除的元素

> 原文:[https://www . geeksforgeeks . org/count-可被另一个数组中至少一个元素整除的元素/](https://www.geeksforgeeks.org/count-elements-that-are-divisible-by-at-least-one-element-in-another-array/)

给定两个数组 arr1[]和 arr2[]。任务是找出第一个数组中至少有一个因子存在于第二个数组中的这种元素的数量。
**例** :

```
Input : arr1[] = {10, 2, 13, 4, 15} ; arr2[] = {2, 4, 5, 6}
Output : 4
There is no factor of 13 which is present in the 
second array. Except 13, factors of the rest 4 
elements of the first array is present in the 
second array.

Input : arr1[] = {11, 13, 17, 15} ; arr2[] = {3, 7, 9, 5}
Output : 1
```

其思想是将第二个数组的所有元素插入到一个散列中，这样因子的查找可以在恒定的时间内完成。现在，遍历第一个数组，对于每个元素[从 1](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 开始生成所有因子，并检查散列中是否存在任何因子。
以下是上述办法的实施情况:

## C++

```
// CPP program to find count of
// elements in first array whose
// atleast one factor is present
// in second array.
#include <bits/stdc++.h>
using namespace std;

// Util function to count the elements
// in first array whose atleast
// one factor is present in second array
int elementCount(int arr1[], int n1, int arr2[], int n2)
{

    // counter to count number of elements
    int count = 0;

    // Hash of second array elements
    unordered_set<int> hash;
    for (int i = 0; i < n2; i++)
        hash.insert(arr2[i]);

    // loop to traverse through array elements
    // and check for its factors
    for (int i = 0; i < n1; i++) {

        // generate factors of elements
        // of first array
        for (int j = 1; j * j <= arr1[i]; j++) {

            // Check if j is a factor
            if (arr1[i] % j == 0) {

                // check if the factor is present in
                // second array using the hash
                if ((hash.find(j) != hash.end()) ||
                        (hash.find(arr1[i] / j) != hash.end())) {
                    count++;
                    break;
                }
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr1[] = { 10, 2, 13, 4, 15 };
    int arr2[] = { 2, 4, 5, 6 };

    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    cout << elementCount(arr1, n1, arr2, n2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of
// elements in first array whose
// atleast one factor is present
// in second array.
import java.util.*;

class GFG
{

    // Util function to count the elements
    // in first array whose atleast
    // one factor is present in second array
    static int elementCount(int arr1[], int n1,
                            int arr2[], int n2)
    {

        // counter to count number of elements
        int count = 0;

        // Hash of second array element
        HashSet<Integer> hash = new HashSet<>();
        for (int i = 0; i < n2; i++)
        {
            hash.add(arr2[i]);
        }

        // loop to traverse through array elements
        // and check for its factors
        for (int i = 0; i < n1; i++)
        {

            // generate factors of elements
            // of first array
            for (int j = 1; j * j <= arr1[i]; j++)
            {

                // Check if j is a factor
                if (arr1[i] % j == 0)
                {

                    // check if the factor is present in
                    // second array using the hash
                    if ((hash.contains(j) && j !=
                        (int) hash.toArray()[hash.size() - 1]) ||
                        (hash.contains(arr1[i] / j) && (arr1[i] / j) !=
                        (int) hash.toArray()[hash.size() - 1]))
                    {
                        count++;
                        break;
                    }
                }
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = {10, 2, 13, 4, 15};
        int arr2[] = {2, 4, 5, 6};

        int n1 = arr1.length;
        int n2 = arr2.length;
        System.out.println(elementCount(arr1, n1, arr2, n2));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python program to find count of
# elements in first array whose
# atleast one factor is present
# in second array.

# Importing sqrt() function
from math import sqrt

# Util function to count the
# elements in first array
# whose atleast one factor is
# present in second array
def elementCount(arr1, arr2):

  # counter to count
  # number of elements
  count = 0

  # Hash of second array elements
  hash = frozenset(arr2)

  # loop to traverse through array
  # elements and check for its factors
  for x in arr1:

    # generate factors of
    # elements of first array
    for j in range(1, int(sqrt(x)) + 1):

      # Check if j is a factor
      if x % j == 0:

        # check if the factor is present
        # in second array using the hash
        if (j in hash or
            x / j in hash):
          count+=1
          break

  return count

# Driver code
arr1 = [ 10, 2, 13, 4, 15 ]
arr2 = [ 2, 4, 5, 6 ]

print(elementCount(arr1, arr2))

# This code is contributed
# by vaibhav29498
```

## C#

```
// C# program to find count of
// elements in first array whose
// atleast one factor is present
// in second array.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

    // Util function to count the elements
    // in first array whose atleast
    // one factor is present in second array
    static int elementCount(int []arr1, int n1,
                            int []arr2, int n2)
    {

        // counter to count number of elements
        int count = 0;

        // Hash of second array element
        HashSet<int> hash = new HashSet<int>();
        for (int i = 0; i < n2; i++)
        {
            hash.Add(arr2[i]);
        }

        // loop to traverse through array elements
        // and check for its factors
        for (int i = 0; i < n1; i++)
        {

            // generate factors of elements
            // of first array
            for (int j = 1; j * j <= arr1[i]; j++)
            {

                // Check if j is a factor
                if (arr1[i] % j == 0)
                {

                    // check if the factor is present in
                    // second array using the hash
                    if ((hash.Contains(j) && j !=
                        (int) hash.ToArray()[hash.Count- 1]) ||
                        (hash.Contains(arr1[i] / j) && (arr1[i] / j) !=
                        (int) hash.ToArray()[hash.Count - 1]))
                    {
                        count++;
                        break;
                    }
                }
            }
        }

        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr1 = {10, 2, 13, 4, 15};
        int []arr2 = {2, 4, 5, 6};

        int n1 = arr1.Length;
        int n2 = arr2.Length;
        Console.WriteLine(elementCount(arr1, n1, arr2, n2));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of
// elements in first array whose
// atleast one factor is present
// in second array.

// Util function to count the
// elements in first array
// whose atleast one factor is
// present in second array
function elementCount($arr1, $arr2)
{
    // counter to count
    // number of elements
    $count = 0;

    // Hash of second array elements
    $hash = array_unique($arr2);

    // loop to traverse through array
    // elements and check for its factors
    foreach($arr1 as &$x)

        // generate factors of
        // elements of first array
        for ($j = 1; $j < (int)(sqrt($x)) + 1; $j++)

        // Check if j is a factor
        if ($x % $j == 0)
        {

            // check if the factor is present
            // in second array using the hash
            if (in_array($j, $hash) ||
                in_array((int)($x / $j), $hash))
            {
                $count++;
                break;
            }
        }

    return $count;
}

// Driver code
$arr1 = array( 10, 2, 13, 4, 15 );
$arr2 = array( 2, 4, 5, 6 );

print(elementCount($arr1, $arr2));

// This code is contributed mits
?>
```

## java 描述语言

```
<script>
// javascript program to find count of
// elements in first array whose
// atleast one factor is present
// in second array.

    // Util function to count the elements
    // in first array whose atleast
    // one factor is present in second array
    function elementCount(arr1 , n1 , arr2 , n2) {

        // counter to count number of elements
        var count = 0;

        // Hash of second array element
        var hash = new Set();
        for (i = 0; i < n2; i++) {
            hash.add(arr2[i]);
        }

        // loop to traverse through array elements
        // and check for its factors
        for (i = 0; i < n1; i++) {

            // generate factors of elements
            // of first array
            for (j = 1; j * j <= arr1[i]; j++) {

                // Check if j is a factor
                if (arr1[i] % j == 0) {

                    // check if the factor is present in
                    // second array using the hash
                    if ((hash.has(j) && j != parseInt( hash[hash.length - 1])
                            || (hash.has(arr1[i] / j) && (arr1[i] / j) != parseInt( hash[hash.length - 1])))) {
                        count++;
                        break;
                    }
                }
            }
        }

        return count;
    }

    // Driver code

        var arr1 = [ 10, 2, 13, 4, 15 ];
        var arr2 = [ 2, 4, 5, 6 ];

        var n1 = arr1.length;
        var n2 = arr2.length;
        document.write(elementCount(arr1, n1, arr2, n2));

// This code contributed by umadevi9616
</script>
```

**输出** :

```
4
```