# 查找乘积最大的四元组的数量

> 原文：[https://www.geeksforgeeks.org/find-the-number-of-maximum-product-quadruples/](https://www.geeksforgeeks.org/find-the-number-of-maximum-product-quadruples/)

给定一个由`N`个正元素组成的数组，可以找到数字的四元组`(i, j, k, m)`，使得`i < j < k < m`，并且`a[i], a[j], a[k], a[m]`的乘积是最大可能值。

**示例**：

```
Input : N = 7, arr = {1, 2, 3, 3, 3, 3, 5}  
Output : 4 
 Explanation 
The maximum quadruple product possible is 135, which can be 
achieved by the following quadruples {i, j, k, m} such that a<sub>i</sub>a<sub>j</sub>a<sub>k</sub>a<sub>m</sub> = 135:
1) a<sub>3</sub>a<sub>4</sub>a<sub>5</sub>a<sub>7</sub>
2) a<sub>3</sub>a<sub>4</sub>a<sub>6</sub>a<sub>7</sub>
3) a<sub>4</sub>a<sub>5</sub>a<sub>6</sub>a<sub>7</sub>
4) a<sub>3</sub>a<sub>5</sub>a<sub>6</sub>a<sub>7</sub>

Input : N = 4, arr = {1, 5, 2, 1} 
Output : 1 
 Explanation 
The maximum quadruple product possible is 10, which can be 
achieved by the following quadruple {1, 2, 3, 4} as a<sub>1</sub>a<sub>2</sub>a<sub>3</sub>a<sub>4</sub> = 10

```

**暴力生成**：`O(N ^ 4)`。

计算所有可能的四元组，从而得到最大乘积。

**优化的解决方案**：

很容易看出，四个最大数字的乘积将最大。 因此，现在可以将问题减少到找到选择四个最大元素的方式数量。 为此，请维护一个频率数组，该数组存储该数组每个元素的频率。

假定最大元素是频率为`F[X]`的`X`，则如果该元素的频率`>= 4`，则最适合选择四个元素`X, X, X`作为给定最大乘积，并且实现方法的数量为`C(F[X], 4)`。

如果频率小于 4 时，选择它的方式数为 1，现在所需的元素数为`4 – F[X]`。 对于第二个元素，假设`Y`，方法的数量为： `C(F[X], remaining_choices)`。 `remaining_choices`表示选择第一个元素后需要选择的其他元素的数量。 如果在任何时候剩余的选择`= 0`，则表示选择了四倍，因此我们可以停止算法。

## C++

```cpp

// CPP program to find the number of Quadruples
// having maximum product
#include <bits/stdc++.h>
using namespace std;

// Returns the number of ways to select r objects
// out of available n choices
int NCR(int n, int r)
{
    int numerator = 1;
    int denominator = 1;

    // ncr = (n * (n - 1) * (n - 2) * .....
    // ... (n - r + 1)) / (r * (r - 1) * ... * 1)
    while (r > 0) {
        numerator *= n;
        denominator *= r;
        n--;
        r--;
    }

    return (numerator / denominator);
}

// Returns the number of quadruples having maximum product
int findWays(int arr[], int n)
{
    // stores the frequency of each element
    map<int, int> count;

    if (n < 4)
        return 0;

    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
    }

    // remaining_choices denotes the remaining 
    // elements to select inorder to form quadruple
    int remaining_choices = 4;
    int ans = 1;

    // traverse the elements of the map in reverse order
    for (auto iter = count.rbegin(); iter != count.rend(); ++iter) {
        int number = iter->first;
        int frequency = iter->second;

        // If Frequeny of element < remaining choices,
        // select all of these elements, else select only 
        // the number of elements required
        int toSelect = min(remaining_choices, frequency);
        ans = ans * NCR(frequency, toSelect);

        // Decrement remaining_choices acc to the number
        // of the current elements selected
        remaining_choices -= toSelect;

        // if the quadruple is formed stop the algorithm
        if (!remaining_choices) {
            break;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 3, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int maxQuadrupleWays = findWays(arr, n);
    cout << maxQuadrupleWays;

    return 0;
}

```

## Java

```java

// Java program to find the number of Quadruples
// having maximum product
import java.util.*;
class Solution
{
// Returns the number of ways to select r objects
// out of available n choices
static int NCR(int n, int r)
{
    int numerator = 1;
    int denominator = 1;

    // ncr = (n * (n - 1) * (n - 2) * .....
    // ... (n - r + 1)) / (r * (r - 1) * ... * 1)
    while (r > 0) {
        numerator *= n;
        denominator *= r;
        n--;
        r--;
    }

    return (numerator / denominator);
}

// Returns the number of quadruples having maximum product
static int findWays(int arr[], int n)
{
    // stores the frequency of each element
    HashMap<Integer,Integer> count= new HashMap<Integer,Integer>();

    if (n < 4)
        return 0;

    for (int i = 0; i < n; i++) {
        count.put(arr[i],(count.get(arr[i])==null?0🙁int)count.get(arr[i])));
    }

    // remaining_choices denotes the remaining 
    // elements to select inorder to form quadruple
    int remaining_choices = 4;
    int ans = 1;

    // Getting an iterator 
        Iterator hmIterator = count.entrySet().iterator(); 

        while (hmIterator.hasNext()) { 
            Map.Entry mapElement = (Map.Entry)hmIterator.next();
            int number =(int) mapElement.getKey();
            int frequency =(int)mapElement.getValue();

              // If Frequeny of element < remaining choices,
        // select all of these elements, else select only 
        // the number of elements required
        int toSelect = Math.min(remaining_choices, frequency);
        ans = ans * NCR(frequency, toSelect);

        // Decrement remaining_choices acc to the number
        // of the current elements selected
        remaining_choices -= toSelect;

        // if the quadruple is formed stop the algorithm
        if (remaining_choices==0) {
            break;
        }
        }

    return ans;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 3, 3, 5 };
    int n = arr.length;

    int maxQuadrupleWays = findWays(arr, n);
    System.out.print( maxQuadrupleWays);
}
}
//contributed by Arnab Kundu

```

## Python3

```py

# Python3 program to find 
# the number of Quadruples
# having maximum product
from collections import defaultdict

# Returns the number of ways 
# to select r objects out of
# available n choices
def NCR(n, r):

    numerator = 1
    denominator = 1

    # ncr = (n * (n - 1) * 
    # (n - 2) * .....
    # ... (n - r + 1)) / 
    # (r * (r - 1) * ... * 1)
    while (r > 0):
        numerator *= n
        denominator *= r
        n -= 1
        r -= 1

    return (numerator // denominator)

# Returns the number of
# quadruples having 
# maximum product
def findWays(arr, n):

    # stores the frequency 
    # of each element
    count = defaultdict (int)

    if (n < 4):
        return 0

    for i in range (n):
        count[arr[i]] += 1

    # remaining_choices denotes 
    # the remaining elements to 
    # select inorder to form quadruple
    remaining_choices = 4
    ans = 1

    # traverse the elements of 
    # the map in reverse order
    for it in reversed(sorted(count.keys())):
        number = it
        frequency = count[it]

        # If Frequeny of element < 
        # remaining choices, select
        # all of these elements, 
        # else select only the 
        # number of elements required
        toSelect = min(remaining_choices, 
                       frequency)
        ans = ans * NCR(frequency, 
                        toSelect)

        # Decrement remaining_choices 
        # acc to the number of the
        # current elements selected
        remaining_choices -= toSelect

        # if the quadruple is 
        # formed stop the algorithm
        if (not remaining_choices):
            break
    return ans

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 3, 3, 5]
    n = len(arr)
    maxQuadrupleWays = findWays(arr, n)
    print (maxQuadrupleWays)

# This code is contributed by Chitranayal

```

**输出**：

```
1

```

**时间复杂度**：`O(NlogN)`，其中`N`是数组的大小



* * *

* * *



