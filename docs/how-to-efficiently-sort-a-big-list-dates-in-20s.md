# 如何高效排序 20 年代的大名单日期

> 原文:[https://www . geeksforgeeks . org/如何高效排序大列表-日期在 20 秒内/](https://www.geeksforgeeks.org/how-to-efficiently-sort-a-big-list-dates-in-20s/)

给定一个 20 年代的日期大列表，如何高效地对列表进行排序。

**例:**

```
Input:
       Date arr[] = {{20,  1, 2014},
                    {25,  3, 2010},
                    { 3, 12, 2000},
                    {18, 11, 2001},
                    {19,  4, 2015},
                    { 9,  7, 2005}}
Output:
      Date arr[] = {{ 3, 12, 2000},
                    {18, 11, 2001},
                    { 9,  7, 2005},
                    {25,  3, 2010},
                    {20,  1, 2014},
                    {19,  4, 2015}}
```

一个简单的解决方案是使用类似[合并排序](http://geeksquiz.com/merge-sort/)的 O(N log N)算法和自定义比较器。但是我们可以使用[基数排序](https://www.geeksforgeeks.org/radix-sort/)在 O(n)时间内对列表进行排序。在典型的[基数排序](https://www.geeksforgeeks.org/radix-sort/)实现中，我们首先按最后一个数字排序，然后按倒数第二个数字排序，以此类推。强烈建议首先通过基数排序来理解这个方法。在该方法中，我们按照以下顺序排序:

*   Use counting sort first.
*   Sort by day, and then use counting sort.
*   Sort by month, and finally use counting sort.

按年排序

由于天数、月数和年数是固定的，因此这三个步骤都需要 O(n)个时间。因此，整体时间复杂度为 O(n)。

下面是上述思路的 C++实现:

## c++

```
// C++ program to sort an array
// of dates using Radix Sort

#include <bits/stdc++.h>
using namespace std;

// Utilitiy function to obtain
// maximum date or month or year
int getMax(int arr[][3],int n, int q)
{
    int maxi = INT_MIN;
    for(int i=0;i<n;i++){
        maxi = max(maxi,arr[i][q]);
    }
    return maxi;
}

// A function to do counting sort of arr[]
// according to given q i.e.
// (0 for day, 1 for month, 2 for year)
void sortDatesUtil(int arr[][3],
                   int n, int q)
{
    int maxi = getMax(arr,n,q);
    int p = 1;
    while(maxi>0){
        //to extract last digit  divide
        // by p then %10
        // Store count of occurrences in cnt[]
        int cnt[10]={0};

        for(int i=0;i<n;i++)
        {
            cnt[(arr[i][q]/p)%10]++;
        }
        for(int i=1;i<10;i++)
        {
            cnt[i]+=cnt[i-1];
        }
        int ans[n][3];
        for(int i=n-1;i>=0;i--)
        {
            int lastDigit = (arr[i][q]/p)%10;

            // Build the output array
            for(int j=0;j<3;j++)
            {
                ans[cnt[lastDigit]-1][j]
                  =arr[i][j];   
            }
            cnt[lastDigit]--;
        }
        // Copy the output array to arr[],
        // so that arr[] now
        // contains sorted numbers
        // according to current digit
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<3;j++)
            {
                arr[i][j] = ans[i][j];
            }
        }
        // update p to get
        // the next digit
        p*=10;
        maxi/=10;
    }
}

// The main function that sorts
// array of dates
// using Radix Sort
void sortDates(int dates[][3], int n)
{
    // First sort by day
    sortDatesUtil(dates, n, 0);

    // Then by month
    sortDatesUtil(dates, n, 1);
    // Finally by year
    sortDatesUtil(dates, n, 2);
}

// A utility function to print an array
void printArr(int arr[][3], int n)
{
   for(int i=0;i<6;i++)
   {
        for(int j=0;j<3;j++)
        {
            cout<<arr[i][j]<<" ";
        }
        cout<<endl;
    }
}

// Driver Code
int main()
{
    int dates[][3] = {{20,  1, 2014},
                    {25,  3, 2010},
                    { 3, 12, 2000},
                    {18, 11, 2000},
                    {19,  4, 2015},
                    { 9,  7, 2005}};
    int n = sizeof(dates)/sizeof(dates[0]);

    // Function Call
    sortDates(dates,n);
    cout<<"\nSorted Dates\n";
    printArr(dates,n);
    return 0;
}
```

## Java

```
// Java program to sort an array
// of dates using Radix Sort
import java.util.*;
class GFG{

// Utilitiy function to obtain
// maximum date or month or year
static int getMax(int arr[][], int n, int q)
{
    int maxi = Integer.MIN_VALUE;
    for(int i = 0; i < n; i++)
    {
        maxi = Math.max(maxi, arr[i][q]);
    }
    return maxi;
}

// A function to do counting sort of arr[]
// according to given q i.e.
// (0 for day, 1 for month, 2 for year)
static void sortDatesUtil(int arr[][],
                   int n, int q)
{
    int maxi = getMax(arr,n,q);
    int p = 1;
    while(maxi > 0)
    {
        // to extract last digit  divide
        // by p then %10
        // Store count of occurrences in cnt[]
        int []cnt = new int[10];

        for(int i = 0; i < n; i++)
        {
            cnt[(arr[i][q]/p) % 10]++;
        }
        for(int i = 1; i < 10; i++)
        {
            cnt[i] += cnt[i - 1];
        }
        int [][]ans = new int[n][3];
        for(int i = n - 1; i >= 0; i--)
        {
            int lastDigit = (arr[i][q]/p) % 10;

            // Build the output array
            for(int j = 0; j < 3; j++)
            {
                ans[cnt[lastDigit]-1][j]
                  =arr[i][j];   
            }
            cnt[lastDigit]--;
        }

        // Copy the output array to arr[],
        // so that arr[] now
        // contains sorted numbers
        // according to current digit
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < 3; j++)
            {
                arr[i][j] = ans[i][j];
            }
        }

        // update p to get
        // the next digit
        p *= 10;
        maxi /= 10;
    }
}

// The main function that sorts
// array of dates
// using Radix Sort
static void sortDates(int dates[][], int n)
{

    // First sort by day
    sortDatesUtil(dates, n, 0);

    // Then by month
    sortDatesUtil(dates, n, 1);
    // Finally by year
    sortDatesUtil(dates, n, 2);
}

// A utility function to print an array
static void printArr(int arr[][], int n)
{
   for(int i = 0; i < 6; i++)
   {
        for(int j = 0; j < 3; j++)
        {
            System.out.print(arr[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int dates[][] = {{20,  1, 2014},
                    {25,  3, 2010},
                    { 3, 12, 2000},
                    {18, 11, 2000},
                    {19,  4, 2015},
                    { 9,  7, 2005}};
    int n = dates.length;

    // Function Call
    sortDates(dates,n);
    System.out.print("\nSorted Dates\n");
    printArr(dates,n);
}
}

// This code is contributed by Rajput-Ji
```

## python 3

T2T19】c#T21

```
// C# program to sort an array
// of dates using Radix Sort
using System;
public class GFG
{

// Utilitiy function to obtain
// maximum date or month or year
static int getMax(int [,]arr, int n, int q)
{
    int maxi = int.MinValue;
    for(int i = 0; i < n; i++)
    {
        maxi = Math.Max(maxi, arr[i,q]);
    }
    return maxi;
}

// A function to do counting sort of []arr
// according to given q i.e.
// (0 for day, 1 for month, 2 for year)
static void sortDatesUtil(int [,]arr,
                   int n, int q)
{
    int maxi = getMax(arr,n,q);
    int p = 1;
    while(maxi > 0)
    {
        // to extract last digit  divide
        // by p then %10
        // Store count of occurrences in cnt[]
        int []cnt = new int[10];

        for(int i = 0; i < n; i++)
        {
            cnt[(arr[i,q]/p) % 10]++;
        }
        for(int i = 1; i < 10; i++)
        {
            cnt[i] += cnt[i - 1];
        }
        int [,]ans = new int[n,3];
        for(int i = n - 1; i >= 0; i--)
        {
            int lastDigit = (arr[i,q]/p) % 10;

            // Build the output array
            for(int j = 0; j < 3; j++)
            {
                ans[cnt[lastDigit]-1,j]
                  =arr[i,j];   
            }
            cnt[lastDigit]--;
        }

        // Copy the output array to []arr,
        // so that []arr now
        // contains sorted numbers
        // according to current digit
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < 3; j++)
            {
                arr[i,j] = ans[i,j];
            }
        }

        // update p to get
        // the next digit
        p *= 10;
        maxi /= 10;
    }
}

// The main function that sorts
// array of dates
// using Radix Sort
static void sortDates(int [,]dates, int n)
{

    // First sort by day
    sortDatesUtil(dates, n, 0);

    // Then by month
    sortDatesUtil(dates, n, 1);
    // Finally by year
    sortDatesUtil(dates, n, 2);
}

// A utility function to print an array
static void printArr(int [,]arr, int n)
{
   for(int i = 0; i < 6; i++)
   {
        for(int j = 0; j < 3; j++)
        {
            Console.Write(arr[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{
    int [,]dates = {{20,  1, 2014},
                    {25,  3, 2010},
                    { 3, 12, 2000},
                    {18, 11, 2000},
                    {19,  4, 2015},
                    { 9,  7, 2005}};
    int n = dates.GetLength(0);

    // Function Call
    sortDates(dates,n);
    Console.Write("\nSorted Dates\n");
    printArr(dates,n);
}
}

// This code is contributed by aashish1995.
```

T22

## Javascript

T4T29】输出 T5

本文由 [**tpriyanshu**](https://tpriyanshu.bitbucket.io) 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论