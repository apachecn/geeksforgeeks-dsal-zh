# 求所有有效对的 a[i]%a[j]的和

> 原文:[https://www . geesforgeks . org/find-sum-of-aiaj-for-all-valid-pairs/](https://www.geeksforgeeks.org/find-sum-of-aiaj-for-all-valid-pairs/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找到所有有效对的 **arr[i] % arr[j]** 之和。答案可以很大。于是，输出答案模 1000000007
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:**5
> (1% 1)+(1% 2)+(1% 3)+(2% 1)+(2% 2)
> +(2% 3)+(3% 1)+(3% 2)+(3% 3)= 5
> **输入:** arr[] = {1，2，4，4，4}
> **输出:**

**方法:**存储每个元素的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)，在频率数组上运行嵌套循环，找到需要的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define mod (int)(1e9 + 7)

// Function to return the sum of (a[i] % a[j])
// for all valid pairs
int Sum_Modulo(int a[], int n)
{
    int max = *max_element(a, a + n);

    // To store the frequency of each element
    int cnt[max + 1] = { 0 };

    // Store the frequency of each element
    for (int i = 0; i < n; i++)
        cnt[a[i]]++;

    // To store the required answer
    long long ans = 0;

    // For all valid pairs
    for (int i = 1; i <= max; i++) {
        for (int j = 1; j <= max; j++) {

            // Update the count
            ans = ans + cnt[i] * cnt[j] * (i % j);
            ans = ans % mod;
        }
    }

    return (int)(ans);
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << Sum_Modulo(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int mod = (int)(1e9 + 7);

// Function to return the sum of (a[i] % a[j])
// for all valid pairs
static int Sum_Modulo(int a[], int n)
{
    int max = Arrays.stream(a).max().getAsInt();

    // To store the frequency of each element
    int []cnt=new int[max + 1];

    // Store the frequency of each element
    for (int i = 0; i < n; i++)
        cnt[a[i]]++;

    // To store the required answer
    long ans = 0;

    // For all valid pairs
    for (int i = 1; i <= max; i++)
    {
        for (int j = 1; j <= max; j++)
        {

            // Update the count
            ans = ans + cnt[i] *
                        cnt[j] * (i % j);
            ans = ans % mod;
        }
    }

    return (int)(ans);
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3 };
    int n = a.length;

    System.out.println(Sum_Modulo(a, n));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 10**9 + 7

# Function to return the sum of
# (a[i] % a[j]) for all valid pairs
def Sum_Modulo(a, n):

    Max = max(a)

    # To store the frequency of each element
    cnt = [0 for i in range(Max + 1)]

    # Store the frequency of each element
    for i in a:
        cnt[i] += 1

    # To store the required answer
    ans = 0

    # For all valid pairs
    for i in range(1, Max + 1):
        for j in range(1, Max + 1):

            # Update the count
            ans = ans + cnt[i] * \
                        cnt[j] * (i % j)
            ans = ans % mod

    return ans

# Driver code
a = [1, 2, 3]
n = len(a)

print(Sum_Modulo(a, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;
class GFG
{

static int mod = (int)(1e9 + 7);

// Function to return the sum of (a[i] % a[j])
// for all valid pairs
static int Sum_Modulo(int []a, int n)
{
    int max = a.Max();

    // To store the frequency of each element
    int []cnt = new int[max + 1];

    // Store the frequency of each element
    for (int i = 0; i < n; i++)
        cnt[a[i]]++;

    // To store the required answer
    long ans = 0;

    // For all valid pairs
    for (int i = 1; i <= max; i++)
    {
        for (int j = 1; j <= max; j++)
        {

            // Update the count
            ans = ans + cnt[i] *
                        cnt[j] * (i % j);
            ans = ans % mod;
        }
    }
    return (int)(ans);
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3 };
    int n = a.Length;

    Console.WriteLine(Sum_Modulo(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let mod = 1e9 + 7

// Function to return the sum of (a[i] % a[j])
// for all valid pairs
function Sum_Modulo(a, n)
{
    let max = a.sort((a, b) => b - a)[0];

    // To store the frequency of each element
    let cnt = new Array(max + 1).fill(0);

    // Store the frequency of each element
    for (let i = 0; i < n; i++)
        cnt[a[i]]++;

    // To store the required answer
    let ans = 0;

    // For all valid pairs
    for (let i = 1; i <= max; i++) {
        for (let j = 1; j <= max; j++) {

            // Update the count
            ans = ans + cnt[i] * cnt[j] * (i % j);
            ans = ans % mod;
        }
    }

    return (ans);
}

// Driver code

let a = [1, 2, 3];
let n = a.length;

document.write(Sum_Modulo(a, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
5
```