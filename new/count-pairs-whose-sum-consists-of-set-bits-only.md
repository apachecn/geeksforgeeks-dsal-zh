# 计数对，其总和仅由设置的位组成

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是查找给定数组中无序对的计数，其总和包含所有设置位。

**示例**：

> **输入**：arr [] = {1,2,5}
> **输出**：2
> **说明**：满足条件的可能对为：
> 
> *   （1，2）：1 + 2 = 3（11）所有位均以 3 的二进制表示形式设置。
> *   2）（2，5）：2 + 5 = 7（111）所有位均以二进制表示形式 7 设置。
> 
> 因此，计数为 2。
> 
> **输入**：arr [] = {1,2,5,10}
> **输出**：3
> **说明**：满足条件的可能对为 ：
> 
> *   （1，2）：1 + 2 = 3（11）所有位均以 3 的二进制表示形式设置。
> *   （2，5）：2 + 5 = 7（111）所有位均以二进制表示形式 7 设置。
> *   （5，10）：5 + 10 = 15（1111）所有位均以 15 的二进制表示形式设置。

**天真的方法**：的想法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)并检查其[总和是否设置了所有位](https://www.geeksforgeeks.org/check-bits-number-set/)。 如果发现是真的，则在结果计数中计算该对。 检查所有对后，打印计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number num
// has all set bits or not
bool allSetBits(int num)
{
    // Find total bitsac
    int totalBits = log2(num) + 1;

    // Find count of set bit
    int setBits = __builtin_popcount(num);

    // Return true if all bit are set
    if (totalBits == setBits)
        return true;
    else
        return false;
}

// Function that find the count of
// pairs whose sum has all set bits
int countPairs(int arr[], int n)
{
    // Stores the count of pairs
    int ans = 0;

    // Generate all the pairs
    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++) {

            // Find the sum of current pair
            int sum = arr[i] + arr[j];

            // If all bits are set
            if (allSetBits(sum))
                ans++;
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countPairs(arr, N);

    return 0;
}

```

## Java

```java

// Java program for the 
// above approach
import java.util.*;
class GFG{

// Function to check if the 
// number num has all set 
// bits or not
static boolean allSetBits(int num)
{
  // Find total bitsac
  int totalBits = (int)Math.log(num) + 1;

  // Find count of set bit
  int setBits = Integer.bitCount(num);

  // Return true if all 
  // bit are set
  if (totalBits == setBits)
    return true;
  else
    return false;
}

// Function that find the 
// count of pairs whose sum 
// has all set bits
static int countPairs(int arr[], 
                      int n)
{
  // Stores the count 
  // of pairs
  int ans = 0;

  // Generate all the pairs
  for (int i = 0; i < n; i++) 
  {
    for (int j = i + 1; j < n; j++) 
    {
      // Find the sum of 
      // current pair
      int sum = arr[i] + arr[j];

      // If all bits are set
      if (allSetBits(sum))
        ans++;
    }
  }

  // Return the final count
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 2, 5, 10};
  int N = arr.length;

  // Function Call
  System.out.print(countPairs(arr, N));
}
}

// This code is contributed by gauravrajput1

```

## Python3

```py

# Python3 program for the above approach
from math import log2

# Function to check if the number num
# has all set bits or not
def allSetBits(num):

    # Find total bits
    totalBits = int(log2(num) + 1)

    # Find count of set bit
    setBits = bin(num).count('1')

    # Return true if all bit are set
    if (totalBits == setBits):
        return True
    else:
        return False

# Function that find the count of
# pairs whose sum has all set bits
def countPairs(arr, n):

    # Stores the count of pairs
    ans = 0

    # Generate all the pairs
    for i in range(n):
        for j in range(i + 1, n):

            # Find the sum of current pair
            sum = arr[i] + arr[j]

            # If all bits are set
            if (allSetBits(sum)):
                ans += 1

    # Return the final count
    return ans

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 5, 10 ]
    N = len(arr)

    # Function Call
    print(countPairs(arr, N))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for the 
// above approach
using System;
class GFG{

static int countSetBits(int n) 
{ 
  int count = 0; 

  while (n > 0) 
  { 
    count += n & 1; 
    n >>= 1; 
  } 
  return count; 
} 

// Function to check if the 
// number num has all set 
// bits or not
static bool allSetBits(int num)
{
  // Find total bitsac
  int totalBits = (int)Math.Log(num) + 1;

  // Find count of set bit
  int setBits = countSetBits(num);

  // Return true if all 
  // bit are set
  if (totalBits == setBits)
    return true;
  else
    return false;
}

// Function that find the 
// count of pairs whose sum 
// has all set bits
static int countPairs(int []arr, 
                      int n)
{
  // Stores the count 
  // of pairs
  int ans = 0;

  // Generate all the pairs
  for (int i = 0; i < n; i++) 
  {
    for (int j = i + 1; j < n; j++) 
    {
      // Find the sum of 
      // current pair
      int sum = arr[i] + arr[j];

      // If all bits are set
      if (allSetBits(sum))
        ans++;
    }
  }

  // Return the readonly count
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {1, 2, 5, 10};
  int N = arr.Length;

  // Function Call
  Console.Write(countPairs(arr, N));
}
}

