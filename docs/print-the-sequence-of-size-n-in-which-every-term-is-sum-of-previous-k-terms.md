# 打印大小为 N 的序列，其中每一项都是前 K 项的总和

> 原文:[https://www . geesforgeks . org/print-the-sequence-of-size-n-in-每个术语都是前 k 个术语的总和/](https://www.geeksforgeeks.org/print-the-sequence-of-size-n-in-which-every-term-is-sum-of-previous-k-terms/)

给定两个整数 **N** 和 **K** ，任务是生成一系列 **N** 项，其中每个项都是之前的 **K** 项的和。
**注:**该系列的第一个术语是 **1** ，如果之前的术语不够，那么其他术语应该是 **0** 。
**示例:**

> **输入:** N = 8， K = 3
> **输出:** 1 1 2 4 7 13 24 44
> **说明:**
> 系列生成如下:
> a[0]= 1
> a[1]= 1+0+0 = 1
> a[2]= 1+1+0 = 2
> a[3]= 2+1+1 = 4
> a[4]= 4+2+1 = 7
> a[5]= 1 = 13+7+4 = 24
> a[7]= 24+13+7 = 44
> **输入:** N = 10，K = 4
> **输出:**1 2 4 8 15 29 56 108 208

**天真方法:**想法是运行两个循环生成 N 项级数。下面是步骤的图示:

*   遍历从 **0** 到**N–1**的第一个循环，生成该系列的每个项。
*   运行从 **max(0，I–K)**到 **i** 的循环，计算前 K 项的总和。
*   将当前系列索引的总和更新为当前术语。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// series in which every term is
// sum of previous K terms

#include <iostream>

using namespace std;

// Function to generate the
// series in the form of array
void sumOfPrevK(int N, int K)
{
    int arr[N];
    arr[0] = 1;

    // Pick a starting point
    for (int i = 1; i < N; i++) {
        int j = i - 1, count = 0,
            sum = 0;
        // Find the sum of all
        // elements till count < K
        while (j >= 0 && count < K) {
            sum += arr[j];
            j--;
            count++;
        }
        // Find the value of
        // sum at i position
        arr[i] = sum;
    }
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int N = 10, K = 4;
    sumOfPrevK(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// series in which every term is
// sum of previous K terms

class Sum {
    // Function to generate the
    // series in the form of array
    void sumOfPrevK(int N, int K)
    {
        int arr[] = new int[N];
        arr[0] = 1;

        // Pick a starting point
        for (int i = 1; i < N; i++) {
            int j = i - 1, count = 0,
                sum = 0;
            // Find the sum of all
            // elements till count < K
            while (j >= 0 && count < K) {
                sum += arr[j];
                j--;
                count++;
            }
            // Find the value of
            // sum at i position
            arr[i] = sum;
        }
        for (int i = 0; i < N; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        Sum s = new Sum();
        int N = 10, K = 4;
        s.sumOfPrevK(N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the
# series in which every term is
# sum of previous K terms

# Function to generate the
# series in the form of array
def sumOfPrevK(N, K):
    arr = [0 for i in range(N)]
    arr[0] = 1

    # Pick a starting point
    for i in range(1,N):
        j = i - 1
        count = 0
        sum = 0

        # Find the sum of all
        # elements till count < K
        while (j >= 0 and count < K):
            sum = sum + arr[j]
            j = j - 1
            count = count + 1

        # Find the value of
        # sum at i position
        arr[i] = sum

    for i in range(0, N):
        print(arr[i])

# Driver Code
N = 10
K = 4
sumOfPrevK(N, K)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to find the
// series in which every term is
// sum of previous K terms
using System;

class Sum {
    // Function to generate the
    // series in the form of array
    void sumOfPrevK(int N, int K)
    {
        int []arr = new int[N];
        arr[0] = 1;

        // Pick a starting point
        for (int i = 1; i < N; i++) {
            int j = i - 1, count = 0,
                sum = 0;

            // Find the sum of all
            // elements till count < K
            while (j >= 0 && count < K) {
                sum += arr[j];
                j--;
                count++;
            }

            // Find the value of
            // sum at i position
            arr[i] = sum;
        }
        for (int i = 0; i < N; i++) {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver Code
    public static void Main(String []args)
    {
        Sum s = new Sum();
        int N = 10, K = 4;
        s.sumOfPrevK(N, K);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// series in which every term is
// sum of previous K terms

// Function to generate the
// series in the form of array
function sumOfPrevK(N, K)
{
    let arr = new Array(N);
    arr[0] = 1;

    // Pick a starting point
    for (let i = 1; i < N; i++) {
        let j = i - 1, count = 0, sum = 0;
        // Find the sum of all
        // elements till count < K
        while (j >= 0 && count < K) {
            sum += arr[j];
            j--;
            count++;
        }
        // Find the value of
        // sum at i position
        arr[i] = sum;
    }
    for (let i = 0; i < N; i++) {
        document.write(arr[i] + " ");
    }
}

// Driver Code

let N = 10, K = 4;
sumOfPrevK(N, K);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1 1 2 4 8 15 29 56 108 208 
```

**性能分析:**

*   ***时间复杂度:** O(N * K)*
*   ***空间复杂度:** O(N)*

**有效方法:**想法是将当前的和存储在一个变量中，在每一步中减去最后一个 **K <sup>第</sup>T5】项，并将最后一项添加到预和中，以计算该系列的每个项。
以下是上述方法的实现:**

## C++

```
// C++ implementation to find the
// series in which every term is
// sum of previous K terms

#include <iostream>

using namespace std;

// Function to generate the
// series in the form of array
void sumOfPrevK(int N, int K)
{
    int arr[N], prevsum = 0;
    arr[0] = 1;

    // Pick a starting point
    for (int i = 0; i < N - 1; i++) {

        // Computing the previous sum
        if (i < K) {
            arr[i + 1] = arr[i] + prevsum;
            prevsum = arr[i + 1];
        }
        else {
            arr[i + 1] = arr[i] + prevsum
                         - arr[i + 1 - K];
            prevsum = arr[i + 1];
        }
    }

    // Loop to print the series
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int N = 8, K = 3;
    sumOfPrevK(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// series in which every term is
// sum of previous K terms

class Sum {
    // Function to generate the
    // series in the form of array
    void sumOfPrevK(int N, int K)
    {
        int arr[] = new int[N];
        int prevsum = 0;
        arr[0] = 1;

        // Pick a starting point
        for (int i = 0; i < N - 1; i++) {

            // Computing the previous sum
            if (i < K) {
                arr[i + 1] = arr[i] + prevsum;
                prevsum = arr[i + 1];
            }
            else {
                arr[i + 1] = arr[i] + prevsum
                             - arr[i + 1 - K];
                prevsum = arr[i + 1];
            }
        }

        // Loop to print the series
        for (int i = 0; i < N; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        Sum s = new Sum();
        int N = 8, K = 3;
        s.sumOfPrevK(N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the
# series in which every term is
# sum of previous K terms

# Function to generate the
# series in the form of array
def sumOfPrevK(N, K):
    arr = [0]*N;
    prevsum = 0;
    arr[0] = 1;

    # Pick a starting point
    for i in range(N-1):

        # Computing the previous sum
        if (i < K):
            arr[i + 1] = arr[i] + prevsum;
            prevsum = arr[i + 1];
        else:
            arr[i + 1] = arr[i] + prevsum - arr[i + 1 - K];
            prevsum = arr[i + 1];

    # Loop to print the series
    for i in range(N):
        print(arr[i], end=" ");

# Driver code
if __name__ == '__main__':
    N = 8;
    K = 3;
    sumOfPrevK(N, K);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to find the
// series in which every term is
// sum of previous K terms
using System;
public class Sum {
    // Function to generate the
    // series in the form of array
    void sumOfPrevK(int N, int K)
    {
        int []arr = new int[N];
        int prevsum = 0;
        arr[0] = 1;

        // Pick a starting point
        for (int i = 0; i < N - 1; i++) {

            // Computing the previous sum
            if (i < K) {
                arr[i + 1] = arr[i] + prevsum;
                prevsum = arr[i + 1];
            }
            else {
                arr[i + 1] = arr[i] + prevsum
                             - arr[i + 1 - K];
                prevsum = arr[i + 1];
            }
        }

        // Loop to print the series
        for (int i = 0; i < N; i++) {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        Sum s = new Sum();
        int N = 8, K = 3;
        s.sumOfPrevK(N, K);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// series in which every term is
// sum of previous K terms

// Function to generate the
// series in the form of array
function sumOfPrevK(N, K)
{
    let arr = new Array(N), prevsum = 0;
    arr[0] = 1;

    // Pick a starting point
    for (let i = 0; i < N - 1; i++) {

        // Computing the previous sum
        if (i < K) {
            arr[i + 1] = arr[i] + prevsum;
            prevsum = arr[i + 1];
        }
        else {
            arr[i + 1] = arr[i] + prevsum
                         - arr[i + 1 - K];
            prevsum = arr[i + 1];
        }
    }

    // Loop to print the series
    for (let i = 0; i < N; i++) {
        document.write(arr[i] + " ");
    }
}

// Driver Code
    let N = 8, K = 3;
    sumOfPrevK(N, K);

    // This code is contributed by rishavmahato348.
</script>
```

**复杂度分析:**

*   ***时间复杂度:** O(N)*
*   ***空间复杂度:** O(N)*