# Q 的可能值，使得对于 R 的任何值，它们的乘积等于它们之和的 X 倍

> 原文:[https://www . geeksforgeeks . org/q 的可能值，即他们的产品的任何值等于他们的总和的 x 倍/](https://www.geeksforgeeks.org/possible-values-of-q-such-that-for-any-value-of-r-their-product-is-equal-to-x-times-their-sum/)

给定一个**整数 X** ，任务是为这对 **(Q，R)** 找到 **Q** 的可能值，使得它们的乘积等于 **X** 乘以它们的和，其中 *Q ≤ R 和 X < 10 <sup>7</sup>* 。将 **Q** 这些数值的总数连同数值一起打印出来。

**示例:**

> **输入:** X = 3
> **输出:**
> 2
> 4、6
> **说明:**
> 关于取 Q = 4 和 R = 12，
> LHS = 12×4 = 48
> RHS = 3(12+4)= 3×16 = 48 = LHS
> 同样，对于 Q = 6 和 R = 6，方程也成立。
> LHS = 6 x 6 = 36
> RHS = 3(6+6)= 3 x 12 = 36 = LHS
> 
> **输入:** X = 16
> **输出:**
> 5
> 17、18、20、24、32
> **说明:**
> 如果 Q = 17 且 R = 272，
> LHS = 17 X 272 = 4624
> RHS = 16(17+272)= 16(289)= 4624 = LHS。
> 同样，输出中给出的所有其他 Q 值都存在一个 R 值。

**做法:**思路是理解问题形成方程，即**(Q×R)= X(Q+R)。**

*   想法是从 1 迭代到 X，并检查每一个 if**(((X+I)* X)% I)=****0**。
*   初始化一个结果向量，从 1 开始迭代 X 的所有值。
*   检查上述条件是否成立。如果是，则在向量中推数值 **X+i** 。
*   让我们打破这个等式，以便更清楚地理解它，

> 给定的表达式是 **(Q x R) = X(Q + R)**
> 在简化后我们得到，
> 
> = > QR–qx = rx
> or，QR–rx = qx
> or，r = qx/(q–x)

*   因此，观察 **(X+i)** 是 Q 的可能值， **(X+i)*X** 是 r 的可能值

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible values of Q
void values_of_Q(int X)
{
    // Vector initialization
    // to store all numbers
    // satisfying the given condition
    vector<int> val_Q;

    // Iterate for all the values of X
    for (int i = 1; i <= X; i++) {

        // Check if condition satisfied
        // then push the number
        if ((((X + i) * X)) % i == 0) {

            // Possible value of Q
            val_Q.push_back(X + i);
        }
    }

    cout << val_Q.size() << endl;

    // Print all the numbers
    for (int i = 0; i < val_Q.size(); i++) {
        cout << val_Q[i] << " ";
    }
}

// Driver code
int main()
{
    int X = 3;

    values_of_Q(X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find all possible values of Q
static void values_of_Q(int X)
{
    // Vector initialization
    // to store all numbers
    // satisfying the given condition
    ArrayList<Integer> val_Q = new ArrayList<Integer>();

    // Iterate for all the values of X
    for (int i = 1; i <= X; i++)
    {

        // Check if condition satisfied
        // then push the number
        if ((((X + i) * X)) % i == 0)
        {

            // Possible value of Q
            val_Q.add(X + i);
        }
    }

    System.out.println(val_Q.size());

    // Print all the numbers
    for (int i = 0; i < val_Q.size(); i++)
    {
        System.out.print(val_Q.get(i)+" ");
    }
}

// Driver code
public static void main(String[] args)
{
    int X = 3;

    values_of_Q(X);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all possible values of Q
def values_of_Q(X):

    # Vector initialization
    # to store all numbers
    # satisfying the given condition
    val_Q = []

    # Iterate for all the values of X
    for i in range(1, X + 1):

        # Check if condition satisfied
        # then push the number
        if ((((X + i) * X)) % i == 0):

            # Possible value of Q
            val_Q.append(X + i)

    print(len(val_Q))

    # Print all the numbers
    for i in range(len(val_Q)):
        print(val_Q[i], end = " ")

# Driver Code       
X = 3

values_of_Q(X)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find all possible
// values of Q
static void values_of_Q(int X)
{

    // List initialization
    // to store all numbers
    // satisfying the given condition
    List<int> val_Q = new List<int>();

    // Iterate for all the values of X
    for(int i = 1; i <= X; i++)
    {

        // Check if condition satisfied
        // then push the number
        if ((((X + i) * X)) % i == 0)
        {

            // Possible value of Q
            val_Q.Add(X + i);
        }
    }

    Console.WriteLine(val_Q.Count);

    // Print all the numbers
    for(int i = 0; i < val_Q.Count; i++)
    {
        Console.Write(val_Q[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int X = 3;

    values_of_Q(X);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find all possible values of Q
    function values_of_Q(X)
    {

        // Vector initialization
        // to store all numbers
        // satisfying the given condition
        let val_Q = [];

        // Iterate for all the values of X
        for (let i = 1; i <= X; i++)
        {

            // Check if condition satisfied
            // then push the number
            if ((((X + i) * X)) % i == 0)
            {

                // Possible value of Q
                val_Q.push(X + i);
            }
        }

        document.write(val_Q.length + "</br>");

        // Print all the numbers
        for (let i = 0; i < val_Q.length; i++) {
            document.write(val_Q[i] + " ");
        }
    }

    let X = 3;
    values_of_Q(X);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
2
4 6
```

**时间复杂度:** O(N)

**辅助空间:** O(X)