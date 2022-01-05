# 计算一个粒子所做的功和消耗的功率

> 原文:[https://www . geeksforgeeks . org/计算一个粒子所做的功和消耗的功率/](https://www.geeksforgeeks.org/calculate-work-done-and-power-consumed-by-a-particle/)

给定三个整数 **F、D** 和 **T** ，分别代表作用在粒子上的力、粒子移动的位移和消耗的时间，任务是计算该粒子所做的功( **W** )和消耗的功率( **P** )。

**示例:**

> **输入:** F = 100，D = 20，T = 100
> **输出:**
> 完成功:2000
> 消耗功率:200
> 
> **输入:** F=40.2，D=10.6，T=20
> **输出:**
> 完成功:426.12
> 消耗功率:21.306

**方法:**使用以下公式计算完成的功和消耗的功率可以解决该问题:

> 做功(W) =作用在质点上的力(F) *质点的位移(D)

> 消耗的功率(P) =作用在粒子上的力(F) *粒子的位移(D) /消耗的时间(T)

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate work done
float workDone(float F, float D)
{
    // Stores the work done
    float W;
    W = F * D;

    return W;
}
// Function to calculate power consumed
float power(float F, float D, float T)
{
    // Stores the amount
    // of power consumed
    float P;
    P = (F * D) / T;

    return P;
}

// Driver Code
int main()
{
    float F = 100, D = 20, T = 100;

    cout << workDone(F, D) << endl;
    cout << power(F, D, T) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to calculate work done
static float workDone(float F, float D)
{

    // Stores the work done
    float W;
    W = F * D;

    return W;
}

// Function to calculate power consumed
static float power(float F, float D, float T)
{

    // Stores the amount
    // of power consumed
    float P;
    P = (F * D) / T;

    return P;
}

// Driver code
public static void main(String[] args)
{
    float F = 100, D = 20, T = 100;

    System.out.println(workDone(F, D));
    System.out.println(power(F, D, T));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate work done
def workDone(F, D):

    return F * D

# Function to calculate power consumed
def power(F, D, T):

    return ((F * D) / T)

# Driver code
F = 100
D = 20
T = 100

print(workDone(F, D))
print(power(F, D, T))

# This code is contributed by abhinavjain194
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate work done
static float workDone(float F, float D)
{

    // Stores the work done
    float W;
    W = F * D;

    return W;
}

// Function to calculate power consumed
static float power(float F, float D, float T)
{

    // Stores the amount
    // of power consumed
    float P;
    P = (F * D) / T;

    return P;
}

// Driver code
static void Main()
{
    float F = 100, D = 20, T = 100;

    Console.WriteLine(workDone(F, D));
    Console.WriteLine(power(F, D, T));
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to calculate work done
function workDone(F, D)
{

    // Stores the work done
    var W;
    W = F * D;

    return W;
}

// Function to calculate power consumed
function power(F, D, T)
{

    // Stores the amount
    // of power consumed
    var P;
    P = (F * D) / T;

    return P;
}

// Driver code
var F = 100, D = 20, T = 100;

document.write(workDone(F, D) + "<br>");
document.write(power(F, D, T));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
2000
20
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)