# 偶数位置的正元素和奇数位置的负元素(不维持相对顺序)

> 原文:[https://www . geeksforgeeks . org/偶数位置的正元素和奇数位置的负元素-相对顺序-未维护/](https://www.geeksforgeeks.org/positive-elements-at-even-and-negative-at-odd-positions-relative-order-not-maintained/)

已经给了你一个数组，你必须编写一个程序来转换这个数组，使得正元素出现在数组的偶数位置，负元素出现在数组的奇数位置。我们必须在适当的地方做。
可以有不相等数量的正值和负值，多余的值必须保持原样。

**示例:**

```
Input : arr[] = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10}
Output : arr[] = {1, -3, 5, -3, 6, 6, 7, -4, 9, 10}

Input : arr[] = {-1, 3, -5, 6, 3, 6, -7, -4, -9, 10}
Output : arr[] = {3, -1, 6, -5, 3, -7, 6, -4, 10, -9}
```

想法是使用[快速排序](https://www.geeksforgeeks.org/quick-sort/)的[霍尔分区](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)过程。
我们有两个积极和消极的指标。我们在数组的开头设置正指针，在数组的第一个位置设置负指针。

我们将正指针向前移动两步，直到它找到负元素。同样，我们将负指针向前移动两个位置，直到它在其位置找到一个正值。

如果正指针和负指针在数组中，那么我们将交换这些索引处的值，否则我们将停止执行该过程。

## C++

```
// C++ program to rearrange positive and negative
// numbers
#include <bits/stdc++.h>
using namespace std;

void rearrange(int a[], int size)
{
    int positive = 0, negative = 1;

    while (true) {

        /* Move forward the positive pointer till
         negative number number not encountered */
        while (positive < size && a[positive] >= 0)
            positive += 2;

        /* Move forward the negative pointer till
         positive number number not encountered   */
        while (negative < size && a[negative] <= 0)
            negative += 2;

        // Swap array elements to fix their position.
        if (positive < size && negative < size)
            swap(a[positive], a[negative]);

        /* Break from the while loop when any index
            exceeds the size of the array */
        else
            break;
    }
}

// Driver code
int main()
{
    int arr[] = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 };
    int n = (sizeof(arr) / sizeof(arr[0]));

    rearrange(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange positive
// and negative numbers
import java.io.*;

class GFG {

static void rearrange(int a[], int size)
{
  int positive = 0, negative = 1, temp;

    while (true) {

    /* Move forward the positive pointer till
    negative number number not encountered */
    while (positive < size && a[positive] >= 0)
        positive += 2;

    /* Move forward the negative pointer till
        positive number number not encountered */
    while (negative < size && a[negative] <= 0)
        negative += 2;

    // Swap array elements to fix their position.
    if (positive < size && negative < size) {
        temp = a[positive];
        a[positive] = a[negative];
        a[negative] = temp;
    }

    /* Break from the while loop when any index
    exceeds the size of the array */
    else
        break;
    }
}

// Driver code
public static void main(String args[]) {
    int arr[] = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10};
    int n = arr.length;

    rearrange(arr, n);
    for (int i = 0; i < n; i++)
    System.out.print(arr[i] + " ");
}
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to rearrange
# positive and negative numbers

def rearrange(a, size) :

    positive = 0
    negative = 1

    while (True) :

        # Move forward the positive
        # pointer till negative number
        # number not encountered
        while (positive < size and a[positive] >= 0) :
            positive = positive + 2

        # Move forward the negative
        # pointer till positive number
        # number not encountered
        while (negative < size and a[negative] <= 0) :
            negative = negative + 2

        # Swap array elements to fix
        # their position.
        if (positive < size and negative < size) :
            temp = a[positive]
            a[positive] = a[negative]
            a[negative] = temp

        # Break from the while loop when
        # any index exceeds the size of
        # the array
        else :
            break

# Driver code
arr =[ 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 ]
n = len(arr)

rearrange(arr, n)
for i in range(0, n) :
    print(arr[i], end = " ")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to rearrange positive
// and negative numbers
using System;

class GFG {

// Function to rearrange
static void rearrange(int []a, int size)
{
int positive = 0, negative = 1, temp;

    while (true) {

    // Move forward the positive pointer till
    // negative number number not encountered
    while (positive < size && a[positive] >= 0)
        positive += 2;

    // Move forward the negative pointer till
    // positive number number not encountered
    while (negative < size && a[negative] <= 0)
        negative += 2;

    // Swap array elements to fix their position.
    if (positive < size && negative < size) {
        temp = a[positive];
        a[positive] = a[negative];
        a[negative] = temp;
    }

    // Break from the while loop when any
    // index exceeds the size of the array
    else
        break;
    }
}

// Driver Code
public static void Main(String []args) {
    int []arr = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10};
    int n = arr.Length;

    rearrange(arr, n);
    for (int i = 0; i < n; i++)
    Console.Write(arr[i] + " ");
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to rearrange positive
// and negative numbers

function rearrange(&$a, $size)
{
    $positive = 0;
    $negative = 1;

    while (true)
    {

        /* Move forward the positive
        pointer till negative number
        number not encountered */
        while ($positive < $size &&
               $a[$positive] >= 0)
            $positive += 2;

        /* Move forward the negative
        pointer till positive number
        number not encountered */
        while ($negative < $size &&
               $a[$negative] <= 0)
            $negative += 2;

        // Swap array elements to fix
        // their position.
        if ($positive < $size &&
            $negative < $size)
        {
            $temp = $a[$positive];
            $a[$positive] = $a[$negative];
            $a[$negative] = $temp;
        }

        /* Break from the while loop
        when any index exceeds the
        size of the array */
        else
            break;
    }
}

// Driver code
$arr = array( 1, -3, 5, 6, -3,
              6, 7, -4, 9, 10 );
$n = sizeof($arr);

rearrange($arr, $n);
for ($i = 0; $i < $n; $i++)
    echo $arr[$i] ." ";

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript  program to rearrange positive
// and negative numbers
function rearrange(a, size)
{
    let  positive = 0;
    let negative = 1;
    let temp;

    while (true)
    {

        // Move forward the positive
        // pointer till negative number
        // number not encountered
        while (positive < size && a[positive] >= 0)
            positive += 2;

        // Move forward the negative pointer
        // till positive number number not encountered
        while (negative < size && a[negative] <= 0)
            negative += 2;

        // Swap array elements to fix their position.
        if (positive < size && negative < size)
        {
            temp = a[positive];
            a[positive] = a[negative];
            a[negative] = temp;
        }

        // Break from the while loop when any index
        // exceeds the size of the array
        else
            break;
    }
}

// Driver code
let arr = [ 1, -3, 5, 6, -3,
            6, 7, -4, 9, 10 ];
let n = arr.length;

rearrange(arr, n);

for(let i = 0; i < n; i++)
    document.write(arr[i] + " ");

// This code is contributed by sravan kumar G

</script>
```

**输出:**

```
1 -3 5 -3 6 6 7 -4 9 10 
```

让我们解释第一个例子中代码的工作方式
arr[] = {1，-3，5，6，-3，6，7，-4，9，10}
我们声明两个变量正和负正指向第零个位置，负指向第一个位置
正= 0 负= 1
在第一次迭代中，正将移动 4 位到第五个位置，因为[4]小于零，正= 4。
负数将移动 2 位，并将指向第四个位置作为[3] > 0
我们将交换正负位置值，因为它们小于数组的大小。
在第一次迭代后，数组变成 arr[] = {1，-3，5，-3，6，6，7，-4，9，10}
现在正值位于第四个位置，负值位于第三个位置
在第二次迭代中，正值将移动 6 个位置，其值将超过数组的大小
。

负指针将向前移动两步，并指向第 5 个位置
当正指针值变得大于数组大小时，我们将不会执行任何交换操作并脱离 while 循环。
最终输出将是
arr[] = {1，-3，5，-3，6，6，7，-4，9，10}

**不维持相对顺序的例子:**T2 {-1，-2，-3，-4，-5，6，7，8 }；

**另一种方法:-**
其思想是找到一个位置不正确的正/负元素(即奇数处为正，偶数处为负)，然后在剩余数组中找到同样位置不正确的符号相反的元素，然后交换这两个元素。

下面是上述想法的实现。

## C++

```
// C++ program to rearrange positive
// and negative numbers
#include<iostream>
using namespace std;

// Swap function
void swap(int* a, int i , int j)
{
    int temp = a[i];
    a[i] = a[j];
    a[j] = temp;
    return ;
}

// Print array function
void printArray(int* a, int n)
{
    for(int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
    return ;
}

// Driver code
int main()
{
    int arr[] = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 };
    int n = sizeof(arr)/sizeof(arr[0]);

    //before modification
    printArray(arr, n);

    for(int i = 0; i < n; i++)
    {
        if(arr[i] >= 0 && i % 2 == 1)
        {
            // out of order positive element
            for(int j = i + 1; j < n; j++)
            {
                if(arr[j] < 0 && j % 2 == 0)
                {
                    // find out of order negative
                    // element in remaining array
                    swap(arr, i, j);
                    break ;
                }
            }
        }
        else if(arr[i] < 0 && i % 2 == 0)
        {
            // out of order negative element
            for(int j = i + 1; j < n; j++)
            {
                if(arr[j] >= 0 && j % 2 == 1)
                {
                    // find out of order positive
                    // element in remaining array
                    swap(arr, i, j);
                    break;
                }
            }
        }
    }

    //after modification
    printArray(arr, n);
    return 0;
}

// This code is contributed by AnitAggarwal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange positive
// and negative numbers
import java.io.*;
import java.util.*;

class GFG
{

    // Swap function
    static void swap(int[] a, int i, int j)
    {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

    // Print array function
    static void printArray(int[] a, int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        int[] arr = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 };
        int n = arr.length;

        //before modification
        printArray(arr, n);

        for (int i = 0; i < n; i++)
        {
            if (arr[i] >= 0 && i % 2 == 1)
            {
                // out of order positive element
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[j] < 0 && j % 2 == 0)
                    {
                        // find out of order negative
                        // element in remaining array
                        swap(arr, i, j);
                        break ;
                    }
                }
            }

            else if (arr[i] < 0 && i % 2 == 0)
            {
                // out of order negative element
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[j] >= 0 && j % 2 == 1)
                    {
                        // find out of order positive
                        // element in remaining array
                        swap(arr, i, j);
                        break;
                    }
                }
            }
        }

        //after modification
        printArray(arr, n);
    }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program to rearrange positive
# and negative numbers

# Print array function
def printArray(a, n):
    for i in a:
        print(i, end = " ")
    print()

# Driver code
arr = [1, -3, 5, 6, -3, 6, 7, -4, 9, 10]
n = len(arr)

# before modification
printArray(arr, n)

for i in range(n):

    if(arr[i] >= 0 and i % 2 == 1):

        # out of order positive element
        for j in range(i + 1, n):

            if(arr[j] < 0 and j % 2 == 0):

                # find out of order negative
                # element in remaining array
                arr[i], arr[j] = arr[j], arr[i]
                break

    elif (arr[i] < 0 and i % 2 == 0):

        # out of order negative element
        for j in range(i + 1, n):

            if(arr[j] >= 0 and j % 2 == 1):

                # find out of order positive
                # element in remaining array
                arr[i], arr[j] = arr[j], arr[i]
                break

# after modification
printArray(arr, n);

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to rearrange positive
// and negative numbers
using System;

class GFG
{

    // Swap function
    static void swap(int[] a, int i, int j)
    {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

    // Print array function
    static void printArray(int[] a, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(a[i] + " ");
        Console.WriteLine();
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 };
        int n = arr.Length;

        //before modification
        printArray(arr, n);

        for (int i = 0; i < n; i++)
        {
            if (arr[i] >= 0 && i % 2 == 1)
            {
                // out of order positive element
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[j] < 0 && j % 2 == 0)
                    {
                        // find out of order negative
                        // element in remaining array
                        swap(arr, i, j);
                        break ;
                    }
                }
            }

            else if (arr[i] < 0 && i % 2 == 0)
            {
                // out of order negative element
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[j] >= 0 && j % 2 == 1)
                    {
                        // find out of order positive
                        // element in remaining array
                        swap(arr, i, j);
                        break;
                    }
                }
            }
        }

        // after modification
        printArray(arr, n);
    }
}

// This code is contributed by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript program to rearrange positive
// and negative numbers

    // Swap function
    function  swap(a,i,j)
    {
        let temp = a[i];
        a[i] = a[j];
        a[j] = temp;

    }

    // Print array function
    function printArray(a,n)
    {
        for (let i = 0; i < n; i++)
            document.write(a[i] + " ");
        document.write("<br>");
    }

     // Driver code
    let arr=[1, -3, 5, 6, -3, 6, 7, -4, 9, 10];
    let n = arr.length;

        //before modification
        printArray(arr, n);

        for (let i = 0; i < n; i++)
        {
            if (arr[i] >= 0 && i % 2 == 1)
            {
                // out of order positive element
                for (let j = i + 1; j < n; j++)
                {
                    if (arr[j] < 0 && j % 2 == 0)
                    {
                        // find out of order negative
                        // element in remaining array
                        swap(arr, i, j);
                        break ;
                    }
                }
            }

            else if (arr[i] < 0 && i % 2 == 0)
            {
                // out of order negative element
                for (let j = i + 1; j < n; j++)
                {
                    if (arr[j] >= 0 && j % 2 == 1)
                    {
                        // find out of order positive
                        // element in remaining array
                        swap(arr, i, j);
                        break;
                    }
                }
            }
        }

        //after modification
        printArray(arr, n);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
1 -3 5 6 -3 6 7 -4 9 10 
1 -3 5 -3 6 6 7 -4 9 10 
```

本文由 **Ashish Madaan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。