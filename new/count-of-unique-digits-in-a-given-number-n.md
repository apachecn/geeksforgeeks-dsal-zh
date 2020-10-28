# 给定数字 N 中的唯一数字计数

给定数字 **N** ，任务是计算给定数字中唯一数字的数量。

**示例**：

> **输入**：N = 22342
> **输出**：2
> **说明**：
> 数字 3 和 4 仅出现一次。 因此，输出为 2。
> 
> **输入**：N = 99677
> **输出**：1
> **说明**：
> 数字 6 仅出现一次。 因此，输出为 1。

**天真的方法**：通过这种方法，可以使用两个嵌套循环来解决问题。 在第一个循环中，从数字的第一个数字到最后一个数字一个一个地遍历。 然后，对于第一个循环中的每个数字，运行第二个循环，并搜索该数字是否出现在数字的其他任何地方。 如果否，则将所需的计数增加 1。最后，打印计算出的所需计数。

***时间复杂度**：O（L <sup>2</sup> ）*

***辅助空间**：O（1）*

**有效方法**：的想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来存储数字的频率，然后以 *1* 的频率对数字进行计数。 请按照以下步骤解决问题：

1.  为数字 0-9 创建一个大小为 10 的哈希表。 最初将每个索引存储为 0。

2.  现在，对于数字 N 的每个数字，在哈希表中增加该索引的计数。

3.  遍历哈希表并计算值等于 1 的索引。

4.  最后，打印/返回此计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <iostream> 
using namespace std; 

// Function that returns the count of 
// unique digits of the given number 
int countUniqueDigits(int N) 
{ 
    // Initialize a variable to store 
    // count of unique digits 
    int res = 0; 

    // Initialize cnt array to store 
    // digit count 
    int cnt[10] = { 0 }; 

    // Iterate through the digits of N 
    while (N > 0) { 

        // Retrieve the last digit of N 
        int rem = N % 10; 

        // Increase the count 
        // of the last digit 
        cnt[rem]++; 

        // Remove the last digit of N 
        N = N / 10; 
    } 

    // Iterate through the cnt array 
    for (int i = 0; i < 10; i++) { 

        // If frequency of 
        // digit is 1 
        if (cnt[i] == 1) { 

            // Increment the count 
            // of unique digits 
            res++; 
        } 
    } 

    // Return the count/ of unique digit 
    return res; 
} 

// Driver Code 
int main() 
{ 
    // Given array arr[] 
    int N = 2234262; 

    // Function Call 
    cout << countUniqueDigits(N); 
    return 0; 
}

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG { 

    // Function that returns the count 
    // of unique digits of number N 
    public static void
    countUniqueDigits(int N) 
    { 
        // Initialize a variable to 
        // store count of unique digits 
        int res = 0; 

        // Initialize cnt array to 
        // store digit count 
        int cnt[] = { 0, 0, 0, 0, 0, 
                      0, 0, 0, 0, 0 }; 

        // Iterate through digits of N 
        while (N > 0) { 

            // Retrieve the last 
            // digit of N 
            int rem = N % 10; 

            // Increase the count 
            // of the last digit 
            cnt[rem]++; 

            // Remove the last 
            // digit of N 
            N = N / 10; 
        } 

        // Iterate through the 
        // cnt array 
        for (int i = 0; 
             i < cnt.length; i++) { 

            // If frequency of 
            // digit is 1 
            if (cnt[i] == 1) { 

                // Increment the count 
                // of unique digits 
                res++; 
            } 
        } 

        // Return the count of unique digit 
        System.out.println(res); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given Number N 
        int N = 2234262; 

        // Function Call 
        countUniqueDigits(N); 
    } 
}

```

## Python3

```py

# Python3 program for the above approach  

# Function that returns the count of  
# unique digits of the given number  
def countUniqueDigits(N): 

    # Initialize a variable to store 
    # count of unique digits 
    res = 0

    # Initialize cnt list to store 
    # digit count 
    cnt = [0] * 10

    # Iterate through the digits of N 
    while (N > 0): 

        # Retrieve the last digit of N 
        rem = N % 10

        # Increase the count 
        # of the last digit 
        cnt[rem] += 1

        # Remove the last digit of N 
        N = N // 10

    # Iterate through the cnt list 
    for i in range(10): 

        # If frequency of 
        # digit is 1 
        if (cnt[i] == 1): 

            # Increment the count 
            # of unique digits 
            res += 1

    # Return the count of unique digit 
    return res  

# Driver Code 

# Given number N 
N = 2234262

# Function call  
print(countUniqueDigits(N))  

# This code is contributed by vishu2908 

```

## C#

```cs

// C# program for the above approach 
using System; 

class GFG{ 

// Function that returns the count 
// of unique digits of number N 
public static void countUniqueDigits(int N) 
{ 

    // Initialize a variable to 
    // store count of unique digits 
    int res = 0; 

    // Initialize cnt array to 
    // store digit count 
    int[] cnt = { 0, 0, 0, 0, 0, 
                  0, 0, 0, 0, 0 }; 

    // Iterate through digits of N 
    while (N > 0)  
    { 

        // Retrieve the last 
        // digit of N 
        int rem = N % 10; 

        // Increase the count 
        // of the last digit 
        cnt[rem]++; 

        // Remove the last 
        // digit of N 
        N = N / 10; 
    } 

    // Iterate through the 
    // cnt array 
    for(int i = 0; i < cnt.Length; i++) 
    { 

        // If frequency of 
        // digit is 1 
        if (cnt[i] == 1)  
        { 

            // Increment the count 
            // of unique digits 
            res++; 
        } 
    } 

    // Return the count of unique digit 
    Console.WriteLine(res); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Given Number N 
    int N = 2234262; 

    // Function Call 
    countUniqueDigits(N); 
} 
} 

// This code is contributed by jrishabh99 

```

**Output:**

```
3

```

**时间复杂度**：*O（N）*，其中 *N* 是该数字的位数。

***辅助空间**：O（1）*

**注意**：由于使用的哈希表的大小仅为 10，因此其时间和空间复杂度将接近恒定。 因此，在上述时间和辅助空间中不计入。



* * *

* * *



