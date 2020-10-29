# 检查是否可以通过交换字符使数组的所有字符串相同

> 原文：[https://www.geeksforgeeks.org/check-if-all-strings-of-an-array-can-be-made-same-by-interchanging-characters/](https://www.geeksforgeeks.org/check-if-all-strings-of-an-array-can-be-made-same-by-interchanging-characters/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，该数组由相等长度的字符串组成，任务是检查是否可以使数组的所有字符串 通过将一个字符串的任何字符与同一字符串或另一字符串的任何字符交换来确定是否相等。

**注意**：执行 **0** 或以上次。

**示例**：

> **输入**：arr [] **= {** *“ fdd”，“ fhh”}*
> **输出**：*是*
> **说明**：
> 交换（arr [0] [1]，arr [1] [1]）然后 arr [] = {*“ fhd”，“ fdh”* }
> 交换（arr [1] [1]，arr [1] [2]）然后 arr [] = {*“ fhd”，“ fhd”* }。 因此，可以使所有字符串相等。
> 
> **输入**：arr [] = {*“ fde”，“ fhg”* }
> **输出**：否

**方法**：该问题可以通过计算给定数组的每个字符的[频率并检查是否可以被 **N** 整除来解决。 请按照以下步骤解决问题：](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)

1.  初始化数组 **hash [256] = {0}** 以存储字符的频率。

2.  遍历 **hash []** 数组，并检查所有字符的频率是否可被 **N** 整除。

3.  如果所有字符的频率都可以被 **N** 整除，则打印**是**。

4.  否则，打印**否**。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Fuction to check if all strings 
// are equal after swap operations 
bool checkEqual(string arr[], int N) 
{ 
    // Stores the frequency 
    // of characters 
    int hash[256] = { 0 }; 

    // Stores the length of string 
    int M = arr[0].length(); 

    // Traverse the array 
    for (int i = 0; i < N; i++) { 
        // Traverse each string 
        for (int j = 0; j < M; j++) { 
            hash[arr[i][j]]++; 
        } 
    } 

    // Check if frequency of character 
    // is divisible by N 
    for (int i = 0; i < 256; i++) { 
        if (hash[i] % N != 0) { 
            return false; 
        } 
    } 

    return true; 
} 

// Driver Code 
int main() 
{ 

    string arr[] = { "fdd", "fhh" }; 
    int N = sizeof(arr) / sizeof(arr[0]); 

    if (checkEqual(arr, N)) { 
        cout << "Yes"; 
    } 
    else { 
        cout << "No"; 
    } 

    return 0; 
}

```

## Java

```java

// Java Program to implement 
// the above approach 
class GFG{ 

// Fuction to check if all Strings 
// are equal after swap operations 
static boolean checkEqual(String arr[],  
                          int N) 
{ 
  // Stores the frequency 
  // of characters 
  int hash[] = new int[256]; 

  // Stores the length of String 
  int M = arr[0].length(); 

  // Traverse the array 
  for (int i = 0; i < N; i++)  
  { 
    // Traverse each String 
    for (int j = 0; j < M; j++)  
    { 
      hash[arr[i].charAt(j)]++; 
    } 
  } 

  // Check if frequency of character 
  // is divisible by N 
  for (int i = 0; i < 256; i++)  
  { 
    if (hash[i] % N != 0)  
    { 
      return false; 
    } 
  } 

  return true; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
  String arr[] = {"fdd", "fhh"}; 
  int N = arr.length; 

  if (checkEqual(arr, N))  
  { 
    System.out.print("Yes"); 
  } 
  else 
  { 
    System.out.print("No"); 
  } 
} 
} 

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Fuction to check if all strings  
# are equal after swap operations 
def checkEqual(arr, N): 

    # Stores the frequency 
    # of characters 
    hash = [0] * 256

    # Stores the length of string 
    M = len(arr[0]) 

    # Traverse the array 
    for i in range(N): 

        # Traverse each string 
        for j in range(M): 
            hash[ord(arr[i][j])] += 1

    # Check if frequency of character 
    # is divisible by N 
    for i in range(256): 
        if(hash[i] % N != 0): 
            return False

    return True

# Driver Code 
arr = [ "fdd", "fhh" ] 
N = len(arr) 

# Function call 
if(checkEqual(arr, N)): 
    print("Yes") 
else: 
    print("No") 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 

class GFG{ 

// Fuction to check if all Strings 
// are equal after swap operations 
static bool checkEqual(String []arr,  
                       int N) 
{ 

    // Stores the frequency 
    // of characters 
    int []hash = new int[256]; 

    // Stores the length of String 
    int M = arr[0].Length; 

    // Traverse the array 
    for(int i = 0; i < N; i++)  
    { 

        // Traverse each String 
        for(int j = 0; j < M; j++)  
        { 
            hash[arr[i][j]]++; 
        } 
    } 

    // Check if frequency of character 
    // is divisible by N 
    for(int i = 0; i < 256; i++)  
    { 
        if (hash[i] % N != 0)  
        { 
            return false; 
        } 
    } 
    return true; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String []arr = { "fdd", "fhh" }; 
    int N = arr.Length; 

    if (checkEqual(arr, N))  
    { 
        Console.Write("Yes"); 
    } 
    else
    { 
        Console.Write("No"); 
    } 
} 
} 

// This code is contributed by Amit Katiyar

```

**Output:** 

```
Yes

```

***时间复杂度**：`O(n)`*

***辅助空间**：O（1）*



* * *

* * *



