# 检查 K 个不同的数组元素是否形成奇数和

> 原文:[https://www . geesforgeks . org/check-if-k-distinct-array-elements-form-a-odd-sum/](https://www.geeksforgeeks.org/check-if-k-distinct-array-elements-form-an-odd-sum/)

给定一个大小为 **N** 的数组 **A[]** ，任务是检查是否有可能使用数组中不同的元素 **K** 得到奇数和。
**示例:**

> **输入:** N = 4，K = 2，A = {10，19，14，14}
> **输出:** YES
> **解释:**
> 19 + 14 = 33，这是奇数
> **输入:** N = 3，K = 3，A = {101，102，103}
> **输出:** NO
> **解释**

**进场:**

*   让我们看看一些基本的数学性质:

```
EVEN + EVEN = EVEN
ODD  + ODD  = EVEN
EVEN + ODD  = ODD
```

*   从以上性质，我们可以得出结论，当奇数个奇数被加到任何偶数个偶数时，结果总是奇数。

> **示例:**
> 
> *   3 + 2 + 6 = 11(奇数)
> *   1 + 3 + 7 + 4 = 15(奇数)

因此，请按照以下步骤解决问题:

*   计算数组中不同的奇数和偶数元素。
*   如果数组中存在 K 个或更多奇数元素，则打印“是”。
*   否则，对于奇数的每个奇数计数，检查数组中是否有足够的偶数。
*   如果出现任何此类情况，请打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return if
// odd sum is possible or not
bool oddSum(vector<int>& A,
            int N, int K)
{

    // Stores distinct odd elements
    set<int> Odd;
    // Stores distinct even elements
    set<int> Even;

    // Iterating through given array
    for (int i = 0; i < N; i++) {

        // If element is even
        if (A[i] % 2 == 0) {
            Even.insert(A[i]);
        }
        // If element is odd
        else {
            Odd.insert(A[i]);
        }
    }

    // If atleast K elements
    // in the array are odd
    if (Odd.size() >= K)
        return true;

    bool flag = false;

    // Check for all odd frequencies
    // of odd elements whether
    // sufficient even numbers
    // are present or not
    for (int i = 1; i < K; i += 2) {

        // Count of even numbers
        // required
        int needed = K - i;

        // If required even numbers
        // are present in the array
        if (needed <= Even.size()) {

            return true;
        }
    }

    return flag;
}

// Driver Program
int main()
{
    int K = 5;
    vector<int> A = { 12, 1, 7, 7, 26, 18 };
    int N = 3;

    if (oddSum(A, N, K))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return if
// odd sum is possible or not
static boolean oddSum(int []A,
                      int N, int K)
{

    // Stores distinct odd elements
    HashSet<Integer> Odd = new HashSet<Integer>();

    // Stores distinct even elements
    HashSet<Integer> Even = new HashSet<Integer>();

    // Iterating through given array
    for(int i = 0; i < N; i++)
    {

        // If element is even
        if (A[i] % 2 == 0)
        {
            Even.add(A[i]);
        }

        // If element is odd
        else
        {
            Odd.add(A[i]);
        }
    }

    // If atleast K elements
    // in the array are odd
    if (Odd.size() >= K)
        return true;

    boolean flag = false;

    // Check for all odd frequencies
    // of odd elements whether
    // sufficient even numbers
    // are present or not
    for(int i = 1; i < K; i += 2)
    {

        // Count of even numbers
        // required
        int needed = K - i;

        // If required even numbers
        // are present in the array
        if (needed <= Even.size())
        {
            return true;
        }
    }
    return flag;
}

// Driver code
public static void main(String[] args)
{
    int K = 5;
    int []A = { 12, 1, 7, 7, 26, 18 };
    int N = 3;

    if (oddSum(A, N, K))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to return if
# odd sum is possible or not
def oddSum(A, N, K):

    # Stores distinct odd elements
    Odd = set([])
    # Stores distinct even elements
    Even = set([])

    # Iterating through given array
    for i in range (N):

        # If element is even
        if (A[i] % 2 == 0):
            Even.add(A[i])

        # If element is odd
        else:
            Odd.add(A[i])

    # If atleast K elements
    # in the array are odd
    if (len(Odd) >= K):
        return True

    flag = False

    # Check for all odd frequencies
    # of odd elements whether
    # sufficient even numbers
    # are present or not
    for i in range (1, K, 2):

        # Count of even numbers
        # required
        needed = K - i

        # If required even numbers
        # are present in the array
        if (needed <= len(Even)):
            return True

    return flag

# Driver Program
if __name__ == "__main__":

    K = 5
    A = [12, 1, 7,
         7, 26, 18]
    N = 3

    if (oddSum(A, N, K)):
        print ("YES")
    else:
        print("NO")

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return if
// odd sum is possible or not
static bool oddSum(int []A, int N, int K)
{

    // Stores distinct odd elements
    HashSet<int> Odd = new HashSet<int>();

    // Stores distinct even elements
    HashSet<int> Even = new HashSet<int>();

    // Iterating through given array
    for(int i = 0; i < N; i++)
    {

        // If element is even
        if (A[i] % 2 == 0) 
        {
            Even.Add(A[i]);
        }

        // If element is odd
        else
        {
            Odd.Add(A[i]);
        }
    }

    // If atleast K elements
    // in the array are odd
    if (Odd.Count >= K)
        return true;

    bool flag = false;

    // Check for all odd frequencies
    // of odd elements whether
    // sufficient even numbers
    // are present or not
    for(int i = 1; i < K; i += 2)
    {

        // Count of even numbers
        // required
        int needed = K - i;

        // If required even numbers
        // are present in the array
        if (needed <= Even.Count)
        {
            return true;
        }
    }
    return flag;
}

// Driver code
public static void Main(String[] args)
{
    int K = 5;
    int []A = { 12, 1, 7, 7, 26, 18 };
    int N = 3;

    if (oddSum(A, N, K))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to return if
   // odd sum is possible or not
    function oddSum(A,N,K)
    {
        // Stores distinct odd elements
    let Odd = new Set();

    // Stores distinct even elements
    let Even = new Set();

    // Iterating through given array
    for(let i = 0; i < N; i++)
    {

        // If element is even
        if (A[i] % 2 == 0)
        {
            Even.add(A[i]);
        }

        // If element is odd
        else
        {
            Odd.add(A[i]);
        }
    }

    // If atleast K elements
    // in the array are odd
    if (Odd.size >= K)
        return true;

    let flag = false;

    // Check for all odd frequencies
    // of odd elements whether
    // sufficient even numbers
    // are present or not
    for(let i = 1; i < K; i += 2)
    {

        // Count of even numbers
        // required
        let needed = K - i;

        // If required even numbers
        // are present in the array
        if (needed <= Even.size)
        {
            return true;
        }
    }
    return flag;
    }

    // Driver code
    let K = 5;
    let A=[12, 1, 7, 7, 26, 18];
    let N = 3;
    if (oddSum(A, N, K))
        document.write("YES");
    else
        document.write("NO");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
NO
```

***时间复杂度:** O(N)*