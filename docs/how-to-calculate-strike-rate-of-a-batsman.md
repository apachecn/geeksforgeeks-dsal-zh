# 击球手的打击率如何计算

> 原文:[https://www . geesforgeks . org/击球手击球率计算方法/](https://www.geeksforgeeks.org/how-to-calculate-strike-rate-of-a-batsman/)

给定两个整数 **A** 和 **B** ，代表板球比赛中击球手得分和面对的球。任务是计算击球手的[打击率](https://en.wikipedia.org/wiki/Strike_rate)。

> 击球率是衡量击球手达到击球主要目标的速度。数学上等于:
> **打击率=(得分/面对球数)* 100**

**示例:**

> **输入:** A = 264，B = 173
> **输出:** 152.601
> **说明:**
> 击球员的斯瑞克率等于(264 / 173) * 100 = 162.601
> 
> **输入:** A = 0，B = 10
> T3】输出: 0.00

**进场:**

1.  使用罢工率公式计算罢工率。
    **打击率=(得分/面对球数)* 100**
2.  以浮点数据类型格式返回罢工率。

下面是上述方法的实现:

## C++

```
// C++ program to calculate strike
// rate of a batsman

#include <bits/stdc++.h>
using namespace std;

// function to calculate strike
// rate of a batsman
float strikerate(int bowls, int runs)
{
    float z;
    z = (float(runs) / bowls) * 100;
    return z;
}

// Driver Code
int main()
{
    int A, B;
    A = 264;
    B = 173;

    cout << strikerate(B, A)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate strike
// rate of a batsman
class GFG{

// function to calculate strike
// rate of a batsman
static float strikerate(float bowls, float runs)
{
    float z;
    z = (runs / bowls) * 100;
    return z;
}

// Driver Code
public static void main(String[] args)
{
    int A, B;
    A = 264;
    B = 173;

    System.out.println(strikerate(B, A));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to calculate strike
# rate of a batsman

# function to calculate strike
# rate of a batsman
def strikerate(bowls, runs):

    z = (float(runs) / bowls) * 100;
    return z;

# Driver Code
A = 264;
B = 173;
print(strikerate(B, A));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to calculate strike
// rate of a batsman
using System;
class GFG{

// function to calculate strike
// rate of a batsman
static float strikerate(float bowls,
                        float runs)
{
    float z;
    z = (runs / bowls) * 100;
    return z;
}

// Driver Code
public static void Main()
{
    int A, B;
    A = 264;
    B = 173;

    Console.Write(strikerate(B, A));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to calculate strike
// rate of a batsman

// function to calculate strike
// rate of a batsman
function strikerate(bowls, runs)
{
    let z;
    z = (runs / bowls) * 100;
    return z.toFixed(3);
}

// Driver code   
let A, B;
A = 264;
B = 173;

document.write(strikerate(B, A));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
152.601
```

***时间复杂度:** O (1)*
***辅助空间:** O (1)*