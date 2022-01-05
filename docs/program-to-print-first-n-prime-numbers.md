# 打印从 1 到 n 的质数的程序

> 原文:[https://www . geesforgeks . org/program-to-print-first-n-prime-numbers/](https://www.geeksforgeeks.org/program-to-print-first-n-prime-numbers/)

给定一个数字 N，任务是打印从 1 到 N 的质数
**示例:**

```
Input: N = 10
Output: 2, 3, 5, 7

Input: N = 5
Output: 2, 3, 5 
```

**算法:**

*   首先，以数字 N 为输入。
*   然后使用 for 循环将数字从 1 迭代到 N
*   然后检查每个数字是否是质数。如果是质数，就打印出来。

> **方法 1:** 现在，根据形式定义，一个数‘n’如果不能被 1 和 n 以外的任何数整除，就是素数，换句话说，一个数如果不能被 2 到 n-1 之间的任何数整除，就是素数。

下面是上述方法的实现:

## C++

```
// C++ program to display first N Prime numbers
#include <bits/stdc++.h>
using namespace std;

//function to check if a given number is prime
bool isPrime(int n){
      //since 0 and 1 is not prime return false.
      if(n==1||n==0) return false;

      //Run a loop from 2 to n-1
      for(int i=2; i<n; i++){
        // if the number is divisible by i, then n is not a prime number.
        if(n%i==0) return false;
      }
      //otherwise, n is prime number.
      return true;
}

// Driver code
int main()
{
    int N = 100;

    //check for every number from 1 to N
      for(int i=1; i<=N; i++){
          //check if current number is prime
          if(isPrime(i)) {
            cout << i << " ";
          }
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to display
// first N Prime numbers
class GFG
{
      //function to check if a given number is prime
     static boolean isPrime(int n){
          //since 0 and 1 is not prime return false.
          if(n==1||n==0)return false;

          //Run a loop from 2 to n-1
          for(int i=2; i<n; i++){
            // if the number is divisible by i, then n is not a prime number.
                if(n%i==0)return false;
          }
          //otherwise, n is prime number.
          return true;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 100;
        //check for every number from 1 to N
        for(int i=1; i<=N; i++){
            //check if current number is prime
            if(isPrime(i)) {
                System.out.print(i + " ");
            }
        }

    }
}
```

## 蟒蛇 3

```
# Python3 program to display first N Prime numbers

#function to check if a given number is prime
def isPrime(n):
  #since 0 and 1 is not prime return false.
  if(n==1 or n==0):
    return False

  #Run a loop from 2 to n-1
  for i in range(2,n):
    #if the number is divisible by i, then n is not a prime number.
    if(n%i==0):
      return False

  #otherwise, n is prime number.
  return True

# Driver code
N = 100;
#check for every number from 1 to N
for i in range(1,N+1):
  #check if current number is prime
  if(isPrime(i)):
    print(i,end=" ")
```

## C#

```
// C# program to display
// first N Prime numbers
using System;

class GFG
{

     //function to check if a given number is prime
     static bool isPrime(int n){
        //since 0 and 1 is not prime return false.
        if(n==1||n==0) return false;

        //Run a loop from 2 to n-1
        for(int i=2; i<n; i++) {
            // if the number is divisible by i, then n is not a prime number.
            if(n%i==0) return false;
        }
      //otherwise, n is prime number.
      return true;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int N = 100;
        //check for every number from 1 to N
        for(int i=1; i<=N; i++) {
          //check if current number is prime
            if(isPrime(i)) {
              Console.Write(i + " ");
            }
        }

    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to display first N Prime numbers

// function to check if a given number is prime
function isPrime( n)
{
      // since 0 and 1 is not prime return false.
      if(n == 1 || n == 0) return false;

      // Run a loop from 2 to n-1
      for(var i = 2; i < n; i++)
      {

        // if the number is divisible by i, then n is not a prime number.
        if(n % i == 0) return false;
      }
      // otherwise, n is prime number.
      return true;
}

// Driver code
var N = 100;

// check for every number from 1 to N
  for(var i = 1; i <= N; i++)
  {
      // check if current number is prime
      if(isPrime(i)) {
        console.log( i );
      }
}

// This code is contributed by ukasp.
</script>
```

**Output**

```
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97 
```

**时间复杂度:O(N^2)，空间复杂度:O(1)**

> **方法 2** :为了检查一个数是否是质数，我们真的需要遍历所有从 2 到 n-1 的数吗？我们已经知道，一个数“n”不能除以任何大于“n/2”的数。因此，根据这个逻辑，我们只需要迭代 2 到 n/2，因为大于 n/2 的数不能除以 n。

## C++

```
// C++ program to display first N Prime numbers
#include <bits/stdc++.h>
using namespace std;

//function to check if a given number is prime
bool isPrime(int n){
    //since 0 and 1 is not prime return false.
    if(n==1||n==0) return false;

    //Run a loop from 2 to n/2.
    for(int i=2; i<=n/2; i++) {
          // if the number is divisible by i, then n is not a prime number.
          if(n%i==0) return false;
    }
    //otherwise, n is prime number.
    return true;
}

// Driver code
int main()
{
    int N = 100;

    //check for every number from 1 to N
      for(int i=1; i<=N; i++){
        //check if current number is prime
        if(isPrime(i)) {
          cout << i << " ";
        }
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to display
// first N Prime numbers
class GFG
{
     //function to check if a given number is prime
     static boolean isPrime(int n){
          //since 0 and 1 is not prime return false.
          if(n==1||n==0) return false;

        //Run a loop from 2 to n-1
        for(int i=2; i<=n/2; i++){
            // if the number is divisible by i, then n is not a prime number.
            if(n%i==0)return false;
        }
        //otherwise, n is prime number.
        return true;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 100;
        //check for every number from 1 to N
        for(int i=1; i<=N; i++){
            //check if current number is prime
            if(isPrime(i)) {
              System.out.print(i + " ");
            }
        }

    }
}
```

## 蟒蛇 3

```
# Python3 program to display first N Prime numbers

#function to check if a given number is prime
def isPrime(n):
  #since 0 and 1 is not prime return false.
  if(n==1 or n==0):
    return False

  #Run a loop from 2 to n/2
  for i in range(2,(n//2)+1):
    #if the number is divisible by i, then n is not a prime number.
    if(n%i==0):
      return False

  #otherwise, n is prime number.
  return True

# Driver code
N = 100;
#check for every number from 1 to N
for i in range(1,N+1):
  #check if current number is prime
  if(isPrime(i)):
    print(i,end=" ")
```

## C#

```
// C# program to display
// first N Prime numbers
using System;

class GFG
{

 //function to check if a given number is prime
 static bool isPrime(int n){
      //since 0 and 1 is not prime return false.
     if(n==1||n==0)return false;

      //Run a loop from 2 to n/2.
      for(int i=2; i<=n/2; i++){
        // if the number is divisible by i, then n is not a prime number.
        if(n%i==0)return false;
      }
  //otherwise, n is prime number.
  return true;
}

// Driver code
public static void Main (String[] args)
{
    int N = 100;
    //check for every number from 1 to N
      for(int i=1; i<=N; i++){
      //check if current number is prime
      if(isPrime(i)) {
        Console.Write(i + " ");
      }
    }

}
}

// This code is contributed by Rajput-Ji
```

**Output**

```
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97 
```

**时间复杂度:O(N^2)，空间复杂度:O(1)**

> **方法 3:** 如果一个数‘n’没有被任何小于或等于 n 的平方根的数除，那么它就不会被任何其他大于 n 的平方根的数除。所以，我们只需要检查到 n 的平方根

## C++

```
// C++ program to display first N Prime numbers
#include <bits/stdc++.h>
using namespace std;

//function to check if a given number is prime
bool isPrime(int n){
  //since 0 and 1 is not prime return false.
  if(n==1||n==0)return false;

  //Run a loop from 2 to square root of n.
  for(int i=2; i*i<=n; i++){
    // if the number is divisible by i, then n is not a prime number.
    if(n%i==0)return false;
  }
  //otherwise, n is prime number.
  return true;
}

// Driver code
int main()
{
    int N = 100;

    //check for every number from 1 to N
      for(int i=1; i<=N; i++){
      //check if current number is prime
      if(isPrime(i)) {
        cout << i << " ";
      }
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to display
// first N Prime numbers
class GFG
{
  //function to check if a given number is prime
 static boolean isPrime(int n){
  //since 0 and 1 is not prime return false.
  if(n==1||n==0)return false;

  //Run a loop from 2 to square root of n
  for(int i=2; i*i<=n; i++){
    // if the number is divisible by i, then n is not a prime number.
    if(n%i==0)return false;
  }
  //otherwise, n is prime number.
  return true;
}

// Driver code
public static void main (String[] args)
{
    int N = 100;
        //check for every number from 1 to N
      for(int i=1; i<=N; i++){
      //check if current number is prime
      if(isPrime(i)) {
        System.out.print(i + " ");
      }
    }

}
}
```

## 蟒蛇 3

```
# Python3 program to display first N Prime numbers

#function to check if a given number is prime
def isPrime(n):
  #since 0 and 1 is not prime return false.
  if(n==1 or n==0):
    return False

  #Run a loop from 2 to square root of n.
  for i in range(2,int(n**(1/2))+1):
    #if the number is divisible by i, then n is not a prime number.
    if(n%i==0):
      return False

  #otherwise, n is prime number.
  return True

# Driver code
N = 100;
#check for every number from 1 to N
for i in range(1,N+1):
  #check if current number is prime
  if(isPrime(i)):
    print(i,end=" ")
```

## C#

```
// C# program to display
// first N Prime numbers
using System;

class GFG
{

 //function to check if a given number is prime
 static bool isPrime(int n){
      //since 0 and 1 is not prime return false.
     if(n==1||n==0)return false;

      //Run a loop from 2 to square root of n.
      for(int i=2; i*i<=n; i++){
        // if the number is divisible by i, then n is not a prime number.
        if(n%i==0)return false;
      }
  //otherwise, n is prime number.
  return true;
}

// Driver code
public static void Main (String[] args)
{
    int N = 100;
    //check for every number from 1 to N
      for(int i=1; i<=N; i++){
      //check if current number is prime
      if(isPrime(i)) {
        Console.Write(i + " ");
      }
    }

}
}

// This code is contributed by Rajput-Ji
```

**Output**

```
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97 
```

**时间复杂度:O(N^(3/2)，空间复杂度:O(1)**

可以进一步优化时间复杂度到 **O(n*log(log(n)))。**查[**筛厄拉多塞**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 。