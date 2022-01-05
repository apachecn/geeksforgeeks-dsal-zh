# 找出回文的时间，该时间在给定时间

之后

> 原文:[https://www . geesforgeks . org/find-the-time-of-is-回文并在给定时间后出现/](https://www.geeksforgeeks.org/find-the-time-which-is-palindromic-and-comes-after-the-given-time/)

给定一个以 24 小时格式存储时间的字符串 **str** 为 **HH:MM** ，使得 **0 ≤ HH ≤ 23** 和 **0 ≤ MM ≤ 59** 。任务是找到下一个最近的时间，当作为字符串读取时，这是一个回文。如果不存在这样的字符串，则打印 **-1** 。
**举例:**

> **输入:** str = "21:12"
> **输出:** 22:22
> 给定小时内唯一可能的回文时间为 21:12
> 但不大于给定时间，因此输出将为
> 下一小时的回文时间，即 22:22
> **输入:** str = "23:32"
> **输出:**--

**方法:**有三种可能的情况:

1.  如果 **MM <反转(HH)** 则输出为 **HH** 小时，**反转(HH)** 分钟。
2.  如果**HH = 23****MM≥32**，则输出为 **00:00，即上午 12:00**。
3.  否则输出将是 **HH + 1** 小时，**反转(HH + 1)** 分钟。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// Function to return the required time
string getTime(string s, int n)
{
    // To store the resultant time
    string res;

    // Hours are stored in h as integer
    int h = stoi(s.substr(0, 2));

    // Minutes are stored in m as integer
    int m = stoi(s.substr(3, 2));

    // Reverse of h
    int rev_h = (h % 10) * 10 + ((h % 100) - (h % 10)) / 10;

    // Reverse of h as a string
    string rev_hs = to_string(rev_h);

    if (h == 23 && m >= 32) {
        res = "-1";
    }

    // If MM < reverse of (HH)
    else if (m < rev_h) {
        string temp;

        // 0 is added if HH < 10
        if (h < 10)
            temp = "0";
        temp = temp + to_string(h);

        // 0 is added if rev_h < 10
        if (rev_h < 10)
            res = res + temp + ":0" + rev_hs;
        else
            res = res + temp + ":" + rev_hs;
    }
    else {

        // Increment hours
        h++;

        // Reverse of the hour after incrementing 1
        rev_h = (h % 10) * 10 + ((h % 100) - (h % 10)) / 10;
        rev_hs = to_string(rev_h);

        string temp;

        // 0 is added if HH < 10
        if (h < 10)
            temp = "0";
        temp = temp + to_string(h);

        // 0 is added if rev_h < 10
        if (rev_h < 10)
            res = res + temp + ":0" + rev_hs;
        else
            res = res + temp + ":" + rev_hs;
    }
    return res;
}

// Driver code
int main()
{
    string s = "21:12";
    int n = s.length();

    cout << getTime(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the required time
    static String getTime(String s, int n)
    {

        // To store the resultant time
        String res = "";

        // Hours are stored in h as integer
        int h = Integer.parseInt(s.substring(0, 0 + 2));

        // Minutes are stored in m as integer
        int m = Integer.parseInt(s.substring(3, 3 + 2));

        // Reverse of h
        int rev_h = (h % 10) * 10 +
                   ((h % 100) - (h % 10)) / 10;

        // Reverse of h as a string
        String rev_hs = Integer.toString(rev_h);
        if (h == 23 && m >= 32)
        {
            res = "-1";
        }

        // If MM < reverse of (HH)
        else if (m < rev_h)
        {
            String temp = "";

            // 0 is added if HH < 10
            if (h < 10)
                temp = "0";
            temp = temp + Integer.toString(h);

            // 0 is added if rev_h < 10
            if (rev_h < 10)
                res = res + temp + ":0" + rev_hs;
            else
                res = res + temp + ":" + rev_hs;
        }
        else
        {

            // Increment hours
            h++;

            // Reverse of the hour after incrementing 1
            rev_h = (h % 10) * 10 + ((h % 100) -
                    (h % 10)) / 10;
            rev_hs = Integer.toString(rev_h);

            String temp = "";

            // 0 is added if HH < 10
            if (h < 10)
                temp = "0";
            temp = temp + Integer.toString(h);

            // 0 is added if rev_h < 10
            if (rev_h < 10)
                res = res + temp + ":0" + rev_hs;
            else
                res = res + temp + ":" + rev_hs;
        }
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "21:12";
        int n = s.length();
        System.out.println(getTime(s, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required time
def getTime(s, n) :

    # Hours are stored in h as integer
    h = int(s[0 : 2]);

    # Minutes are stored in m as integer
    m = int(s[3 : 5]);

    # Reverse of h
    rev_h = (h % 10) * 10 + ((h % 100) - (h % 10)) // 10;

    # Reverse of h as a string
    rev_hs = str(rev_h)

    temp = ""
    res  = ""

    if (h == 23 and m >= 32) :
        res = "-1";

    # If MM < reverse of (HH)
    elif (m < rev_h) :

        # 0 is added if HH < 10
        if (h < 10) :
            temp = "0";

        temp = temp + str(h);

        # 0 is added if rev_h < 10
        if (rev_h < 10) :
            res = res + temp + ":0" + rev_hs;
        else :
            res = res + temp + ":" + rev_hs;

    else :

        # Increment hours
        h += 1

        # Reverse of the hour after incrementing 1
        rev_h = (h % 10) * 10 + ((h % 100) - (h % 10)) //10;

        rev_hs = str(rev_h);

        # 0 is added if HH < 10
        if (h < 10) :
            temp = "0";

        temp = temp + str(h);

        # 0 is added if rev_h < 10
        if (rev_h < 10) :
            res = res + temp + ":0" + rev_hs;
        else :
            res = res + temp + ":" + rev_hs;

    return res;

# Driver code
if __name__ == "__main__" :

    s = "21:12";
    n = len(s);

    print(getTime(s, n));

    # This code is contributed by AnkitRai01
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

//PHP implementation of the approach

// Function to return the required time
function getTime( $s, $n)
{
    // To store the resultant time
    $res="";

    // Hours are stored in h as integer
    $h = intval($s.substr(0, 2));

    // Minutes are stored in m as integer
    $m = intval($s.substr(3, 2));

    // Reverse of h
    $rev_h = ($h % 10) * 10 + (($h % 100) - ($h % 10)) / 10;

    // Reverse of h as a string
    $rev_hs = strval($rev_h);

    if ($h == 23 && $m >= 32) {
        $res = "-1";
    }

    // If MM < reverse of (HH)
    else if ($m < $rev_h) {
        $temp="";

        // 0 is added if HH < 10
        if ($h < 10)
            $temp = "0";
        $temp = $temp . strval($h);

        // 0 is added if rev_h < 10
        if ($rev_h < 10)
            $res = $res . $temp . ":0" . $rev_hs;
        else
            $res = $res. $temp .":" . $rev_hs;
    }
    else {

        // Increment hours
        $h++;

        // Reverse of the hour after incrementing 1
        $rev_h = ($h % 10) * 10 + (($h % 100) - ($h % 10)) / 10;
        $rev_hs = strval($rev_h);

        $temp="";

        // 0 is added if HH < 10
        if ($h < 10)
            $temp = "0";
        $temp = $temp . strval($h);

        // 0 is added if rev_h < 10
        if ($rev_h < 10)
            $res = $res . $temp . ":0" . $rev_hs;
        else
            $res = $res . $temp . ":" . $rev_hs;
    }
    return $res;
}

// Driver code

    $s = "21:12";
    $n = strlen($s);

    echo getTime($s, $n);

    return 0;

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

 // Function to return the required time
    function getTime(s,n)
    {
    // To store the resultant time
        let res = "";

        // Hours are stored in h as integer
        let h = parseInt(s.substring(0, 0 + 2));

        // Minutes are stored in m as integer
        let m = parseInt(s.substring(3, 3 + 2));

        // Reverse of h
       let rev_h = (h % 10) * 10 +
                   ((h % 100) - (h % 10)) / 10;

        // Reverse of h as a string
        let rev_hs = (rev_h).toString();
        if (h == 23 && m >= 32)
        {
            res = "-1";
        }

        // If MM < reverse of (HH)
        else if (m < rev_h)
        {
            let temp = "";

            // 0 is added if HH < 10
            if (h < 10)
                temp = "0";
            temp = temp + h.toString();

            // 0 is added if rev_h < 10
            if (rev_h < 10)
                res = res + temp + ":0" + rev_hs;
            else
                res = res + temp + ":" + rev_hs;
        }
        else
        {

            // Increment hours
            h++;

            // Reverse of the hour after incrementing 1
            rev_h = (h % 10) * 10 + ((h % 100) -
                    (h % 10)) / 10;
            rev_hs = (rev_h).toString();

            let temp = "";

            // 0 is added if HH < 10
            if (h < 10)
                temp = "0";
            temp = temp + h.toString();

            // 0 is added if rev_h < 10
            if (rev_h < 10)
                res = res + temp + ":0" + rev_hs;
            else
                res = res + temp + ":" + rev_hs;
        }
        return res;
    }

 // Driver Code
    let  s = "21:12";
    let n = s.length;
    document.write(getTime(s, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
22:22
```