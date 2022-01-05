# 对按位异或等于 0 的偶数长度子阵列进行计数

> 原文:[https://www . geeksforgeeks . org/count-偶数长度子数组-按位异或-等于-0/](https://www.geeksforgeeks.org/count-even-length-subarrays-having-bitwise-xor-equal-to-0/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是计算所有可能的[偶长度子数组](https://www.geeksforgeeks.org/maximum-sum-subarray-of-even-length/)，子数组元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **0** 。

**示例:**

> **输入:** arr[] = {2，2，3，3，6，7，8}
> **输出:** 3
> **解释:**
> 元素异或等于 0 的子阵为:{{2，2}，{3，3}，{2，2，3，3}}
> 因此，需要的输出为 3。
> 
> **输入:** arr[] = {1，2，3，3 }
> T3】输出: 1

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。对于每个子阵列，检查子阵列的长度是否均匀，子阵列元素的**位异或**是否为 **0** 。按照以下步骤解决问题:

*   初始化一个变量，比如 **res** 来存储满足给定条件的子阵列的计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。
*   对于每个子阵列，检查子阵列的长度是否为偶数，其元素的按位异或是否为 0，然后将 **res** 增加 1。
*   最后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of even-length subarrays
// having Bitwise XOR equal to 0
int cntSubarr(int arr[], int N)
{
    // Stores the count of
    // required subarrays
    int res = 0;

    // Stores prefix-XOR
    // of arr[i, i+1, ...N-1]
    int prefixXor = 0;

    // Traverse the array
    for (int i = 0; i < N - 1;
         i++) {

        prefixXor = arr[i];

        for (int j = i + 1; j < N;
             j++) {

            // Calculate the prefix-XOR
            // of current subarray
            prefixXor ^= arr[j];

            // Check if XOR of the
            // current subarray is 0
            // and length is even
            if (prefixXor == 0
                && (j - i + 1) % 2 == 0) {
                res++;
            }
        }
    }
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 2, 2, 3, 3, 6, 7, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntSubarr(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to count the number
// of even-length subarrays
// having Bitwise XOR equal to 0
static int cntSubarr(int arr[], int N)
{

    // Stores the count of
    // required subarrays
    int res = 0;

    // Stores prefix-XOR
    // of arr[i, i+1, ...N-1]
    int prefixXor = 0;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {
        prefixXor = arr[i];

        for(int j = i + 1; j < N; j++)
        {

            // Calculate the prefix-XOR
            // of current subarray
            prefixXor ^= arr[j];

            // Check if XOR of the
            // current subarray is 0
            // and length is even
            if (prefixXor == 0 &&
               (j - i + 1) % 2 == 0)
            {
                res++;
            }
        }
    }
    return res;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 2, 2, 3, 3, 6, 7, 8 };
    int N = arr.length;

    System.out.println(cntSubarr(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number
# of even-length subarrays
# having Bitwise XOR equal to 0
def cntSubarr(arr, N):

    # Stores the count of
    # required subarrays
    res = 0

    # Stores prefix-XOR
    # of arr[i, i+1, ...N-1]
    prefixXor = 0

    # Traverse the array
    for i in range(N - 1):
        prefixXor = arr[i]
        for j in range(i + 1, N):

            # Calculate the prefix-XOR
            # of current subarray
            prefixXor ^= arr[j]

            # Check if XOR of the
            # current subarray is 0
            # and length is even
            if (prefixXor == 0 and
               (j - i + 1) % 2 == 0):
                res += 1

    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 2, 3, 3, 6, 7, 8 ]
    N = len(arr)

    print(cntSubarr(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to count the number
// of even-length subarrays
// having Bitwise XOR equal to 0
static int cntSubarr(int[] arr, int N)
{

    // Stores the count of
    // required subarrays
    int res = 0;

    // Stores prefix-XOR
    // of arr[i, i+1, ...N-1]
    int prefixXor = 0;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {
        prefixXor = arr[i];

        for(int j = i + 1; j < N; j++)
        {

            // Calculate the prefix-XOR
            // of current subarray
            prefixXor ^= arr[j];

            // Check if XOR of the
            // current subarray is 0
            // and length is even
            if (prefixXor == 0 &&
               (j - i + 1) % 2 == 0)
            {
                res++;
            }
        }
    }
    return res;
}

// Driver Code
public static void Main ()
{
    int[] arr = { 2, 2, 3, 3, 6, 7, 8 };
    int N = arr.Length;

    Console.WriteLine(cntSubarr(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the number
// of even-length subarrays
// having Bitwise XOR equal to 0
function cntSubarr(arr, N)
{
    // Stores the count of
    // required subarrays
    var res = 0;

    // Stores prefix-XOR
    // of arr[i, i+1, ...N-1]
    var prefixXor = 0;
    var i,j;
    // Traverse the array
    for (i = 0; i < N - 1;
         i++) {

        prefixXor = arr[i];

        for (j = i + 1; j < N;
             j++) {

            // Calculate the prefix-XOR
            // of current subarray
            prefixXor ^= arr[j];

            // Check if XOR of the
            // current subarray is 0
            // and length is even
            if (prefixXor == 0
                && (j - i + 1) % 2 == 0) {
                res++;
            }
        }
    }
    return res;
}

// Driver Code
    var arr = [2, 2, 3, 3, 6, 7, 8];
    var N = arr.length;
    document.write(cntSubarr(arr, N));

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法**:使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决问题。其思想是将**前缀异或**的频率存储在两个独立的数组中，比如**奇数[]** 和**偶数[]** ，以存储给定数组的奇数和偶数索引的前缀异或的频率。最后，打印值大于或等于 **2** 的**偶数[]** 和**奇数[]** 数组中所有可能的对的计数。以下是观察结果:

> 奇数索引–奇数索引=偶数长度
> 偶数索引–偶数索引=偶数长度
> 
> **如果偶数[X] ≥ 2:** 给定数组的两个偶数索引之间的所有元素的按位异或必须为 0，并且子数组的长度也是偶数(偶数索引–偶数索引)。
> 
> **如果奇数[X] ≥ 2:** 给定阵列的两个奇数索引之间的所有元素的按位异或必须为 0，并且子阵列的长度也是偶数(奇数索引–奇数索引)。

按照以下步骤解决问题:

*   初始化两个数组，比如**偶数[]** 和**奇数[]** 分别存储给定数组的偶数和奇数索引处的前缀异或的频率。
*   初始化一个变量，比如 **cntSub** ，以存储满足给定条件的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的计数。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并计算给定数组的**前缀异或**。
*   将给定数组的偶数和奇数索引处的**前缀异或**的频率分别存储在数组**偶数[]** 和**奇数[]** 中。
*   最后，打印值大于或等于 **2** 的所有可能的**偶[]** 和**奇[]** 对的计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define M 1000000

// Function to get the count
// of even length subarrays
// having bitwise xor 0
int cntSubXor(int arr[], int N)
{
    // Stores prefix-xor of
    // the given array
    int prefixXor = 0;

    // Stores prefix-xor at
    // even index of the  array.
    int Even[M];

    // Stores prefix-xor at
    // odd index of the  array.
    int Odd[M];

    // Stores count of subarrays
    // that satisfy the condition
    int cntSub = 0;

    // length from 0 index
    // to odd index is even
    Odd[0] = 1;

    // Traverse the array.
    for (int i = 0; i < N; i++) {
        // Take prefix-xor
        prefixXor ^= arr[i];

        // If index is odd
        if (i % 2 == 1) {

            // Calculate pairs
            cntSub += Odd[prefixXor];

            // Increment prefix-xor
            // at odd index
            Odd[prefixXor]++;
        }
        else {

            // Calculate pairs
            cntSub += Even[prefixXor];

            // Increment prefix-xor
            // at odd index
            Even[prefixXor]++;
        }
    }
    return cntSub;
}

// Driver Code
int main()
{
    int arr[] = { 2, 2, 3, 3, 6, 7, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntSubXor(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static final int M =  1000000;

// Function to get the count
// of even length subarrays
// having bitwise xor 0
static int cntSubXor(int arr[], int N)
{

    // Stores prefix-xor of
    // the given array
    int prefixXor = 0;

    // Stores prefix-xor at
    // even index of the  array.
    int []Even = new int[M];

    // Stores prefix-xor at
    // odd index of the  array.
    int []Odd = new int[M];

    // Stores count of subarrays
    // that satisfy the condition
    int cntSub = 0;

    // length from 0 index
    // to odd index is even
    Odd[0] = 1;

    // Traverse the array.
    for(int i = 0; i < N; i++)
    {

        // Take prefix-xor
        prefixXor ^= arr[i];

        // If index is odd
        if (i % 2 == 1)
        {

            // Calculate pairs
            cntSub += Odd[prefixXor];

            // Increment prefix-xor
            // at odd index
            Odd[prefixXor]++;
        }
        else
        {

            // Calculate pairs
            cntSub += Even[prefixXor];

            // Increment prefix-xor
            // at odd index
            Even[prefixXor]++;
        }
    }
    return cntSub;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 2, 3, 3, 6, 7, 8 };
    int N = arr.length;

    System.out.print(cntSubXor(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
M = 1000000;

# Function to get the count
# of even length subarrays
# having bitwise xor 0
def cntSubXor(arr, N):

    # Stores prefix-xor of
    # the given array
    prefixXor = 0;

    # Stores prefix-xor at
    # even index of the array.
    Even =[0] * M;

    # Stores prefix-xor at
    # odd index of the array.
    Odd = [0] * M;

    # Stores count of subarrays
    # that satisfy the condition
    cntSub = 0;

    # length from 0 index
    # to odd index is even
    Odd[0] = 1;

    # Traverse the array.
    for i in range(0, N):

        # Take prefix-xor
        prefixXor ^= arr[i];

        # If index is odd
        if (i % 2 == 1):

            # Calculate pairs
            cntSub += Odd[prefixXor];

            # Increment prefix-xor
            # at odd index
            Odd[prefixXor] += 1;
        else:

            # Calculate pairs
            cntSub += Even[prefixXor];

            # Increment prefix-xor
            # at odd index
            Even[prefixXor] += 1;

    return cntSub;

# Driver Code
if __name__ == '__main__':

    arr = [2, 2, 3, 3,
           6, 7, 8];
    N = len(arr);
    print(cntSubXor(arr, N));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static readonly int M =  1000000;

// Function to get the count
// of even length subarrays
// having bitwise xor 0
static int cntSubXor(int []arr, int N)
{

    // Stores prefix-xor of
    // the given array
    int prefixXor = 0;

    // Stores prefix-xor at
    // even index of the  array.
    int []Even = new int[M];

    // Stores prefix-xor at
    // odd index of the  array.
    int []Odd = new int[M];

    // Stores count of subarrays
    // that satisfy the condition
    int cntSub = 0;

    // length from 0 index
    // to odd index is even
    Odd[0] = 1;

    // Traverse the array.
    for(int i = 0; i < N; i++)
    {

        // Take prefix-xor
        prefixXor ^= arr[i];

        // If index is odd
        if (i % 2 == 1)
        {

            // Calculate pairs
            cntSub += Odd[prefixXor];

            // Increment prefix-xor
            // at odd index
            Odd[prefixXor]++;
        }
        else
        {

            // Calculate pairs
            cntSub += Even[prefixXor];

            // Increment prefix-xor
            // at odd index
            Even[prefixXor]++;
        }
    }
    return cntSub;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 2, 3, 3, 6, 7, 8 };
    int N = arr.Length;

    Console.Write(cntSubXor(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
let M =  1000000;

// Function to get the count
// of even length subarrays
// having bitwise xor 0
function cntSubXor(arr, N)
{

    // Stores prefix-xor of
    // the given array
    let prefixXor = 0;

    // Stores prefix-xor at
    // even index of the  array.
    let Even = Array.from({length: M}, (_, i) => 0);

    // Stores prefix-xor at
    // odd index of the  array.
    let Odd = Array.from({length: M}, (_, i) => 0);

    // Stores count of subarrays
    // that satisfy the condition
    let cntSub = 0;

    // length from 0 index
    // to odd index is even
    Odd[0] = 1;

    // Traverse the array.
    for(let i = 0; i < N; i++)
    {

        // Take prefix-xor
        prefixXor = Math.floor(prefixXor ^ arr[i]);

        // If index is odd
        if (i % 2 == 1)
        {

            // Calculate pairs
            cntSub += Odd[prefixXor];

            // Increment prefix-xor
            // at odd index
            Odd[prefixXor]++;
        }
        else
        {

            // Calculate pairs
            cntSub += Even[prefixXor];

            // Increment prefix-xor
            // at odd index
            Even[prefixXor]++;
        }
    }
    return cntSub;
}

// Driver Code
let arr = [ 2, 2, 3, 3, 6, 7, 8 ];
let N = arr.length;

document.write(cntSubXor(arr, N));

// This code is contributed by target_2         

</script>
```

**Output**

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(M)，其中 M 是所有子阵中可能的最大按位异或。*