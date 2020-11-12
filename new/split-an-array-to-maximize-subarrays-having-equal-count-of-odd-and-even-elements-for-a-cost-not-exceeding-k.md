# 分割一个数组以使子数组最大化，而子数组的奇数和偶数元素数量相等，而成本不超过 K

> 原文：[https://www.geeksforgeeks.org/split-an-array-to-maximize-subarrays-having-equal-count-of-odd-and-even-elements-for-a-cost-not-exceeding-k/](https://www.geeksforgeeks.org/split-an-array-to-maximize-subarrays-having-equal-count-of-odd-and-even-elements-for-a-cost-not-exceeding-k/)

给定大小为`N`的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`和整数`K`，任务是将给定数组拆分为最大可能的子数组，偶数和奇数元素的[计数相等](https://www.geeksforgeeks.org/count-subarrays-with-same-even-and-odd-elements/)，拆分数组的成本不超过`K`。

> 将数组拆分为子数组的成本分别是子数组的最后一个元素与第一个元素之间的差。

**示例**：

> **输入**：`arr[] = {1, 2, 5, 10, 15, 20}, K = 4`
>
> **输出**：1
>
> **说明**：
>
> 最佳方法是在 2 和 5 之间分割数组。
>
> 因此将其分割为`{1, 2}`和`{5, 10, 15, 20}`。
>
> 此外，两个子数组都包含相等数量的偶数和奇数元素。 拆分的成本为`abs(2 – 5) = 3 ≤ K`。
> 
> **输入**：`arr[] = {1,2,3,4,5,6}, K = 100`
>
> **输出**：2
>
> **说明**：
>
> 最佳方法是进行两个拆分，以使形成的子数组为`{1, 2}, {3, 4}, {5, 6}`。
>
> 总费用为`abs(2 - 3) + abs(4 - 5) = 2`

**朴素的方法**：解决此问题的最简单方法如下：

1.  在每个索引处拆分数组，并检查开销是否小于`K`。

2.  如果代价小于`K`，则检查子数组中奇数和偶数元素的数量是否相等。

3.  现在，通过重复相同的步骤，检查是否可以进行其他拆分。

4.  检查所有可能的分割后，打印最小成本，其总和小于`K`。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(1)`

**高效方法**：想法是维护计数器，该计数器在数组中存储偶数和奇数。 步骤如下：

1.  初始化一个数组（例如`poss[]`），该数组存储所有可能的拆分成本。

2.  遍历数组`arr[]`。 对于每个索引，检查直到该索引的子数组和从下一个索引开始的子数组的奇数和偶数元素计数是否相等。

3.  如果满足以上条件，则可以拆分。 将与此拆分相关的成本存储在`poss[]`中。

4.  对数组中的所有元素重复上述步骤，并存储每次拆分的成本。

5.  可以通过`abs(arr[i + 1] – arr[i])`来获得索引`i`的分割成本。

6.  现在，为了找到最大可能拆分的数量，[对包含每个可能拆分成本的数组`poss[]`排序](https://www.geeksforgeeks.org/sorting-algorithms/)。

7.  现在，从总和小于或等于`K`的`poss[]`中选择所有最低成本。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the cost of 
// splitting the arrays into subarray 
// with cost less than K 
int make_cuts(int arr[], int n, int K) 
{ 
    // Store the possible splits 
    int ans = 0; 

    // Stores the cost of each split 
    vector<int> poss; 

    // Stores the count of even numbers 
    int ce = 0; 

    // Stores the count 
    // of odd numbers 
    int co = 0; 

    for (int x = 0; x < n - 1; x++) { 

        // Count of odd & even elements 
        if (arr[x] % 2 == 0) 
            ce++; 
        else
            co++; 

        // Check the required conditions 
        // for a valid split 
        if (ce == co && co > 0 
            && ce > 0) { 
            poss.push_back( 
                abs(arr[x] 
                    - arr[x + 1])); 
        } 
    } 

    // Sort the cost of splits 
    sort(poss.begin(), poss.end()); 

    // Find the minimum split costs 
    // adding up to sum less than K 
    for (int x : poss) { 
        if (K >= x) { 
            ans++; 
            K -= x; 
        } 
        else
            break; 
    } 
    return ans; 
} 

// Driver Code 
int main() 
{ 
    // Given array and K 
    int N = 6; 
    int K = 4; 

    int arr[] = { 1, 2, 5, 10, 15, 20 }; 

    // Function Call 
    cout << make_cuts(arr, N, K); 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to find the cost of 
// splitting the arrays into subarray 
// with cost less than K 
static int make_cuts(int arr[], int n, int K) 
{ 

    // Store the possible splits 
    int ans = 0; 

    // Stores the cost of each split 
    Vector<Integer> poss = new Vector<Integer>(); 

    // Stores the count of even numbers 
    int ce = 0; 

    // Stores the count 
    // of odd numbers 
    int co = 0; 

    for(int x = 0; x < n - 1; x++) 
    { 

        // Count of odd & even elements 
        if (arr[x] % 2 == 0) 
            ce++; 
        else
            co++; 

        // Check the required conditions 
        // for a valid split 
        if (ce == co && co > 0 && ce > 0) 
        { 
            poss.add(Math.abs(arr[x] -  
                              arr[x + 1])); 
        } 
    } 

    // Sort the cost of splits 
    Collections.sort(poss); 

    // Find the minimum split costs 
    // adding up to sum less than K 
    for(int x : poss) 
    { 
        if (K >= x)  
        { 
            ans++; 
            K -= x; 
        } 
        else
            break; 
    } 
    return ans; 
} 

// Driver Code 
public static void main(String[] args) 
{ 

    // Given array and K 
    int N = 6; 
    int K = 4; 

    int arr[] = { 1, 2, 5, 10, 15, 20 }; 

    // Function call 
    System.out.print(make_cuts(arr, N, K)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

## Python3

```py

# Python3 program for the above approach  

# Function to find the cost of 
# splitting the arrays into subarray 
# with cost less than K 
def make_cuts(arr, n, K): 

    # Store the possible splits 
    ans = 0

    # Stores the cost of each split 
    poss = [] 

    # Stores the count of even numbers 
    ce = 0

    # Stores the count 
    # of odd numbers 
    co = 0

    for x in range(n - 1): 

        # Count of odd & even elements 
        if(arr[x] % 2 == 0): 
            ce += 1
        else: 
            co += 1

        # Check the required conditions 
        # for a valid split 
        if(ce == co and co > 0 and ce > 0): 
            poss.append(abs(arr[x] - 
                            arr[x + 1])) 

    # Sort the cost of splits 
    poss.sort() 

    # Find the minimum split costs 
    # adding up to sum less than K 
    for x in poss: 
        if (K >= x): 
            ans += 1
            K -= x 
        else: 
            break

    return ans 

# Driver Code 

# Given array and K 
N = 6
K = 4

arr = [ 1, 2, 5, 10, 15, 20 ] 

# Function call 
print(make_cuts(arr, N, K)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the cost of 
// splitting the arrays into subarray 
// with cost less than K 
static int make_cuts(int []arr, int n, int K) 
{ 

    // Store the possible splits 
    int ans = 0; 

    // Stores the cost of each split 
    List<int> poss = new List<int>(); 

    // Stores the count of even numbers 
    int ce = 0; 

    // Stores the count 
    // of odd numbers 
    int co = 0; 

    for(int x = 0; x < n - 1; x++) 
    { 

        // Count of odd & even elements 
        if (arr[x] % 2 == 0) 
            ce++; 
        else
            co++; 

        // Check the required conditions 
        // for a valid split 
        if (ce == co && co > 0 && ce > 0) 
        { 
            poss.Add(Math.Abs(arr[x] -  
                              arr[x + 1])); 
        } 
    } 

    // Sort the cost of splits 
    poss.Sort(); 

    // Find the minimum split costs 
    // adding up to sum less than K 
    foreach(int x in poss) 
    { 
        if (K >= x)  
        { 
            ans++; 
            K -= x; 
        } 
        else
            break; 
    } 
    return ans; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Given array and K 
    int N = 6; 
    int K = 4; 

    int []arr = { 1, 2, 5, 10, 15, 20 }; 

    // Function call 
    Console.Write(make_cuts(arr, N, K)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

**输出**： 

```
1

```

**时间复杂度**：`O(N log(N))`

**辅助空间**：`O(n)`



* * *

* * *



