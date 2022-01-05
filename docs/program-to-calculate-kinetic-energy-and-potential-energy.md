# 计算动能和势能的程序

> 原文:[https://www . geesforgeks . org/计算动能和势能的程序/](https://www.geeksforgeeks.org/program-to-calculate-kinetic-energy-and-potential-energy/)

给定分别代表物体质量、速度和高度的三个浮点值 **M** 、 **H** 和 **V** ，任务是计算其[动能](https://www.geeksforgeeks.org/kinetic-energy/)以及[势能](https://en.wikipedia.org/wiki/Potential_energy)、
***注:**重力加速度值(g)为 9.8，忽略单位。*

**示例:**

> **输入:** M = 25，H = 10，V = 15
> **输出:**
> 动能= 2812.5
> 势能= 2450
> **说明:**粒子动能为 2812.5，势能为 2450。
> 
> **输入:** M=5.5，H=23.5，V = 10.5
> T3】输出:T5】303.188
> 1266.65

**方法:**动能和势能的要求值可以用以下两个公式计算:

> 动能= 0.5 *质量(M ) *速度(V ) <sup>2</sup>

> 势能=质量(M ) *高度(H ) *重力加速度(g)

下面是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate Kinetic Energy
float kineticEnergy(float M, float V)
{
    // Stores the Kinetic Energy
    float KineticEnergy;

    KineticEnergy = 0.5 * M * V * V;

    return KineticEnergy;
}

// Function to calculate Potential Energy
float potentialEnergy(float M, float H)
{
    // Stores the Potential Energy
    float PotentialEnergy;

    PotentialEnergy = M * 9.8 * H;

    return PotentialEnergy;
}

// Driver Code
int main()
{
    float M = 5.5, H = 23.5, V = 10.5;

    cout << "Kinetic Energy = "
         << kineticEnergy(M, V) << endl;
    cout << "Potential Energy = "
         << potentialEnergy(M, H) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to calculate Kinetic Energy
static double kineticEnergy(double M, double V)
{

    // Stores the Kinetic Energy
    double KineticEnergy;

    KineticEnergy = 0.5 * M * V * V;

    return KineticEnergy;
}

// Function to calculate Potential Energy
static double potentialEnergy(double M, double H)
{

    // Stores the Potential Energy
    double PotentialEnergy;

    PotentialEnergy = M * 9.8 * H;

    return PotentialEnergy;
}

// Driver Code
public static void main(String []args)
{
    double M = 5.5, H = 23.5, V = 10.5;

    System.out.println("Kinetic Energy = " +
                       kineticEnergy(M, V));
    System.out.println("Potential Energy = " +
                       potentialEnergy(M, H));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate Kinetic Energy
def kineticEnergy(M, V):

    # Stores the Kinetic Energy
    KineticEnergy = 0.5 * M * V * V

    return KineticEnergy

# Function to calculate Potential Energy
def potentialEnergy(M, H):

    # Stores the Potential Energy
    PotentialEnergy = M * 9.8 * H

    return PotentialEnergy

# Driver Code
if __name__ ==  "__main__":

    M = 5.5
    H = 23.5
    V = 10.5

    print("Kinetic Energy = ", kineticEnergy(M, V))
    print("Potential Energy = ", potentialEnergy(M, H))

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

/// Function to calculate Kinetic Energy
static double kineticEnergy(double M, double V)
{

    // Stores the Kinetic Energy
    double KineticEnergy;

    KineticEnergy = 0.5 * M * V * V;

    return KineticEnergy;
}

// Function to calculate Potential Energy
static double potentialEnergy(double M, double H)
{

    // Stores the Potential Energy
    double PotentialEnergy;

    PotentialEnergy = M * 9.8 * H;

    return PotentialEnergy;
}

// Driver Code
public static void Main()
{
    double M = 5.5, H = 23.5, V = 10.5;

    Console.WriteLine("Kinetic Energy = " +
                      kineticEnergy(M, V));
    Console.Write("Potential Energy = " +
                  potentialEnergy(M, H));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

      // Javascript program for the above approach

      // Function to calculate Kinetic Energy
        function kineticEnergy(M, V)
        {
          // Stores the Kinetic Energy
            let KineticEnergy;

            KineticEnergy = 0.5 * M * V * V;

            return KineticEnergy;
        }

        // Function to calculate Potential Energy
        function potentialEnergy(M, H) {
            // Stores the Potential Energy
            let PotentialEnergy;

            PotentialEnergy = M * 9.8 * H;

            return PotentialEnergy;
        }

        // Driver Code

        let M = 5.5, H = 23.5, V = 10.5;

        document.write("Kinetic Energy = "
            + kineticEnergy(M, V))

        document.write("<br>");

        document.write( "Potential Energy = "
            + potentialEnergy(M, H))

        // This code is contributed by Hritik

 </script>
```

**Output:** 

```
Kinetic Energy = 303.188
Potential Energy = 1266.65
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)