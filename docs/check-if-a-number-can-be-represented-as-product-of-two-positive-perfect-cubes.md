# 检查一个数是否可以表示为两个正完美立方体的乘积

> 原文:[https://www . geesforgeks . org/check-如果一个数字可以表示为两个正完美立方体的乘积/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-product-of-two-positive-perfect-cubes/)

给定一个正整数 **N** ，任务是检查给定的数字 **N** 是否可以表示为两个正的[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)的乘积。如果可能，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 216
> **输出:**是
> **说明:**
> 给定的数字 N(= 216)可以表示为 8 * 27 = 2 <sup>3</sup> * 3 <sup>3</sup> 。
> 因此，打印“是”。
> 
> **输入:**N = 10
> T3】输出:否

**方法:**解决给定问题最简单的方法是将从 **1** 到[的所有数字的完美立方根**N**T7】存储在](https://www.geeksforgeeks.org/find-cubic-root-of-a-number/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，并检查 **N** 是否可以表示为地图中存在的两个数字[的乘积](https://www.geeksforgeeks.org/map-find-function-in-c-stl/)。

按照以下步骤解决问题:

*   初始化一个[有序地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说**立方体**，它以有序的顺序存储完美的立方体。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)查看是否有产品为 **N** 的配对，然后打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N can
// be represented as the product
// of two perfect cubes or not
void productOfTwoPerfectCubes(int N)
{
    // Stores the perfect cubes
    map<int, int> cubes;

    for (int i = 1;
         i * i * i <= N; i++)
        cubes[i * i * i] = i;

    // Traverse the Map
    for (auto itr = cubes.begin();
         itr != cubes.end();
         itr++) {

        // Stores the first number
        int firstNumber = itr->first;

        if (N % itr->first == 0) {

            // Stores the second number
            int secondNumber = N / itr->first;

            // Search the pair for the
            // first number to obtain
            // product N from the Map
            if (cubes.find(secondNumber)
                != cubes.end()) {
                cout << "Yes";
                return;
            }
        }
    }

    // If N cannot be represented
    // as the product of the two
    // positive perfect cubes
    cout << "No";
}

// Driver Code
int main()
{
    int N = 216;
    productOfTwoPerfectCubes(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if N can
// be represented as the product
// of two perfect cubes or not
static void productOfTwoPerfectCubes(int N)
{

    // Stores the perfect cubes
    Map<Integer, Integer> cubes = new HashMap<>();

    for(int i = 1; i * i * i <= N; i++)
        cubes.put(i * i * i,i);

    // Traverse the Map
    for(Map.Entry<Integer,
                  Integer> itr: cubes.entrySet())
    {

        // Stores the first number
        int firstNumber = itr.getKey();

        if (N % itr.getKey() == 0)
        {

            // Stores the second number
            int secondNumber = N / itr.getKey();

            // Search the pair for the
            // first number to obtain
            // product N from the Map
            if (cubes.containsKey(secondNumber))
            {
                System.out.println("Yes");
                return;
            }
        }
    }

    // If N cannot be represented
    // as the product of the two
    // positive perfect cubes
    System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int N = 216;

    productOfTwoPerfectCubes(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N can
# be represented as the product
# of two perfect cubes or not
def productOfTwoPerfectCubes(N):

    # Stores the perfect cubes
    cubes = {}

    i = 1

    while i * i * i <= N:
        cubes[i * i * i] = i
        i += 1

    # Traverse the Map
    for itr in cubes:

        # Stores the first number
        firstNumber = itr

        if (N % itr == 0):

            # Stores the second number
            secondNumber = N // itr

            # Search the pair for the
            # first number to obtain
            # product N from the Map
            if (secondNumber in cubes):
                print("Yes")
                return

    # If N cannot be represented
    # as the product of the two
    # positive perfect cubes
    print("No")

# Driver Code
if __name__ == "__main__":

    N = 216

    productOfTwoPerfectCubes(N)

# This code is contributed by mohit ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

 // Function to check if N can
// be represented as the product
// of two perfect cubes or not
static void productOfTwoPerfectCubes(int N)
{
    // Stores the perfect cubes
    Dictionary<int,int> cubes = new Dictionary<int,int>();

    for (int i = 1; i * i * i <= N; i++){
       cubes.Add(i * i * i, i);
    }

    // Traverse the Map
    foreach(KeyValuePair<int, int> kvp in cubes)
   {

        // Stores the first number
        int firstNumber = kvp.Key;

        if (N % kvp.Key == 0) {

            // Stores the second number
            int secondNumber = N / kvp.Key;

            // Search the pair for the
            // first number to obtain
            // product N from the Map
            if (cubes.ContainsKey(secondNumber)) {
                Console.Write("Yes");
                return;
            }
        }
    }

    // If N cannot be represented
    // as the product of the two
    // positive perfect cubes
    Console.Write("No");
}

// Driver Code
public static void Main()
{
    int N = 216;
    productOfTwoPerfectCubes(N);

}
}

// This code is contributed by ipg2016107..
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if N can
// be represented as the product
// of two perfect cubes or not
function productOfTwoPerfectCubes(N)
{

    // Stores the perfect cubes
    let cubes = new Map();

    for(let i = 1; i * i * i <= N; i++)
        cubes.set(i * i * i, i);

    // Traverse the Map
    for(let [key, value] of cubes.entries())
    {

        // Stores the first number
        let firstNumber = key;

        if (N % key == 0)
        {

            // Stores the second number
            let secondNumber = N / key;

            // Search the pair for the
            // first number to obtain
            // product N from the Map
            if (cubes.has(secondNumber))
            {
                document.write("Yes<br>");
                return;
            }
        }
    }

    // If N cannot be represented
    // as the product of the two
    // positive perfect cubes
    document.write("No<br>");
}

// Driver code
let N = 216;

productOfTwoPerfectCubes(N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>1/3</sup>* log(N))*
***辅助空间:** O(N <sup>1/3</sup> )*

**高效方法:**上述方法也可以基于这样的观察进行优化，即只有完美立方体可以表示为 2 个完美立方体的乘积。

> 让两个数为 **x** 和 **y** 这样 x<sup>3</sup>* y<sup>3</sup>= N**—(1)
> 等式(1)可以写成:
> =>(x * y)<sup>3</sup>= N
> 取立方根两边，
> = > x*y = (N) <sup>1/3 【T17</sup>**

**所以，问题就简化为[检查 **N** 是否是一个完美的立方体](https://www.geeksforgeeks.org/perfect-cube/)。如果发现是真的，打印**“是”**，否则**“否”**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the number N
// can be represented as the product
// of two perfect cubes or not
void productOfTwoPerfectCubes(int N)
{
    int cube_root;
    cube_root = round(cbrt(N));

    // If cube of cube_root is N
    if (cube_root * cube_root
            * cube_root
        == N) {

        cout << "Yes";
        return;
    }

    // Otherwise, print No
    else {
        cout << "No";
        return;
    }
}

// Driver Code
int main()
{
    int N = 216;
    productOfTwoPerfectCubes(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.lang.*;

class GFG{

// Function to check if the number N
// can be represented as the product
// of two perfect cubes or not
public static void productOfTwoPerfectCubes(double N)
{
    double cube_root;
    cube_root = Math.round(Math.cbrt(N));

    // If cube of cube_root is N
    if (cube_root * cube_root * cube_root == N)
    {
        System.out.println("Yes");
        return;
    }

    // Otherwise, print No
    else
    {
        System.out.println("No");
        return;
    }
}

// Driver Code
public static void main(String args[])
{
    double N = 216;

    productOfTwoPerfectCubes(N);
}
}

// This code is contributed by SoumikMondal
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to check if the number N
# can be represented as the product
# of two perfect cubes or not
def productOfTwoPerfectCubes(N):

    cube_root = round((N) ** (1 / 3))
    print(cube_root)

    # If cube of cube_root is N
    if (cube_root * cube_root * cube_root == N):
        print("Yes")
        return

    # Otherwise, prNo
    else:
        print("No")
        return

# Driver Code
if __name__ == '__main__':

    N = 216

    productOfTwoPerfectCubes(N)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to check if the number N
// can be represented as the product
// of two perfect cubes or not
public static void productOfTwoPerfectCubes(double N)
{
    double cube_root;
    cube_root = Math.Round(Math.Cbrt(N));

    // If cube of cube_root is N
    if (cube_root * cube_root * cube_root == N)
    {
        Console.Write("Yes");
        return;
    }

    // Otherwise, print No
    else
    {
        Console.Write("No");
        return;
    }
}

// Driver Code
static public void Main()
{
    double N = 216;

    productOfTwoPerfectCubes(N);
}
}

// This code is contributed by mohit kumar 29.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to check if the number N
// can be represented as the product
// of two perfect cubes or not
function productOfTwoPerfectCubes(N)
{
    var cube_root;
    cube_root = Math.round(Math.cbrt(N));

    // If cube of cube_root is N
    if (cube_root * cube_root * cube_root == N)
    {
        document.write("Yes");
        return;
    }

    // Otherwise, print No
    else
    {
        document.write("No");
        return;
    }
}

// Driver code
var N = 216;
productOfTwoPerfectCubes(N);

// This code is contributed by Ankita saini

</script>
```

****Output:** 

```
Yes
```** 

*****时间复杂度:**O(N<sup>1/3</sup>)*
***辅助空间:** O(1)***