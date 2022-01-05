# 找出击球手的击球率

> 原文:[https://www . geesforgeks . org/find-击球手的平均击球率/](https://www.geeksforgeeks.org/find-the-batting-average-of-a-batsman/)

给定三个整数**分别代表得分的跑数、**、**匹配**、**未出局**代表击球手打出的局数和他保持未出局的次数，任务是计算击球手的[击球率](https://en.wikipedia.org/wiki/Batting_average_(cricket))。

> ![\text{Batting Average} = \frac{\text{Runs Scored}}{\text{Number of dismissals}}   ](img/2628788556db1af888f381602f84e03b.png "Rendered by QuickLaTeX.com")
> 
> ![\text{Number of dismissals = Number of innings - Number of innings he remained Not Out}   ](img/bc6ffe37f61e28dbb9a3afbcf3364322.png "Rendered by QuickLaTeX.com")

**注:**如果击球手从未被解雇，则打印“NA”作为可以定义的无平均值。

**示例:**

> **输入:**跑位= 10000，匹配= 250，不出局= 50
> **输出:** 50
> **说明:**
> 击球手被解雇次数= 250–50 = 200
> 击球率= 10000 / 200 = 50。
> 
> **输入:**运行= 100，匹配= 1，非输出= 1
> T3】输出: NA

**方法:**
按照以下步骤解决问题:

1.  计算解雇次数，等于**匹配-不匹配**。
2.  计算击球率，等于**跑/(比赛–不出局)**。

下面是上述方法的实现:

## C++

```
// C++ program to calculate
// the average of a batsman
#include <bits/stdc++.h>
using namespace std;

// Function to find the average
// of a batsman
double averageRuns(int runs,
                   int matches,
                   int notout)
{
    // Calculate number of
    // dismissals
    int out = matches - notout;

    // check for 0 times out
    if (out == 0)
        return -1;

    // Calculate batting average
    double avg = double(runs) / out;

    return avg;
}

// Driver Program
int main()
{
    int runs = 10000;
    int matches = 250;
    int notout = 50;

    double avg
        = averageRuns(
            runs, matches, notout);

    if (avg == -1)
        cout << "NA";
    else
        cout << avg;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the average of a batsman
class GFG{

// Function to find the average
// of a batsman
static int averageRuns(int runs,
                       int matches,
                       int notout)
{

    // Calculate number of
    // dismissals
    int out = matches - notout;

    // Check for 0 times out
    if (out == 0)
        return -1;

    // Calculate batting average
    int avg = (runs) / out;

    return avg;
}

// Driver code
public static void main(String[] args)
{
    int runs = 10000;
    int matches = 250;
    int notout = 50;

    int avg = averageRuns(runs, matches,
                                notout);
    if (avg == -1)
        System.out.print("NA");
    else
        System.out.print(avg);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to calculate
# the average of a batsman

# Function to find the average
# of a batsman
def averageRuns(runs, matches, notout):

    # Calculate number of
    # dismissals
    out = matches - notout;

    # check for 0 times out
    if (out == 0):
        return -1;

    # Calculate batting average
    avg = runs // out;

    return avg;

# Driver Program
runs = 10000;
matches = 250;
notout = 50;

avg = averageRuns(runs, matches, notout);

if (avg == -1):
    print("NA");
else:
    print(avg);

# This code is contributed by Akanksha_rai
```

## C#

```
// C# program to calculate
// the average of a batsman
using System;
class GFG{

// Function to find the average
// of a batsman
static int averageRuns(int runs,
                       int matches,
                       int notout)
{

    // Calculate number of
    // dismissals
    int out1;
    out1 = matches - notout;

    // Check for 0 times out
    if (out1 == 0)
        return -1;

    // Calculate batting average
    int avg = (runs) / out1;

    return avg;
}

// Driver code
public static void Main (string[] args)
{
    int runs = 10000;
    int matches = 250;
    int notout = 50;

    int avg = averageRuns(runs, matches,
                                notout);
    if (avg == -1)
        Console.Write("NA");
    else
        Console.Write(avg);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to calculate
// the average of a batsman

// Function to find the average
// of a batsman
function averageRuns(runs, matches, notout)
{

    // Calculate number of
    // dismissals
    let out1;
    out1 = matches - notout;

    // Check for 0 times out
    if (out1 == 0)
        return -1;

    // Calculate batting average
    let avg = parseInt((runs) / out1, 10);

    return avg;
}

// Driver code     
let runs = 10000;
let matches = 250;
let notout = 50;
let avg = averageRuns(runs, matches, notout);

if (avg == -1)
    document.write("NA");
else
    document.write(avg);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
50
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*