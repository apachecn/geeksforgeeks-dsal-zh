# 根据给定条件从无限类型的无限项中找出第 n 项分布

> 原文:[https://www . geeksforgeeks . org/find-n-item-distributed-from-items-of-infinite-type-based-on-给定条件/](https://www.geeksforgeeks.org/find-nth-item-distributed-from-infinite-items-of-infinite-types-based-on-given-conditions/)

给定一个正整数 **N** ，当存在无限数量类型的无限个项目时，任务是找到给出的第 **N <sup>第</sup>T5】个项目，使得项目以如下方式给出:**

*   **第 1 天:**发出 1 个第一类物品。
*   **第 2 天:**给出 2 项ⅱ型和 1 项ⅰ型。
*   **第三天:**给出三类 3 项，二类 2 项，一类 1 项。
*   **第 4 天:**给出 4 项第四类、3 项第三类、2 项第二类、1 项第一类。
*   等等…

**示例:**

> **输入:** N = 10
> **输出:** 1
> **说明:**
> 以下为给出的项目顺序:
> 
> *   **第 1 天:**发出 1 个第一类物品。序列是{1}。
> *   **第 2 天:**给出 2 项ⅱ型和 1 项ⅰ型。序列是{1，2，2，1}。
> *   **第三天:**给出三类 3 项，二类 2 项，一类 1 项。序列是{1，2，2，1，3，3，3，2，2，1}。
> 
> 从以上移除项目的顺序来看，给出的第 N <sup>个</sup> (= 10 个<sup>个</sup>)项目为 1。因此，打印 1。
> 
> **输入:**N = 399
> T3】输出: 11

**方法:**解决给定问题最简单的方法是按照给定的顺序记录每天给定项目的天数和计数，并打印在第 N 个<sup>回合</sup>给出的项目。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the type of the
// item given out according to the
// given rules
int itemType(int n)
{
    // Stores the count of item given
    // out at each step
    int count = 0;

    // Iterate over the days from 1
    for (int day = 1;; day++) {

        // Iterate over type of item
        // on that day
        for (int type = day; type > 0; type--) {
            count += type;

            // Count of items given out
            // should exceed n
            if (count >= n)
                return type;
        }
    }
}

// Driver Code
int main()
{
    int N = 10;
    cout << itemType(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;
class GFG
{

  // Function to find the type of the
// item given out according to the
// given rules
static int itemType(int n)
{
    // Stores the count of item given
    // out at each step
    int count = 0;

    // Iterate over the days from 1
    for (int day = 1;; day++) {

        // Iterate over type of item
        // on that day
        for (int type = day; type > 0; type--) {
            count += type;

            // Count of items given out
            // should exceed n
            if (count >= n)
                return type;
        }
    }
}

// Driver Code
    public static void main (String[] args) {

        int N = 10;

        System.out.println( itemType(N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the type of the
# item given out according to the
# given rules
def itemType(n):

    # Stores the count of item given
    # out at each step
    count = 0

    # Iterate over the days from 1
    day = 1

    while(True):

        # Iterate over type of item
        # on that day
        for type in range(day, 0, -1):
            count += type

            # Count of items given out
            # should exceed n
            if (count >= n):
                return type

# Driver Code
N = 10

print(itemType(N))

# This code is contributed by ShubhamSingh10
```

## C#

```
//C# code for the above approach
using System;

public class GFG{
    // Function to find the type of the
    // item given out according to the
    // given rules
    static int itemType(int n)
    {
        // Stores the count of item given
        // out at each step
        int count = 0;

        // Iterate over the days from 1
        for (int day = 1;; day++) {

            // Iterate over type of item
            // on that day
            for (int type = day; type > 0; type--) {
                count += type;

                // Count of items given out
                // should exceed n
                if (count >= n)
                    return type;
            }
        }
    }

    // Driver Code
   static public void Main ()
   {

        int N = 10;

        Console.WriteLine( itemType(N));
    }
}

// This code is contributed by shubhamsingh10.
```

## java 描述语言

```
// Javascript program for the above approach

// Function to find the type of the
// item given out according to the
// given rules
function itemType(n)
{

  // Stores the count of item given
  // out at each step
  let count = 0;

  // Iterate over the days from 1
  for (let day = 1; ; day++)
  {

    // Iterate over type of item
    // on that day
    for (let type = day; type > 0; type--)
    {
      count += type;

      // Count of items given out
      // should exceed n
      if (count >= n) return type;
    }
  }
}

// Driver Code
let N = 10;
document.write(itemType(N));

// This code is contributed by _saurabh_jaiswal.
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**上述方法也可以通过使用以下事实进行优化:在给定的特定日期 **D** 给出的项目数量是[从 **1** 到**D**T9】的数字总和，从**第 1 天**到该日的数字总和应小于或等于 **N** 。按照以下步骤解决问题:](https://www.geeksforgeeks.org/count-sum-of-digits-in-numbers-from-1-to-n/)

*   初始化变量，说**计数**为 **0** 存储给定的物品数量，**日**存储当天的物品数量。
*   [迭代一个循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**(计数+日*(日+ 1))/2** 的值小于 **N** 并执行以下步骤:
    *   将**天*(天+ 1)/2** 的值添加到变量**计数**中。
    *   通过 **1** 增加**日**的数值。
*   [使用变量**类型**迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/) **【天，0】**，并执行以下任务:
    *   将**类型**的值添加到变量**计数**中。
    *   如果**计数**的值大于等于 **N** ，则打印**类型的值**作为结果答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the type of the
// item given out according to the
// given rules
int itemType(int n)
{

    // Stores the count of item given
    // out at each step
    int count = 0;
    int day = 1;

    // Iterate to find the Nth day
    // present is given out
    while (count + day * (day + 1) / 2
           < n) {

        // Find the number of presents
        // given on day is day*(day+1)/2
        count += day * (day + 1) / 2;
        day++;
    }

    for (int type = day; type > 0; type--) {

        // Iterate over the type
        count += type;

        // Return the resultant type
        if (count >= n) {
            return type;
        }
    }
}

// Driver Code
int main()
{
    int N = 10;
    cout << itemType(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the type of the
// item given out according to the
// given rules
static int itemType(int n)
{

    // Stores the count of item given
    // out at each step
    int count = 0;
    int day = 1;

    // Iterate to find the Nth day
    // present is given out
    while (count + day * (day + 1) / 2
           < n) {

        // Find the number of presents
        // given on day is day*(day+1)/2
        count += day * (day + 1) / 2;
        day++;
    }

    for (int type = day; type > 0; type--)
    {

        // Iterate over the type
        count += type;

        // Return the resultant type
        if (count >= n) {
            return type;
        }
    }
    return 0;
}

// Driver Code
public static void main(String[] args)
  {
    int N = 10;
    System.out.println( itemType(N));
}
}

// This code is contribured by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the type of the
# item given out according to the
# given rules
def itemType(n):

    # Stores the count of item given
    # out at each step
    count = 0
    day = 1

    # Iterate to find the Nth day
    # present is given out
    while (count + day * (day + 1) // 2 < n):

        # Find the number of presents
        # given on day is day*(day+1)/2
        count += day * (day + 1) // 2;
        day += 1

    type = day
    while(type > 0):
        # Iterate over the type
        count += type

        # Return the resultant type
        if (count >= n):
            return type

        type -= 1

# Driver Code
if __name__ == '__main__':
    N = 10
    print(itemType(N))

    # This code is contributed by bgaangwar59.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find the type of the
// item given out according to the
// given rules
static int itemType(int n)
{

    // Stores the count of item given
    // out at each step
    int count = 0;
    int day = 1;

    // Iterate to find the Nth day
    // present is given out
    while (count + day * (day + 1) / 2
           < n) {

        // Find the number of presents
        // given on day is day*(day+1)/2
        count += day * (day + 1) / 2;
        day++;
    }

    for (int type = day; type > 0; type--)
    {

        // Iterate over the type
        count += type;

        // Return the resultant type
        if (count >= n) {
            return type;
        }
    }
    return 0;
}

// Driver Code
public static void Main(String[] args)
  {
    int N = 10;
    Console.Write ( itemType(N));
}
}

// This code is contribured by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the type of the
// item given out according to the
// given rules
function itemType(n)
{

    // Stores the count of item given
    // out at each step
    let count = 0;
    let day = 1;

    // Iterate to find the Nth day
    // present is given out
    while (count + day * (day + 1) / 2 < n)
    {

        // Find the number of presents
        // given on day is day*(day+1)/2
        count += day * (day + 1) / 2;
        day++;
    }

    for(let type = day; type > 0; type--)
    {

        // Iterate over the type
        count += type;

        // Return the resultant type
        if (count >= n)
        {
            return type;
        }
    }
}

// Driver code
let N = 10;

document.write(itemType(N));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(1)*