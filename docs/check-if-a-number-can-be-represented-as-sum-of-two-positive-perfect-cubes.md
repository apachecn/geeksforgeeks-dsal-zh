# 检查一个数是否可以表示为两个正完美立方体的和

> 原文:[https://www . geesforgeks . org/check-如果一个数字可以表示为两个正完美立方体的总和/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-sum-of-two-positive-perfect-cubes/)

给定一个整数 **N** ，任务是检查 **N** 是否可以表示为两个正的[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)的和。

**示例:**

> **输入:** N = 28
> **输出:**是
> **说明:**
> 自，28 = 27+1 = 3<sup>3</sup>+1<sup>3</sup>。
> 因此，要求的答案是肯定的。
> 
> **输入:**N = 34
> T3】输出:否

**方法:**想法是将从 **1** 到[的所有数字的完美立方存储在](https://www.geeksforgeeks.org/find-cubic-root-of-a-number/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，并检查 **N** 是否可以表示为地图中存在的两个数字[的和](https://www.geeksforgeeks.org/map-find-function-in-c-stl/)。按照以下步骤解决问题:

*   初始化一个[有序图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如**立方体，**按照排序顺序存储前 N 个自然数的完美立方体。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并检查总和等于 **N** 的对。
*   如果发现这样的一对具有总和 **N** ，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be represented
// as sum of two perfect cubes or not
void sumOfTwoPerfectCubes(int N)
{
    // Stores the perfect cubes
    // of first N natural numbers
    map<int, int> cubes;
    for (int i = 1; i * i * i <= N; i++)
        cubes[i * i * i] = i;

    // Traverse the map
    map<int, int>::iterator itr;
    for (itr = cubes.begin();
         itr != cubes.end(); itr++) {

        // Stores first number
        int firstNumber = itr->first;

        // Stores second number
        int secondNumber = N - itr->first;

        // Search the pair for the first
        // number to obtain sum N from the Map
        if (cubes.find(secondNumber)
            != cubes.end()) {
            cout << "True";
            return;
        }
    }

    // If N cannot be represented as
    // sum of two positive perfect cubes
    cout << "False";
}

// Driver Code
int main()
{
    int N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    sumOfTwoPerfectCubes(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to check if N can be represented
  // as sum of two perfect cubes or not
  public static void sumOfTwoPerfectCubes(int N)
  {

    // Stores the perfect cubes
    // of first N natural numbers
    HashMap<Integer, Integer> cubes = new HashMap<>();
    for (int i = 1; i * i * i <= N; i++)
      cubes.put((i * i * i), i);

    // Traverse the map
    Iterator<Map.Entry<Integer, Integer> > itr
      = cubes.entrySet().iterator();
    while (itr.hasNext())
    {
      Map.Entry<Integer, Integer> entry = itr.next();

      // Stores first number
      int firstNumber = entry.getKey();

      // Stores second number
      int secondNumber = N - entry.getKey();

      // Search the pair for the first
      // number to obtain sum N from the Map
      if (cubes.containsKey(secondNumber))
      {
        System.out.println("True");
        return;
      }
    }

    // If N cannot be represented as
    // sum of two positive perfect cubes
    System.out.println("False");
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    sumOfTwoPerfectCubes(N);
  }
}

// This code is contributed by shailjapriya.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N can be represented
# as sum of two perfect cubes or not
def sumOfTwoPerfectCubes(N) :

    # Stores the perfect cubes
    # of first N natural numbers
    cubes = {}
    i = 1
    while i*i*i <= N :
        cubes[i*i*i] = i
        i += 1

    # Traverse the map
    for itr in cubes :

        # Stores first number
        firstNumber = itr

        # Stores second number
        secondNumber = N - itr

        # Search the pair for the first
        # number to obtain sum N from the Map
        if secondNumber in cubes :
            print("True", end = "")
            return

    # If N cannot be represented as
    # sum of two positive perfect cubes
    print("False", end = "")

N = 28

# Function call to check if N
# can be represented as
# sum of two perfect cubes or not
sumOfTwoPerfectCubes(N)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

  // Function to check if N can be represented
  // as sum of two perfect cubes or not
  public static void sumOfTwoPerfectCubes(int N)
  {

    // Stores the perfect cubes
    // of first N natural numbers
    Dictionary<int,
             int> cubes = new Dictionary<int,
                                      int>();
    for (int i = 1; i * i * i <= N; i++)
      cubes.Add((i * i * i), i);

    var val = cubes.Keys.ToList();
    foreach(var key in val)
    {
      // Stores first number
      int firstNumber = cubes[1];

      // Stores second number
      int secondNumber = N - cubes[1];

      // Search the pair for the first
      // number to obtain sum N from the Map
      if (cubes.ContainsKey(secondNumber))
      {
        Console.Write("True");
        return;
      }
    }

    // If N cannot be represented as
    // sum of two positive perfect cubes
    Console.Write("False");
  }

// Driver Code
static public void Main()
{
    int N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    sumOfTwoPerfectCubes(N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if N can be represented
// as sum of two perfect cubes or not
function sumOfTwoPerfectCubes(N)
{
    // Stores the perfect cubes
    // of first N natural numbers
    var cubes = new Map();
    for (var i = 1; i * i * i <= N; i++)
        cubes.set(i * i * i, i);

    var ans = false;
    // Traverse the map
    cubes.forEach((value, key) => {
        // Stores first number
        var firstNumber = key;

        // Stores second number
        var secondNumber = N - value;

        // Search the pair for the first
        // number to obtain sum N from the Map
        if (cubes.has(secondNumber)) {
            document.write( "True");
            ans = true;
            return;
        }
    });

    if(ans)
    {
        return;
    }
    // If N cannot be represented as
    // sum of two positive perfect cubes
    document.write( "False");
}

// Driver Code
var N = 28;
// Function call to check if N
// can be represented as
// sum of two perfect cubes or not
sumOfTwoPerfectCubes(N);

</script>
```

**Output**

```
True
```

***时间复杂度:**O(N<sup>1/3</sup>* log(N<sup>1/3</sup>)*
***辅助空间:** O(N <sup>1/3</sup> )*

***<u>进场 2 :</u>***

**使用两个指针:**

我们将 lo 声明为 1，hi 声明为 n(给定数字)的立方根，然后通过(lo<=hi)这个条件，如果电流小于 n，我们将增加 lo，反之，如果大于，则减少 hi，其中电流为(lo*lo*lo + hi*hi*hi)

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be represented
// as sum of two perfect cubes or not
bool sumOfTwoCubes(int n)
{
    long long int lo = 1, hi = (long long int)cbrt(n);
    while (lo <= hi) {
        long long int curr = (lo * lo * lo + hi * hi * hi);
        if (curr == n)
            // if it is same return true;
            return true;
        if (curr < n)
            // if the curr smaller than n increment the lo
            lo++;
        else
            // if the curr is greater than curr decrement
            // the hi
            hi--;
    }
    return false;
}

// Driver Code
int main()
{
    int N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    if (sumOfTwoCubes(N)) {
        cout << "True";
    }
    else {
        cout << "False";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

// Function to check if N can be represented
// as sum of two perfect cubes or not
static boolean sumOfTwoCubes(int n)
{
    int lo = 1, hi = (int)Math.cbrt(n);
    while (lo <= hi) {
        int curr = (lo * lo * lo + hi * hi * hi);
        if (curr == n)

            // if it is same return true;
            return true;
        if (curr < n)

            // if the curr smaller than n increment the lo
            lo++;
        else

            // if the curr is greater than curr decrement
            // the hi
            hi--;
    }
    return false;
}

// Driver Code
public static void main (String[] args)
{
    int N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    if (sumOfTwoCubes(N)) {
        System.out.println("True");
    }
    else {
        System.out.println("False");
    }

}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if N can be represented
# as sum of two perfect cubes or not
def sumOfTwoCubes(n):

    lo = 1
    hi = round(math.pow(n, 1 / 3))

    while (lo <= hi):
        curr = (lo * lo * lo + hi * hi * hi)
        if (curr == n):

            # If it is same return true;
            return True
        if (curr < n):

            # If the curr smaller than n increment the lo
            lo += 1
        else:

            # If the curr is greater than curr decrement
            # the hi
            hi -= 1

    return False

# Driver Code
N = 28

# Function call to check if N
# can be represented as sum of
# two perfect cubes or not
if (sumOfTwoCubes(N)):
    print("True")
else:
    print("False")

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to check if N can be represented
// as sum of two perfect cubes or not
static bool sumOfTwoCubes(int n)
{
    int lo = 1, hi = (int)Math.Pow(n, (1.0 / 3.0));
    while (lo <= hi) {
        int curr = (lo * lo * lo + hi * hi * hi);
        if (curr == n)

            // if it is same return true;
            return true;
        if (curr < n)

            // if the curr smaller than n increment the lo
            lo++;
        else

            // if the curr is greater than curr decrement
            // the hi
            hi--;
    }
    return false;
}

// Driver Code
public static void Main (String[] args)
{
    int N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    if (sumOfTwoCubes(N)) {
        Console.Write("True");
    }
    else {
        Console.Write("False");
    }

}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to check if N can be represented
// as sum of two perfect cubes or not
function sumOfTwoCubes(n)
{
    var lo = 1, hi = (n);
    while (lo <= hi) {
        var curr = (lo * lo * lo + hi * hi * hi);
        if (curr == n)

            // if it is same return true;
            return true;
        if (curr < n)

            // if the curr smaller than n increment the lo
            lo++;
        else

            // if the curr is greater than curr decrement
            // the hi
            hi--;
    }
    return false;
}

// Driver Code
    var N = 28;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    if (sumOfTwoCubes(N)) {
        document.write("True");
    }
    else {
        document.write("False");
    }

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
True
```

**时间复杂度:** O(sqrt(n))，其中 n 为给定数

**空间复杂度:** O(1)