# A、B、C 的倍数集合中的第 k 个数

> 原文:[https://www . geeksforgeeks . org/kth-从 a-B-和-c 的倍数集合中选择数字/](https://www.geeksforgeeks.org/kth-number-from-the-set-of-multiples-of-numbers-a-b-and-c/)

给定四个整数 **A** 、 **B** 、 **C** 和 **K** 。假设 **A** 、 **B** 、 **C** 的所有倍数按照排序顺序存储在一个集合中，没有重复，现在的任务是从那个集合中找到 **K <sup>第</sup>** 个元素。
**例:**

> **输入:** A = 1，B = 2，C = 3，K = 4
> **输出:** 4
> 所需设置为{1，2，3，4，5，…}
> **输入:** A = 2，B = 4，C = 5，K = 5
> **输出:** 8

**进场:** [二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以在 **K** 这里使用，找到套内的 **K <sup>th</sup>** 号。如果是 **A** 的倍数，我们来找 **K <sup>第</sup>** 号。
将二分搜索法涂抹在 **A** 的倍数上，从 **1** 到 **K** (因为可能会有最大 **K** 的 **A** 的倍数，在所需的集合中找到 **K <sup>th</sup>** 号)。
现在，对于一个值 **mid** ，所需的 **A** 的倍数将是 **A * mid** **(说 X)** 。现在的任务是找出这是否是 **K <sup>第</sup>号**所需要的套号。可以找到如下所示:

> 求 **A** 的倍数小于 **X** 说**A1**T6】求 **B** 小于 **X** 说**B1**T13】求 **C** 小于 **X** 说**C1**T20】求 **lcm(A， B)** (可被 A 和 B 整除)小于 **X** 说 **AB1**
> 求 **lcm(B，C)** 的倍数小于 **X** 说**BC1**T34】求 **lcm(C，A)** 的倍数小于 **X** 说 **CA1 【T40**

现在，根据[包含和排除](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/)的原则，小于 **X** 的所需集合中的数字计数将为**A1+B1+C1–AB1–BC1–CA1+ABC1**。
如果**计数= K–1**，则 **X** 为必选项。
如果**计数<K–1**，则该倍数大于 **X** 意味着设置**开始=中间+ 1** 否则设置**结束=中间–1**。
对 **B** 执行相同的步骤(如果 **K <sup>th</sup>** 号不是 **A** 的倍数)，然后对 **C** 执行相同的步骤。
既然 **K <sup>th</sup>** 号必然是**A****B**或者 **C** 的倍数，这三个二分搜索法肯定会传回结果。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return the
// GCD of A and B
int gcd(int A, int B)
{
    if (B == 0)
        return A;
    return gcd(B, A % B);
}

// Function to return the
// LCM of A and B
int lcm(int A, int B)
{
    return (A * B) / gcd(A, B);
}

// Function to return the Kth element from
// the required set if it a multiple of A
int checkA(int A, int B, int C, int K)
{
    // Start and End for Binary Search
    int start = 1;
    int end = K;

    // If no answer found return -1
    int ans = -1;

    while (start <= end) {
        int mid = (start + end) / 2;
        int value = A * mid;

        int divA = mid - 1;
        int divB = (value % B == 0) ? value / B - 1
                                    : value / B;
        int divC = (value % C == 0) ? value / C - 1
                                    : value / C;
        int divAB = (value % lcm(A, B) == 0)
                        ? value / lcm(A, B) - 1
                        : value / lcm(A, B);
        int divBC = (value % lcm(C, B) == 0)
                        ? value / lcm(C, B) - 1
                        : value / lcm(C, B);
        int divAC = (value % lcm(A, C) == 0)
                        ? value / lcm(A, C) - 1
                        : value / lcm(A, C);
        int divABC = (value % lcm(A, lcm(B, C)) == 0)
                         ? value / lcm(A, lcm(B, C)) - 1
                         : value / lcm(A, lcm(B, C));

        // Inclusion and Exclusion
        int elem = divA + divB + divC - divAC
                   - divBC - divAB + divABC;
        if (elem == (K - 1)) {
            ans = value;
            break;
        }

        // Multiple should be smaller
        else if (elem > (K - 1)) {
            end = mid - 1;
        }

        // Multiple should be bigger
        else {
            start = mid + 1;
        }
    }

    return ans;
}

// Function to return the Kth element from
// the required set if it a multiple of B
int checkB(int A, int B, int C, int K)
{
    // Start and End for Binary Search
    int start = 1;
    int end = K;

    // If no answer found return -1
    int ans = -1;

    while (start <= end) {
        int mid = (start + end) / 2;
        int value = B * mid;

        int divB = mid - 1;
        int divA = (value % A == 0) ? value / A - 1
                                    : value / A;
        int divC = (value % C == 0) ? value / C - 1
                                    : value / C;
        int divAB = (value % lcm(A, B) == 0)
                        ? value / lcm(A, B) - 1
                        : value / lcm(A, B);
        int divBC = (value % lcm(C, B) == 0)
                        ? value / lcm(C, B) - 1
                        : value / lcm(C, B);
        int divAC = (value % lcm(A, C) == 0)
                        ? value / lcm(A, C) - 1
                        : value / lcm(A, C);
        int divABC = (value % lcm(A, lcm(B, C)) == 0)
                         ? value / lcm(A, lcm(B, C)) - 1
                         : value / lcm(A, lcm(B, C));

        // Inclusion and Exclusion
        int elem = divA + divB + divC - divAC
                   - divBC - divAB + divABC;
        if (elem == (K - 1)) {
            ans = value;
            break;
        }

        // Multiple should be smaller
        else if (elem > (K - 1)) {
            end = mid - 1;
        }

        // Multiple should be bigger
        else {
            start = mid + 1;
        }
    }

    return ans;
}

// Function to return the Kth element from
// the required set if it a multiple of C
int checkC(int A, int B, int C, int K)
{
    // Start and End for Binary Search
    int start = 1;
    int end = K;

    // If no answer found return -1
    int ans = -1;

    while (start <= end) {
        int mid = (start + end) / 2;
        int value = C * mid;

        int divC = mid - 1;
        int divB = (value % B == 0) ? value / B - 1
                                    : value / B;
        int divA = (value % A == 0) ? value / A - 1
                                    : value / A;
        int divAB = (value % lcm(A, B) == 0)
                        ? value / lcm(A, B) - 1
                        : value / lcm(A, B);
        int divBC = (value % lcm(C, B) == 0)
                        ? value / lcm(C, B) - 1
                        : value / lcm(C, B);
        int divAC = (value % lcm(A, C) == 0)
                        ? value / lcm(A, C) - 1
                        : value / lcm(A, C);
        int divABC = (value % lcm(A, lcm(B, C)) == 0)
                         ? value / lcm(A, lcm(B, C)) - 1
                         : value / lcm(A, lcm(B, C));

        // Inclusion and Exclusion
        int elem = divA + divB + divC - divAC
                   - divBC - divAB + divABC;
        if (elem == (K - 1)) {
            ans = value;
            break;
        }

        // Multiple should be smaller
        else if (elem > (K - 1)) {
            end = mid - 1;
        }

        // Multiple should be bigger
        else {
            start = mid + 1;
        }
    }

    return ans;
}

// Function to return the Kth element from
// the set of multiples of A, B and C
int findKthMultiple(int A, int B, int C, int K)
{

    // Apply binary search on the multiples of A
    int res = checkA(A, B, C, K);

    // If the required element is not a
    // multiple of A then the multiples
    // of B and C need to be checked
    if (res == -1)
        res = checkB(A, B, C, K);

    // If the required element is neither
    // a multiple of A nor a multiple
    // of B then the multiples of C
    // need to be checked
    if (res == -1)
        res = checkC(A, B, C, K);

    return res;
}

// Driver code
int main()
{
    int A = 2, B = 4, C = 5, K = 5;

    cout << findKthMultiple(A, B, C, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the
    // GCD of A and B
    static int gcd(int A, int B)
    {
        if (B == 0)
            return A;
        return gcd(B, A % B);
    }

    // Function to return the
    // LCM of A and B
    static int lcm(int A, int B)
    {
        return (A * B) / gcd(A, B);
    }

    // Function to return the Kth element from
    // the required set if it a multiple of A
    static int checkA(int A, int B, int C, int K)
    {
        // Start and End for Binary Search
        int start = 1;
        int end = K;

        // If no answer found return -1
        int ans = -1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int value = A * mid;

            int divA = mid - 1;
            int divB = (value % B == 0) ? value / B - 1
                                        : value / B;
            int divC = (value % C == 0) ? value / C - 1
                                        : value / C;
            int divAB = (value % lcm(A, B) == 0) ?
                           value / lcm(A, B) - 1 :
                           value / lcm(A, B);
            int divBC = (value % lcm(C, B) == 0) ?
                           value / lcm(C, B) - 1 :
                           value / lcm(C, B);
            int divAC = (value % lcm(A, C) == 0) ?
                           value / lcm(A, C) - 1 :
                           value / lcm(A, C);
            int divABC = (value % lcm(A, lcm(B, C)) == 0) ?
                            value / lcm(A, lcm(B, C)) - 1 :
                            value / lcm(A, lcm(B, C));

            // Inclusion and Exclusion
            int elem = divA + divB + divC - divAC -
                              divBC - divAB + divABC;
            if (elem == (K - 1))
            {
                ans = value;
                break;
            }

            // Multiple should be smaller
            else if (elem > (K - 1))
            {
                end = mid - 1;
            }

            // Multiple should be bigger
            else
            {
                start = mid + 1;
            }
        }
        return ans;
    }

    // Function to return the Kth element from
    // the required set if it a multiple of B
    static int checkB(int A, int B, int C, int K)
    {
        // Start and End for Binary Search
        int start = 1;
        int end = K;

        // If no answer found return -1
        int ans = -1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int value = B * mid;

            int divB = mid - 1;
            int divA = (value % A == 0) ? value / A - 1
                                        : value / A;
            int divC = (value % C == 0) ? value / C - 1
                                        : value / C;
            int divAB = (value % lcm(A, B) == 0) ?
                           value / lcm(A, B) - 1 :
                           value / lcm(A, B);
            int divBC = (value % lcm(C, B) == 0) ?
                           value / lcm(C, B) - 1 :
                           value / lcm(C, B);
            int divAC = (value % lcm(A, C) == 0) ?
                           value / lcm(A, C) - 1 :
                           value / lcm(A, C);
            int divABC = (value % lcm(A, lcm(B, C)) == 0) ?
                            value / lcm(A, lcm(B, C)) - 1 :
                            value / lcm(A, lcm(B, C));

            // Inclusion and Exclusion
            int elem = divA + divB + divC - divAC
                    - divBC - divAB + divABC;
            if (elem == (K - 1))
            {
                ans = value;
                break;
            }

            // Multiple should be smaller
            else if (elem > (K - 1))
            {
                end = mid - 1;
            }

            // Multiple should be bigger
            else
            {
                start = mid + 1;
            }
        }
        return ans;
    }

    // Function to return the Kth element from
    // the required set if it a multiple of C
    static int checkC(int A, int B, int C, int K)
    {
        // Start and End for Binary Search
        int start = 1;
        int end = K;

        // If no answer found return -1
        int ans = -1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int value = C * mid;

            int divC = mid - 1;
            int divB = (value % B == 0) ? value / B - 1
                                        : value / B;
            int divA = (value % A == 0) ? value / A - 1
                                        : value / A;
            int divAB = (value % lcm(A, B) == 0) ?
                           value / lcm(A, B) - 1 :
                           value / lcm(A, B);
            int divBC = (value % lcm(C, B) == 0) ?
                           value / lcm(C, B) - 1 :
                           value / lcm(C, B);
            int divAC = (value % lcm(A, C) == 0) ?
                           value / lcm(A, C) - 1 :
                           value / lcm(A, C);
            int divABC = (value % lcm(A, lcm(B, C)) == 0) ?
                            value / lcm(A, lcm(B, C)) - 1 :
                            value / lcm(A, lcm(B, C));

            // Inclusion and Exclusion
            int elem = divA + divB + divC - divAC -
                       divBC - divAB + divABC;
            if (elem == (K - 1))
            {
                ans = value;
                break;
            }

            // Multiple should be smaller
            else if (elem > (K - 1))
            {
                end = mid - 1;
            }

            // Multiple should be bigger
            else
            {
                start = mid + 1;
            }
        }
        return ans;
    }

    // Function to return the Kth element from
    // the set of multiples of A, B and C
    static int findKthMultiple(int A, int B, int C, int K)
    {

        // Apply binary search on the multiples of A
        int res = checkA(A, B, C, K);

        // If the required element is not a
        // multiple of A then the multiples
        // of B and C need to be checked
        if (res == -1)
            res = checkB(A, B, C, K);

        // If the required element is neither
        // a multiple of A nor a multiple
        // of B then the multiples of C
        // need to be checked
        if (res == -1)
            res = checkC(A, B, C, K);

        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        int A = 2, B = 4, C = 5, K = 5;

        System.out.println(findKthMultiple(A, B, C, K));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the GCD of A and B
def gcd(A, B):
    if (B == 0):
        return A
    return gcd(B, A % B)

# Function to return the
# LCM of A and B
def lcm(A, B):
    return (A * B) // gcd(A, B)

# Function to return the Kth element from
# the required set if it a multiple of A
def checkA(A, B, C, K):

    # Start and End for Binary Search
    start = 1
    end = K

    # If no answer found return -1
    ans = -1

    while (start <= end):
        mid = (start + end) // 2
        value = A * mid

        divA = mid - 1

        divB = value // B - 1 if (value % B == 0) \
                              else value // B

        divC = value // C - 1 if (value % C == 0) \
                              else value // C

        divAB = value // lcm(A, B) - 1 \
        if (value % lcm(A, B) == 0) \
        else value // lcm(A, B)

        divBC = value // lcm(C, B) - 1 \
        if (value % lcm(C, B) == 0) \
        else value // lcm(C, B)

        divAC = value // lcm(A, C) - 1 \
        if (value % lcm(A, C) == 0) \
        else value // lcm(A, C)

        divABC = value // lcm(A, lcm(B, C)) - 1 \
        if (value % lcm(A, lcm(B, C)) == 0) \
        else value // lcm(A, lcm(B, C))

        # Inclusion and Exclusion
        elem = divA + divB + divC - \
               divAC - divBC - divAB + divABC
        if (elem == (K - 1)):
            ans = value
            break

        # Multiple should be smaller
        elif (elem > (K - 1)):
            end = mid - 1

        # Multiple should be bigger
        else :
            start = mid + 1

    return ans

# Function to return the Kth element from
# the required set if it a multiple of B
def checkB(A, B, C, K):

    # Start and End for Binary Search
    start = 1
    end = K

    # If no answer found return -1
    ans = -1

    while (start <= end):
        mid = (start + end) // 2
        value = B * mid

        divB = mid - 1

        if (value % A == 0):
            divA = value // A - 1
        else: value // A

        if (value % C == 0):
            divC = value // C - 1
        else: value // C

        if (value % lcm(A, B) == 0):
            divAB = value // lcm(A, B) -1
        else: value // lcm(A, B)

        if (value % lcm(C, B) == 0):
            divBC = value // lcm(C, B) -1
        else: value // lcm(C, B)

        if (value % lcm(A, C) == 0):
            divAC = value // lcm(A, C) -1
        else: value // lcm(A, C)

        if (value % lcm(A, lcm(B, C)) == 0):
            divABC = value // lcm(A, lcm(B, C)) - 1
        else: value // lcm(A, lcm(B, C))

        # Inclusion and Exclusion
        elem = divA + divB + divC - \
               divAC - divBC - divAB + divABC
        if (elem == (K - 1)):
            ans = value
            break

        # Multiple should be smaller
        elif (elem > (K - 1)):
            end = mid - 1

        # Multiple should be bigger
        else :
            start = mid + 1

    return ans

# Function to return the Kth element from
# the required set if it a multiple of C
def checkC(A, B, C, K):

    # Start and End for Binary Search
    start = 1
    end = K

    # If no answer found return -1
    ans = -1

    while (start <= end):
        mid = (start + end) // 2
        value = C * mid

        divC = mid - 1

        if (value % B == 0):
            divB = value // B - 1 
        else: value // B

        if (value % A == 0):
            divA = value // A - 1 
        else: value // A

        if (value % lcm(A, B) == 0):
            divAB = value // lcm(A, B) -1
        else: value // lcm(A, B)

        if (value % lcm(C, B) == 0):
            divBC = value // lcm(C, B) -1
        else: value // lcm(C, B)

        if (value % lcm(A, C) == 0):
            divAC = value // lcm(A, C) -1 
        else: value // lcm(A, C)

        if (value % lcm(A, lcm(B, C)) == 0):
            divABC = value // lcm(A, lcm(B, C)) - 1
        else: value // lcm(A, lcm(B, C))

        # Inclusion and Exclusion
        elem = divA + divB + divC - \
               divAC - divBC - divAB + divABC
        if (elem == (K - 1)):
            ans = value
            break

        # Multiple should be smaller
        elif (elem > (K - 1)):
            end = mid - 1

        # Multiple should be bigger
        else :
            start = mid + 1

    return ans

# Function to return the Kth element from
# the set of multiples of A, B and C
def findKthMultiple(A, B, C, K):

    # Apply binary search on the multiples of A
    res = checkA(A, B, C, K)

    # If the required element is not a
    # multiple of A then the multiples
    # of B and C need to be checked
    if (res == -1):
        res = checkB(A, B, C, K)

    # If the required element is neither
    # a multiple of A nor a multiple
    # of B then the multiples of C
    # need to be checked
    if (res == -1):
        res = checkC(A, B, C, K)

    return res

# Driver code
A = 2
B = 4
C = 5
K = 5

print(findKthMultiple(A, B, C, K))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the
    // GCD of A and B
    static int gcd(int A, int B)
    {
        if (B == 0)
            return A;
        return gcd(B, A % B);
    }

    // Function to return the
    // LCM of A and B
    static int lcm(int A, int B)
    {
        return (A * B) / gcd(A, B);
    }

    // Function to return the Kth element from
    // the required set if it a multiple of A
    static int checkA(int A, int B, int C, int K)
    {
        // Start and End for Binary Search
        int start = 1;
        int end = K;

        // If no answer found return -1
        int ans = -1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int value = A * mid;

            int divA = mid - 1;
            int divB = (value % B == 0) ? value / B - 1
                                        : value / B;
            int divC = (value % C == 0) ? value / C - 1
                                        : value / C;
            int divAB = (value % lcm(A, B) == 0) ?
                           value / lcm(A, B) - 1 :
                           value / lcm(A, B);
            int divBC = (value % lcm(C, B) == 0) ?
                           value / lcm(C, B) - 1 :
                           value / lcm(C, B);
            int divAC = (value % lcm(A, C) == 0) ?
                        value / lcm(A, C) - 1 :
                        value / lcm(A, C);
            int divABC = (value % lcm(A, lcm(B, C)) == 0) ?
                            value / lcm(A, lcm(B, C)) - 1 :
                            value / lcm(A, lcm(B, C));

            // Inclusion and Exclusion
            int elem = divA + divB + divC - divAC -
                              divBC - divAB + divABC;
            if (elem == (K - 1))
            {
                ans = value;
                break;
            }

            // Multiple should be smaller
            else if (elem > (K - 1))
            {
                end = mid - 1;
            }

            // Multiple should be bigger
            else
            {
                start = mid + 1;
            }
        }
        return ans;
    }

    // Function to return the Kth element from
    // the required set if it a multiple of B
    static int checkB(int A, int B, int C, int K)
    {
        // Start and End for Binary Search
        int start = 1;
        int end = K;

        // If no answer found return -1
        int ans = -1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int value = B * mid;

            int divB = mid - 1;
            int divA = (value % A == 0) ? value / A - 1
                                        : value / A;
            int divC = (value % C == 0) ? value / C - 1
                                        : value / C;
            int divAB = (value % lcm(A, B) == 0) ?
                           value / lcm(A, B) - 1 :
                           value / lcm(A, B);
            int divBC = (value % lcm(C, B) == 0) ?
                           value / lcm(C, B) - 1 :
                           value / lcm(C, B);
            int divAC = (value % lcm(A, C) == 0) ?
                           value / lcm(A, C) - 1 :
                           value / lcm(A, C);
            int divABC = (value % lcm(A, lcm(B, C)) == 0) ?
                            value / lcm(A, lcm(B, C)) - 1 :
                            value / lcm(A, lcm(B, C));

            // Inclusion and Exclusion
            int elem = divA + divB + divC - divAC -
                       divBC - divAB + divABC;
            if (elem == (K - 1))
            {
                ans = value;
                break;
            }

            // Multiple should be smaller
            else if (elem > (K - 1))
            {
                end = mid - 1;
            }

            // Multiple should be bigger
            else
            {
                start = mid + 1;
            }
        }
        return ans;
    }

    // Function to return the Kth element from
    // the required set if it a multiple of C
    static int checkC(int A, int B, int C, int K)
    {
        // Start and End for Binary Search
        int start = 1;
        int end = K;

        // If no answer found return -1
        int ans = -1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int value = C * mid;

            int divC = mid - 1;
            int divB = (value % B == 0) ? value / B - 1
                                        : value / B;
            int divA = (value % A == 0) ? value / A - 1
                                        : value / A;
            int divAB = (value % lcm(A, B) == 0) ?
                           value / lcm(A, B) - 1 :
                           value / lcm(A, B);
            int divBC = (value % lcm(C, B) == 0) ?
                           value / lcm(C, B) - 1 :
                           value / lcm(C, B);
            int divAC = (value % lcm(A, C) == 0) ?
                           value / lcm(A, C) - 1 :
                           value / lcm(A, C);
            int divABC = (value % lcm(A, lcm(B, C)) == 0) ?
                            value / lcm(A, lcm(B, C)) - 1 :
                            value / lcm(A, lcm(B, C));

            // Inclusion and Exclusion
            int elem = divA + divB + divC - divAC -
                       divBC - divAB + divABC;
            if (elem == (K - 1))
            {
                ans = value;
                break;
            }

            // Multiple should be smaller
            else if (elem > (K - 1))
            {
                end = mid - 1;
            }

            // Multiple should be bigger
            else
            {
                start = mid + 1;
            }
        }
        return ans;
    }

    // Function to return the Kth element from
    // the set of multiples of A, B and C
    static int findKthMultiple(int A, int B, int C, int K)
    {

        // Apply binary search on the multiples of A
        int res = checkA(A, B, C, K);

        // If the required element is not a
        // multiple of A then the multiples
        // of B and C need to be checked
        if (res == -1)
            res = checkB(A, B, C, K);

        // If the required element is neither
        // a multiple of A nor a multiple
        // of B then the multiples of C
        // need to be checked
        if (res == -1)
            res = checkC(A, B, C, K);

        return res;
    }

    // Driver code
    public static void Main(String []args)
    {
        int A = 2, B = 4, C = 5, K = 5;

        Console.WriteLine(findKthMultiple(A, B, C, K));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach
      // Function to return the
      // GCD of A and B
      function gcd(A, B) {
        if (B === 0) return A;
        return gcd(B, A % B);
      }

      // Function to return the
      // LCM of A and B
      function lcm(A, B) {
        return (A * B) / gcd(A, B);
      }

      // Function to return the Kth element from
      // the required set if it a multiple of A
      function checkA(A, B, C, K) {
        // Start and End for Binary Search
        var start = 1;
        var end = K;

        // If no answer found return -1
        var ans = -1;

        while (start <= end) {
          var mid = parseInt((start + end) / 2);
          var value = A * mid;

          var divA = mid - 1;
          var divB = parseInt(value % B === 0 ? value / B - 1 : value / B);
          var divC = parseInt(value % C === 0 ? value / C - 1 : value / C);
          var divAB = parseInt(
            value % lcm(A, B) === 0 ? value / lcm(A, B) - 1 : value / lcm(A, B)
          );
          var divBC = parseInt(
            value % lcm(C, B) === 0 ? value / lcm(C, B) - 1 : value / lcm(C, B)
          );
          var divAC = parseInt(
            value % lcm(A, C) === 0 ? value / lcm(A, C) - 1 : value / lcm(A, C)
          );
          var divABC = parseInt(
            value % lcm(A, lcm(B, C)) === 0
              ? value / lcm(A, lcm(B, C)) - 1
              : value / lcm(A, lcm(B, C))
          );

          // Inclusion and Exclusion
          var elem = divA + divB + divC - divAC - divBC - divAB + divABC;
          if (elem === K - 1) {
            ans = value;
            break;
          }

          // Multiple should be smaller
          else if (elem > K - 1) {
            end = mid - 1;
          }

          // Multiple should be bigger
          else {
            start = mid + 1;
          }
        }
        return ans;
      }

      // Function to return the Kth element from
      // the required set if it a multiple of B
      function checkB(A, B, C, K) {
        // Start and End for Binary Search
        var start = 1;
        var end = K;

        // If no answer found return -1
        var ans = -1;

        while (start <= end) {
          var mid = parseInt((start + end) / 2);
          var value = B * mid;

          var divB = mid - 1;
          var divA = parseInt(value % A === 0 ? value / A - 1 : value / A);
          var divC = parseInt(value % C === 0 ? value / C - 1 : value / C);
          var divAB = parseInt(
            value % lcm(A, B) === 0 ? value / lcm(A, B) - 1 : value / lcm(A, B)
          );
          var divBC = parseInt(
            value % lcm(C, B) === 0 ? value / lcm(C, B) - 1 : value / lcm(C, B)
          );
          var divAC = parseInt(
            value % lcm(A, C) === 0 ? value / lcm(A, C) - 1 : value / lcm(A, C)
          );
          var divABC = parseInt(
            value % lcm(A, lcm(B, C)) === 0
              ? value / lcm(A, lcm(B, C)) - 1
              : value / lcm(A, lcm(B, C))
          );

          // Inclusion and Exclusion
          var elem = divA + divB + divC - divAC - divBC - divAB + divABC;
          if (elem === K - 1) {
            ans = value;
            break;
          }

          // Multiple should be smaller
          else if (elem > K - 1) {
            end = mid - 1;
          }

          // Multiple should be bigger
          else {
            start = mid + 1;
          }
        }
        return ans;
      }

      // Function to return the Kth element from
      // the required set if it a multiple of C
      function checkC(A, B, C, K) {
        // Start and End for Binary Search
        var start = 1;
        var end = K;

        // If no answer found return -1
        var ans = -1;

        while (start <= end) {
          var mid = parseInt((start + end) / 2);
          var value = C * mid;

          var divC = mid - 1;
          var divB = parseInt(value % B === 0 ? value / B - 1 : value / B);
          var divA = parseInt(value % A === 0 ? value / A - 1 : value / A);
          var divAB = parseInt(
            value % lcm(A, B) === 0 ? value / lcm(A, B) - 1 : value / lcm(A, B)
          );
          var divBC = parseInt(
            value % lcm(C, B) === 0 ? value / lcm(C, B) - 1 : value / lcm(C, B)
          );
          var divAC = parseInt(
            value % lcm(A, C) === 0 ? value / lcm(A, C) - 1 : value / lcm(A, C)
          );
          var divABC = parseInt(
            value % lcm(A, lcm(B, C)) === 0
              ? value / lcm(A, lcm(B, C)) - 1
              : value / lcm(A, lcm(B, C))
          );

          // Inclusion and Exclusion
          var elem = divA + divB + divC - divAC - divBC - divAB + divABC;
          if (elem === K - 1) {
            ans = value;
            break;
          }

          // Multiple should be smaller
          else if (elem > K - 1) {
            end = mid - 1;
          }

          // Multiple should be bigger
          else {
            start = mid + 1;
          }
        }
        return ans;
      }

      // Function to return the Kth element from
      // the set of multiples of A, B and C
      function findKthMultiple(A, B, C, K) {
        // Apply binary search on the multiples of A
        var res = checkA(A, B, C, K);
        console.log(res);

        // If the required element is not a
        // multiple of A then the multiples
        // of B and C need to be checked
        if (res === -1) res = checkB(A, B, C, K);

        // If the required element is neither
        // a multiple of A nor a multiple
        // of B then the multiples of C
        // need to be checked
        if (res === -1) res = checkC(A, B, C, K);

        return res;
      }

      // Driver code
      var A = 2,
        B = 4,
        C = 5,
        K = 5;

      document.write(findKthMultiple(A, B, C, K));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
8
```