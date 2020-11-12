# 检查`N`是否除以除以`K`以外的所有值的唯一余数

> 原文：[https://www.geeksforgeeks.org/check-if-n-leaves-only-distinct-remainders-on-division-by-all-values-up-to-k/](https://www.geeksforgeeks.org/check-if-n-leaves-only-distinct-remainders-on-division-by-all-values-up-to-k/)

给定两个整数`N`和`K`，任务是检查`N`在除以范围`[1, K]`内的所有整数时，是否仅剩下不同的余数。 如果是这样，则打印`Yes`。 否则，打印`No`。

**示例**：

> **输入**：`N = 5, K = 3`
>
> **输出**：`Yes`
>
> **说明**：
>
> ```
> (5 % 1) == 0
> (5 % 2) == 1
> (5 % 3) == 2
> ```
>
> 因为所有余数`{0,1,2,3}`是不同的。
> 
> **输入**：`N = 5, K = 4`
>
> **输出**：`No`
>
> **说明**：
>
> ```
> (5 % 1) == 0
> (5 % 2) == 1
> (5 % 3) == 2
> (5 % 4) == 1
> ```
> 
> 这不是不同的。

**方法**：

请按照以下步骤解决问题：

*   初始化[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)`S`

*   在`[1, K]`范围内迭代。

*   在每次迭代中，检查**集合**`S`中是否已经存在`N % i`。

*   如果不存在，则将`N % i`插入到集合`S`中。

*   否则，打印`No`并终止。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to check if all 
// remainders are distinct or not 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check and return 
// if all remainders are distinct 
bool is_distinct(long long n, long long k) 
{ 

    // Stores the remainder 
    unordered_set<long long> s; 

    for (int i = 1; i <= k; i++) { 

        // Calculate the remainder 
        long long tmp = n % i; 

        // If remainder already occurred 
        if (s.find(tmp) != s.end()) { 
            return false; 
        } 

        // Insert into the set 
        s.insert(tmp); 
    } 

    return true; 
} 

// Driver Code 
int main() 
{ 

    long long N = 5, K = 3; 

    if (is_distinct(N, K)) 
        cout << "Yes"; 
    else
        cout << "No"; 

    return 0; 
} 

```

## Java

```java

// Java program to check if all 
// remainders are distinct or not 
import java.util.*; 

class GFG{ 

// Function to check and return 
// if all remainders are distinct 
static boolean is_distinct(long n, long k) 
{ 

    // Stores the remainder 
    HashSet<Long> s = new HashSet<Long>(); 

    for(int i = 1; i <= k; i++) 
    { 

        // Calculate the remainder 
        long tmp = n % i; 

        // If remainder already occurred 
        if (s.contains(tmp)) 
        { 
            return false; 
        } 

        // Insert into the set 
        s.add(tmp); 
    } 
    return true; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    long N = 5, K = 3; 

    if (is_distinct(N, K)) 
        System.out.print("Yes"); 
    else
        System.out.print("No"); 
} 
} 

// This code is contributed by gauravrajput1 

```

## Python3

```py

# Python3 program to check if all 
# remainders are distinct or not 

# Function to check and return 
# if all remainders are distinct 
def is_distinct(n, k): 

    # Stores the remainder 
    s = set() 

    for i in range(1, k + 1): 

        # Calculate the remainder 
        tmp = n % i 

        # If remainder already occurred 
        if (tmp in s): 
            return False

        # Insert into the set  
        s.add(tmp) 

    return True

# Driver Code 
if __name__ == '__main__': 

    N = 5
    K = 3

    if (is_distinct(N, K)): 
        print("Yes") 
    else: 
        print("No") 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program to check if all 
// remainders are distinct or not 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to check and return 
// if all remainders are distinct 
static bool is_distinct(long n, long k) 
{ 

    // Stores the remainder 
    HashSet<long> s = new HashSet<long>(); 

    for(int i = 1; i <= k; i++) 
    { 

        // Calculate the remainder 
        long tmp = n % i; 

        // If remainder already occurred 
        if (s.Contains(tmp)) 
        { 
            return false; 
        } 

        // Insert into the set 
        s.Add(tmp); 
    } 
    return true; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    long N = 5, K = 3; 

    if (is_distinct(N, K)) 
        Console.Write("Yes"); 
    else
        Console.Write("No"); 
} 
} 

// This code is contributed by gauravrajput1

```

**输出**： 

```
Yes

```

**时间复杂度**：`O(K)`。

**辅助空间**：`O(K)`。



* * *

* * *



