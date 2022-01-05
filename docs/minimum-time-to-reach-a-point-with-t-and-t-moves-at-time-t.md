# 在时间 t 到达+t 和-t 移动点的最短时间

> 原文:[https://www . geeksforgeeks . org/到达 t 点的最短时间 t 点移动时间/](https://www.geeksforgeeks.org/minimum-time-to-reach-a-point-with-t-and-t-moves-at-time-t/)

给定一个正坐标“X”，并且你在坐标“0”，任务是通过以下移动找到到达坐标“X”所需的最短时间:
在时间“t”时，你可以停留在相同的位置，或者向左或向右跳一段长度正好为“t”的距离。换句话说，你可以在坐标' x–t '，' x '或' x + t '的时间' t '处，其中' x '是当前位置。
**例:**

```
Input: 6
Output: 3
At time 1, jump from x = 0 to x = 1 (x = x + 1)
At time 2, jump from x = 1 to x = 3 (x = x + 2)
At time 3, jump from x = 3 to x = 6 (x = x + 3)
So, minimum required time is 3.

Input: 9
Output: 4
At time 1, do not jump i.e x = 0 
At time 2, jump from x = 0 to x = 2 (x = x + 2)
At time 3, jump from x = 2 to x = 5 (x = x + 3)
At time 4, jump from x = 5 to x = 9 (x = x + 4)
So, minimum required time is 4.
```

**方法:**下面的贪婪策略起作用:
我们只需要找到最小的‘t’，这样 1 + 2 + 3 + … + t > = X.

*   如果(t * (t + 1)) / 2 = X，则答案为“t”。
*   否则如果(t * (t + 1)) / 2 > X，那么我们找到(t *(t+1))/2–X，并从序列[1，2，3，…，t]中删除这个数字。得到的序列加起来是“X”。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <iostream>

using namespace std;

   // returns the minimum time
    // required to reach 'X'
    long cal_minimum_time(long X)
    {

        // Stores the minimum time
        long t = 0;
        long sum = 0;

        while (sum < X) {

            // increment 't' by 1
            t++;

            // update the sum
            sum = sum + t;
        }

        return t;
    }

// Driver code
int main()
{
        long n = 6;
        long ans = cal_minimum_time(n);
        cout << "The minimum time required is : " << ans ;

   return 0;

   // This code is contributed by ANKITRAI1
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // returns the minimum time
    // required to reach 'X'
    static long cal_minimum_time(long X)
    {

        // Stores the minimum time
        long t = 0;
        long sum = 0;

        while (sum < X) {

            // increment 't' by 1
            t++;

            // update the sum
            sum = sum + t;
        }

        return t;
    }

    // Driver code
    public static void main(String[] args)
    {
        long n = 6;
        long ans = cal_minimum_time(n);
        System.out.println("The minimum time required is : " + ans);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# returns the minimum time
# required to reach 'X'
def cal_minimum_time(X):

    # Stores the minimum time
    t = 0
    sum = 0

    while (sum < X):

        # increment 't' by 1
        t = t + 1

        # update the sum
        sum = sum + t;

    return t;

# Driver code
if __name__ == '__main__':
    n = 6
    ans = cal_minimum_time(n)
    print("The minimum time required is :", ans)

# This code is contributed By
# Surendra_Gangwar
```

## C#

```
// C#  implementation of the above approach
using System;

public class GFG{

    // returns the minimum time
    // required to reach 'X'
    static long cal_minimum_time(long X)
    {

        // Stores the minimum time
        long t = 0;
        long sum = 0;

        while (sum < X) {

            // increment 't' by 1
            t++;

            // update the sum
            sum = sum + t;
        }

        return t;
    }

    // Driver code
    static public void Main (){
        long n = 6;
        long ans = cal_minimum_time(n);
        Console.WriteLine("The minimum time required is : " + ans);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// returns the minimum time
// required to reach 'X'
function cal_minimum_time($X)
{
    // Stores the minimum time
    $t = 0;
    $sum = 0;

    while ($sum < $X)
    {

        // increment 't' by 1
        $t++;

        // update the sum
        $sum = $sum + $t;
    }

    return $t;
}

// Driver code
$n = 6;
$ans = cal_minimum_time($n);
echo "The minimum time required is : " . $ans;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

    // returns the minimum time
    // required to reach 'X'
    function cal_minimum_time(X)
    {

        // Stores the minimum time
        let t = 0;
        let sum = 0;

        while (sum < X) {

            // increment 't' by 1
            t++;

            // update the sum
            sum = sum + t;
        }

        return t;
    }

// driver code

  let n = 6;
  let ans = cal_minimum_time(n);
  document.write("The minimum time required is : " + ans);

</script>
```

**Output:** 

```
The minimum time required is : 3
```