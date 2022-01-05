# 骰子问题

> 原文:[https://www.geeksforgeeks.org/the-dice-problem/](https://www.geeksforgeeks.org/the-dice-problem/)

给你一个有 **6** 面的**立方骰子**。所有的个人脸上都印着一个数字。像任何普通骰子一样，数字在 **1 到 6** 的范围内。你将得到这个立方体的一个面，你的任务是猜测立方体反面的数字。

**示例:**

> **输入:** N = 2
> **输出:** 5
> **说明:**
> 对于面向 5 号对面的骰子面会有 2 号。
> 
> **输入:**N = 6
> T3】输出: 1

**天真方法:**在正常的 6 面骰子中，1 与 6 相对，2 与 5 相对，3 与 4 相对。因此，可以放置一个正常的 if-else-if 块

**方法:**这个想法是基于一个立方体骰子的两个相对面之和等于 **7** 的观察。所以，只要从 **7** 中减去给定的 **N** 就可以打印答案了。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find number
// written on the
// opposite face of the dice
int oppositeFaceOfDice(int N)
{
    // Stores number on opposite face
    // of dice
    int ans = 7 - N;

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given value of N
    int N = 2;

    // Function call to find number written on
    // the opposite face of the dice
    oppositeFaceOfDice(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find number
    // written on the
    // opposite face of the dice
    static void oppositeFaceOfDice(int N)
    {

        // Stores number on opposite face
        // of dice
        int ans = 7 - N;

        // Print the answer
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given value of N
        int N = 2;

        // Function call to find number written on
        // the opposite face of the dice
        oppositeFaceOfDice(N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find number written on the
# opposite face of the dice
def oppositeFaceOfDice(N):

    # Stores number on opposite face
    # of dice
    ans = 7 - N

    # Print the answer
    print(ans)

# Driver Code

# Given value of N
N = 2

# Function call to find number written on
# the opposite face of the dice
oppositeFaceOfDice(N)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find number
// written on the
// opposite face of the dice
static void oppositeFaceOfDice(int N)
{

    // Stores number on opposite face
    // of dice
    int ans = 7 - N;

    // Print the answer
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    // Given value of N
    int N = 2;

    // Function call to find number written on
    // the opposite face of the dice
    oppositeFaceOfDice(N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find number
// written on the
// opposite face of the dice
function oppositeFaceOfDice(N) {
  // Stores number on opposite face
  // of dice
  let ans = 7 - N;

  // Print the answer
  document.write(ans);
}

// Driver Code

// Given value of N
let N = 2;

// Function call to find number written on
// the opposite face of the dice
oppositeFaceOfDice(N);

// This code is contributed by gfgking

</script>
```

**Output**

```
5
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)