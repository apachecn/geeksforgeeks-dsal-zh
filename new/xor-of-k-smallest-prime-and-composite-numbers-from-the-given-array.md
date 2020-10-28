# 来自给定数组

的 K 个最小素数和复合数的 XOR

给定 **N** 个非零正整数的数组 **arr []** 和一个整数 **K** ，任务是找到 **K [XOR]。** 最大质数和复合数。

**示例**：

> **输入**：arr [] = {4、2、12、13、5、19}，K = 3
> **输出**：
> 原始 XOR = 10
> 复合 XOR = 8
> 2，5 和 13 是给定数组中的三个最大素数
> ，2 ^ 5 ^ 13 =10。
> 数组中只有 2 个复合素，即 4 和 12。
> 和 4 ^ 12 = 8
> 
> **输入**：arr [] = {1、2、3、4、5、6、7}，K = 1
> **输出**：
> 主 XOR = 2 [
> 复合 XOR = 4

**方法**：使用 [Eratosthenes 筛网](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成一个布尔向量，该布尔向量达到数组中最大元素的大小，该布尔向量可用于检查数字是否为质数。

现在遍历数组，并在 min 堆 **minHeapPrime** 中插入所有质数，并在 min 堆 **minHeapNonPrime** 中插入所有组合数字。

现在，从两个最小堆中弹出顶部的 **K** 个元素，并对这些元素进行异或。

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
void kMinXOR(int arr[], int n, int k) 
{ 
    // Find maximum value in the array 
    int max_val = *max_element(arr, arr + n); 

    // Use sieve to find all prime numbers 
    // less than or equal to max_val 
    vector<bool> prime = SieveOfEratosthenes(max_val); 

    // Max Heaps to store all the 
    // prime and composite numbers 
    priority_queue<int> maxHeapPrime, maxHeapNonPrime; 

    for (int i = 0; i < n; i++) { 

        // If current element is prime  
        if (prime[arr[i]]) { 

            // Max heap will only store k elements 
            if (maxHeapPrime.size() < k)  
                maxHeapPrime.push(arr[i]);  

            // If the size of max heap is K and the  
            // top element is greater than the current  
            // element than it needs to be replaced  
            // by the current element as only  
            // minimum k elements are required  
            else if (maxHeapPrime.top() > arr[i]) {  
                maxHeapPrime.pop();  
                maxHeapPrime.push(arr[i]);  
            } 
        } 

        // If current element is composite 
        else if (arr[i] != 1) { 

            // Heap will only store k elements  
            if (maxHeapNonPrime.size() < k)  
                maxHeapNonPrime.push(arr[i]);  

            // If the size of max heap is K and the  
            // top element is greater than the current  
            // element than it needs to be replaced  
            // by the current element as only  
            // minimum k elements are required  
            else if (maxHeapNonPrime.top() > arr[i]) {  
                maxHeapNonPrime.pop();  
                maxHeapNonPrime.push(arr[i]);  
            } 
        } 
    } 

    long long int primeXOR = 0, nonPrimeXor = 0; 
    while (k--) { 

        // Calculate the xor 
        if (maxHeapPrime.size() > 0) { 
            primeXOR ^= maxHeapPrime.top(); 
            maxHeapPrime.pop(); 
        } 

        if (maxHeapNonPrime.size() > 0) { 
            nonPrimeXor ^= maxHeapNonPrime.top(); 
            maxHeapNonPrime.pop(); 
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

    kMinXOR(arr, n, k); 

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

    // Function that calculates the sum 
    // and product of k smallest and k 
    // largest composite numbers in an array 
    static void kMinXOR(Integer[] arr, int n, int k)  
    { 

        // Find maximum value in the array 
        int max_val = Collections.max(Arrays.asList(arr)); 

        // Use sieve to find all prime numbers 
        // less than or equal to max_val 
        boolean[] prime = SieveOfEratosThenes(max_val); 

        // Max Heap to store all the prime and composite numbers 
        PriorityQueue<Integer> maxHeapPrime =  
                           new PriorityQueue<Integer>((x, y) -> y - x); 
        PriorityQueue<Integer> maxHeapNonPrime =  
                           new PriorityQueue<Integer>((x, y) -> y - x); 

        for (int i = 0; i < n; i++)  
        { 

            // If current element is prime 
            if (prime[arr[i]])  
            { 

                // Max heap will only store k elements 
                if (maxHeapPrime.size() < k) 
                    maxHeapPrime.add(arr[i]); 

                // If the size of max heap is K and the 
                // top element is greater than the current 
                // element than it needs to be replaced 
                // by the current element as only 
                // minimum k elements are required 
                else if (maxHeapPrime.peek() > arr[i])  
                { 
                    maxHeapPrime.poll(); 
                    maxHeapPrime.add(arr[i]); 
                } 
            } 

            // If current element is composite 
            else if (arr[i] != -1)  
            { 

                // Heap will only store k elements 
                if (maxHeapNonPrime.size() < k) 
                    maxHeapNonPrime.add(arr[i]); 

                // If the size of max heap is K and the 
                // top element is greater than the current 
                // element than it needs to be replaced 
                // by the current element as only 
                // minimum k elements are required 
                else if (maxHeapNonPrime.peek() > arr[i]) 
                { 
                    maxHeapNonPrime.poll(); 
                    maxHeapNonPrime.add(arr[i]); 
                } 
            } 
        } 

        long primeXOR = 0, nonPrimeXor = 0; 

        while (k-- > 0)  
        { 

            // Calculate the xor 
            if (maxHeapPrime.size() > 0)  
            { 
                primeXOR ^= maxHeapPrime.peek(); 
                maxHeapPrime.poll(); 
            } 

            if (maxHeapNonPrime.size() > 0)  
            { 
                nonPrimeXor ^= maxHeapNonPrime.peek(); 
                maxHeapNonPrime.poll(); 
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

## Python 3

```

from math import sqrt 
# Python 3 implementation of the approach 

# Function for Sieve of Eratosthenes 
def SieveOfEratosthenes(max_val): 

    # Create a boolean vector "prime[0..n]". A 
    # value in prime[i] will finally be false 
    # if i is Not a prime, else true. 
    prime = [True for i in range(max_val + 1)] 

    # Set 0 and 1 as non-primes as 
    # they don't need to be 
    # counted as prime numbers 
    prime[0] = False
    prime[1] = False

    for p in range(2,int(sqrt(max_val)) + 1, 1): 

        # If prime[p] is not changed, then 
        # it is a prime 
        if (prime[p] == True): 

            # Update all multiples of p 
            for i in range(p * 2,max_val+1,p): 
                prime[i] = False

    return prime 

# Function that calculates the xor 
# of k smallest and k 
# largest prime numbers in an array 
def kMinXOR(arr, n, k): 

    # Find maximum value in the array 
    max_val = max(arr) 

    # Use sieve to find all prime numbers 
    # less than or equal to max_val 
    prime = SieveOfEratosthenes(max_val) 

    # Max Heaps to store all the 
    # prime and composite numbers 
    maxHeapPrime = [] 
    maxHeapNonPrime = [] 

    for i in range(n): 

        # If current element is prime  
        if (prime[arr[i]]): 

            # Max heap will only store k elements 
            if (len(maxHeapPrime) < k): 
                maxHeapPrime.append(arr[i])  
                maxHeapPrime.sort(reverse = True) 

            # If the size of max heap is K and the  
            # top element is greater than the current  
            # element than it needs to be replaced  
            # by the current element as only  
            # minimum k elements are required  
            elif(maxHeapPrime[0] > arr[i]): 
                maxHeapPrime.remove(maxHeapPrime[0])  
                maxHeapPrime.append(arr[i]) 
                maxHeapPrime.sort(reverse = True) 

        # If current element is composite 
        elif(arr[i] != 1): 

            # Heap will only store k elements  
            if (len(maxHeapNonPrime) < k): 
                maxHeapNonPrime.append(arr[i]) 
                maxHeapNonPrime.sort(reverse = True)  

            # If the size of max heap is K and the  
            # top element is greater than the current  
            # element than it needs to be replaced  
            # by the current element as only  
            # minimum k elements are required  
            elif(maxHeapNonPrime[0] > arr[i]): 
                maxHeapNonPrime.remove(maxHeapNonPrime[0])  
                maxHeapNonPrime.append(arr[i]) 
                maxHeapNonPrime.sort(reverse = True) 

    primeXOR = 0
    nonPrimeXor = 0
    while (k): 

        # Calculate the xor 
        if (len(maxHeapPrime) > 0): 
            primeXOR ^= maxHeapPrime[0] 
            maxHeapPrime.remove(maxHeapPrime[0]) 

        if (len(maxHeapNonPrime) > 0): 
            nonPrimeXor ^= maxHeapNonPrime[0]; 
            maxHeapNonPrime.remove(maxHeapNonPrime[0]) 

        k -= 1

    print("Prime XOR = ",primeXOR) 
    print("Composite XOR = ",nonPrimeXor) 

# Driver code 
if __name__ == '__main__': 
    arr = [4, 2, 12, 13, 5, 19] 
    n = len(arr) 
    k = 3

    kMinXOR(arr, n, k); 

# This code is contributed by Surendra_Gangwar 

```

**Output:**

```
Prime XOR = 10
Composite XOR = 8

```



* * *

* * *



