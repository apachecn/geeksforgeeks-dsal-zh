# 鸡尾酒种类

> 原文:[https://www.geeksforgeeks.org/cocktail-sort/](https://www.geeksforgeeks.org/cocktail-sort/)

鸡尾酒排序是[气泡排序](https://www.geeksforgeeks.org/bubble-sort/)的变体。冒泡排序算法总是从左侧遍历元素，并在第一次迭代中将最大的元素移动到正确的位置，在第二次迭代中将第二大元素移动到正确的位置，以此类推。鸡尾酒排序交替地在两个方向上遍历给定的数组。
**算法:**
算法的每次迭代分为 2 个阶段:

1.  第一阶段从左到右循环遍历数组，就像冒泡排序一样。在循环过程中，比较相邻的项目，如果左边的值大于右边的值，则交换值。在第一次迭代结束时，最大的数字将位于数组的末尾。
2.  第二阶段以相反的方向在数组中循环——从最近排序的项之前的项开始，然后移回数组的开头。此外，还会比较相邻的项目，并在需要时进行交换。

**示例:**

让我们考虑一个示例数组(5 1 4 2 8 0 2)

**第一个向前传球:**
( **5 1** 4 2 8 0 2)？( **1 5** 4 2 8 0 2)、互换自 5 > 1
(1 **5 4** 2 8 0 2)？(1 **4 5** 2 8 0 2)、互换自 5>4
(1 4**5 2**8 0 2)？(1 4 **2 5** 8 0 2)、互换自 5>2
(1 4 2**5 8**0 2)？(1 4 2**5 8**0 2)
(1 4 2 5**8 0**2)？(1 4 2 5 **0 8** 2)、互换自 8 > 0
(1 4 2 5 0 **8 2** )？(1 4 2 5 0 **2 8** )，交换自 8 > 2
第一次向前传递后，数组中最大的元素将出现在数组的最后一个索引处。
**第一次倒传球:**
(1 4 2 5 **0 2** 8)？(1 4 2 5**0 2**8)
(1 4 2**5 0**2 8)？(1 4 2 **0 5** 2 8)，互换自 5>0
(1 4**2 0**5 2 8)？(1 4 **0 2** 5 2 8)、互换自 2>0
(1**4 0**2 5 2 8)？(1 **0 4** 2 5 2 8)，互换自 4>0
(**1 0**4 2 5 2 8)？( **0 1** 4 2 5 2 8)，交换自 1 > 0
第一次向后传递后，数组的最小元素将出现在数组的第一个索引处。
**第二次向前传球:**
(0 **1 4** 2 5 2 8)？(0**1 4**2 5 2 8)
(0 1**4 2**5 2 8)？(0 1 **2 4** 5 2 8)，互换自 4>2
(0 1 2**4 5**2 8)？(0 1 2**4 5**2 8)
(0 1 2 4**5 2**8)？(0 1 2 4 **2 5** 8)、互换自 5>2
T86】第二次倒传球:T88】(0 1 2**4 2**5 8)？(0 1 2 **2 4** 5 8)、交换自 4 > 2
现在数组已经排序了，但是我们的算法不知道是否完成。算法需要在没有任何**交换**的情况下完成这一整道，才能知道排序。
(0 1 **2 2** 4 5 8)？(0 1**2 2**4 5 8)
(0**1 2**2 4 5 8)？(0 **1 2** 2 4 5 8)
以下是上述算法的实现:

## C++

```
// C++ implementation of Cocktail Sort
#include <bits/stdc++.h>
using namespace std;

// Sorts arrar a[0..n-1] using Cocktail sort
void CocktailSort(int a[], int n)
{
    bool swapped = true;
    int start = 0;
    int end = n - 1;

    while (swapped)
    {
        // reset the swapped flag on entering
        // the loop, because it might be true from
        // a previous iteration.
        swapped = false;

        // loop from left to right same as
        // the bubble sort
        for (int i = start; i < end; ++i)
        {
            if (a[i] > a[i + 1]) {
                swap(a[i], a[i + 1]);
                swapped = true;
            }
        }

        // if nothing moved, then array is sorted.
        if (!swapped)
            break;

        // otherwise, reset the swapped flag so that it
        // can be used in the next stage
        swapped = false;

        // move the end point back by one, because
        // item at the end is in its rightful spot
        --end;

        // from right to left, doing the
        // same comparison as in the previous stage
        for (int i = end - 1; i >= start; --i)
        {
            if (a[i] > a[i + 1]) {
                swap(a[i], a[i + 1]);
                swapped = true;
            }
        }

        // increase the starting point, because
        // the last stage would have moved the next
        // smallest number to its rightful spot.
        ++start;
    }
}

/* Prints the array */
void printArray(int a[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);
    printf("\n");
}

// Driver code
int main()
{
    int a[] = { 5, 1, 4, 2, 8, 0, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    CocktailSort(a, n);
    printf("Sorted array :\n");
    printArray(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of Cocktail Sort
public class CocktailSort
{
    void cocktailSort(int a[])
    {
        boolean swapped = true;
        int start = 0;
        int end = a.length;

        while (swapped == true)
        {
            // reset the swapped flag on entering the
            // loop, because it might be true from a
            // previous iteration.
            swapped = false;

            // loop from bottom to top same as
            // the bubble sort
            for (int i = start; i < end - 1; ++i)
            {
                if (a[i] > a[i + 1]) {
                    int temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // if nothing moved, then array is sorted.
            if (swapped == false)
                break;

            // otherwise, reset the swapped flag so that it
            // can be used in the next stage
            swapped = false;

            // move the end point back by one, because
            // item at the end is in its rightful spot
            end = end - 1;

            // from top to bottom, doing the
            // same comparison as in the previous stage
            for (int i = end - 1; i >= start; i--)
            {
                if (a[i] > a[i + 1])
                {
                    int temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // increase the starting point, because
            // the last stage would have moved the next
            // smallest number to its rightful spot.
            start = start + 1;
        }
    }

    /* Prints the array */
    void printArray(int a[])
    {
        int n = a.length;
        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
    {
        CocktailSort ob = new CocktailSort();
        int a[] = { 5, 1, 4, 2, 8, 0, 2 };
        ob.cocktailSort(a);
        System.out.println("Sorted array");
        ob.printArray(a);
    }
}
```

## 计算机编程语言

```
# Python program for implementation of Cocktail Sort

def cocktailSort(a):
    n = len(a)
    swapped = True
    start = 0
    end = n-1
    while (swapped == True):

        # reset the swapped flag on entering the loop,
        # because it might be true from a previous
        # iteration.
        swapped = False

        # loop from left to right same as the bubble
        # sort
        for i in range(start, end):
            if (a[i] > a[i + 1]):
                a[i], a[i + 1] = a[i + 1], a[i]
                swapped = True

        # if nothing moved, then array is sorted.
        if (swapped == False):
            break

        # otherwise, reset the swapped flag so that it
        # can be used in the next stage
        swapped = False

        # move the end point back by one, because
        # item at the end is in its rightful spot
        end = end-1

        # from right to left, doing the same
        # comparison as in the previous stage
        for i in range(end-1, start-1, -1):
            if (a[i] > a[i + 1]):
                a[i], a[i + 1] = a[i + 1], a[i]
                swapped = True

        # increase the starting point, because
        # the last stage would have moved the next
        # smallest number to its rightful spot.
        start = start + 1

# Driver code
a = [5, 1, 4, 2, 8, 0, 2]
cocktailSort(a)
print("Sorted array is:")
for i in range(len(a)):
    print("% d" % a[i])
```

## C#

```
// C# program for implementation of Cocktail Sort
using System;

class GFG {

    static void cocktailSort(int[] a)
    {
        bool swapped = true;
        int start = 0;
        int end = a.Length;

        while (swapped == true) {

            // reset the swapped flag on entering the
            // loop, because it might be true from a
            // previous iteration.
            swapped = false;

            // loop from bottom to top same as
            // the bubble sort
            for (int i = start; i < end - 1; ++i) {
                if (a[i] > a[i + 1]) {
                    int temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // if nothing moved, then array is sorted.
            if (swapped == false)
                break;

            // otherwise, reset the swapped flag so that it
            // can be used in the next stage
            swapped = false;

            // move the end point back by one, because
            // item at the end is in its rightful spot
            end = end - 1;

            // from top to bottom, doing the
            // same comparison as in the previous stage
            for (int i = end - 1; i >= start; i--) {
                if (a[i] > a[i + 1]) {
                    int temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // increase the starting point, because
            // the last stage would have moved the next
            // smallest number to its rightful spot.
            start = start + 1;
        }
    }

    /* Prints the array */
    static void printArray(int[] a)
    {
        int n = a.Length;
        for (int i = 0; i < n; i++)
            Console.Write(a[i] + " ");
        Console.WriteLine();
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 5, 1, 4, 2, 8, 0, 2 };
        cocktailSort(a);
        Console.WriteLine("Sorted array ");
        printArray(a);
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>
    // Javascript program for implementation of Cocktail Sort

    function cocktailSort(a)
    {
        let swapped = true;
        let start = 0;
        let end = a.length;

        while (swapped == true) {

            // reset the swapped flag on entering the
            // loop, because it might be true from a
            // previous iteration.
            swapped = false;

            // loop from bottom to top same as
            // the bubble sort
            for (let i = start; i < end - 1; ++i) {
                if (a[i] > a[i + 1]) {
                    let temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // if nothing moved, then array is sorted.
            if (swapped == false)
                break;

            // otherwise, reset the swapped flag so that it
            // can be used in the next stage
            swapped = false;

            // move the end point back by one, because
            // item at the end is in its rightful spot
            end = end - 1;

            // from top to bottom, doing the
            // same comparison as in the previous stage
            for (let i = end - 1; i >= start; i--) {
                if (a[i] > a[i + 1]) {
                    let temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // increase the starting point, because
            // the last stage would have moved the next
            // smallest number to its rightful spot.
            start = start + 1;
        }
    }

    /* Prints the array */
    function printArray(a)
    {
        let n = a.length;
        for (let i = 0; i < n; i++)
            document.write(a[i] + " ");
        document.write("</br>");
    }

    let a = [ 5, 1, 4, 2, 8, 0, 2 ];
    cocktailSort(a);
    document.write("Sorted array :" + "</br>");
    printArray(a);

    // This code is contributed by decode2207.
</script>
```

**Output**

```
Sorted array :
0 1 2 2 4 5 8 
```

**最坏和平均情况时间复杂度:** O(n*n)。
**最佳案例时间复杂度:** O(n)。最佳情况发生在数组已经排序的时候。
**辅助空间:** O(1)
**排序到位:**是
**稳定:**是
**与冒泡排序的比较:**
时间复杂度相同，但鸡尾酒表现优于冒泡排序。一般来说，鸡尾酒分类的速度比泡沫分类快不到两倍。考虑这个例子(2，3，4，5，1)。对于这个例子，冒泡排序需要四次数组遍历，而鸡尾酒排序只需要两次遍历。(来源[维基](https://en.wikipedia.org/wiki/Cocktail_shaker_sort) )
**参考文献:**

*   **https://en . Wikipedia . org/wiki/鸡尾酒 _shaker_sort**
*   [**http://will.thimbleby.net/algorithms/doku.php?id =鸡尾酒 _ 排序**](http://will.thimbleby.net/algorithms/doku.php?id=cocktail_sort)
*   [**http://www . programming-algorithms . net/article/40270/Shaker-sort**](http://www.programming-algorithms.net/article/40270/Shaker-sort)

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。