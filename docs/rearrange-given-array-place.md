# 重新排列一个数组，使 arr[i]变成 arr[arr[i]]，并有 O(1)个额外空间

> 原文:[https://www.geeksforgeeks.org/rearrange-given-array-place/](https://www.geeksforgeeks.org/rearrange-given-array-place/)

给定一个大小为 *n* 的数组 *arr[]* ，其中每个元素都在从 *0* 到 *n-1* 的范围内。重新排列给定的数组，使 *arr[i]* 变成 *arr[arr[i]]* 。这应该用 *O(1)* 的额外空间来完成。

**示例:**

```
Input: arr[]  = {3, 2, 0, 1}
Output: arr[] = {1, 0, 3, 2}
Explanation: 
In the given array 
arr[arr[0]] is 1 so arr[0] in output array is 1
arr[arr[1]] is 0 so arr[1] in output array is 0
arr[arr[2]] is 3 so arr[2] in output array is 3
arr[arr[3]] is 2 so arr[3] in output array is 2

Input: arr[] = {4, 0, 2, 1, 3}
Output: arr[] = {3, 4, 2, 0, 1}
Explanation:
arr[arr[0]] is 3 so arr[0] in output array is 3
arr[arr[1]] is 4 so arr[1] in output array is 4
arr[arr[2]] is 2 so arr[2] in output array is 2
arr[arr[3]] is 0 so arr[3] in output array is 0
arr[arr[4]] is 1 so arr[4] in output array is 1

Input: arr[] = {0, 1, 2, 3}
Output: arr[] = {0, 1, 2, 3}
Explanation:
arr[arr[0]] is 0 so arr[0] in output array is 0
arr[arr[1]] is 1 so arr[1] in output array is 1
arr[arr[2]] is 2 so arr[2] in output array is 2
arr[arr[3]] is 3 so arr[3] in output array is 3
```

*如果去掉多余的空间条件，问题就变得很简单了。问题的主要部分是在没有额外空间的情况下做这件事。*

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/rearrange-an-array-with-o1-extra-space3142/1)

