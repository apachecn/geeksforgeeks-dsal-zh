# Pentanacci 数字

> 原文:[https://www.geeksforgeeks.org/pentanacci-numbers/](https://www.geeksforgeeks.org/pentanacci-numbers/)

[**五项数列**](https://oeis.org/A001591) 是斐波那契数列的推广，其中每个项都是前面五个项的和。前几个 **Pentanacci 编号**如下–**0，0，0，0，1，1，2，4，8，16，31，61，120，236，464，912，1793，3525，6930，13624，26784，52656，103519…..**

五元数的第 n 项由下式给出:

> **T(n)= T(n-1)+T(n-2)+T(n-3)+T(n-4)+T(n-5)**
> 同 **T(0) = T(1) = T(2) = T(3) = 0，T(4) = 1**

### 找到第 N <sup>个</sup>个 Pentanacci 号

给定一个数字 **N** 。任务是找到第 N 个 Pentanacci 数。

**示例:**

> **输入:**N = 7
> T3】输出: 2
> 
> **输入:**N = 10
> T3】输出: 16

**天真法:**思路是遵循递归求数，用递归求解。

> 递推关系:
> T(n)= T(n-1)+T(n-2)+T(n-3)+T(n-4)+T(n-5)

下面是上述方法的实现:

## C++14

```
// A simple recursive program to print
// Nth Pentanacci number
#include<bits/stdc++.h>
using namespace std;

// Recursive function to find the Nth
// Pentanacci number
int printpentaRec(int n)
{
    if (n == 0 || n == 1 ||
        n == 2 || n == 3 ||
        n == 4)
        return 0;

    else if (n == 5)
        return 1;
    else
        return (printpentaRec(n - 1) +
                printpentaRec(n - 2) +
                printpentaRec(n - 3)+
                printpentaRec(n - 4)+
                printpentaRec(n - 5));
}

// Function to print the Nth
// Pentanacci number
void printPenta(int n)
{
    cout << printpentaRec(n) << "\n";
}

// Driver code
int main()
{
    int n = 10;

    printPenta(n);

    return 0;
}

// This code is contributed by yatinagg
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple recursive program to print
// Nth Pentanacci number
import java.util.*;
class GFG{

// Recursive function to find the Nth
// Pentanacci number
static int printpentaRec(int n)
{
    if (n == 0 || n == 1 ||
        n == 2 || n == 3 ||
        n == 4)
        return 0;

    else if (n == 5)
        return 1;
    else
        return (printpentaRec(n - 1) +
                printpentaRec(n - 2) +
                printpentaRec(n - 3) +
                printpentaRec(n - 4) +
                printpentaRec(n - 5));
}

// Function to print the Nth
// Pentanacci number
static void printPenta(int n)
{
    System.out.print(printpentaRec(n) + "\n");
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    printPenta(n);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# A simple recursive program to print
# Nth Pentanacci number

# Recursive program to find the Nth
# Pentanacci number
def printpentaRec(n) :
    if (n == 0 or n == 1 or\
        n == 2 or n == 3 or n == 4):
        return 0
    elif (n == 5):
        return 1
    else :
        return (printpentaRec(n - 1) +
                printpentaRec(n - 2) +
                printpentaRec(n - 3)+
                printpentaRec(n - 4)+
                printpentaRec(n - 5))

# Function to print the Nth
# Pentanacci number
def printPenta(n) :
    print(printpentaRec(n))

# Driver code
n = 10
printPenta(n)
```

## C#

```
// A simple recursive program to print
// Nth Pentanacci number
using System;

class GFG{

// Recursive function to find the Nth
// Pentanacci number
static int printpentaRec(int n)
{
    if (n == 0 || n == 1 ||
        n == 2 || n == 3 ||
        n == 4)
        return 0;

    else if (n == 5)
        return 1;
    else
        return (printpentaRec(n - 1) +
                printpentaRec(n - 2) +
                printpentaRec(n - 3) +
                printpentaRec(n - 4) +
                printpentaRec(n - 5));
}

// Function to print the Nth
// Pentanacci number
static void printPenta(int n)
{
    Console.WriteLine(printpentaRec(n));
}

// Driver code
static void Main()
{
    int n = 10;

    printPenta(n);
}
}

// This code is contributed divyeshrabadiya07
```

## java 描述语言

```
<script>
    // A simple recursive program to print
    // Nth Pentanacci number

    // Recursive function to find the Nth
    // Pentanacci number
    function printpentaRec(n)
    {
        if (n == 0 || n == 1 ||
            n == 2 || n == 3 ||
            n == 4)
            return 0;
        else if (n == 5)
            return 1;
        else
            return (printpentaRec(n - 1) +
                    printpentaRec(n - 2) +
                    printpentaRec(n - 3)+
                    printpentaRec(n - 4)+
                    printpentaRec(n - 5));
    }

    // Function to print the Nth
    // Pentanacci number
    function printPenta(n)
    {
        document.write(printpentaRec(n) + "</br>");
    }

    let n = 10;    
    printPenta(n);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
16
```

**高效途径:**思路是用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 来解决这个问题。也就是把最后四项的解用四个变量来记忆，这样就不会一次又一次地计算同一个子问题。

下面是上述方法的实现:

## C++14

```
// C++14 implementation to print
// Nth Pentanacci numbers.
#include<bits/stdc++.h>
using namespace std;

// Function to print Nth
// Pentanacci number
void printpenta(int n)
{
    if (n < 0)
        return;

    // Initialize first five
    // numbers to base cases
    int first = 0;
    int second = 0;
    int third = 0;
    int fourth = 0;
    int fifth = 1;

    // Declare a current variable
    int curr = 0;

    if (n == 0 || n == 1 ||
        n == 2 || n == 3)
        cout << first << "\n";

    else if (n == 5)
        cout << fifth << "\n";

    else
    {

        // Loop to add previous five numbers
        // for each number starting from 5
        // and then assign first, second,
        // third, fourth to second, third, fourth
        // and curr to fifth respectively
        for(int i = 5; i < n; i++)
        {
            curr = first + second +
                   third + fourth + fifth;
            first = second;
            second = third;
            third = fourth;
            fourth = fifth;
            fifth = curr;
        }
    cout << curr << "\n";
    }
}

// Driver code
int main()
{
    int n = 10;

    printpenta(n);

    return 0;
}

// This code is contributed by yatinagg
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// Nth Pentanacci numbers.
import java.util.*;
class GFG{

// Function to print Nth
// Pentanacci number
static void printpenta(int n)
{
  if (n < 0)
    return;

  // Initialize first five
  // numbers to base cases
  int first = 0;
  int second = 0;
  int third = 0;
  int fourth = 0;
  int fifth = 1;

  // Declare a current variable
  int curr = 0;

  if (n == 0 || n == 1 ||
      n == 2 || n == 3)
    System.out.print(first + "\n");
  else if (n == 5)
    System.out.print(fifth + "\n");
  else
  {
    // Loop to add previous five numbers
    // for each number starting from 5
    // and then assign first, second,
    // third, fourth to second, third,
    // fourth and curr to fifth respectively
    for(int i = 5; i < n; i++)
    {
      curr = first + second +
             third + fourth + fifth;
      first = second;
      second = third;
      third = fourth;
      fourth = fifth;
      fifth = curr;
    }
    System.out.print(curr + "\n");
  }
}

// Driver code
public static void main(String[] args)
{
  int n = 10;
  printpenta(n);   
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to print
# Nth Pentanacci numbers.

# Function to print Nth
# Pentanacci number     
def printpenta(n) :
    if (n < 0): 
        return 

    # Initialize first five 
    # numbers to base cases 
    first = 0 
    second = 0 
    third = 0 
    fourth = 0
    fifth = 1

    # declare a current variable 
    curr = 0 

    if (n == 0  or n == 1 or\
        n == 2 or n == 3): 
        print(first)
    elif (n == 5): 
        print(fifth) 

    else:

        # Loop to add previous five numbers 
        # for each number starting from 5 
        # and then assign first, second, 
        # third, fourth to second, third, fourth 
        # and curr to fifth respectively 
        for i in range(5, n):
            curr = first + second +\
                 third + fourth + fifth
            first = second 
            second = third 
            third = fourth 
            fourth = fifth
            fifth = curr 

    print(curr)  

# Driver code
n = 10
printpenta(n)
```

## C#

```
// C# implementation to print
// Nth Pentanacci numbers.
using System;
class GFG{

// Function to print Nth
// Pentanacci number
static void printpenta(int n)
{
  if (n < 0)
    return;

  // Initialize first five
  // numbers to base cases
  int first = 0;
  int second = 0;
  int third = 0;
  int fourth = 0;
  int fifth = 1;

  // Declare a current variable
  int curr = 0;

  if (n == 0 || n == 1 ||
      n == 2 || n == 3)
    Console.Write(first + "\n");
  else if (n == 5)
    Console.Write(fifth + "\n");
  else
  {
    // Loop to add previous five numbers
    // for each number starting from 5
    // and then assign first, second,
    // third, fourth to second, third,
    // fourth and curr to fifth respectively
    for(int i = 5; i < n; i++)
    {
      curr = first + second +
             third + fourth + fifth;
      first = second;
      second = third;
      third = fourth;
      fourth = fifth;
      fifth = curr;
    }
    Console.Write(curr + "\n");
  }
}

// Driver code
public static void Main(String[] args)
{
  int n = 10;
  printpenta(n);   
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // Javascript implementation to print
    // Nth Pentanacci numbers.

    // Function to print Nth
    // Pentanacci number
    function printpenta(n)
    {
      if (n < 0)
        return;

      // Initialize first five
      // numbers to base cases
      let first = 0;
      let second = 0;
      let third = 0;
      let fourth = 0;
      let fifth = 1;

      // Declare a current variable
      let curr = 0;

      if (n == 0 || n == 1 ||
          n == 2 || n == 3)
        document.write(first + "</br>");
      else if (n == 5)
        document.write(fifth + "</br>");
      else
      {
        // Loop to add previous five numbers
        // for each number starting from 5
        // and then assign first, second,
        // third, fourth to second, third,
        // fourth and curr to fifth respectively
        for(let i = 5; i < n; i++)
        {
          curr = first + second +
                 third + fourth + fifth;
          first = second;
          second = third;
          third = fourth;
          fourth = fifth;
          fifth = curr;
        }
        document.write(curr + "</br>");
      }
    }

    let n = 10;
      printpenta(n); 

</script>
```

**Output:** 

```
16
```