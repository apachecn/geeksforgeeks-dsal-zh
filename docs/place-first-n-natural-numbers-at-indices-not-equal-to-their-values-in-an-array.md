# 将前 N 个自然数放在数组中与其值不相等的索引处

> 原文:[https://www . geesforgeks . org/place-first-n-natural-numbers-at-index-不等于数组中的值/](https://www.geeksforgeeks.org/place-first-n-natural-numbers-at-indices-not-equal-to-their-values-in-an-array/)

给定一个整数 **N** ( *N > 1* ，任务是将范围**【1，N】**中的所有整数排列在一个数组中，使得没有一个元素与它们在数组中出现的索引(*基于 1 的索引*)相同。

**示例:**

> **输入:** N = 2
> **输出:** 2 1
> **解释:**大小为 2 的数组唯一可能的排列方式是 2 1。
> 
> **输入:** N=5
> **输出:** 2 1 5 3 4
> **解释:**大小为 5 的数组的一种可能排列是 2 1 5 3 4l。

**方法:**最简单的想法是将 **N** 放在第一个索引处，将其余元素**【1，N–1】**放在其余索引处。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to place first N natural
// numbers in an array such that none
// of the values are equal to its indices
void generatepermutation(int N)
{

  // Stores the required array
    vector<int> answer;

    // Place N at the first position
    answer.push_back(N);

    // Iterate the range [1, N)
    for (int i = 1; i < N; i++)
    {
        // Append elements to the sequence
        answer.push_back(i);
    }

    // Print the sequence
    for(int i:answer) cout << i << " ";

}

// Driver Code
int main()
{
  int N = 4;
  generatepermutation(N);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to place first N natural
// numbers in an array such that none
// of the values are equal to its indices
static void generatepermutation(int N)
{

  // Stores the required array
    Vector<Integer> answer = new Vector<Integer>();

    // Place N at the first position
    answer.add(N);

    // Iterate the range [1, N)
    for (int i = 1; i < N; i++)
    {
        // Append elements to the sequence
        answer.add(i);
    }

    // Print the sequence
    for(int i:answer) System.out.print(i+ " ");
}

// Driver Code
public static void main(String[] args)
{
  int N = 4;
  generatepermutation(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to place first N natural
# numbers in an array such that none
# of the values are equal to its indices
def generatepermutation(N):

  # Stores the required array
    answer = []

    # Place N at the first position
    answer.append(N)

    # Iterate the range [1, N)
    for i in range(1, N):

        # Append elements to the sequence
        answer.append(i)

    # Print the sequence
    print(*answer)

# Driver Code
N = 4
generatepermutation(N)
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to place first N natural
// numbers in an array such that none
// of the values are equal to its indices
static void generatepermutation(int N)
{

    // Stores the required array
    int[] answer = new int[N];

    // Place N at the first position
    answer[0] = N;

    // Iterate the range [1, N)
    for (int i = 1; i < N; i++)
    {

        // Append elements to the sequence
        answer[i] = i;
    }

    // Print the sequence
    foreach(int i in answer) Console.Write(i+ " ");
}

// Driver Code
static public void Main ()
{
  int N = 4;
  generatepermutation(N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to place first N natural
      // numbers in an array such that none
      // of the values are equal to its indices
      function generatepermutation(N)
      {
        // Stores the required array
        var answer = [];

        // Place N at the first position
        answer.push(N);
        console.log(answer);
        // Iterate the range [1, N)
        for (var i = 1; i < N; i++) {
          console.log(answer);
          // Append elements to the sequence
          answer.push(i);
        }

        // Print the sequence
        for (var i in answer)
        document.write(answer[i] + "  ");
      }

      // Driver Code
      var N = 4;
      generatepermutation(N);

</script>
```

**Output**

```
4 1 2 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)