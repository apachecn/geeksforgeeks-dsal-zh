# 将 N 个自然数分成两组，其和的 GCD 大于 1

> 原文:[https://www . geeksforgeeks . org/split-n-自然数-分成两组-它们的总和的 gcd 大于-1/](https://www.geeksforgeeks.org/split-n-natural-numbers-into-two-sets-having-gcd-of-their-sums-greater-than-1/)

给定一个整数 **N** ，任务是创建从 **1 到 N** 的两组不同元素，使得它们各自和的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 大于 1。打印相应的器械包。如果无法进行这种拆分，请打印-1。

**示例:**

> **输入:** N = 5
> **输出:**
> 2 4
> 1 3 5
> **解释:**
> GCD(Sum({2，4})、Sum({1，3，5}) = GCD(6，9) = 3
> 
> **输入:** N = 2
> **输出:** -1
> **说明:**
> 对于 N = 2，不可能分成两个其和的 GCD 大于 1 的集合。

**方法 1:** 一种简单的方法是将 N 以内的所有偶数拆分为一个集合，将所有奇数拆分为另一个集合。

下面的代码是该方法的实现:

## C++

```
// C++ program to split N natural numbers
// into two sets having GCD
// of their sums greater than 1

#include <bits/stdc++.h>
using namespace std;

// Function to create
// and print the two sets
void createSets(int N)
{
    // No such split
    // possible for N <= 2
    if (N <= 2) {
        cout << "-1" << endl;
        return;
    }

    // Print the first set
    // consisting of even elements
    for (int i = 2; i <= N; i += 2)
        cout << i << " ";
    cout << "\n";
    // Print the second set
    // consisting of odd ones
    for (int i = 1; i <= N; i += 2) {
        cout << i << " ";
    }
}
// Driver Code
int main()
{

    int N = 6;
    createSets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split N natural numbers
// into two sets having GCD
// of their sums greater than 1
class GFG{

// Function to create
// and print the two sets
static void createSets(int N)
{
    // No such split
    // possible for N <= 2
    if (N <= 2)
    {
        System.out.println("-1" );
        return;
    }

    // Print the first set
    // consisting of even elements
    for (int i = 2; i <= N; i += 2)
        System.out.print(i + " ");
    System.out.print("\n") ;

    // Print the second set
    // consisting of odd ones
    for (int i = 1; i <= N; i += 2)
    {
        System.out.print(i + " ");
    }
}
// Driver Code
public static void main(String[] args)
{

    int N = 6;
    createSets(N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to split N natural numbers
# into two sets having GCD
# of their sums greater than 1

# Function to create
# and print the two sets
def createSets(N):

    # No such split
    # possible for N <= 2
    if (N <= 2):
        print("-1");
        return;

    # Print the first set
    # consisting of even elements
    for i in range(2, N + 1, 2):
        print(i, end=" ");
    print("");

    # Print the second set
    # consisting of odd ones
    for i in range(1, N + 1, 2):
        print(i, end = " ");

# Driver Code
if __name__ == '__main__':
    N = 6;
    createSets(N);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to split N natural numbers
// into two sets having GCD
// of their sums greater than 1
using System;
class GFG{

// Function to create
// and print the two sets
static void createSets(int N)
{
    // No such split
    // possible for N <= 2
    if (N <= 2)
    {
        Console.WriteLine("-1" );
        return;
    }

    // Print the first set
    // consisting of even elements
    for (int i = 2; i <= N; i += 2)
        Console.Write(i + " ");
    Console.Write("\n") ;

    // Print the second set
    // consisting of odd ones
    for (int i = 1; i <= N; i += 2)
    {
        Console.Write(i + " ");
    }
}
// Driver Code
public static void Main(String[] args)
{

    int N = 6;
    createSets(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to split N natural numbers
    // into two sets having GCD
    // of their sums greater than 1

    // Function to create
    // and print the two sets
    function createSets(N)
    {
        // No such split
        // possible for N <= 2
        if (N <= 2) {
            document.write("-1");
            return;
        }

        // Print the first set
        // consisting of even elements
        for (let i = 2; i <= N; i += 2)
            document.write(i + " ");
        document.write("</br>");
        // Print the second set
        // consisting of odd ones
        for (let i = 1; i <= N; i += 2) {
            document.write(i + " ");
        }
    }

    let N = 6;
    createSets(N);

</script>
```

**Output:** 

```
2 4 6 
1 3 5
```

时间复杂度:0(N)

辅助空间:0(1)

**方法 2:** 这种方法可以根据 N 分为 2 种情况:

1.  **如果 N 为奇数:**
    *   本例中 N 个自然数之和可被 **(N+1)/2** 整除。
    *   所以我们只需要将 **(N+1)/2 放入第一套**中，剩余的数字放入第二套。
    *   这将自动使其总和的 GCD 大于 1。
2.  **如果 N 为偶数:**
    *   在这种情况下，N 个自然数的和可以被 **N/2** 整除。
    *   因此我们只需要将 **N/2 放入第一套**中，剩余的数字放入第二套。
    *   这将自动使其总和的 GCD 大于 1。

下面是上述方法的实现:

## C++

```
// C++ program to split N natural numbers
// into two sets having GCD
// of their sums greater than 1

#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to create
// and print the two sets
void createSets(ll n)
{
    // For n <= 2 such sets
    // can never be formed
    if (n <= 2) {
        cout << "-1";
        return;
    }

    else {

        // Check if N is even or odd
        // and store the element
        // which divides the sum of N
        // natural numbers accordingly
        ll x = (n % 2 == 0) ? (n / 2)
                            : ((n + 1) / 2);

        // First set
        cout << x << endl;

        // Print elements of second set
        for (ll i = 1; i <= n; i++) {

            if (i == x)
                continue;

            cout << i << " ";
        }
    }
    return;
}

// Driver code
int main()
{
    ll N = 7;

    createSets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split N natural numbers
// into two sets having GCD
// of their sums greater than 1
class GFG{

// Function to create
// and print the two sets
static void createSets(long n)
{

    // For n <= 2 such sets
    // can never be formed
    if (n <= 2)
    {
        System.out.print("-1");
        return;
    }
    else
    {

        // Check if N is even or odd
        // and store the element
        // which divides the sum of N
        // natural numbers accordingly
        long x = (n % 2 == 0) ? (n / 2) :
                          ((n + 1) / 2);

        // First set
        System.out.print(x + "\n");

        // Print elements of second set
        for(int i = 1; i <= n; i++)
        {
            if (i == x)
                continue;

            System.out.print(i + " ");
        }
    }
    return;
}

// Driver code
public static void main(String[] args)
{
    long N = 7;

    createSets(N);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to split N natural numbers
# into two sets having GCD
# of their sums greater than 1

# Function to create
# and print the two sets
def createSets(n):

    # For n <= 2 such sets
    # can never be formed
    if (n <= 2):
        print("-1");
        return;
    else:

        # Check if N is even or odd
        # and store the element
        # which divides the sum of N
        # natural numbers accordingly
        x = (n // 2) if(n % 2 == 0) else (
            (n + 1) // 2);

        # First set
        print(x, " ");

        # Print elements of second set
        for i in range(1, n + 1):
            if (i == x):
                continue;

            print(i, end = " ");

    return;

# Driver code
if __name__ == '__main__':

    N = 7;

    createSets(N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to split N natural numbers
// into two sets having GCD
// of their sums greater than 1
using System;
class GFG{

// Function to create
// and print the two sets
static void createSets(long n)
{

    // For n <= 2 such sets
    // can never be formed
    if (n <= 2)
    {
        Console.Write("-1");
        return;
    }
    else
    {

        // Check if N is even or odd
        // and store the element
        // which divides the sum of N
        // natural numbers accordingly
        long x = (n % 2 == 0) ? (n / 2) :
                          ((n + 1) / 2);

        // First set
        Console.Write(x + "\n");

        // Print elements of second set
        for(int i = 1; i <= n; i++)
        {
            if (i == x)
                continue;

            Console.Write(i + " ");
        }
    }
    return;
}

// Driver code
public static void Main(String[] args)
{
    long N = 7;

    createSets(N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
    // Javascript program to split N natural numbers
    // into two sets having GCD
    // of their sums greater than 1

    // Function to create
    // and print the two sets
    function createSets(n)
    {

        // For n <= 2 such sets
        // can never be formed
        if (n <= 2) {
            document.write("-1");
            return;
        }

        else {

            // Check if N is even or odd
            // and store the element
            // which divides the sum of N
            // natural numbers accordingly
            let x = (n % 2 == 0) ? (n / 2) : ((n + 1) / 2);

            // First set
            document.write(x + "</br>");

            // Print elements of second set
            for (let i = 1; i <= n; i++)
            {
                if (i == x)
                    continue;
                document.write(i + " ");
            }
        }
        return;
    }

// Driver code
    let N = 7;
    createSets(N);

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
4
1 2 3 5 6 7
```

**时间复杂度:***O(N)*
T5】辅助空间复杂度: *O(1)*