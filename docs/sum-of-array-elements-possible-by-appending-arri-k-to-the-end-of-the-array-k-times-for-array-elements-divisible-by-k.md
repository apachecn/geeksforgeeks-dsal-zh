# 对于可被 K 整除的数组元素，通过将 arr[I/K]附加到数组末尾 K 次，可以得到的数组元素的总和

> 原文:[https://www . geeksforgeeks . org/array-k-to-end-k-time-for-array-elements-sum-by-k-除尽/](https://www.geeksforgeeks.org/sum-of-array-elements-possible-by-appending-arri-k-to-the-end-of-the-array-k-times-for-array-elements-divisible-by-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，如果 **arr[i]** 可被**K**整除，则任务是通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在数组末尾添加 **arr[i] / K** 、 **K** 次来找到数组元素[的和否则，停止遍历。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {4，6，8，2}，K = 2
> **输出:** 44
> **解释:**
> 执行以下操作:
> 
> 1.  **对于 arr[0](= 4):** arr[0](= 4)可被 2 整除，因此在数组末尾追加 4/2 = 2，2 个次数。现在，数组修改为{4，6，8，2，2，2}。
> 2.  **对于 arr[1](= 6):** arr[1](= 6)可被 2 整除，因此在数组末尾追加 6/2 = 3，2 的次数。现在，数组修改为{4，6，8，2，2，2，3，3}。
> 3.  **对于 arr[2](= 8):** arr[2](= 8)可被 2 整除，因此在数组末尾追加 8/2 = 4，2 的次数。现在，数组修改为{4，6，8，2，2，2，3，3，4，4}。
> 4.  **对于 arr[3](= 2):** arr[3](= 2)可被 2 整除，因此在数组末尾追加 2/2 = 1，2 的次数。现在，数组修改为{4，6，8，2，2，2，3，3，4，4，1，1}。
> 5.  **对于 arr[4](= 2):** arr[4](= 2)可被 2 整除，因此在数组末尾追加 2/2 = 1，2 的次数。现在，数组修改为{4，6，8，2，2，2，3，3，4，4，1，1，1，1}。
> 6.  **对于 arr[5](= 2):** arr[5](= 2)可被 2 整除，因此在数组末尾追加 2/2 = 1，2 的次数。现在，数组修改为{4，6，8，2，2，2，3，3，4，4，1，1，1，1，1，1}。
> 
> 完成上述步骤后，数组元素之和为= 4+6+8+2+2+2+3+3+4+4+1+1+1+1+1+1 = 44。
> 
> **输入:** arr[] = {4，6，8，9}，K = 2
> T3】输出: 45

**天真法:**解决给定问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在数组末尾多次添加值**(arr[I/K)****K**。完成上述步骤后，打印数组元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of array
// elements after adding arr[i] / K
// to the end of the array if arr[i]
// is divisible by K
int sum(int arr[], int N, int K)
{
    // Stores the sum of the array
    int sum = 0;

    vector<long long> v;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        v.push_back(arr[i]);
    }

    // Traverse the vector
    for (int i = 0;
         i < v.size(); i++) {

        // If v[i] is divisible by K
        if (v[i] % K == 0) {

            long long x = v[i] / K;

            // Iterate over the range
            // [0, K]
            for (int j = 0; j < K; j++) {
                // Update v
                v.push_back(x);
            }
        }
        // Otherwise
        else
            break;
    }

    // Traverse the vector v
    for (int i = 0; i < v.size(); i++)
        sum = sum + v[i];

    // Return the sum of the updated array
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 4, 6, 8, 2 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << sum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to calculate sum of array
// elements after adding arr[i] / K
// to the end of the array if arr[i]
// is divisible by K
static int sum(int arr[], int N, int K)
{

    // Stores the sum of the array
    int sum = 0;

    ArrayList<Integer> v = new ArrayList<>();

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        v.add(arr[i]);
    }

    // Traverse the vector
    for(int i = 0; i < v.size(); i++)
    {

        // If v[i] is divisible by K
        if (v.get(i) % K == 0)
        {
            int x = v.get(i) / K;

            // Iterate over the range
            // [0, K]
            for(int j = 0; j < K; j++)
            {

                // Update v
                v.add(x);
            }
        }

        // Otherwise
        else
            break;
    }

    // Traverse the vector v
    for(int i = 0; i < v.size(); i++)
        sum = sum + v.get(i);

    // Return the sum of the updated array
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 8, 2 };
    int K = 2;
    int N = arr.length;

    System.out.println(sum(arr, N, K));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of array
# elements after adding arr[i] / K
# to the end of the array if arr[i]
# is divisible by K
def summ(arr, N, K):

    # Stores the sum of the array
    sum = 4

    v = [i for i in arr]

    # Traverse the vector
    for i in range(len(v)):

        # If v[i] is divisible by K
        if (v[i] % K == 0):

            x = v[i] // K

            # Iterate over the range
            # [0, K]
            for j in range(K):

                # Update v
                v.append(x)

        # Otherwise
        else:
            break

    # Traverse the vector v
    for i in range(len(v)):
        sum = sum + v[i]

    # Return the sum of the updated array
    return sum

# Driver Code
if __name__ == '__main__':

    arr = [ 4, 6, 8, 2 ]
    K = 2
    N = len(arr)

    print(summ(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to calculate sum of array
    // elements after adding arr[i] / K
    // to the end of the array if arr[i]
    // is divisible by K
    static int sum(int[] arr, int N, int K)
    {

        // Stores the sum of the array
        int sum = 0;

        List<int> v = new List<int>();

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {
            v.Add(arr[i]);
        }

        // Traverse the vector
        for (int i = 0; i < v.Count; i++) {

            // If v[i] is divisible by K
            if (v[i] % K == 0) {
                int x = v[i] / K;

                // Iterate over the range
                // [0, K]
                for (int j = 0; j < K; j++) {

                    // Update v
                    v.Add(x);
                }
            }

            // Otherwise
            else
                break;
        }

        // Traverse the vector v
        for (int i = 0; i < v.Count; i++)
            sum = sum + v[i];

        // Return the sum of the updated array
        return sum;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 4, 6, 8, 2 };
        int K = 2;
        int N = arr.Length;

        Console.WriteLine(sum(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate sum of array
// elements after adding arr[i] / K
// to the end of the array if arr[i]
// is divisible by K
function sum(arr, N, K)
{
    // Stores the sum of the array
    var sum = 0;

    var v = [];

    // Traverse the array arr[]
    for (var i = 0; i < N; i++) {
        v.push(arr[i]);
    }

    // Traverse the vector
    for (var i = 0;
         i < v.length; i++) {

        // If v[i] is divisible by K
        if (v[i] % K == 0) {

            var x = v[i] / K;

            // Iterate over the range
            // [0, K]
            for (var j = 0; j < K; j++) {
                // Update v
                v.push(x);
            }
        }
        // Otherwise
        else
            break;
    }

    // Traverse the vector v
    for (var i = 0; i < v.length; i++)
        sum = sum + v[i];

    // Return the sum of the updated array
    return sum;
}

// Driver Code
var arr = [4, 6, 8, 2];
var K = 2;
var N = arr.length;
document.write( sum(arr, N, K));

</script>
```

**Output:** 

```
44
```

***时间复杂度:**O(N * K * log N)*
T5**辅助空间:** O(M)，M 是 [*数组的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   如果 **arr[i]** 可被 **K** 整除，那么将 **arr[i] / K** 、 **K** 次相加将和增加 **arr[i]** 。
*   因此，想法是在向量的末尾只推一次**arr【I/K】**。

按照以下步骤解决问题:

*   初始化一个变量，将 **sum** 设为 **0** ，存储所有数组元素的 [sum 数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **A[]** 。
*   初始化一个数组，说 **A[]** 并将所有数组元素 **arr[]** 存储在 **A[]** 中。
*   初始化一个变量，比如说**将**标记为 **0** ，该变量存储元素是否要添加到数组的末尾。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**A【】**并执行以下步骤:
    *   如果**标志**的值为 **0** 、**A【I】**可被 **K** 整除，则在 **V** 末尾推**A【I】**。
    *   否则，将**标志**的值更新为 **1** 。
    *   将**和**的值增加**V【I % N】**。
*   完成上述步骤后，打印**总和**的值作为合成总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of array
// elements after adding arr[i] / K
// to the end of the array if arr[i]
// is divisible by K
int sum(int arr[], int N, int K)
{
    // Stores the sum of the array
    int sum = 0;

    // Stores the array elements
    vector<int> v;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        v.push_back(arr[i]);
    }

    // Stores if the operation
    // should be formed or not
    bool flag = 0;

    // Traverse the vector V
    for (int i = 0; i < v.size(); i++) {

        // If flag is false and if
        // v[i] is divisible by K
        if (!flag && v[i] % K == 0)
            v.push_back(v[i] / K);

        // Otherwise, set flag as true
        else {
            flag = 1;
        }

        // Increment the sum by v[i % N]
        sum = sum + v[i % N];
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 4, 6, 8, 2 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << sum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

      // Function to calculate sum of array
    // elements after adding arr[i] / K
    // to the end of the array if arr[i]
    // is divisible by K
    static int sum(int arr[], int N, int K)
    {
        // Stores the sum of the array
        int sum = 0;

        // Stores the array elements
        ArrayList<Integer> v = new ArrayList<Integer>();

        // Traverse the array
        for (int i = 0; i < N; i++) {
            v.add(arr[i]);
        }

        // Stores if the operation
        // should be formed or not
        boolean flag = false;

        // Traverse the vector V
        for (int i = 0; i < v.size(); i++) {

            // If flag is false and if
            // v[i] is divisible by K
            if (!flag && v.get(i) % K == 0)
                v.add(v.get(i) / K);

            // Otherwise, set flag as true
            else {
                flag = true;
            }

            // Increment the sum by v[i % N]
            sum = sum + v.get(i % N);
        }

        // Return the resultant sum
        return sum;
    }

    // Driver Code
    public static void main (String[] args) {
        int arr[] = { 4, 6, 8, 2 };
        int K = 2;
        int N = arr.length;
        System.out.println(sum(arr, N, K));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python  program for the above approach

# Function to calculate sum of array
# elements after adding arr[i] / K
# to the end of the array if arr[i]
# is divisible by K
def Sum(arr, N, K):

    # Stores the sum of the array
    sum = 0

    # Stores the array elements
    v = []

    # Traverse the array
    for i in range(N):
        v.append(arr[i])

    # Stores if the operation
    # should be formed or not
    flag = False

    i = 0
    lenn = len(v)

    # Traverse the vector V
    while(i < lenn):

        # If flag is false and if
        # v[i] is divisible by K
        if( flag == False and (v[i] % K == 0)):
            v.append(v[i]//K)

        # Otherwise, set flag as true
        else:
            flag = True

        # Increment the sum by v[i % N]
        sum += v[i % N]
        i += 1
        lenn = len(v)

    # Return the resultant sum
    return sum

# Driver Code
arr = [ 4, 6, 8, 2]
K = 2
N = len(arr)
print(Sum(arr, N, K))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate sum of array
// elements after adding arr[i] / K
// to the end of the array if arr[i]
// is divisible by K
static int sum(int []arr, int N, int K)
{

    // Stores the sum of the array
    int sum = 0;

    // Stores the array elements
    List<int> v = new List<int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        v.Add(arr[i]);
    }

    // Stores if the operation
    // should be formed or not
    bool flag = false;

    // Traverse the vector V
    for(int i = 0; i < v.Count; i++)
    {

        // If flag is false and if
        // v[i] is divisible by K
        if (!flag && v[i] % K == 0)
            v.Add(v[i] / K);

        // Otherwise, set flag as true
        else
        {
            flag = true;
        }

        // Increment the sum by v[i % N]
        sum = sum + v[i % N];
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
static void Main()
{
    int[] arr = { 4, 6, 8, 2 };
    int K = 2;
    int N = arr.Length;

    Console.WriteLine(sum(arr, N, K));
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to calculate sum of array
// elements after adding arr[i] / K
// to the end of the array if arr[i]
// is divisible by K
function sum(arr, N, K)
{
    // Stores the sum of the array
    var sum = 0;
    var i;
    // Stores the array elements
    var v = [];

    // Traverse the array
    for (i = 0; i < N; i++) {
        v.push(arr[i]);
    }

    // Stores if the operation
    // should be formed or not
    var flag = 0;

    // Traverse the vector V
    for (i = 0; i < v.length; i++) {

        // If flag is false and if
        // v[i] is divisible by K
        if (!flag && v[i] % K == 0)
            v.push(v[i] / K);

        // Otherwise, set flag as true
        else {
            flag = 1;
        }

        // Increment the sum by v[i % N]
        sum = sum + v[i % N];
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
    var arr = [4, 6, 8, 2];
    var K = 2;
    var N = arr.length;
    document.write(sum(arr, N, K));

</script>
```

**Output:** 

```
44
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N * log N)*