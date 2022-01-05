# 数组中 k 个最小和 k 个最大合成数的和与积

> 原文:[https://www . geesforgeks . org/k 最小和 k 最大组合数组中的数字之和与乘积/](https://www.geeksforgeeks.org/sum-and-product-of-k-smallest-and-k-largest-composite-numbers-in-the-array/)

给定一个整数 *k* 和一个整数数组 *arr* ，任务是找出数组中最小的 *k* 和最大的 *k* 的和与积。
假设数组中至少有 *k* 个复合数。
**举例:**

> **输入:** arr[] = {2，5，6，8，10，11}，k = 2
> **输出:**k-最小合成数之和为 14
> k-最大合成数之和为 18
> k-最小合成数之积为 48
> k-最大合成数之积为 80
> {6，8，10}是数组中唯一的合成数。其中{6，8}最小，{8，10}最大。
> **输入:** arr[] = {6，4，2，12，13，5，19，10}，k = 3
> **输出:**k-最小合成数之和为 20
> k-最大合成数之和为 28
> k-最小合成数之积为 240
> k-最大合成数之积为 720

**进场:**

1.  使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)从数组中生成一个达到最大元素大小的布尔向量，该向量可用于检查一个数是否是复合数。
2.  同时将 *0* 和 *1* 设置为质数，这样它们就不会被算作复合数。
3.  现在遍历数组，将所有组合在两个[堆](https://www.geeksforgeeks.org/binary-heap/)中的数字插入，一个最小堆和一个最大堆。
4.  现在，从*最小堆*中弹出顶部 *k* 元素，取最小 *k* 组合数的*和*与*乘积*。
5.  对*最大堆*做同样的操作，得到最大 *k* 复合数的*和*与*乘积*。
6.  最后，打印结果。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum and
// product of k smallest and k largest
// composite numbers in an array
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
// largest composite numbers in an array
void compositeSumAndProduct(int arr[], int n, int k)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    vector<bool> prime = SieveOfEratosthenes(max_val);

    // Set 0 and 1 as primes so that
    // they don't get counted as
    // composite numbers
    prime[0] = true;
    prime[1] = true;

    // Max Heap to store all the composite numbers
    priority_queue<int> maxHeap;

    // Min Heap to store all the composite numbers
    priority_queue<int, vector<int>, greater<int>>
        minHeap;

    // Push all the composite numbers
    // from the array to the heaps
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]]) {
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

    cout << "Sum of k-minimum composite numbers is "
         << minSum << "\n";
    cout << "Sum of k-maximum composite numbers is "
         << maxSum << "\n";
    cout << "Product of k-minimum composite numbers is "
         << minProduct << "\n";
    cout << "Product of k-maximum composite numbers is "
         << maxProduct;
}

// Driver code
int main()
{

    int arr[] = { 4, 2, 12, 13, 5, 19 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 3;

    compositeSumAndProduct(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum and
// product of k smallest and k largest
// composite numbers in an array
import java.util.*;

class GFG
{
    static boolean[] SieveOfEratosThenes(int max_val)
    {

        // Create a boolean vector "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        boolean[] prime = new boolean[max_val + 1];
        Arrays.fill(prime, true);

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
    static void compositeSumAndProduct(Integer[] arr,
                                       int n, int k)
    {

        // Find maximum value in the array
        int max_val = Collections.max(Arrays.asList(arr));

        // Use sieve to find all prime numbers
        // less than or equal to max_val
        boolean[] prime = SieveOfEratosThenes(max_val);

        // Set 0 and 1 as primes so that
        // they don't get counted as
        // composite numbers
        prime[0] = true;
        prime[1] = true;

        // Max Heap to store all the composite numbers
        PriorityQueue<Integer> maxHeap =
                  new PriorityQueue<Integer>((x, y) -> y - x);

        // Min Heap to store all the composite numbers
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        // Push all the composite numbers
        // from the array to the heaps
        for (int i = 0; i < n; i++)
        {
            if (!prime[arr[i]])
            {
                minHeap.add(arr[i]);
                maxHeap.add(arr[i]);
            }
        }

        long minProduct = 1, maxProduct = 1,
                 minSum = 0, maxSum = 0;
        Integer lastMin = 0, lastMax = 0;
        while (k-- > 0)
        {
            if (minHeap.peek() != null ||
                maxHeap.peek() != null)
            {

                // Calculate the products
                minProduct *= minHeap.peek();
                maxProduct *= maxHeap.peek();

                // Calculate the sum
                minSum += minHeap.peek();
                maxSum += maxHeap.peek();

                // Pop the current minimum element
                lastMin = minHeap.poll();

                // Pop the current maximum element
                lastMax = maxHeap.poll();
            }
            else
            {

                // when maxHeap or minHeap is exhausted
                // then this condition will run
                minProduct *= lastMin;
                maxProduct *= lastMax;

                minSum += lastMin;
                maxSum += lastMax;
            }
        }

        System.out.println("Sum of k-minimum composite" +
                                " numbers is " + minSum);
        System.out.println("Sum of k-maximum composite" +
                                " numbers is " + maxSum);
        System.out.println("Product of k-minimum composite" +
                                " numbers is " + minProduct);
        System.out.println("Product of k-maximum composite" +
                                " numbers is " + maxProduct);
    }

    // Driver Code
    public static void main(String[] args)
    {
        Integer[] arr = { 4, 2, 12, 13, 5, 19 };
        int n = arr.length;
        int k = 3;

        compositeSumAndProduct(arr, n, k);
    }
}

// This code is contributed by
// sanjeev2552
```

**Output:** 

```
Sum of k-minimum composite numbers is 28
Sum of k-maximum composite numbers is 20
Product of k-minimum composite numbers is 576
Product of k-maximum composite numbers is 192
```