以下解决方案的功劳归于[加内什拉姆·孙达拉姆](http://www.careercup.com/question?id=4909367207919616)。

**方法:**给定数组的数组元素位于 0 到 n-1 之间。现在需要一个可以同时存储两个不同值的数组元素。为了实现这种增量，第一个索引处的每个元素都要增加*(arr[arr[I]% n)* n*。在第一步的增量操作之后，每个元素都保存旧值和新值。旧值可以通过 *arr[i]%n* 获得，新值可以通过 *arr[i]/n* 获得。

**这是如何实现的？**
假设一个元素是 *a* ，另一个元素是 *b* ，两个元素都小于 n，那么如果一个元素 *a* 递增 *b*n* 。这样元素就变成了 *a + b*n* 所以当 *a + b*n* 除以 n，那么值就是 b， *a + b*n* % n 就是 a。

**算法:**

1.  从头到尾遍历数组。
2.  对于每个索引，将元素增加*数组[数组[索引]]【T1]%n。要获得第 I 个元素，请找到 n 的模，即数组[索引]% n。*
3.  再次从头到尾跟踪数组
4.  将 ith 元素除以 n 后打印出 ith 元素，即数组[I/n]。

**执行:**

## C++

```
#include <iostream>
using namespace std;

// The function to rearrange an array
// in-place so that arr[i] becomes arr[arr[i]].
void rearrange(int arr[], int n)
{
    // First step: Increase all values by (arr[arr[i]]%n)*n
    for (int i=0; i < n; i++)
        arr[i] += (arr[arr[i]]%n)*n;

    // Second Step: Divide all values by n
    for (int i=0; i<n; i++)
        arr[i] /= n;
}

// A utility function to print an array of size n
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

/* Driver program to test above functions*/
int main()
{
    int arr[] = {3, 2, 0, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Given array is \n";
    printArr(arr, n);

    rearrange(arr, n);

    cout << "Modified array is \n";
    printArr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Rearrange
{
    // The function to rearrange an array in-place so that arr[i]
    // becomes arr[arr[i]].
    void rearrange(int arr[], int n)
    {
        // First step: Increase all values by (arr[arr[i]]%n)*n
        for (int i = 0; i < n; i++)
            arr[i] += (arr[arr[i]] % n) * n;

        // Second Step: Divide all values by n
        for (int i = 0; i < n; i++)
            arr[i] /= n;
    }

    // A utility function to print an array of size n
    void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
        System.out.println("");
    }

    /* Driver program to test above functions */
    public static void main(String[] args)
    {
        Rearrange rearrange = new Rearrange();
        int arr[] = {3, 2, 0, 1};
        int n = arr.length;

        System.out.println("Given Array is :");
        rearrange.printArr(arr, n);

        rearrange.rearrange(arr, n);

        System.out.println("Modified Array is :");
        rearrange.printArr(arr, n);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to Rearrange
# an array so that arr[i] becomes
# arr[arr[i]]

# The function to rearrange an
# array in-place so that arr[i]
# becomes arr[arr[i]].
def rearrange(arr, n):

    # First step: Increase all values
    # by (arr[arr[i]] % n) * n
    for i in range(0, n):
        arr[i] += (arr[arr[i]] % n) * n

    # Second Step: Divide all values
    # by n
    for i in range(0, n):
        arr[i] = int(arr[i] / n)

# A utility function to print
# an array of size n
def printArr(arr, n):

    for i in range(0, n):
        print (arr[i], end =" ")
    print ("")

# Driver program
arr = [3, 2, 0, 1]
n = len(arr)

print ("Given array is")
printArr(arr, n)

rearrange(arr, n);
print ("Modified array is")
printArr(arr, n)

# This code is contributed by shreyanshi_arun
```

## C#

```
// C# Program to rearrange an array
// so that arr[i] becomes arr[arr[i]]
// with O(1) extra space
using System;

class Rearrange
{

    // Function to rearrange an
    // array in-place so that arr[i]
    // becomes arr[arr[i]].
    void rearrange(int []arr, int n)
    {

        // First step: Increase all values
        // by (arr[arr[i]] % n) * n
        for (int i = 0; i < n; i++)
            arr[i] += (arr[arr[i]] % n) * n;

        // Second Step: Divide all values by n
        for (int i = 0; i < n; i++)
            arr[i] /= n;
    }

    // A utility function to
    // print an array of size n
    void printArr(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine("");
    }

    //  Driver Code
    public static void Main()
    {
        Rearrange rearrange = new Rearrange();
        int []arr = {3, 2, 0, 1};
        int n = arr.Length;

        Console.Write("Given Array is :");
        rearrange.printArr(arr, n);

        rearrange.rearrange(arr, n);

        Console.Write("Modified Array is :");
        rearrange.printArr(arr, n);
    }
}

// This code has been contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// The function to rearrange an array
// in-place so that arr[i] becomes arr[arr[i]].
function rearrange(&$arr, $n)
{
    // First step: Increase all values
    // by (arr[arr[i]]%n)*n
    for ($i = 0; $i < $n; $i++)
        $arr[$i] += ($arr[$arr[$i]] % $n) * $n;

    // Second Step: Divide all values by n
    for ($i = 0; $i < $n; $i++)
        $arr[$i] = intval($arr[$i] / $n);
}

// A utility function to print
// an array of size n
function printArr(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] ." ";
    echo "\n";
}

// Driver Code
$arr = array(3, 2, 0, 1);
$n = sizeof($arr);

echo "Given array is \n";
printArr($arr, $n);

rearrange($arr, $n);

echo "Modified array is \n";
printArr($arr, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// The function to rearrange an array
// in-place so that arr[i] becomes arr[arr[i]].
function rearrange(arr, n)
{

    // First step: Increase all values by (arr[arr[i]]%n)*n
    for (let i = 0; i < n; i++)
        arr[i] += (arr[arr[i]] % n) * n;

    // Second Step: Divide all values by n
    for (let i = 0; i < n; i++)
        arr[i] = Math.floor(arr[i] / n);
}

// A utility function to print an array of size n
function printArr(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
    document.write("<br>");
}

/* Driver program to test above functions*/
    let arr = [3, 2, 0, 1];
    let n = arr.length;

    document.write("Given array is <br>");
    printArr(arr, n);
    rearrange(arr, n);

    document.write("Modified array is <br>");
    printArr(arr, n);

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
Given array is
3 2 0 1
Modified array is
1 0 3 2
```

**复杂度分析:**

*   **时间复杂度:** O(n)，只需要遍历数组一次。所以时间复杂度是 O(n)。
*   **辅助空间:** O(1)，不需要额外空间。

*上述解决方案的问题是，可能会造成溢出。*

**这里有一个更好的解决方案:**
[**重新排列一个数组，使得‘arr[j]’变成‘I’，如果‘arr[I]’是‘j’**](https://www.geeksforgeeks.org/rearrange-array-arrj-becomes-arri-j/)

本文由**希曼舒·古普塔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息