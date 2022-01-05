# 数组中具有相同“与”、“或”和“异或”值的子集数量

> 原文:[https://www . geesforgeks . org/数组中值相同或异或的子集数/](https://www.geeksforgeeks.org/number-of-subsets-with-same-and-or-and-xor-values-in-an-array/)

给定一个由非负整数组成的大小为 **N** 的数组 **arr[]** ，任务是找到数组中非空子集的数量，使得子序列的[位“与”、位“或”和位“异或”值彼此相等。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

**注意:**既然答案可以大，那就用 **1000000007** 来 mod 吧。

**示例:**

> **输入:** arr[] = [1，3，2，1，2，1]
> **输出:** 7
> **解释:**
> 按位异或、按位或、按位与的子序列之一为{1，1，1}。
> 
> **输入:** arr = [2，3，4，5]
> **输出:** 4

**朴素方法**这个问题的朴素方法是[以迭代的方式遍历数组](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)的所有子集，对于每个子集找到按位 and、or 和 XOR 值，并检查它们是否相等。最后，返回这样相等子集的计数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the number
// of subsets with equal bitwise AND,
// OR and XOR values

#include <bits/stdc++.h>
using namespace std;
const int mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
int countSubsets(int a[], int n)
{
    int answer = 0;

    // Traverse through all the subsets
    for (int i = 0; i < (1 << n); i++) {

        int bitwiseAND = -1;
        int bitwiseOR = 0;
        int bitwiseXOR = 0;

        // Finding the subsets with the bits
        // of 'i' which are set
        for (int j = 0; j < n; j++) {

            // Computing the bitwise AND
            if (i & (1 << j)) {
                if (bitwiseAND == -1)
                    bitwiseAND = a[j];
                else
                    bitwiseAND &= a[j];

                // Computing the bitwise OR
                bitwiseOR |= a[j];

                // Computing the bitwise XOR
                bitwiseXOR ^= a[j];
            }
        }

        // Comparing all the three values
        if (bitwiseAND == bitwiseOR
            && bitwiseOR == bitwiseXOR)
            answer = (answer + 1) % mod;
    }
    return answer;
}

// Driver code
int main()
{
    int N = 6;
    int A[N] = { 1, 3, 2, 1, 2, 1 };

    cout << countSubsets(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the number
// of subsets with equal bitwise AND,
// OR and XOR values
import java.io.*;

class GFG {
static int mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
static int countSubsets(int a[], int n)
{
    int answer = 0;

    // Traverse through all the subsets
    for (int i = 0; i < (1 << n); i++) {

        int bitwiseAND = -1;
        int bitwiseOR = 0;
        int bitwiseXOR = 0;

        // Finding the subsets with the bits
        // of 'i' which are set
        for (int j = 0; j < n; j++) {

            // Computing the bitwise AND
            if ((i & (1 << j)) == 0) {
                if (bitwiseAND == -1)
                    bitwiseAND = a[j];
                else
                    bitwiseAND &= a[j];

                // Computing the bitwise OR
                bitwiseOR |= a[j];

                // Computing the bitwise XOR
                bitwiseXOR ^= a[j];
            }
        }

        // Comparing all the three values
        if (bitwiseAND == bitwiseOR
            && bitwiseOR == bitwiseXOR)
            answer = (answer + 1) % mod;
    }
    return answer;
}

// Driver Code
public static void main (String[] args)
{
    int N = 6;
    int A[] = { 1, 3, 2, 1, 2, 1 };

    System.out.print(countSubsets(A, N));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation to find the number
# of subsets with equal bitwise AND,
# OR and XOR values

mod = 1000000007;

# Function to find the number of
# subsets with equal bitwise AND,
# OR and XOR values
def countSubsets(a, n) :

    answer = 0;

    # Traverse through all the subsets
    for i in range(1 << n) :

        bitwiseAND = -1;
        bitwiseOR = 0;
        bitwiseXOR = 0;

        # Finding the subsets with the bits
        # of 'i' which are set
        for j in range(n) :

            # Computing the bitwise AND
            if (i & (1 << j)) :
                if (bitwiseAND == -1) :
                    bitwiseAND = a[j];
                else :
                    bitwiseAND &= a[j];

                # Computing the bitwise OR
                bitwiseOR |= a[j];

                # Computing the bitwise XOR
                bitwiseXOR ^= a[j];

        # Comparing all the three values
        if (bitwiseAND == bitwiseOR and bitwiseOR == bitwiseXOR) :
            answer = (answer + 1) % mod;

    return answer;

# Driver code
if __name__ == "__main__" :

    N = 6;
    A = [ 1, 3, 2, 1, 2, 1 ];

    print(countSubsets(A, N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the number
// of subsets with equal bitwise AND,
// OR and XOR values
using System;

class GFG {
static int mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
static int countSubsets(int []a, int n)
{
    int answer = 0;

    // Traverse through all the subsets
    for (int i = 0; i < (1 << n); i++) {

        int bitwiseAND = -1;
        int bitwiseOR = 0;
        int bitwiseXOR = 0;

        // Finding the subsets with the bits
        // of 'i' which are set
        for (int j = 0; j < n; j++) {

            // Computing the bitwise AND
            if ((i & (1 << j)) == 0) {
                if (bitwiseAND == -1)
                    bitwiseAND = a[j];
                else
                    bitwiseAND &= a[j];

                // Computing the bitwise OR
                bitwiseOR |= a[j];

                // Computing the bitwise XOR
                bitwiseXOR ^= a[j];
            }
        }

        // Comparing all the three values
        if (bitwiseAND == bitwiseOR
            && bitwiseOR == bitwiseXOR)
            answer = (answer + 1) % mod;
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 6;
    int []A = { 1, 3, 2, 1, 2, 1 };

    Console.Write(countSubsets(A, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript implementation to find the number
    // of subsets with equal bitwise AND,
    // OR and XOR values

    let mod = 1000000007;

    // Function to find the number of
    // subsets with equal bitwise AND,
    // OR and XOR values
    function countSubsets(a, n)
    {
        let answer = 0;

        // Traverse through all the subsets
        for (let i = 0; i < (1 << n); i++) {

            let bitwiseAND = -1;
            let bitwiseOR = 0;
            let bitwiseXOR = 0;

            // Finding the subsets with the bits
            // of 'i' which are set
            for (let j = 0; j < n; j++) {

                // Computing the bitwise AND
                if ((i & (1 << j)) != 0) {
                    if (bitwiseAND == -1)
                        bitwiseAND = a[j];
                    else
                        bitwiseAND &= a[j];

                    // Computing the bitwise OR
                    bitwiseOR |= a[j];

                    // Computing the bitwise XOR
                    bitwiseXOR ^= a[j];
                }
            }

            // Comparing all the three values
            if (bitwiseAND == bitwiseOR
                && bitwiseOR == bitwiseXOR)
                answer = (answer + 1) % mod;
        }
        return answer;
    }

    let N = 6;
    let A = [ 1, 3, 2, 1, 2, 1 ];

    document.write(countSubsets(A, N));

</script>
```

**Output:** 

```
7
```

**时间复杂度:** *O(N * 2 <sup>N</sup> )* 其中 N 是数组的大小。

**辅助空间:** O(1)

**高效方法:**高效方法的背后是按位运算的特性。

*   利用按位 and 和按位 OR 的性质，我们可以说，如果 a & b == a | b，那么 a 等于 b。因此，如果子集的 AND 和 OR 值相等，那么子集的所有元素都是相同的(比如 x)。所以 AND 和 OR 值等于 x。
*   因为子序列的所有值彼此相等，所以异或值出现两种情况:
    1.  **子集大小为奇数**:异或值等于 x。
    2.  **子集大小为偶数**:异或值等于 0。
*   因此，从上面的观察，我们可以得出结论，所有奇数大小的子序列/子集具有相等的元素遵循该属性。
*   除此之外，如果子集的所有元素都是 0，那么子集将遵循属性(与子集大小无关)。所以所有只有 0 作为元素的子集都会被添加到答案中。
*   如果某个元素的频率为 K，那么它可以形成的奇数大小子集的数量为**2<sup>K–1</sup>**，它可以形成的非空子集的总数为**2<sup>K</sup>–1**。

下面是上述方法的实现:

## C++

```
// C++ program to find the number
// of subsets with equal bitwise
// AND, OR and XOR values

#include <bits/stdc++.h>
using namespace std;
const int mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
int countSubsets(int a[], int n)
{
    int answer = 0;

    // Precompute the modded powers
    // of two for subset counting
    int powerOfTwo[100005];
    powerOfTwo[0] = 1;

    // Loop to iterate and find the modded
    // powers of two for subset counting
    for (int i = 1; i < 100005; i++)
        powerOfTwo[i]
            = (powerOfTwo[i - 1] * 2)
              % mod;

    // Map to store the frequency of
    // each element
    unordered_map<int, int> frequency;

    // Loop to compute the frequency
    for (int i = 0; i < n; i++)
        frequency[a[i]]++;

    // For every element > 0, the number of
    // subsets formed using this element only
    // is equal to 2 ^ (frequency[element]-1).
    // And for 0, we have to find all
    // the subsets, so 2^(frequency[element]) -1
    for (auto el : frequency) {

        // If element is greater than 0
        if (el.first != 0)
            answer
                = (answer % mod
                   + powerOfTwo[el.second - 1])
                  % mod;

        else
            answer
                = (answer % mod
                   + powerOfTwo[el.second]
                   - 1 + mod)
                  % mod;
    }
    return answer;
}

// Driver code
int main()
{
    int N = 6;
    int A[N] = { 1, 3, 2, 1, 2, 1 };

    cout << countSubsets(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of subsets with equal bitwise
// AND, OR and XOR values

import java.util.*;

class GFG{
static int mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
static int countSubsets(int a[], int n)
{
    int answer = 0;

    // Precompute the modded powers
    // of two for subset counting
    int []powerOfTwo = new int[100005];
    powerOfTwo[0] = 1;

    // Loop to iterate and find the modded
    // powers of two for subset counting
    for (int i = 1; i < 100005; i++)
        powerOfTwo[i]
            = (powerOfTwo[i - 1] * 2)
              % mod;

    // Map to store the frequency of
    // each element
    HashMap<Integer,Integer> frequency = new HashMap<Integer,Integer>();

    // Loop to compute the frequency
    for (int i = 0; i < n; i++)
        if(frequency.containsKey(a[i])){
            frequency.put(a[i], frequency.get(a[i])+1);
        }else{
            frequency.put(a[i], 1);
    }

    // For every element > 0, the number of
    // subsets formed using this element only
    // is equal to 2 ^ (frequency[element]-1).
    // And for 0, we have to find all
    // the subsets, so 2^(frequency[element]) -1
    for (Map.Entry<Integer,Integer> el : frequency.entrySet()) {

        // If element is greater than 0
        if (el.getKey() != 0)
            answer
                = (answer % mod
                   + powerOfTwo[el.getValue() - 1])
                  % mod;

        else
            answer
                = (answer % mod
                   + powerOfTwo[el.getValue()]
                   - 1 + mod)
                  % mod;
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int N = 6;
    int A[] = { 1, 3, 2, 1, 2, 1 };

    System.out.print(countSubsets(A, N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the number
# of subsets with equal bitwise
# AND, OR and XOR values
mod = 1000000007

# Function to find the number of
# subsets with equal bitwise AND,
# OR and XOR values
def countSubsets(a, n):

    answer = 0

    # Precompute the modded powers
    # of two for subset counting
    powerOfTwo = [0 for x in range(100005)]
    powerOfTwo[0] = 1

    # Loop to iterate and find the modded
    # powers of two for subset counting
    for i in range(1, 100005):
        powerOfTwo[i] = (powerOfTwo[i - 1] * 2) % mod

    # Map to store the frequency of
    # each element
    frequency = {}

    # Loop to compute the frequency
    for i in range(0, n):
        if a[i] in frequency:
            frequency[a[i]] += 1
        else:
            frequency[a[i]] = 1

    # For every element > 0, the number of
    # subsets formed using this element only
    # is equal to 2 ^ (frequency[element]-1).
    # And for 0, we have to find all
    # the subsets, so 2^(frequency[element]) -1
    for key, value in frequency.items():

        # If element is greater than 0
        if (key != 0):
            answer = (answer % mod +
                  powerOfTwo[value - 1]) % mod
        else:
            answer = (answer % mod +
                 powerOfTwo[value] - 1 + mod)% mod

    return answer

# Driver code
N = 6
A = [ 1, 3, 2, 1, 2, 1 ]

print(countSubsets(A, N))

# This code is contributed by amreshkumar3
```

## C#

```
// C# program to find the number
// of subsets with equal bitwise
// AND, OR and XOR values
using System;
using System.Collections.Generic;

class GFG{

static int mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
static int countSubsets(int []a, int n)
{
    int answer = 0;

    // Precompute the modded powers
    // of two for subset counting
    int []powerOfTwo = new int[100005];
    powerOfTwo[0] = 1;

    // Loop to iterate and find the modded
    // powers of two for subset counting
    for(int i = 1; i < 100005; i++)
       powerOfTwo[i] = (powerOfTwo[i - 1] * 2) % mod;

    // Map to store the frequency
    // of each element
    Dictionary<int, int> frequency = new Dictionary<int, int>();

    // Loop to compute the frequency
    for(int i = 0; i < n; i++)
       if(frequency.ContainsKey(a[i]))
       {
           frequency[a[i]] = frequency[a[i]] + 1;
       }
       else
       {
           frequency.Add(a[i], 1);
       }

    // For every element > 0, the number of
    // subsets formed using this element only
    // is equal to 2 ^ (frequency[element]-1).
    // And for 0, we have to find all
    // the subsets, so 2^(frequency[element]) -1
    foreach (KeyValuePair<int, int> el in frequency)
    {

        // If element is greater than 0
        if (el.Key != 0)
            answer = (answer % mod +
                      powerOfTwo[el.Value - 1]) % mod;
        else
            answer = (answer % mod +
                      powerOfTwo[el.Value] - 1 +
                      mod) % mod;
    }
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int N = 6;
    int []A = { 1, 3, 2, 1, 2, 1 };

    Console.Write(countSubsets(A, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of subsets with equal bitwise
// AND, OR and XOR values
var mod = 1000000007;

// Function to find the number of
// subsets with equal bitwise AND,
// OR and XOR values
function countSubsets(a, n)
{
    var answer = 0;

    // Precompute the modded powers
    // of two for subset counting
    var powerOfTwo = Array(100005).fill(0);
    powerOfTwo[0] = 1;

    // Loop to iterate and find the modded
    // powers of two for subset counting
    for(var i = 1; i < 100005; i++)
        powerOfTwo[i] = (powerOfTwo[i - 1] * 2) % mod;

    // Map to store the frequency
    // of each element
    var frequency = new Map();

    // Loop to compute the frequency
    for(var i = 0; i < n; i++)
        if (frequency.has(a[i]))
        {
            frequency.set(a[i], frequency.get(a[i]) + 1);
        }
        else
        {
            frequency.set(a[i], 1);
        }

    // For every element > 0, the number of
    // subsets formed using this element only
    // is equal to 2 ^ (frequency[element]-1).
    // And for 0, we have to find all
    // the subsets, so 2^(frequency[element]) -1
    frequency.forEach((value, key) => {

        // If element is greater than 0
        if (key != 0)
            answer = (answer % mod +
                      powerOfTwo[value - 1]) % mod;
        else
            answer = (answer % mod +
                      powerOfTwo[value] - 1 +
                      mod) % mod;
    });
    return answer;
}

// Driver code
var N = 6;
var A = [ 1, 3, 2, 1, 2, 1 ];

document.write(countSubsets(A, N));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
7
```

**时间复杂度:** *O(N)* ，其中 N 是数组的大小。

**辅助空间:** O(N + 10 <sup>5</sup>