// This code is contributed by Princi Singh

```

**Output**

```
3
```

***时间复杂度**：O（N <sup>2</sup> log N），其中 N 是给定数组的大小。*

***辅助空间**：O（N）*

**高效方法**：关键观察结果是，从 **0** 到 **N** 仅存在 **log N** 个数字，其中包含所有设置位。 此属性可用于优化上述方法。 请按照以下步骤解决问题：

*   将所有 **log（MAX_INTEGER）**元素存储在数组 **setArray []** 中。

*   将数组 **arr []** 的所有元素映射到[映射数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，其中元素是键，其频率是值。

*   [遍历范围为 **[0，N – 1]** 的给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr []** ，并在嵌套循环中遍历数组 **setArray [] [HTG7 从 **j = 0 到 log（MAX_INTEGER）**，然后将 **ans** 递增 **map [setArray [j] – arr [i]]** 其中 **ans [** 存储所需对的总数。**

*   由于存在重复计数，因为**（a，b）**和**（b，a）**被计数了两次。 因此，打印 **ans / 2** 的值以获得所需的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Store numbers having all set bits
vector<int> setArray;

// Store frequency of values in arr[]
map<int, int> mp;

// Function to fill setArray[] with
// numbers that have all set bits
void fillsetArray()
{
    for (int i = 1; i < 31; i++) {
        setArray.push_back((1 << i) - 1);
    }
}

// Function to find the count of pairs
// whose sum contains all set bits
int countPairs(int arr[], int n)
{
    // Stores the count of pairs
    int ans = 0;

    fillsetArray();

    // Hash the values of arr[] in mp
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Iterate over the range [0, 30]
        for (int j = 0; j < 30; j++) {

            // Find the difference
            int value = setArray[j] - arr[i];

            // Update the final count
            ans += mp[value];
        }
    }

    // Return the final count
    return ans / 2;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countPairs(arr, N);

    return 0;
}

```

## Java

```java

// Java program for the 
// above approach
import java.util.*;
class GFG{

// Store numbers having
// all set bits
static Vector<Integer> setArray = 
              new Vector<>();

// Store frequency of 
// values in arr[]
static HashMap<Integer,
               Integer> mp = new HashMap<Integer,
                                         Integer>();

// Function to fill setArray[] 
// with numbers that have all 
// set bits
static void fillsetArray()
{
  for (int i = 1; i < 31; i++) 
  {
    setArray.add((1 << i) - 1);
  }
}

// Function to find the count 
// of pairs whose sum contains 
// all set bits
static int countPairs(int arr[], 
                      int n)
{
  // Stores the count 
  // of pairs
  int ans = 0;

  fillsetArray();

  // Hash the values of 
  // arr[] in mp
  for (int i = 0; i < n; i++)
    if(mp.containsKey(arr[i]))
    {
      mp.put(arr[i], 
             mp.get(arr[i]) + 1);
    }
    else
    {
      mp.put(arr[i], 1);
    }

  // Traverse the array arr[]
  for (int i = 0; i < n; i++) 
  {
    // Iterate over the range 
    // [0, 30]
    for (int j = 0; j < 30; j++) 
    {
      // Find the difference
      int value = setArray.get(j) - 
        arr[i];

      // Update the final count
      if(mp.containsKey(value))
        ans += mp.get(value);
    }
  }

  // Return the final count
  return ans / 2;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 2, 5, 10};
  int N = arr.length;

  // Function Call
  System.out.print(countPairs(arr, N));
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program for the 
# above approach
from collections import defaultdict

# Store numbers having 
# all set bits
setArray = []

# Store frequency of values 
# in arr[]
mp = defaultdict (int)

# Function to fill setArray[] with
# numbers that have all set bits
def fillsetArray():

    for i in range (1, 31):
        setArray.append((1 << i) - 1)

# Function to find the 
# count of pairs whose sum 
# contains all set bits
def countPairs(arr, n):

    # Stores the count of pairs
    ans = 0

    fillsetArray()

    # Hash the values of 
    # arr[] in mp
    for i in range (n):
        mp[arr[i]] += 1

    # Traverse the array arr[]
    for i in range (n):

        # Iterate over the range 
        # [0, 30]
        for j in range (30):

            # Find the difference
            value = setArray[j] - arr[i]

            # Update the final count
            ans += mp[value]

    # Return the final count
    return ans // 2

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 5, 10]
    N = len(arr) 

    # Function Call
    print (countPairs(arr, N))

# This code is contributed by Chitranayal

```

**Output**

```
3
```

***时间复杂度**：O（N * 32），其中 N 是给定数组的大小。*

***辅助空间**：O（N）*



* * *

* * *



