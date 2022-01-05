# 不能被完美平方整除的数的最大除数

> 原文:[https://www . geesforgeks . org/一个不能被完美平方整除的数的最大除数/](https://www.geeksforgeeks.org/largest-divisor-of-a-number-not-divisible-by-a-perfect-square/)

给定一个正整数， **N** 。求给定数中不能被大于 1 的完美平方整除的最大除数。

**示例:**

```
Input : 12
Output : 6
Explanation : Divisors of 12 are 1, 2, 3, 4, 6 and 12\. 
Since 12 is divisible by 4 (a perfect square), 
it can't be required divisor. 6 is not divisible 
by any perfect square.

Input :97
Output :97
```

一个**简单的方法**是通过迭代到 N 的平方根找到给定数 **N** 的所有除数，并在列表中保持它们的排序顺序(降序)。这里，我们按照降序将它们插入到[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，以保持它们的排序。此外，通过从 1 到 10 <sup>5</sup> 的迭代，列出最多 10 个 <sup>10</sup> 的所有完美方块。
现在，对于从最大的除数开始的每个除数，检查它是否能被列表中的任何完美平方整除。如果一个除数不能被任何完全数整除，只需将它作为答案返回即可。

下面是上述方法的实现。

## C++

```
// C++ Program to find the largest
// divisor not divisible by any
// perfect square greater than 1
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1e5;

// Function to find the largest
// divisor not divisible by any
// perfect square greater than 1
int findLargestDivisor(int n)
{
    // set to store divisors in
    // descending order
    int m = n;
    set<int, greater<int> > s;
    s.insert(1);
    s.insert(n);

    for (int i = 2; i < sqrt(n) + 1; i++) {
        // If the number is divisible
        // by i, then insert it
        if (n % i == 0) {
            s.insert(n / i);
            s.insert(i);
            while (m % i == 0)
                m /= i;
        }
    }

    if (m > 1)
        s.insert(m);

    // Vector to store perfect squares
    vector<int> vec;
    for (int i = 2; i <= MAX; i++)
        vec.push_back(i * i);

    // Check for each divisor, if it is not
    // divisible by any perfect square,
    // simply return it as the answer.
    for (auto d : s) {
        int divi = 0;
        for (int j = 0; j < vec.size()
                        && vec[j] <= d;
             j++) {
            if (d % vec[j] == 0) {
                divi = 1;
                break;
            }
        }
        if (!divi)
            return d;
    }
}

// Driver Code
int main()
{
    int n = 12;
    cout << findLargestDivisor(n) << endl;

    n = 97;
    cout << findLargestDivisor(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the largest
// divisor not divisible by any
// perfect square greater than 1
import java.util.*;
class Main{

static int MAX = (int)1e5;

// Function to find the largest
// divisor not divisible by any
// perfect square greater than 1
public static int findLargestDivisor(int n)
{
  // set to store divisors in
  // descending order
  int m = n;
  Set<Integer> s =
      new HashSet<Integer>();
  s.add(1);
  s.add(n);

  for (int i = 2;
           i < (int)Math.sqrt(n) + 1; i++)
  {
    // If the number is divisible
    // by i, then insert it
    if (n % i == 0)
    {
      s.add(n / i);
      s.add(i);
      while (m % i == 0)
        m /= i;
    }
  }

  if (m > 1)
    s.add(m);

  List<Integer> l =
       new ArrayList<Integer>(s);

  Collections.sort(l);
  Collections.reverse(l);

  // Vector to store
  // perfect squares
  Vector<Integer> vec =
         new Vector<Integer>();

  for (int i = 2; i <= MAX; i++)
    vec.add(i * i);

  // Check for each divisor, if
  // it is not divisible by any
  // perfect square, simply return
  // it as the answer.
  for (int d : l)
  {
    int divi = 0;

    for (int j = 0;
             j < vec.size() &&
             vec.get(j) <= d; j++)
    {
      if (d % vec.get(j) == 0)
      {
        divi = 1;
        break;
      }
    }
    if (divi == 0)
      return d;
  }
  return 0;
}

// Driver code   
public static void main(String[] args)
{
  int n = 12;
  System.out.println(findLargestDivisor(n));

  n = 97;
  System.out.println(findLargestDivisor(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 Program to find the largest
# divisor not divisible by any
# perfect square greater than 1

MAX = 10 ** 5

# Function to find the largest
# divisor not divisible by any
# perfect square greater than 1
def findLargestDivisor(n):

    # set to store divisors in
    # descending order
    m = n
    s = set()
    s.add(1)
    s.add(n)

    for i in range(2, int(n ** (0.5)) + 1):

        # If the number is divisible
        # by i, then insert it
        if n % i == 0:
            s.add(n // i)
            s.add(i)
            while m % i == 0:
                m //= i

    if m > 1:
        s.add(m)

    # Vector to store perfect squares
    vec = [i**2 for i in range(2, MAX + 1)]

    # Check for each divisor, if it is not
    # divisible by any perfect square,
    # simply return it as the answer.
    for d in sorted(s, reverse = True):

        divi, j = 0, 0
        while j < len(vec) and vec[j] <= d:

            if d % vec[j] == 0:
                divi = 1
                break
            j += 1       

        if not divi:
            return d

# Driver Code
if __name__ == "__main__":

    n = 12
    print(findLargestDivisor(n))

    n = 97
    print(findLargestDivisor(n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the largest
// divisor not divisible by any
// perfect square greater than 1
using System;
using System.Collections.Generic;

class GFG{

static int MAX = (int)1e5;

// Function to find the largest
// divisor not divisible by any
// perfect square greater than 1
static int findLargestDivisor(int n)
{

    // Set to store divisors in
    // descending order
    int m = n;

    HashSet<int> s = new HashSet<int>();
    s.Add(1);
    s.Add(n);

    for(int i = 2;
            i < (int)Math.Sqrt(n) + 1;
            i++)
    {

        // If the number is divisible
        // by i, then insert it
        if (n % i == 0)
        {
            s.Add(n / i);
            s.Add(i);

            while (m % i == 0)
                m /= i;
        }
    }

    if (m > 1)
        s.Add(m);

    List<int> l = new List<int>(s);
    l.Sort();
    l.Reverse();

    // Vector to store
    // perfect squares
    List<int> vec = new List<int>();

    for(int i = 2; i <= MAX; i++)
        vec.Add(i * i);

    // Check for each divisor, if
    // it is not divisible by any
    // perfect square, simply return
    // it as the answer.
    foreach(int d in l)
    {
        int divi = 0;

        for(int j = 0;
                j < vec.Count && vec[j] <= d;
                j++)
        {
            if (d % vec[j] == 0)
            {
                divi = 1;
                break;
            }
        }
        if (divi == 0)
            return d;
    }
    return 0;
} 

// Driver code
static void Main()
{
    int n = 12;
    Console.WriteLine(findLargestDivisor(n));

    n = 97;
    Console.WriteLine(findLargestDivisor(n));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// Javascript Program to find the largest
// divisor not divisible by any
// perfect square greater than 1

let MAX = 100000;

// Function to find the largest
// divisor not divisible by any
// perfect square greater than 1
function findLargestDivisor(n)
{
  // set to store divisors in
  // descending order
  let m = n;
  let s = new Set();
  s.add(1);
  s.add(n);

  for (let i = 2;
           i < Math.floor(Math.sqrt(n)) + 1; i++)
  {
    // If the number is divisible
    // by i, then insert it
    if (n % i == 0)
    {
      s.add(Math.floor(n / i));
      s.add(i);
      while (m % i == 0)
        m = Math.floor(m/i);
    }
  }

  if (m > 1)
    s.add(m);

  let l =Array.from(s);

  l.sort(function(a,b){return a-b;});
  l.reverse();
  // Vector to store
  // perfect squares
  let vec = [];

  for (let i = 2; i <= MAX; i++)
    vec.push(i * i);

  // Check for each divisor, if
  // it is not divisible by any
  // perfect square, simply return
  // it as the answer.
  for (let d=0;d<l.length;d++)
  {
    let divi = 0;

    for (let j = 0;
             j < vec.length &&
             vec[j] <= l[d]; j++)
    {
      if (l[d] % vec[j] == 0)
      {
        divi = 1;
        break;
      }
    }
    if (divi == 0)
      return l[d];
  }
  return 0;
}

// Driver code  
let n = 12;
document.write(findLargestDivisor(n)+"<br>");

n = 97;
document.write(findLargestDivisor(n)+"<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
6
97
```

一种**有效的方法**是对每个 I 用 I 除 n，使得(i * i)除 n。

## C++

```
// Efficient C++ Program to find the
// largest divisor not divisible by any
// perfect square greater than 1
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// divisor not divisible by any
// perfect square greater than 1
int findLargestDivisor(int n)
{
    for (int i = 2; i < sqrt(n) + 1; i++) {

        // If the number is divisible
        // by i*i, then remove one i
        while (n % (i * i) == 0) {
            n = n / i;
        }
    }

    // Now all squares are removed from n
    return n;   
}

// Driver Code
int main()
{
    int n = 12;
    cout << findLargestDivisor(n) << endl;

    n = 97;
    cout << findLargestDivisor(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java Program to find the
// largest divisor not divisible by any
// perfect square greater than 1

public class GFG
{

    // Function to find the largest
    // divisor not divisible by any
    // perfect square greater than 1
    static int findLargestDivisor(int n)
    {
        for (int i = 2; i < Math.sqrt(n) + 1; i++) {

            // If the number is divisible
            // by i*i, then remove one i
            while (n % (i * i) == 0) {
                n = n / i;
            }
        }

        // Now all squares are removed from n
        return n;    
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 12;
        System.out.println(findLargestDivisor(n)) ;

        n = 97;
        System.out.println(findLargestDivisor(n)) ;

    }
    // This code is contributed
    // by Ryuga
}
```

## 蟒蛇 3

```
# Efficient Python3 Program to find the
# largest divisor not divisible by any
# perfect square greater than 1
import math

# Function to find the largest
# divisor not divisible by any
# perfect square greater than 1
def findLargestDivisor( n):

    for i in range (2, int(math.sqrt(n)) + 1) :

        # If the number is divisible
        # by i*i, then remove one i
        while (n % (i * i) == 0) :
            n = n // i

    # Now all squares are removed from n
    return n

# Driver Code
if __name__ == "__main__":

    n = 12
    print (findLargestDivisor(n))

    n = 97
    print (findLargestDivisor(n))

# This code is contributed by ita_c
```

## C#

```
// Efficient C# Program to find the
// largest divisor not divisible by any
// perfect square greater than 1
using System;
public class GFG
{

    // Function to find the largest
    // divisor not divisible by any
    // perfect square greater than 1
    static int findLargestDivisor(int n)
    {
        for (int i = 2; i < Math.Sqrt(n) + 1; i++) {

            // If the number is divisible
            // by i*i, then remove one i
            while (n % (i * i) == 0) {
                n = n / i;
            }
        }

        // Now all squares are removed from n
        return n;    
    }

    // Driver Code
    public static void Main()
    {
        int n = 12;
        Console.WriteLine(findLargestDivisor(n)) ;

        n = 97;
        Console.WriteLine(findLargestDivisor(n)) ;

    }
}
    // This code is contributed
    // by Mukul Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP Program to find the
// largest divisor not divisible by
// any perfect square greater than 1

// Function to find the largest
// divisor not divisible by any
// perfect square greater than 1
function findLargestDivisor($n)
{
    for ($i = 2; $i < sqrt($n) + 1; $i++)
    {

        // If the number is divisible
        // by i*i, then remove one i
        while ($n % ($i * $i) == 0)
        {
            $n = $n / $i;
        }
    }

    // Now all squares are removed from n
    return $n;
}

// Driver Code
$n = 12;
echo(findLargestDivisor($n));
echo("\n");

$n = 97;
echo(findLargestDivisor($n)) ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Efficient Javascript Program to find the
    // largest divisor not divisible by any
    // perfect square greater than 1

    // Function to find the largest
    // divisor not divisible by any
    // perfect square greater than 1
    function findLargestDivisor(n)
    {
        for (let i = 2; i < Math.sqrt(n) + 1; i++)
        {

            // If the number is divisible
            // by i*i, then remove one i
            while (n % (i * i) == 0) {
                n = n / i;
            }
        }

        // Now all squares are removed from n
        return n;  
    }

    let n = 12;
    document.write(findLargestDivisor(n) + "</br>");

    n = 97;
    document.write(findLargestDivisor(n) + "</br>");

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
6
97
```