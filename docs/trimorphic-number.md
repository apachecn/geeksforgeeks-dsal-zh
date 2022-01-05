# 三态数

> 原文:[https://www.geeksforgeeks.org/trimorphic-number/](https://www.geeksforgeeks.org/trimorphic-number/)

给定一个数 N，任务是检查这个数是否是三态数。当且仅当一个数的立方与数本身以相同的数字结束时，该数称为三态数。换句话说，数字出现在其立方体的末端。

**示例:**

```
Input : 5 
Output : trimorphic 
Explanation: 5*5*5=125

Input : 24 
Output : trimorphic 
Explanation: 24*24*24=13824 

Input:10 
Output: not trimorphic 
Explanation: 10*10*10=1000 
```

**进场:**

```
1\. Store the cube of given number.
2\. Loop until N becomes 0 as we have to match 
   all digits with its cube.
    i) Check if (n%10 == cube%10) i.e. last digit 
       of number = last digit of cube or not
        a) if not equal, return false.
    ii) Otherwise continue i.e. reduce number and 
        cube i.e. n = n/10 and cube = cube/10;
3- Return true if all digits matched.
```

下面是该方法的实现。

## C++

```
// C++ program to check if a
// number is Trimorphic
#include <iostream>
using namespace std;

// Function to check Trimorphic number
bool isTrimorphic(int N)
{
    // Store the cube
    int cube = N * N * N;

    // Start Comparing digits
    while (N > 0)
    {
        // Return false, if any digit
        // of N doesn't match with
        // its cube's digits from last
        if (N % 10 != cube % 10)
            return false;

        // Reduce N and cube
        N /= 10;
        cube /= 10;
    }

    return true;
}

// Driver code
int main()
{
    int N = 24;

    isTrimorphic(N) ? cout << "trimorphic" :
                      cout << "not trimporphic";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// number is Trimorphic

class GFG {

  // Function to check Trimorphic number
    static boolean isTrimorphic(int N)
    {
        // Store the cube
        int cube = N * N * N;

        // Start Comparing digits
        while (N > 0) {

         // Return false, if any digit
         // of N doesn't match with
         // its cube's digits from last
         if (N % 10 != cube % 10)
            return false;

            // Reduce N and cube
            N /= 10;
            cube /= 10;
        }

        return true;
    }

// Driver code
public static void main(String[] args)
    {
        int N = 24;

        if (isTrimorphic(N) == true)
        System.out.println("trimorphic");
        else
        System.out.println("not trimorphic");
    }
}

//This article is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python 3 program to check
# if a number is Trimorphic

# Function to check
# Trimorphic number
def isTrimorphic(N) :

    # Store the cube
    cube = N * N * N

    # Start Comparing digits
    while (N > 0) :

        # Return false, if any digit
        # of N doesn't match with
        # its cube's digits from last
        if (N % 10 != cube % 10) :
            return False

        # Reduce N and cube
        N = N // 10
        cube = cube // 10

    return True

# Driver code
N = 24
if(isTrimorphic(N)) :
    print("trimorphic")
else :
    print("not trimporphic")

# This code is contributed by Nikita tiwari.
```

## C#

```
// C# program to check if
// a number is Trimorphic
using System;

class GFG {

// Function to check Trimorphic number
    static bool isTrimorphic(int N)
    {
        // Store the cube
        int cube = N * N * N;

        // Start Comparing digits
        while (N > 0) {

        // Return false, if any digit
        // of N doesn't match with
        // its cube's digits from last
        if (N % 10 != cube % 10)
            return false;

            // Reduce N and cube
            N /= 10;
            cube /= 10;
        }

        return true;
    }

// Driver code
public static void Main()
    {
        int N = 24;

        if (isTrimorphic(N) == true)
        Console.Write("trimorphic");
        else
        Console.Write("not trimorphic");
    }
}

// This article is contributed
// by Smitha Dinesh Semwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to check if a
// number is Trimorphic

// Function to check Trimorphic
// number
function isTrimorphic($N)
{

    // Store the cube
    $cube = $N * $N * $N;

    // Start Comparing digits
    while ($N > 0)
    {

        // Return false, if any digit
        // of N doesn't match with
        // its cube's digits from last
        if ($N % 10 != $cube % 10)
            return -1;

        // Reduce N and cube
        $N /= 10;
        $cube /= 10;
    }

    return 1;
}

// Driver code
    $N = 24;

    $r = isTrimorphic($N) ? "trimorphic" :
                      "not trimporphic";
    echo $r;

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to check if
// a number is Trimorphic

// Function to check Trimorphic number
function isTrimorphic(N)
{

    // Store the cube
    let cube = N * N * N;

    // Start Comparing digits
    while (N > 0)
    {

        // Return false, if any digit
        // of N doesn't match with
        // its cube's digits from last
        if (N % 10 != cube % 10)
            return false;

        // Reduce N and cube
        N = parseInt(N / 10, 10);
        cube = parseInt(cube / 10, 10);
    }
    return true;
}

// Driver code
let N = 24;

if (isTrimorphic(N) == true)
    document.write("trimorphic");
else
    document.write("not trimorphic");

// This code is contributed by rameshtravel07

</script>
```

输出:

```
trimorphic
```

**查找第 n 个三态数**
**示例:**

```
Input  : 10 
Output : 51

Input  : 11
Output : 75
```

## C++

```
// CPP program to find nth
// Trimorphic number
#include <iostream>
using namespace std;

# define INT_MAX 2147483647
// Functions to find nth
// Trimorphic number
bool checkTrimorphic(int num)
{
    int cube = num * num * num;
    // Comparing the digits
    while(num > 0)
    {
        // Return false, if any digit
        // of num doesn't match with
        // its cube's digits from last
        if (num % 10 != cube % 10)
            return false;

        // Reduce num and cube
        num /= 10;
        cube /= 10;
    }
    return true;
}
int nthTrimorphic(int n)
{

    int count = 0;
    // Check in max int size
    for(int i = 0; i < INT_MAX; i++)
    {
        //check number is Trimorphic or not
        if(checkTrimorphic(i))
            count++;

        // if counter is equal to the
        // n then return nth number
        if(count == n)
            return i;
    }
}

// Driver code
int main()
{
    int n = 9;
    cout<< nthTrimorphic(n);
    return 0;
}

// This code is contributed by jaingyayak.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth
// Trimorphic number

class GFG
{
static int INT_MAX = 2147483647;

// Functions to find nth
// Trimorphic number
static boolean checkTrimorphic(int num)
{
    int cube = num * num * num;

    // Comparing the digits
    while(num > 0)
    {
        // Return false, if any
        // digit of num doesn't
        // match with its cube's
        // digits from last
        if (num % 10 != cube % 10)
            return false;

        // Reduce num and cube
        num /= 10;
        cube /= 10;
    }
    return true;
}

static int nthTrimorphic(int n)
{

    int count = 0;

    // Check in max int size
    for(int i = 0; i < INT_MAX; i++)
    {
        // check number is
        // Trimorphic or not
        if(checkTrimorphic(i))
            count++;

        // if counter is equal to
        // the n then return nth number
        if(count == n)
            return i;
    }
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int n = 9;
    System.out.println(nthTrimorphic(n));
}
}

// This code is contributed by mits.
```

## 蟒蛇 3

```
# Python3 program to find
# nth Trimorphic number
import sys
# Functions to find nth
# Trimorphic number
def checkTrimorphic(num):

    cube = num * num * num

    # Comparing the digits
    while(num > 0):
        # Return false, if any digit
        # of num doesn't match with
        # its cube's digits from last
        if (num % 10 != cube % 10):
            return False

        # Reduce num and cube
        num = int(num / 10)
        cube = int(cube / 10)
    return True

def nthTrimorphic(n):
    count = 0

    # Check in max int size
    for i in range(sys.maxsize):
        # check number is
        # Trimorphic or not
        if(checkTrimorphic(i)):
            count+=1

        # if counter is equal to
        # the n then return nth
        # number
        if(count == n):
            return i

# Driver code
if __name__=='__main__':
    n = 9
    print(nthTrimorphic(n))

# This code is contributed
# by mits.
```

## C#

```
// C# program to find nth
// Trimorphic number
using System;

class GFG
{
static int INT_MAX = 2147483647;

// Functions to find nth
// Trimorphic number
static bool checkTrimorphic(int num)
{
    int cube = num * num * num;

    // Comparing the digits
    while(num > 0)
    {
        // Return false, if any
        // digit of num doesn't
        // match with its cube's
        // digits from last
        if (num % 10 != cube % 10)
            return false;

        // Reduce num and cube
        num /= 10;
        cube /= 10;
    }
    return true;
}

static int nthTrimorphic(int n)
{

    int count = 0;

    // Check in max int size
    for(int i = 0; i < INT_MAX; i++)
    {
        // check number is
        // Trimorphic or not
        if(checkTrimorphic(i))
            count++;

        // if counter is equal to
        // the n then return nth number
        if(count == n)
            return i;
    }
    return -1;
}

// Driver code
static int Main()
{
    int n = 9;
    Console.Write(nthTrimorphic(n));
    return 0;
}
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// nth Trimorphic number

// Functions to find nth
// Trimorphic number
function checkTrimorphic($num)
{
    $cube = $num * $num * $num;

    // Comparing the digits
    while($num > 0)
    {
        // Return false, if any digit
        // of num doesn't match with
        // its cube's digits from last
        if ($num % 10 != $cube % 10)
            return false;

        // Reduce num and cube
        $num = (int)($num / 10);
        $cube = (int)($cube / 10);
    }
    return true;
}

function nthTrimorphic($n)
{
    $count = 0;

    // Check in max int size
    for($i = 0;
        $i < PHP_INT_MAX; $i++)
    {
        // check number is
        // Trimorphic or not
        if(checkTrimorphic($i))
            $count++;

        // if counter is equal to
        // the n then return nth
        // number
        if($count == $n)
            return $i;
    }
}

// Driver code
$n = 9;
echo nthTrimorphic($n);

// This code is contributed
// by mits.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let LET_MAX = 2147483647;

// Functions to find nth
// Trimorphic number
function checkTrimorphic(num)
{
    let cube = num * num * num;

    // Comparing the digits
    while(num > 0)
    {
        // Return false, if any
        // digit of num doesn't
        // match with its cube's
        // digits from last
        if (num % 10 != cube % 10)
            return false;

        // Reduce num and cube
        num = Math.floor(num / 10);
        cube = Math.floor(cube / 10);
    }
    return true;
}

function nthTrimorphic(n)
{

    let count = 0;

    // Check in max let size
    for(let i = 0; i < LET_MAX; i++)
    {
        // check number is
        // Trimorphic or not
        if(checkTrimorphic(i))
            count++;

        // if counter is equal to
        // the n then return nth number
        if(count == n)
            return i;
    }
    return -1;
}

// Driver Code

    let n = 9;
    document.write(nthTrimorphic(n));

</script>
```

**输出:**

```
49
```