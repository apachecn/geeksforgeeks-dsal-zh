# 如何在 C/C++中对日期数组进行排序？

> 原文:[https://www . geesforgeks . org/如何对 cc 中的日期数组进行排序/](https://www.geeksforgeeks.org/how-to-sort-an-array-of-dates-in-cc/)

给定一系列日期，如何对它们进行排序。

**示例:**

```
Input:
       Date arr[] = {{20,  1, 2014},
                    {25,  3, 2010},
                    { 3, 12, 1676},
                    {18, 11, 1982},
                    {19,  4, 2015},
                    { 9,  7, 2015}}

Output:
      Date arr[] = {{ 3, 12, 1676},
                    {18, 11, 1982},
                    {25,  3, 2010},
                    {20,  1, 2014},
                    {19,  4, 2015},
                    { 9,  7, 2015}}

```

**强烈建议你尽量减少浏览器，先自己试试这个**
想法是用内置函数来[c++中的排序函数](http://www.cplusplus.com/reference/algorithm/sort/)。我们可以编写自己的比较函数，首先比较年，然后月，然后天。

下面是一个完整的 C++程序。

```
// C++ program to sort an array of dates
#include<bits/stdc++.h>
using namespace std;

// Structure for date
struct Date
{
    int day, month, year;
};

// This is the compare function used by the in-built sort
// function to sort the array of dates.
// It takes two Dates as parameters (const is
// given to tell the compiler that the value won't be
// changed during the compare - this is for optimization..)

// Returns true if dates have to be swapped and returns
// false if not. Since we want ascending order, we return
// true if the first Date is less than the second date
bool compare(const Date &d1, const Date &d2)
{
    // All cases when true should be returned
    if (d1.year < d2.year)
        return true;
    if (d1.year == d2.year && d1.month < d2.month)
        return true;
    if (d1.year == d2.year && d1.month == d2.month &&
                              d1.day < d2.day)
        return true;

    // If none of the above cases satisfy, return false
    return false;
}

// Function to sort array arr[0..n-1] of dates
void sortDates(Date arr[], int n)
{
    // Calling in-built sort function.
    // First parameter array beginning,
    // Second parameter - array ending,
    // Third is the custom compare function
    sort(arr, arr+n, compare);
}

// Driver Program
int main()
{
    Date arr[] = {{20,  1, 2014},
                  {25,  3, 2010},
                  { 3, 12, 1676},
                  {18, 11, 1982},
                  {19,  4, 2015},
                  { 9,  7, 2015}};
    int n = sizeof(arr)/sizeof(arr[0]);

    sortDates(arr, n);

    cout << "Sorted dates are\n";
    for (int i=0; i<n; i++)
    {
        cout << arr[i].day << " " << arr[i].month
             << " " << arr[i].year;
        cout << endl;
    }
}
```

输出:

```
Sorted dates are
3 12 1676
18 11 1982
25 3 2010
20 1 2014
19 4 2015
9 7 2015
```

同样在 C 中，我们可以使用 [qsort()](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/) 函数。

相关问题:
[如何高效排序 20 年代的大名单日期](https://www.geeksforgeeks.org/how-to-efficiently-sort-a-big-list-dates-in-20s/)

本文由 [**Dinesh T.P.D**](https://www.facebook.com/Dinesh.TP) 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论