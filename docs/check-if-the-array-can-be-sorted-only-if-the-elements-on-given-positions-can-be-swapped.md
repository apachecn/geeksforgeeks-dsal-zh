# 检查只有给定位置的元素可以交换时，数组才能排序

> 原文:[https://www . geesforgeks . org/check-if-the-array-can-sorted-only-if-the-elements-on-给定位置-可以交换/](https://www.geeksforgeeks.org/check-if-the-array-can-be-sorted-only-if-the-elements-on-given-positions-can-be-swapped/)

给定一个长度为 **N** 的数组**arr【】**和另一个包含{a <sub>1</sub> 、a <sub>2</sub> 、… a <sub>k</sub> }的数组**P【】**,该数组代表给定数组 arr【】的位置，任务是检查该数组是否只能通过交换元素“arr ”[ a<sub>I</sub>、arr[a <sub>i+1</sub> ]来排序，其中“I”
**示例:**

> **输入:** arr[] = {3，2，1}，P[] = {1，2}
> **输出:**是
> **解释:**
> 最初，i = 1(即)第一个元素和第二个元素交换。因此，arr[0] < = > arr[1]。arr[] = {2，3，1}。
> 同样，i = 2(即)第二元素和第三元素互换。arr[] = {2，1，3}。
> 最后，i = 1(即)第一元素和第二元素交换。arr[] = {1，2，3}。
> 因为这个数组是排序的，所以给定的数组可以排序。
> **输入:** arr[] = {5，3，-4，1，12}，P[] = {2，4，3}
> **输出:**否

**逼近**:思路是用[双指针逼近](https://www.geeksforgeeks.org/two-pointers-technique/)检查数组是否可以排序。

*   最初，我们创建一个大小为 **N** 的位置数组 **pos[]** 。该阵列将用于标记阵列中的给定位置 **P[]** 。那就是:

```
if j = ai (1 ≤ i ≤ K)
then the element pos[ai-1] will be 1
else 0
```

*   现在，遍历数组并检查 **pos[i] = 1** 是否存在。
*   如果我们遇到 **pos[i]=1** ，我们将迭代器存储在一个临时变量中，然后我们用值 **1** 递增迭代器，直到我们连续拥有 **pos[i]=1** ，即，

```
j = i
while (j < N and pos[j]) 
    j=j+1
```

*   在这个增量之后，我们对从 I 到 j+1 得到的这个片段进行[排序，最后，在我们必须检查的向量中的位置 j 之后进行检查，因为我们已经排序到这个片段。](https://www.geeksforgeeks.org/sorting-algorithms/)

```
Sort(arr[i] to arr[j+1])
i=j
```

*   最后，在这个循环完成后，我们必须检查数组是否已经排序。

以下是上述方法的实现:

## C++

```
// C++ program to check if the array
// can be sorted only if the elements
// on the given positions can be swapped

#include <bits/stdc++.h>
using namespace std;

// Function to check if the array can
// be sorted only if the elements on
// the given positions can be swapped
void check_vector(vector<int> A, int n,
                vector<int> p)
{

    // Creating an array for marking
    // the positions
    vector<int> pos(A.size());

    // Iterating through the array and
    // mark the positions
    for (int i = 0; i < p.size(); i++) {
        pos[p[i] - 1] = 1;
    }

    int flag = 1;

    // Iterating through the given array
    for (int i = 0; i < n; i++) {
        if (pos[i] == 0)
            continue;
        int j = i;

        // If pos[i] is 1, then incrementing
        // till 1 is continuously present in pos
        while (j < n && pos[j])
            ++j;

        // Sorting the required segment
        sort(A.begin() + i, A.begin() + j + 1);
        i = j;
    }

    // Checking if the vector is sorted or not
    for (int i = 0; i < n - 1; i++) {
        if (A[i] > A[i + 1]) {
            flag = 0;
            break;
        }
    }

    // Print yes if it is sorted
    if (flag == 1)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    vector<int> A{ 3, 2, 1 };
    vector<int> p{ 1, 2 };

    check_vector(A, A.size(), p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the array
// can be sorted only if the elements
// on the given positions can be swapped
import java.util.Arrays;

class GFG{

// Function to check if the array can
// be sorted only if the elements on
// the given positions can be swapped
public static void check_vector(int[] A,
                                int n,
                                int[] p)
{

    // Creating an array for marking
    // the positions
    int[] pos = new int[A.length];

    // Iterating through the array and
    // mark the positions
    for(int i = 0; i < p.length; i++)
    {
        pos[p[i] - 1] = 1;
    }

    int flag = 1;

    // Iterating through the given array
    for(int i = 0; i < n; i++)
    {
        if (pos[i] == 0)
            continue;

        int j = i;

        // If pos[i] is 1, then incrementing
        // till 1 is continuously present in pos
        while (j < n && pos[j] != 0)
            ++j;

        // Sorting the required segment
        Arrays.sort(A, i, j + 1);
        i = j;
    }

    // Checking if the vector is sorted or not
    for(int i = 0; i < n - 1; i++)
    {
        if (A[i] > A[i + 1])
        {
            flag = 0;
            break;
        }
    }

    // Print yes if it is sorted
    if (flag == 1)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 3, 2, 1 };
    int p[] = { 1, 2 };

    check_vector(A, A.length, p);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to check if the array
# can be sorted only if the elements
# on the given positions can be swapped

# Function to check if the array can
# be sorted only if the elements on
# the given positions can be swapped
def check_vector(A, n, p):

    # Creating an array for marking
    # the positions
    pos = [0 for i in range(len(A))]

    # Iterating through the array and
    # mark the positions
    for i in range(len(p)):
        pos[p[i] - 1] = 1

    flag = 1

    # Iterating through the given array
    for i in range(n):
        if (pos[i] == 0):
            continue
        j = i

        # If pos[i] is 1, then incrementing
        # till 1 is continuously present in pos
        while (j < n and pos[j]):
            j += 1

        # Sorting the required segment
        p = A[: i]
        q = A[i : i + j + 1]
        r = A[i + j + 1 : len(A)]

        q.sort(reverse = False)
        A = p + q + r
        i = j

    # Checking if the vector is sorted or not
    for i in range(n - 1):
        if (A[i] > A[i + 1]):
            flag = 0
            break

    # Print yes if it is sorted
    if (flag == 1):
        print("Yes")
    else:
        print("No");

# Driver code
if __name__ == '__main__':

    A = [ 3, 2, 1 ]
    p = [ 1, 2 ]

    check_vector(A,len(A), p)

# This code is contributed by Samarth
```

## C#

```
// C# program to check
// if the array can be
// sorted only if the
// elements on the given
// positions can be swapped
using System;
class GFG{

// Function to check if the array can
// be sorted only if the elements on
// the given positions can be swapped
public static void check_vector(int[] A,
                                int n,
                                int[] p)
{
  // Creating an array for marking
  // the positions
  int[] pos = new int[A.Length];

  // Iterating through the array and
  // mark the positions
  for(int i = 0; i < p.Length; i++)
  {
    pos[p[i] - 1] = 1;
  }

  int flag = 1;

  // Iterating through the given array
  for(int i = 0; i < n; i++)
  {
    if (pos[i] == 0)
      continue;

    int j = i;

    // If pos[i] is 1, then
    // incrementing till 1
    // is continuously present in pos
    while (j < n && pos[j] != 0)
      ++j;

    // Sorting the required segment
    Array.Sort(A, i, j + 1);
    i = j;
  }

  // Checking if the vector
  // is sorted or not
  for(int i = 0; i < n - 1; i++)
  {
    if (A[i] > A[i + 1])
    {
      flag = 0;
      break;
    }
  }

  // Print yes if it is sorted
  if (flag == 1)
    Console.Write("Yes");
  else
    Console.Write("No");
}

// Driver code
public static void Main()
{
  int[] A = {3, 2, 1};
  int[] p = {1, 2};
  check_vector(A, A.Length, p);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript program to check if the array
// can be sorted only if the elements
// on the given positions can be swapped

// Function to check if the array can
// be sorted only if the elements on
// the given positions can be swapped
function check_vector(A, n, p)
{

    // Creating an array for marking
    // the positions
    var pos = A.length;

    // Iterating through the array and
    // mark the positions
    for (var i = 0; i < p.length; i++) {
        pos[p[i] - 1] = 1;
    }

    var flag = 1;

    // Iterating through the given array
    for (var i = 0; i < n; i++) {
        if (pos[i] == 0)
            continue;
        var j = i;

        // If pos[i] is 1, then incrementing
        // till 1 is continuously present in pos
        while (j < n && pos[j])
            ++j;

        // Sorting the required segment
         A = Array.prototype.concat(
         A.slice(0, i),
         A.slice(i+1, j+1).sort((a,b)=>a-b),
         A.slice(j+2).sort((a,b)=>a-b));

        i = j;
    }

    // Checking if the vector is sorted or not
    for (var i = 0; i < n - 1; i++) {
        if (A[i] > A[i + 1]) {
            flag = 0;
            break;
        }
    }

    // Print yes if it is sorted
    if (flag == 1)
        document.write( "Yes");
    else
        document.write( "No");
}

// Driver code
var A = [ 3, 2, 1 ];
var p = [ 1, 2 ];
check_vector(A, A.length, p);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(N * log(N))* ，其中 N 是数组的大小。