# 总和等于 K 的所有唯一组合

> 原文:[https://www . geesforgeks . org/all-unique-组合拳-其和等于-k/](https://www.geeksforgeeks.org/all-unique-combinations-whose-sum-equals-to-k/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** 。任务是从给定的数组中找到所有唯一的组合，使得每个组合中的元素之和等于 **K** 。

**示例:**

> **输入:** arr[] = {1，2，3}，K = 3
> **输出:**
> {1，2}
> {3}
> **说明:**
> 这些是和等于 3 的组合。
> 
> **输入:** arr[] = {2，2，2}，K = 4
> **输出:**
> {2，2}

**方法:**某些元素可以在给定的数组中重复。确保迭代这些元素的出现次数，以避免重复组合。一旦你做到了这一点，事情就相当简单了。用剩余的和调用一个[递归](https://www.geeksforgeeks.org/recursion/)函数，使指数向前移动。当总和达到 K 时，打印所有被选中的元素以获得这个总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all unique combination of
// given elements such that their sum is K
void unique_combination(int l, int sum, int K,
                        vector<int>& local,
                        vector<int>& A)
{
    // If a unique combination is found
    if (sum == K) {
        cout << "{";
        for (int i = 0; i < local.size(); i++)
        {
            if (i != 0)
                cout << " ";
            cout << local[i];
            if (i != local.size() - 1)
                cout << ", ";
        }
        cout << "}" << endl;
        return;
    }

    // For all other combinations
    for (int i = l; i < A.size(); i++)
    {

        // Check if the sum exceeds K
        if (sum + A[i] > K)
            continue;

        // Check if it is repeated or not
        if (i > l and A[i] == A[i - 1])
            continue;

        // Take the element into the combination
        local.push_back(A[i]);

        // Recursive call
        unique_combination(i + 1, sum + A[i], K, local, A);

        // Remove element from the combination
        local.pop_back();
    }
}

// Function to find all combination
// of the given elements
void Combination(vector<int> A, int K)
{
    // Sort the given elements
    sort(A.begin(), A.end());

    // To store combination
    vector<int> local;

    unique_combination(0, 0, K, local, A);
}

// Driver code
int main()
{
    vector<int> A = { 10, 1, 2, 7, 6, 1, 5 };

    int K = 8;

    // Function call
    Combination(A, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to find all unique combination of
    // given elements such that their sum is K
    static void unique_combination(int l, int sum, int K,
                                   Vector<Integer> local,
                                   Vector<Integer> A)
    {
        // If a unique combination is found
        if (sum == K) {
            System.out.print("{");
            for (int i = 0; i < local.size(); i++) {
                if (i != 0)
                    System.out.print(" ");
                System.out.print(local.get(i));
                if (i != local.size() - 1)
                    System.out.print(", ");
            }
            System.out.println("}");
            return;
        }

        // For all other combinations
        for (int i = l; i < A.size(); i++) {

            // Check if the sum exceeds K
            if (sum + A.get(i) > K)
                continue;

            // Check if it is repeated or not
            if (i > l && A.get(i) == A.get(i - 1) )
                continue;

            // Take the element into the combination
            local.add(A.get(i));

            // Recursive call
            unique_combination(i + 1, sum + A.get(i), K,
                               local, A);

            // Remove element from the combination
            local.remove(local.size() - 1);
        }
    }

    // Function to find all combination
    // of the given elements
    static void Combination(Vector<Integer> A, int K)
    {
        // Sort the given elements
        Collections.sort(A);

        // To store combination
        Vector<Integer> local = new Vector<Integer>();

        unique_combination(0, 0, K, local, A);
    }

    // Driver code
    public static void main(String[] args)
    {
        Integer[] arr = { 10, 1, 2, 7, 6, 1, 5 };
        Vector<Integer> A
            = new Vector<>(Arrays.asList(arr));

        int K = 8;

        // Function call
        Combination(A, K);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to find all unique combination of
# given elements such that their sum is K

def unique_combination(l, sum, K, local, A):

    # If a unique combination is found
    if (sum == K):
        print("{", end="")
        for i in range(len(local)):
            if (i != 0):
                print(" ", end="")
            print(local[i], end="")
            if (i != len(local) - 1):
                print(", ", end="")
        print("}")
        return

    # For all other combinations
    for i in range(l, len(A), 1):

        # Check if the sum exceeds K
        if (sum + A[i] > K):
            continue

        # Check if it is repeated or not
        if (i > l and
                A[i] == A[i - 1]):
            continue

        # Take the element into the combination
        local.append(A[i])

        # Recursive call
        unique_combination(i + 1, sum + A[i],
                           K, local, A)

        # Remove element from the combination
        local.remove(local[len(local) - 1])

# Function to find all combination
# of the given elements

def Combination(A, K):

    # Sort the given elements
    A.sort(reverse=False)

    local = []

    unique_combination(0, 0, K, local, A)

# Driver code
if __name__ == '__main__':
    A = [10, 1, 2, 7, 6, 1, 5]

    K = 8

    # Function call
    Combination(A, K)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to find all unique combination of
    // given elements such that their sum is K
    static void unique_combination(int l, int sum, int K,
                                   List<int> local,
                                   List<int> A)
    {
        // If a unique combination is found
        if (sum == K)
        {
            Console.Write("{");
            for (int i = 0; i < local.Count; i++)
            {
                if (i != 0)
                    Console.Write(" ");
                Console.Write(local[i]);
                if (i != local.Count - 1)
                    Console.Write(", ");
            }
            Console.WriteLine("}");
            return;
        }

        // For all other combinations
        for (int i = l; i < A.Count; i++)
        {
            // Check if the sum exceeds K
            if (sum + A[i] > K)
                continue;

            // Check if it is repeated or not
            if (i >l && A[i] == A[i - 1])
                continue;

            // Take the element into the combination
            local.Add(A[i]);

            // Recursive call
            unique_combination(i + 1, sum + A[i], K, local,
                               A);

            // Remove element from the combination
            local.RemoveAt(local.Count - 1);
        }
    }

    // Function to find all combination
    // of the given elements
    static void Combination(List<int> A, int K)
    {
        // Sort the given elements
        A.Sort();

        // To store combination
        List<int> local = new List<int>();

        unique_combination(0, 0, K, local, A);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 10, 1, 2, 7, 6, 1, 5 };
        List<int> A = new List<int>(arr);

        int K = 8;

        // Function call
        Combination(A, K);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find all unique combination of
// given elements such that their sum is K
function unique_combination(l, sum, K, local, A) {
    // If a unique combination is found
    if (sum == K) {
        document.write("{");
        for (let i = 0; i < local.length; i++) {
            if (i != 0)
                document.write(" ");
            document.write(local[i]);
            if (i != local.length - 1)
                document.write(", ");
        }
        document.write("}" + "<br>");
        return;
    }

    // For all other combinations
    for (let i = l; i < A.length; i++) {

        // Check if the sum exceeds K
        if (sum + A[i] > K)
            continue;

        // Check if it is repeated or not
        if (i > l && A[i] == A[i - 1])
            continue;

        // Take the element into the combination
        local.push(A[i]);

        // Recursive call
        unique_combination(i + 1, sum + A[i], K, local, A);

        // Remove element from the combination
        local.pop();
    }
}

// Function to find all combination
// of the given elements
function Combination(A, K) {
    // Sort the given elements
    A.sort((a, b) => a - b);

    // To store combination
    let local = [];

    unique_combination(0, 0, K, local, A);
}

// Driver code

let A = [10, 1, 2, 7, 6, 1, 5];

let K = 8;

// Function call
Combination(A, K);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
{1,  1,  6}
{1,  2,  5}
{1,  7}
{2,  6}
```