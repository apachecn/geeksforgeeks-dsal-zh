# 交替质数直到 N

> 原文:[https://www.geeksforgeeks.org/alternate-primes-till-n/](https://www.geeksforgeeks.org/alternate-primes-till-n/)

我们必须打印**交替质数**直到**n .**
T5【例:

```
Input : N = 10
Output : 2 5 

Input : N = 15
Output : 2 5 11 
```

**天真方法:**我们只需简单地迭代 N 次，检查数字是否为质数，只需保留一个简单的修改标志变量，就可以打印出备用数字。

## C++

```
/* C++ program to print all
primes smaller than or
equal to n using Naive approach.*/
#include<bits/stdc++.h>
using namespace std;

/* Function for checking
number is prime or not */
int prime(int num)
{
    int i, flag = 0;
    for(i = 2; i<= num / 2; i++)
    {
        if(num % i == 0)
        {
            flag = 1;
            break;
        }
    }

    // if flag = 0 then number
    // is prime and return 1
    // otherwise return 0
    if(flag == 0)
        return 1;
    else
        return 0;
}

// Function for printing
// alternate prime number
void print_alternate_prime(int n)
{
    // counter is initialize with 0
    int counter = 0;

    // looping through 2 to n-1
    for(int num = 2; num < n; num++)
    {
        // function calling along
        // with if condition
        if (prime(num) == 1)
        {
            // if counter is multiple of 2
            // then only print prime number
            if (counter % 2 == 0)
                cout << num << " ";

            counter ++;
        }
    }
}

// Driver code
int main()
{
    int n = 15;
    cout << "Following are the alternate prime"
         << " number smaller than or equal to "
         << n << endl;

    // Function calling
    print_alternate_prime(n);
}

// This code is contributed
// by ChitraNayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// primes smaller than or
// equal to n using Naive approach.
class GFG
{

/* Function for checking
number is prime or not */
static int prime(int num)
{
int i, flag = 0;
for(i = 2; i<= num / 2; i++)
{
    if(num % i == 0)
    {
        flag = 1;
        break;
    }
}

// if flag = 0 then number is prime
// and return 1 otherwise return 0
if(flag == 0)
    return 1;
else
    return 0;
}

// Function for printing
// alternate prime number
static void print_alternate_prime(int n)
{
// counter is initialize with 0
int counter = 0;

// looping through 2 to n-1
for(int num = 2; num < n; num++)
{
    // function calling along
    // with if condition
    if (prime(num) == 1)
    {
        // if counter is multiple of 2
        // then only print prime number
        if (counter % 2 == 0)
            System.out.print(num + " ");

        counter ++;
    }
}
}

// Driver code
public static void main(String[] args)
{
    int n = 15;
    System.out.println("Following are the alternate " +
                         "prime number smaller than " +
                                   "or equal to " + n);

    // Function calling
    print_alternate_prime(n);
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to print all
# primes smaller than or
# equal to n using Naive approach.

# Function for checking number
# is prime or not
def prime(num) :
    flag = 0
    for i in range(2,num // 2 + 1) :
        if num % i == 0 :
            flag = 1
            break
    # if flag = 0 then number is prime
    # and return 1 otherwise return 0
    if flag == 0 :
        return 1
    else :
        return 0

# Function for printing alternate prime number
def print_alternate_prime(n):

    # counter is initialize with 0
    counter = 0

    # looping through 2 to n-1
    for num in range(2,n) :

        # function calling along with if condition
        if prime(num) == 1 :

            # if counter is multiple of 2 then
            # only print prime number
            if counter % 2 == 0 :
                print(num,end =" ")

            counter += 1

# Driver code
if __name__ == "__main__":
    n = 15
    print("Following are the alternate prime"
          +"number smaller than or equal to",n)

    # Function calling
    print_alternate_prime(n)

```

## C#

```
// C# program to print all
// primes smaller than or
// equal to n using Naive approach.
using System;
class GFG
{
/* Function for checking
number is prime or not */
static int prime(int num)
{
int i, flag = 0;
for(i = 2; i <= num / 2; i++)
{
    if(num % i == 0)
    {
        flag = 1;
        break;
    }
}

// if flag = 0 then number is prime
// and return 1 otherwise return 0
if(flag == 0)
    return 1;
else
    return 0;
}

// Function for printing
// alternate prime number
static void print_alternate_prime(int n)
{
// counter is initialize with 0
int counter = 0;

// looping through 2 to n-1
for(int num = 2; num < n; num++)
{
    // function calling along
    // with if condition
    if (prime(num) == 1)
    {
        // if counter is multiple of 2
        // then only print prime number
        if (counter % 2 == 0)
            Console.Write(num + " ");

        counter ++;
    }
}
}

// Driver code
public static void Main()
{
    int n = 15;
    Console.Write("Following are the alternate " +
                    "prime number smaller than " +
                       "or equal to " + n + "\n");

    // Function calling
    print_alternate_prime(n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all
// primes smaller than or
// equal to n using Naive approach.

// Function for checking number
// is prime or not
function prime($num)
{
    $flag = 0;
    for($i = 2; $i <= $num / 2; $i++)
    {
        if ($num % $i == 0)
        {
            $flag = 1;
            break;
        }
    }

    // if flag = 0 then number is prime
    // and return 1 otherwise return 0
    if ($flag == 0)
        return 1;
    else
        return 0;
}

// Function for printing
// alternate prime number
function print_alternate_prime($n)
{

    // counter is initialize with 0
    $counter = 0;

    // looping through 2 to n-1
    for($num = 2; $num < $n; $num++)
    {
        // function calling along
        // with if condition
        if(prime($num) == 1)
        {
            // if counter is multiple of 2
            // then only print prime number
            if ($counter % 2 == 0 )
                echo $num . " ";

            $counter += 1;
        }
    }
}

// Driver code
$n = 15;
echo "Following are the alternate prime ".
      "number smaller than or equal to " .
                                $n . "\n";
// Function calling
print_alternate_prime($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// javascript program to print all
// primes smaller than or
// equal to n using Naive approach.   
/*
     * Function for checking number is prime or not
     */
    function prime(num) {
        var i, flag = 0;
        for (i = 2; i <= num / 2; i++) {
            if (num % i == 0) {
                flag = 1;
                break;
            }
        }

        // if flag = 0 then number is prime
        // and return 1 otherwise return 0
        if (flag == 0)
            return 1;
        else
            return 0;
    }

    // Function for printing
    // alternate prime number
    function print_alternate_prime(n)
    {

        // counter is initialize with 0
        var counter = 0;

        // looping through 2 to n-1
        for (num = 2; num < n; num++)
        {

            // function calling along
            // with if condition
            if (prime(num) == 1)
            {

                // if counter is multiple of 2
                // then only print prime number
                if (counter % 2 == 0)
                    document.write(num + " ");

                counter++;
            }
        }
    }

    // Driver code
    var n = 15;
    document.write("Following are the alternate " + "prime number smaller than " + "or equal to " + n+"<br/>");

    // Function calling
    print_alternate_prime(n);

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
Following are the alternate prime numbers smaller  than or equal to 15
2 5 11
```