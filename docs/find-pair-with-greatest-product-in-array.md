# 找到数组中乘积最大的对

> 原文:[https://www . geeksforgeeks . org/find-与阵列中最大产品配对/](https://www.geeksforgeeks.org/find-pair-with-greatest-product-in-array/)

给定一个由 n 个元素组成的数组，任务是找到最大的数，使得它是给定数组的两个元素的乘积。如果不存在这样的元素，打印-1。元素在 1 到 10^5.的范围内
**例:**

```
Input :  arr[] = {10, 3, 5, 30, 35}
Output:  30
Explanation: 30 is the product of 10 and 3.

Input :  arr[] = {2, 5, 7, 8}
Output:  -1
Explanation: Since, no such element exists.

Input :  arr[] = {10, 2, 4, 30, 35}
Output:  -1

Input :  arr[] = {10, 2, 2, 4, 30, 35}
Output:  4

Input  : arr[] = {17, 2, 1, 35, 30}
Output : 35
```

一种简单的方法是选择一个元素，然后检查每对乘积是否等于这个数，如果这个数是最大的，则更新最大值，重复直到整个数组被遍历(花费 O(n^3 时间)。

## C++

```
// C++ program to find a pair with product
// in given array.
#include<bits/stdc++.h>
using namespace std;

// Function to find greatest number that us
int findGreatest( int arr[] , int n)
{
    int result = -1;
    for (int i = 0; i < n ; i++)
        for (int j = 0; j < n-1; j++)
            for (int k = j+1 ; k < n  ; k++)
                if (arr[j] * arr[k] == arr[i])
                    result = max(result, arr[i]);
    return result;
}

// Driver code
int main()
{
    // Your C++ Code
    int arr[] = {30, 10, 9, 3, 35};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << findGreatest(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a pair
// with product in given array.
import java.io.*;

class GFG{

static int findGreatest( int []arr , int n)
{
    int result = -1;
    for (int i = 0; i < n ; i++)
        for (int j = 0; j < n-1; j++)
            for (int k = j+1 ; k < n ; k++)
                if (arr[j] * arr[k] == arr[i])
                    result = Math.max(result, arr[i]);
    return result;
}

    // Driver code
    static public void main (String[] args)
    {
        int []arr = {30, 10, 9, 3, 35};
        int n = arr.length;

        System.out.println(findGreatest(arr, n));
    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find a pair
# with product in given array.

# Function to find greatest number
def findGreatest( arr , n):

    result = -1
    for i in range(n):
        for j in range(n - 1):
            for k in range(j + 1, n):
                if (arr[j] * arr[k] == arr[i]):
                    result = max(result, arr[i])
    return result

# Driver code
if __name__ == "__main__":

    arr = [ 30, 10, 9, 3, 35]
    n = len(arr)

    print(findGreatest(arr, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find a pair with product
// in given array.
using System;

class GFG{

static int findGreatest( int []arr , int n)
{
    int result = -1;
    for (int i = 0; i < n ; i++)
        for (int j = 0; j < n-1; j++)
            for (int k = j+1 ; k < n ; k++)
                if (arr[j] * arr[k] == arr[i])
                    result = Math.Max(result, arr[i]);
    return result;
}

    // Driver code
    static public void Main ()
    {
       int []arr = {30, 10, 9, 3, 35};
       int n = arr.Length;

       Console.WriteLine(findGreatest(arr, n));
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a pair
// with product in given array.

// Function to find
// greatest number
function findGreatest($arr , $n)
{
    $result = -1;
    for ($i = 0; $i < $n ; $i++)
        for ($j = 0; $j < $n - 1; $j++)
            for ($k = $j + 1 ; $k < $n ; $k++)
                if ($arr[$j] * $arr[$k] == $arr[$i])
                    $result = max($result, $arr[$i]);
    return $result;
}

// Driver code
$arr = array(30, 10, 9, 3, 35);
$n = count($arr);

echo findGreatest($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find a pair
// with product in given array.

function findGreatest(arr , n)
{
    let result = -1;
    for (let i = 0; i < n ; i++)
        for (let j = 0; j < n-1; j++)
            for (let k = j+1 ; k < n ; k++)
                if (arr[j] * arr[k] == arr[i])
                    result = Math.max(result, arr[i]);
    return result;
}

// Driver code   

    let arr = [30, 10, 9, 3, 35];
    let n = arr.length;

    document.write(findGreatest(arr, n));

      // This code is contributed by splevel62.

</script>
```

**输出:**

```
30
```

一种**高效的方法**如下实现:-

1.  创建一个空哈希表，并在其中存储所有数组元素。
2.  按升序对数组进行排序。
3.  从数组的末尾一个接一个地挑选元素。
4.  并检查是否存在乘积等于该数的对。在这方面可以达到效率。这个想法是达到这个数字的四分之一。如果在 sqrt 之前我们没有得到这一对，那就意味着不存在这样的一对。我们使用哈希表来确保我们可以在 O(1)时间内找到配对的其他元素。
5.  重复步骤 2 到 3，直到遍历完元素或整个数组。

下面是实现。

## C++

```
// C++ program to find the largest product number
#include <bits/stdc++.h>
using namespace std;

// Function to find greatest number
int findGreatest(int arr[], int n)
{
    // Store occurrences of all elements in hash
    // array
    unordered_map<int, int> m;
    for (int i = 0; i < n; i++)
        m[arr[i]]++;

    // Sort the array and traverse all elements from
    // end.
    sort(arr, arr + n);

    for (int i = n - 1; i > 1; i--) {
        // For every element, check if there is another
        // element which divides it.
        for (int j = 0; j < i && arr[j] <= sqrt(arr[i]);
             j++) {
            if (arr[i] % arr[j] == 0) {
                int result = arr[i] / arr[j];

                // Check if the result value exists in array
                // or not if yes the return arr[i]
                if (result != arr[j] && result!=arr[i] && m[result] > 0)
                    return arr[i];

                // To handle the case like arr[i] = 4 and
                // arr[j] = 2
                else if (result == arr[j] && m[result] > 1)
                    return arr[i];
            }
        }
    }
    return -1;
}

// Drivers code
int main()
{
    int arr[] = { 17, 2, 1, 15, 30 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findGreatest(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest product number
import java.util.*;

class GFG
{

    // Function to find greatest number
    static int findGreatest(int arr[], int n)
    {
        // Store occurrences of all
        // elements in hash array
        Map<Integer, Integer> m = new HashMap<>();
        for (int i = 0; i < n; i++)
        {
            if (m.containsKey(arr[i]))
            {
                m.put(arr[i], m.get(arr[i]) + 1);
            }
            else
            {
                m.put(arr[i], m.get(arr[i]));
            }
        }

        // m[arr[i]]++;
        // Sort the array and traverse
        // all elements from end.
        Arrays.sort(arr);

        for (int i = n - 1; i > 1; i--)
        {
            // For every element, check if there is another
            // element which divides it.
            for (int j = 0; j < i &&
                arr[j] <= Math.sqrt(arr[i]); j++)
            {
                if (arr[i] % arr[j] == 0)
                {
                    int result = arr[i] / arr[j];

                    // Check if the result value exists in array
                    // or not if yes the return arr[i]
                    if (result != arr[j] &&
                        m.get(result) == null|| m.get(result) > 0)
                    {
                        return arr[i];
                    }

                    // To handle the case like arr[i] = 4
                    // and arr[j] = 2
                    else if (result == arr[j] && m.get(result) > 1)
                    {
                        return arr[i];
                    }
                }
            }
        }
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {17, 2, 1, 15, 30};
        int n = arr.length;
        System.out.println(findGreatest(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python3 program to find the largest product number
from math import sqrt

# Function to find greatest number
def findGreatest(arr, n):

    # Store occurrences of all elements in hash
    # array
    m = dict()

    for i in arr:
        m[i] = m.get(i, 0) + 1

    # Sort the array and traverse all elements from
    # end.
    arr=sorted(arr)

    for i in range(n - 1, 0, -1):

        # For every element, check if there is another
        # element which divides it.
        j = 0
        while(j < i and arr[j] <= sqrt(arr[i])):

            if (arr[i] % arr[j] == 0):

                result = arr[i]//arr[j]

                # Check if the result value exists in array
                # or not if yes the return arr[i]
                if (result != arr[j] and (result in m.keys() )and m[result] > 0):
                    return arr[i]

                # To handle the case like arr[i] = 4 and
                # arr[j] = 2
                elif (result == arr[j] and (result in m.keys()) and m[result] > 1):
                    return arr[i]

            j += 1

    return -1

# Drivers code
arr= [17, 2, 1, 15, 30]
n = len(arr)
print(findGreatest(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find the largest product number
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find greatest number
    static int findGreatest(int []arr, int n)
    {
        // Store occurrences of all
        // elements in hash array
        Dictionary<int,int> m = new Dictionary<int,int> ();
        for (int i = 0; i < n; i++)
        {
            if (m.ContainsKey(arr[i]))
            {
                var a = m[arr[i]] + 1;

                // m.Remove(arr[i]);
                m.Add(arr[i], a);
            }
            else
            {
                m.Add(arr[i], arr[i]);
            }
        }

        // m[arr[i]]++;
        // Sort the array and traverse
        // all elements from end.
        Array.Sort(arr);

        for (int i = n - 1; i > 1; i--)
        {
            // For every element, check if there is another
            // element which divides it.
            for (int j = 0; j < i &&
                arr[j] <= Math.Sqrt(arr[i]); j++)
            {
                if (arr[i] % arr[j] == 0)
                {
                    int result = arr[i] / arr[j];

                    // Check if the result value exists in array
                    // or not if yes the return arr[i]
                    if (result != arr[j] &&
                        m[result] == null|| m[result] > 0)
                    {
                        return arr[i];
                    }

                    // To handle the case like arr[i] = 4
                    // and arr[j] = 2
                    else if (result == arr[j] && m[result] > 1)
                    {
                        return arr[i];
                    }
                }
            }
        }
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {17, 2, 1, 15, 30};
        int n = arr.Length;
        Console.WriteLine(findGreatest(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the largest product number

    // Function to find greatest number
    function findGreatest(arr,n)
    {
        // Store occurrences of all
        // elements in hash array
        let m = new Map();
        for (let i = 0; i < n; i++)
        {
            if (m.has(arr[i]))
            {
                m.set(arr[i], m[arr[i]] + 1);
            }
            else
            {
                m.set(arr[i], m.get(arr[i]));
            }
        }

        // m[arr[i]]++;
        // Sort the array and traverse
        // all elements from end.
        arr.sort(function(a,b){return a-b;});

        for (let i = n - 1; i > 1; i--)
        {
            // For every element, check if there is another
            // element which divides it.
            for (let j = 0; j < i &&
                arr[j] <= Math.sqrt(arr[i]); j++)
            {
                if (arr[i] % arr[j] == 0)
                {
                    let result = Math.floor(arr[i] / arr[j]);

                    // Check if the result value exists in array
                    // or not if yes the return arr[i]
                    if (result != arr[j] &&
                        m[result] == null|| m[result] > 0)
                    {
                        return arr[i];
                    }

                    // To handle the case like arr[i] = 4
                    // and arr[j] = 2
                    else if (result == arr[j] && m[result] > 1)
                    {
                        return arr[i];
                    }
                }
            }
        }
        return -1;
    }

    // Driver code
    let arr=[17, 2, 1, 15, 30];
    let n = arr.length;
    document.write(findGreatest(arr, n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
30
```

**时间复杂度:** O(nlogn)
本文由 [**萨哈布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。