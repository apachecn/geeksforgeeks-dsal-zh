# 根据给定的条件计算 N 天后的分数总和

> 原文:[https://www . geesforgeks . org/基于给定条件计算 n 天后的分数总和/](https://www.geeksforgeeks.org/calculate-sum-of-scores-after-n-days-based-on-given-conditions/)

给定一个代表天数的整数 **N，**，任务是根据以下条件求出 **N** 天后的分数之和:

*   在第一个**周一**，分数被设置为 **1** 。
*   在每一个**周一**的时候，比分变成 **1** 大于前一个**周一的比分。**
*   每隔一天，分数变得等于 **1** 大于前一天的分数。

**示例:**

> **输入:** N=4
> **输出:** 10
> **说明:**
> 四天每天的分数如下:
> 周一:1
> 周二:2
> 周三:3
> 周四:4
> 分数总和= 1 + 2 + 3 + 4 = 10
> 
> **输入:** N=8
> **输出:** 30
> **说明:**
> 这 8 天每天的分数如下:
> 周一:1
> 周二:2
> 周三:3
> 周四:4
> 周五:5
> 周六:6
> 周日:7
> 周一:2
> 分数总和= 1 + 2 + 3 + 4 + 5 + 6 + 7

**天真法:**解决问题最简单的方法就是[遍历](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**的范围，每天不停的加分数。最后，打印获得的所有分数的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to c sum of calculate
// sum of scores after n days
void findScoreSum(int n)
{
    // Store the required sum
    int total = 0;

    // Store the score on previous
    // monday and current day respectively
    int prev_monday = 0, curr_day = 0;

    // Iterate over the range [1, n]
    for (int day = 1; day <= n; day++) {

        // If the current day is monday
        if (day % 7 == 1) {

            // Increment score of
            // prev_monday by 1
            prev_monday++;

            // Update score of current day
            curr_day = prev_monday;
        }

        // Add score of current day and
        // increment score for next day
        total += curr_day++;
    }

    // Print the result
    cout << total;
}

// Driver Code
int main()
{
    int N = 8;
    findScoreSum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
class GFG
{

  // Function to c sum of calculate
  // sum of scores after n days
  static void findScoreSum(int n)
  {

    // Store the required sum
    int total = 0;

    // Store the score on previous
    // monday and current day respectively
    int prev_monday = 0, curr_day = 0;

    // Iterate over the range [1, n]
    for (int day = 1; day <= n; day++)
    {

      // If the current day is monday
      if (day % 7 == 1)
      {

        // Increment score of
        // prev_monday by 1
        prev_monday++;

        // Update score of current day
        curr_day = prev_monday;
      }

      // Add score of current day and
      // increment score for next day
      total += curr_day++;
    }

    // Print the result
    System.out.println(total);
  }

  // Driver Code
  public static void main (String[] args)
  {
    int N = 8;
    findScoreSum(N);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to c sum of calculate
# sum of scores after n days
def findScoreSum(n):

    # Store the required sum
    total = 0

    # Store the score on previous
    # monday and current day respectively
    prev_monday, curr_day = 0, 0

    # Iterate over the range [1, n]
    for day in range(1, n + 1):

        # If the current day is monday
        if (day % 7 == 1):

            # Increment score of
            # prev_monday by 1
            prev_monday += 1

            # Update score of current day
            curr_day = prev_monday

        # Add score of current day and
        # increment score for next day
        total += curr_day
        curr_day += 1

    # Print the result
    print(total)

# Driver Code
if __name__ == '__main__':

    N = 8

    findScoreSum(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to implement
// the above approach
using System;

class GFG
{

// Function to c sum of calculate
// sum of scores after n days
static void findScoreSum(int n)
{
    // Store the required sum
    int total = 0;

    // Store the score on previous
    // monday and current day respectively
    int prev_monday = 0, curr_day = 0;

    // Iterate over the range [1, n]
    for (int day = 1; day <= n; day++) {

        // If the current day is monday
        if (day % 7 == 1) {

            // Increment score of
            // prev_monday by 1
            prev_monday++;

            // Update score of current day
            curr_day = prev_monday;
        }

        // Add score of current day and
        // increment score for next day
        total += curr_day++;
    }

    // Print the result
    Console.Write(total);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 8;
    findScoreSum(N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to c sum of calculate
// sum of scores after n days
function findScoreSum(n)
{

    // Store the required sum
    let total = 0;

    // Store the score on previous
    // monday and current day respectively
    let prev_monday = 0, curr_day = 0;

    // Iterate over the range [1, n]
    for(let day = 1; day <= n; day++)
    {

        // If the current day is monday
        if (day % 7 == 1)
        {

            // Increment score of
            // prev_monday by 1
            prev_monday++;

            // Update score of current day
            curr_day = prev_monday;
        }

        // Add score of current day and
        // increment score for next day
        total += curr_day++;
    }

    // Print the result
    document.write(total);
}

// Driver code
let N = 8;

findScoreSum(N);

// This code is contributed by target_2

</script>
```

**Output:** 

```
30
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**上述方法可以基于以下观察进行优化:

> 让整周数为 **F** ，剩余天数为 **D** 。
> 第 **N** 天之后的分数总和=第 **F** 周的分数总和+剩余 **D** 天的分数总和
> 
> 第一 **F** 周得分之和:
> 第一**周得分之和= 1 + 2 + 3 + … + 7
> 第二**周得分之和= 2 + 3 + 4 + … + 8 = 7*1 + (1 + 2 + 3 + … + 7)
> 第三**周的分数总和= 3+4+5+……+9 = 7 * 2+(1+2+3+……+7)
> ……
> 第 F <sup>周的分数总和= 7 *(F–1)+(1+2+3+……+7)
> 前 F 周的分数总和= F *(1+2+3+……+7) +7(1+2+……+(F–1))
> = F *(7 * 8)/2)+7 *(F *(F–1)/2)
> = F/2 *(49+7 * F)</sup>**
> 
> 剩余 **D** 天得分之和:
> 剩余 **D** 天得分之和=(F+1)+(F+2)+……+(F+D)
> = F * D+D *(D+1)/2
> = D/2 *(2 * F+D+1)

所以，分数的总和就是**【F/2 *(49+7 * F)】+【D/2 *(2 * F+D+1)】**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum
// of scores after n days
void findScoreSum(int n)
{
    // Store the number
    // of full weeks
    int F = n / 7;

    // Stores the remaining
    // days in the last week
    int D = n % 7;

    // Store the sum of scores
    // in the first F full weeks
    int fullWeekScore
        = (49 + 7 * F) * F / 2;

    // Store the sum of scores
    // in the last week
    int lastNonFullWeekScore
        = (2 * F + D + 1) * D / 2;

    // Print the result
    cout << fullWeekScore + lastNonFullWeekScore;
}

// Driver Code
int main()
{
    int N = 8;
    findScoreSum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to calculate sum
  // of scores after n days
  static void findScoreSum(int n)
  {
    // Store the number
    // of full weeks
    int F = n / 7;

    // Stores the remaining
    // days in the last week
    int D = n % 7;

    // Store the sum of scores
    // in the first F full weeks
    int fullWeekScore = (49 + 7 * F) * F / 2;

    // Store the sum of scores
    // in the last week
    int lastNonFullWeekScore = (2 * F + D + 1) * D / 2;

    // Print the result
    System.out.println(fullWeekScore
                       + lastNonFullWeekScore);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 8;
    findScoreSum(N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum
# of scores after n days
def findScoreSum(n):
    # Store the number
    # of full weeks
    F = n // 7

    # Stores the remaining
    # days in the last week
    D = n % 7

    # Store the sum of scores
    # in the first F full weeks
    fullWeekScore = (49 + 7 * F) * F // 2

    # Store the sum of scores
    # in the last week
    lastNonFullWeekScore = (2 * F + D + 1) * D // 2

    # Print the result
    print(fullWeekScore + lastNonFullWeekScore)

# Driver Code
if __name__ == '__main__':
    N = 8
    findScoreSum(N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum
// of scores after n days
static void findScoreSum(int n)
{

    // Store the number
    // of full weeks
    int F = n / 7;

    // Stores the remaining
    // days in the last week
    int D = n % 7;

    // Store the sum of scores
    // in the first F full weeks
    int fullWeekScore = (49 + 7 * F) * F / 2;

    // Store the sum of scores
    // in the last week
    int lastNonFullWeekScore = (2 * F + D + 1) * D / 2;

    // Print the result
    Console.WriteLine(fullWeekScore +
                      lastNonFullWeekScore);
}

// Driver Code
static public void Main()
{
    int N = 8;

    findScoreSum(N);
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

  // Function to calculate sum
  // of scores after n days
  function findScoreSum(n)
  {
    // Store the number
    // of full weeks
    let F = n / 7;

    // Stores the remaining
    // days in the last week
    let D = n % 7;

    // Store the sum of scores
    // in the first F full weeks
    let fullWeekScore = (49 + 7 * F) * F / 2;

    // Store the sum of scores
    // in the last week
    let lastNonFullWeekScore = (2 * F + D + 1) * D / 2;

    // Prlet the result
    document.write(Math.floor(fullWeekScore
                       + lastNonFullWeekScore));
  }

// Driver code
    let N = 8;
    findScoreSum(N);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
30
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)