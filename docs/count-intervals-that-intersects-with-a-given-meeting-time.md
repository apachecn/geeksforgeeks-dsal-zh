# 计算与给定会议时间相交的时间间隔

> 原文:[https://www . geesforgeks . org/count-intervals-与给定会议时间相交的时间间隔/](https://www.geeksforgeeks.org/count-intervals-that-intersects-with-a-given-meeting-time/)

给定一个由代表开始和结束时间(以 [12 小时格式](https://en.wikipedia.org/wiki/24-hour_clock))的**N**T6】对串[和代表会议时间的](https://www.geeksforgeeks.org/stringstream-c-applications/)[串](https://www.geeksforgeeks.org/string-data-structure/) **P** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr[]【2】**，任务是找出包含时间的间隔计数**P**

**示例:**

> **输入:**P =“12:01:AM”，arr[][2]= {“12:00:AM”、“11:55:PM”}、{“12:01:AM”、“11:50:AM”}、{“12:30:AM”、“12:00:PM”}、{“11:57:AM”、“11:59:PM”} }
> **输出:** 2
> **解释:【T7**
> 
> **输入:**P =“12:01:AM”，arr[][2]= { {“09:57:AM”，“12:00:PM”}
> T3】输出:0
> T6】说明:无区间包含时间 P

**进场:**思路是先[把所有时间从 12 小时格式转换成 24 小时格式](https://www.geeksforgeeks.org/program-convert-time-12-hour-24-hour-format/)然后和时间 **P** 进行范围对比。按照以下步骤解决问题:

*   首先[将 12 小时格式的所有时间转换为 24 小时格式](https://www.geeksforgeeks.org/program-convert-time-12-hour-24-hour-format/)，然后存储 24 小时时间格式的整数值。
*   初始化一个变量，比如说 **ans，**来存储 **P** 所在的时间间隔的计数。
*   [若 **(P ≥ L & & P ≤ R)** 或 **(P ≥ R & & P ≤ L)** ，则遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将 **ans** 的计数增加 **1** 。
*   最后，完成以上步骤后，打印 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert a time in 24
// hour format to an equivalent integer
int convert(string str)
{
    // Removes ":" at 3rd position
    str.replace(2, 1, "");

    // Calculate hours
    int h1 = (int)str[1] - '0';
    int h2 = (int)str[0] - '0';
    int hh = (h2 * 10 + h1 % 10);

    // Stores the time in 24 hours format
    int time = 0;

    // If time is in "AM"
    if (str[5] == 'A') {

        // If hh is equal to 12
        if (hh == 12)
            time += stoi(str.substr(2, 2));

        else {
            time += stoi(str.substr(0, 2));
        }
    }

    // If time is in "PM"
    else {

        // If hh is equal to 12
        if (hh == 12) {

            time += stoi(str.substr(0, 4));
        }
        else {

            time += stoi(str.substr(0, 4));
            time += 1200;
        }
    }

    // Return time
    return time;
}
// Function to count number
// of intervals in which p lies
int countOverlap(string arr[][2],
                 int n, string p)
{
    // Stores the count
    int ans = 0;

    // Stores the integer value of
    // 24 hours time format of P
    int M = convert(p);

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Stores the integer value of
        // 24 hours time format of arr[i][0]
        int L = convert(arr[i][0]);

        // Stores the integer value of
        // 24 hours time format of arr[i][1]
        int R = convert(arr[i][1]);

        // If M lies within the [L, R]
        if ((L <= M && M <= R)
            || (M >= R && M <= L))
            // Increment ans by 1
            ans++;
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    string arr[][2] = { { "12:00:AM", "11:55:PM" },
                        { "12:01:AM", "11:50:AM" },
                        { "12:30:AM", "12:00:PM" },
                        { "11:57:AM", "11:59:PM" } };
    string P = "12:01:PM";
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countOverlap(arr, N, P) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
class GFG
{

    // Function to convert a time in 24
    // hour format to an equivalent integer
    static int convert(String str)
    {

        // Removes ":" at 3rd position
        str = str.substring(0, 2) + str.substring(3);

        // Calculate hours
        int h1 = (int)str.charAt(1) - '0';
        int h2 = (int)str.charAt(0) - '0';
        int hh = (h2 * 10 + h1 % 10);

        // Stores the time in 24 hours format
        int time = 0;

        // If time is in "AM"
        if (str.charAt(5) == 'A') {

            // If hh is equal to 12
            if (hh == 12)
                time += Integer.parseInt(
                    str.substring(2, 4));

            else {
                time += Integer.parseInt(
                    str.substring(0, 2));
            }
        }

        // If time is in "PM"
        else {

            // If hh is equal to 12
            if (hh == 12) {
                time += Integer.parseInt(
                    str.substring(0, 4));
            }
            else {

                time += Integer.parseInt(
                    str.substring(0, 4));
                time += 1200;
            }
        }

        // Return time
        return time;
    }

    // Function to count number
    // of intervals in which p lies
    static int countOverlap(String arr[][], int n, String p)
    {

        // Stores the count
        int ans = 0;

        // Stores the integer value of
        // 24 hours time format of P
        int M = convert(p);

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // Stores the integer value of
            // 24 hours time format of arr[i][0]
            int L = convert(arr[i][0]);

            // Stores the integer value of
            // 24 hours time format of arr[i][1]
            int R = convert(arr[i][1]);

            // If M lies within the [L, R]
            if ((L <= M && M <= R) || (M >= R && M <= L))

                // Increment ans by 1
                ans++;
        }

        // Return ans
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String[][] arr
            = new String[][] { { "12:00:AM", "11:55:PM" },
                               { "12:01:AM", "11:50:AM" },
                               { "12:30:AM", "12:00:PM" },
                               { "11:57:AM", "11:59:PM" } };
        String P = "12:01:PM";
        int N = arr.length;

        System.out.println(countOverlap(arr, N, P));
    }
}

// This code is contributed by Dharanendra L V
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to convert a time in 24
// hour format to an equivalent integer
static int convert(String str)
{

    // Removes ":" at 3rd position
    str = str.Substring(0, 2) + str.Substring(3);

    // Calculate hours
    int h1 = (int)str[1] - '0';
    int h2 = (int)str[0] - '0';
    int hh = (h2 * 10 + h1 % 10);

    // Stores the time in 24 hours format
    int time = 0;

    // If time is in "AM"
    if (str[5] == 'A')
    {

        // If hh is equal to 12
        if (hh == 12)
            time += Int32.Parse(
                str.Substring(2, 2));

        else
        {
            time += Int32.Parse(
                str.Substring(0, 2));
        }
    }

    // If time is in "PM"
    else
    {

        // If hh is equal to 12
        if (hh == 12)
        {
            time += Int32.Parse(
                str.Substring(0, 4));
        }
        else
        {
            time += Int32.Parse(
                str.Substring(0, 4));
            time += 1200;
        }
    }

    // Return time
    return time;
}

// Function to count number
// of intervals in which p lies
static int countOverlap(String [,]arr, int n,
                        String p)
{

    // Stores the count
    int ans = 0;

    // Stores the integer value of
    // 24 hours time format of P
    int M = convert(p);

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Stores the integer value of
        // 24 hours time format of arr[i,0]
        int L = convert(arr[i,0]);

        // Stores the integer value of
        // 24 hours time format of arr[i,1]
        int R = convert(arr[i,1]);

        // If M lies within the [L, R]
        if ((L <= M && M <= R) ||
            (M >= R && M <= L))

            // Increment ans by 1
            ans++;
    }

    // Return ans
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String[,] arr = new String[,]{
         { "12:00:AM", "11:55:PM" },
         { "12:01:AM", "11:50:AM" },
         { "12:30:AM", "12:00:PM" },
         { "11:57:AM", "11:59:PM" } };
    String P = "12:01:PM";
    int N = arr.GetLength(0);

    Console.WriteLine(countOverlap(arr, N, P));
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)