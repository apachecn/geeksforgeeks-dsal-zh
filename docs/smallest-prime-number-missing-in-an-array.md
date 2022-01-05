# 数组中缺少的最小素数

> 原文:[https://www . geesforgeks . org/minist-prime-number-in-a-array/](https://www.geeksforgeeks.org/smallest-prime-number-missing-in-an-array/)

给定一个包含 n 个不同数字的数组。任务是找到数组中不存在的最小素数。
**注意:**如果数组最大元素没有素数丢失，则打印“没有素数丢失”。
**示例:**

```
Input: arr[] = {9, 11, 4, 2, 3, 7, 0, 1}
Output: 5
5 is the smallest prime, which is not present in array.

Input: arr[] = {3, 0, 2, 5}
Output: No prime number missing
As 5 is the maximum element and all prime numbers upto 5 
are present in the array.
```

**方法:**首先使用厄拉多塞的[筛找出所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)，然后依次检查哪一个不存在。只需遍历数组，使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)检查数字是否存在。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// this store all prime number
// upto 10^5
// this function find all prime
vector<ll> findPrime(int MAX)
{
    bool pm[MAX + 1];
    memset(pm, true, sizeof(pm));

    // use sieve to find prime
    pm[0] = pm[1] = false;
    for (int i = 2; i <= MAX; i++)
        if (pm[i])
            for (int j = 2 * i; j <= MAX; j += i)
                pm[j] = false;

    // if number is prime then
    // store it in prime vector
    vector<ll> prime;
    for (int i = 0; i <= MAX; i++)
        if (pm[i])
            prime.push_back(i);

    return prime;
}

