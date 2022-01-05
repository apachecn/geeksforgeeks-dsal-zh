# 从具有相同位数总和的两个数组中计数不同的对

> 原文:[https://www . geesforgeks . org/count-distinct-pairs-from-two-array-具有相同的数字总和/](https://www.geeksforgeeks.org/count-distinct-pairs-from-two-arrays-having-same-sum-of-digits/)

给定两个数组 arr1[]和 arr2[]。任务是找到**个不同的**对的总数(从 arr1 中选取 1 个元素，从 arr2 中选取 1 个元素)，这样这一对的两个元素都有数字的总和。
**注意:**出现一次以上的对必须只统计一次。
**示例** :

```
Input : arr1[] = {33, 41, 59, 1, 3}
        arr2[] = {3, 32, 51, 3}
Output : 3
Possible pairs are:
(33, 51), (41, 32), (3, 3)

Input : arr1[] = {1, 6, 4, 22}
        arr2[] = {1, 3, 24}
Output : 2
Possible pairs are:
(1, 1), (6, 24)
```

**进场:**

*   运行两个嵌套循环，从两个数组中生成所有可能的对，从 arr1[]中获取一个元素，从 arr2[]中获取一个元素。
*   如果数字总和相等，则将对(a，b)插入一个集合，以避免重复，其中 a 是较小的元素，b 是较大的元素。
*   总对将是最终集的大小。

以下是上述方法的实现:

## C++

```
// C++ program to count total number of
// pairs having elements with same
// sum of digits

#include <bits/stdc++.h>
using namespace std;

// Function for returning
// sum of digits of a number
int digitSum(int n)
{
    int sum = 0;
    while (n > 0) {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to return the total pairs
// of elements with equal sum of digits
int totalPairs(int arr1[], int arr2[], int n, int m)
{

    // set is used to avoid duplicate pairs
    set<pair<int, int> > s;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // check sum of digits
            // of both the elements
            if (digitSum(arr1[i]) == digitSum(arr2[j])) {

                if (arr1[i] < arr2[j])
                    s.insert(make_pair(arr1[i], arr2[j]));
                else
                    s.insert(make_pair(arr2[j], arr1[i]));
            }
        }
    }

    // return size of the set
    return s.size();
}

// Driver code
int main()
{
    int arr1[] = { 100, 3, 7, 50 };
    int arr2[] = { 5, 1, 10, 4 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    int m = sizeof(arr2) / sizeof(arr2[0]);

    cout << totalPairs(arr1, arr2, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total number of
// pairs having elements with same
// sum of digits
import java.util.*;

class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function for returning
// sum of digits of a number
static int digitSum(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to return the total pairs
// of elements with equal sum of digits
static int totalPairs(int arr1[], int arr2[],
                      int n, int m)
{

    // set is used to avoid duplicate pairs
    Set<pair> s = new HashSet<>();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // check sum of digits
            // of both the elements
            if (digitSum(arr1[i]) == digitSum(arr2[j]))
            {
                if (arr1[i] < arr2[j])
                    s.add(new pair(arr1[i], arr2[j]));
                else
                    s.add(new pair(arr2[j], arr1[i]));
            }
        }
    }

    // return size of the set
    return s.size();
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 100, 3, 7, 50 };
    int arr2[] = { 5, 1, 10, 4 };
    int n = arr1.length;
    int m = arr2.length;

    System.out.println(totalPairs(arr1, arr2, n, m));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count total number of
# pairs having elements with same sum of digits

# Function for returning
# sum of digits of a number
def digitSum(n):

    Sum = 0
    while n > 0: 
        Sum += n % 10
        n = n // 10

    return Sum

# Function to return the total pairs
# of elements with equal sum of digits
def totalPairs(arr1, arr2, n, m):

    # set is used to avoid duplicate pairs
    s = set()

    for i in range(0, n): 
        for j in range(0, m): 

            # check sum of digits
            # of both the elements
            if digitSum(arr1[i]) == digitSum(arr2[j]): 

                if arr1[i] < arr2[j]:
                    s.add((arr1[i], arr2[j]))
                else:
                    s.add((arr2[j], arr1[i]))

    # return size of the set
    return len(s)

# Driver code
if __name__ == "__main__":

    arr1 = [100, 3, 7, 50] 
    arr2 = [5, 1, 10, 4]
    n = len(arr1)
    m = len(arr2)

    print(totalPairs(arr1, arr2, n, m))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count total number of
// pairs having elements with same
// sum of digits
using System;
using System.Collections.Generic;

class GFG
{

public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function for returning
// sum of digits of a number
static int digitSum(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to return the total pairs
// of elements with equal sum of digits
static int totalPairs(int []arr1, int []arr2,
                      int n, int m)
{

    // set is used to avoid duplicate pairs
    HashSet<pair> s = new HashSet<pair>();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // check sum of digits
            // of both the elements
            if (digitSum(arr1[i]) == digitSum(arr2[j]))
            {
                if (arr1[i] < arr2[j])
                    s.Add(new pair(arr1[i], arr2[j]));
                else
                    s.Add(new pair(arr2[j], arr1[i]));
            }
        }
    }

    // return size of the set
    return s.Count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = { 100, 3, 7, 50 };
    int []arr2 = { 5, 1, 10, 4 };
    int n = arr1.Length;
    int m = arr2.Length;

    Console.WriteLine(totalPairs(arr1, arr2, n, m));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to count total number of
// pairs having elements with same
// sum of digits

// Function for returning
// sum of digits of a number
function digitSum(n)
{
    var sum = 0;
    while (n > 0) {
        sum += n % 10;
        n = parseInt(n / 10);
    }
    return sum;
}

// Function to return the total pairs
// of elements with equal sum of digits
function totalPairs(arr1, arr2, n, m)
{

    // set is used to avoid duplicate pairs
    var s = new Set();

    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {

            // check sum of digits
            // of both the elements
            if (digitSum(arr1[i]) == digitSum(arr2[j])) {

                if (arr1[i] < arr2[j])
                    s.add([arr1[i], arr2[j]]);
                else
                    s.add([arr2[j], arr1[i]]);
            }
        }
    }

    // return size of the set
    return s.size;
}

// Driver code
var arr1 = [100, 3, 7, 50 ];
var arr2 = [5, 1, 10, 4 ];
var n = arr1.length;
var m = arr2.length;
document.write( totalPairs(arr1, arr2, n, m));

</script>
```

**Output:** 

```
3
```