# 按递增顺序对偶数和奇数放置的元素进行排序

> 原文:[https://www . geeksforgeeks . org/sort-偶数和奇数-按递增顺序放置元素/](https://www.geeksforgeeks.org/sort-even-and-odd-placed-elements-in-increasing-order/)

给定一个列表 *N* ，任务是将奇数和偶数位置的所有元素按升序排序。排序后，我们需要把所有奇数位置的元素放在一起，然后是所有偶数位置的元素。

**示例:**

```
Input : [3, 2, 7, 6, 8]
Output : 3 7 8 2 6
Explanation: 
Odd position elements in sorted order are 3, 7, 8.
Even position elements in sorted order are 2, 6.

Input : 1 0 2 7 0 0
Output : 0 1 2 0 0 7
Odd {1, 2, 0}
Even {0, 7, 0} 
```

**进场:**

*   初始化两个列表来存储奇数和偶数索引数字。
*   遍历所有数字，将奇数索引数字存储在*奇数索引*列表中，将偶数索引数字存储在*偶数索引*列表中。
*   按排序顺序打印 odd_indexes 列表中的元素。
*   按排序顺序打印偶数索引列表中的元素。

下面是实现:

## C++

```
// C++ implementation of above approach
#include<bits/stdc++.h>
using namespace std;

// function to print the odd and even indexed digits
void odd_even(int arr[], int n)
{

    // lists to store the odd and
    // even positioned digits
    vector<int> odd_indexes;
    vector<int>even_indexes;

    // traverse through all the indexes
    // in the integer
    for (int i = 0; i < n;i++)
    {

        // if the digit is in odd_index position
        // append it to odd_position list
        if (i % 2 == 0)
        odd_indexes.push_back(arr[i]);

        // else append it to the even_position list
        else
        even_indexes.push_back(arr[i]);

    }

    // print the elements in the list in sorted order
    sort(odd_indexes.begin(), odd_indexes.end());
    sort(even_indexes.begin(), even_indexes.end());

    for(int i = 0; i < odd_indexes.size();i++)
        cout << odd_indexes[i] << " ";

    for(int i = 0; i < even_indexes.size(); i++)
        cout << even_indexes[i] << " ";

}

// Driver code
int main()
{
    int arr[] = {3, 2, 7, 6, 8};
    int n = sizeof(arr)/sizeof(arr[0]);
    odd_even(arr, n);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// function to print the odd and even indexed digits
static void odd_even(int arr[], int n)
{

    // lists to store the odd and
    // even positioned digits
    Vector<Integer> odd_indexes = new Vector<Integer>();
    Vector<Integer> even_indexes = new Vector<Integer>();

    // traverse through all the indexes
    // in the integer
    for (int i = 0; i < n;i++)
    {

        // if the digit is in odd_index position
        // append it to odd_position list
        if (i % 2 == 0)
            odd_indexes.add(arr[i]);

        // else append it to the even_position list
        else
            even_indexes.add(arr[i]);

    }

    // print the elements in the list in sorted order
    Collections.sort(odd_indexes);
    Collections.sort(even_indexes);

    for(int i = 0; i < odd_indexes.size(); i++)
        System.out.print(odd_indexes.get(i) + " ");

    for(int i = 0; i < even_indexes.size(); i++)
        System.out.print(even_indexes.get(i) + " ");

}

// Driver code
public static void main(String[] args)
{
    int arr[] = {3, 2, 7, 6, 8};
    int n = arr.length;
    odd_even(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# function to print the odd and even indexed digits
def odd_even(n):

    # lists to store the odd and
    # even positioned digits
    odd_indexes = []
    even_indexes = []

    # traverse through all the indexes
    # in the integer
    for i in range(len(n)):

        # if the digit is in odd_index position
        # append it to odd_position list
        if i % 2 == 0: odd_indexes.append(n[i])

        # else append it to the even_position list
        else: even_indexes.append(n[i])

    # print the elements in the list in sorted order
    for i in sorted(odd_indexes): print(i, end =" ")
    for i in sorted(even_indexes): print(i, end =" ")

# Driver Code
n = [3, 2, 7, 6, 8]
odd_even(n)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// function to print the odd and even indexed digits
static void odd_even(int []arr, int n)
{

    // lists to store the odd and
    // even positioned digits
    List<int> odd_indexes = new List<int>();
    List<int> even_indexes = new List<int>();

    // traverse through all the indexes
    // in the integer
    for (int i = 0; i < n;i++)
    {

        // if the digit is in odd_index position
        // append it to odd_position list
        if (i % 2 == 0)
            odd_indexes.Add(arr[i]);

        // else append it to the even_position list
        else
            even_indexes.Add(arr[i]);

    }

    // print the elements in the list in sorted order
    odd_indexes.Sort();
    even_indexes.Sort();

    for(int i = 0; i < odd_indexes.Count; i++)
        Console.Write(odd_indexes[i] + " ");

    for(int i = 0; i < even_indexes.Count; i++)
        Console.Write(even_indexes[i] + " ");

}

// Driver code
public static void Main(String[] args)
{
    int []arr = {3, 2, 7, 6, 8};
    int n = arr.Length;
    odd_even(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// function to prin the odd and even
// indexed digits
function odd_even($n)
{

    // lists to store the odd and
    // even positioned digits
    $odd_indexes = array();
    $even_indexes = array();

    // traverse through all the indexes
    // in the integer
    for ($i = 0; $i < sizeof($n); $i++)
    {

        // if the digit is in odd_index position
        // append it to odd_position list
        if ($i % 2 == 0)
            array_push($odd_indexes, $n[$i]);

        // else append it to the even_position list
        else
            array_push($even_indexes, $n[$i]);

    }

    // print the elements in the list in sorted order
    sort($odd_indexes);
    for ($i = 0; $i < sizeof($odd_indexes); $i++)
        echo $odd_indexes[$i], " ";

    sort($even_indexes) ;
    for ($i = 0; $i < sizeof($even_indexes); $i++)
        echo $even_indexes[$i], " ";
}

// Driver Code
$n = array(3, 2, 7, 6, 8);
odd_even($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
// function to print the odd and even indexed digits
function odd_even(arr, n)
{

    // lists to store the odd and
    // even positioned digits
    var odd_indexes = [];
    var even_indexes = [];

    // traverse through all the indexes
    // in the integer
    for (var i = 0; i < n;i++)
    {

        // if the digit is in odd_index position
        // append it to odd_position list
        if (i % 2 == 0)
            odd_indexes.push(arr[i]);

        // else append it to the even_position list
        else
            even_indexes.push(arr[i]);

    }

    // print the elements in the list in sorted order
    odd_indexes.sort();
    even_indexes.sort();

    for(var i = 0; i < odd_indexes.length;i++)
        document.write( odd_indexes[i] + " ");

    for(var i = 0; i < even_indexes.length; i++)
        document.write( even_indexes[i] + " ");

}

// Driver code
var arr = [3, 2, 7, 6, 8];
var n = arr.length;
odd_even(arr, n);

</script>
```

**Output:** 

```
3 7 8 2 6
```

**时间复杂度:** O(nlogn)