# 分针和时针重合的时间

> 原文:[https://www . geeksforgeeks . org/time-分-手-时-手-重合/](https://www.geeksforgeeks.org/time-minute-hand-hour-hand-coincide/)

给定以小时为单位的时间，找出分针和时针在下一个小时重合的时间(以分钟为单位)。
**例:**

```
Input : 3 
Output : (180/11) minutes

Input :7
Output : (420/11) minutes
```

**进场:**
1。取小时“h1 和 h2”的两个变量，然后求出角度“theta”[theta =(30 * h1)]，再除以“11”求出分钟(m)的时间。我们用 11 分开， 因为时钟的指针在 12 小时内重合 11s 时间，在 24 小时内重合 22 次:
**公式:**这可以用时间 h1 到 h2 的公式来计算，意思是【11m/2–30(h1)】
这意味着【m =((30 * h1)* 2)/11】】
【m =(θ* 2)/11】
其中【θ=(30 * h1)】
其中 A 和 B 是小时，即如果给定的小时是(2，

## C++

```
// CPP code to find the minute at which
// the minute hand and hour hand coincide
#include <bits/stdc++.h>
using namespace std;

// function to find the minute
void find_time(int h1)
{
  // finding the angle between minute
  // hand and the first hour hand
  int theta = 30 * h1;
  cout << "(" << (theta * 2) << "/"
       << "11"
       << ")"
       << " minutes";
}

// Driver code
int main() {
  int h1 = 3; 
  find_time(h1); 
  return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java code to find the minute 
// at which the minute hand and
// hour hand coincide
import java.io.*;

class GFG
{

    // function to find the minute
    static void find_time(int h1)
    {

    // finding the angle between
    // minute hand and the first
    // hour hand
    int theta = 30 * h1;
    System.out.println("(" + theta *
                           2 + "/" +
                   " 11 ) minutes");
    }

    //Driver Code
    public static void main (String[] args)
    {
        int h1 = 3;
        find_time(h1);    
    }
}

// This code is contributed by
// upendra singh bartwal
```

## 蟒蛇 3

```
# Python3 code to find the
# minute at which the minute
# hand and hour hand coincide

# Function to find the minute
def find_time(h1):

    # Finding the angle between
    # minute hand and the first
    # hour hand
    theta = 30 * h1
    print("(", end = "")
    print((theta * 2),"/ 11) minutes")

# Driver code
h1 = 3
find_time(h1)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# code to find the minute
// at which the minute hand
// and hour hand coincide
using System;

class GFG
{

    // function to find the minute
    static void find_time(int h1)
    {

        // finding the angle between minute
        // hand and the first hour hand
        int theta = 30 * h1;
        Console.WriteLine("(" + theta * 2 +
                     "/" + " 11 )minutes");
    }

    //Driver Code
    public static void Main()
    {
        int h1 = 3;

        find_time(h1);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the minute
// at which the minute hand and
// hour hand coincide

// function to find the minute
function find_time($h1)
{
    // finding the angle between
    // minute hand and the first
    // hour hand
    $theta = 30 * $h1;
    echo("(" . ($theta * 2) .
           "/" . "11" . ")" .
                 " minutes");
}

// Driver code
$h1 = 3;
find_time($h1);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript code to find the minute at which
// the minute hand and hour hand coincide

// function to find the minute
function find_time(h1)
{
// finding the angle between minute
// hand and the first hour hand
theta = 30 * h1;
document.write("(" + (theta * 2) + "/"
    + "11"
    + ")"
    + " minutes");
}

// Driver code
h1 = 3;
find_time(h1);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output :** 

```
(180/11) minutes
```