# 数组中 k 个最小素数和 k 个最大素数的和与积

> 原文:[https://www . geeksforgeeks . org/数组中 k 个最小素数和 k 个最大素数的和与积/](https://www.geeksforgeeks.org/sum-and-product-of-k-smallest-and-k-largest-prime-numbers-in-the-array/)

给定一个整数 *k* 和一个整数数组 *arr* ，任务是找出数组中最小的 *k* 和最大的 *k* 素数的和与积。
假设数组中至少有 *k* 个素数。
**举例:**

> **输入:** arr[] = {2，5，6，8，10，11}，k = 2
> **输出:**k-最小素数之和为 7
> k-最大素数之和为 16
> k-最小素数之积为 10
> k-最大素数之积为 55
> {2，5，11}是数组中唯一的素数。其中{2，5}最小，{5，11}最大。
> **输入:** arr[] = {4，2，12，13，5，19}，k = 3
> **输出:**k-最小素数之和为 20
> k-最大素数之和为 37
> k-最小素数之积为 130
> k-最大素数之积为 1235

**进场:**

1.  使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)从数组中生成一个达到最大元素大小的布尔向量，用于检查一个数是否是质数。
2.  同时将 *0* 和 *1* 设置为非质数，这样它们就不会被算作质数。
3.  现在遍历数组，插入两个[堆](https://www.geeksforgeeks.org/binary-heap/)中所有质数，一个最小堆和一个最大堆。
4.  现在，从*最小堆*中弹出顶部 *k* 元素，取最小 *k* 素数的*和*与*乘积*。
5.  对*最大堆*做同样的操作，得到最大 *k* 素数的*和*与*乘积*。
6.  最后，打印结果。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum
// and product of k smallest and
// k largest prime numbers in an array
#include <bits/stdc++.h>
using namespace std;

vector<bool> SieveOfEratosthenes(int max_val)
{
    // Create a boolean vector "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);
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

// Function that calculates the sum
// and product of k smallest and k
// largest prime numbers in an array
void primeSumAndProduct(int arr[], int n, int k)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    vector<bool> prime = SieveOfEratosthenes(max_val);

    // Set 0 and 1 as non-primes as
    // they don't need to be
    // counted as prime numbers
    prime[0] = false;
    prime[1] = false;

    // Max Heap to store all the prime numbers
    priority_queue<int> maxHeap;

    // Min Heap to store all the prime numbers
    priority_queue<int, vector<int>, greater<int>>
        minHeap;

    // Push all the prime numbers
    // from the array to the heaps
    for (int i = 0; i < n; i++)
        if (prime[arr[i]]) {
            minHeap.push(arr[i]);
            maxHeap.push(arr[i]);
        }
    long long int minProduct = 1
        , maxProduct = 1
        , minSum = 0
        , maxSum = 0;
    while (k--) {

        // Calculate the products
        minProduct *= minHeap.top();
        maxProduct *= maxHeap.top();

        // Calculate the sum
        minSum += minHeap.top();
        maxSum += maxHeap.top();

        // Pop the current minimum element
        minHeap.pop();

        // Pop the current maximum element
        maxHeap.pop();
    }

    cout << "Sum of k-minimum prime numbers is "
         << minSum << "\n";
    cout << "Sum of k-maximum prime numbers is "
         << maxSum << "\n";
    cout << "Product of k-minimum prime numbers is "
         << minProduct << "\n";
    cout << "Product of k-maximum prime numbers is "
         << maxProduct;
}

// Driver code
int main()
{

    int arr[] = { 4, 2, 12, 13, 5, 19 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 3;

    primeSumAndProduct(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// and product of k smallest and
// k largest prime numbers in an array
import java.util.*;

class GFG
{
    public static void main(String[] args)
    {
        int arr[] = { 4, 2, 12, 13, 5, 19 };
        int n = arr.length;
        int k = 3;
        primeSumAndProduct(arr, n, k);
    }

    static boolean[] SieveOfEratosthenes(int max_val)
    {
        // Create a boolean vector "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        boolean[] prime = new boolean[max_val + 1];
        for(int i = 0;i <= max_val ; i++)
        prime[i] = true;
        for (int p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true)
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
    // largest prime numbers in an array
    static void primeSumAndProduct(int arr[], int n, int k)
    {
        // Find maximum value in the array
        int max_val = 0;
        for (int i = 0; i < n; i++)
            max_val = Math.max(max_val, arr[i]);

        // Use sieve to find all prime numbers
        // less than or equal to max_val
        boolean[] prime = SieveOfEratosthenes(max_val);

        // Set 0 and 1 as non-primes as
        // they don't need to be
        // counted as prime numbers
        prime[0] = false;
        prime[1] = false;

        // Max Heap to store all the prime numbers
        PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(Collections.reverseOrder());

        // Min Heap to store all the prime numbers
        PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>();

        // Push all the prime numbers
        // from the array to the heaps
        for (int i = 0; i < n; i++)
            if (prime[arr[i]]) {
                minHeap.add(arr[i]);
                maxHeap.add(arr[i]);
            }

        long minProduct = 1, maxProduct = 1, minSum = 0, maxSum = 0;
        while (k > 0)
        {
            k--;

            // Calculate the products
            minProduct *= minHeap.peek();
            maxProduct *= maxHeap.peek();

            // Calculate the sum
            minSum += minHeap.peek();
            maxSum += maxHeap.peek();

            // Pop the current minimum element
            minHeap.remove();

            // Pop the current maximum element
            maxHeap.remove();
        }

        System.out.println("Sum of k-minimum prime numbers is " + minSum);
        System.out.println("Sum of k-maximum prime numbers is " + maxSum);
        System.out.println("Product of k-minimum prime numbers is " + minProduct);
        System.out.println("Product of k-maximum prime numbers is " + maxProduct);
    }

}

// This code is contributed by ankush_953
```

## 蟒蛇 3

```
# Python program to find the sum
# and product of k smallest and
# k largest prime numbers in an array
import heapq

def SieveOfEratosthenes(max_val):
    # Create a boolean vector "prime[0..n]". A
    # value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True for i in range(max_val+1)]
    p = 2
    while p*p <= max_val:
        # If prime[p] is not changed, then
        # it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for j in range(2*p,max_val+1,p):
                prime[j] = False
        p += 1

    return prime

# Function that calculates the sum
# and product of k smallest and k
# largest prime numbers in an array
def primeSumAndProduct(arr, n, k):
    # Find maximum value in the array
    max_val = max(arr)

    # Use sieve to find all prime numbers
    # less than or equal to max_val
    prime = SieveOfEratosthenes(max_val)

    # Set 0 and 1 as non-primes as
    # they don't need to be
    # counted as prime numbers
    prime[0] = False
    prime[1] = False

    # Heap to store all the prime numbers
    Heap = []

    # Push all the prime numbers
    # from the array to the heaps
    for i in range(n):
        if (prime[arr[i]]):
            Heap.append(arr[i])

    minProduct = 1
    maxProduct = 1
    minSum = 0
    maxSum = 0

    min_k = heapq.nsmallest(k,Heap)
    max_k = heapq.nlargest(k,Heap)

    minSum = sum(min_k)
    maxSum = sum(max_k)

    for val in min_k:
        minProduct *= val

    for val in max_k:
        maxProduct *= val

    print("Sum of k-minimum prime numbers is", minSum)
    print("Sum of k-maximum prime numbers is", maxSum)
    print("Product of k-minimum prime numbers is", minProduct)
    print("Product of k-maximum prime numbers is", maxProduct)

# Driver code
arr = [ 4, 2, 12, 13, 5, 19 ]
n = len(arr)
k = 3
primeSumAndProduct(arr, n, k)

# This code is contributed by ankush_953
```

**Output:** 

```
Sum of k-minimum prime numbers is 20
Sum of k-maximum prime numbers is 37
Product of k-minimum prime numbers is 130
Product of k-maximum prime numbers is 1235
```

***时间复杂度**:O(N * log(N)+max_val * log(log(max _ val)))*其中 N 为元素总数，max _ val 为数组中的最大值。
***辅助空间** : O(N + max_val)*