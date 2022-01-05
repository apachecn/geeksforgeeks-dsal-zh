# 使用冒泡排序对字符串进行排序

> 原文:[https://www . geesforgeks . org/sorting-strings-using-bubble-sort-2/](https://www.geeksforgeeks.org/sorting-strings-using-bubble-sort-2/)

给定字符串数组 arr[]。使用冒泡排序对给定字符串进行排序，并显示排序后的数组。

在[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)中，每当 arr[i] > arr[i+1]时，两个连续的字符串 arr[i]和 arr[i+1]被交换。较大的值下沉到底部，因此称为下沉排序。在每一轮结束时，较小的值逐渐“冒泡”到顶部，因此称为冒泡排序。

经过所有的传递，我们得到了所有的字符串排序顺序。以上算法复杂度为 O(N <sup>2</sup> )。

让我们看看代码片段:

## C++

```
// C++ implementation

#include<bits/stdc++.h>
using namespace std;
#define MAX 100

void sortStrings(char arr[][MAX], int n)
{
    char temp[MAX];

    // Sorting strings using bubble sort
    for (int j=0; j<n-1; j++)
    {
        for (int i=j+1; i<n; i++)
        {
            if (strcmp(arr[j], arr[i]) > 0)
            {
                strcpy(temp, arr[j]);
                strcpy(arr[j], arr[i]);
                strcpy(arr[i], temp);
            }
        }
    }
}

int main()
{
    char arr[][MAX] = {"GeeksforGeeks","Quiz","Practice","Gblogs","Coding"};
    int n = sizeof(arr)/sizeof(arr[0]);

    sortStrings(arr, n);

    printf("Strings in sorted order are : ");
    for (int i=0; i<n; i++)
        printf("\n String %d is %s", i+1, arr[i]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
class GFG
{

    static int MAX = 100;

    public static void sortStrings(String[] arr, int n) 
    {
        String temp;

        // Sorting strings using bubble sort
        for (int j = 0; j < n - 1; j++)
        {
            for (int i = j + 1; i < n; i++) 
            {
                if (arr[j].compareTo(arr[i]) > 0)
                {
                    temp = arr[j];
                    arr[j] = arr[i];
                    arr[i] = temp;
                }
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String[] arr = { "GeeksforGeeks", "Quiz", 
                        "Practice", "Gblogs", "Coding" };
        int n = arr.length;
        sortStrings(arr, n);
        System.out.println("Strings in sorted order are : ");
        for (int i = 0; i < n; i++)
            System.out.println("String " + (i + 1) + " is " + arr[i]);
    }
}

// This code is contributed by
// sanjeev2552
```

## C#

```
// C# implementation 
using System;

class GFG
{
    static int MAX = 100;

    public static void sortStrings(String[] arr, 
                                   int n) 
    {
        String temp;

        // Sorting strings using bubble sort
        for (int j = 0; j < n - 1; j++)
        {
            for (int i = j + 1; i < n; i++) 
            {
                if (arr[j].CompareTo(arr[i]) > 0)
                {
                    temp = arr[j];
                    arr[j] = arr[i];
                    arr[i] = temp;
                }
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String[] arr = {"GeeksforGeeks", "Quiz", 
                        "Practice", "Gblogs", "Coding"};
        int n = arr.Length;
        sortStrings(arr, n);
        Console.WriteLine("Strings in sorted order are : ");
        for (int i = 0; i < n; i++)
            Console.WriteLine("String " + (i + 1) +
                              " is " + arr[i]);
    }
}

// This code is contributed by Princi Singh
```

**输出:**

```
Strings in sorted order are : 
 String 1 is Coding
 String 2 is Gblogs
 String 3 is GeeksforGeeks
 String 4 is Practice
 String 5 is Quiz
```

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论