# 通过重复将余数加到 S 上来检查一个数 S 是否能被 D 整除

> 原文:[https://www . geesforgeks . org/check-if-a-number-s-可被 d 整除-通过重复将余数加到 s/](https://www.geeksforgeeks.org/check-if-a-number-s-can-be-made-divisible-by-d-by-repeatedly-adding-the-remainder-to-s/)

给定两个整数 **S** 和 **D** ，任务是通过重复将 **S** 模 **D** 加到 **S** 来检查整数 **S** 是否能被 **D** 整除。如果 **S** 被 **D** 整除，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** S = 3，D = 6
> **输出:**是
> **解释:**
> 假设第 i <sup>个</sup>区间 mod D 上的值为 V(i)，即**V(I)=(V(I–1)+V(I–1)% D)% D**，则
> V(0) = S % D = 3
> V(1) = (V 因此，打印“是”。
> 
> **输入:** S = 1，D = 5
> T3】输出:否

**方法:**给定的问题可以用[鸽子洞原理](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)解决。按照以下步骤解决问题:

*   根据原理，如果与 **D** 取模的数字超过 **D** ，则**(【0，D–1】)**范围内至少有一个值会出现两次。
*   迭代 **(D + 1)** 次，将 **V(i)** 的值存储在 [HashMap](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 中，如果有重复，则退出循环。
*   当余数值为 **0** 、[退出循环](https://www.geeksforgeeks.org/break-statement-cc/)时，存在一个边缘情况，在这种情况下，这也是一个可除的情况，但我们的逻辑将其视为一个循环。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if S is divisible
// by D while changing S to (S + S%D)
string isDivisibleByDivisor(int S, int D)
{
    // V(0) = S % D
    S %= D;

    // Stores the encountered values
    unordered_set<int> hashMap;
    hashMap.insert(S);

    for (int i = 0; i <= D; i++) {

        // V(i) = (V(i-1) + V(i-1)%D) % D
        S += (S % D);
        S %= D;

        // Check if the value has
        // already been encountered
        if (hashMap.find(S)
            != hashMap.end()) {

            // Edge Case
            if (S == 0) {
                return "Yes";
            }
            return "No";
        }

        // Otherwise, insert it into
        // the hashmap
        else
            hashMap.insert(S);
    }
    return "Yes";
}

// Driver Code
int main()
{
    int S = 3, D = 6;
    cout << isDivisibleByDivisor(S, D);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if S is divisible
// by D while changing S to (S + S%D)
static String isDivisibleByDivisor(int S, int D)
{

    // V(0) = S % D
    S %= D;

    // Stores the encountered values
    Set<Integer> hashMap = new HashSet<>();
    hashMap.add(S);

    for(int i = 0; i <= D; i++)
    {

        // V(i) = (V(i-1) + V(i-1)%D) % D
        S += (S % D);
        S %= D;

        // Check if the value has
        // already been encountered
        if (hashMap.contains(S))
        {

            // Edge Case
            if (S == 0)
            {
                return "Yes";
            }
            return "No";
        }

        // Otherwise, insert it into
        // the hashmap
        else
            hashMap.add(S);
    }
    return "Yes";
}

// Driver code
public static void main(String[] args)
{
    int S = 3, D = 6;

    System.out.println(isDivisibleByDivisor(S, D));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if S is divisible
# by D while changing S to (S + S%D)
def isDivisibleByDivisor(S, D):
    # V(0) = S % D
    S %= D

    # Stores the encountered values
    hashMap = set()
    hashMap.add(S)

    for i in range(D+1):

        # V(i) = (V(i-1) + V(i-1)%D) % D
        S += (S % D)
        S %= D

        # Check if the value has
        # already been encountered
        if (S in hashMap):

            # Edge Case
            if (S == 0):
                return "Yes"
            return "No"

        # Otherwise, insert it into
        # the hashmap
        else:
            hashMap.add(S)
    return "Yes"

# Driver Code
if __name__ == '__main__':
    S = 3
    D = 6
    print(isDivisibleByDivisor(S, D))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG {

// Function to check if S is divisible
// by D while changing S to (S + S%D)
static string isDivisibleByDivisor(int S, int D)
{
    // V(0) = S % D
    S %= D;

    // Stores the encountered values
    List<int> hashMap = new List<int>();;
    hashMap.Add(S);

    for (int i = 0; i <= D; i++) {

        // V(i) = (V(i-1) + V(i-1)%D) % D
        S += (S % D);
        S %= D;

        // Check if the value has
        // already been encountered
        if (hashMap.Contains(S)) {

            // Edge Case
            if (S == 0) {
                return "Yes";
            }
            return "No";
        }

        // Otherwise, insert it into
        // the hashmap
        else
            hashMap.Add(S);
    }
    return "Yes";
}

    // Driver Code
    static void Main()
    {
        int S = 3, D = 6;
        Console.Write( isDivisibleByDivisor(S, D));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to check if S is divisible
      // by D while changing S to (S + S%D)
      function isDivisibleByDivisor(S, D)
      {

        // V(0) = S % D
        S %= D;

        // Stores the encountered values
        var hashMap = [];
        hashMap.push(S);

        for (var i = 0; i <= D; i++)
        {

          // V(i) = (V(i-1) + V(i-1)%D) % D
          S += S % D;
          S %= D;

          // Check if the value has
          // already been encountered
          if (hashMap.includes(S)) {
            // Edge Case
            if (S == 0) {
              return "Yes";
            }
            return "No";
          }

          // Otherwise, insert it into
          // the hashmap
          else hashMap.push(S);
        }
        return "Yes";
      }

      // Driver Code
      var S = 3,
        D = 6;
      document.write(isDivisibleByDivisor(S, D));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(D)*
T5**辅助空间:** O(D)