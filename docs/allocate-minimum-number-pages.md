# 分配最小页数

> 原文:[https://www . geesforgeks . org/allocate-最小页数/](https://www.geeksforgeeks.org/allocate-minimum-number-pages/)

给定 n 本不同的书和 m 个学生的页数。这些书按页数的升序排列。每个学生都被指定连续读一些书。任务是以分配给学生的最大页数最少的方式分配书籍。
**例:**

```
Input : pages[] = {12, 34, 67, 90}
        m = 2
Output : 113
Explanation:
There are 2 number of students. Books can be distributed 
in following fashion : 
  1) [12] and [34, 67, 90]
      Max number of pages is allocated to student 
      2 with 34 + 67 + 90 = 191 pages
  2) [12, 34] and [67, 90]
      Max number of pages is allocated to student
      2 with 67 + 90 = 157 pages 
  3) [12, 34, 67] and [90]
      Max number of pages is allocated to student 
      1 with 12 + 34 + 67 = 113 pages

Of the 3 cases, Option 3 has the minimum pages = 113\. 
```

想法是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。我们将页数固定为当前最小值和最大值的中间值。我们将最小值和最大值分别初始化为 0 和所有页面的总和。如果当前的 mid 可以是一个解决方案，那么我们在下半部分搜索，否则我们在上半部分搜索。
现在问题来了，如何检查中间值是否可行？基本上，我们需要检查是否可以以最大数量不超过当前值的方式为所有学生分配页面。为此，我们依次为每个学生分配页面，同时当前分配的页面数量不超过该值。在这个过程中，如果学生的数量变得超过 m，那么解决方案是不可行的。否则可行。
以下是上述思路的一个实现。

## C++

```
// C++ program for optimal allocation of pages
#include<bits/stdc++.h>
using namespace std;

// Utility function to check if current minimum value
// is feasible or not.
bool isPossible(int arr[], int n, int m, int curr_min)
{
    int studentsRequired = 1;
    int curr_sum = 0;

    // iterate over all books
    for (int i = 0; i < n; i++)
    {
        // check if current number of pages are greater
        // than curr_min that means we will get the result
        // after mid no. of pages
        if (arr[i] > curr_min)
            return false;

        // count how many students are required
        // to distribute curr_min pages
        if (curr_sum + arr[i] > curr_min)
        {
            // increment student count
            studentsRequired++;

            // update curr_sum
            curr_sum = arr[i];

            // if students required becomes greater
            // than given no. of students,return false
            if (studentsRequired > m)
                return false;
        }

        // else update curr_sum
        else
            curr_sum += arr[i];
    }
    return true;
}

// function to find minimum pages
int findPages(int arr[], int n, int m)
{
    long long sum = 0;

    // return -1 if no. of books is less than
    // no. of students
    if (n < m)
        return -1;

    // Count total number of pages
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // initialize start as 0 pages and end as
    // total pages
    int start = 0, end = sum;
    int result = INT_MAX;

    // traverse until start <= end
    while (start <= end)
    {
        // check if it is possible to distribute
        // books by using mid as current minimum
        int mid = (start + end) / 2;
        if (isPossible(arr, n, m, mid))
        {
            // update result to current distribution
              // as it's the best we have found till now.
              result = mid;

            // as we are finding minimum and books
            // are sorted so reduce end = mid -1
            // that means
            end = mid - 1;
        }

        else
            // if not possible means pages should be
            // increased so update start = mid + 1
            start = mid + 1;
    }

    // at-last return minimum no. of  pages
    return result;
}

// Drivers code
int main()
{
    //Number of pages in books
    int arr[] = {12, 34, 67, 90};
    int n = sizeof arr / sizeof arr[0];
    int m = 2; //No. of students

    cout << "Minimum number of pages = "
         << findPages(arr, n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for optimal allocation of pages

public class GFG
{
    // Utility method to check if current minimum value
    // is feasible or not.
    static boolean isPossible(int arr[], int n, int m, int curr_min)
    {
        int studentsRequired = 1;
        int curr_sum = 0;

        // iterate over all books
        for (int i = 0; i < n; i++)
        {
            // check if current number of pages are greater
            // than curr_min that means we will get the result
            // after mid no. of pages
            if (arr[i] > curr_min)
                return false;

            // count how many students are required
            // to distribute curr_min pages
            if (curr_sum + arr[i] > curr_min)
            {
                // increment student count
                studentsRequired++;

                // update curr_sum
                curr_sum = arr[i];

                // if students required becomes greater
                // than given no. of students,return false
                if (studentsRequired > m)
                    return false;
            }

            // else update curr_sum
            else
                curr_sum += arr[i];
        }
        return true;
    }

    // method to find minimum pages
    static int findPages(int arr[], int n, int m)
    {
        long sum = 0;

        // return -1 if no. of books is less than
        // no. of students
        if (n < m)
            return -1;

        // Count total number of pages
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // initialize start as 0 pages and end as
        // total pages
        int start = 0, end = (int) sum;
        int result = Integer.MAX_VALUE;

        // traverse until start <= end
        while (start <= end)
        {
            // check if it is possible to distribute
            // books by using mid is current minimum
            int mid = (start + end) / 2;
            if (isPossible(arr, n, m, mid))
            {
                // update result to current distribution
                // as it's the best we have found till now.
                result = mid;

                // as we are finding minimum and books
                // are sorted so reduce end = mid -1
                // that means
                end = mid - 1;
            }

            else
                // if not possible means pages should be
                // increased so update start = mid + 1
                start = mid + 1;
        }

        // at-last return minimum no. of  pages
        return result;
    }

    // Driver Method
    public static void main(String[] args)
    {
        //Number of pages in books
        int arr[] = {12, 34, 67, 90};

        int m = 2; //No. of students

        System.out.println("Minimum number of pages = " +
                          findPages(arr, arr.length, m));
    }
}
```

## 蟒蛇 3

```
# Python3 program for optimal allocation of pages

# Utility function to check if
# current minimum value is feasible or not.
def isPossible(arr, n, m, curr_min):
    studentsRequired = 1
    curr_sum = 0

    # iterate over all books
    for i in range(n):

        # check if current number of pages are
        # greater than curr_min that means
        # we will get the result after
        # mid no. of pages
        if (arr[i] > curr_min):
            return False

        # count how many students are required
        # to distribute curr_min pages
        if (curr_sum + arr[i] > curr_min):

            # increment student count
            studentsRequired += 1

            # update curr_sum
            curr_sum = arr[i]

            # if students required becomes greater
            # than given no. of students, return False
            if (studentsRequired > m):
                return False

        # else update curr_sum
        else:
            curr_sum += arr[i]

    return True

# function to find minimum pages
def findPages(arr, n, m):

    sum = 0

    # return -1 if no. of books is
    # less than no. of students
    if (n < m):
        return -1

    # Count total number of pages
    for i in range(n):
        sum += arr[i]

    # initialize start as 0 pages and
    # end as total pages
    start, end = 0, sum
    result = 10**9

    # traverse until start <= end
    while (start <= end):

        # check if it is possible to distribute
        # books by using mid as current minimum
        mid = (start + end) // 2
        if (isPossible(arr, n, m, mid)):

            # update result to current distribution
              # as it's the best we have found till now.
            result = mid

            # as we are finding minimum and books
            # are sorted so reduce end = mid -1
            # that means
            end = mid - 1

        else:
            # if not possible means pages should be
            # increased so update start = mid + 1
            start = mid + 1

    # at-last return minimum no. of pages
    return result

# Driver Code

# Number of pages in books
arr = [12, 34, 67, 90]
n = len(arr)
m = 2   # No. of students

print("Minimum number of pages = ",
              findPages(arr, n, m))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for optimal
// allocation of pages
using System;

class GFG
{

// Utility function to check
// if current minimum value
// is feasible or not.
static bool isPossible(int []arr, int n,
                       int m, int curr_min)
{
    int studentsRequired = 1;
    int curr_sum = 0;

    // iterate over all books
    for (int i = 0; i < n; i++)
    {
        // check if current number of
        // pages are greater than curr_min
        // that means we will get the
        // result after mid no. of pages
        if (arr[i] > curr_min)
            return false;

        // count how many students
        // are required to distribute
        // curr_min pages
        if (curr_sum + arr[i] > curr_min)
        {
            // increment student count
            studentsRequired++;

            // update curr_sum
            curr_sum = arr[i];

            // if students required becomes
            // greater than given no. of
            // students, return false
            if (studentsRequired > m)
                return false;
        }

        // else update curr_sum
        else
            curr_sum += arr[i];
    }
    return true;
}

// function to find minimum pages
static int findPages(int []arr,
                     int n, int m)
{
    long sum = 0;

    // return -1 if no. of books
    // is less than no. of students
    if (n < m)
        return -1;

    // Count total number of pages
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // initialize start as 0 pages
    // and end as total pages
    int start = 0, end = (int)sum;
    int result = int.MaxValue;

    // traverse until start <= end
    while (start <= end)
    {
        // check if it is possible to
        // distribute books by using
        // mid as current minimum
        int mid = (start + end) / 2;
        if (isPossible(arr, n, m, mid))
        {
            // update result to current distribution
              // as it's the best we have found till now.
              result = mid;

            // as we are finding minimum and
            // books are sorted so reduce
            // end = mid -1 that means
            end = mid - 1;
        }

        else
            // if not possible means pages
            // should be increased so update
            // start = mid + 1
            start = mid + 1;
    }

    // at-last return
    // minimum no. of pages
    return result;
}

// Drivers code
static public void Main ()
{

//Number of pages in books
int []arr = {12, 34, 67, 90};
int n = arr.Length;
int m = 2; // No. of students

Console.WriteLine("Minimum number of pages = " +
                          findPages(arr, n, m));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for optimal allocation
// of pages

// Utility function to check if current
// minimum value is feasible or not.

function isPossible($arr, $n, $m,
                    $curr_min)
{
    $studentsRequired = 1;
    $curr_sum = 0;

    // iterate over all books
    for ( $i = 0; $i < $n; $i++)
    {
        // check if current number of pages
        // are greater than curr_min that
        // means we will get the result
        // after mid no. of pages
        if ($arr[$i] > $curr_min)
            return false;

        // count how many students are
        // required to distribute
        // curr_min pages
        if ($curr_sum + $arr[$i] > $curr_min)
        {
            // increment student count
            $studentsRequired++;

            // update curr_sum
            $curr_sum = $arr[$i];

            // if students required becomes
            // greater than given no. of
            // students, return false
            if ($studentsRequired > $m)
                return false;
        }

        // else update curr_sum
        else
            $curr_sum += $arr[$i];
    }
    return true;
}

// function to find minimum pages
function findPages($arr, $n, $m)
{
    $sum = 0;

    // return -1 if no. of books is
    // less than no. of students
    if ($n < $m)
        return -1;

    // Count total number of pages
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // initialize start as 0 pages
    // and end as total pages
    $start = 0;
    $end = $sum;
    $result = PHP_INT_MAX;

    // traverse until start <= end
    while ($start <= $end)
    {
        // check if it is possible to
        // distribute books by using
        // mid as current minimum
        $mid = (int)($start + $end) / 2;
        if (isPossible($arr, $n, $m, $mid))
        {
            // update result to current distribution
              // as it's the best we have found till now
            $result = $mid;

            // as we are finding minimum and
            // books are sorted so reduce
            // end = mid -1 that means
            $end = $mid - 1;
        }

        else
            // if not possible means pages
            // should be increased so update
            // start = mid + 1
            $start = $mid + 1;
    }

    // at-last return minimum
    // no. of pages
    return $result;
}

// Driver code

// Number of pages in books
$arr = array(12, 34, 67, 90);
$n = count($arr);
$m = 2; // No. of students

echo "Minimum number of pages = ",
    findPages($arr, $n, $m), "\n";

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>
// Javascript program for optimal allocation of pages

// Utility method to check if current minimum value
    // is feasible or not.
function isPossible(arr,n,m,curr_min)
{
    let studentsRequired = 1;
    let curr_sum = 0;

    // iterate over all books
    for (let i = 0; i < n; i++)
    {
        // check if current number of pages are greater
        // than curr_min that means we will get the result
        // after mid no. of pages
        if (arr[i] > curr_min)
            return false;

        // count how many students are required
        // to distribute curr_min pages
        if (curr_sum + arr[i] > curr_min)
        {
            // increment student count
            studentsRequired++;

            // update curr_sum
            curr_sum = arr[i];

            // if students required becomes greater
            // than given no. of students,return false
            if (studentsRequired > m)
                return false;
        }

        // else update curr_sum
        else
            curr_sum += arr[i];
    }
    return true;
}

// method to find minimum pages
function findPages(arr,n,m)
{
    let sum = 0;

    // return -1 if no. of books is less than
    // no. of students
    if (n < m)
        return -1;

    // Count total number of pages
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // initialize start as 0 pages and end as
    // total pages
    let start = 0, end = sum;
    let result = Number.MAX_VALUE;

    // traverse until start <= end
    while (start <= end)
    {
        // check if it is possible to distribute
        // books by using mid as current minimum
        let mid =Math.floor( (start + end) / 2);
        if (isPossible(arr, n, m, mid))
        {
            // if yes then find the minimum distribution
            result = Math.min(result, mid);

            // as we are finding minimum and books
            // are sorted so reduce end = mid -1
            // that means
            end = mid - 1;
        }

        else
            // if not possible means pages should be
            // increased so update start = mid + 1
            start = mid + 1;
    }

    // at-last return minimum no. of  pages
    return result;
}

// Driver Method
let arr=[12, 34, 67, 90];
let m = 2; //No. of students
document.write("Minimum number of pages = " +
                          findPages(arr, arr.length, m));

// This code is contributed by patel2127
</script>
```

**输出:**

```
Minimum number of pages = 113
```

本文由 [**萨希尔·查布拉(akku)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。