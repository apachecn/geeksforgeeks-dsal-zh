# 具有复合频率的阵列中元素的总和

> 原文:[https://www . geeksforgeeks . org/数组元素之和-具有复合频率/](https://www.geeksforgeeks.org/sum-of-elements-in-an-array-having-composite-frequency/)

给定一个整数数组 **arr** 的大小 **N** ，任务是找出数组中具有[复合](https://www.geeksforgeeks.org/composite-number/)频率的元素的和。
**举例:**

> **输入:** arr[] = {1，2，1，1，1，3，3，2}
> **输出:** 1
> 1 出现 4 次，为复合。所有其他元素 2 和 3 出现 2 次，这是质数。所以，答案只是 1。
> **输入:** arr[] = {4，6，7}
> **输出:** 0
> 所有元素 4，6，7 出现 1 次，既不是素数也不是复合数。所以，答案是 0。

**进场:**

1.  遍历数组，将所有元素的频率存储在[图](http://geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  构建厄拉多塞的[筛，用于测试一个数在 O(1)时间内的素性。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
3.  使用上一步中计算的筛阵列计算具有复合频率的元素的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find sum of elements
// in an array having composite frequency
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// Function to create
// Sieve to check primes
void SieveOfEratosthenes(
    vector<bool>& composite)
{
    for (int i = 0; i < N; i++)
        composite[i] = false;

    for (int p = 2; p * p < N; p++) {

        // If composite[p] is not changed,
        // then it is a prime
        if (!composite[p]) {

            // Update all multiples of p,
            // set them to composite
            for (int i = p * 2; i < N; i += p)
                composite[i] = true;
        }
    }
}

// Function to return the sum of elements
// in an array having composite frequency
int sumOfElements(
    int arr[], int n)
{
    vector<bool> composite(N);

    SieveOfEratosthenes(composite);

    // Map is used to store
    // element frequencies
    unordered_map<int, int> m;
    for (int i = 0; i < n; i++)
        m[arr[i]]++;

    // To store sum
    int sum = 0;

    // Traverse the map using iterators
    for (auto it = m.begin();
         it != m.end(); it++) {

        // Count the number of elements
        // having composite frequencies
        if (composite[it->second]) {
            sum += (it->first);
        }
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 1, 1,
                  3, 3, 2, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << sumOfElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of elements
// in an array having composite frequency
import java.util.*;

class GFG{
static final int N = 10005;

// Function to create
// Sieve to check primes
static void SieveOfEratosthenes(Vector<Boolean> composite)
{
    for (int i = 0; i < N; i++)
    {
        composite.add(i, false);
    }

    for (int p = 2; p * p < N; p++) {

        // If composite[p] is not changed,
        // then it is a prime
        if (!composite.get(p)) {

            // Update all multiples of p,
            // set them to composite
            for (int i = p * 2; i < N; i += p) {
                composite.add(i, true);
            }
        }
    }
}

// Function to return the sum of elements
// in an array having composite frequency
static int sumOfElements(int arr[], int n)
{
    Vector<Boolean> composite = new Vector<Boolean>();
    for (int i = 0; i < N; i++)
        composite.add(false);
    SieveOfEratosthenes(composite);

    // Map is used to store
    // element frequencies
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();
    for (int i = 0; i < n; i++)
        if(mp.containsKey(arr[i])){
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else{
            mp.put(arr[i], 1);
        }

    // To store sum
    int sum = 0;

    // Traverse the map using iterators
    for (Map.Entry<Integer,Integer> it : mp.entrySet()){

        // Count the number of elements
        // having composite frequencies
        if (composite.get(it.getValue())) {
            sum += (it.getKey());
        }
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 1, 1, 1,
                3, 3, 2, 4 };

    int n = arr.length;

    // Function call
    System.out.print(sumOfElements(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find sum of elements
# in an array having composite frequency

N = 100005

# Function to create
# Sieve to check primes
def SieveOfEratosthenes(composite):

    for p in range(2, N):
        if p*p > N:
            break

        # If composite[p] is not changed,
        # then it is a prime
        if (composite[p] == False):

            # Update all multiples of p,
            # set them to composite
            for i in range(2*p, N, p):
                composite[i] = True

# Function to return the sum of elements
# in an array having composite frequency
def sumOfElements(arr, n):
    composite = [False] * N

    SieveOfEratosthenes(composite)

    # Map is used to store
    # element frequencies
    m = dict();
    for i in range(n):
        m[arr[i]] = m.get(arr[i], 0) + 1

    # To store sum
    sum = 0

    # Traverse the map using iterators
    for it in m:

        # Count the number of elements
        # having composite frequencies
        if (composite[m[it]]):
            sum += (it)

    return sum

# Driver code
if __name__ == '__main__':
    arr=[1, 2, 1, 1, 1,3, 3, 2, 4]

    n = len(arr)

    # Function call
    print(sumOfElements(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find sum of elements
// in an array having composite frequency
using System;
using System.Collections.Generic;

class GFG{
static readonly int N = 10005;

// Function to create
// Sieve to check primes
static void SieveOfEratosthenes(List<Boolean> composite)
{
    for (int i = 0; i < N; i++)
    {
        composite.Insert(i, false);
    }

    for (int p = 2; p * p < N; p++) {

        // If composite[p] is not changed,
        // then it is a prime
        if (!composite[p]) {

            // Update all multiples of p,
            // set them to composite
            for (int i = p * 2; i < N; i += p) {
                composite.Insert(i, true);
            }
        }
    }
}

// Function to return the sum of elements
// in an array having composite frequency
static int sumOfElements(int []arr, int n)
{
    List<Boolean> composite = new List<Boolean>();
    for (int i = 0; i < N; i++)
        composite.Add(false);
    SieveOfEratosthenes(composite);

    // Map is used to store
    // element frequencies
    Dictionary<int,int> mp = new Dictionary<int,int>();
    for (int i = 0; i < n; i++)
        if(mp.ContainsKey(arr[i])){
            mp[arr[i]] =  mp[arr[i]] + 1;
        }
        else{
            mp.Add(arr[i], 1);
        }

    // To store sum
    int sum = 0;

    // Traverse the map using iterators
    foreach (KeyValuePair<int,int> it in mp){

        // Count the number of elements
        // having composite frequencies
            if (composite[it.Value]) {
                sum += (it.Key);
        }
    }

    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 1, 1, 1,
                3, 3, 2, 4 };

    int n = arr.Length;

    // Function call
    Console.Write(sumOfElements(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find sum of elements
// in an array having composite frequency

let N = 100005

// Function to create
// Sieve to check primes
function SieveOfEratosthenes(composite)
{
    for (let i = 0; i < N; i++)
        composite[i] = false;

    for (let p = 2; p * p < N; p++) {

        // If composite[p] is not changed,
        // then it is a prime
        if (!composite[p]) {

            // Update all multiples of p,
            // set them to composite
            for (let i = p * 2; i < N; i += p)
                composite[i] = true;
        }
    }
}

// Function to return the sum of elements
// in an array having composite frequency
function sumOfElements(arr, n)
{
    let composite = new Array(N);

    SieveOfEratosthenes(composite);
    // Map is used to store
    // element frequencies
    let m = new Map();

    for (let i = 0; i < n; i++)
    if(m.has(arr[i])){
        m[arr[i]] =  m[arr[i]] + 1;
    }
    else{
        m.set(arr[i], 1);
    }

    // To store sum
    let sum = 0;

    // Traverse the map using iterators

        m.forEach((value, key)=>{
            // Count the number of elements
            // having composite frequencies
                if (composite[key]) {
                    sum += value;
            }
      })

    return sum;
}

// Driver code

let arr = [ 1, 2, 1, 1, 1,
            3, 3, 2, 4 ];

let n = arr.length;

// Function call
document.write(sumOfElements(arr, n));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
1
```

时间复杂度:O(N <sup>3/2</sup> )

辅助空间:O(N)