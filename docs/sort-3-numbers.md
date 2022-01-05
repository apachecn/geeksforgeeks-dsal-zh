# 排序 3 个数字

> 原文:[https://www.geeksforgeeks.org/sort-3-numbers/](https://www.geeksforgeeks.org/sort-3-numbers/)

给定三个数字，如何排序？

**示例**:

```
Input  : arr[] = {3, 2, 1}
Output : arr[] = {1, 2, 3}

Input : arr[] = {6, 5, 0}
Output :arr[] = {0, 5, 6}
```

一个简单的解决方法是使用**排序**功能。

## C++

```
// C++ program to sort an array of size 3
#include <algorithm>
#include <iostream>
using namespace std;

int main()
{
    int a[] = {10, 12, 5};

    sort(a, a + 3);

    for (int i = 0; i < 3; i++)
        cout << a[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort
// an array of size 3
import java.io.*;
import java .util.*;

class GFG
{
    public static void main (String[] args)
    {
        int a[] = {10, 12, 5};

        Arrays.sort(a);

        for (int i = 0; i < 3; i++)
            System.out.print( a[i] + " ");
    }
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python3 program to sort
# an array of size 3
a = [10, 12, 5]
a.sort()
for i in range(len(a)):
    print(a[i], end = ' ')

# This code is contributed
# by Samyukta S Hegde
```

## C#

```
// C# program to sort
// an array of size 3
using System;
class GFG
{
    public static void Main ()
    {
        int []a = {10, 12, 5};

        Array.Sort(a);

        for (int i = 0; i < 3; i++)
         Console.Write( a[i] + " ");
    }
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort
// an array of size 3
$a = array(10, 12, 5);

sort($a);

for ($i = 0; $i < 3; $i++)
    echo $a[$i] , " ";

// This code is contributed
// by chandan_jnu.
?>
```

## java 描述语言

```
<script>

// Javascript program to sort an array of size 3
let arr = [10, 12, 5];

arr.sort((a, b) => a - b);

for (let i = 0; i < 3; i++)
document.write(arr[i] + " ");

// This code is contributed by Jana_Sayantan.
</script>
```

**Output:** 

```
5 10 12
```

**如何编写自己的做最小比较不使用额外变量的排序函数？**
想法是使用[插入排序](https://www.geeksforgeeks.org/insertion-sort/)因为插入排序最适合小数组。

## C++

```
// C++ program to sort an array of size 3
#include <algorithm>
#include <iostream>
using namespace std;

int sort3(int arr[])
{
    // Insert arr[1]
    if (arr[1] < arr[0])
       swap(arr[0], arr[1]);

    // Insert arr[2]
    if (arr[2] < arr[1])
    {
       swap(arr[1], arr[2]);
       if (arr[1] < arr[0])
          swap(arr[1], arr[0]);
    }
}

int main()
{
    int a[] = {10, 12, 5};

    sort3(a);

    for (int i = 0; i < 3; i++)
        cout << a[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort
// an array of size 3
import java.io.*;
import java.util.*;

class GFG
{
static void sort3(int arr[],
                  int temp[])
{
    // Insert arr[1]
    if (arr[1] < arr[0])
        {
            temp[0] = arr[0];
            arr[0] = arr[1];
            arr[1] = temp[0];
        }

    // Insert arr[2]
    if (arr[2] < arr[1])
    {
            temp[0] = arr[1];
            arr[1] = arr[2];
            arr[2] = temp[0];

    if (arr[1] < arr[0])
        {
            temp[0] = arr[0];
            arr[0] = arr[1];
            arr[1] = temp[0];
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int a[] = new int[]{10, 12, 5};
    int temp1[] = new int[10];
    sort3(a, temp1);

    for (int i = 0; i < 3; i++)
        System.out.print( a[i] + " ");
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to sort an array of size 3
def sort3(arr):

    # Insert arr[1]
    if (arr[1] < arr[0]):
        arr[0], arr[1] = arr[1], arr[0]

    # Insert arr[2]
    if (arr[2] < arr[1]):
        arr[1], arr[2] = arr[2], arr[1]
        if (arr[1] < arr[0]):
            arr[1], arr[0] = arr[0], arr[1]

# Driver code
a = [10, 12, 5]

sort3(a)

for i in range(3):
    print(a[i],end=" ")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to sort
// an array of size 3
using System;

class GFG {

static void sort3(int []arr, int []temp)
{

    // Insert arr[1]
    if (arr[1] < arr[0])
        {
            temp[0] = arr[0];
            arr[0] = arr[1];
            arr[1] = temp[0];
        }

    // Insert arr[2]
    if (arr[2] < arr[1])
    {
        temp[0] = arr[1];
        arr[1] = arr[2];
        arr[2] = temp[0];

        if (arr[1] < arr[0])
        {
            temp[0] = arr[0];
            arr[0] = arr[1];
            arr[1] = temp[0];
        }
    }
}

    // Driver Code
    public static void Main(String []args)
    {
        int []a= new int[]{10, 12, 5};
        int []temp1 = new int[10];
        sort3(a, temp1);

        for (int i = 0; i < 3; i++)
            Console.Write( a[i] + " ");
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort an array of size 3
function sort3(&$arr, $temp)
{
    // Insert arr[1]
    if ($arr[1] < $arr[0])
    {
        $temp[0] = $arr[0];
        $arr[0] = $arr[1];
        $arr[1] = $temp[0];
    }

    // Insert arr[2]
    if ($arr[2] < $arr[1])
    {
        $temp[0] = $arr[1];
        $arr[1] = $arr[2];
        $arr[2] = $temp[0];
    }

    if ($arr[1] < $arr[0])
    {
        $temp[0] = $arr[0];
        $arr[0] = $arr[1];
        $arr[1] = $temp[0];
    }
}

// Driver Code
$a = array(10, 12, 5);
$temp1 = array(10);
sort3($a, $temp1);

for ($i = 0; $i < 3; $i++)
    echo($a[$i] . " ");

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript program to sort an
// array of size 3
function sort3(arr, temp)
{

    // Insert arr[1]
    if (arr[1] < arr[0])
    {
        temp[0] = arr[0];
        arr[0] = arr[1];
        arr[1] = temp[0];
    }

    // Insert arr[2]
    if (arr[2] < arr[1])
    {
        temp[0] = arr[1];
        arr[1] = arr[2];
        arr[2] = temp[0];

        if (arr[1] < arr[0])
        {
            temp[0] = arr[0];
            arr[0] = arr[1];
            arr[1] = temp[0];
        }
    }
}

// Driver code
let a = [ 10, 12, 5 ];
let temp1 = [10];
sort3(a, temp1);

for(let i = 0; i < 3; i++)
    document.write( a[i] + " ");

// This code is contributed by decode2207

</script>
```

**Output:** 

```
5 10 12
```