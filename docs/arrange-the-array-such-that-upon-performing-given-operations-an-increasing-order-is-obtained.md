# 排列阵列，使得在执行给定操作时获得递增的顺序

> 原文:[https://www . geesforgeks . org/array-of-the-array-so-在执行给定操作时-获得递增顺序/](https://www.geeksforgeeks.org/arrange-the-array-such-that-upon-performing-given-operations-an-increasing-order-is-obtained/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是打印数组的排列，以便在对该排列执行以下操作时，获得递增顺序作为输出:

1.  取第一个(0 <sup>第</sup>个索引)元素，从数组中移除并打印。
2.  如果数组中还有元素，将下一个顶部元素移到数组的末尾。
3.  重复上述步骤，直到数组不为空。

**示例:**

> **输入:** arr = {1，2，3，4，5，6，7，8}
> **输出:** {1，5，2，7，3，6，4，8}
> **解释:**
> 让初始数组为{1，5，2，7，3，6，4，8}，其中 1 是数组的顶部。
> 1 打印，5 移到最后。数组现在是{2，7，3，6，4，8，5}。
> 2 打印，7 移到最后。数组现在是{3，6，4，8，5，7}。
> 3 打印，6 移到最后。数组现在是{4，8，5，7，6}。
> 打印 4，移动 8 到最后。数组现在是{5，7，6，8}。
> 打印 5，移动 7 到最后。数组现在是{6，8，7}。
> 打印 6，移动 8 到最后。数组现在是{7，8}。
> 打印 7，移动 8 到最后。数组现在是{8}。
> 8 打印。
> 打印顺序为 1、2、3、4、5、6、7、8，依次递增。
> **输入:** arr = {3，2，25，2，3，1，2，6，5，45，4，89，5}
> **输出:** {1，45，2，5，2，25，2，5，3，89，3，6，4}

**方法:**
想法是模拟给定的过程。为此，使用了[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)。

1.  给定的数组被排序，队列通过添加数组索引来准备。
2.  然后遍历给定的数组，对于每个元素，弹出队列前面的索引，并将当前数组元素添加到结果数组中弹出的索引处。
3.  如果队列仍然不是空的，那么下一个索引(在队列前面)被移到队列的后面。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Function to print the arrangement
vector<int> arrangement(vector<int> arr)
{
    // Sorting the list
    sort(arr.begin(), arr.end());

    // Finding Length of the List
    int length = arr.size();

    // Initializing the result array
    vector<int> ans(length, 0);

    // Initializing the Queue
    deque<int> Q;
    for (int i = 0; i < length; i++)
        Q.push_back(i);

    // Adding current array element to the
    // result at an index which is at the
    // front of the Q and then if still
    // elements are left then putting the next
    // top element the bottom of the array.
    for (int i = 0; i < length; i++)
    {
        int j = Q.front();
        Q.pop_front();
        ans[j] = arr[i];

        if (Q.size() != 0)
        {
            j = Q.front();
            Q.pop_front();
            Q.push_back(j);
        }
    }
    return ans;
}

// Driver code
int main()
{
    vector<int> arr = { 1, 2, 3, 4, 5, 6, 7, 8 };

    vector<int> answer = arrangement(arr);

    for (int i : answer)
        cout << i << " ";
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;

public class GfG
{

    // Function to find the array
    // arrangement
    static public int[] arrayIncreasing(int[] arr)
    {

        // Sorting the array
        Arrays.sort(arr);

        // Finding size of array
        int length = arr.length;

        // Empty array to store resultant order
        int answer[] = new int[length];

        // Doubly Ended Queue to
        // simulate the process
        Deque<Integer> dq = new LinkedList<>();

        // Loop to initialize queue with indexes
        for (int i = 0; i < length; i++) {
            dq.add(i);
        }

        // Adding current array element to the
        // result at an index which is at the
        // front of the queue and then if still
        // elements are left then putting the next
        // top element the bottom of the array.
        for (int i = 0; i < length; i++)
        {

            answer[dq.pollFirst()] = arr[i];

            if (!dq.isEmpty())
                dq.addLast(dq.pollFirst());
        }

        // Returning the resultant order
        return answer;
    }

    // Driver code
    public static void main(String args[])
    {
        int A[] = { 1, 2, 3, 4, 5, 6, 7, 8 };

        // Calling the function
        int ans[] = arrayIncreasing(A);

        // Printing the obtained pattern
        for (int i = 0; i < A.length; i++)
            System.out.print(ans[i] + " ");
    }
}
```

## 计算机编程语言

```
# Python3 Code for the approach

# Importing Queue from Collections Module
from collections import deque

# Function to print the arrangement
def arrangement(arr):
    # Sorting the list
    arr.sort()

    # Finding Length of the List
    length = len(arr)

    # Initializing the result array
    answer = [0 for x in range(len(arr))]

    # Initializing the Queue
    queue = deque()
    for i in range(length):
        queue.append(i)

    # Adding current array element to the
    # result at an index which is at the
    # front of the queue and then if still
    # elements are left then putting the next
    # top element the bottom of the array.
    for i in range(length):

        answer[queue.popleft()] = arr[i]

        if len(queue) != 0:
            queue.append(queue.popleft())
    return answer

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7, 8]
answer = arrangement(arr)
# Printing the obtained result
print(*answer, sep = ' ')
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GfG
{

    // Function to find the array
    // arrangement
    static public int[] arrayIncreasing(int[] arr)
    {

        // Sorting the array
        Array.Sort(arr);

        // Finding size of array
        int length = arr.Length;

        // Empty array to store resultant order
        int []answer = new int[length];

        // Doubly Ended Queue to
        // simulate the process
        List<int> dq = new List<int>();

        // Loop to initialize queue with indexes
        for (int i = 0; i < length; i++)
        {
            dq.Add(i);
        }

        // Adding current array element to the
        // result at an index which is at the
        // front of the queue and then if still
        // elements are left then putting the next
        // top element the bottom of the array.
        for (int i = 0; i < length; i++)
        {

            answer[dq[0]] = arr[i];
            dq.RemoveAt(0);
            if (dq.Count != 0)
            {
                dq.Add(dq[0]);
                dq.RemoveAt(0);
            }
        }

        // Returning the resultant order
        return answer;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []A = { 1, 2, 3, 4, 5, 6, 7, 8 };

        // Calling the function
        int []ans = arrayIncreasing(A);

        // Printing the obtained pattern
        for (int i = 0; i < A.Length; i++)
            Console.Write(ans[i] + " ");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to find the array
    // arrangement
    function arrayIncreasing(arr)
    {

        // Sorting the array
        arr.sort(function(a, b){return a - b});

        // Finding size of array
        let length = arr.length;

        // Empty array to store resultant order
        let answer = new Array(length);

        // Doubly Ended Queue to
        // simulate the process
        let dq = [];

        // Loop to initialize queue with indexes
        for (let i = 0; i < length; i++)
        {
            dq.push(i);
        }

        // Adding current array element to the
        // result at an index which is at the
        // front of the queue and then if still
        // elements are left then putting the next
        // top element the bottom of the array.
        for (let i = 0; i < length; i++)
        {

            answer[dq[0]] = arr[i];
            dq.shift();
            if (dq.length != 0)
            {
                dq.push(dq[0]);
                dq.shift(0);
            }
        }

        // Returning the resultant order
        return answer;
    }

    let A = [ 1, 2, 3, 4, 5, 6, 7, 8 ];

    // Calling the function
    let ans = arrayIncreasing(A);

    // Printing the obtained pattern
    for (let i = 0; i < A.length; i++)
      document.write(ans[i] + " ");

      // This code is contributed by decode2207.
</script>
```

**Output**

```
1 5 2 7 3 6 4 8
```

**时间复杂度:**O(NlogN)
T3】另一种方法:

如果你仔细观察它，你会发现它遵循一个模式。

只要逆向思考。

*   对输入数组进行排序，并尝试从给定的步骤进入前一阶段。
*   从 i=N-1 迭代到 1，每一步都将 I 减 1。
*   从数组中删除最后一个元素，并将其插入到第个位置。
*   重复以上两步，直到达到 i=1
*   到达 i=1 后，您将得到最终的结果数组。

下面是上述方法的实现:

## C++

```
// C++ program to find the desired output
// after performing given operations

#include <bits/stdc++.h>
using namespace std;
// Function to arrange array in such a way
// that after performing given operation
// We get increasing sorted array

void Desired_Array(vector<int>& v)
{
    // Size of given array
    int n = v.size();

    // Sort the given array
    sort(v.begin(), v.end());

    // Start erasing last element and place it at
    // ith index
    int i = n - 1;
    // While we reach at starting

    while (i > 0) {
        // Store last element
        int p = v[n - 1];

        // Shift all elements by 1 position in right
        for (int j = n - 1; j >= i; j--)
        {
            v[j + 1] = v[j];
        }

        // insert last element at ith position
        v[i] = p;
        i--;
    }

    // print desired Array
    for (auto x : v)
        cout << x << " ";
    cout << "\n";
}

// Driver Code
int main()
{

    // Given Array
    vector<int> v = { 1, 2, 3, 4, 5 };
    Desired_Array(v);

    vector<int> v1 = { 1, 12, 2, 10, 4, 16, 6 };
    Desired_Array(v1);
    return 0;
}

// Contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// desired output after
// performing given operations
import java.util.Arrays;
class Main{

// Function to arrange array in
// such a way that after performing
// given operation We get increasing
// sorted array
public static void Desired_Array(int v[])
{
  // Size of given array
  int n = v.length;

  // Sort the given array
  Arrays.sort(v);

  // Start erasing last element
  // and place it at ith index
  int i = n - 1;

  // While we reach at starting
  while (i > 0)
  {
    // Store last element
    int p = v[n - 1];

    // Shift all elements by
    // 1 position in right
    for (int j = n - 1;
             j >= i; j--)
    {
      v[j] = v[j - 1];
    }

    // insert last element at
    // ith position
    v[i] = p;
    i--;
  }

  // Print desired Array
  for(int x = 0; x < v.length; x++)
  {
    System.out.print(v[x] + " ");
  }

  System.out.println();
}

// Driver code   
public static void main(String[] args)
{
  // Given Array
  int v[] = {1, 2, 3, 4, 5};
  Desired_Array(v);

  int v1[] = {1, 12, 2, 10, 4, 16, 6};
  Desired_Array(v1);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the desired output
# after performing given operations

# Function to arrange array in such a way
# that after performing given operation
# We get increasing sorted array
def Desired_Array(v):

    # Size of given array
    n = len(v)

    # Sort the given array
    v.sort()

    # Start erasing last element and place it at
    # ith index
    i = n - 1
    # While we reach at starting

    while (i > 0) :
        # Store last element
        p = v[n - 1]

        # Shift all elements by 1 position in right
        for j in range(n-1, i - 1, -1) :

            v[j] = v[j - 1]

        # insert last element at ith position
        v[i] = p
        i -= 1

    # print desired Array
    for x in v :
        print(x, end = " ")
    print()

# Given Array
v = [ 1, 2, 3, 4, 5 ]
Desired_Array(v)

v1 = [ 1, 12, 2, 10, 4, 16, 6 ]
Desired_Array(v1)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the desired
// output after performing given
// operations
using System;

class GFG{

// Function to arrange array in
// such a way that after performing
// given operation We get increasing
// sorted array
public static void Desired_Array(int[] v)
{

    // Size of given array
    int n = v.Length;

    // Sort the given array
    Array.Sort(v);

    // Start erasing last element
    // and place it at ith index
    int i = n - 1;

    // While we reach at starting
    while (i > 0)
    {

        // Store last element
        int p = v[n - 1];

        // Shift all elements by
        // 1 position in right
        for(int j = n - 1;
                j >= i; j--)
        {
            v[j] = v[j - 1];
        }

        // Insert last element at
        // ith position
        v[i] = p;
        i--;
    }

    // Print desired Array
    for(int x = 0; x < v.Length; x++)
    {
        Console.Write(v[x] + " ");
    }

    Console.WriteLine();
}

// Driver code       
static public void Main()
{

    // Given Array
    int[] v = { 1, 2, 3, 4, 5 };
    Desired_Array(v);

    int[] v1 = { 1, 12, 2, 10, 4, 16, 6 };
    Desired_Array(v1);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

    // Javascript program to find the desired
    // output after performing given
    // operations

    // Function to arrange array in
    // such a way that after performing
    // given operation We get increasing
    // sorted array
    function Desired_Array(v)
    {

        // Size of given array
        let n = v.length;

        // Sort the given array
        v.sort(function(a, b){return a - b});

        // Start erasing last element
        // and place it at ith index
        let i = n - 1;

        // While we reach at starting
        while (i > 0)
        {

            // Store last element
            let p = v[n - 1];

            // Shift all elements by
            // 1 position in right
            for(let j = n - 1; j >= i; j--)
            {
                v[j] = v[j - 1];
            }

            // Insert last element at
            // ith position
            v[i] = p;
            i--;
        }

        // Print desired Array
        for(let x = 0; x < v.length; x++)
        {
            document.write(v[x] + " ");
        }

        document.write("</br>");
    }

    // Given Array
    let v = [ 1, 2, 3, 4, 5 ];
    Desired_Array(v);

    let v1 = [ 1, 12, 2, 10, 4, 16, 6 ];
    Desired_Array(v1);

</script>
```

**Output**

```
1 5 2 4 3 
1 12 2 10 4 16 6
```