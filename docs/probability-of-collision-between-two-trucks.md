# 两辆卡车相撞的概率

> 原文:[https://www . geesforgeks . org/两辆卡车相撞概率/](https://www.geeksforgeeks.org/probability-of-collision-between-two-trucks/)

给定两条[线](https://www.geeksforgeeks.org/string-data-structure/)T2 S 和 **T** ，其中 **S** 代表车辆从左向右移动的第一条车道， **T** 代表车辆从右向左移动的第二条车道。车辆可以是 **B(自行车)**、 **C(汽车)**，也可以是 **T(卡车)**。任务是找出两辆卡车相撞的概率。

**示例:**

> **输入:** S = "TCCBCTTB "，T = "BTCCBBTT"
> **输出:** 0.194444
> **解释:**
> 总碰撞= 7
> 总事故= 36
> 因此，概率可按 7/36 = 0.19444 计算。
> 
> **输入:** S = "BTT "，T = " BTCBT "
> T3】输出: 0.25000

插图:

```
S = "TCCBCTTB", T = "BTCCBBTT"

Possible cases   | Accidents | Collision
-----------------------------------------       
TCCBCT<u>T</u>B         |           |
BTCCBB<u>T</u>T         |     8     |   1
                 |           | 
 <u>T</u>CCBC<u>TT</u>B        |           |
B<u>T</u>CCBB<u>TT         |     7</u>     |   3
 |           |
  TCCBC<u>T</u>TB       |           |
BTCCBBT<u>T</u>         |     6     |   1
                 |           |
   TCCBCTTB      |           |
BTCCBBTT |     5     |   0
                 |           |
    TCCBCTTB     |           |
BTCCBBTT         |     4     |   0
                 |           |
     TCCBCTTB    |           |
BTCCBBTT         |     3     |   0
                 |           |
      <u>T</u>CCBCTTB   |           |
BTCCBB<u>T</u>T         |     2     |   1
                 |           |
       <u>T</u>CCBCTTB  |           |
BTCCBBT<u>T</u>         |     1     |   1

Total number of accidents: 8+7+6+5+4+3+2+1=36
Total number of collision: 1+3+1+0+0+0+1+1=7
Probability: 7/36=0.19444
```

**方法:**按照以下步骤解决问题:

*   找出有利结果的总数作为碰撞总数(卡车之间的事故)和可能结果的总数(碰撞总数)作为事故总数。
*   初始化一个变量**答案**等于 **0** 来存储碰撞计数。
*   计算字符串 **T** 中的卡车数量，并将其存储在变量**计数**中。
*   [同时迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 和 **T** 的字符:
    *   如果 **S[i]** 等于**‘T’**，将**答案**增加**计数**。
    *   如果 **T[i]** 等于“T”，则按 **1** 递减**计数**。
*   现在，计算可能结果的总数(事故总数)。如果将字符串 a 向右或字符串 b 向左移动一个单位，它就是所有重叠长度的总和。
*   假设弦的长度为 **N** ，弦 b 为 **M** 。那么，重叠的总数将是:
    *   若 **N > M** 则为[前 M 个自然数](https://www.geeksforgeeks.org/sum-of-natural-numbers-using-recursion/)之和，即 **M*(M + 1)/2** 。
    *   否则为**N *(N+1)/2+(M–N)* N**。
*   求碰撞次数与事故次数之比的概率。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate total
// number of accidents
double count_of_accident(string a,
                         string b)
{
    // String size
    int n = a.size(), m = b.size();

    if (n > m)
        return (m * (m + 1)) / 2;
    else
        return (n * (n + 1))
                   / 2
               + (m - n) * n;
}

// Function to calculate count
// of all possible collision
double count_of_collision(string a,
                          string b)
{
    int n = a.size(), m = b.size();

    // Stores the count of collisions
    int answer = 0;

    // Total number of truck in lane b
    int count_of_truck_in_lane_b = 0;
    for (int i = 0; i < m; i++)
        if (b[i] == 'T')
            count_of_truck_in_lane_b++;

    // Count total number of collisions
    // while traversing the string a
    for (int i = 0; i < n && i < m; i++) {
        if (a[i] == 'T')
            answer
                += count_of_truck_in_lane_b;

        if (b[i] == 'T')
            count_of_truck_in_lane_b--;
    }
    return answer;
}

// Function to calculate the
// probability of collisions
double findProbability(string a,
                       string b)
{
    // Evaluate total outcome that is
    // all the possible accident
    double total_outcome
        = count_of_accident(a, b);

    // Evaluate favourable outcome i.e.,
    // count of collision of trucks
    double favourable_outcome
        = count_of_collision(a, b);

    // Print desired probability
    cout << favourable_outcome
                / total_outcome;
}

// Driver Code
int main()
{
    string S = "TCCBCTTB", T = "BTCCBBTT";

    // Function Call
    findProbability(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to calculate total
// number of accidents
static int count_of_accident(String a,
                         String b)
{
    // String size
    int n = a.length(), m = b.length();

    if (n > m)
        return (m * (m + 1)) / 2;
    else
        return (n * (n + 1))
                   / 2
               + (m - n) * n;
}

// Function to calculate count
// of all possible collision
static double count_of_collision(String a,
                          String b)
{
    int n = a.length(), m = b.length();

    // Stores the count of collisions
    double answer = 0;

    // Total number of truck in lane b
    int count_of_truck_in_lane_b = 0;
    for (int i = 0; i < m; i++)
        if (b.charAt(i) == 'T')
            count_of_truck_in_lane_b++;

    // Count total number of collisions
    // while traversing the String a
    for (int i = 0; i < n && i < m; i++)
    {
        if (a.charAt(i) == 'T')
            answer
                += count_of_truck_in_lane_b;

        if (b.charAt(i) == 'T')
            count_of_truck_in_lane_b--;
    }
    return answer;
}

// Function to calculate the
// probability of collisions
static void findProbability(String a,
                       String b)
{
    // Evaluate total outcome that is
    // all the possible accident
    int total_outcome
        = count_of_accident(a, b);

    // Evaluate favourable outcome i.e.,
    // count of collision of trucks
    double favourable_outcome
        = count_of_collision(a, b);

    // Print desired probability
    System.out.printf("%4f",favourable_outcome
                / total_outcome);
}

// Driver Code
public static void main(String[] args)
{
    String S = "TCCBCTTB", T = "BTCCBBTT";

    // Function Call
    findProbability(S, T);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate total
# number of accidents
def count_of_accident(a, b):

    n = len(a)
    m = len(b)

    if (n > m):
        return (m * (m + 1)) / 2
    else:
        return ((n * (n + 1)) / 2 +
                (m - n) * n)

# Function to calculate count
# of all possible collision
def count_of_collision(a, b):

    # Size of string
    n = len(a)
    m = len(b)

    # Stores the count of collisions
    answer = 0

    # Total number of truck in lane b
    count_of_truck_in_lane_b = 0

    for i in range(0, m):
        if (b[i] == 'T'):
            count_of_truck_in_lane_b += 1

    # Count total number of collisions
    # while traversing the string a
    i = 0
    while (i < m and i < n):
        if (a[i] == 'T'):
            answer += count_of_truck_in_lane_b
        if (b[i] == 'T'):
            count_of_truck_in_lane_b -= 1

        i += 1

    return answer

# Function to calculate the
# probability of collisions
def findProbability(a, b):

    # Evaluate total outcome that is
    # all the possible accident
    total_outcome = count_of_accident(a, b);

    # Evaluate favourable outcome i.e.,
    # count of collision of trucks
    favourable_outcome = count_of_collision(a, b);

    # Print desired probability
    print(favourable_outcome / total_outcome)

# Driver Code 
if __name__ == "__main__" :

    S = "TCCBCTTB"
    T = "BTCCBBTT"

    # Function Call
    findProbability(S, T)

# This code is contributed by Virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to calculate total
// number of accidents
static int count_of_accident(String a,
                         String b)
{
    // String size
    int n = a.Length, m = b.Length;

    if (n > m)
        return (m * (m + 1)) / 2;
    else
        return (n * (n + 1))
                   / 2
               + (m - n) * n;
}

// Function to calculate count
// of all possible collision
static double count_of_collision(String a,
                          String b)
{
    int n = a.Length, m = b.Length;

    // Stores the count of collisions
    double answer = 0;

    // Total number of truck in lane b
    int count_of_truck_in_lane_b = 0;
    for (int i = 0; i < m; i++)
        if (b[i] == 'T')
            count_of_truck_in_lane_b++;

    // Count total number of collisions
    // while traversing the String a
    for (int i = 0; i < n && i < m; i++)
    {
        if (a[i] == 'T')
            answer
                += count_of_truck_in_lane_b;

        if (b[i] == 'T')
            count_of_truck_in_lane_b--;
    }
    return answer;
}

// Function to calculate the
// probability of collisions
static void findProbability(String a,
                       String b)
{
    // Evaluate total outcome that is
    // all the possible accident
    int total_outcome
        = count_of_accident(a, b);

    // Evaluate favourable outcome i.e.,
    // count of collision of trucks
    double favourable_outcome
        = count_of_collision(a, b);

    // Print desired probability
    Console.Write("{0:F4}", favourable_outcome
                / total_outcome);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "TCCBCTTB", T = "BTCCBBTT";

    // Function Call
    findProbability(S, T);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to calculate total
// number of accidents
function count_of_accident(a, b)
{
    // String size
    let n = a.length, m = b.length;

    if (n > m)
        return (m * (m + 1)) / 2;
    else
        return (n * (n + 1))
                   / 2
               + (m - n) * n;
}

// Function to calculate count
// of all possible collision
function count_of_collision(a, b)
{
    let n = a.length, m = b.length;

    // Stores the count of collisions
    let answer = 0;

    // Total number of truck in lane b
    let count_of_truck_in_lane_b = 0;
    for (let i = 0; i < m; i++)
        if (b[i] == 'T')
            count_of_truck_in_lane_b++;

    // Count total number of collisions
    // while traversing the String a
    for (let i = 0; i < n && i < m; i++)
    {
        if (a[i] == 'T')
            answer
                += count_of_truck_in_lane_b;

        if (b[i] == 'T')
            count_of_truck_in_lane_b--;
    }
    return answer;
}

// Function to calculate the
// probability of collisions
function findProbability(a, b)
{
    // Evaluate total outcome that is
    // all the possible accident
    let total_outcome
        = count_of_accident(a, b);

    // Evaluate favourable outcome i.e.,
    // count of collision of trucks
    let favourable_outcome
        = count_of_collision(a, b);

    // Print desired probability
    document.write( favourable_outcome
                / total_outcome);
}

    // Driver Code

    let S = "TCCBCTTB", T = "BTCCBBTT";

    // Function Call
    findProbability(S, T);

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
0.194444
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)