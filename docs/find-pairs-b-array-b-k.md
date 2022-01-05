# 找出数组中的所有对(a，b)，使得 a % b = k

> 原文:[https://www.geeksforgeeks.org/find-pairs-b-array-b-k/](https://www.geeksforgeeks.org/find-pairs-b-array-b-k/)

给定一个具有不同元素的数组，任务是找到数组中的对，使得 a % b = k，其中 k 是给定的整数。

**示例:**

```
Input  :  arr[] = {2, 3, 5, 4, 7}   
              k = 3
Output :  (7, 4), (3, 4), (3, 5), (3, 7)
7 % 4 = 3
3 % 4 = 3
3 % 5 = 3
3 % 7 = 3
```

一个**天真的解决方案**是把所有的对一个一个的做出来，检查它们的模是否等于 k。如果等于 k，则打印该对。

## C++

```
// C++ implementation to find such pairs
#include <bits/stdc++.h>
using namespace std;

// Function to find pair such that (a % b = k)
bool printPairs(int arr[], int n, int k)
{
    bool isPairFound = true;

    // Consider each and every pair
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            // Print if their modulo equals to k
            if (i != j && arr[i] % arr[j] == k) {
                cout << "(" << arr[i] << ", "
                     << arr[j] << ")"
                     << " ";
                isPairFound = true;
            }
        }
    }

    return isPairFound;
}

// Driver program
int main()
{
    int arr[] = { 2, 3, 5, 4, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    if (printPairs(arr, n, k) == false)
        cout << "No such pair exists";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find such pairs

class Test {
    // method to find pair such that (a % b = k)
    static boolean printPairs(int arr[], int n, int k)
    {
        boolean isPairFound = true;

        // Consider each and every pair
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                // Print if their modulo equals to k
                if (i != j && arr[i] % arr[j] == k) {
                    System.out.print("(" + arr[i] + ", " + arr[j] + ")"
                                     + " ");
                    isPairFound = true;
                }
            }
        }

        return isPairFound;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 2, 3, 5, 4, 7 };
        int k = 3;

        if (printPairs(arr, arr.length, k) == false)
            System.out.println("No such pair exists");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find such pairs

# Function to find pair such that (a % b = k)
def printPairs(arr, n, k):

    isPairFound = True

    # Consider each and every pair
    for i in range(0, n):

        for j in range(0, n):

            # Print if their modulo equals to k
            if (i != j and arr[i] % arr[j] == k):

                print("(", arr[i], ", ", arr[j], ")",
                                 sep = "", end = " ")
                isPairFound = True

    return isPairFound

# Driver Code
arr = [2, 3, 5, 4, 7]
n = len(arr)
k = 3
if (printPairs(arr, n, k) == False):
    print("No such pair exists")

# This article is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# implementation to find such pair
using System;

public class GFG {

    // method to find pair such that (a % b = k)
    static bool printPairs(int[] arr, int n, int k)
    {
        bool isPairFound = true;

        // Consider each and every pair
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
            {
                // Print if their modulo equals to k
                if (i != j && arr[i] % arr[j] == k)
                {
                    Console.Write("(" + arr[i] + ", "
                                + arr[j] + ")" + " ");
                    isPairFound = true;
                }
            }
        }

        return isPairFound;
    }

    // Driver method
    public static void Main()
    {
        int[] arr = { 2, 3, 5, 4, 7 };
        int k = 3;

        if (printPairs(arr, arr.Length, k) == false)
            Console.WriteLine("No such pair exists");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find such pairs

// Function to find pair
// such that (a % b = k)
function printPairs($arr, $n, $k)
{
    $isPairFound = true;

    // Consider each and every pair
    for ($i = 0; $i < $n; $i++)
    {
        for ( $j = 0; $j < $n; $j++)
        {
            // Print if their modulo
            // equals to k
            if ($i != $j && $arr[$i] %
                            $arr[$j] == $k)
            {
                echo "(" , $arr[$i] , ", ",
                       $arr[$j] , ")", " ";
                $isPairFound = true;
            }
        }
    }

    return $isPairFound;
}

// Driver Code
$arr = array(2, 3, 5, 4, 7);
$n = sizeof($arr);
$k = 3;

if (printPairs($arr, $n, $k) == false)
    echo "No such pair exists";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to find such pair

    // method to find pair such that (a % b = k)
    function printPairs(arr, n, k)
    {
        let isPairFound = true;

        // Consider each and every pair
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++)
            {
                // Print if their modulo equals to k
                if (i != j && arr[i] % arr[j] == k)
                {
                    document.write("(" + arr[i] + ", " + arr[j] + ")" + " ");
                    isPairFound = true;
                }
            }
        }

        return isPairFound;
    }

    let arr = [ 2, 3, 5, 4, 7 ];
    let k = 3;

    if (printPairs(arr, arr.length, k) == false)
      document.write("No such pair exists");

</script>
```

**输出:**

```
(3, 5) (3, 4) (3, 7) (7, 4)
```

**时间复杂度:** O(n <sup>2</sup> )
一个**高效解决方案**基于以下观察:

1.  如果 k 本身存在于 arr[]，那么 k 与所有元素 arr[i]形成一对，其中 k < arr[i]。对于所有这样的 arr[i]，我们有 k % arr[i] = k。
2.  对于大于或等于 k 的所有元素，我们使用以下事实。

```
   If arr[i] % arr[j] = k, 
   ==> arr[i] = x * arr[j] + k
   ==> (arr[i] - k) = x * arr[j]
  We find all divisors of (arr[i] - k)
  and see if they are present in arr[].
```

为了快速检查数组中是否存在元素，我们使用散列法。

## C++

```
// C++ program to find all pairs such that
// a % b = k.
#include <bits/stdc++.h>
using namespace std;

// Utiltity function to find the divisors of
// n and store in vector v[]
vector<int> findDivisors(int n)
{
    vector<int> v;

    // Vector is used to store  the divisors
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            // If n is a square number, push
            // only one occurrence
            if (n / i == i)
                v.push_back(i);
            else {
                v.push_back(i);
                v.push_back(n / i);
            }
        }
    }
    return v;
}

// Function to find pairs such that (a%b = k)
bool printPairs(int arr[], int n, int k)
{
    // Store all the elements in the map
    // to use map as hash for finding elements
    // in O(1) time.
    unordered_map<int, bool> occ;
    for (int i = 0; i < n; i++)
        occ[arr[i]] = true;

    bool isPairFound = false;
    for (int i = 0; i < n; i++) {
        // Print all the pairs with (a, b) as
        // (k, numbers greater than k) as
        // k % (num (> k)) = k i.e. 2%4 = 2
        if (occ[k] && k < arr[i]) {
            cout << "(" << k << ", " << arr[i] << ") ";
            isPairFound = true;
        }

        // Now check for the current element as 'a'
        // how many b exists such that a%b = k
        if (arr[i] >= k) {
            // find all the divisors of (arr[i]-k)
            vector<int> v = findDivisors(arr[i] - k);

            // Check for each divisor i.e. arr[i] % b = k
            // or not, if yes then print that pair.
            for (int j = 0; j < v.size(); j++) {
                if (arr[i] % v[j] == k && arr[i] != v[j] && occ[v[j]]) {
                    cout << "(" << arr[i] << ", "
                         << v[j] << ") ";
                    isPairFound = true;
                }
            }

            // Clear vector
            v.clear();
        }
    }

    return isPairFound;
}

// Driver program
int main()
{
    int arr[] = { 3, 1, 2, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    if (printPairs(arr, n, k) == false)
        cout << "No such pair exists";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all pairs such that
// a % b = k.

import java.util.HashMap;
import java.util.Vector;

class Test {
    // Utility method to find the divisors of
    // n and store in vector v[]
    static Vector<Integer> findDivisors(int n)
    {
        Vector<Integer> v = new Vector<>();

        // Vector is used to store  the divisors
        for (int i = 1; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {
                // If n is a square number, push
                // only one occurrence
                if (n / i == i)
                    v.add(i);
                else {
                    v.add(i);
                    v.add(n / i);
                }
            }
        }
        return v;
    }

    // method to find pairs such that (a%b = k)
    static boolean printPairs(int arr[], int n, int k)
    {
        // Store all the elements in the map
        // to use map as hash for finding elements
        // in O(1) time.
        HashMap<Integer, Boolean> occ = new HashMap<>();
        for (int i = 0; i < n; i++)
            occ.put(arr[i], true);

        boolean isPairFound = false;
        for (int i = 0; i < n; i++) {
            // Print all the pairs with (a, b) as
            // (k, numbers greater than k) as
            // k % (num (> k)) = k i.e. 2%4 = 2
            if (occ.get(k) && k < arr[i]) {
                System.out.print("(" + k + ", " + arr[i] + ") ");
                isPairFound = true;
            }

            // Now check for the current element as 'a'
            // how many b exists such that a%b = k
            if (arr[i] >= k) {
                // find all the divisors of (arr[i]-k)
                Vector<Integer> v = findDivisors(arr[i] - k);

                // Check for each divisor i.e. arr[i] % b = k
                // or not, if yes then print that pair.
                for (int j = 0; j < v.size(); j++) {
                    if (arr[i] % v.get(j) == k && arr[i] != v.get(j) && occ.get(v.get(j))) {
                        System.out.print("(" + arr[i] + ", "
                                         + v.get(j) + ") ");
                        isPairFound = true;
                    }
                }

                // Clear vector
                v.clear();
            }
        }

        return isPairFound;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 3, 1, 2, 5, 4 };
        int k = 2;

        if (printPairs(arr, arr.length, k) == false)
            System.out.println("No such pair exists");
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all pairs
# such that a % b = k.

# Utiltity function to find the divisors
# of n and store in vector v[]
import math as mt

def findDivisors(n):

    v = []

    # Vector is used to store the divisors
    for i in range(1, mt.floor(n**(.5)) + 1):
        if (n % i == 0):

            # If n is a square number, push
            # only one occurrence
            if (n / i == i):
                v.append(i)
            else:
                v.append(i)
                v.append(n // i)

    return v

# Function to find pairs such that (a%b = k)
def printPairs(arr, n, k):

    # Store all the elements in the map
    # to use map as hash for finding elements
    # in O(1) time.
    occ = dict()
    for i in range(n):
        occ[arr[i]] = True

    isPairFound = False

    for i in range(n):

        # Print all the pairs with (a, b) as
        # (k, numbers greater than k) as
        # k % (num (> k)) = k i.e. 2%4 = 2
        if (occ[k] and k < arr[i]):
            print("(", k, ",", arr[i], ")", end = " ")
            isPairFound = True

        # Now check for the current element as 'a'
        # how many b exists such that a%b = k
        if (arr[i] >= k):

            # find all the divisors of (arr[i]-k)
            v = findDivisors(arr[i] - k)

            # Check for each divisor i.e. arr[i] % b = k
            # or not, if yes then prthat pair.
            for j in range(len(v)):
                if (arr[i] % v[j] == k and
                    arr[i] != v[j] and
                    occ[v[j]]):
                    print("(", arr[i], ",", v[j],
                                       ")", end = " ")
                    isPairFound = True

    return isPairFound

# Driver Code
arr = [3, 1, 2, 5, 4]
n = len(arr)
k = 2

if (printPairs(arr, n, k) == False):
    print("No such pair exists")

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find all pairs
// such that a % b = k.
using System;
using System.Collections.Generic;

class GFG
{
// Utility method to find the divisors
// of n and store in vector v[]
public static List<int> findDivisors(int n)
{
    List<int> v = new List<int>();

    // Vector is used to store
    // the divisors
    for (int i = 1;
             i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0)
        {
            // If n is a square number,
            // push only one occurrence
            if (n / i == i)
            {
                v.Add(i);
            }
            else
            {
                v.Add(i);
                v.Add(n / i);
            }
        }
    }
    return v;
}

// method to find pairs such
// that (a%b = k)
public static bool printPairs(int[] arr,
                              int n, int k)
{
    // Store all the elements in the
    // map to use map as hash for
    // finding elements in O(1) time.
    Dictionary<int,
               bool> occ = new Dictionary<int,
                                          bool>();
    for (int i = 0; i < n; i++)
    {
        occ[arr[i]] = true;
    }

    bool isPairFound = false;
    for (int i = 0; i < n; i++)
    {
        // Print all the pairs with (a, b) as
        // (k, numbers greater than k) as
        // k % (num (> k)) = k i.e. 2%4 = 2
        if (occ[k] && k < arr[i])
        {
            Console.Write("(" + k + ", " +
                           arr[i] + ") ");
            isPairFound = true;
        }

        // Now check for the current element
        // as 'a' how many b exists such that
        // a%b = k
        if (arr[i] >= k)
        {
            // find all the divisors of (arr[i]-k)
            List<int> v = findDivisors(arr[i] - k);

            // Check for each divisor i.e.
            // arr[i] % b = k or not, if
            // yes then print that pair.
            for (int j = 0; j < v.Count; j++)
            {
                if (arr[i] % v[j] == k &&
                    arr[i] != v[j] && occ[v[j]])
                {
                    Console.Write("(" + arr[i] +
                                  ", " + v[j] + ") ");
                    isPairFound = true;
                }
            }

            // Clear vector
            v.Clear();
        }
    }

    return isPairFound;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {3, 1, 2, 5, 4};
    int k = 2;

    if (printPairs(arr, arr.Length, k) == false)
    {
        Console.WriteLine("No such pair exists");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to find all pairs such that
// a % b = k.   

    // Utility method to find the divisors of
    // n and store in vector v[]
    function findDivisors(n)
    {
        let v = [];

        // Vector is used to store  the divisors
        for (let i = 1; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0) {
                // If n is a square number, push
                // only one occurrence
                if (n / i == i)
                    v.push(i);
                else {
                    v.push(i);
                    v.push(Math.floor(n / i));
                }
            }
        }
        return v;
    }

    // method to find pairs such that (a%b = k)
    function printPairs(arr,n,k)
    {
        // Store all the elements in the map
        // to use map as hash for finding elements
        // in O(1) time.
        let occ = new Map();
        for (let i = 0; i < n; i++)
            occ.set(arr[i], true);

        let isPairFound = false;
        for (let i = 0; i < n; i++) {
            // Print all the pairs with (a, b) as
            // (k, numbers greater than k) as
            // k % (num (> k)) = k i.e. 2%4 = 2
            if (occ.get(k) && k < arr[i]) {
                document.write("(" + k + ", " +
                arr[i] + ") ");
                isPairFound = true;
            }

            // Now check for the current element as 'a'
            // how many b exists such that a%b = k
            if (arr[i] >= k) {
                // find all the divisors of (arr[i]-k)
                let v = findDivisors(arr[i] - k);

                // Check for each divisor
                // i.e. arr[i] % b = k
                // or not, if yes then
                // print that pair.
                for (let j = 0; j < v.length; j++)
                {
                    if (arr[i] % v[j] == k &&
                    arr[i] != v[j] &&
                    occ.get(v[j]))
                    {
                        document.write("(" + arr[i] + ", "
                                         + v[j] + ") ");
                        isPairFound = true;
                    }
                }

                // Clear vector
                v=[];
            }
        }

        return isPairFound;
    }

    // Driver method
    let arr=[3, 1, 2, 5, 4 ];
    let k = 2;
    if (printPairs(arr, arr.length, k) == false)
            document.write("No such pair exists");

// This code is contributed by unknown2108

</script>
```

**输出:**

```
(2, 3) (2, 5) (5, 3) (2, 4)
```

**时间复杂度:** O(n* sqrt(max))其中 max 是数组中最大的元素。
**参考:**
[https://stackoverflow . com/questions/12732939/find-pairs-in-a B- k-where-k-是给定的整数](https://stackoverflow.com/questions/12732939/find-pairs-in-an-array-such-that-ab-k-where-k-is-a-given-integer)

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。