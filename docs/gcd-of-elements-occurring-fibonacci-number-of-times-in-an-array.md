# 数组中出现斐波那契次数的元素的 GCD

> 原文:[https://www . geesforgeks . org/gcd-of-elements-occurrent-Fibonacci-数组中的次数/](https://www.geeksforgeeks.org/gcd-of-elements-occurring-fibonacci-number-of-times-in-an-array/)

给定一个包含 **N** 元素的数组 **arr[]** ，任务是找到具有频率计数的元素的 [GCD](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，该频率计数是数组中的[斐波那契数](http://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**举例:**

> **输入:** arr[] = { 5，3，6，5，6，6，5，5 }
> **输出:** 3
> **解释:**
> 元素 5，3，6 分别出现 4，1，3 次。
> 因此，3 和 6 具有斐波那契频率。
> 所以，gcd(3，6) = 1
> **输入:** arr[] = {4，2，3，3，3，3}
> **输出:** 2
> **解释:**
> 元素 4，2，3 分别出现 1，1，4 次。
> 因此，4 和 2 有斐波那契频率。
> 所以，gcd(4，2) = 2

**方法:**想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)来预计算并存储[斐波那契节点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)直到最大值，以使检查变得容易且高效(在 O(1)时间内)。
预计算[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)后:

1.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并将所有元素的频率存储在[图](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  使用映射和散列，使用预先计算的散列计算具有斐波那契频率的元素的 [gcd](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。

以下是上述方法的实现:

## C++

```
// C++ program to find the GCD of
// elements which occur Fibonacci
// number of times

#include <bits/stdc++.h>
using namespace std;

// Function to create hash table
// to check Fibonacci numbers
void createHash(set<int>& hash,
                int maxElement)
{
    // Inserting the first two
    // numbers into the hash
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    // Adding the remaining Fibonacci
    // numbers using the previously
    // added elements
    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the GCD of elements
// in an array having fibonacci frequency
int gcdFibonacciFreq(int arr[], int n)
{
    set<int> hash;

    // Creating the hash
    createHash(hash,
               *max_element(arr,
                            arr + n));

    int i, j;

    // Map is used to store the
    // frequencies of the elements
    unordered_map<int, int> m;

    // Iterating through the array
    for (i = 0; i < n; i++)
        m[arr[i]]++;

    int gcd = 0;

    // Traverse the map using iterators
    for (auto it = m.begin();
         it != m.end(); it++) {

        // Calculate the gcd of elements
        // having fibonacci frequencies
        if (hash.find(it->second)
            != hash.end()) {
            gcd = __gcd(gcd,
                        it->first);
        }
    }

    return gcd;
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 6, 5,
                  6, 6, 5, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << gcdFibonacciFreq(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the GCD of
// elements which occur Fibonacci
// number of times
import java.util.*;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<Integer> hash,
                int maxElement)
{
    // Inserting the first two
    // numbers into the hash
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Adding the remaining Fibonacci
    // numbers using the previously
    // added elements
    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the GCD of elements
// in an array having fibonacci frequency
static int gcdFibonacciFreq(int arr[], int n)
{
    HashSet<Integer> hash = new HashSet<Integer>();

    // Creating the hash
    createHash(hash,Arrays.stream(arr).max().getAsInt());

    int i;

    // Map is used to store the
    // frequencies of the elements
    HashMap<Integer,Integer> m = new HashMap<Integer,Integer>();

    // Iterating through the array
    for (i = 0; i < n; i++) {
        if(m.containsKey(arr[i])){
            m.put(arr[i], m.get(arr[i])+1);
        }
        else{
            m.put(arr[i], 1);
        }
    }

    int gcd = 0;

    // Traverse the map using iterators
    for (Map.Entry<Integer, Integer> it : m.entrySet()) {

        // Calculate the gcd of elements
        // having fibonacci frequencies
        if (hash.contains(it.getValue())) {
            gcd = __gcd(gcd,
                        it.getKey());
        }
    }

    return gcd;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 3, 6, 5,
                  6, 6, 5, 5 };
    int n = arr.length;

    System.out.print(gcdFibonacciFreq(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program to find the GCD of
# elements which occur Fibonacci
# number of times
from collections import defaultdict
import math

# Function to create hash table
# to check Fibonacci numbers
def createHash(hash1,maxElement):

    # Inserting the first two
    # numbers into the hash
    prev , curr = 0, 1
    hash1.add(prev)
    hash1.add(curr)

    # Adding the remaining Fibonacci
    # numbers using the previously
    # added elements
    while (curr <= maxElement):
        temp = curr + prev
        if temp <= maxElement:
            hash1.add(temp)
        prev = curr
        curr = temp

# Function to return the GCD of elements
# in an array having fibonacci frequency
def gcdFibonacciFreq(arr, n):

    hash1 = set()

    # Creating the hash
    createHash(hash1,max(arr))

    # Map is used to store the
    # frequencies of the elements
    m = defaultdict(int)

    # Iterating through the array
    for i in range(n):
        m[arr[i]] += 1

    gcd = 0

    # Traverse the map using iterators
    for it in m.keys():

        # Calculate the gcd of elements
        # having fibonacci frequencies
        if (m[it] in hash1):
            gcd = math.gcd(gcd,it)
    return gcd

# Driver code
if __name__ == "__main__":

    arr = [ 5, 3, 6, 5,
                  6, 6, 5, 5 ]
    n = len(arr)

    print(gcdFibonacciFreq(arr, n))

 # This code is contributed by chitranayal
```

## C#

```
// C# program to find the GCD of
// elements which occur Fibonacci
// number of times
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<int> hash,
                int maxElement)
{
    // Inserting the first two
    // numbers into the hash
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    // Adding the remaining Fibonacci
    // numbers using the previously
    // added elements
    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the GCD of elements
// in an array having fibonacci frequency
static int gcdFibonacciFreq(int []arr, int n)
{
    HashSet<int> hash = new HashSet<int>();

    // Creating the hash
    createHash(hash, hash.Count > 0 ? hash.Max():0);

    int i;

    // Map is used to store the
    // frequencies of the elements
    Dictionary<int,int> m = new Dictionary<int,int>();

    // Iterating through the array
    for (i = 0; i < n; i++) {
        if(m.ContainsKey(arr[i])){
            m[arr[i]] = m[arr[i]] + 1;
        }
        else{
            m.Add(arr[i], 1);
        }
    }

    int gcd = 0;

    // Traverse the map using iterators
    foreach(KeyValuePair<int, int> it in m) {

        // Calculate the gcd of elements
        // having fibonacci frequencies
        if (hash.Contains(it.Value)) {
            gcd = __gcd(gcd,
                        it.Key);
        }
    }

    return gcd;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 3, 6, 5,
                  6, 6, 5, 5 };
    int n = arr.Length;

    Console.Write(gcdFibonacciFreq(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the GCD of
// elements which occur Fibonacci
// number of times

// Function to create hash table
// to check Fibonacci numbers
function createHash(hash, maxElement)
{
    // Inserting the first two
    // numbers into the hash
    let prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Adding the remaining Fibonacci
    // numbers using the previously
    // added elements
    while (curr <= maxElement) {
        let temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the GCD of elements
// in an array having fibonacci frequency
function gcdFibonacciFreq(arr, n)
{
    let hash = new Set();

    // Creating the hash
    createHash(hash, arr.sort((a, b) => b - a)[0]);

    let i, j;

    // Map is used to store the
    // frequencies of the elements
    let m = new Map();

    // Iterating through the array
    for (i = 0; i < n; i++){
        if(m.has(arr[i])){
            m.set(arr[i], m.get(arr[i]) + 1)
        }else{
            m.set(arr[i], 1)
        }
    }

    let gcd = 0;

    // Traverse the map using iterators
    for (let it of m) {

        // Calculate the gcd of elements
        // having fibonacci frequencies
        if (hash.has(it[1])) {
            gcd = __gcd(gcd, it[0]);
        }
    }

    return gcd;
}

function __gcd(a, b) 
{ 
    return (b == 0? a:__gcd(b, a % b));    
}

// Driver code

let arr = [ 5, 3, 6, 5,
            6, 6, 5, 5 ];
let n = arr.length;

document.write(gcdFibonacciFreq(arr, n));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
3
```

时间复杂度:0(N)

辅助空间:O(N)