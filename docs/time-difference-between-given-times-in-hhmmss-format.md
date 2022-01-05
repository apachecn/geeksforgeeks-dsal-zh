# 给定时间之间的时间差，格式为 HH:MM:SS

> 原文:[https://www . geeksforgeeks . org/time-difference-in-hhmmss-format/](https://www.geeksforgeeks.org/time-difference-between-given-times-in-hhmmss-format/)

给定 2 次 **HH: MM: SS** 格式的 **st** 和 **et** 。任务是以 **HH:MM: SS** 格式打印 **st** 与 **et** 的**时差**

示例:

> **输入** : st = 13:50:45，et = 14:55:50
> **输出** : 01:05:05
> **解释**:时间间隙为 1 小时 5 分 5 秒。
> 
> **输入** : st = 12:00:00，et = 24:00:00
> **输出** : 12:00:00
> **解释**:时间间隔为 12 小时。

**逼近**:将两个给定时间都转换为**秒**格式&即可求解任务，然后求出两者之间的**绝对差**。然后将这个绝对差值转换成 **HH:MM: SS** 格式
以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Function to find the time difference
    long long int getTimeInSeconds(string str)
    {

        vector<int> curr_time;
        istringstream ss(str);
        string token;

        while (getline(ss, token, ':')) {

            curr_time.push_back(stoi(token));
        }

        long long int t = curr_time[0] * 60 * 60
                          + curr_time[1] * 60
                          + curr_time[2];

        return t;
    }

    // Function to convert seconds back to hh::mm:ss
    // format
    string convertSecToTime(long long int t)
    {
        int hours = t / 3600;
        string hh = hours < 10 ? "0" + to_string(hours)
                               : to_string(hours);
        int min = (t % 3600) / 60;
        string mm = min < 10 ? "0" + to_string(min)
                             : to_string(min);
        int sec = ((t % 3600) % 60);
        string ss = sec < 10 ? "0" + to_string(sec)
                             : to_string(sec);
        string ans = hh + ":" + mm + ":" + ss;
        return ans;
    }

    // Function to find the time gap
    string timeGap(string st, string et)
    {

        long long int t1 = getTimeInSeconds(st);
        long long int t2 = getTimeInSeconds(et);

        long long int time_diff
            = (t1 - t2 < 0) ? t2 - t1 : t1 - t2;

        return convertSecToTime(time_diff);
    }
};

