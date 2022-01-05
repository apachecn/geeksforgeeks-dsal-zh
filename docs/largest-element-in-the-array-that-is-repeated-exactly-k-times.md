# 数组中重复恰好 k 次的最大元素

> 原文:[https://www . geeksforgeeks . org/数组中最大重复元素精确 k 次/](https://www.geeksforgeeks.org/largest-element-in-the-array-that-is-repeated-exactly-k-times/)

给定一个整数数组和一个整数“k”，任务是从该数组中找到重复恰好“k”次的最大元素。
**例:**

```
Input: arr = {1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6}, k = 2
Output: 5
The elements that exactly occur 2 times are 1, 3 and 5
And, the largest element among them is 5.

Input: arr = {1, 2, 3, 4, 5, 6}, k = 2
Output: No such element
There isn't any element in the array 
that occurs exactly 2 times.
```

**简单的方法:**

*   对数组排序。
*   开始从头到尾遍历数组(因为我们对满足条件的最大元素感兴趣)，并通过将元素与其相邻元素进行比较来计算每个元素的频率。
*   右边第一个恰好出现 k 次的元素就是答案。
*   如果没有找到恰好出现“k”次的元素，则打印“没有这样的元素”。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the largest
// element which is repeated 'k' times
void solve(int arr[], int n, int k)
{
    // sort the array
    sort(arr, arr + n);

    // if the value of 'k' is 1 and the
    // largest appears only once in the array
    if (k == 1 && arr[n - 2] != arr[n - 1]) {
        cout << arr[n - 1] << endl;
        return;
    }

    // counter  to count
    // the repeated elements
    int count = 1;

    for (int i = n - 2; i >= 0; i--) {

        // check if the element at index 'i'
        // is equal to the element at index 'i+1'
        // then increase the count
        if (arr[i] == arr[i + 1])
            count++;

        // else set the count to 1
        // to start counting the frequency
        // of the new number
        else
            count = 1;

        // if the count is equal to k
        // and the previous element
        // is not equal to this element
        if (count == k && (i == 0 || (arr[i - 1] != arr[i]))) {
            cout << arr[i] << endl;
            return;
        }
    }

    // if there is no such element
    cout << "No such element" << endl;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 };
    int k = 2;
    int n = sizeof(arr) / sizeof(int);

    // find the largest element
    // that is repeated K times
    solve(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.Arrays ;

public class GFG {

    // Function that finds the largest
    // element which is repeated 'k' times
    static void solve(int arr[], int n, int k)
    {
        // sort the array
        Arrays.sort(arr);

        // if the value of 'k' is 1 and the
        // largest appears only once in the array
        if (k == 1 && arr[n - 2] != arr[n - 1]) {
            System.out.println(arr[n - 1]);
            return;
        }

        // counter  to count
        // the repeated elements
        int count = 1;

        for (int i = n - 2; i >= 0; i--) {

            // check if the element at index 'i'
            // is equal to the element at index 'i+1'
            // then increase the count
            if (arr[i] == arr[i + 1])
                count++;

            // else set the count to 1
            // to start counting the frequency
            // of the new number
            else
                count = 1;

            // if the count is equal to k
            // and the previous element
            // is not equal to this element
            if (count == k && (i == 0 || (arr[i - 1] != arr[i]))) {
                System.out.println(arr[i]);
                return;
            }
        }

        // if there is no such element
        System.out.println("No such element");
    }

    // Driver code
    public static void main(String args[])
    {
              int arr[] = { 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 };
            int k = 2;
            int n = arr.length;

            // find the largest element
            // that is repeated K times
            solve(arr, n, k);

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that finds the largest
# element which is repeated 'k' times
def solve(arr, n, k):

    # sort the array
    arr.sort()

    # if the value of 'k' is 1 and the
    # largest appears only once in the array
    if (k == 1 and arr[n - 2] != arr[n - 1]):
        print( arr[n - 1] )
        return

    # counter to count
    # the repeated elements
    count = 1

    for i in range(n - 2, -1, -1) :

        # check if the element at index 'i'
        # is equal to the element at index 'i+1'
        # then increase the count
        if (arr[i] == arr[i + 1]):
            count += 1

        # else set the count to 1
        # to start counting the frequency
        # of the new number
        else:
            count = 1

        # if the count is equal to k
        # and the previous element
        # is not equal to this element
        if (count == k and (i == 0 or
           (arr[i - 1] != arr[i]))):
            print(arr[i])
            return

    # if there is no such element
    print("No such element")

# Driver code
if __name__ == "__main__":

    arr = [ 1, 1, 2, 3, 3, 4,
            5, 5, 6, 6, 6 ]
    k = 2
    n = len(arr)

    # find the largest element
    # that is repeated K times
    solve(arr, n, k)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function that finds the largest
// element which is repeated 'k' times
static void solve(int []arr, int n, int k)
{
    // sort the array
    Array.Sort(arr);

    // if the value of 'k' is 1 and the
    // largest appears only once in the array
    if (k == 1 && arr[n - 2] != arr[n - 1])
    {
        Console.WriteLine(arr[n - 1]);
        return;
    }

    // counter to count
    // the repeated elements
    int count = 1;

    for (int i = n - 2; i >= 0; i--)
    {

        // check if the element at index 'i'
        // is equal to the element at index 'i+1'
        // then increase the count
        if (arr[i] == arr[i + 1])
            count++;

        // else set the count to 1
        // to start counting the frequency
        // of the new number
        else
            count = 1;

        // if the count is equal to k
        // and the previous element
        // is not equal to this element
        if (count == k && (i == 0 ||
           (arr[i - 1] != arr[i])))
        {
            Console.WriteLine(arr[i]);
            return;
        }
    }

    // if there is no such element
    Console.WriteLine("No such element");
}

// Driver code
static public void Main ()
{
    int []arr = { 1, 1, 2, 3, 3, 4,
                  5, 5, 6, 6, 6 };
    int k = 2;
    int n = arr.Length;

    // find the largest element
    // that is repeated K times
    solve(arr, n, k);
}
}

// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that finds the largest
// element which is repeated 'k' times
function solve(&$arr, $n, $k)
{
    // sort the array
    sort($arr);

    // if the value of 'k' is 1 and the
    // largest appears only once in the array
    if ($k == 1 && $arr[$n - 2] != $arr[$n - 1])
    {
        echo $arr[$n - 1] ;
        echo ("\n");
        return;
    }

    // counter to count
    // the repeated elements
    $count = 1;

    for ($i = $n - 2; $i >= 0; $i--)
    {

        // check if the element at index 'i'
        // is equal to the element at index 'i+1'
        // then increase the count
        if ($arr[$i] == $arr[$i + 1])
            $count++;

        // else set the count to 1
        // to start counting the frequency
        // of the new number
        else
            $count = 1;

        // if the count is equal to k
        // and the previous element
        // is not equal to this element
        if ($count == $k && ($i == 0 ||
           ($arr[$i - 1] != $arr[$i])))
        {
            echo ($arr[$i]);
            echo ("\n");
            return;
        }
    }

    // if there is no such element
    echo ("No such element");
    echo ("\n");
}

// Driver code
$arr = array(1, 1, 2, 3, 3, 4,
             5, 5, 6, 6, 6 );
$k = 2;
$n = sizeof($arr);

// find the largest element
// that is repeated K times
solve($arr, $n, $k);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that finds the largest
// element which is repeated 'k' times
function solve(arr, n, k)
{
    // sort the array
    arr.sort((a,b)=> a-b)

    // if the value of 'k' is 1 and the
    // largest appears only once in the array
    if (k == 1 && arr[n - 2] != arr[n - 1]) {
        cout << arr[n - 1] << endl;
        return;
    }

    // counter  to count
    // the repeated elements
    var count = 1;

    for (var i = n - 2; i >= 0; i--) {

        // check if the element at index 'i'
        // is equal to the element at index 'i+1'
        // then increase the count
        if (arr[i] == arr[i + 1])
            count++;

        // else set the count to 1
        // to start counting the frequency
        // of the new number
        else
            count = 1;

        // if the count is equal to k
        // and the previous element
        // is not equal to this element
        if (count == k && (i == 0 || (arr[i - 1] != arr[i]))) {
            document.write( arr[i] + "<br>");
            return;
        }
    }

    // if there is no such element
    document.write( "No such element" );
}

// Driver code
var arr = [ 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 ];
var k = 2;
var n = arr.length;
// find the largest element
// that is repeated K times
solve(arr, n, k);

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N*log(N))
**高效进场:**

*   创建一个地图，并存储地图中每个元素的频率。
*   然后，遍历数组，找出频率等于“k”的最大元素。
*   如果找到，打印号码
*   否则，打印“无此元素”。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the largest
// element that occurs exactly 'k' times
void solve(int arr[], int n, int k)
{
    // store the frequency
    // of each element
    unordered_map<int, int> m;
    for (int i = 0; i < n; i++) {
        m[arr[i]]++;
    }

    // to store the maximum element
    int max = INT_MIN;

    for (int i = 0; i < n; i++) {

        // if current element has frequency 'k'
        // and current maximum hasn't been set
        if (m[arr[i]] == k && max == INT_MIN) {

            // set the current maximum
            max = arr[i];
        }

        // if current element has
        // frequency 'k' and it is
        // greater than the current maximum
        else if (m[arr[i]] == k && max < arr[i]) {

            // change the current maximum
            max = arr[i];
        }
    }

    // if there is no element
    // with frequency 'k'
    if (max == INT_MIN)
        cout << "No such element" << endl;

    // print the largest element
    // with frequency 'k'
    else
        cout << max << endl;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 };
    int k = 4;
    int n = sizeof(arr) / sizeof(int);

    // find the largest element
    // that is repeated K times
    solve(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.HashMap;
import java.util.Map;

class GfG
{

    // Function that finds the largest
    // element that occurs exactly 'k' times
    static void solve(int arr[], int n, int k)
    {
        // store the frequency of each element
        HashMap<Integer, Integer> m = new HashMap<>();
        for (int i = 0; i < n; i++)
        {
            if (!m.containsKey(arr[i]))
                m.put(arr[i], 0);
            m.put(arr[i], m.get(arr[i]) + 1);
        }

        // to store the maximum element
        int max = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++)
        {

            // If current element has frequency 'k'
            // and current maximum hasn't been set
            if (m.get(arr[i]) == k && max == Integer.MIN_VALUE)
            {

                // set the current maximum
                max = arr[i];
            }

            // if current element has
            // frequency 'k' and it is
            // greater than the current maximum
            else if (m.get(arr[i]) == k && max < arr[i])
            {

                // change the current maximum
                max = arr[i];
            }
        }

        // if there is no element
        // with frequency 'k'
        if (max == Integer.MIN_VALUE)
            System.out.println("No such element");

        // print the largest element
        // with frequency 'k'
        else
            System.out.println(max);
    }

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 };
        int k = 4;
        int n = arr.length;

        // find the largest element
        // that is repeated K times
        solve(arr, n, k);
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python implementation of above approach
import sys

# Function that finds the largest
# element that occurs exactly 'k' times
def solve(arr, n, k):

    # store the frequency
    # of each element
    m = {};

    for i in range(0, n - 1):
        if(arr[i] in m.keys()):
            m[arr[i]] += 1;
        else:
            m[arr[i]] = 1;
        i += 1;

    # to store the maximum element
    max = sys.maxsize;

    for i in range(0, n - 1):

        # if current element has frequency 'k'
        # and current maximum hasn't been set
        if (m[arr[i]] == k and
            max == sys.maxsize):

            # set the current maximum
            max = arr[i];

        # if current element has
        # frequency 'k' and it is
        # greater than the current maximum
        elif (m[arr[i]] == k and max < arr[i]):

            # change the current maximum
            max = arr[i];
        i += 1

    # if there is no element
    # with frequency 'k'
    if (max == sys.maxsize):
        print("No such element");

    # print the largest element
    # with frequency 'k'
    else:
        print(max);

# Driver code
arr = [ 1, 1, 2, 3, 3, 4,
           5, 5, 6, 6, 6 ]
k = 4;
n = len(arr)

# find the largest element
# that is repeated K times
solve(arr, n, k)

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# Implementation of the above approach
using System;
using System.Collections.Generic;

class GfG
{

    // Function that finds the largest
    // element that occurs exactly 'k' times
    static void solve(int []arr, int n, int k)
    {
        // store the frequency of each element
        Dictionary<int,int> m = new Dictionary<int,int>();
        for (int i = 0 ; i < n; i++)
        {
            if(m.ContainsKey(arr[i]))
            {
                var val = m[arr[i]];
                m.Remove(arr[i]);
                m.Add(arr[i], val + 1);
            }
            else
            {
                m.Add(arr[i], 1);
            }
        }

        // to store the maximum element
        int max = int.MinValue;

        for (int i = 0; i < n; i++)
        {

            // If current element has frequency 'k'
            // and current maximum hasn't been set
            if (m[arr[i]] == k && max ==int.MinValue)
            {

                // set the current maximum
                max = arr[i];
            }

            // if current element has
            // frequency 'k' and it is
            // greater than the current maximum
            else if (m[arr[i]] == k && max < arr[i])
            {

                // change the current maximum
                max = arr[i];
            }
        }

        // if there is no element
        // with frequency 'k'
        if (max == int.MinValue)
            Console.WriteLine("No such element");

        // print the largest element
        // with frequency 'k'
        else
            Console.WriteLine(max);
    }

    // Driver code
    public static void Main(String []args)
    {

        int []arr = { 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 };
        int k = 4;
        int n = arr.Length;

        // find the largest element
        // that is repeated K times
        solve(arr, n, k);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that finds the largest
// element that occurs exactly 'k' times
function solve(arr, n, k)
{
    // store the frequency
    // of each element
    var m = new Map();
    for (var i = 0; i < n; i++) {
        m.set(arr[i], m.get(arr[i])+1);
    }

    // to store the maximum element
    var max = -1000000000;

    for (var i = 0; i < n; i++) {

        // if current element has frequency 'k'
        // and current maximum hasn't been set
        if (m.get(arr[i]) == k && max == -1000000000) {

            // set the current maximum
            max = arr[i];
        }

        // if current element has
        // frequency 'k' and it is
        // greater than the current maximum
        else if (m.get(arr[i]) == k && max < arr[i]) {

            // change the current maximum
            max = arr[i];
        }
    }

    // if there is no element
    // with frequency 'k'
    if (max == -1000000000)
        document.write( "No such element");

    // print the largest element
    // with frequency 'k'
    else
        document.write( max);
}

// Driver code
var arr = [ 1, 1, 2, 3, 3, 4, 5, 5, 6, 6, 6 ];
var k = 4;
var n = arr.length;
// find the largest element
// that is repeated K times
solve(arr, n, k);

</script>
```

**Output:** 

```
No such element
```

**时间复杂度:** O(N)