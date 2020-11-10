# 来自给定数组的`K`个最大质数和合数的 XOR

> 原文：[https://www.geeksforgeeks.org/xor-of-k-largest-prime-and-composite-numbers-from-the-given-array/](https://www.geeksforgeeks.org/xor-of-k-largest-prime-and-composite-numbers-from-the-given-array/)



给定`N`个非零正整数的数组`arr[]`和一个整数`K`，任务是找到`K`个最大质数和合数的 XOR。

**示例**：

> **输入**：`arr[] = {4, 2, 12, 13, 5, 19}, K = 3`
>
> **输出**：
>
> 质数`XOR = 27`
>
> 合数`XOR = 8`
>
> 5、13 和 19 是给定数组中的三个最大质数，`5 XOR 13 XOR 19 = 27`。
>
> 数组中只有 2 个合数，即 4 和 12，`4 XOR 12 = 8`
> 
> **输入**：`arr[] = {1, 2, 3, 4, 5, 6, 7}, K = 1`
>
> **输出**：
>
> 质数`XOR = 7`
>
> 合数`XOR = 6`

**方法**：使用 [Eratosthenes 筛网](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成一个布尔向量，该布尔向量达到数组中最大元素的大小，该布尔向量可用于检查数字是否为质数。

现在遍历数组，并在最大堆 **maxHeapPrime** 中插入所有质数，并在最大堆 **maxHeapNonPrime** 中插入所有组合数。

现在，从两个最大堆中弹出顶部的 **K** 个元素，并对这些元素进行异或。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function for Sieve of Eratosthenes 
vector<bool> SieveOfEratosthenes(int max_val) 
{ 
    // Create a boolean vector "prime[0..n]". A 
    // value in prime[i] will finally be false 
    // if i is Not a prime, else true. 
    vector<bool> prime(max_val + 1, true); 

    // Set 0 and 1 as non-primes as 
    // they don't need to be 
    // counted as prime numbers 
    prime[0] = false; 
    prime[1] = false; 

    for (int p = 2; p * p <= max_val; p++) { 

        // If prime[p] is not changed, then 
        // it is a prime 
        if (prime[p] == true) { 

            // Update all multiples of p 
            for (int i = p * 2; i <= max_val; i += p) 
                prime[i] = false; 
        } 
    } 
    return prime; 
} 

// Function that calculates the xor 
// of k smallest and k 
// largest prime numbers in an array 
void kMaxXOR(int arr[], int n, int k) 
{ 
    // Find maximum value in the array 
    int max_val = *max_element(arr, arr + n); 

    // Use sieve to find all prime numbers 
    // less than or equal to max_val 
    vector<bool> prime = SieveOfEratosthenes(max_val); 

    // Min Heaps to store the max K prime 
    // and composite numbers 
    priority_queue<int, vector<int>, greater<int> > 
        minHeapPrime, minHeapNonPrime; 

    for (int i = 0; i < n; i++) { 

        // If current element is prime 
        if (prime[arr[i]]) { 

            // Min heap will only store k elements 
            if (minHeapPrime.size() < k) 
                minHeapPrime.push(arr[i]); 

            // If the size of min heap is K and the 
            // top element is smaller than the current 
            // element than it needs to be replaced 
            // by the current element as only 
            // max k elements are required 
            else if (minHeapPrime.top() < arr[i]) { 
                minHeapPrime.pop(); 
                minHeapPrime.push(arr[i]); 
            } 
        } 

        // If current element is composite 
        else if (arr[i] != 1) { 

            // Heap will only store k elements 
            if (minHeapNonPrime.size() < k) 
                minHeapNonPrime.push(arr[i]); 

            // If the size of min heap is K and the 
            // top element is smaller than the current 
            // element than it needs to be replaced 
            // by the current element as only 
            // max k elements are required 
            else if (minHeapNonPrime.top() < arr[i]) { 
                minHeapNonPrime.pop(); 
                minHeapNonPrime.push(arr[i]); 
            } 
        } 
    } 

    long long int primeXOR = 0, nonPrimeXor = 0; 
    while (k--) { 

        // Calculate the xor 
        if (minHeapPrime.size() > 0) { 
            primeXOR ^= minHeapPrime.top(); 
            minHeapPrime.pop(); 
        } 

        if (minHeapNonPrime.size() > 0) { 
            nonPrimeXor ^= minHeapNonPrime.top(); 
            minHeapNonPrime.pop(); 
        } 
    } 

    cout << "Prime XOR = " << primeXOR << "\n"; 
    cout << "Composite XOR = " << nonPrimeXor << "\n"; 
} 

// Driver code 
int main() 
{ 

    int arr[] = { 4, 2, 12, 13, 5, 19 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 

    kMaxXOR(arr, n, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
import java.util.*; 

class GFG  
{ 

    // Function for Sieve of Eratosthenes 
    static boolean[] SieveOfEratosThenes(int max_val) 
    { 

        // Create a boolean vector "prime[0..n]". A 
        // value in prime[i] will finally be false 
        // if i is Not a prime, else true. 
        boolean[] prime = new boolean[max_val + 1]; 
        Arrays.fill(prime, true); 

        // Set 0 and 1 as non-primes as 
        // they don't need to be 
        // counted as prime numbers 
        prime[0] = false; 
        prime[1] = false; 

        for (int p = 2; p * p <= max_val; p++) 
        { 

            // If prime[p] is not changed, then 
            // it is a prime 
            if (prime[p])  
            { 

                // Update all multiples of p 
                for (int i = p * 2; i <= max_val; i += p) 
                    prime[i] = false; 
            } 
        } 
        return prime; 
    } 

    // Function that calculates the xor 
    // of k smallest and k 
    // largest prime numbers in an array 
    static void kMinXOR(Integer[] arr, int n, int k)  
    { 

        // Find maximum value in the array 
        int max_val = Collections.max(Arrays.asList(arr)); 

        // Use sieve to find all prime numbers 
        // less than or equal to max_val 
        boolean[] prime = SieveOfEratosThenes(max_val); 

        // Min Heaps to store the max K prime 
        // and composite numbers 
        PriorityQueue<Integer> minHeapPrime = new PriorityQueue<>(); 
        PriorityQueue<Integer> minHeapNonPrime = new PriorityQueue<>(); 

        for (int i = 0; i < n; i++) 
        { 

            // If current element is prime 
            if (prime[arr[i]])  
            { 

                // Min heap will only store k elements 
                if (minHeapPrime.size() < k) 
                    minHeapPrime.add(arr[i]); 

                // If the size of min heap is K and the 
                // top element is smaller than the current 
                // element than it needs to be replaced 
                // by the current element as only 
                // max k elements are required 
                else if (minHeapPrime.peek() < arr[i]) 
                { 
                    minHeapPrime.poll(); 
                    minHeapPrime.add(arr[i]); 
                } 
            } 

            // If current element is composite 
            else if (arr[i] != -1) 
            { 

                // Heap will only store k elements 
                if (minHeapNonPrime.size() < k) 
                    minHeapNonPrime.add(arr[i]); 

                // If the size of min heap is K and the 
                // top element is smaller than the current 
                // element than it needs to be replaced 
                // by the current element as only 
                // max k elements are required 
                else if (minHeapNonPrime.peek() < arr[i])  
                { 
                    minHeapNonPrime.poll(); 
                    minHeapNonPrime.add(arr[i]); 
                } 
            } 
        } 

        long primeXOR = 0, nonPrimeXor = 0; 

        while (k-- > 0)  
        { 

            // Calculate the xor 
            if (minHeapPrime.size() > 0) 
            { 
                primeXOR ^= minHeapPrime.peek(); 
                minHeapPrime.poll(); 
            } 

            if (minHeapNonPrime.size() > 0)  
            { 
                nonPrimeXor ^= minHeapNonPrime.peek(); 
                minHeapNonPrime.poll(); 
            } 
        } 

        System.out.println("Prime XOR = " + primeXOR); 
        System.out.println("Composite XOR = " + nonPrimeXor); 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        Integer[] arr = { 4, 2, 12, 13, 5, 19 }; 
        int n = arr.length; 
        int k = 3; 

        kMinXOR(arr, n, k); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python implimentation of above approach 

import heapq 

# Function for Sieve of Eratosthenes 
def SieveOfEratosthenes(max_val: int) -> list: 

    # Create a boolean vector "prime[0..n]". A 
    # value in prime[i] will finally be false 
    # if i is Not a prime, else true. 
    prime = [True] * (max_val + 1) 

    # Set 0 and 1 as non-primes as 
    # they don't need to be 
    # counted as prime numbers 
    prime[0] = False
    prime[1] = False

    p = 2
    while p * p <= max_val: 

        # If prime[p] is not changed, then 
        # it is a prime 
        if prime[p]: 

            # Update all multiples of p 
            for i in range(p * 2, max_val + 1, p): 
                prime[i] = False
        p += 1
    return prime 

# Function that calculates the xor 
# of k smallest and k 
# largest prime numbers in an array 
def kMaxXOR(arr: list, n: int, k: int): 

    # Find maximum value in the array 
    max_val = max(arr) 

    # Use sieve to find all prime numbers 
    # less than or equal to max_val 
    prime = SieveOfEratosthenes(max_val) 

    # Min Heaps to store the max K prime 
    # and composite numbers 
    minHeapPrime, minHeapNonPrime = [], [] 
    heapq.heapify(minHeapPrime) 
    heapq.heapify(minHeapNonPrime) 

    for i in range(n): 

        # If current element is prime 
        if prime[arr[i]]: 

            # Min heap will only store k elements 
            if len(minHeapPrime) < k: 
                heapq.heappush(minHeapPrime, arr[i]) 

            # If the size of min heap is K and the 
            # top element is smaller than the current 
            # element than it needs to be replaced 
            # by the current element as only 
            # max k elements are required 
            elif heapq.nsmallest(1, minHeapPrime)[0] < arr[i]: 
                heapq.heappop(minHeapPrime) 
                heapq.heappush(minHeapPrime, arr[i]) 

        # If current element is composite 
        elif arr[i] != 1: 

            # Heap will only store k elements 
            if len(minHeapNonPrime) < k: 
                heapq.heappush(minHeapNonPrime, arr[i]) 

            # If the size of min heap is K and the 
            # top element is smaller than the current 
            # element than it needs to be replaced 
            # by the current element as only 
            # max k elements are required 
            elif heapq.nsmallest(1, minHeapNonPrime)[0] < arr[i]: 
                heapq.heappop(minHeapNonPrime) 
                heapq.heappush(minHeapNonPrime, arr[i]) 

    primeXOR = 0
    nonPrimeXor = 0

    while k > 0: 

        # Calculate the xor 
        if len(minHeapPrime) > 0: 
            primeXOR ^= heapq.nsmallest(1, minHeapPrime)[0] 
            heapq.heappop(minHeapPrime) 

        if len(minHeapNonPrime) > 0: 
            nonPrimeXor ^= heapq.nsmallest(1, minHeapNonPrime)[0] 
            heapq.heappop(minHeapNonPrime) 
        k -= 1

    print("Prime XOR =", primeXOR) 
    print("Composite XOR =", nonPrimeXor) 

# Driver Code 
if __name__ == "__main__": 

    arr = [4, 2, 12, 13, 5, 19] 
    n = len(arr) 
    k = 3
    kMaxXOR(arr, n, k) 

# This code is contributed by 
# sanjeev2552 

```

**输出**：

```
Prime XOR = 27
Composite XOR = 8

```



* * *

* * *



