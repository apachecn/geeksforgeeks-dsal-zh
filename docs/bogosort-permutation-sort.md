# 排序或排列排序

> 原文:[https://www.geeksforgeeks.org/bogosort-permutation-sort/](https://www.geeksforgeeks.org/bogosort-permutation-sort/)

BogoSort 也称为排列排序、愚蠢排序、缓慢排序、猎枪排序或猴子排序，是一种基于生成和测试范式的特别无效的算法。该算法连续生成输入的排列，直到找到一个排序的。( [Wiki](https://en.wikipedia.org/wiki/Bogosort) )
例如，如果使用 bogosort 对一副牌进行排序，它将包括检查该副牌是否有序，如果没有，则将该副牌抛向空中，随机捡起牌，并重复该过程直到该副牌被排序。

**伪代码:**

```
while not Sorted(list) do
    shuffle (list)
done
```

**示例:**
让我们考虑一个示例数组(3 2 5 1 0 4 )
4 5 0 3 2 1(第一次洗牌)
4 1 3 2 5 0(第二次洗牌)
1 0 3 2 5 4(第三次洗牌)
3 1 0 2 4 5(第四次洗牌)
1 4 5 0 3 2(第五次洗牌)
。
。
。
0 1 2 3 4 5(第 n 次洗牌)——排序数组
这里，n 是未知的，因为算法不知道结果排列将在哪个步骤出来排序。

## C++

```
// C++ implementation of Bogo Sort
#include<bits/stdc++.h>
using namespace std;

// To check if array is sorted or not
bool isSorted(int a[], int n)
{
    while ( --n > 1 )
        if (a[n] < a[n-1])
            return false;
    return true;
}

// To generate permutation of the array
void shuffle(int a[], int n)
{
    for (int i=0; i < n; i++)
        swap(a[i], a[rand()%n]);
}

// Sorts array a[0..n-1] using Bogo sort
void bogosort(int a[], int n)
{
    // if array is not sorted then shuffle
    // the array again
    while ( !isSorted(a, n) )
        shuffle(a, n);
}

// prints the array
void printArray(int a[], int n)
{
    for (int i=0; i<n; i++)
        printf("%d ", a[i]);
    printf("\n");
}

// Driver code
int main()
{
    int a[] = {3, 2, 5, 1, 0, 4};
    int n = sizeof a/sizeof a[0];
    bogosort(a, n);
    printf("Sorted array :\n");
    printArray(a,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement BogoSort
public class BogoSort
{
    // Sorts array a[0..n-1] using Bogo sort
    void bogoSort(int[] a)
    {
        // if array is not sorted then shuffle the
        // array again
        while (isSorted(a) == false)
            shuffle(a);
    }

    // To generate permutation of the array
    void shuffle(int[] a)
    {
         // Math.random() returns a double positive
         // value, greater than or equal to 0.0 and
         // less than 1.0.
         for (int i=1; i <= n; i++)
             swap(a, i, (int)(Math.random()*i));
    }

    // Swapping 2 elements
    void swap(int[] a, int i, int j)
    {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

    // To check if array is sorted or not
    boolean isSorted(int[] a)
    {
        for (int i=1; i<a.length; i++)
            if (a[i] < a[i-1])
                return false;
        return true;
    }

    // Prints the array
    void printArray(int[] arr)
    {
        for (int i=0; i<arr.length; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    public static void main(String[] args)
    {
        //Enter array to be sorted here
        int[] a = {3, 2, 5, 1, 0, 4};
        BogoSort ob = new BogoSort();

        ob.bogoSort(a);

        System.out.print("Sorted array: ");
        ob.printArray(a);
    }
}
```

## 计算机编程语言

```
# Python program for implementation of Bogo Sort
import random

# Sorts array a[0..n-1] using Bogo sort
def bogoSort(a):
    n = len(a)
    while (is_sorted(a)== False):
        shuffle(a)

# To check if array is sorted or not
def is_sorted(a):
    n = len(a)
    for i in range(0, n-1):
        if (a[i] > a[i+1] ):
            return False
    return True

# To generate permutation of the array
def shuffle(a):
    n = len(a)
    for i in range (0,n):
        r = random.randint(0,n-1)
        a[i], a[r] = a[r], a[i]

# Driver code to test above
a = [3, 2, 4, 1, 0, 5]
bogoSort(a)
print("Sorted array :")
for i in range(len(a)):
    print ("%d" %a[i]),
```

## C#

```
// C# implementation of Bogo Sort
using System;

class GFG
{
    // To Swap two given numbers
    static void Swap<T>(ref T lhs, ref T rhs)
    {
        T temp;
        temp = lhs;
        lhs = rhs;
        rhs = temp;
    }

    // To check if array is sorted or not
    public static bool isSorted(int[] a, int n)
    {
        int i = 0;
        while(i<n-1)
        {
            if(a[i]>a[i+1])
                return false;
            i++;
        }
        return true;
    }

    // To generate permutation of the array
    public static void shuffle(int[] a, int n)
    {
        Random rnd = new Random();
        for (int i=0; i < n; i++)
            Swap(ref a[i], ref a[rnd.Next(0,n)]);
    }

    // Sorts array a[0..n-1] using Bogo sort
    public static void bogosort(int[] a, int n)
    {
        // if array is not sorted then shuffle
        // the array again
        while ( !isSorted(a, n) )
            shuffle(a, n);
    }

    // prints the array
    public static void printArray(int[] a, int n)
    {
        for (int i=0; i<n; i++)
            Console.Write(a[i] + " ");
        Console.Write("\n");
    }

    // Driver code
    static void Main()
    {
        int[] a = {3, 2, 5, 1, 0, 4};
        int n = a.Length;
        bogosort(a, n);
        Console.Write("Sorted array :\n");
        printArray(a,n);
    }
    //This code is contributed by DrRoot_
}
```

**输出:**

```
Sorted array :
0 1 2 3 4 5 
```

**时间复杂度:**

*   最坏的情况:O(∞)(因为这个算法没有上限)
*   平均案例:O(n*n！)
*   最佳情况:O(n)(当给定的数组已经排序时)

**辅助空间:** O(1)
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。