# 求自然数 N 的第 k 个最小除数

> 原文:[https://www . geeksforgeeks . org/find-the-kth-最小自然数除数-n/](https://www.geeksforgeeks.org/find-the-kth-smallest-divisor-of-a-natural-number-n/)

给你一个数字 **N** 和一个数字 **K** 。我们的任务是找到 **N** 的 **k <sup>th</sup>** 最小除数。
**示例:**

```
Input : N = 12, K = 5
Output : 6
The divisors of 12 after sorting are 1, 2, 3, 4, 6 and 12\. 
Where the value of 5th divisor is equal to 6.

Input : N = 16, K 2
Output : 2
```

**简单的方法:**简单的方法是运行一个从 1 到√N 的循环，找到 N 的所有因子，并把它们推合成一个向量。最后，对向量进行排序，并打印向量的第 K 个值。
**注意**:向量中的元素最初不会排序，因为我们同时推了因子(I)和(n/i)。这就是为什么需要在打印第 K 个因子之前对向量进行排序。
以下是上述方法的实施:

## C++

```
// C++ program to find K-th smallest factor

#include <bits/stdc++.h>
using namespace std;

// function to find the k'th divisor
void findkth(int n, int k)
{
    // initialize a vector v
    vector<long long> v;

    // store all the divisors
    // so the loop will needs to run till sqrt ( n )
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            v.push_back(i);
            if (i != sqrt(n))
                v.push_back(n / i);
        }
    }

    // sort the vector in an increasing order
    sort(v.begin(), v.end());

    // if k is greater than the size of vector
    // then no divisor can be possible
    if (k > v.size())
        cout << "Doesn't Exist";
    // else print the ( k - 1 )th value of vector
    else
        cout << v[k - 1];
}

// Driver code
int main()
{
    int n = 15, k = 2;

    findkth(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find K-th smallest factor
import java.util.*;

class GFG{

// function to find the k'th divisor
static void findkth(int n, int k)
{
    // initialize a vector v
    Vector<Integer> v = new Vector<Integer>();

    // store all the divisors
    // so the loop will needs to run till sqrt ( n )
    for (int i = 1; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {
            v.add(i);
            if (i != Math.sqrt(n))
                v.add(n / i);
        }
    }

    // sort the vector in an increasing order
    Collections.sort(v);

    // if k is greater than the size of vector
    // then no divisor can be possible
    if (k > v.size())
        System.out.print("Doesn't Exist");

    // else print the ( k - 1 )th value of vector
    else
        System.out.print(v.get(k - 1));
}

// Driver code
public static void main(String[] args)
{
    int n = 15, k = 2;

    findkth(n, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find K-th smallest factor
from math import sqrt

# function to find the k'th divisor
def findkth(n, k):

    # initialize a vector v
    v = []

    # store all the divisors so the loop
    # will needs to run till sqrt ( n )
    p = int(sqrt(n)) + 1
    for i in range(1, p, 1):
        if (n % i == 0):
            v.append(i)
            if (i != sqrt(n)):
                v.append(n / i);

    # sort the vector in an increasing order
    v.sort(reverse = False)

    # if k is greater than the size of vector
    # then no divisor can be possible
    if (k > len(v)):
        print("Doesn't Exist")

    # else print the (k - 1)th
    # value of vector
    else:
        print(v[k - 1])

# Driver code
if __name__ == '__main__':
    n = 15
    k = 2

    findkth(n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find K-th smallest factor
using System;
using System.Collections.Generic;

class GFG{

// function to find the k'th divisor
static void findkth(int n, int k)
{
    // initialize a vector v
    List<int> v = new List<int>();

    // store all the divisors
    // so the loop will needs to run till sqrt ( n )
    for (int i = 1; i <= Math.Sqrt(n); i++) {
        if (n % i == 0) {
            v.Add(i);
            if (i != Math.Sqrt(n))
                v.Add(n / i);
        }
    }

    // sort the vector in an increasing order
    v.Sort();

    // if k is greater than the size of vector
    // then no divisor can be possible
    if (k > v.Count)
        Console.Write("Doesn't Exist");

    // else print the ( k - 1 )th value of vector
    else
        Console.Write(v[k - 1]);
}

// Driver code
public static void Main(String[] args)
{
    int n = 15, k = 2;

    findkth(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
function findkth( n,  k)
{
    // initialize a vector v
    var v=[];

    // store all the divisors
    // so the loop will needs to run till sqrt ( n )
    for (var i = 1; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {
            v.push(i);
            if (i != Math.sqrt(n))
                v.push(n / i);
        }
    }

    // sort the vector in an increasing order
    v.sort(function fun(a,b){ return a-b });

    // if k is greater than the size of vector
    // then no divisor can be possible
    if (k > v.length)
        document.write("Doesn't Exist");
    // else print the ( k - 1 )th value of vector
    else
    document.write( v[k - 1]);
}

var n = 15, k = 2;

    findkth(n, k);

</script>
```

**Output**

```
3
```

**时间复杂度** : √N log( √N )
**高效方法**:高效方法是将因子存储在两个独立的向量中。也就是说，对于从 1 到√N 的所有 I，因子 I 将存储在单独的向量中，而 N/i 将存储在单独的向量中。
现在，如果仔细观察，可以看到第一个向量已经按递增顺序排序，第二个向量按递减顺序排序。所以，反转第二个向量，从它所在的向量中打印第 K 个元素。
以下是上述方法的实现:

## C++

```
// C++ program to find the K-th smallest factor

#include <bits/stdc++.h>
using namespace std;

// Function to find the k'th divisor
void findkth ( int n, int k)
{
    // initialize vectors v1 and v2
    vector <int> v1;
    vector <int> v2;

    // store all the divisors in the two vectors
    // accordingly
    for( int i = 1 ; i <= sqrt( n ); i++ )
    {
        if ( n % i == 0 )
        {
            v1.push_back ( i );

            if ( i != sqrt ( n ) )
                v2.push_back ( n / i );
        }
    }

    // reverse the vector v2 to sort it
    // in increasing order
    reverse(v2.begin(), v2.end());

    // if k is greater than the size of vectors
    // then no divisor can be possible
    if ( k > (v1.size() + v2.size()))
        cout << "Doesn't Exist" ;
    // else print the ( k - 1 )th value of vector
    else
    {
        // If K is lying in first vector
        if(k <= v1.size())
            cout<<v1[k-1];
        // If K is lying in second vector
        else
            cout<<v2[k-v1.size()-1];
    }
}

// Driver code
int main()
{
    int n = 15, k = 2;

    findkth ( n, k) ;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the K-th smallest factor
import java.util.*;

class GFG
{

// Function to find the k'th divisor
static void findkth ( int n, int k)
{
    // initialize vectors v1 and v2
    Vector<Integer> v1 = new Vector<Integer>();
    Vector <Integer> v2 = new Vector<Integer>();

    // store all the divisors in the two vectors
    // accordingly
    for( int i = 1 ; i <= Math.sqrt( n ); i++ )
    {
        if ( n % i == 0 )
        {
            v1.add ( i );

            if ( i != Math.sqrt ( n ) )
                v2.add ( n / i );
        }
    }

    // reverse the vector v2 to sort it
    // in increasing order
    Collections.reverse(v2);

    // if k is greater than the size of vectors
    // then no divisor can be possible
    if ( k > (v1.size() + v2.size()))
        System.out.print("Doesn't Exist");

    // else print the ( k - 1 )th value of vector
    else
    {
        // If K is lying in first vector
        if(k <= v1.size())
            System.out.print(v1.get(k - 1));

        // If K is lying in second vector
        else
            System.out.print(v2.get(k-v1.size() - 1));
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 15, k = 2;

    findkth ( n, k) ;
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the K-th
# smallest factor
import math as mt

# Function to find the k'th divisor
def findkth (n, k):

    # initialize vectors v1 and v2
    v1 = list()
    v2 = list()

    # store all the divisors in the
    # two vectors accordingly
    for i in range(1, mt.ceil(n**(.5))):

        if (n % i == 0):

            v1.append(i)

            if (i != mt.ceil(mt.sqrt(n))):
                v2.append(n // i)

    # reverse the vector v2 to sort it
    # in increasing order
    v2[::-1]

    # if k is greater than the size of vectors
    # then no divisor can be possible
    if ( k > (len(v1) + len(v2))):
        print("Doesn't Exist", end = "")

    # else print the ( k - 1 )th value of vector
    else:

        # If K is lying in first vector
        if(k <= len(v1)):
            print(v1[k - 1])

        # If K is lying in second vector
        else:
            print(v2[k - len(v1) - 1])

# Driver code
n = 15
k = 2
findkth (n, k)

# This code is contributed by Mohit kumar
```

## C#

```
// C# program to find
// the K-th smallest factor
using System;
using System.Collections.Generic;
class GFG{

// Function to find the k'th divisor
static void findkth (int n, int k)
{
  // initialize vectors v1 and v2
  List<int> v1 = new List<int>();
  List <int> v2 = new List<int>();

  // store all the divisors in the
  // two vectors accordingly
  for(int i = 1; i <= Math.Sqrt(n); i++)
  {
    if (n % i == 0)
    {
      v1.Add (i);

      if (i != Math.Sqrt (n))
        v2.Add (n / i);
    }
  }

  // reverse the vector v2 to sort it
  // in increasing order
  v2.Reverse();

  // if k is greater than the
  // size of vectors then no
  // divisor can be possible
  if (k > (v1.Count + v2.Count))
    Console.Write("Doesn't Exist");

  // else print the (k - 1)th
  // value of vector
  else
  {
    // If K is lying in first vector
    if(k <= v1.Count)
      Console.Write(v1[k - 1]);

    // If K is lying in second vector
    else
      Console.Write(v2[k - v1.Count - 1]);
  }
}

// Driver code
public static void Main(String[] args)
{
  int n = 15, k = 2;
  findkth (n, k);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to find the K-th smallest factor

 // Function to find the k'th divisor
function findkth ( n,k)
{
    // initialize vectors v1 and v2
    let v1 = [];
    let v2 = [];

    // store all the divisors in the two vectors
    // accordingly
    for( let i = 1 ; i <= Math.sqrt( n ); i++ )
    {
        if ( n % i == 0 )
        {
            v1.push ( i );

            if ( i != Math.sqrt ( n ) )
                v2.push ( n / i );
        }
    }

    // reverse the vector v2 to sort it
    // in increasing order
    v2.reverse();

    // if k is greater than the size of vectors
    // then no divisor can be possible
    if ( k > (v1.length + v2.length))
        document.write("Doesn't Exist");

    // else print the ( k - 1 )th value of vector
    else
    {
        // If K is lying in first vector
        if(k <= v1.length)
            document.write(v1[k - 1]);

        // If K is lying in second vector
        else
            document.write(v2[k-v1.length - 1]);
    }
}

// Driver code
let n = 15, k = 2;
findkth ( n, k) ;

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度** : √N