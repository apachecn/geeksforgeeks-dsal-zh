# 对不超过 N 的整数进行计数，该整数至少等于任何超过 1 的整数的 2 次幂

> 原文:[https://www . geesforgeks . org/count-整数-向上-n-等于-至少-任意整数的 2 次幂-超过-1/](https://www.geeksforgeeks.org/count-integers-up-to-n-that-are-equal-to-at-least-2nd-power-of-any-integer-exceeding-1/)

给定一个正整数 **N** ，任务是从可以表示为**a<sup>b</sup>T7】的范围**【1，N】**中计算整数个数，其中 **a** 和 **b** 是大于 **1** 的整数。**

**示例:**

> **输入:** N = 6
> **输出:** 1
> **解释:**
> 只有范围【1，6】中的这样的整数才是 4 (= 2 <sup>2</sup> )。
> 因此，要求计数为 1。
> 
> **输入:**N = 10
> T3】输出: 3

**方法:**给定的问题可以通过计算所有可能的元素对 **(a，b)** 来解决，使得**a<sup>b</sup>T7】最多为**N**。按照以下步骤解决问题:**

*   初始化一个 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 来存储**a<sup>b</sup>T5】的所有可能值，最多为**N**。**
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，√N】**，对于 **a** 的每个值，插入值**最多为 N 的 **a <sup>b</sup>** 的所有可能值，**其中 b 位于范围**【1，N】**内。
*   完成上述步骤后，打印 HashSet 的[尺寸作为整数的合成计数。](https://www.geeksforgeeks.org/hashset-size-method-in-java/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the integers
// up to N that can be represented
// as a ^ b, where a &b > 1
void printNumberOfPairs(int N)
{

    // Initialize a HashSet
    unordered_set<int> st;

    // Iterating over the range
    // [2, sqrt(N)]
    for(int i = 2; i * i <= N; i++)
    {
        int x = i;

        // Generate all possible
        // power of x
        while (x <= N)
        {

            // Multiply x by i
            x *= i;

            // If the generated number
            // lies in the range [1, N]
            // then insert it in HashSet
            if (x <= N)
            {
                st.insert(x);
            }
        }
    }

    // Print the total count
    cout << st.size();
}

// Driver code
int main()
{
    int N = 10000;
    printNumberOfPairs(N);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.HashSet;

public class GFG {

    // Function to count the integers
    // up to N that can be represented
    // as a ^ b, where a &b > 1
    static void printNumberOfPairs(int N)
    {
        // Initialize a HashSet
        HashSet<Integer> st
            = new HashSet<Integer>();

        // Iterating over the range
        // [2, sqrt(N)]
        for (int i = 2; i * i <= N; i++) {

            int x = i;

            // Generate all possible
            // power of x
            while (x <= N) {

                // Multiply x by i
                x *= i;

                // If the generated number
                // lies in the range [1, N]
                // then insert it in HashSet
                if (x <= N) {
                    st.add(x);
                }
            }
        }

        // Print the total count
        System.out.println(st.size());
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 10000;
        printNumberOfPairs(N);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import sqrt

# Function to count the integers
# up to N that can be represented
# as a ^ b, where a &b > 1
def printNumberOfPairs(N):

    # Initialize a HashSet
    st = set()

    # Iterating over the range
    # [2, sqrt(N)]
    for i in range(2, int(sqrt(N)) + 1, 1):
        x = i

        # Generate all possible
        # power of x
        while(x <= N):

            # Multiply x by i
            x *= i

            # If the generated number
            # lies in the range [1, N]
            # then insert it in HashSet
            if (x <= N):
                st.add(x)

    # Print the total count
    print(len(st))

# Driver code
if __name__ == '__main__':
    N = 10000
    printNumberOfPairs(N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the integers
// up to N that can be represented
// as a ^ b, where a &b > 1
static void printNumberOfPairs(int N)
{

    // Initialize a HashSet
    HashSet<int> st = new HashSet<int>();

    // Iterating over the range
    // [2, sqrt(N)]
    for(int i = 2; i * i <= N; i++)
    {
        int x = i;

        // Generate all possible
        // power of x
        while (x <= N)
        {

            // Multiply x by i
            x *= i;

            // If the generated number
            // lies in the range [1, N]
            // then insert it in HashSet
            if (x <= N)
            {
                st.Add(x);
            }
        }
    }

    // Print the total count
    Console.WriteLine(st.Count);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 10000;
    printNumberOfPairs(N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the integers
// up to N that can be represented
// as a ^ b, where a &b > 1
function printNumberOfPairs( N)
{
    // Initialize a HashSet
    var st = new Set();

    // Iterating over the range
    // [2, sqrt(N)]
    for (let i = 2; i * i <= N; i++) {

        let x = i;

        // Generate all possible
        // power of x
        while (x <= N) {

            // Multiply x by i
            x *= i;

            // If the generated number
            // lies in the range [1, N]
            // then insert it in HashSet
            if (x <= N) {
                st.add(x);
            }
        }
    }

    // Print the total count
    document.write(st.size);
}

// Driver Code

let N = 10000;
printNumberOfPairs(N);

</script>
```

**Output:** 

```
124
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*