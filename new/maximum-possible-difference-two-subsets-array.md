# 数组

> 原文：[https://www.geeksforgeeks.org/maximum-possible-difference-two-subsets-array/](https://www.geeksforgeeks.org/maximum-possible-difference-two-subsets-array/)

的两个子集的最大可能差

给定一个 n 整数数组。 该数组可以包含重复元素，但是任何元素的最高频率不得超过两个。 您必须制作两个子集，以使它们的元素之和的差最大，并且它们两个共同包含给定数组的所有元素以及最重要的条件，任何子集都不应包含重复元素。

**范例**：

```
Input : arr[] = {5, 8, -1, 4}
Output : Maximum Difference = 18
Explanation : 
Let Subset A = {5, 8, 4} & Subset B = {-1}
Sum of elements of subset A = 17, of subset B = -1
Difference of Sum of Both subsets = 17 - (-1) = 18

Input : arr[] = {5, 8, 5, 4}
Output : Maximum Difference = 12
Explanation : 
Let Subset A = {5, 8, 4} & Subset B = {5}
Sum of elements of subset A = 17, of subset B = 5
Difference of Sum of Both subsets = 17 - 5 = 12

```

在解决这个问题之前，我们必须照顾一些给定的条件，它们被列为：

*   在构建子集时，请注意任何子集都不应包含重复元素。 因此，我们可以得出结论，所有这些频率为 2 的元素将成为两个子集的一部分，因此总的来说，它们对子集和的差值没有任何影响。 因此，我们可以轻松地忽略它们。

*   为了使两个子集的元素之和的差最大，我们必须以所有正元素都属于一个子集而负元素属于其他子集的方式来使子集。

**时间复杂度为 O（n <sup>2</sup> ）的算法**：

```
for i=0 to n-1
    isSingleOccurance = true;
    for  j= i+1 to n-1

        // if frequency of any element is two
        // make both equal to zero
        if arr[i] equals arr[j]
            arr[i] = arr[j] = 0
            isSingleOccurance = false;
            break;

    if isSingleOccurance == true
        if (arr[i] > 0)
            SubsetSum_1 += arr[i];
        else 
            SubsetSum_2 += arr[i];
return abs(SubsetSum_1 - SubsetSum2)            

```

## C++

```cpp

// CPP find maximum difference of subset sum
#include <bits/stdc++.h>
using namespace std;

// function for maximum subset diff
int maxDiff(int arr[], int n)
{
    int SubsetSum_1 = 0, SubsetSum_2 = 0;
    for (int i = 0; i <= n - 1; i++) {

        bool isSingleOccurance = true;
        for (int j = i + 1; j <= n - 1; j++) {

            // if frequency of any element is two
            // make both equal to zero
            if (arr[i] == arr[j]) {
                isSingleOccurance = false;
                arr[i] = arr[j] = 0;
                break;
            }
        }
        if (isSingleOccurance) {
            if (arr[i] > 0)
                SubsetSum_1 += arr[i];
            else
                SubsetSum_2 += arr[i];
        }
    }
    return abs(SubsetSum_1 - SubsetSum_2);
}

// driver program
int main()
{
    int arr[] = { 4, 2, -3, 3, -2, -2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Difference = " << maxDiff(arr, n);
    return 0;
}

```

## Java

```java

// java find maximum difference
// of subset sum
import java .io.*;

public class GFG {

    // function for maximum subset diff
    static int maxDiff(int []arr, int n)
    {
        int SubsetSum_1 = 0, SubsetSum_2 = 0;
        for (int i = 0; i <= n - 1; i++)
        {
            boolean isSingleOccurance = true;
            for (int j = i + 1; j <= n - 1; j++)
            {

                // if frequency of any element
                // is two make both equal to
                // zero
                if (arr[i] == arr[j])
                {
                    isSingleOccurance = false;
                    arr[i] = arr[j] = 0;
                    break;
                }
            }
            if (isSingleOccurance)
            {
                if (arr[i] > 0)
                    SubsetSum_1 += arr[i];
                else
                    SubsetSum_2 += arr[i];
            }
        }

        return Math.abs(SubsetSum_1 - SubsetSum_2);
    }

    // driver program
    static public void main (String[] args)
    {
        int []arr = { 4, 2, -3, 3, -2, -2, 8 };
        int n = arr.length;

        System.out.println("Maximum Difference = "
                               + maxDiff(arr, n));
    }
}

// This code is contributed by vt_m.

```

## Python3

```py

# Python3 find maximum difference
# of subset sum

import math

# function for maximum subset diff
def maxDiff(arr, n) :
    SubsetSum_1 = 0
    SubsetSum_2 = 0
    for i in range(0, n) :

        isSingleOccurance = True
        for j in range(i + 1, n) :

            # if frequency of any element
            # is two make both equal to 
            # zero
            if (arr[i] == arr[j]) : 
                isSingleOccurance = False
                arr[i] = arr[j] = 0
                break

        if (isSingleOccurance == True) :
            if (arr[i] > 0) :
                SubsetSum_1 += arr[i]
            else :
                SubsetSum_2 += arr[i]

    return abs(SubsetSum_1 - SubsetSum_2)

# Driver Code
arr = [4, 2, -3, 3, -2, -2, 8]
n = len(arr)
print ("Maximum Difference = {}"
               . format(maxDiff(arr, n)))

# This code is contributed by Manish Shaw
# (manishshaw1)

```

## C#

```cs

// C# find maximum difference of
// subset sum
using System;

public class GFG {

    // function for maximum subset diff
    static int maxDiff(int []arr, int n)
    {
        int SubsetSum_1 = 0, SubsetSum_2 = 0;
        for (int i = 0; i <= n - 1; i++)
        {

            bool isSingleOccurance = true;
            for (int j = i + 1; j <= n - 1; j++)
            {

                // if frequency of any element
                // is two make both equal to
                // zero
                if (arr[i] == arr[j])
                {
                    isSingleOccurance = false;
                    arr[i] = arr[j] = 0;
                    break;
                }
            }
            if (isSingleOccurance)
            {
                if (arr[i] > 0)
                    SubsetSum_1 += arr[i];
                else
                    SubsetSum_2 += arr[i];
            }
        }

        return Math.Abs(SubsetSum_1 - SubsetSum_2);
    }

    // driver program
    static public void Main ()
    {
        int []arr = { 4, 2, -3, 3, -2, -2, 8 };
        int n = arr.Length;

        Console.WriteLine("Maximum Difference = "
                              + maxDiff(arr, n));
    }
}

// This code is contributed by vt_m.

```

## PHP

```php

<?php
// PHP find maximum difference
// of subset sum

// function for maximum subset diff
function maxDiff($arr, $n)
{
    $SubsetSum_1 = 0;
    $SubsetSum_2 = 0;
    for ($i = 0; $i <= $n - 1; $i++)
    {

        $isSingleOccurance = true;
        for ($j = $i + 1; $j <= $n - 1; $j++)
        {

            // if frequency of any element is two
            // make both equal to zero
            if ($arr[$i] == $arr[$j]) 
            {
                $isSingleOccurance = false;
                $arr[$i] = $arr[$j] = 0;
                break;
            }
        }
        if ($isSingleOccurance) 
        {
            if ($arr[$i] > 0)
                $SubsetSum_1 += $arr[$i];
            else
                $SubsetSum_2 += $arr[$i];
        }
    }
    return abs($SubsetSum_1 - $SubsetSum_2);
}

    // Driver Code
    $arr = array(4, 2, -3, 3, -2, -2, 8);
    $n = sizeof($arr);
    echo "Maximum Difference = " , maxDiff($arr, $n);

// This code is contributed by nitin mittal
?>

```

**Output:** 

```
Maximum Difference = 20

```

**时间复杂度为 O（n log n）的算法**：

```
-> sort the array
-> for i =0 to n-2
      // consecutive two elements are not equal
      // add absolute arr[i] to result
      if arr[i] != arr[i+1]
          result += abs(arr[i])
      // else skip next element too
      else
          i++;

// special check for last two elements
-> if (arr[n-2] != arr[n-1])
    result += arr[n-1]

-> return result;           

```

## C++

```cpp

// CPP find maximum difference of subset sum
#include <bits/stdc++.h>
using namespace std;

// function for maximum subset diff
int maxDiff(int arr[], int n)
{
    int result = 0;

    // sort the array
    sort(arr, arr + n);

    // calculate the result
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] != arr[i + 1])
            result += abs(arr[i]);
        else
            i++;
    }

    // check for last element
    if (arr[n - 2] != arr[n - 1])
        result += abs(arr[n - 1]);

    // return result
    return result;
}

// driver program
int main()
{
    int arr[] = { 4, 2, -3, 3, -2, -2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Difference = " << maxDiff(arr, n);
    return 0;
}

```

## Java

```java

// java find maximum difference of
// subset sum
import java. io.*;
import java .util.*;

public class GFG {

    // function for maximum subset diff
    static int maxDiff(int []arr, int n)
    {
        int result = 0;

        // sort the array
        Arrays.sort(arr);

        // calculate the result
        for (int i = 0; i < n - 1; i++)
        {
            if (arr[i] != arr[i + 1])
                result += Math.abs(arr[i]);
            else
                i++;
        }

        // check for last element
        if (arr[n - 2] != arr[n - 1])
            result += Math.abs(arr[n - 1]);

        // return result
        return result;
    }

    // driver program
    static public void main (String[] args)
    {
        int[] arr = { 4, 2, -3, 3, -2, -2, 8 };
        int n = arr.length;

        System.out.println("Maximum Difference = "
                                + maxDiff(arr, n));
    }
}

// This code is contributed by vt_m.

```

## Python 3

```

# Python 3 find maximum difference 
# of subset sum

# function for maximum subset diff
def maxDiff(arr, n):

    result = 0

    # sort the array
    arr.sort()

    # calculate the result
    for i in range(n - 1):
        if (abs(arr[i]) != abs(arr[i + 1])):
            result += abs(arr[i])

        else:
            pass

    # check for last element
    if (arr[n - 2] != arr[n - 1]):
        result += abs(arr[n - 1])

    # return result
    return result

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 2, -3, 3, -2, -2, 8 ]
    n = len(arr)
    print("Maximum Difference = " ,
                   maxDiff(arr, n))

# This code is contributed by ita_c

```c

## C#

```cs

// C# find maximum difference
// of subset sum
using System;

public class GFG {

    // function for maximum subset diff
    static int maxDiff(int []arr, int n)
    {
        int result = 0;

        // sort the array
        Array.Sort(arr);

        // calculate the result
        for (int i = 0; i < n - 1; i++)
        {
            if (arr[i] != arr[i + 1])
                result += Math.Abs(arr[i]);
            else
                i++;
        }

        // check for last element
        if (arr[n - 2] != arr[n - 1])
            result += Math.Abs(arr[n - 1]);

        // return result
        return result;
    }

    // driver program
    static public void Main ()
    {
        int[] arr = { 4, 2, -3, 3, -2, -2, 8 };
        int n = arr.Length;

        Console.WriteLine("Maximum Difference = "
                              + maxDiff(arr, n));
    }
}

// This code is contributed by vt_m.

```

## PHP

```php

<?php
// PHP find maximum difference of subset sum

// function for maximum subset diff
function maxDiff( $arr, $n)
{
    $result = 0;

    // sort the array
    sort($arr);

    // calculate the result
    for ( $i = 0; $i < $n - 1; $i++) 
    {
        if ($arr[$i] != $arr[$i + 1])
            $result += abs($arr[$i]);
        else
            $i++;
    }

    // check for last element
    if ($arr[$n - 2] != $arr[$n - 1])
        $result += abs($arr[$n - 1]);

    // return result
    return $result;
}

    // Driver Code
    $arr = array( 4, 2, -3, 3, -2, -2, 8 );
    $n = count($arr);
    echo "Maximum Difference = "
        , maxDiff($arr, $n);

// This code is contributed by anuj_67.
?>

```

**Output:** 

```
Maximum Difference = 20

```

时间复杂度为`O(n)`的算法：

```
make hash table for positive elements:
    for all positive elements(arr[i])
        if frequency == 1
            SubsetSum_1 += arr[i];
make hash table for negative elements:
    for all negative elements
        if frequency == 1
            SubsetSum_2 += arr[i];
return abs(SubsetSum_1 - SubsetSum2)            

```

## C++

```cpp

// CPP find maximum difference of subset sum
#include <bits/stdc++.h>
using namespace std;

// function for maximum subset diff
int maxDiff(int arr[], int n)
{
    unordered_map<int, int> hashPositive;
    unordered_map<int, int> hashNegative;

    int SubsetSum_1 = 0, SubsetSum_2 = 0;

    // construct hash for positive elements
    for (int i = 0; i <= n - 1; i++)
        if (arr[i] > 0)
            hashPositive[arr[i]]++;

    // calculate subset sum for positive elements
    for (int i = 0; i <= n - 1; i++)
        if (arr[i] > 0 && hashPositive[arr[i]] == 1)
            SubsetSum_1 += arr[i];

    // construct hash for negative elements
    for (int i = 0; i <= n - 1; i++)
        if (arr[i] < 0)
            hashNegative[abs(arr[i])]++;

    // calculate subset sum for negative elements
    for (int i = 0; i <= n - 1; i++)
        if (arr[i] < 0 && 
            hashNegative[abs(arr[i])] == 1)
            SubsetSum_2 += arr[i];

    return abs(SubsetSum_1 - SubsetSum_2);
}

// driver program
int main()
{
    int arr[] = { 4, 2, -3, 3, -2, -2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Difference = " << maxDiff(arr, n);
    return 0;
}

```

## Java

```java

// Java find maximum 
// difference of subset sum 
import java.util.*;
class GFG{

// Function for maximum subset diff 
public static int maxDiff(int arr[], 
                          int n) 
{ 
  HashMap<Integer, 
          Integer> hashPositive = new HashMap<>();
  HashMap<Integer, 
          Integer> hashNegative = new HashMap<>(); 

  int SubsetSum_1 = 0, 
      SubsetSum_2 = 0; 

  // Construct hash for 
  // positive elements 
  for (int i = 0; i <= n - 1; i++) 
  {
    if (arr[i] > 0) 
    {
      if(hashPositive.containsKey(arr[i]))
      {
        hashPositive.replace(arr[i], 
        hashPositive.get(arr[i]) + 1);
      }
      else
      {
        hashPositive.put(arr[i], 1);
      }
    }
  }

  // Calculate subset sum 
  // for positive elements 
  for (int i = 0; i <= n - 1; i++) 
  {
    if(arr[i] > 0 && 
       hashPositive.containsKey(arr[i]))
    {
      if(hashPositive.get(arr[i]) == 1)
      {
        SubsetSum_1 += arr[i];
      }
    }
  }

  // Construct hash for 
  // negative elements 
  for (int i = 0; i <= n - 1; i++) 
  {
    if (arr[i] < 0)
    {
      if(hashNegative.containsKey(Math.abs(arr[i])))
      {
        hashNegative.replace(Math.abs(arr[i]), 
        hashNegative.get(Math.abs(arr[i])) + 1);
      }
      else
      {
        hashNegative.put(Math.abs(arr[i]), 1);
      }
    }
  }

  // Calculate subset sum for
  // negative elements 
  for (int i = 0; i <= n - 1; i++) 
  {
    if (arr[i] < 0 && 
        hashNegative.containsKey(Math.abs(arr[i])))
    {
      if(hashNegative.get(Math.abs(arr[i])) == 1)
      {
        SubsetSum_2 += arr[i]; 
      }
    }
  }

  return Math.abs(SubsetSum_1 - SubsetSum_2); 
} 

// Driver code
public static void main(String[] args) 
{
  int arr[] = {4, 2, -3, 3, 
               -2, -2, 8}; 
  int n = arr.length;
  System.out.print("Maximum Difference = " + 
                    maxDiff(arr, n));
}
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```py

# Python3 find maximum difference of subset sum

# function for maximum subset diff
def maxDiff(arr, n):

    hashPositive = dict()
    hashNegative = dict()

    SubsetSum_1, SubsetSum_2 = 0, 0

    # construct hash for positive elements
    for i in range(n):
        if (arr[i] > 0):
            hashPositive[arr[i]] = \
                hashPositive.get(arr[i], 0) + 1

    # calculate subset sum for positive elements
    for i in range(n):
        if (arr[i] > 0 and arr[i] in
            hashPositive.keys() and
            hashPositive[arr[i]] == 1):
            SubsetSum_1 += arr[i]

    # construct hash for negative elements
    for i in range(n):
        if (arr[i] < 0):
            hashNegative[abs(arr[i])] = \
                hashNegative.get(abs(arr[i]), 0) + 1

    # calculate subset sum for negative elements
    for i in range(n):
        if (arr[i] < 0 and abs(arr[i]) in
            hashNegative.keys() and
            hashNegative[abs(arr[i])] == 1):
            SubsetSum_2 += arr[i]

    return abs(SubsetSum_1 - SubsetSum_2)

# Driver Code
arr = [4, 2, -3, 3, -2, -2, 8]
n = len(arr)
print("Maximum Difference =", maxDiff(arr, n))

# This code is contributed by mohit kumar

```

**Output:** 

```
Maximum Difference = 20

```



* * *

* * *



