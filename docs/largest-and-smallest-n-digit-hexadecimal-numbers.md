# 最大和最小 N 位十六进制数

> 原文:[https://www . geesforgeks . org/最大和最小 n 位十六进制数字/](https://www.geeksforgeeks.org/largest-and-smallest-n-digit-hexadecimal-numbers/)

给定一个整数 **N** ，任务是找到最小和最大的 **N 位**数字[六进制数字系统](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)。

**示例:**

> **输入:** N = 4
> **输出:**
> 最大:FFFF
> 最小:1000
> 
> **输入:**N = 2
> T3】输出:T5】最大:FF
> 最小:10

**方法:**可以按照以下步骤完成所需答案:

*   **最大数字:**要得到最大的数字，数字的每个数字都必须是最大的。六进制数字系统中的最大位数是“ **F** ”。因此:

```
1 Digit Largest Number: 'F'
2 Digit Largest Number: 'FF'
3 Digit Largest Number: 'FFF'
                .
                .
                .
N Digit Largest Number: 'FFF....(N) times'
```

*   **最小数:**十六进制数中最小的数是“ **0** ”。其思想是第一个数字需要尽可能小，而不是 0，0 是“1”，其余的数字需要是 **0** 。因此:

```
1 Digit Smallest Number: '1'
2 Digit Smallest Number: '10'
3 Digit Smallest Number: '100'
                .
                .
                .
N Digit Smallest Number: '100....(N - 1) times'
```

下面是上述方法的实现:

## C++

```
// C++ program to find the largest
// and smallest N-digit numbers
// in Hexa-Decimal Number System

#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// N-digit number in Hexa-Decimal
// Number System
string findLargest(int N)
{
    // Append 'F' N times
    string largest = string(N, 'F');

    return largest;
}

// Function to return the smallest
// N-digit number in Hexa-Decimal
// Number System
string findSmallest(int N)
{
    // Append '0' (N - 1) times to 1
    string smallest = "1" + string((N - 1), '0');

    return smallest;
}

// Function to print the largest and smallest
// N-digit Hexa-Decimal number
void print(int largest)
{
    cout << "Largest: " << findLargest(largest) << endl;
    cout << "Smallest: " << findSmallest(largest) << endl;
}

// Driver code
int main()
{

    int N = 4;
    print(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest
// and smallest N-digit numbers
// in Hexa-Decimal Number System
class GFG {

    // Function to return the largest
    // N-digit number in Hexa-Decimal
    // Number System
    static String findLargest(int N)
    {

        String largest = "";
        // Append 'F' N times
        for (int i = 0; i < N ; i++)
            largest += 'F';

        return largest;
    }

    // Function to return the smallest
    // N-digit number in Hexa-Decimal
    // Number System
    static String findSmallest(int N)
    {

        String smallest = "1" ;
        // Append '0' (N - 1) times to 1
        for(int i = 0; i < N - 1; i++)
            smallest += '0';

        return smallest;
    }

    // Function to print the largest and smallest
    // N-digit Hexa-Decimal number
    static void print(int largest)
    {
        System.out.println("Largest: " + findLargest(largest)) ;
        System.out.println("Smallest: " + findSmallest(largest)) ;
    }

    // Driver code
    public static void main (String[] args)
    {

        int N = 4;
        print(N);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the largest
# and smallest N-digit numbers
# in Hexa-Decimal Number System

# Function to return the largest
# N-digit number in Hexa-Decimal
# Number System
def findLargest(N) :

    # Append 'F' N times
    largest = 'F'*N

    return largest;

# Function to return the smallest
# N-digit number in Hexa-Decimal
# Number System
def findSmallest(N) :

    # Append '0' (N - 1) times to 1
    smallest = '1' + '0'*(N - 1)

    return smallest;

# Function to print the largest and smallest
# N-digit Hexa-Decimal number
def printAns(largest) :

    print("Largest: " , findLargest(largest));
    print("Smallest: " , findSmallest(largest));

# Driver code
if __name__ == "__main__" :

    N = 4;
    printAns(N);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the largest
// and smallest N-digit numbers
// in Hexa-Decimal Number System
using System;

class GFG {

    // Function to return the largest
    // N-digit number in Hexa-Decimal
    // Number System
    static string findLargest(int N)
    {

        string largest = "";

        // Append 'F' N times
        for (int i = 0; i < N ; i++)
            largest += 'F';

        return largest;
    }

    // Function to return the smallest
    // N-digit number in Hexa-Decimal
    // Number System
    static string findSmallest(int N)
    {

        string smallest = "1" ;

        // Append '0' (N - 1) times to 1
        for(int i = 0; i < N - 1; i++)
            smallest += '0';

        return smallest;
    }

    // Function to print the largest and smallest
    // N-digit Hexa-Decimal number
    static void print(int largest)
    {
        Console.WriteLine("Largest: " +
                    findLargest(largest)) ;
        Console.WriteLine("Smallest: " +
                    findSmallest(largest)) ;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int N = 4;
        print(N);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascipt implementation of the
// above approach

// Function to return the largest
// N-digit number in Hexa-Decimal
// Number System
function findLargest(N)
{
    // Append 'F' N times "a".repeat(10)
    var largest = "F".repeat(N);

    return largest;
}

// Function to return the smallest
// N-digit number in Hexa-Decimal
// Number System
function findSmallest(N)
{
    // Append '0' (N - 1) times to 1
    var smallest = "1" + "0".repeat(N-1);

    return smallest;
}

// Function to print the largest and smallest
// N-digit Hexa-Decimal number
function print(largest)
{
    document.write("Largest: " + findLargest(largest) + "<br>");
    document.write("Smallest: " + findSmallest(largest) + "<br>");
}

// Driver code
var N = 4;
print(N);

// This code is contributed by Shivanisingh
</script>
```

**Output:** 

```
Largest: FFFF
Smallest: 1000
```

**时间复杂度:** O(N)，其中 N 是字符串的长度。