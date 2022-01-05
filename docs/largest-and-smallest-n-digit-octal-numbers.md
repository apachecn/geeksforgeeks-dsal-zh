# 最大和最小的 N 位八进制数

> 原文:[https://www . geesforgeks . org/最大和最小 n 位八进制数/](https://www.geeksforgeeks.org/largest-and-smallest-n-digit-octal-numbers/)

给定一个整数 **N** ，任务是在[八进制数字系统](https://www.geeksforgeeks.org/program-decimal-octal-conversion/)中找到最小和最大的 **N 位**数字。

**示例:**

> **输入:** N = 4
> **输出:**
> 最大:7777
> 最小:1000
> 
> **输入:** N = 2
> **输出:**
> 最大:77
> 最小:10

**方法:**可以按照以下步骤计算所需答案:

*   **最大数字:**要得到最大的数字，数字的每个数字都必须是最大的。八进制数字系统中的最大位数是“ **7** ”。因此:

```
1 Digit Largest Number: '7'
2 Digit Largest Number: '77'
3 Digit Largest Number: '777'
                .
                .
                .
N Digit Largest Number: '777....(N) times'
```

*   **最小数:**八进制数中最小的数是“ **0** ”。其思想是第一个数字需要尽可能小，而不是 0，0 是“1”，其余的数字需要是 **0** 。因此:

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
// in Octal Number System

#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// N-digit number in Octal
// Number System
string findLargest(int N)
{
    // Append '7' N times
    string largest = string(N, '7');

    return largest;
}

// Function to return the smallest
// N-digit number in Octal
// Number System
string findSmallest(int N)
{
    // Append '0' (N - 1) times to 1
    string smallest
        = "1"
          + string((N - 1), '0');

    return smallest;
}

// Function to print the largest and
// smallest N-digit Octal number
void printLargestSmallest(int N)
{
    cout << "Largest: "
         << findLargest(N) << endl;
    cout << "Smallest: "
         << findSmallest(N) << endl;
}

// Driver code
int main()
{
    int N = 4;

    // Function Call
    printLargestSmallest(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest
// and smallest N-digit numbers
// in Octal Number System
class GFG
{

// Function to return the largest
// N-digit number in Octal
// Number System
static String findLargest(int N)
{
    // Append '7' N times
    String largest = strings(N, '7');

    return largest;
}

// Function to return the smallest
// N-digit number in Octal
// Number System
static String findSmallest(int N)
{
    // Append '0' (N - 1) times to 1
    String smallest
        = "1"
          + strings((N - 1), '0');

    return smallest;
}

private static String strings(int N, char c) {
    String temp ="";
    for(int i= 0; i < N; i++) {
        temp+=c;
    }
    return temp;
}

// Function to print the largest and
// smallest N-digit Octal number
static void printLargestSmallest(int N)
{
    System.out.print("Largest: "
         + findLargest(N) +"\n");
    System.out.print("Smallest: "
         + findSmallest(N) +"\n");
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    // Function Call
    printLargestSmallest(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find the largest
# and smallest N-digit numbers
# in Octal Number System

# Function to return the largest
# N-digit number in Octal
# Number System
def findLargest(N):

    # Append '7' N times
    largest = strings(N, '7');
    return largest;

# Function to return the smallest
# N-digit number in Octal
# Number System
def findSmallest(N):

    # Append '0' (N - 1) times to 1
    smallest = "1" + strings((N - 1), '0');
    return smallest;

def strings(N, c):
    temp = "";
    for i in range(N):
        temp += c;
    return temp;

# Function to print the largest and
# smallest N-digit Octal number
def printLargestSmallest(N):
    print("Largest: ",findLargest(N));
    print("Smallest: ",findSmallest(N));

# Driver code
if __name__ == '__main__':
    N = 4;

    # Function Call
    printLargestSmallest(N);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program to find the largest
// and smallest N-digit numbers
// in Octal Number System
using System;

class GFG
{

// Function to return the largest
// N-digit number in Octal
// Number System
static String findLargest(int N)
{
    // Append '7' N times
    String largest = strings(N, '7');

    return largest;
}

// Function to return the smallest
// N-digit number in Octal
// Number System
static String findSmallest(int N)
{
    // Append '0' (N - 1) times to 1
    String smallest
        = "1"
          + strings((N - 1), '0');

    return smallest;
}

private static String strings(int N, char c) {
    String temp ="";
    for(int i= 0; i < N; i++) {
        temp+=c;
    }
    return temp;
}

// Function to print the largest and
// smallest N-digit Octal number
static void printLargestSmallest(int N)
{
    Console.Write("Largest: "
         + findLargest(N) +"\n");
    Console.Write("Smallest: "
         + findSmallest(N) +"\n");
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;

    // Function Call
    printLargestSmallest(N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the largest
// and smallest N-digit numbers
// in Octal Number System

// Function to return the largest
// N-digit number in Octal
// Number System
function findLargest(N)
{
    // Append '7' N times
    var largest = new Array(N+1).join( '7' );
    return largest;
}

// Function to return the smallest
// N-digit number in Octal
// Number System
function findSmallest(N)
{
    // Append '0' (N - 1) times to 1
    var smallest
        = "1"
          + new Array(N).join( '0' );

    return smallest;
}

// Function to print the largest and
// smallest N-digit Octal number
function printLargestSmallest(N)
{
    document.write("Largest: "
         + findLargest(N) + "<br>");

    document.write( "Smallest: "
         + findSmallest(N));
}

// Driver code
var N = 4;
// Function Call
printLargestSmallest(N);

</script>
```

**Output:** 

```
Largest: 7777
Smallest: 1000
```

**时间复杂度:** **O(N)** 其中 N 是字符串的长度。

**辅助空间:** O(1)