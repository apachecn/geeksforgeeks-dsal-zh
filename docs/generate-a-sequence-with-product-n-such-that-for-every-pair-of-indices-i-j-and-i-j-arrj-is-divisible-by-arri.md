# 生成具有乘积 N 的序列，使得对于每对指数(I，j)和 i < j，arr[j]可被 arr[i]

整除

> 原文:[https://www . geesforgeks . org/generate-a-sequence-with-product-n-so-for-每对索引-I-j-和-I-j-arrj-可被 arri 除尽/](https://www.geeksforgeeks.org/generate-a-sequence-with-product-n-such-that-for-every-pair-of-indices-i-j-and-i-j-arrj-is-divisible-by-arri/)

给定一个正整数 **N** ，任务是生成一个最大长度为**arr【】**的序列，其中所有元素**至少为 2** ，使得序列中所有数字的[乘积为 **N** ，对于任意一对索引 **(i，j)** 和 **i < j** ，**arr【j】**可被**arr**整除](https://www.geeksforgeeks.org/program-for-product-of-array/)

**示例:**

> **输入:** N = 360
> **输出:**最大大小= 3，最终数组= {2，2，90}
> **解释:**
> 将数组 arr[]视为结果数组，然后可以执行以下操作:
> 
> 1.  向数组 arr[]中添加 2。现在，N = 360/2 = 180，arr[] = {2}。
> 2.  向数组 arr[]中添加 2。现在，N = 180/2 = 90，arr[] = {2，2}。
> 3.  将数组 arr[]加上 90。现在，arr[] = {2，2，90}。
> 
> 经过上述操作后，数组的最大大小为 3，结果数组为{2，2，90}。
> 
> **输入:**N = 810
> T3】输出:最大大小= 4，最终数组= {3，3，3，30}

**方法:**利用[素因子分解](https://www.geeksforgeeks.org/prime-factor/)的概念可以解决给定的问题，思路是找到出现频率最大的[素数](https://www.geeksforgeeks.org/prime-numbers/)为 **N** ，可以表示为素数的[积为:](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)

> n =(a)<sup>【P1】</sup>)*(a)<sub>【2】</sub>*(a)

按照以下步骤解决问题:

*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **M** ，它把所有[质数](https://www.geeksforgeeks.org/tag/prime-number/)存储为一个键，把它们的幂存储为值。例如，对于值 **2 <sup>3</sup>** ，映射 **M** 存储为**M【2】= 3**。
*   选择具有最大功率因数的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)并将该功率存储在一个变量中，比如说**和**，并将该质数存储在一个变量中，比如说 **P** 。
*   如果**和**的值小于 **2** ，则得到的数组大小为 **1** ，数组元素等于 **N** 。
*   否则，打印 **ans** 的值作为最大长度，要打印最终序列，打印**P****(ans–1)**次数的值，然后在最后打印( **N/2 <sup>ans</sup> )** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the prime
// factors of N with their count
vector<pair<int, int> > primeFactor(
    int N)
{
    // Initialize a vector, say v
    vector<pair<int, int> > v;

    // Initialize the count
    int count = 0;

    // Count the number of divisors
    while (!(N % 2)) {

        // Divide the value of N by 2
        N >>= 1;
        count++;
    }

    // For factor 2 divides it
    if (count)
        v.push_back({ 2, count });

    // Find all prime factors
    for (int i = 3;
         i <= sqrt(N); i += 2) {

        // Count their frequency
        count = 0;
        while (N % i == 0) {
            count++;
            N = N / i;
        }

        // Push it to the vector
        if (count) {
            v.push_back({ i, count });
        }
    }

    // Push N if it is not 1
    if (N > 2)
        v.push_back({ N, 1 });

    return v;
}

// Function to print the array that
// have the maximum size
void printAnswer(int n)
{
    // Stores the all prime factor
    // and their powers
    vector<pair<int, int> > v
        = primeFactor(n);

    int maxi_size = 0, prime_factor = 0;

    // Traverse the vector and find
    // the maximum power of prime
    // factor
    for (int i = 0; i < v.size(); i++) {

        if (maxi_size < v[i].second) {
            maxi_size = v[i].second;
            prime_factor = v[i].first;
        }
    }

    // If max size is less than 2
    if (maxi_size < 2) {
        cout << 1 << ' ' << n;
    }

    // Otherwise
    else {

        int product = 1;

        // Print the maximum size
        // of sequence
        cout << maxi_size << endl;

        // Print the final sequence
        for (int i = 0;
             i < maxi_size - 1; i++) {

            // Print the prime factor
            cout << prime_factor << " ";
            product *= prime_factor;
        }

        // Print the last value of
        // the sequence
        cout << (n / product);
    }
}

// Driver Code
int main()
{
    int N = 360;
    printAnswer(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Function to calculate the prime
// factors of N with their count
static Vector<pair > primeFactor(
    int N)
{

    // Initialize a vector, say v
    Vector<pair > v = new Vector<>();

    // Initialize the count
    int count = 0;

    // Count the number of divisors
    while ((N % 2)==0) {

        // Divide the value of N by 2
        N >>= 1;
        count++;
    }

    // For factor 2 divides it
    if (count!=0)
        v.add(new pair( 2, count ));

    // Find all prime factors
    for (int i = 3;
         i <= Math.sqrt(N); i += 2) {

        // Count their frequency
        count = 0;
        while (N % i == 0) {
            count++;
            N = N / i;
        }

        // Push it to the vector
        if (count!=0) {
            v.add(new pair( i, count ));
        }
    }

    // Push N if it is not 1
    if (N > 2)
        v.add(new pair( N, 1 ));

    return v;
}

// Function to print the array that
// have the maximum size
static void printAnswer(int n)
{
    // Stores the all prime factor
    // and their powers
    Vector<pair > v
        = primeFactor(n);

    int maxi_size = 0, prime_factor = 0;

    // Traverse the vector and find
    // the maximum power of prime
    // factor
    for (int i = 0; i < v.size(); i++) {

        if (maxi_size < v.get(i).second) {
            maxi_size = v.get(i).second;
            prime_factor = v.get(i).first;
        }
    }

    // If max size is less than 2
    if (maxi_size < 2) {
        System.out.print(1 << ' ');
    }

    // Otherwise
    else {

        int product = 1;

        // Print the maximum size
        // of sequence
        System.out.print(maxi_size +"\n");

        // Print the final sequence
        for (int i = 0;
             i < maxi_size - 1; i++) {

            // Print the prime factor
            System.out.print(prime_factor+ " ");
            product *= prime_factor;
        }

        // Print the last value of
        // the sequence
        System.out.print((n / product));
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 360;
    printAnswer(N);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Function to calculate the prime
# factors of N with their count
def primeFactor(N):

    # Initialize a vector, say v
    v = []

    # Initialize the count
    count = 0

    # Count the number of divisors
    while ((N % 2) == 0):

        # Divide the value of N by 2
        N >>= 1
        count += 1

    # For factor 2 divides it
    if (count):
        v.append([2, count])

    # Find all prime factors
    for i in range(3, int(sqrt(N)) + 1, 2):

        # Count their frequency
        count = 0
        while (N % i == 0):
            count += 1
            N = N / i

        # Push it to the vector
        if (count):
            v.append([i, count])

    # Push N if it is not 1
    if (N > 2):
        v.append([N, 1])

    return v

# Function to print the array that
# have the maximum size
def printAnswer(n):

    # Stores the all prime factor
    # and their powers
    v = primeFactor(n)

    maxi_size = 0
    prime_factor = 0

    # Traverse the vector and find
    # the maximum power of prime
    # factor
    for i in range(len(v)):
        if (maxi_size < v[i][1]):
            maxi_size = v[i][1]
            prime_factor = v[i][0]

    # If max size is less than 2
    if (maxi_size < 2):
        print(1, n)

    # Otherwise
    else:
        product = 1

        # Print the maximum size
        # of sequence
        print(maxi_size)

        # Print the final sequence
        for i in range(maxi_size - 1):

            # Print the prime factor
            print(prime_factor, end = " ")
            product *= prime_factor

        # Print the last value of
        # the sequence
        print(n // product)

# Driver Code
if __name__ == '__main__':

    N = 360

    printAnswer(N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    class pair
    {
        public int first;
        public int second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to calculate the prime
// factors of N with their count
static List<pair > primeFactor(
    int N)
{

    // Initialize a vector, say v
    List<pair > v = new List<pair>();

    // Initialize the count
    int count = 0;

    // Count the number of divisors
    while ((N % 2)==0) {

        // Divide the value of N by 2
        N >>= 1;
        count++;
    }

    // For factor 2 divides it
    if (count!=0)
        v.Add(new pair( 2, count ));

    // Find all prime factors
    for (int i = 3;
         i <= Math.Sqrt(N); i += 2) {

        // Count their frequency
        count = 0;
        while (N % i == 0) {
            count++;
            N = N / i;
        }

        // Push it to the vector
        if (count!=0) {
            v.Add(new pair( i, count ));
        }
    }

    // Push N if it is not 1
    if (N > 2)
        v.Add(new pair( N, 1 ));

    return v;
}

// Function to print the array that
// have the maximum size
static void printAnswer(int n)
{

    // Stores the all prime factor
    // and their powers
    List<pair > v
        = primeFactor(n);

    int maxi_size = 0, prime_factor = 0;

    // Traverse the vector and find
    // the maximum power of prime
    // factor
    for (int i = 0; i < v.Count; i++) {

        if (maxi_size < v[i].second) {
            maxi_size = v[i].second;
            prime_factor = v[i].first;
        }
    }

    // If max size is less than 2
    if (maxi_size < 2) {
        Console.Write(1 << ' ');
    }

    // Otherwise
    else {

        int product = 1;

        // Print the maximum size
        // of sequence
        Console.Write(maxi_size +"\n");

        // Print the readonly sequence
        for (int i = 0;
             i < maxi_size - 1; i++) {

            // Print the prime factor
            Console.Write(prime_factor+ " ");
            product *= prime_factor;
        }

        // Print the last value of
        // the sequence
        Console.Write((n / product));
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 360;
    printAnswer(N);

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the prime
// factors of N with their count
function primeFactor(N)
{

    // Initialize a vector, say v
    let v = [];

    // Initialize the count
    let count = 0;

    // Count the number of divisors
    while (!(N % 2)) {

        // Divide the value of N by 2
        N >>= 1;
        count++;
    }

    // For factor 2 divides it
    if (count)
        v.push([2, count]);

    // Find all prime factors
    for (let i = 3; i <= Math.sqrt(N); i += 2) {

        // Count their frequency
        count = 0;
        while (N % i == 0) {
            count++;
            N = Math.floor(N / i);
        }

        // Push it to the vector
        if (count) {
            v.push([i, count]);
        }
    }

    // Push N if it is not 1
    if (N > 2)
        v.push([N, 1]);

    return v;
}

// Function to print the array that
// have the maximum size
function printAnswer(n)
{

    // Stores the all prime factor
    // and their powers
    let v = primeFactor(n);

    let maxi_size = 0, prime_factor = 0;

    // Traverse the vector and find
    // the maximum power of prime
    // factor
    for (let i = 0; i < v.length; i++) {

        if (maxi_size < v[i][1]) {
            maxi_size = v[i][1];
            prime_factor = v[i][0];
        }
    }

    // If max size is less than 2
    if (maxi_size < 2) {
        document.write(1 + ' ' + n);
    }

    // Otherwise
    else {

        let product = 1;

        // Print the maximum size
        // of sequence
        document.write(maxi_size + "<br>");

        // Print the final sequence
        for (let i = 0; i < maxi_size - 1; i++) {

            // Print the prime factor
            document.write(prime_factor + " ");
            product *= prime_factor;
        }

        // Print the last value of
        // the sequence
        document.write(Math.floor((n / product)));
    }
}

// Driver Code

let N = 360;
printAnswer(N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
3
2 2 90
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(N)*