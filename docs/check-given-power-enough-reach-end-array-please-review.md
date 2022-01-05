# 检查给定的数字 K 是否足够到达一个数组的末尾

> 原文:[https://www . geesforgeks . org/check-given-power-tower-end-array-请查看/](https://www.geeksforgeeks.org/check-given-power-enough-reach-end-array-please-review/)

给定一个由 n 个元素和 k 个数字组成的数组 arr[]。任务是通过执行以下操作来确定是否有可能到达数组的末尾:
遍历给定的数组，

*   如果发现任何元素不是质数，则将 K 的值减 1。
*   如果任何元素是质数，那么重新填充 K 的值到它的初始值。

如果有可能到达数组末尾(K > 0)，则打印是，否则打印否

**示例**:

```
Input : K = 2, arr[]={ 6, 3, 4, 5, 6};
Output : Yes
Explanation :
 1- arr[0] is not prime, so K = K-1 = 1
 2- arr[1] is prime so K will be refilled to its 
    initial value. Therefore,  K = 2.
 3- arr[2] is not prime.
    Therefore,  K = 2-1 = 1
 4- arr[3] is prime so K will be refilled to its 
    initial value. Therefore,  K = 2.
 5- arr[4] is not prime.
    Therefore,  K = 2-1 = 1
 6- Since the end of the array is reached with K>=0
    So output is YES

Input :  k=3, arr[]={ 1, 2, 10, 4, 6, 8};
Output : No
```

[推荐:请先在“<u>”上解，再进行解。</u>](https://practice.geeksforgeeks.org/problems/winter-is-coming/0)

<u>**简单方法**:</u>

*   <u>遍历数组的每个元素，检查当前元素的值是否为质数。</u>
*   <u>如果是质数，则再填充 K 的幂，否则递减 1。</u>
*   <u>如果有可能到达数组末尾(K > 0)，则打印“是”，否则打印“否”。</u>

<u>下面是上述方法的实现:</u>

## <u>C++</u>

```
// C++ program to check if it is possible
// to reach the end of the array
#include <iostream>
using namespace std;

// Function To check number is prime or not
bool is_Prime( int num )
{
    // because 1 is not prime
    if(num == 1)
    return false;

    for(int i=2 ; i*i <= num ; i++ )
    {
        if( num % i == 0 )
        return false;
    }

return true;
}

// Function to check whether it is possible
// to reach the end of the array or not    
bool isReachable( int arr[] , int n , int k)
{  
    // store initial value of K
    int x = k ;

    for(int i=0 ; i < n ; i++ )
    {
        // Call is_prime function to
        // check if a number is prime.
        if( is_Prime(arr[i]) )
        {
            // Refill K to initial value
            k = x;
        }                
        else
        {
            // Decrement k by 1
            k-- ;                
        }

        if( k <= 0 && i < (n-1) && (!is_Prime(arr[i+1])) )
            return false ;
    }

    return true ;
}

// Driver Code
int main()
{
    int arr[] = { 6, 3, 4, 5, 6};
    int n = sizeof(arr)/sizeof(arr[0]) ;
    int k = 2 ;

    isReachable( arr , n , k ) ? cout << "Yes" << endl :
                                    cout << "No" << endl ;

    return 0 ;
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to check if
// it is possible to reach
// the end of the array
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{

// Function To check
// number is prime or not
static boolean is_Prime(int num)
{
    // because 1 is not prime
    if(num == 1)
    return false;

    for(int i = 2 ;
            i * i <= num ; i++ )
    {
        if(num % i == 0)
        return false;
    }

return true;
}

// Function to check whether
// it is possible to reach
// the end of the array or not    
static boolean isReachable(int arr[] ,
                           int n , int k)
{
    // store initial value of K
    int x = k ;

    for(int i = 0 ; i < n ; i++ )
    {
        // Call is_prime function to
        // check if a number is prime.
        if(is_Prime(arr[i]))
        {
            // Refill K to
            // initial value
            k = x;
        }                
        else
        {
            // Decrement k by 1
            k-- ;                
        }

        if(k <= 0 && i < (n - 1) &&
          (is_Prime(arr[i + 1]) != true))
            return false ;
    }

    return true ;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = new int[]{ 6, 3, 4, 5, 6};
    int n = arr.length;
    int k = 2 ;

    if(isReachable(arr, n, k) == true)
        System.out.print("Yes" + "\n");
     else
        System.out.print("No" + "\n");
}
}
```

## <u>蟒蛇 3</u>

```
# Python 3 program to check if it is
# possible to reach the end of the array
from math import sqrt

# Function To check number is prime or not
def is_Prime(num):

    # because 1 is not prime
    if(num == 1):
        return False
    k = int(sqrt(num)) + 1

    for i in range(2, k, 1):
        if(num % i == 0):
            return False

    return True

# Function to check whether it is possible
# to reach the end of the array or not
def isReachable(arr, n , k):

    # store initial value of K
    x = k

    for i in range(0, n, 1):

        # Call is_prime function to
        # check if a number is prime.
        if( is_Prime(arr[i])):

            # Refill K to initial value
            k = x    
        else:

            # Decrement k by 1
            k -= 1       

        if(k <= 0 and i < (n - 1) and
          (is_Prime(arr[i + 1])) == False):
            return False

    return True

# Driver Code
if __name__ == '__main__':
    arr = [6, 3, 4, 5, 6]
    n = len(arr)
    k = 2

    if (isReachable( arr , n , k )):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Sahil_Shelangia
```

## <u>C#</u>

```
// C# program to check if
// it is possible to reach
// the end of the array
using System;

class GFG
{

// Function To check
// number is prime or not
static bool is_Prime(int num)
{
    // because 1 is not prime
    if(num == 1)
    return false;

    for(int i = 2 ;
            i * i <= num ; i++ )
    {
        if(num % i == 0)
        return false;
    }

return true;
}

// Function to check whether
// it is possible to reach
// the end of the array or not
static bool isReachable(int []arr ,
                        int n , int k)
{
    // store initial
    // value of K
    int x = k ;

    for(int i = 0 ; i < n ; i++ )
    {
        // Call is_prime function
        // to check if a number
        // is prime.
        if(is_Prime(arr[i]))
        {
            // Refill K to
            // initial value
            k = x;
        }            
        else
        {
            // Decrement k by 1
            k-- ;            
        }

        if(k <= 0 && i < (n - 1) &&
        (is_Prime(arr[i + 1]) != true))
            return false ;
    }

    return true ;
}

// Driver Code
public static void Main()
{
    int []arr = new int[]{ 6, 3, 4, 5, 6};
    int n = arr.Length;
    int k = 2 ;

    if(isReachable(arr, n, k) == true)
        Console.WriteLine("Yes" + "\n");
    else
        Console.WriteLine("No" + "\n");
}
}

// This code is contributed by vt_m
```

## <u>服务器端编程语言（Professional Hypertext Preprocessor 的缩写）</u>

```
<?php
// PHP program to check if it is possible
// to reach the end of the array

// Function To check number
// is prime or not
function is_Prime($num )
{
    // because 1 is not prime
    if($num == 1)
    return false;

    for($i = 2 ; ($i * $i) <= $num ; $i++ )
    {
        if($num % $i == 0)
        return false;
    }

    return true;
}

// Function to check whether it is possible
// to reach the end of the array or not
function isReachable($arr , $n , $k)
{
    // store initial value of K
    $x = $k ;

    for($i = 0 ; $i < $n ; $i++)
    {
        // Call is_prime function to
        // check if a number is prime.
        if(is_Prime($arr[$i]))
        {
            // Refill K to initial value
            $k = $x;
        }            
        else
        {
            // Decrement k by 1
            $k-- ;            
        }

        if($k <= 0 && $i < ($n - 1) &&
            (!is_Prime($arr[$i + 1])))
            return false ;
    }

    return true ;
}

// Driver Code
$arr = array(6, 3, 4, 5, 6);
$n = sizeof($arr);
$k = 2;

if(isReachable( $arr , $n , $k ))
    echo "Yes";
else
    echo "No" ;

// This code is contributed
// by Sach_Code
?>
```

## <u>java 描述语言</u>

```
<script>

// Javascript program to check if
// it is possible to reach
// the end of the array

// Function To check
// number is prime or not
function is_Prime(num)
{

    // Because 1 is not prime
    if(num == 1)
        return false;

    for(let i = 2; i * i <= num; i++)
    {
        if(num % i == 0)
            return false;
    }
    return true;
}

// Function to check whether
// it is possible to reach
// the end of the array or not
function isReachable(arr, n, k)
{

    // Store initial
    // value of K
    let x = k ;

    for(let i = 0 ; i < n ; i++ )
    {

        // Call is_prime function
        // to check if a number
        // is prime.
        if (is_Prime(arr[i]))
        {

            // Refill K to
            // initial value
            k = x;
        }           
        else
        {

            // Decrement k by 1
            k-- ;           
        }

        if (k <= 0 && i < (n - 1) &&
           (is_Prime(arr[i + 1]) != true))
            return false;
    }
    return true;
}

// Driver code
let arr = [ 6, 3, 4, 5, 6 ];
let n = arr.length;
let k = 2 ;

if (isReachable(arr, n, k) == true)
    document.write("Yes" + "</br>");
else
    document.write("No" + "</br>");

// This code is contributed by decode2207

</script>
```

<u>**Output:** 

```
Yes
```</u> 

<u>**时间复杂度:** O(N(sqrt N))</u>

<u>**有效方法:**上述方法可以通过使用厄拉多塞的[筛来检查一个数是否是素数来优化。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)</u>

<u>下面是高效方法的实现:</u>

## <u>C++</u>

```
// C++ program to check if it is possible
// to reach the end of the array
#include <iostream>
#define MAX 1000000
using namespace std;

// Function for Sieve of Eratosthenes
void SieveOfEratosthenes( int sieve[], int max )
{  
    for(int i=0; i<max; i++)
        sieve[i] = 1;

    for(int i=2 ; i*i <= max ; i++ )
    {
        if( sieve[i] == 1 )
        {
            for( int j=i*2 ; j <= max ; j+=i )
                sieve[ j ] = 0;
        }
    }
}

// Function to check if it is possible to
// reach end of the array    
bool isReachable( int arr[] , int n , int sieve[] , int k)
{  
    // store initial value of K
    int x = k;

    for(int i=0 ; i < n ; i++ )
    {  
        if( sieve[arr[i]] )
        {  
            // Refill K to initial value
            k = x;
        }                
         else
        {
            // Decrement k by 1
            k -= 1;                
        }

        if((k <= 0) && (i < (n-1)) &&
                        (sieve[arr[i+1]] == 0))
        {
            return false ;  
        }              
    }

    return true ;
}

// Driver Code
int main()
{
    int arr[] = {6, 3, 4, 5, 6};

    int sieve[MAX];

    int n = sizeof(arr)/sizeof(arr[0]) ;

    int k = 2;

    SieveOfEratosthenes(sieve, MAX) ;

    isReachable( arr , n , sieve , k ) ? cout << "Yes" << endl :
                                            cout << "No" << endl ;

    return 0 ;
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to check if it is possible
// to reach the end of the array
class GFG
{

    static int MAX = 1000000;

    // Function for Sieve of Eratosthenes
    static void SieveOfEratosthenes(int sieve[], int max)
    {
        for (int i = 0; i < max; i++)
        {
            sieve[i] = 1;
        }

        for (int i = 2; i * i < max; i++)
        {
            if (sieve[i] == 1)
            {
                for (int j = i * 2; j < max; j += i)
                {
                    sieve[j] = 0;
                }
            }
        }
    }

    // Function to check if it is possible to
    // reach end of the array    
    static boolean isReachable(int arr[], int n,
                                int sieve[], int k)
    {
        // store initial value of K
        int x = k;

        for (int i = 0; i < n; i++)
        {
            if (sieve[arr[i]] == 1)
            {
                // Refill K to initial value
                k = x;
            }
            else
            {
                // Decrement k by 1
                k -= 1;
            }

            if ((k <= 0) && (i < (n - 1))
                    && (sieve[arr[i + 1]] == 0))
            {
                return false;
            }
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {6, 3, 4, 5, 6};
        int[] sieve = new int[MAX];
        int n = arr.length;
        int k = 2;

        SieveOfEratosthenes(sieve, MAX);

        if (isReachable(arr, n, sieve, k))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## <u>蟒蛇 3</u>

```
# Python3 program to check if it is
# possible to reach the end of the
# array
import math

# Function for Sieve of Eratosthenes
def SieveOfEratosthenes(sieve, max):

    for i in range(0, max):
        sieve[i] = 1

    sqt = int(math.sqrt(max))

    for i in range(2, sqt):
        if (sieve[i] == 1):
            for j in range(i * 2, max, i):
                sieve[j] = 0

# Function to check if it is possible to
# reach end of the array    
def isReachable(arr, n, sieve, k):

    # store initial value of K
    x = k
    for i in range(0, n):
        if (sieve[arr[i]] != 0):

            # Refill K to initial value
            k = x       
        else:

            # Decrement k by 1
            k -= 1
        if ((k <= 0) and (i < (n - 1)) and
           (sieve[arr[i + 1]] == 0)):
            return 0

    return 1

# Driver Code
arr = [ 6, 3, 4, 5, 6 ]
sieve = [0 for x in range(1000000)]

n = len(arr)
k = 2

SieveOfEratosthenes(sieve, 1000000)

ch = isReachable(arr, n, sieve, k)

if (ch):
    print("Yes")
else:
    print("No")

# This code is contributed by Stream_Cipher
```

## <u>C#</u>

```
// C# program to check if it is possible
// to reach the end of the array
using System;

class GFG
{
    static int MAX = 1000000;

    // Function for Sieve of Eratosthenes
    static void SieveOfEratosthenes(int []sieve, int max)
    {
        for (int i = 0; i < max; i++)
        {
            sieve[i] = 1;
        }

        for (int i = 2; i * i < max; i++)
        {
            if (sieve[i] == 1)
            {
                for (int j = i * 2; j < max; j += i)
                {
                    sieve[j] = 0;
                }
            }
        }
    }

    // Function to check if it is possible to
    // reach end of the array
    static bool isReachable(int []arr, int n,
                                int []sieve, int k)
    {
        // store initial value of K
        int x = k;

        for (int i = 0; i < n; i++)
        {
            if (sieve[arr[i]] == 1)
            {
                // Refill K to initial value
                k = x;
            }
            else
            {
                // Decrement k by 1
                k -= 1;
            }

            if ((k <= 0) && (i < (n - 1))
                    && (sieve[arr[i + 1]] == 0))
            {
                return false;
            }
        }

        return true;
    }

    // Driver Code
    static public void Main ()
    {
        int []arr = {6, 3, 4, 5, 6};
        int[] sieve = new int[MAX];
        int n = arr.Length;
        int k = 2;

        SieveOfEratosthenes(sieve, MAX);

        if (isReachable(arr, n, sieve, k))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

/* This code contributed by ajit. */
```

## <u>java 描述语言</u>

```
<script>
    // Javascript program to check if it is possible
    // to reach the end of the array

    let MAX = 1000000;

    // Function for Sieve of Eratosthenes
    function SieveOfEratosthenes(sieve, max)
    {
        for (let i = 0; i < max; i++)
        {
            sieve[i] = 1;
        }

        for (let i = 2; i * i < max; i++)
        {
            if (sieve[i] == 1)
            {
                for (let j = i * 2; j < max; j += i)
                {
                    sieve[j] = 0;
                }
            }
        }
    }

    // Function to check if it is possible to
    // reach end of the array
    function isReachable(arr, n, sieve, k)
    {
        // store initial value of K
        let x = k;

        for (let i = 0; i < n; i++)
        {
            if (sieve[arr[i]] == 1)
            {
                // Refill K to initial value
                k = x;
            }
            else
            {
                // Decrement k by 1
                k -= 1;
            }

            if ((k <= 0) && (i < (n - 1)) && (sieve[arr[i + 1]] == 0))
            {
                return false;
            }
        }

        return true;
    }

    let arr = [6, 3, 4, 5, 6];
    let sieve = new Array(MAX);
    let n = arr.length;
    let k = 2;

    SieveOfEratosthenes(sieve, MAX);

    if (isReachable(arr, n, sieve, k))
    {
      document.write("Yes");
    }
    else
    {
      document.write("No");
    }

</script>
```

<u>**Output:** 

```
Yes
```</u> 

<u>**时间复杂度:** O(？Max * log log log(Max))+O(n)</u>