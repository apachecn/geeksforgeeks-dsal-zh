# 检查给定堆栈中是否存在所有数组元素

> 原文：[https://www.geeksforgeeks.org/check-if-all-array-elements-are-present-in-a-given-stack-or-not/](https://www.geeksforgeeks.org/check-if-all-array-elements-are-present-in-a-given-stack-or-not/)

给定一个整数`S`的堆栈和一个整数`arr[]`的数组，任务是检查堆栈中是否存在所有数组元素。

**示例**：

> **输入**：`S = {10, 20, 30, 40, 50}, arr[] = {20, 30}`
> 
> **输出**：`Yes`
> 
> **说明**：
> 
> 元素 20 和 30 存在于堆栈中。
> 
> **输入**：`S = {50, 60}, arr[] = {60, 50}`
> 
> **输出**：是
> 
> **说明**：堆栈中存在元素 50 和 60。

**方法**：这个想法是要维持[`Hashmap`](https://www.geeksforgeeks.org/hashing-data-structure/)中数组元素的频率。 现在，当堆栈不为空时，请继续从堆栈中弹出元素，并降低`Hashmap`中元素的频率。 最后，当堆栈为空时，检查哈希映射中每个元素的频率是否为零。 如果发现是真的，则打印是。 否则，打印编号

下面是上述方法的实现：

## C++

```cpp

// C++ program of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if all array
// elements is present in the stack
bool checkArrInStack(stack<int>s, int arr[],
                                  int n)
{
    map<int, int>freq;

    // Store the frequency
    // of array elements
    for(int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Loop while the elements in the 
    // stack is not empty
    while (!s.empty())
    {
        int poppedEle = s.top();
        s.pop();

        // Condition to check if the
        // element is present in the stack
        if (freq[poppedEle])
            freq[poppedEle] -= 1;
    }
    if (freq.size() == 0)
        return 0;

    return 1;
}

// Driver code
int main()
{
    stack<int>s;
    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);
    s.push(50);

    int arr[] = {20, 30};

    int n = sizeof arr / sizeof arr[0];

    if (checkArrInStack(s, arr, n))
        cout << "YES\n";
    else
        cout << "NO\n";
}

// This code is contributed by Stream_Cipher

```

## Java

```java

// Java program of 
// the above approach
import java.util.*;
class GFG{

// Function to check if all array
// elements is present in the stack
static boolean checkArrInStack(Stack<Integer>s, 
                               int arr[], int n)
{
  HashMap<Integer,
          Integer>freq = new HashMap<Integer,
                                     Integer>();

  // Store the frequency
  // of array elements
  for(int i = 0; i < n; i++)
    if(freq.containsKey(arr[i]))
      freq.put(arr[i], freq.get(arr[i]) + 1);
  else
    freq.put(arr[i], 1);

  // Loop while the elements in the 
  // stack is not empty
  while (!s.isEmpty())
  {
    int poppedEle = s.peek();
    s.pop();

    // Condition to check if the
    // element is present in the stack
    if (freq.containsKey(poppedEle))
      freq.put(poppedEle, freq.get(poppedEle) - 1);
  }
  if (freq.size() == 0)
    return false;
  return true;
}

// Driver code
public static void main(String[] args)
{
  Stack<Integer> s = new Stack<Integer>();
  s.add(10);
  s.add(20);
  s.add(30);
  s.add(40);
  s.add(50);

  int arr[] = {20, 30};
  int n = arr.length;

  if (checkArrInStack(s, arr, n))
    System.out.print("YES\n");
  else
    System.out.print("NO\n");
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python program of 
# the above approach

# Function to check if all array
# elements is present in the stack
def checkArrInStack(s, arr):
  freq = {}

  # Store the frequency
  # of array elements
  for ele in arr:
    freq[ele] = freq.get(ele, 0) + 1

  # Loop while the elements in the 
  # stack is not empty
  while s:
    poppedEle = s.pop()

    # Condition to check if the
    # element is present in the stack
    if poppedEle in freq:
      freq[poppedEle] -= 1

      if not freq[poppedEle]:
        del freq[poppedEle]
  if not freq:
    return True
  return False

# Driver Code
if __name__ == "__main__":
  s = [10, 20, 30, 40, 50]
  arr = [20, 30]

  if checkArrInStack(s, arr):
    print("YES")
  else:
    print("NO")

```

## C#

```cs

// C# program of 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check if all array
// elements is present in the stack
static bool checkArrInStack(Stack<int>s, 
                            int []arr, int n)
{
  Dictionary<int,
             int>freq = new Dictionary<int,
                                       int>();

  // Store the frequency
  // of array elements
  for(int i = 0; i < n; i++)
    if(freq.ContainsKey(arr[i]))
      freq[arr[i]] = freq[arr[i]] + 1;
  else
    freq.Add(arr[i], 1);

  // Loop while the elements in the 
  // stack is not empty
  while (s.Count != 0)
  {
    int poppedEle = s.Peek();
    s.Pop();

    // Condition to check if the
    // element is present in the stack
    if (freq.ContainsKey(poppedEle))
      freq[poppedEle] = freq[poppedEle] - 1;
  }
  if (freq.Count == 0)
    return false;
  return true;
}

// Driver code
public static void Main(String[] args)
{
  Stack<int> s = new Stack<int>();
  s.Push(10);
  s.Push(20);
  s.Push(30);
  s.Push(40);
  s.Push(50);
  int []arr = {20, 30};
  int n = arr.Length;

  if (checkArrInStack(s, arr, n))
    Console.Write("YES\n");
  else
    Console.Write("NO\n");
}
}

// This code is contributed by 29AjayKumar

```

**输出**： 

```
YES

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



