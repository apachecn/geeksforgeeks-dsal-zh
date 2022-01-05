# 找出 t 时刻站在体育场内的观众人数

> 原文:[https://www . geesforgeks . org/find-number-观众-站立-体育场-time-t/](https://www.geeksforgeeks.org/find-number-spectators-standing-stadium-time-t/)

体育场内有 n 名观众，标记为从 1 到 n。
时间 1，第一个观众站起来。
时间 2，第二个观众站起来。
……
在时间 k，第 k 个观众站了起来。
在时间 k + 1，第(k + 1)个观众站起来，第一个观众坐下。
时间 k + 2，第(k + 2)位观众起立，第二位观众就座。
……
在时间 n，第 n 个观众站起来，第(n–k)个观众坐下。
在时间 n + 1，第(n+1–k)个观众入座。
……
第 n + k 时间，第 n 位观众入座。
求一次 t 站在体育场的观众人数。

**示例:**

```
Input : 10 5 3
Output : 3
Explanation : 
n = 10, k = 5, t = 3
At time 1, 1st spectator stands.
At time 2, 2nd spectator stands.
At time 3, 3rd spectator stands.

Thus, the result is 3 as there are 
total of 3 spectators standing.

Input :10 5 7
Output : 5
Explanation :
n = 10, k = 5, t = 7
At time 1, 1st spectator stands.
At time 2, 2nd spectator stands.
At time 3, 3rd spectator stands.
At time 4, 4th spectator stands.
At time 5, 5th spectator stands.
At time 6, 6th spectator stands
and 1st spectator sits [(n-k) = 6 - 5 = 1
as mentioned above].
At time 7, 7th spectator stands
and 2nd spectator sits.

So, now there are total of 5 spectators
standing.
Thus, result is 5.
```

**进场:**
现在我们可以观察**这个问题中的某些条件**:
**注:**场内最多只能站 k 名观众。
1)如果时间小于 k 值，则表示观众仍在站立。所以结果会是 t.
2)在 n 和 k(含)之间的时间里，站着的观众是 k【观察】
3)n 次之后，观众开始一个接一个地坐着。所以我们计算坐在**' t–n】**旁边的观众。然后用这个值减去 k。这就产生了结果。

下面是上述方法的实现:

## C++

```
// CPP program to find number of spectators
// standing at a time
#include <bits/stdc++.h>
using namespace std;

void result(long long n, long long k, long long t)
{
    // If the time is less than k
    // then we can print directly t time.
    if (t <= k)
        cout << t;

    // If the time is n then k spectators
    // are standing.
    else if (t <= n)
        cout << k;

    // Otherwise we calculate the spectators
    // standing.
    else {
        long long temp = t - n;
        temp = k - temp;
        cout << temp;
    }
}

// Driver code
int main()
{
    // Stores the value of n, k and t
    // t is time
    // n & k is the number of specators
    long long n, k, t;
    n = 10;
    k = 5;
    t = 12;
    result(n, k, t);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of spectators
// standing at a time

class GFG {

    static void result(long n, long k,long t)
    {
        // If the time is less than k
        // then we can print directly t time.
        if (t <= k)
            System.out.println(t);

        // If the time is n then k spectators
        // are standing.
        else if (t <= n)
            System.out.println(k);

        // Otherwise we calculate the
        // spectators standing.
        else {
            long temp = t - n;
            temp = k - temp;
            System.out.println(temp);
        }
    }

    // Driver code
    public static void main(String args[])
    {
        // Stores the value of n, k and t
        // t is time
        // n & k is the number of specators
        long n, k, t;
        n = 10;
        k = 5;
        t = 12;
        result(n, k, t);

    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python program to find number of spectators
# standing at a time

def result(n, k, t) :

    # If the time is less than k
    # then we can print directly t time.
    if (t <= k) :
        print(t )

    # If the time is n then k spectators
    # are standing.
    elif (t <= n) :
        print( k)

    # Otherwise we calculate the
    # spectators standing.
    else :

        temp = t - n
        temp = k - temp
        print (temp)

# Driver code

# Stores the value of n, k and t
# t is time
# n & k is the number of specators
n = 10
k = 5
t = 12
result(n, k, t)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find number of
// spectators standing at a time
using System;

class GFG {

    static void result(long n, long k,long t)
    {
        // If the time is less than k
        // then we can print directly t time.
        if (t <= k)
            Console.WriteLine(t);

        // If the time is n then k spectators
        // are standing.
        else if (t <= n)
            Console.WriteLine(k);

        // Otherwise we calculate the
        // spectators standing.
        else {
            long temp = t - n;
            temp = k - temp;
            Console.WriteLine(temp);
        }
    }

    // Driver code
    public static void Main()
    {
        // Stores the value of n, k and t
        // t is time
        // n & k is the number of specators
        long n, k, t;
        n = 10;
        k = 5;
        t = 12;
        result(n, k, t);

    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// spectators standing at a time

function result($n, $k, $t)
{
    // If the time is less
    // than k then we can
    // print directly t time.
    if ($t <= $k)
        echo t;

    // If the time is n then
    // k spectators are standing.
    else if ($t <= $n)
        echo k;

    // Otherwise we calculate
    // the spectators standing.
    else
    {
        $temp = $t - $n;
        $temp = $k - $temp;
        echo $temp;
    }
}

// Driver code

// Stores the value of n, k and t
// t is time
// n & k is the number of specators
$n = 10;
$k = 5;
$t = 12;
result($n, $k, $t);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of
// spectators standing at a time
function result(n, k, t)
{

    // If the time is less than k
    // then we can print directly t time.
    if (t <= k)
        document.write(t);

    // If the time is n then k spectators
    // are standing.
    else if (t <= n)
        document.write(k);

    // Otherwise we calculate the
    // spectators standing.
    else
    {
        let temp = t - n;
        temp = k - temp;
        document.write(temp);
    }
}

// Driver code

// Stores the value of n, k and t
// t is time
// n & k is the number of specators
let n, k, t;
n = 10;
k = 5;
t = 12;

result(n, k, t);

// This code is contributed by susmitakundugoaldanga 

</script>
```

**输出:**

```
3
```

**时间复杂度:O(1)**
**空间复杂度:O(1)**
本文由 [**萨钦毕舍**](https://www.linkedin.com/in/sachin-bisht-984b5013a/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。