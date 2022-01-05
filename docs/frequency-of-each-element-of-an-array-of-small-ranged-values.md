# 小范围值数组中每个元素的频率

> 原文:[https://www . geeksforgeeks . org/小范围值数组中每个元素的频率/](https://www.geeksforgeeks.org/frequency-of-each-element-of-an-array-of-small-ranged-values/)

给定一个数组，其中小范围内的元素。数组中的最大元素不超过数组的大小。找出元素的频率。
**例:**

```
Input : arr[] = {3, 1, 2, 3, 4, 5, 4}
Output: 1-->1
        2-->1
        3-->2
        4-->2
        5-->1

Input : arr[] = {1, 2, 2, 1, 2}
Output: 1-->2
        2-->3

Input : arr[] = {1, 2, 4}
Output: 1-->1
        2-->1
        4-->1
```

一个**简单的解决方案**是使用两个嵌套循环。对于每个元素(从 1 到 n，其中 n 是数组的大小)，计算它出现的次数。这个解的时间复杂度是 O(n*n)
A **更好的解**是用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。首先对数组进行排序，排序后，线性遍历数组并计算每个元素的出现次数。这个解决方案的时间复杂度是 O(n Log n)
一个**高效的解决方案**是使用哈希。我们在散列表中插入每个元素，并增加频率。这个解的时间复杂度是 O(n)。具体实施见[竞争性编程测频技术](https://www.geeksforgeeks.org/frequency-measurement-techniques-for-competitive-programming/)。
**有限范围的高效解决方案**
基于哈希的解决方案速度很快，但需要哈希函数计算等。如果我们知道范围很小，我们使用[直接地址表](https://www.geeksforgeeks.org/direct-address-table/)，在这里我们创建一个大小等于最大值的数组，并使用数组元素作为索引。
以上解释执行如下:

## C++

```
// CPP program to find frequencies of elements in
// limited range array.
#include <bits/stdc++.h>
using namespace std;

void frequencyOfEach(int* arr, int n)
{
    // finding maximum element in array
    int max = *max_element(arr, arr + n);

    // make hash array of size equal to maximum
    // element in array
    int hash[max + 1] = { 0 };

    /* Counting frequency of each element of array
       and storing it in hash*/
    for (int i = 0; i < n; i++) {
        hash[arr[i]]++;
    }

    // printing frequency of elements
    for (int i = 0; i <= max; i++) {

        /* If hash[i] has stored any value
           i.e element has occurred atleast
           once in array */
        if (hash[i] != 0)
            cout << i << "-->" << hash[i] << "\n";
    }
}

int main()
{
    int arr[] = { 5, 2, 2, 3, 5, 1, 1, 5, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    frequencyOfEach(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find frequencies of elements in
// limited range array.
import java.util.*;

class solution
{

static void frequencyOfEach(int []arr, int n)
{
    int max = Integer.MIN_VALUE;
    // finding maximum element in array
    for (int i = 0;i<n;i++)
{
    if (arr[i]>max)
        max = arr[i];
}

    // make hash array of size equal to maximum
    // element in array
    int []hash = new int[max + 1];
    Arrays.fill(hash,0);

    /* Counting frequency of each element of array
    and storing it in hash*/
    for (int i = 0; i < n; i++) {
        hash[arr[i]]++;
    }

    // printing frequency of elements
    for (int i = 0; i <= max; i++) {

        /* If hash[i] has stored any value
        i.e element has occurred atleast
        once in array */
        if (hash[i] != 0)
            System.out.println(i+"-->"+hash[i]);
    }
}

public static void main(String args[])
{
    int []arr = { 5, 2, 2, 3, 5, 1, 1, 5, 3, 4 };
    int n = arr.length;
    frequencyOfEach(arr, n);

}
}
//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 program to find frequencies
# of elements in limited range array.
def frequencyOfEach(arr, n) :

    # finding maximum element in array
    max_element = max(arr)

    # make hash array of size equal
    # to maximum element in array
    hash = [0] * (max_element + 1)

    # Counting frequency of each element
    # of array and storing it in hash
    for i in range(n) :
        hash[arr[i]] += 1

    # printing frequency of elements
    for i in range(max_element + 1) :

        # If hash[i] has stored any value
        # i.e element has occurred atleast
        # once in array
        if (hash[i] != 0) :
            print(i, "-->", hash[i])

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, 2, 2, 3, 5,
            1, 1, 5, 3, 4 ]
    n = len(arr)
    frequencyOfEach(arr, n);

# This code is contributed by Ryuga
```

## C#

```
// C# program to find frequencies of elements in
// limited range array.
using System;

public class solution{

    static void frequencyOfEach(int []arr, int n)
    {
        int max = int.MinValue;
        // finding maximum element in array
        for (int i = 0;i<n;i++)
    {
        if (arr[i]>max)
            max = arr[i];
    }

        // make hash array of size equal to maximum
        // element in array
        int []hash = new int[max + 1];

        /* Counting frequency of each element of array
        and storing it in hash*/
        for (int i = 0; i < n; i++) {
            hash[arr[i]]++;
        }

        // printing frequency of elements
        for (int i = 0; i <= max; i++) {

            /* If hash[i] has stored any value
            i.e element has occurred atleast
            once in array */
            if (hash[i] != 0)
                Console.WriteLine (i+"-->"+hash[i]);
        }
    }

    public static void Main()
    {
        int []arr = { 5, 2, 2, 3, 5, 1, 1, 5, 3, 4 };
        int n = arr.Length;
        frequencyOfEach(arr, n);

    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find frequencies of
// elements in limited range array.

function frequencyOfEach(&$arr, $n)
{
    // finding maximum element in array
    $max = max($arr);

    // make hash array of size equal to
    // maximum element in array
    $hash = array_fill(0, $max + 1, NULL);

    /* Counting frequency of each element
    of array and storing it in hash*/
    for ($i = 0; $i < $n; $i++)
    {
        $hash[$arr[$i]]++;
    }

    // printing frequency of elements
    for ($i = 0; $i <= $max; $i++)
    {

        /* If hash[i] has stored any value
        i.e element has occurred atleast
        once in array */
        if ($hash[$i] != 0)
            echo $i . "-->" . $hash[$i] . "\n";
    }
}

// Driver Code
$arr = array(5, 2, 2, 3, 5, 1, 1, 5, 3, 4 );
$n = sizeof($arr);
frequencyOfEach($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find frequencies of elements in
// limited range array.

function frequencyOfEach(arr,n)
{
let max = Number.MIN_VALUE;

    // finding maximum element in array
    for (let i = 0; i < n; i++)
    {
        if (arr[i] > max)
            max = arr[i];
    }

    // make hash array of size equal to maximum
    // element in array
    let hash = new Array(max + 1);
    for(let i = 0; i < hash.length; i++)
    {
        hash[i] = 0;
    }

    /* Counting frequency of each element of array
    and storing it in hash*/
    for (let i = 0; i < n; i++)
    {
        hash[arr[i]]++;
    }

    // printing frequency of elements
    for (let i = 0; i <= max; i++) {

        /* If hash[i] has stored any value
        i.e element has occurred atleast
        once in array */
        if (hash[i] != 0)
            document.write(i+"-->"+hash[i]+"<br>");
    }
}

let arr=[5, 2, 2, 3, 5, 1, 1, 5, 3, 4];
let n = arr.length;
frequencyOfEach(arr, n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1-->2
2-->2
3-->2
4-->1
5-->3
```

**时间复杂度:**O(max _ value)
T3】辅助空间: O(max_value)