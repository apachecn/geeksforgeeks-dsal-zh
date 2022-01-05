# 将 A 或 B 加 N 正好 M 次就可以得到的所有数字打印出来

> 原文:[https://www . geeksforgeeks . org/print-all-numbers-可以通过将-a 或-b-n-精确地-m-次相加来获得/](https://www.geeksforgeeks.org/print-all-numbers-that-can-be-obtained-by-adding-a-or-b-to-n-exactly-m-times/)

给定四个整数 **N** 、 **M** 、 **A** 和 **B** ，任务是将 **A** 或 **B** 加到 **N** 正好 **M** 次可以得到的所有数字(*按递增顺序*)打印出来。

**示例:**

> **输入:** N = 5，M = 3，A = 4，B = 6
> **输出:** 17 19 21 23
> **解释:**
> 第一步:在 **N 上加 4 或 6**生成 9 和 11。
> 第二步:将 4 和 6 加到 **N** 生成 13，15，17。
> 第三步:将 4 和 6 加到 **N** 生成 17，19，21，23。
> 
> **输入:** N = 8，M = 2，A = 5，B = 10
> T3】输出: 18 23 28

**天真方法**:解决这个问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)。每一步只有两个选择，即要么加 **A** 要么加 **B** 。

按照以下步骤解决此问题:

