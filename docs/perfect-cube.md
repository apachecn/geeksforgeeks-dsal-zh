# 完美立方体

> 原文:[https://www.geeksforgeeks.org/perfect-cube/](https://www.geeksforgeeks.org/perfect-cube/)

给定一个数字 **N** ，任务是检查给定的数字 **N** 是否是一个完美的立方体。
**例:**

> **输入:** N = 216
> **输出:**是
> **说明:**
> As 216 = 6*6*6。因此，216 的立方根是 6。
> **输入:** N = 100
> **输出:**否

**方法 1:天真的方法**
想法是检查从 **1** 到 **N** 的每个数字，如果这些数字的立方等于 **N** 。如果是，那么这个数就是 **N** 的立方根，N 就是一个完美的立方体。

下面是上述方法的实现:

## C++

```
// C++ program to check whether the given
// number N is the perfect cube or not
.
#include <bits/stdc++.h>
    using namespace std;

// Function to check if a number
// is a perfect Cube or not
void perfectCube(int N)
{
    int cube;

    // Iterate from 1-N
    for (int i; i <= N; i++) {

        // Find the cube of
        // every number
        cube = i * i * i;

        // Check if cube equals
        // N or not
        if (cube == N) {
            cout << "Yes";
            return;
        }
        else if (cube > N) {
            cout << "NO";
            return;
        }
    }
}

// Driver code
int main()
{
    int N = 216;

    // Function call
    perfectCube(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the given
// number N is the perfect cube or not
class GFG {

    // Function to check if a number
    // is a perfect Cube or not
    static void perfectCube(int N)
    {
        int cube;

        // Iterate from 1-N
        for (int i = 0; i <= N; i++) {

            // Find the cube of
            // every number
            cube = i * i * i;

            // Check if cube equals
            // N or not
            if (cube == N) {
                System.out.println("Yes");
                return;
            }
            else if (cube > N) {
                System.out.println("NO");
                return;
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 216;

        // Function call
        perfectCube(N);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to check whether the given
# number N is the perfect cube or not

# Function to check if a number
# is a perfect Cube or not
def perfectCube(N) :

    cube = 0;

    # Iterate from 1-N
    for i in range(N + 1) :

        # Find the cube of
        # every number
        cube = i * i * i;

        # Check if cube equals
        # N or not
        if (cube == N) :
            print("Yes");
            return;

        elif (cube > N) :
            print("NO");
            return;

# Driver code
if __name__ == "__main__" :

    N = 216;

    # Function call
    perfectCube(N);

# This code is contributed  by Yash_R
```

## C#

```
// C# program to check whether the given
// number N is the perfect cube or not
using System;

class GFG {

    // Function to check if a number
    // is a perfect Cube or not
    static void perfectCube(int N)
    {
        int cube;

        // Iterate from 1-N
        for (int i = 0; i <= N; i++) {

            // Find the cube of
            // every number
            cube = i * i * i;

            // Check if cube equals
            // N or not
            if (cube == N) {
                Console.WriteLine("Yes");
                return;
            }
            else if (cube > N) {
                Console.WriteLine("NO");
                return;
            }
        }
    }

    // Driver code
    public static void Main (string[] args)
    {
        int N = 216;

        // Function call
        perfectCube(N);

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to check whether the given
// number N is the perfect cube or not

// Function to check if a number
// is a perfect Cube or not
function perfectCube(N)
{
    let cube;

    // Iterate from 1-N
    for(let i = 0; i <= N; i++)
    {

        // Find the cube of
        // every number
        cube = i * i * i;

        // Check if cube equals
        // N or not
        if (cube === N)
        {
            document.write("Yes");
            return;
        }
        else if (cube > N)
        {
            document.write("NO");
            return;
        }
    }
}

// Driver code
let N = 216;

// Function call
perfectCube(N);

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)

**辅助空间:** O(1)

**方法二:使用内置函数**
思路是使用内置函数([**【cbrt()**](https://www.geeksforgeeks.org/stdcbrt-in-c/))求一个数的立方根，该数返回该数的立方根 **N** 的[楼层值](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)。如果这个数的立方等于 **N** ，那么 **N** 就是完美立方，否则 **N** 就不是完美立方。

下面是上述方法的实现:

## C++

```
// C++ program to check whether the given
// number N is the perfect cube or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is
// a perfect Cube using inbuilt function
void perfectCube(int N)
{
    int cube_root;
    cube_root = round(cbrt(N));

    // If cube of cube_root is equals to N,
    // then print Yes Else print No
    if (cube_root * cube_root * cube_root == N) {
        cout << "Yes";
        return;
    }
    else {
        cout << "NO";
        return;
    }
}

// Driver's code
int main()
{
    int N = 125;

    // Function call to check
    // N is cube or not
    perfectCube(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the given
// number N is the perfect cube or not
public class GFG {

    // Function to check if a number is
    // a perfect Cube using inbuilt function
    static void perfectCube(int N)
    {
        int cube_root;
        cube_root = (int)Math.round(Math.cbrt(N));

        // If cube of cube_root is equals to N,
        // then print Yes Else print No
        if (cube_root * cube_root * cube_root == N) {
            System.out.println("Yes");
            return;
        }
        else {
            System.out.println("NO");
            return;
        }
    }

    // Driver's code
    public static void main (String[] args)
    {
        int N = 125;

        // Function call to check
        // N is cube or not
        perfectCube(N);

    }

}
// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python program to check whether the given
# number N is the perfect cube or not

# Function to check if a number is
# a perfect Cube using inbuilt function
def perfectCube(N) :

    cube_root = round(N**(1/3));

    # If cube of cube_root is equals to N,
    # then print Yes Else print No
    if cube_root * cube_root * cube_root == N :
        print("Yes");
        return;

    else :
        print("NO");
        return;

# Driver's code
if __name__ == "__main__" :
    N = 125;

    # Function call to check
    # N is cube or not
    perfectCube(N);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to check whether the given
// number N is the perfect cube or not
using System;

class GFG {

    // Function to check if a number is
    // a perfect Cube using inbuilt function
    static void perfectCube(int N)
    {
        int cube_root;
        cube_root = (int)Math.Round(Math.Cbrt(N));

        // If cube of cube_root is equals to N,
        // then print Yes Else print No
        if (cube_root * cube_root * cube_root == N) {
            Console.WriteLine("Yes");
            return;
        }
        else {
            Console.WriteLine("NO");
            return;
        }
    }

    // Driver's code
    public static void Main (string[] args)
    {
        int N = 125;

        // Function call to check
        // N is cube or not
        perfectCube(N);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to check whether the given
// number N is the perfect cube or not

// Function to check if a number is
// a perfect Cube using inbuilt function
function perfectCube(N)
{
    let cube_root;
    cube_root = Math.round(Math.cbrt(N));

    // If cube of cube_root is equals to N,
    // then print Yes Else print No
    if ((cube_root * cube_root * cube_root) == N) {
        document.write("Yes");
        return;
    }
    else {
        document.write("NO");
        return;
    }
}

// Driver's code
let N = 125;

// Function call to check
// N is cube or not
perfectCube(N);

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(cbrt(N))

**辅助空间:** O(1)

**方法三:使用** [**质因数**](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)

1.  使用[这篇](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)文章中的方法找到给定数字 **N** 的所有[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。
2.  将上面获得的所有[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的频率存储在[哈希图](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中。
3.  遍历[哈希图](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)，如果每个[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的频率不是 **3** 的倍数，那么给定的数字 **N** 就不是一个完美的立方体。

下面是上述方法的实现:

## C++

```
// C++ program to check if a number
// is a perfect cube using prime factors
#include<bits/stdc++.h>
using namespace std;

// Inserts the prime factor in HashMap
// if not present
// if present updates it's frequency
map<int, int> insertPF(map<int, int> primeFact,
                           int fact)
{
    if (primeFact.find(fact) != primeFact.end())
    {
        primeFact[fact]++;
    }
    else
    {
        primeFact[fact] = 1;
    }
    return primeFact;
}

// A utility function to find all
// prime factors of a given number N
map<int, int> primeFactors (int n)
{
    map<int, int> primeFact;

    // Insert the number of 2s
    // that divide n
    while (n % 2 == 0)
    {
        primeFact = insertPF(primeFact, 2);
        n /= 2;
    }

    // n must be odd at this point
    // So we can skip one element
    for(int i = 3; i <= sqrt(n); i += 2)
    {

        // while i divides n, insert
        // i and divide n
        while (n % i == 0)
        {
            primeFact = insertPF(primeFact, i);
            n /= i;
        }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if (n > 2)
        primeFact = insertPF(primeFact, n);

    return primeFact;
}

// Function to check if a
// number is perfect cube
string perfectCube (int n)
{
    map<int, int> primeFact;
    primeFact = primeFactors(n);

    // Iteration in Map
    for(auto x : primeFact)
    {
        if (x.second % 3 != 0)
            return "No";
    }
    return "Yes";
}

// Driver Code
int main()
{
    int N = 216;

    // Function to check if N is
    // perfect cube or not
    cout << perfectCube(N);

    return 0;
}

// This code is contributed by himanshu77
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// is a perfect cube using prime factors

import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Inserts the prime factor in the Hash Map
    // if not present
    // If present updates it's frequency
    public static HashMap<Integer, Integer>
    insertPF(HashMap<Integer, Integer> primeFact,
             int fact)
    {
        if (primeFact.containsKey(fact)) {

            int freq;
            freq = primeFact.get(fact);
            primeFact.replace(fact, ++freq);
        }
        else {
            primeFact.put(fact, 1);
        }
        return primeFact;
    }

    // A utility function to find all
    // prime factors of a given number N
    public static HashMap<Integer, Integer>
    primeFactors(int n)
    {

        HashMap<Integer, Integer> primeFact
            = new HashMap<>();

        // Insert the number of 2s
        // that divide n
        while (n % 2 == 0) {
            primeFact = insertPF(primeFact, 2);
            n /= 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        for (int i = 3; i <= Math.sqrt(n);
             i += 2) {

            // While i divides n, insert i
            // and divide n
            while (n % i == 0) {
                primeFact = insertPF(primeFact, i);
                n /= i;
            }
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2
        if (n > 2)
            primeFact = insertPF(primeFact, n);

        return primeFact;
    }

    // Function to check if a number
    // is a perfect cube
    public static String perfectCube(int n)
    {

        HashMap<Integer, Integer> primeFact;
        primeFact = primeFactors(n);

        // Using values() for iteration
        // over keys
        for (int freq : primeFact.values()) {
            if (freq % 3 != 0)
                return "No";
        }
        return "Yes";
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 216;

        // Function to check if N is
        // perfect cube or not
        System.out.println(perfectCube(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if a number
# is a perfect cube using prime factors
import math

# Inserts the prime factor in HashMap
# if not present
# if present updates it's frequency
def insertPF(primeFact, fact) :

    if (fact in primeFact) :

        primeFact[fact] += 1

    else :

        primeFact[fact] = 1

    return primeFact

# A utility function to find all
# prime factors of a given number N
def primeFactors (n) :

    primeFact = {}

    # Insert the number of 2s
    # that divide n
    while (n % 2 == 0) :

        primeFact = insertPF(primeFact, 2)
        n = n // 2

    # n must be odd at this point
    # So we can skip one element
    for i in range(3, int(math.sqrt(n)) + 1, 2) :

        # while i divides n, insert
        # i and divide n
        while (n % i == 0) :

            primeFact = insertPF(primeFact, i)
            n = n // i

    # This condition is to handle 
    # the case when n is a prime
    # number greater than 2
    if (n > 2) :
        primeFact = insertPF(primeFact, n)

    return primeFact

# Function to check if a 
# number is perfect cube
def perfectCube (n) :

    primeFact = {}
    primeFact = primeFactors(n)

    # Iteration in Map
    for x in primeFact :

        if (primeFact[x] % 3 != 0) :
            return "No"

    return "Yes"

N = 216

# Function to check if N is
# perfect cube or not
print(perfectCube(N))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to check if a number
// is a perfect cube using prime factors

using System;
using System.Collections.Generic;

public class GFG {

    // Inserts the prime factor in the Hash Map
    // if not present
    // If present updates it's frequency
    public static Dictionary<int, int>
    insertPF(Dictionary<int, int> primeFact,
             int fact)
    {
        if (primeFact.ContainsKey(fact)) {

            int freq;
            freq = primeFact[fact];
            primeFact[fact] = ++freq;
        }
        else {
            primeFact.Add(fact, 1);
        }
        return primeFact;
    }

    // A utility function to find all
    // prime factors of a given number N
    public static Dictionary<int, int>
    primeFactors(int n)
    {

        Dictionary<int, int> primeFact
            = new Dictionary<int, int>();

        // Insert the number of 2s
        // that divide n
        while (n % 2 == 0) {
            primeFact = insertPF(primeFact, 2);
            n /= 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        for (int i = 3; i <= Math.Sqrt(n);
             i += 2) {

            // While i divides n, insert i
            // and divide n
            while (n % i == 0) {
                primeFact = insertPF(primeFact, i);
                n /= i;
            }
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2
        if (n > 2)
            primeFact = insertPF(primeFact, n);

        return primeFact;
    }

    // Function to check if a number
    // is a perfect cube
    public static String perfectCube(int n)
    {

        Dictionary<int, int> primeFact;
        primeFact = primeFactors(n);

        // Using values() for iteration
        // over keys
        foreach (int freq in primeFact.Values) {
            if (freq % 3 != 0)
                return "No";
        }
        return "Yes";
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 216;

        // Function to check if N is
        // perfect cube or not
        Console.WriteLine(perfectCube(N));
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// is a perfect cube using prime factors

// Inserts the prime factor in HashMap
// if not present
// if present updates it's frequency
function insertPF(primeFact, fact)
{
    if (primeFact.has(fact))
    {
        primeFact.set(fact, primeFact.get(fact)+1);
    }
    else
    {
        primeFact.set(fact, 1);
    }
    return primeFact;
}

// A utility function to find all
// prime factors of a given number N
function primeFactors (n)
{
    var primeFact = new Map();

    // Insert the number of 2s
    // that divide n
    while (n % 2 == 0)
    {
        primeFact = insertPF(primeFact, 2);
        n = parseInt(n/2);
    }

    // n must be odd at this point
    // So we can skip one element
    for(var i = 3; i <= Math.sqrt(n); i += 2)
    {

        // while i divides n, insert
        // i and divide n
        while (n % i == 0)
        {
            primeFact = insertPF(primeFact, i);
            n =parseInt(n/i);
        }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if (n > 2)
        primeFact = insertPF(primeFact, n);

    return primeFact;
}

// Function to check if a
// number is perfect cube
function perfectCube (n)
{
    var primeFact = new Map();
    primeFact = primeFactors(n);

    // Iteration in Map
    primeFact.forEach((value, key) => {

        if (value % 3 != 0)
            return "No";
    });
    return "Yes";
}

// Driver Code
var N = 216;
// Function to check if N is
// perfect cube or not
document.write( perfectCube(N));

// This code is contributed by rrrtnx.
</script>   
```

**Output:** 

```
Yes
```

时间复杂度:O(sqrt(n))

辅助空间:0(sqrt(n))