// Driver Code
int main()
{

    string st = "13:50:45", et = "14:55:50";
    Solution ob;
    cout << ob.timeGap(st, et) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the time difference
    static int getTimeInSeconds(String str) {

        String[] curr_time = str.split(":");
        int t = Integer.parseInt(curr_time[0]) * 60 * 60 + Integer.parseInt(curr_time[1]) * 60
                + Integer.parseInt(curr_time[2]);

        return t;
    }

    // Function to convert seconds back to hh::mm:ss
    // format
    static String convertSecToTime(int t) {
        int hours = t / 3600;
        String hh = hours < 10 ? "0" + Integer.toString(hours)
                : Integer.toString(hours);
        int min = (t % 3600) / 60;
        String mm = min < 10 ? "0" + Integer.toString(min)
                : Integer.toString(min);
        int sec = ((t % 3600) % 60);
        String ss = sec < 10 ? "0" + Integer.toString(sec)
                : Integer.toString(sec);
        String ans = hh + ":" + mm + ":" + ss;
        return ans;
    }

    // Function to find the time gap
    static String timeGap(String st, String et) {

        int t1 = getTimeInSeconds(st);
        int t2 = getTimeInSeconds(et);

        int time_diff = (t1 - t2 < 0) ? t2 - t1 : t1 - t2;

        return convertSecToTime(time_diff);
    }

    // Driver Code
    public static void main(String args[]) {

        String st = "13:50:45", et = "14:55:50";
        System.out.println(timeGap(st, et));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the time difference
def getTimeInSeconds(str):

    curr_time = str.split(':')

    t = (int(curr_time[0]) * 60 * 60
         + int(curr_time[1]) * 60
         + int(curr_time[2]))

    return t

# Function to convert seconds back to hh::mm:ss
# format
def convertSecToTime(t):

    hours = t // 3600
    if hours < 10:
        hh = "0" + str(hours)
    else:
        hh = str(hours)
    min = (t % 3600) // 60
    if min < 10:
        mm = "0" + str(min)
    else:
        mm = str(min)
    sec = ((t % 3600) % 60)
    if sec < 10:
        ss = "0" + str(sec)
    else:
        ss = str(sec)
    ans = hh + ":" + mm + ":" + ss
    return ans

# Function to find the time gap
def timeGap(st,  et):

    t1 = getTimeInSeconds(st)
    t2 = getTimeInSeconds(et)

    if (t1 - t2 < 0):
        time_diff = t2 - t1
    else:
        time_diff = t1 - t2

    return convertSecToTime(time_diff)

# Driver Code
if __name__ == "__main__":

    st = "13:50:45"
    et = "14:55:50"

    print(timeGap(st, et))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG {

    // Function to find the time difference
    static int getTimeInSeconds(String str) {

        String[] curr_time = str.Split(':');
        int t = Int32.Parse(curr_time[0]) * 60 * 60 + Int32.Parse(curr_time[1]) * 60
                + Int32.Parse(curr_time[2]);

        return t;
    }

    // Function to convert seconds back to hh::mm:ss
    // format
    static String convertSecToTime(int t) {
        int hours = t / 3600;
        String hh = hours < 10 ? "0" + hours.ToString()
                : hours.ToString();
        int min = (t % 3600) / 60;
        String mm = min < 10 ? "0" + min.ToString()
                : min.ToString();
        int sec = ((t % 3600) % 60);
        String ss = sec < 10 ? "0" + sec.ToString()
                : sec.ToString();
        String ans = hh + ":" + mm + ":" + ss;
        return ans;
    }

    // Function to find the time gap
    static String timeGap(String st, String et) {

        int t1 = getTimeInSeconds(st);
        int t2 = getTimeInSeconds(et);

        int time_diff = (t1 - t2 < 0) ? t2 - t1 : t1 - t2;

        return convertSecToTime(time_diff);
    }

    // Driver Code
    public static void Main(String []args) {

        String st = "13:50:45", et = "14:55:50";
        Console.WriteLine(timeGap(st, et));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find the time difference
       function getTimeInSeconds(str) {

           let curr_time = [];

           curr_time = str.split(':')
           for (let i = 0; i < curr_time.length; i++) {
               curr_time[i] = parseInt(curr_time[i]);
           }

           let t = curr_time[0] * 60 * 60
               + curr_time[1] * 60
               + curr_time[2];

           return t;
       }

       // Function to convert seconds back to hh::mm:ss
       // format
       function convertSecToTime(t) {
           let hours = Math.floor(t / 3600);
           let hh = hours < 10 ? "0" + (hours).toString()
               : (hours).toString();
           let min = Math.floor((t % 3600) / 60);
           let mm = min < 10 ? "0" + (min).toString()
               : (min).toString();
           let sec = ((t % 3600) % 60);
           let ss = sec < 10 ? "0" + (sec).toString()
               : (sec).toString();
           let ans = hh + ":" + mm + ":" + ss;
           return ans;
       }

       // Function to find the time gap
       function timeGap(st, et) {

           let t1 = getTimeInSeconds(st);
           let t2 = getTimeInSeconds(et);

           let time_diff
               = (t1 - t2 < 0) ? t2 - t1 : t1 - t2;

           return convertSecToTime(time_diff);
       }

       // Driver Code
       let st = "13:50:45", et = "14:55:50";

       document.write(timeGap(st, et) + '<br>');

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
01:05:05
```

***时间复杂度*** : O(1)
***辅助空间*** : O(1)