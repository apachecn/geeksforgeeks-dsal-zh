# 按照字典顺序将数字打印为“A”和“B”的字符串

> 原文:[https://www . geesforgeks . org/print-a-number-as-string-of-a-和-b-in-in-dictionary-order/](https://www.geeksforgeeks.org/print-a-number-as-string-of-a-and-b-in-lexicographic-order/)

给定一个数字 N，任务是打印对应于该数字的字符串“A”和“B”。
如果我们将所有数字表示为一串‘A’和‘B’，如下所示，

```
1 = A
2 = B
3 = AA
4 = AB
5 = BA
6 = BB
7 = AAA
8 = AAB
9 = ABA
10 = ABB
.....
.....
1000000 = BBBABAAAABAABAAAAAB
```

**例:**

```
Input: N = 30
Output: BBBB

Input: N = 55
Output: BBAAA

Input: N = 100
Output: BAABAB
```

**进场:**

1.  这个表示和二进制表示有一点关系。
2.  首先，我们必须找到打印对应于给定数字的字符串所需的字符数，也就是结果字符串的长度。
3.  有 2 个长度为 1 的数字，4 个长度为 2 的数字，8 个长度为 3 的数字等等…
4.  因此‘A’和‘B’k 长度串可以表示从(幂(2，k)-2)+1 到幂(2，k+1)-2 的幂(2，k+1)数，即 AA…A (k 次)到 BB…B (k 次)。
5.  所以打印对应的字符串，首先计算字符串的长度，让它为 k，现在计算，

    ```
    N = M - (pow(2, k)-2);
    ```

6.  现在运行下面的循环来打印相应的字符串。

    ```
    while (k>0)
    {
        num = pow(2, k-1);

        if (num >= N)
            cout <<"A";
        else{
            cout <<"B";
            N -= num;
        }
        k--;
    }
    ```

以下是上述方法的实现:

## C++

```
// C++ program to implement the above approach

#include <cmath>
#include <iostream>
using namespace std;

// Function to calculate number of characters
// in corresponding string of 'A' and 'B'
int no_of_characters(int M)
{

    // Since the minimum number
    // of characters will be 1
    int k = 1;

    // Calculating number of characters
    while (true) {

        // Since k length string can
        // represent at most pow(2, k+1)-2
        // that is if k = 4, it can
        // represent at most pow(2, 4+1)-2 = 30
        // so we have to calculate the
        // length of the corresponding string
        if (pow(2, k + 1) - 2 < M)
            k++;
        else
            break;
    }

    // return the length of
    // the corresponding string
    return k;
}

// Function to print corresponding
// string of 'A' and 'B'
void print_string(int M)
{
    int k, num, N;

    // Find length of string
    k = no_of_characters(M);

    // Since the first number that can be represented
    // by k length string will be (pow(2, k)-2)+1
    // and it will be AAA...A, k times,
    // therefore, N will store that
    // how much we have to print
    N = M - (pow(2, k) - 2);

    // At a particular time,
    // we have to decide whether
    // we have to print 'A' or 'B',
    // this can be check by calculating
    // the value of pow(2, k-1)
    while (k > 0) {
        num = pow(2, k - 1);

        if (num >= N)
            cout << "A";
        else {
            cout << "B";
            N -= num;
        }
        k--;
    }

    // Print new line
    cout << endl;
}

// Driver code
int main()
{

    int M;

    M = 30;
    print_string(M);

    M = 55;
    print_string(M);

    M = 100;
    print_string(M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach 
import java.util.*;

class GFG
{

// Function to calculate number of characters 
// in corresponding string of 'A' and 'B' 
static int no_of_characters(int M) 
{ 

    // Since the minimum number 
    // of characters will be 1 
    int k = 1; 

    // Calculating number of characters 
    while (true)
    { 

        // Since k length string can 
        // represent at most pow(2, k+1)-2 
        // that is if k = 4, it can 
        // represent at most pow(2, 4+1)-2 = 30 
        // so we have to calculate the 
        // length of the corresponding string 
        if ((int)Math.pow(2, k + 1) - 2 < M) 
            k++; 
        else
            break; 
    } 

    // return the length of 
    // the corresponding string 
    return k; 
} 

// Function to print corresponding 
// string of 'A' and 'B' 
static void print_string(int M) 
{ 
    int k, num, N; 

    // Find length of string 
    k = no_of_characters(M); 

    // Since the first number that can be represented 
    // by k length string will be (pow(2, k)-2)+1 
    // and it will be AAA...A, k times, 
    // therefore, N will store that 
    // how much we have to print 
    N = M - ((int)Math.pow(2, k) - 2); 

    // At a particular time, 
    // we have to decide whether 
    // we have to print 'A' or 'B', 
    // this can be check by calculating 
    // the value of pow(2, k-1) 
    while (k > 0) 
    { 
        num = (int)Math.pow(2, k - 1); 

        if (num >= N) 
            System.out.print("A"); 
        else 
        { 
            System.out.print( "B"); 
            N -= num; 
        } 
        k--; 
    } 

    // Print new line 
    System.out.println(); 
} 

// Driver code 
public static void main(String args[])
{ 

    int M; 

    M = 30; 
    print_string(M); 

    M = 55; 
    print_string(M); 

    M = 100; 
    print_string(M); 

} 
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
from math import pow

# Function to calculate number of characters
# in corresponding string of 'A' and 'B'
def no_of_characters(M):

    # Since the minimum number
    # of characters will be 1
    k = 1

    # Calculating number of characters
    while (True):

        # Since k length string can
        # represent at most pow(2, k+1)-2
        # that is if k = 4, it can
        # represent at most pow(2, 4+1)-2 = 30
        # so we have to calculate the
        # length of the corresponding string
        if (pow(2, k + 1) - 2 < M):
            k += 1
        else:
            break

    # return the length of
    # the corresponding string
    return k

# Function to print corresponding
# string of 'A' and 'B'
def print_string(M):

    # Find length of string
    k = no_of_characters(M)

    # Since the first number that can be 
    # represented by k length string will 
    # be (pow(2, k)-2)+1 and it will be 
    # AAA...A, k times, therefore, N will 
    # store that how much we have to print
    N = M - (pow(2, k) - 2)

    # At a particular time,
    # we have to decide whether
    # we have to print 'A' or 'B',
    # this can be check by calculating
    # the value of pow(2, k - 1)
    while (k > 0):
        num = pow(2, k - 1)

        if (num >= N):
            print("A", end = "")
        else:
            print("B", end = "")
            N -= num
        k -= 1

    print("\n", end = "")

# Driver code
if __name__ == '__main__':
    M = 30;
    print_string(M)

    M = 55
    print_string(M)

    M = 100
    print_string(M)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach 
using System;

class GFG 
{ 

    // Function to calculate number of characters 
    // in corresponding string of 'A' and 'B' 
    static int no_of_characters(int M) 
    { 

        // Since the minimum number 
        // of characters will be 1 
        int k = 1; 

        // Calculating number of characters 
        while (true) 
        { 

            // Since k length string can 
            // represent at most pow(2, k+1)-2 
            // that is if k = 4, it can 
            // represent at most pow(2, 4+1)-2 = 30 
            // so we have to calculate the 
            // length of the corresponding string 
            if ((int)Math.Pow(2, k + 1) - 2 < M) 
                k++; 
            else
                break; 
        } 

        // return the length of 
        // the corresponding string 
        return k; 
    } 

    // Function to print corresponding 
    // string of 'A' and 'B' 
    static void print_string(int M) 
    { 
        int k, num, N; 

        // Find length of string 
        k = no_of_characters(M); 

        // Since the first number that can be represented 
        // by k length string will be (pow(2, k)-2)+1 
        // and it will be AAA...A, k times, 
        // therefore, N will store that 
        // how much we have to print 
        N = M - ((int)Math.Pow(2, k) - 2); 

        // At a particular time, 
        // we have to decide whether 
        // we have to print 'A' or 'B', 
        // this can be check by calculating 
        // the value of pow(2, k-1) 
        while (k > 0) 
        { 
            num = (int)Math.Pow(2, k - 1); 

            if (num >= N) 
                Console.Write("A"); 
            else
            { 
                Console.Write( "B"); 
                N -= num; 
            } 
            k--; 
        } 

        // Print new line 
        Console.WriteLine(); 
    } 

    // Driver code 
    public static void Main() 
    { 

        int M; 

        M = 30; 
        print_string(M); 

        M = 55; 
        print_string(M); 

        M = 100; 
        print_string(M); 

    } 
} 

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement 
// the above approach

// Function to calculate number of characters
// in corresponding string of 'A' and 'B'
function no_of_characters($M)
{

    // Since the minimum number
    // of characters will be 1
    $k = 1;

    // Calculating number of characters
    while (true)
    {

        // Since k length string can
        // represent at most pow(2, k+1)-2
        // that is if k = 4, it can
        // represent at most pow(2, 4+1)-2 = 30
        // so we have to calculate the
        // length of the corresponding string
        if (pow(2, $k + 1) - 2 < $M)
            $k++;
        else
            break;
    }

    // return the length of
    // the corresponding string
    return $k;
}

// Function to print corresponding
// string of 'A' and 'B'
function print_string($M)
{
    $k; $num; $N;

    // Find length of string
    $k = no_of_characters($M);

    // Since the first number that can be represented
    // by k length string will be (pow(2, k)-2)+1
    // and it will be AAA...A, k times,
    // therefore, N will store that
    // how much we have to print
    $N = $M - (pow(2, $k) - 2);

    // At a particular time,
    // we have to decide whether
    // we have to print 'A' or 'B',
    // this can be check by calculating
    // the value of pow(2, k-1)
    while ($k > 0) 
    {
        $num = pow(2, $k - 1);

        if ($num >= $N)
            echo "A";
        else {
            echo "B";
            $N -= $num;
        }
        $k--;
    }

    // Print new line
    echo "\n";
}

// Driver code
$M;

$M = 30;
print_string($M);

$M = 55;
print_string($M);

$M = 100;
print_string($M);

// This code is contributed 
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to calculate number of characters
// in corresponding string of 'A' and 'B'
function no_of_characters( M){
    // Since the minimum number
    // of characters will be 1
    let k = 1;

    // Calculating number of characters
    while (true) {

        // Since k length string can
        // represent at most pow(2, k+1)-2
        // that is if k = 4, it can
        // represent at most pow(2, 4+1)-2 = 30
        // so we have to calculate the
        // length of the corresponding string
        if (Math.pow(2, k + 1) - 2 < M)
            k++;
        else
            break;
    }

    // return the length of
    // the corresponding string
    return k;
}

// Function to print corresponding
// string of 'A' and 'B'
function print_string( M)
{
    let k, num, N;

    // Find length of string
    k = no_of_characters(M);

    // Since the first number that can be represented
    // by k length string will be (pow(2, k)-2)+1
    // and it will be AAA...A, k times,
    // therefore, N will store that
    // how much we have to print
    N = M - (Math.pow(2, k) - 2);

    // At a particular time,
    // we have to decide whether
    // we have to print 'A' or 'B',
    // this can be check by calculating
    // the value of pow(2, k-1)
    while (k > 0) {
        num = Math.pow(2, k - 1);

        if (num >= N)
            document.write( "A");
        else {
            document.write( "B");
            N -= num;
        }
        k--;
    }

    // Print new line
    document.write("<br>");
}

// Driver code

    let M;

    M = 30;
    print_string(M);

    M = 55;
    print_string(M);

    M = 100;
    print_string(M);

</script>
```

**Output:** 

```
BBBB
BBAAA
BAABAB
```