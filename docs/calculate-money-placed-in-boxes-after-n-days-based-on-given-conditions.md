# 根据给定条件

计算 N 天后放入箱子的钱

> 原文:[https://www . geeksforgeeks . org/基于给定条件计算 n 天后放入盒子中的钱/](https://www.geeksforgeeks.org/calculate-money-placed-in-boxes-after-n-days-based-on-given-conditions/)

给定 7 个空盒子 **b1、b2、b3、b4、b5、b6、b7** ，以及一个整数 **N** ，任务是根据以下条件找到 **N** 天后可以放入盒子的钱的总数:

1.  每天，钱只能以循环的方式放在一个盒子里 **b1，b2，b3，b4，b5，b6，b7，b1，b2，…..**等等。
2.  在盒子 **b1** 中，放入比盒子 **b1** 中已经存在的钱多的 **1** 。
3.  在除 **b1** 以外的每一个盒子里，放上 **1** 比上一个盒子里的钱多。

**示例:**

> **输入:** N = 4
> **输出:** 15
> **解释:**
> 第 1 天往 b1 箱放钱= 1
> 第 2 天往 b2 箱放钱= 2
> 第 3 天往 b3 箱放钱= 3
> 第 4 天往 b4 箱放钱= 4
> 第 5 天往 b5 箱放钱= 5
> 第 5 天之后，合计金额= 1 + 2 + 3 + 4
> 
> **输入:**N = 15
> T3】输出:66
> T6】说明:第 15 天之后，合计金额= 1+2+3+4+5+6+7+2+3+4+5+6+7+8+3 = 66

**方法:**按照以下步骤解决问题

1.  花在**I<sup>th</sup>T3】日的钱是**((I–1)/7)+((I–1)% 7+1)**其中 **i** 位于**【1，N】**范围内**
2.  模拟相同的天数**【1，N】**
3.  打印总成本。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <iostream>
using namespace std;

// Function to find the total money
// placed in boxes after N days
int totalMoney(int N)
{

    // Stores the total money
    int ans = 0;

    // Iterate for N days
    for(int i = 0; i < N; i++)
    {

        // Adding the Week number
        ans += i / 7;

        // Adding previous amount + 1
        ans += (i % 7 + 1);
    }

    // Return the total amount
    return ans;
}

// Driver code
int main()
{  

    // Input
    int N = 15;

    // Function call to find
    // total money placed
    cout << totalMoney(N);
}

// This code is contributed khushboogoyal499
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach

import java.io.*;

class GFG {

    // Function to find the total money
    // placed in boxes after N days
    public static int totalMoney(int N)
    {

        // Stores the total money
        int ans = 0;

        // Iterate for N days
        for (int i = 0; i < N; i++) {

            // Adding the Week number
            ans += i / 7;

            // Adding previous amount + 1
            ans += (i % 7 + 1);
        }

        // Return the total amount
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int N = 15;

        // Function call to find
        // total money placed
        System.out.println(
            totalMoney(N));
    }
}
```

## 计算机编程语言

```
# Python program for
# the above approach

# Function to find the total money
# placed in boxes after N days
def totalMoney(N):

    # Stores the total money
    ans = 0

    # Iterate for N days
    for i in range(0, N):

        # Adding the Week number
        ans += i / 7

        # Adding previous amount + 1
        ans += (i % 7 + 1)

    # Return the total amount
    return ans

# Driver code

# Input
N = 15

# Function call to find
# total money placed
print(totalMoney(N))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for
// the above approach
using System;

class GFG{

// Function to find the total money
// placed in boxes after N days
public static int totalMoney(int N)
{

    // Stores the total money
    int ans = 0;

    // Iterate for N days
    for(int i = 0; i < N; i++)
    {

        // Adding the Week number
        ans += i / 7;

        // Adding previous amount + 1
        ans += (i % 7 + 1);
    }

    // Return the total amount
    return ans;
}

// Driver code
static public void Main()
{

    // Input
    int N = 15;

    // Function call to find
    // total money placed
    Console.WriteLine(totalMoney(N));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

    // Function to find the total money
    // placed in boxes after N days
    function totalMoney(N)
    {

        // Stores the total money
        let ans = 0;

        // Iterate for N days
        for (let i = 0; i < N; i++) {

            // Adding the Week number
            ans += Math.floor(i / 7);

            // Adding previous amount + 1
            ans += (i % 7 + 1);
        }

        // Return the total amount
        return ans;
    }

// Driver Code

    // Input
        let N = 15;

        // Function call to find
        // total money placed
       document.write(
            totalMoney(N));

</script>
```

**Output:** 

```
66
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方式:**以上方式可以通过找出**完成周数**和**最后一周剩余天数进行优化。**

按照以下步骤解决问题:

1.  初始化变量 **X** 和 **Y** ，分别存储完整周和部分周可以投放的金额。
2.  每周的钱可以计算为:
    *   1 <sup>st</sup> 周:1 2 3 4 5 6 7 = 28 + (7 x 0)
    *   2 <sup>第二</sup>周:2 3 4 5 6 7 8 = 28 + (7 x 1)
    *   3 <sup>rd</sup> 周:3 4 5 6 7 8 9 = 28 + (7 x 2)
    *   4 <sup>第</sup>周:4 5 6 7 8 9 10 = 28 + (7 x 3)以此类推。
3.  因此，更新:
    **X = 28 + 7 x(完成周数–1)**
    **Y =****剩余天数之和+(完成周数*最后一周剩余天数)**
4.  所以总金额等于 **X + Y** 。打印总**金额**放置。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find total
// money placed in the box
int totalMoney(int N)
{
    // Number of complete weeks
    int CompWeeks = N / 7;

    // Remaining days in
    // the last week
    int RemDays = N % 7;

    int X = 28 * CompWeeks
            + 7 * (CompWeeks
                   * (CompWeeks - 1) / 2);

    int Y = RemDays
                * (RemDays + 1) / 2
            + CompWeeks * RemDays;

    int cost = X + Y;

    cout << cost << '\n';
}

// Driver Code
int main()
{
    // Input
    int N = 15;

    // Function call to find
    // the total money placed
    totalMoney(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

// Function to find total
// money placed in the box
static void totalMoney(int N)
{
    // Number of complete weeks
    int CompWeeks = N / 7;

    // Remaining days in
    // the last week
    int RemDays = N % 7;

    int X = 28 * CompWeeks
            + 7 * (CompWeeks
                   * (CompWeeks - 1) / 2);

    int Y = RemDays
                * (RemDays + 1) / 2
            + CompWeeks * RemDays;

    int cost = X + Y;

    System.out.print(cost);
}

    // Driver Code
    public static void main(String[] args)
    {
    // Input
    int N = 15;

    // Function call to find
    // the total money placed
    totalMoney(N);
    }
}

// This code is contributed by souravghosh0416.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find total
// money placed in the box
static void totalMoney(int N)
{

    // Number of complete weeks
    int CompWeeks = N / 7;

    // Remaining days in
    // the last week
    int RemDays = N % 7;

    int X = 28 * CompWeeks + 7 *
    (CompWeeks * (CompWeeks - 1) / 2);

    int Y = RemDays * (RemDays + 1) / 2 +
          CompWeeks * RemDays;

    int cost = X + Y;

    Console.WriteLine(cost);
}   

// Driver Code
public static void Main()
{

    // Input
    int N = 15;

    // Function call to find
    // the total money placed
    totalMoney(N);
}
}

// This code is contriobuted by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to find total
// money placed in the box
function totalMoney( N)
{
    // Number of complete weeks
    let CompWeeks = Math.floor(N / 7);

    // Remaining days in
    // the last week
    let RemDays = N % 7;

    let X = 28 * CompWeeks
            + 7 * Math.floor((CompWeeks
                   * (CompWeeks - 1) / 2));

    let Y = RemDays
                * Math.floor((RemDays + 1) / 2)
            + CompWeeks * RemDays;

    let cost = X + Y;

    document.write(cost ,'<br>');
}

// Driver Code

    // Input
    let N = 15;

    // Function call to find
    // the total money placed
    totalMoney(N);

</script>
```

**Output:** 

```
66
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)