// Function to find the smallest prime missing
int findSmallest(int arr[], int n)
{
    int MAX = *max_element(arr, arr + n);

    // first of all find all prime
    vector<ll> prime = findPrime(MAX);

    // now store all number as index of freq arr
    // so that we can improve searching
    unordered_set<int> s;
    for (int i = 0; i < n; i++)
        s.insert(arr[i]);

    // now check for each prime
    int ans = -1;
    for (int i = 0; i < prime.size(); i++)
        if (s.find(prime[i]) == s.end()) {
            ans = prime[i];
            break;
        }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 3, 0, 1, 2, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // find smallest prime
    // which is not present
    if (findSmallest(arr, n) == -1)
        cout << "No prime number missing";
    else
        cout << findSmallest(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG {

    // this store all prime number
    // upto 10^5
    // this function find all prime
    static Vector<Integer> findPrime(int MAX)
    {
        boolean pm[] = new boolean[MAX + 1];
        for (int i = 0; i < pm.length; i++)
            pm[i] = true;

        // use sieve to find prime
        pm[0] = pm[1] = false;
        for (int i = 2; i <= MAX; i++)
            if (pm[i])
                for (int j = 2 * i; j <= MAX; j += i)
                    pm[j] = false;

        // if number is prime then
        // store it in prime vector
        Vector<Integer> prime = new Vector<Integer>();
        for (int i = 0; i <= MAX; i++)
            if (pm[i])
                prime.add(i);

        return prime;
    }

    static int max_element(int arr[])
    {
        int max = arr[0];

        for (int i = 0; i < arr.length; i++)
            max = Math.max(max, arr[i]);

        return max;
    }

    // Function to find the smallest prime missing
    static int findSmallest(int arr[], int n)
    {
        int MAX = max_element(arr);

        // first of all find all prime
        Vector<Integer> prime = findPrime(MAX);

        // now store all number as index of freq arr
        // so that we can improve searching
        Set<Integer> s = new HashSet<Integer>();
        for (int i = 0; i < arr.length; i++)
            s.add(arr[i]);

        // now check for each prime
        long ans = -1;
        for (int i = 0; i < prime.size(); i++) {
            if (!s.contains(prime.get(i))) {

                ans = (prime.get(i));
                break;
            }
        }
        return (int)ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 3, 0, 1, 2, 7 };
        int n = arr.length;

        // find smallest prime
        // which is not present
        if (findSmallest(arr, n) == -1)
            System.out.print("No prime number missing");
        else
            System.out.print(findSmallest(arr, n));
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# This function finds all
# prime numbers upto 10 ^ 5
def findPrime(MAX):

    pm = [True] * (MAX + 1)

    # use sieve to find prime
    pm[0], pm[1] = False, False

    for i in range(2, MAX + 1):
        if pm[i] == True:

            for j in range(2 * i, MAX + 1, i):
                pm[j] = False

    # If number is prime, then
    # store it in prime list
    prime = []
    for i in range(0, MAX + 1):
        if pm[i] == True:
            prime.append(i)

    return prime

# Function to find the smallest prime missing
def findSmallest(arr, n):

    MAX = max(arr)

    # first of all find all prime
    prime = findPrime(MAX)

    # now store all number as index of freq
    # arr so that we can improve searching
    s = set()
    for i in range(0, n):
        s.add(arr[i])

    # now check for each prime
    ans = -1
    for i in range(0, len(prime)):
        if prime[i] not in s:
            ans = prime[i]
            break

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [3, 0, 1, 2,  7]
    n = len(arr)

    # find smallest prime
    # which is not present
    if(findSmallest(arr, n) == -1):
        print("No prime number missing")
    else:
        print(findSmallest(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

    // this store all prime number
    // upto 10^5
    // this function find all prime
    static ArrayList findPrime(int MAX)
    {
        bool[] pm = new bool[MAX + 1];
        for (int i = 0; i < MAX + 1; i++)
            pm[i] = true;

        // use sieve to find prime
        pm[0] = pm[1] = false;
        for (int i = 2; i <= MAX; i++)
            if (pm[i])
                for (int j = 2 * i; j <= MAX; j += i)
                    pm[j] = false;

        // if number is prime then
        // store it in prime vector
        ArrayList prime = new ArrayList();
        for (int i = 0; i <= MAX; i++)
            if (pm[i])
                prime.Add(i);

        return prime;
    }

    static int max_element(int []arr)
    {
        int max = arr[0];

        for (int i = 0; i < arr.Length; i++)
            max = Math.Max(max, arr[i]);

        return max;
    }

    // Function to find the smallest prime missing
    static int findSmallest(int []arr, int n)
    {
        int MAX = max_element(arr);

        // first of all find all prime
        ArrayList prime = findPrime(MAX);

        // now store all number as index of freq arr
        // so that we can improve searching
        HashSet<int> s = new HashSet<int>();
        for (int i = 0; i < arr.Length; i++)
            s.Add(arr[i]);

        // now check for each prime
        int ans = -1;
        for (int i = 0; i < prime.Count; i++)
        {
            if (!s.Contains((int)prime[i]))
            {

                ans = (int)(prime[i]);
                break;
            }
        }
        return (int)ans;
    }

    // Driver code
    static void Main()
    {
        int []arr = { 3, 0, 1, 2, 7 };
        int n = arr.Length;

        // find smallest prime
        // which is not present
        if (findSmallest(arr, n) == -1)
            Console.Write("No prime number missing");
        else
            Console.Write(findSmallest(arr, n));
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// this store all prime number
// upto 10^5
// this function find all prime
function findPrime(MAX)
{
    let pm = new Array(MAX + 1);
    pm.fill(true);

    // use sieve to find prime
    pm[0] = pm[1] = false;
    for (let i = 2; i <= MAX; i++)
        if (pm[i])
            for (let j = 2 * i; j <= MAX; j += i)
                pm[j] = false;

    // if number is prime then
    // store it in prime vector
    let prime = new Array();
    for (let i = 0; i <= MAX; i++)
        if (pm[i])
            prime.push(i);

    return prime;
}

// Function to find the smallest prime missing
function findSmallest(arr, n) {
    let MAX = arr.sort((A, B) => A - B).reverse()[0];

    // first of all find all prime
    let prime = findPrime(MAX);

    // now store all number as index of freq arr
    // so that we can improve searching
    let s = new Set();
    for (let i = 0; i < n; i++)
        s.add(arr[i]);

    // now check for each prime
    let ans = -1;
    for (let i = 0; i < prime.length; i++){
        if (!s.has(prime[i])) {
            ans = prime[i];
            break;
        }
    }
    return ans;
}

// Driver code
let arr = [3, 0, 1, 2, 7];
let n = arr.length;

// find smallest prime
// which is not present
if (findSmallest(arr, n) == -1)
    document.write("No prime number missing");
else
    document.write(findSmallest(arr, n));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
5
```