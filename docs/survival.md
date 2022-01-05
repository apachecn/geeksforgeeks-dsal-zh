# 检查是否有可能在海岛生存

> 原文:[https://www.geeksforgeeks.org/survival/](https://www.geeksforgeeks.org/survival/)

你是一个岛上的穷人。这个岛上只有一家商店，除了星期天，这家商店一周四天都营业。考虑以下限制:

*   n–每天可以购买的最大食物单位。
*   s–你需要生存的天数。
*   m–每天生存所需的食物单位。

目前，今天是星期一，你需要在接下来的几天里生存下来。
**找到你需要从商店购买食物的最小天数，这样你就可以在接下来的 S 天生存，**或者确定不可能生存。
示例:

> 输入:S = 10 N = 16 M = 2
> 输出:是 2
> **解释 1:** 一种可能的解决方案是第一天(周一)买一盒，从这盒一直吃到第 8 天(周一)就够了。现在，在第 9 天(星期二)，你再买一盒，用里面的巧克力熬过第 9 天和第 10 天。
> 输入:10 20 30
> 输出:否
> 说明 2:你即使买菜也活不下去，因为你一天能买的单位最多也就少了一天所需的食物。

**进场:**
在这个问题上，连续几天前期买菜的贪婪进场才是正确的方向。
如果我们能存活前 7 天，那么我们可以存活任何天数，为此我们需要检查两件事
- >检查我们是否能存活一天。
- > (S > = 7)如果我们在一周的前 6 天购买食物，并且我们可以存活一周，即我们在一周内可以购买的食物总量(6*N)大于或等于我们在一周内生存所需的食物总量(7*M)，那么我们就可以存活。

**注意:我们是前 6 天购买的食物，因为我们从周一开始计算，周日商店仍然关闭。**
如果上述任何条件都不成立，那么我们就无法生存，否则购买食物所需的最短天数将为=上限(所需食物总量/我们每天可以购买的食物单位)。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the minimum days on which
// you need to buy food from the shop so that you
// can survive the next S days
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum days
void survival(int S, int N, int M)
{

    // If we can not buy at least a week
    // supply of food during the first week
    // OR We can not buy a day supply of food
    // on the first day then we can't survive.
    if (((N * 6) < (M * 7) && S > 6) || M > N)
        cout << "No\n";
    else {
        // If we can survive then we can
        // buy ceil(A/N) times where A is
        // total units of food required.
        int days = (M * S) / N;
        if (((M * S) % N) != 0)
            days++;
        cout << "Yes " << days << endl;
    }
}

// Driver code
int main()
{
    int S = 10, N = 16, M = 2;
    survival(S, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum days on which
// you need to buy food from the shop so that you
// can survive the next S days
import java.io.*;

class GFG {

    // function to find the minimum days
    static void survival(int S, int N, int M)
    {

        // If we can not buy at least a week
        // supply of food during the first
        // week OR We can not buy a day supply
        // of food on the first day then we
        // can't survive.
        if (((N * 6) < (M * 7) && S > 6) || M > N)
            System.out.println("No");

        else {

            // If we can survive then we can
            // buy ceil(A/N) times where A is
            // total units of food required.
            int days = (M * S) / N;

            if (((M * S) % N) != 0)
                days++;

            System.out.println("Yes " + days);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int S = 10, N = 16, M = 2;

        survival(S, N, M);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find the minimum days on 
# which you need to buy food from the shop so
# that you can survive the next S days
def survival(S, N, M):

# If we can not buy at least a week
# supply of food during the first week
# OR We can not buy a day supply of food
# on the first day then we can't survive.
    if (((N * 6) < (M * 7) and S > 6) or M > N):
        print("No")
    else:

    # If we can survive then we can
    # buy ceil(A / N) times where A is
    # total units of food required.
        days = (M * S) / N

        if (((M * S) % N) != 0):
            days += 1
        print("Yes "),
        print(days)

# Driver code
S = 10; N = 16; M = 2
survival(S, N, M)

# This code is contributed by upendra bartwal
```

## C#

```
// C# program to find the minimum days
// on which you need to buy food from
// the shop so that you can survive
// the next S days
using System;

class GFG {

    // function to find the minimum days
    static void survival(int S, int N, int M)
    {

        // If we can not buy at least a week
        // supply of food during the first
        // week OR We can not buy a day
        // supply of food on the first day
        // then we can't survive.
        if (((N * 6) < (M * 7) && S > 6) || M > N)
            Console.Write("No");
        else {

            // If we can survive then we can
            // buy ceil(A/N) times where A is
            // total units of food required.
            int days = (M * S) / N;

            if (((M * S) % N) != 0)
                days++;

            Console.WriteLine("Yes " + days);
        }
    }

    // Driver code
    public static void Main()
    {
        int S = 10, N = 16, M = 2;

        survival(S, N, M);
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// minimum days on which
// you need to buy food
// from the shop so that you
// can survive the next S days

// Function to find
// the minimum $days
function survival($S, $N, $M)
{

    // If we can not buy at least a week
    // supply of food during the first week
    // OR We can not buy a day supply of food
    // on the first day then we can't survive.
    if ((($N * 6) < ($M * 7) &&
          $S > 6) || $M >$N)
        echo "No";
    else
    {

        // If we can survive then we can
        // buy ceil(A/N) times where A is
        // total units of food required.
        $days = ($M * $S) / $N;
        if ((($M * $S) % $N) != 0)
            $days++;
        echo "Yes " , floor($days) ;
    }
}

    // Driver code
    $S = 10; $N = 16; $M = 2;
    survival($S, $N, $M);

// This code is contributed by anuj_67

?>
```

## java 描述语言

```
<script>
// JavaScript program to find the minimum days on which
// you need to buy food from the shop so that you
// can survive the next S days

    // function to find the minimum days
    function survival(S, N, M)
    {

        // If we can not buy at least a week
        // supply of food during the first
        // week OR We can not buy a day supply
        // of food on the first day then we
        // can't survive.
        if (((N * 6) < (M * 7) && S > 6) || M > N)
            document.write("No");

        else {

            // If we can survive then we can
            // buy ceil(A/N) times where A is
            // total units of food required.
            let days = (M * S) / N;

            if (((M * S) % N) != 0)
                days++;

            document.write("Yes " + Math.round(days));
        }
    }

// Driver Code
        let S = 10, N = 16, M = 2;
        survival(S, N, M);

        // This code is contributed by splevel62.
</script>
```

**输出:**

```
Yes 2
```

**时间复杂度:**O(1)
T3】空间复杂度: O(1)