*   初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，说**数字，**存储所有可以做的数字。
*   **基本情况**:如果 **M** 等于 **0，**那么唯一可能的数字就是 **N** 。
*   将 **A** 添加到 **N 后，**对**M–1**步进行递归调用。
*   将 **B** 添加到 **N 后，**对**M–1**步进行递归调用。
*   最后，[迭代设置](https://www.geeksforgeeks.org/iterate-over-a-set-in-python/) **数字**并打印所有数字。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly N times
void possibleNumbers(set<int>& numbers,
                     int N, int M,
                     int A, int B)
{
    // If number of steps is 0 and
    // only possible number is N
    if (M == 0) {
        numbers.insert(N);
        return;
    }

    // Add A to N and make a
    // recursive call for M - 1 steps
    possibleNumbers(numbers, N + A, M - 1, A, B);

    // Add B to N and make a
    // recursive call for M-1 steps.
    possibleNumbers(numbers, N + B, M - 1, A, B);
}

// Driver Code
int main()
{
    // Given Inputs
    int N = 5, M = 3, A = 4, B = 6;

    // Stores all possible numbers
    set<int> numbers;

    // Function call
    possibleNumbers(numbers, N, M, A, B);

    // Print all possible numbers
    for (int x : numbers) {
        cout << x << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class MyClass{

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly N times
static void possibleNumbers(Set<Integer> numbers, int N, int M, int A, int B)
{
    // If number of steps is 0 and
    // only possible number is N
    if (M == 0) {
        numbers.add(N);
        return;
    }

    // Add A to N and make a
    // recursive call for M - 1 steps
    possibleNumbers(numbers, N + A, M - 1, A, B);

    // Add B to N and make a
    // recursive call for M-1 steps.
    possibleNumbers(numbers, N + B, M - 1, A, B);
}

// Driver Code
  public static void main(String args[])
{

   // Given Inputs
    int N = 5, M = 3, A = 4, B = 6;

    // Stores all possible numbers
    Set<Integer> numbers = new HashSet<Integer>();

    // Function call
    possibleNumbers(numbers, N, M, A, B);

    // Print all possible numbers
    Iterator<Integer> i = numbers.iterator();
        while (i.hasNext())
            System.out.print(i.next()+ " " );
}}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all possible
# numbers that can be obtained
# by adding A or B to N exactly N times
def possibleNumbers(numbers, N, M, A, B):

    # If number of steps is 0 and
    # only possible number is N
    if (M == 0):
        numbers.add(N)
        return

    # Add A to N and make a
    # recursive call for M - 1 steps
    possibleNumbers(numbers, N + A,
                    M - 1, A, B)

    # Add B to N and make a
    # recursive call for M-1 steps.
    possibleNumbers(numbers, N + B,
                    M - 1, A, B)

# Driver Code
if __name__ == '__main__':

    # Given Inputs
    N = 5
    M = 3
    A = 4
    B = 6

    # Stores all possible numbers
    numbers = set()

    # Function call
    possibleNumbers(numbers, N, M, A, B)

    # Print all possible numbers
    for x in numbers:
        print(x, end = " ")

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class MyClass {

    // Function to find all possible
    // numbers that can be obtained
    // by adding A or B to N exactly N times
    static void possibleNumbers(HashSet<int> numbers, int N,
                                int M, int A, int B)
    {
        // If number of steps is 0 and
        // only possible number is N
        if (M == 0) {
            numbers.Add(N);
            return;
        }

        // Add A to N and make a
        // recursive call for M - 1 steps
        possibleNumbers(numbers, N + A, M - 1, A, B);

        // Add B to N and make a
        // recursive call for M-1 steps.
        possibleNumbers(numbers, N + B, M - 1, A, B);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given Inputs
        int N = 5, M = 3, A = 4, B = 6;

        // Stores all possible numbers
        HashSet<int> numbers = new HashSet<int>();

        // Function call
        possibleNumbers(numbers, N, M, A, B);

        // Print all possible numbers
        foreach(int i in numbers) Console.Write(i + " ");
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

        // Function to find all possible
        // numbers that can be obtained
        // by adding A or B to N exactly N times
        function possibleNumbers(numbers, N, M, A, B) {
            // If number of steps is 0 and
            // only possible number is N
            if (M == 0) {
                numbers.add(N);
                return;
            }

            // Add A to N and make a
            // recursive call for M - 1 steps
            possibleNumbers(numbers, N + A, M - 1, A, B);

            // Add B to N and make a
            // recursive call for M-1 steps.
            possibleNumbers(numbers, N + B, M - 1, A, B);
        }

        // Driver Code

        // Given Inputs
        var N = 5, M = 3, A = 4, B = 6;

        // Stores all possible numbers
        var numbers = new Set();

        // Function call
        possibleNumbers(numbers, N, M, A, B);

        // Print all possible numbers
        for (let x of numbers) {
            document.write(x+' ');
        }

    </script>
```

**Output:** 

```
17 19 21 23
```

***时间复杂度:**O(2<sup>M</sup>)*
***辅助空间:** O(M)*

**有效方法:**该问题具有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构属性](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。因此，可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来优化上述方法。

按照以下步骤解决此问题:

*   初始化一个向量，说 **dp[][]，**和一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，说**数字，**其中 **dp[i][j]** 存储在 **i** 步骤中数字 **j** 是否被访问。
*   **基本情况**:如果 **M** 等于 **0，**那么唯一可能的数字就是 **N** 。
*   如果之前在 **(M-1)** <sup>第</sup>步未获得 **(N+A)** ，则在将 **A** 添加到 **N 后，**递归调用**M–1**步并将**DP【M–1】【N+A】**标记为已访问。
*   如果之前在**(M–1)**<sup>第</sup>步未获得 **(N + B)** ，则在将 **B** 添加到 **N 后，**递归调用**M–1**步并将**DP【M–1】【N+B】**标记为已访问。
*   最后，[迭代设置](https://www.geeksforgeeks.org/iterate-over-a-set-in-python/) **数字**并打印所有数字。

下面是上述方法的实现

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
void possibleNumbers(int N, int M,
                     int A, int B)
{
    // For maintaining
    // increasing order
    if (A > B) {
        swap(A, B);
    }

    // Smallest number that
    // can be obtained
    int number = N + M * A;
    cout << number << " ";

    // If A and B are equal, then only
    // one number can be obtained, i.e. N + M*A
    if (A != B) {

        // For finding others numbers,
        // subtract A from number once
        // and add B to number once
        for (int i = 0; i < M; i++) {
            number = number - A + B;
            cout << number << " ";
        }
    }
}

// Driver Code
int main()
{
    // Given Input
    int N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
static void possibleNumbers(int N, int M,
                            int A, int B)
{

    // For maintaining
    // increasing order
    if (A > B)
    {
        int temp = A;
        A = B;
        B = temp;
    }

    // Smallest number that
    // can be obtained
    int number = N + M * A;
    System.out.print(number + " ");

    // If A and B are equal, then only
    // one number can be obtained, i.e. N + M*A
    if (A != B)
    {

        // For finding others numbers,
        // subtract A from number once
        // and add B to number once
        for(int i = 0; i < M; i++)
        {
            number = number - A + B;
            System.out.print(number + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);
}   
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all possible
# numbers that can be obtained
# by adding A or B to N exactly M times
def possibleNumbers(N, M, A, B):

    # For maintaining
    # increasing order
    if (A > B):
        temp = A
        A = B
        B = temp

    # Smallest number that
    # can be obtained
    number = N + M * A
    print(number, end = " ")

    # If A and B are equal, then only
    # one number can be obtained, i.e. N + M*A
    if (A != B):

        # For finding others numbers,
        # subtract A from number once
        # and add B to number once
        for i in range(M):
            number = number - A + B
            print(number,end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 5
    M = 3
    A = 4
    B = 6

    # Function Call
    possibleNumbers(N, M, A, B)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
static void possibleNumbers(int N, int M, int A, int B)
{

    // For maintaining
    // increasing order
    if (A > B)
    {
        int temp = A;
        A = B;
        B = temp;
    }

    // Smallest number that
    // can be obtained
    int number = N + M * A;
    Console.Write(number + " ");

    // If A and B are equal, then only
    // one number can be obtained, i.e. N + M*A
    if (A != B)
    {

        // For finding others numbers,
        // subtract A from number once
        // and add B to number once
        for(int i = 0; i < M; i++)
        {
            number = number - A + B;
            Console.Write(number + " ");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);
}   
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
function possibleNumbers(N,M,A,B)
{
    var i;
    // For maintaining
    // increasing order
    if (A > B) {
        var temp = A;
        A = B;
        B = temp;
    }

    // Smallest number that
    // can be obtained
    var number = N + M * A;
    document.write(number + " ");

    // If A and B are equal, then only
    // one number can be obtained, i.e. N + M*A
    if (A != B) {

        // For finding others numbers,
        // subtract A from number once
        // and add B to number once
        for (i = 0; i < M; i++) {
            number = number - A + B;
            document.write(number +" ");
        }
    }
}

// Driver Code
    // Given Input
    var N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);

</script>
```

**Output:** 

```
17 19 21 23
```

***时间复杂度:** O(M)*
***辅助空间:** O(M*10 <sup>5</sup> )*

**高效途径:**以上途径可以进一步优化[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决此问题:

*   如果 **A** 大于 **B** ，则[交换](https://www.geeksforgeeks.org/swap-in-cpp/) **A** 和 **B** 维持递增顺序。
*   初始化一个变量，说**号**为 **N + M * A，**即能达到的最小数，打印**号**。
*   如果 **A** 不等于 **B** ，则[使用变量 **i、**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M–1】**，并打印**号–A+B**。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
void possibleNumbers(int N, int M,
                     int A, int B)
{
    // For maintaining increasing order
    if (A > B) {
        swap(A, B);
    }

    // Smallest number that can be achieved
    int number = N + M * A;
    cout << number << " ";

    // If A and B are equal, the only number
    // that can be onbtained is N + M * A
    if (A != B) {

        // For finding other numbers,
        // subtract A from number 1 time
        // and add B to number 1 time
        for (int i = 0; i < M; i++) {

            number = number - A + B;
            cout << number << " ";
        }
    }
}

// Driver Code
int main()
{
    // Given Input
    int N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
static void possibleNumbers(int N, int M,
                     int A, int B)
{

    // For maintaining increasing order
    if (A > B)
    {
        int temp = A;
        A = B;
        B = temp;
    }

    // Smallest number that can be achieved
    int number = N + M * A;
    System.out.print(number +" ");

    // If A and B are equal, the only number
    // that can be onbtained is N + M * A
    if (A != B) {

        // For finding other numbers,
        // subtract A from number 1 time
        // and add B to number 1 time
        for (int i = 0; i < M; i++) {

            number = number - A + B;
            System.out.print(number +" ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find all possible
# numbers that can be obtained
# by adding A or B to N exactly M times
def possibleNumbers(N, M, A, B):

    # For maintaining increasing order
    if (A > B):
        temp = A
        A = B
        B = temp

    # Smallest number that can be achieved
    number = N + M * A
    print(number,end = " ")

    # If A and B are equal, the only number
    # that can be onbtained is N + M * A
    if (A != B):

        # For finding other numbers,
        # subtract A from number 1 time
        # and add B to number 1 time
        for i in range(M):
            number = number - A + B
            print(number,end= " ")

# Driver Code
if __name__ == '__main__':
    # Given Input
    N = 5
    M = 3
    A = 4
    B = 6

    # Function Call
    possibleNumbers(N, M, A, B)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
static void possibleNumbers(int N, int M,
                     int A, int B)
{

    // For maintaining increasing order
    if (A > B)
    {
        int temp = A;
        A = B;
        B = temp;
    }

    // Smallest number that can be achieved
    int number = N + M * A;
    Console.Write(number +" ");

    // If A and B are equal, the only number
    // that can be onbtained is N + M * A
    if (A != B) {

        // For finding other numbers,
        // subtract A from number 1 time
        // and add B to number 1 time
        for (int i = 0; i < M; i++) {

            number = number - A + B;
            Console.Write(number +" ");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to find all possible
// numbers that can be obtained
// by adding A or B to N exactly M times
function possibleNumbers( N,  M, A,  B)
{

    // For maintaining increasing order
    if (A > B)
    {
        var temp = A;
        A = B;
        B = temp;
    }

    // Smallest number that can be achieved
    var number = N + M * A;
    document.write(number +" ");

    // If A and B are equal, the only number
    // that can be onbtained is N + M * A
    if (A != B) {

        // For finding other numbers,
        // subtract A from number 1 time
        // and add B to number 1 time
        for (var i = 0; i < M; i++) {

            number = number - A + B;
            document.write(number +" ");
        }
    }
}

// Driver Code
// Given Input
    var N = 5, M = 3, A = 4, B = 6;

    // Function Call
    possibleNumbers(N, M, A, B);

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
17 19 21 23
```

***时间复杂度:**O(M)*
T5**辅助空间:** O(1)