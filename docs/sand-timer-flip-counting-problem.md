# 沙计时器翻转计数问题

> 原文:[https://www . geesforgeks . org/沙地-计时器-翻转-计数-问题/](https://www.geeksforgeeks.org/sand-timer-flip-counting-problem/)

给定两个整数 **A** 和 **B** ，表示两个不同的沙计时器清空所用的时间。任务是找到每个计时器的翻转计数，直到两个沙计时器同时清空的实例。
**例:**

> **输入:** A = 30，B = 15
> **输出:**0 1
> 15 分钟后:15 0
> 翻转计时器 2: 15 15
> 再过 15 分钟后:0 0
> **输入:** A = 10，B = 8
> **输出:** 3 4

**方法:** [两个数字的最低公因数](https://www.geeksforgeeks.org/lcm-and-hcf/) (LCM)将决定两个砂计时器一起清空的时间。
**【LCM(A，B) = (A * B) / GCD(A，B)**
将 LCM 除以输入将分别给出每个沙计时器的翻转次数。

## C++

```
//C++14 implementation of the approach
#include<bits/stdc++.h>
using namespace std;

//Recursive function to return
//the gcd of a and b
int gcd(int a, int b){
    //Everything divides 0
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

//Function to print the number of
//flips for both the sand timers
void flip(int a,int b){
    int lcm =(a * b)/gcd(a, b);
    a = lcm/a;
    b = lcm/b;
    cout<<a-1<<" "<<b-1;
}

//Driver code
int main(){

int a = 10;
int b = 5;
flip(a, b);

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Recursive function to return
// the gcd of a and b
static int gcd(int a, int b)
{
    // Everything divides 0
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print the number of
// flips for both the sand timers
static void flip(int a, int b)
{
    int lcm = (a * b) / gcd(a, b);
    a = lcm / a;
    b = lcm / b;
    System.out.print((a - 1) + " " + (b - 1));
}

// Driver code
public static void main(String[] args)
{
    int a = 10;
    int b = 5;
    flip(a, b);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to return
# the gcd of a and b
def gcd(a, b):

    # Everything divides 0
    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to print the number of
# flips for both the sand timers
def flip(a, b):
    lcm = (a * b) // gcd(a, b)
    a = lcm // a
    b = lcm // b
    print(a - 1, b - 1)

# Driver code
a = 10
b = 5
flip(a, b)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to return
    // the gcd of a and b
    static int gcd(int a, int b)
    {
        // Everything divides 0
        if (b == 0)
        return a;

        return gcd(b, a % b);
    }

    // Function to print the number of
    // flips for both the sand timers
    static void flip(int a, int b)
    {
        int lcm = (a * b) / gcd(a, b);
        a = lcm / a;
        b = lcm / b ;
        Console.WriteLine((a - 1) + " " +
                          (b - 1));
    }

    // Driver code
    public static void Main()
    {
        int a = 10;
        int b = 5;
        flip(a, b);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Recursive function to return
// the gcd of a and b
function gcd(a, b)
{
    // Everything divides 0
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print the number of
// flips for both the sand timers
function flip(a, b){
    let lcm =parseInt((a * b)/gcd(a, b));
    a = parseInt(lcm/a);
    b = parseInt(lcm/b);
    document.write((a-1)+" "+(b-1));
}

// Driver code
let a = 10;
let b = 5;
flip(a, b);

// This code is contributed by subham348.
</script>
```

**Output:** 

```
0 1
```