# 组织比武问题

> 原文:[https://www . geesforgeks . org/org-组织-锦标赛-问题/](https://www.geeksforgeeks.org/organizing-tournament-problem/)

给定一个正整数 **N** 表示玩游戏的玩家数。游戏在两个队之间进行，每个队至少由一名玩家组成，但是游戏中玩家的总数必须是 **N** 。游戏正好持续 **30 分钟**，任务是检查所有玩家是否会对战游戏如果游戏可以玩到 **T** 小时并且允许玩游戏超过 **1** 次。如果发现为真，则打印**“可能”**。否则，打印**“不可能”**。

**示例:**

> **输入:** N = 3，T = 1
> **输出:**可能
> **解释:**
> 前半小时玩家{ p <sub>1</sub> ，p <sub>2</sub> }与{ p <sub>3</sub> 进行了对局。
> 在 2d 半小时内，玩家{ p <sub>2</sub> 、P <sub>3</sub> }与{ p <sub>1</sub> }
> 进行了比赛，因为所有玩家都在 T(=1)小时内进行了比赛。因此，所需的输出是“可能的”。
> 
> **输入:** N = 4，T = 0.5
> **输出:**不可能
> **解释:**
> 前半小时玩家{ p <sub>1</sub> ，p <sub>2</sub> }与{ p <sub>3</sub> ，p <sub>4</sub> 进行了对局。
> 由于玩家 p <sub>1</sub> 没有在 T(=0.5)小时内与 p <sub>2</sub> 进行比赛。因此，要求的输出是“不可能”。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。以下是观察结果:

> *   In each game, if one of the two teams has only one player, then the game must be played [T0】 N-1 【T1 times.
> *   Every game, if one team has **n/2** players and the other team has **(n+1)/2** , the game must play **(n+1)/2** times.

按照以下步骤解决问题:

*   如果游戏总时间 **N-1** 次小于或等于 **T** ，则打印**“可能”**。
*   如果游戏总时间 **(N + 1) / 2** 次小于或等于 **T** ，则打印**“可能”**。
*   否则，打印**“不可能”**。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <iostream>
using namespace std;

// Function to find the N players
// the game against each other or not
string calculate(int N, int T)
{

   // Base Case
    if (N <= 1 || T <= 0) {

      // Return -1 if not valid
        return "-1";
    }

  // Converting hours into minutes
    int minutes = T * 60;

   // Calculating maximum games that
    // can be played.
    int max_match = N - 1;

  // Time required for conducting
    // maximum games
    int max_time = max_match * 30;

  // Checking if it is possible
    // to conduct maximum games
    if (max_time <= minutes) {

      // Return possible
        return "Possible";
    }

  // Calculating minimum games
    int min_match = N / 2;
    min_match = N - min_match;

  // Time required for conducting
    // minimum games
    int min_time = min_match * 30;

  // Checking if it is possible
   // to conduct minimum games
    if (min_time <= minutes) {

      // Return possible
        return "Possible";
    }

  // Return not possible if time
   // is less than required time
    return "Not Possible";
}

 // Driver Code
 // Total count of players
int main()
{
    int N = 6, T = 2;

  // function call
    cout << calculate(N, T);
    return 0;
}

// This code is contributed by Parth Manchanda
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to find the N players
// the game against each other or not
static String calculate(int N, int T)
{

   // Base Case
    if (N <= 1 || T <= 0) {

      // Return -1 if not valid
        return "-1";
    }

  // Converting hours into minutes
    int minutes = T * 60;

   // Calculating maximum games that
    // can be played.
    int max_match = N - 1;

  // Time required for conducting
    // maximum games
    int max_time = max_match * 30;

  // Checking if it is possible
    // to conduct maximum games
    if (max_time <= minutes) {

      // Return possible
        return "Possible";
    }

  // Calculating minimum games
    int min_match = N / 2;
    min_match = N - min_match;

  // Time required for conducting
    // minimum games
    int min_time = min_match * 30;

  // Checking if it is possible
   // to conduct minimum games
    if (min_time <= minutes) {

      // Return possible
        return "Possible";
    }

  // Return not possible if time
   // is less than required time
    return "Not Possible";
}

// Driver code
public static void main(String[] args)
{
    int N = 6, T = 2;

    // function call
    System.out.println(calculate(N, T));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above problem

# Function to find the N players
# the game against each other or not
def calculate(N, T):

    # Base Case
    if N <= 1 or T <= 0:

        # Return -1 if not valid
        return -1

    # Converting hours into minutes
    minutes = T * 60

    # Calculating maximum games that
    # can be played.
    max_match = N - 1

    # Time required for conducting
    # maximum games
    max_time = max_match * 30

    # Checking if it is possible
    # to conduct maximum games
    if max_time <= minutes:

        # Return possible
        return "Possible"

    # Calculating minimum games
    min_match = N//2
    min_match = N - min_match

    # Time required for conducting
    # minimum games
    min_time = min_match * 30

    # Checking if it is possible
    # to conduct minimum games
    if min_time <= minutes:

        # Return possible
        return "Possible"

    # Return not possible if time
    # is less than required time
    return "Not Possible"

# Driver Code
if __name__ == "__main__":

    # Total count of players
    N = 6

    # Given hours
    T = 2

    # Function call
    ans = calculate(N, T)

    # Print ans
    print(ans)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the N players
// the game against each other or not
static string calculate(int N, int T)
{

   // Base Case
    if (N <= 1 || T <= 0) {

      // Return -1 if not valid
        return "-1";
    }

  // Converting hours into minutes
    int minutes = T * 60;

   // Calculating maximum games that
    // can be played.
    int max_match = N - 1;

  // Time required for conducting
    // maximum games
    int max_time = max_match * 30;

  // Checking if it is possible
    // to conduct maximum games
    if (max_time <= minutes) {

      // Return possible
        return "Possible";
    }

  // Calculating minimum games
    int min_match = N / 2;
    min_match = N - min_match;

  // Time required for conducting
    // minimum games
    int min_time = min_match * 30;

  // Checking if it is possible
   // to conduct minimum games
    if (min_time <= minutes) {

      // Return possible
        return "Possible";
    }

  // Return not possible if time
   // is less than required time
    return "Not Possible";
}

// Driver Code
public static void Main(String[] args)
{
    int N = 6, T = 2;

  // function call
    Console.WriteLine(calculate(N, T));
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to find the N players
       // the game against each other or not
       function calculate(N, T)
       {

           // Base Case
           if (N <= 1 || T <= 0)
           {

               // Return -1 if not valid
               return -1;
           }

           // Converting hours into minutes
           let minutes = T * 60;

           // Calculating maximum games that
           // can be played.
           let max_match = N - 1

           // Time required for conducting
           // maximum games
           max_time = max_match * 30

           // Checking if it is possible
           // to conduct maximum games
           if (max_time <= minutes)
           {

               // Return possible
               return "Possible";
           }

           // Calculating minimum games
           min_match = Math.floor(N / 2);
           min_match = N - min_match

           // Time required for conducting
           // minimum games
           min_time = min_match * 30;

           // Checking if it is possible
           // to conduct minimum games
           if (min_time <= minutes)
           {

               // Return possible
               return "Possible";

               // Return not possible if time
               // is less than required time
               return "Not Possible";
           }

       }

       // Driver Code
       // Total count of players
       let N = 6

       // Given hours
       let T = 2

       // Function call
       let ans = calculate(N, T)

       // Print ans
       document.write(ans);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
Possible
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)