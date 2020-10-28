# 基于给定条件的具有相等总和的对的最大计数

给定长度为 **N** 的数组 **arr []** 包含范围为 **[1，N]** 的数组元素，任务是查找具有 假设数组中的任何元素只能是单个对的一部分，则**等于**之和。

**示例**：

> **输入**：arr [] = {1、4、1、4}
> **输出**：2
> **说明**：对{{1，4 }，{1，4}}的总和为 5。
> 
> **输入**：arr [] = {1、2、4、3、3、5、6}
> **输出**：3
> **说明**：对{{1，5}，{2，4}，{3，3}}的和为 6。

**方法**：

可以从数组中获得的对的总和不能小于数组最小元素的 2 倍，也不能大于最大元素的 2 倍，因此我们找到了每个数组可以获取的最大对数。 这些末端之间的总和，并输出其中的最大值。

实现此方法的方法如下：

1.  存储给定数组的所有元素的频率。

2.  遍历肢体之间的每个总和，并计算我们可以从这些总和中获得的最大对数。

3.  打印获得的所有此类对中的最大计数以得出相同的总和。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum count
// of pairs having equal sum
int maxCount(vector<int>& freq, int mini, int maxi)
{

    // Size of the array
    int n = freq.size() - 1;

    int ans = 0;

    // Iterate through evey sum of pairs
    // possible from the given array
    for (int sum = 2 * mini; sum <= 2 * maxi; ++sum) {

        // Count of pairs with given sum
        int possiblePair = 0;

        for (int firElement = 1; firElement < (sum + 1) / 2;
             firElement++) {

            // Check for a possible pair
            if (sum - firElement <= maxi) {

                // Update count of possible pair
                possiblePair += min(freq[firElement],
                                    freq[sum - firElement]);
            }
        }

        if (sum % 2 == 0) {
            possiblePair += freq[sum / 2] / 2;
        }

        // Update the answer by taking the
        // pair which is maximum
        // for every possible sum
        ans = max(ans, possiblePair);
    }

    // Return the max possible pair
    return ans;
}

// Function to return the
// count of pairs
int countofPairs(vector<int>& a)
{

    // Size of the array
    int n = a.size();
    int mini = *min_element(a.begin(), a.end()),
        maxi = *max_element(a.begin(), a.end());

    // Stores the frequencies
    vector<int> freq(n + 1, 0);

    // Count the frequecy
    for (int i = 0; i < n; ++i)
        freq[a[i]]++;

    return maxCount(freq, mini, maxi);
}

// Driver Code
int main()
{

    vector<int> a = { 1, 2, 4, 3, 3, 5, 6 };

      // Function Call
    cout << countofPairs(a) << endl;
}

```

## Java

```java

// Java program to implement
// the above approach
class GFG{

// Function to find the maximum count
// of pairs having equal sum
static int maxCount(int[] freq,int maxi,int mini)
{

    // Size of the array
    int n = freq.length - 1;

    int ans = 0;

    // Iterate through evey sum of pairs
    // possible from the given array
    for(int sum = 2*mini; sum <= 2 * maxi; ++sum)
    {

        // Count of pairs with given sum
        int possiblePair = 0;

        for(int firElement = 1; 
                firElement < (sum + 1) / 2;
                firElement++) 
        {

            // Check for a possible pair
            if (sum - firElement <= maxi)
            {

                // Update count of possible pair
                possiblePair += Math.min(freq[firElement],
                                   freq[sum - firElement]);
            }
        }

        if (sum % 2 == 0)
        {
            possiblePair += freq[sum / 2] / 2;
        }

        // Update the answer by taking the
        // pair which is maximum
        // for every possible sum
        ans = Math.max(ans, possiblePair);
    }

    // Return the max possible pair
    return ans;
}

// Function to return the
// count of pairs
static int countofPairs(int[] a)
{

    // Size of the array
    int n = a.length;

    // Stores the frequencies
    int []freq = new int[n + 1];
      int maxi = -1;
      int mini = n+1;
    for(int i = 0;i<n;i++) 
    {
          maxi = Math.max(maxi,a[i]);
          mini = Math.min(mini,a[i]);
    }
    // Count the frequecy
    for(int i = 0; i < n; ++i)
        freq[a[i]]++;

    return maxCount(freq,maxi,mini);
}

// Driver Code
public static void main(String[] args)
{
    int []a = { 1, 2, 4, 3, 3, 5, 6 };

    System.out.print(countofPairs(a) + "\n");
}
}

// This code is contributed by Princi Singh

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to find the maximum count
# of pairs having equal sum

def maxCount(freq, maxi, mini):

    # Size of the array
    n = len(freq) - 1

    ans = 0

    # Iterate through evey sum of pairs
    # possible from the given array
    sum = 2*mini
    while sum <= 2 * maxi:

        # Count of pairs with given sum
        possiblePair = 0

        for firElement in range(1, (sum + 1) // 2):

            # Check for a possible pair
            if (sum - firElement <= maxi):

                # Update count of possible pair
                possiblePair += min(freq[firElement],
                                    freq[sum - firElement])

        sum += 1

        if (sum % 2 == 0):
            possiblePair += freq[sum // 2] // 2

        # Update the answer by taking the
        # pair which is maximum
        # for every possible sum
        ans = max(ans, possiblePair)

    # Return the max possible pair
    return ans

# Function to return the
# count of pairs

def countofPairs(a):

    # Size of the array
    n = len(a)

    # Stores the frequencies
    freq = [0] * (n + 1)

    maxi = -1
    mini = n+1

    for i in range(len(a)):
        maxi = max(maxi, a[i])
        mini = min(mini, a[i])
    # Count the frequecy
    for i in range(n):
        freq[a[i]] += 1

    return maxCount(freq, maxi, mini)

# Driver Code
if __name__ == "__main__":

    a = [1, 2, 4, 3, 3, 5, 6]

    print(countofPairs(a))

# This code is contributed by chitranayal

```

## C#

```cs

// C# program to implement
// the above approach
using System;

class GFG {

    // Function to find the maximum count
    // of pairs having equal sum
    static int maxCount(int[] freq)
    {

        // Size of the array
        int n = freq.Length - 1;

        int ans = 0;

        // Iterate through evey sum of pairs
        // possible from the given array
        for (int sum = 2; sum <= 2 * n; ++sum) {

            // Count of pairs with given sum
            int possiblePair = 0;

            for (int firElement = 1;
                 firElement < (sum + 1) / 2; firElement++) {

                // Check for a possible pair
                if (sum - firElement <= n) {

                    // Update count of possible pair
                    possiblePair
                        += Math.Min(freq[firElement],
                                    freq[sum - firElement]);
                }
            }

            if (sum % 2 == 0) {
                possiblePair += freq[sum / 2] / 2;
            }

            // Update the answer by taking the
            // pair which is maximum
            // for every possible sum
            ans = Math.Max(ans, possiblePair);
        }

        // Return the max possible pair
        return ans;
    }

    // Function to return the
    // count of pairs
    static int countofPairs(int[] a)
    {

        // Size of the array
        int n = a.Length;

        // Stores the frequencies
        int[] freq = new int[n + 1];

        // Count the frequecy
        for (int i = 0; i < n; ++i)
            freq[a[i]]++;

        return maxCount(freq);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 1, 2, 4, 3, 3, 5, 6 };

        Console.Write(countofPairs(a) + "\n");
    }
}

// This code is contributed by Amit Katiyar

```

**Output**

```
3

```

**时间复杂度**：*O（N <sup>2</sup> ）*

**辅助空间**：*O（N）*



* * *

* * *



