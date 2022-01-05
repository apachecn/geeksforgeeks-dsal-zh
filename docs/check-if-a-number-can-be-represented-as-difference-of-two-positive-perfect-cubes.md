# 检查一个数是否可以表示为两个正完美立方体的差

> 原文:[https://www . geesforgeks . org/check-如果一个数字可以表示为两个正完美立方体的差/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-difference-of-two-positive-perfect-cubes/)

给定一个正整数 **N** ，任务是检查 **N** 是否可以表示为两个正的[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)之间的差。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 124
> **输出:**是
> **说明:**既然 124 可以表示为(125–1)=(5<sup>3</sup>–1<sup>3</sup>)。因此，打印“是”。
> 
> **输入:**N = 4
> T3】输出:否

**方法:**解决给定问题的思路是将 **1** 到 **X** 的所有数字[完美立方体](https://www.geeksforgeeks.org/perfect-cubes-range/)存储在一张[图中，其中 **X** 是最大整数，**X<sup>3</sup>T13】和**(X–1)<sup>3</sup>T17】之间的差值最多为**N**
按照以下步骤解决问题:****](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)

*   初始化一个[有序图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说**立方体**，按照排序顺序存储第一个 **X** 自然数的完美立方体。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并检查差值等于 **N** 的对。如果存在这样的配对，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the number N
// can be represented as a difference
// between two perfect cubes or not
void differenceOfTwoPerfectCubes(int N)
{
    // Stores the perfect cubes
    // of first X natural numbers
    map<int, int> cubes;

    for (int i = 1;
         (i * i * i) - ((i - 1) * (i - 1) * (i - 1)) <= N;
         i++) {

        cubes[i * i * i] = 1;
    }

    map<int, int>::iterator itr;

    // Traverse the map
    for (itr = cubes.begin(); itr != cubes.end(); itr++) {

        // Stores the first number
        int firstNumber = itr->first;

        // Stores the second number
        int secondNumber = N + itr->first;

        // Search the pair for the second
        // number to obtain difference N
        // from the Map
        if (cubes.find(secondNumber) != cubes.end()) {
            cout << "Yes";
            return;
        }
    }

    // If N cannot be represented
    // as difference between two
    // positive perfect cubes
    cout << "No";
}

// Driver Code
int main()
{
    int N = 124;
    differenceOfTwoPerfectCubes(N);

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
  // as difference of two perfect cubes or not
  public static void differenceOfTwoPerfectCubes(int N)
  {

    // Stores the perfect cubes
    // of first N natural numbers
    HashMap<Integer, Integer> cubes = new HashMap<>();
    for (int i = 1; (i * i * i) - ((i - 1) * (i - 1) * (i - 1)) <= N; i++)
      cubes.put((i * i * i), 1);

    // Traverse the map
    Iterator<Map.Entry<Integer, Integer> > itr
      = cubes.entrySet().iterator();
    while (itr.hasNext())
    {
      Map.Entry<Integer, Integer> entry = itr.next();

      // Stores first number
      int firstNumber = entry.getKey();

      // Stores second number
      int secondNumber = N + entry.getKey();

      // Search the pair for the second
      // number to obtain difference N from the Map
      if (cubes.containsKey(secondNumber))
      {
        System.out.println("Yes");
        return;
      }
    }

    // If N cannot be represented as
    // difference of two positive perfect cubes
    System.out.println("No");
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 124;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    differenceOfTwoPerfectCubes(N);
  }
}

// This code is contributed by shailjapriya.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the number N
# can be represented as a difference
# between two perfect cubes or not
def differenceOfTwoPerfectCubes(N):

    # Stores the perfect cubes
    # of first X natural numbers
    cubes = {}

    i = 1
    while ((i * i * i) - ((i - 1) * (i - 1) * (i - 1)) <= N):
        cubes[i * i * i] = 1
        i += 1

    # Traverse the map
    for itr in cubes.keys():

        # Stores the first number
        firstNumber = itr

        # Stores the second number
        secondNumber = N + itr

        # Search the pair for the second
        # number to obtain difference N
        # from the Map
        if ((secondNumber) in cubes):
            print("Yes")
            return

    # If N cannot be represented
    # as difference between two
    # positive perfect cubes
    print("No")

# Driver Code
if __name__ == "__main__":

    N = 124
    differenceOfTwoPerfectCubes(N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to check if N can be represented
// as difference of two perfect cubes or not
public static void differenceOfTwoPerfectCubes(int N)
{

    // Stores the perfect cubes
    // of first N natural numbers
    Dictionary<int,
               int> cubes = new Dictionary<int,
                                           int>();
    for(int i = 1;
            (i * i * i) - ((i - 1) *
            (i - 1) * (i - 1)) <= N;
            i++)
        cubes.Add((i * i * i), 1);

    // Traverse the map
    foreach(KeyValuePair<int, int> entry in cubes)
    {

        // Stores first number
        int firstNumber = entry.Key;

        // Stores second number
        int secondNumber = N + entry.Key;

        // Search the pair for the second
        // number to obtain difference N from the Map
        if (cubes.ContainsKey(secondNumber))
        {
            Console.Write("Yes");
            return;
        }
    }

    // If N cannot be represented as
    // difference of two positive perfect cubes
    Console.Write("No");
}

// Driver code
static void Main()
{
    int N = 124;

    // Function call to check if N
    // can be represented as
    // sum of two perfect cubes or not
    differenceOfTwoPerfectCubes(N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the number N
// can be represented as a difference
// between two perfect cubes or not
function differenceOfTwoPerfectCubes(N)
{
    // Stores the perfect cubes
    // of first X natural numbers
    var cubes = new Map();

    for (var i = 1;
         (i * i * i) - ((i - 1) * (i - 1) * (i - 1)) <= N;
         i++) {

        cubes.set(i * i * i, 1);
    }

    var ans = false;

    cubes.forEach((value, key) => {
         // Stores the first number
        var firstNumber = key;

        // Stores the second number
        var secondNumber = N + key;

        // Search the pair for the second
        // number to obtain difference N
        // from the Map
        if (cubes.has(secondNumber)) {
            document.write( "Yes");
            ans = true;
            return;
        }
    });

    if(ans)
    {
        return;
    }

    // If N cannot be represented
    // as difference between two
    // positive perfect cubes
    document.write( "No");
}

// Driver Code
var N = 124;
differenceOfTwoPerfectCubes(N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(∛N*log N)*
***辅助空间:** O(∛N)*