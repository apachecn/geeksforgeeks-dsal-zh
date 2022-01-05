# 大小为 k 的每个窗口中的第一个负整数

> 原文:[https://www . geesforgeks . org/first-negative-integer-ever-window-size-k/](https://www.geeksforgeeks.org/first-negative-integer-every-window-size-k/)

给定一个数组和一个正整数 k，找到大小为 k 的每个窗口(连续子数组)的第一个负整数。如果一个窗口不包含负整数，则为该窗口打印 0。

**示例:**

```
Input : arr[] = {-8, 2, 3, -6, 10}, k = 2
Output : -8 0 -6 -6
First negative integer for each window of size k
{-8, 2} = -8
{2, 3} = 0 (does not contain a negative integer)
{3, -6} = -6
{-6, 10} = -6

Input : arr[] = {12, -1, -7, 8, -15, 30, 16, 28} , k = 3
Output : -1 -1 -7 -15 -15 0
```

**天真方法:**运行两个循环。外环取 k 大小的所有子阵(窗)，内环取当前子阵(窗)的第一个负整数。

## C++

```
// C++ implementation to find the first negative
// integer in every window of size k
#include <bits/stdc++.h>
using namespace std;

// function to find the first negative
// integer in every window of size k
void printFirstNegativeInteger(int arr[], int n, int k)
{
    // flag to check whether window contains
    // a negative integer or not
    bool flag;

    // Loop for each subarray(window) of size k
    for (int i = 0; i<(n-k+1); i++)          
    {
        flag = false;

        // traverse through the current window
        for (int j = 0; j<k; j++)
        {
            // if a negative integer is found, then
            // it is the first negative integer for
            // current window. Print it, set the flag
            // and break
            if (arr[i+j] < 0)
            {
                cout << arr[i+j] << " ";
                flag = true;
                break;
            }
        }

        // if the current window does not
        // contain a negative integer
        if (!flag)
            cout << "0" << " ";
    }   
}

// Driver program to test above functions
int main()
{
    int arr[] = {12, -1, -7, 8, -15, 30, 16, 28};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 3;
    printFirstNegativeInteger(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the first negative
// integer in every window of size k
import java.util.*;

class solution
{

// function to find the first negative
// integer in every window of size k
static void printFirstNegativeInteger(int arr[], int n, int k)
{
    // flag to check whether window contains
    // a negative integer or not
    boolean flag;

    // Loop for each subarray(window) of size k
    for (int i = 0; i<(n-k+1); i++)        
    {
        flag = false;

        // traverse through the current window
        for (int j = 0; j<k; j++)
        {
            // if a negative integer is found, then
            // it is the first negative integer for
            // current window. Print it, set the flag
            // and break
            if (arr[i+j] < 0)
            {
                System.out.print((arr[i+j])+" ");
                flag = true;
                break;
            }
        }

        // if the current window does not
        // contain a negative integer
        if (!flag)
            System.out.print("0"+" ");
    }
}

// Driver program to test above functions
public static void main(String args[])
{
    int arr[] = {12, -1, -7, 8, -15, 30, 16, 28};
    int n = arr.length;
    int k = 3;
    printFirstNegativeInteger(arr, n, k);

}
}
// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 implementation to find the first negative
# integer in every window of size k

# Function to find the first negative
# integer in every window of size k
def printFirstNegativeInteger(arr, n, k):

    # Loop for each subarray(window) of size k
    for i in range(0, (n - k + 1)):
        flag = False

        # Traverse through the current window
        for j in range(0, k):

            # If a negative integer is found, then
            # it is the first negative integer for
            # current window. Print it, set the flag
            # and break
            if (arr[i + j] < 0):

                print(arr[i + j], end = " ")
                flag = True
                break

        # If the current window does not
        # contain a negative integer
        if (not(flag)):
            print("0", end = " ")

# Driver Code
arr = [12, -1, -7, 8, -15, 30, 16, 28]
n = len(arr)
k = 3
printFirstNegativeInteger(arr, n, k)

# This code is contributed by 'Smitha dinesh semwal'
```

## C#

```
// C# implementation to find
// the first negative integer
// in every window of size k
using System;

class GFG
{

// function to find the first negative
// integer in every window of size k
static void printFirstNegativeInteger(int []arr,
                                    int n, int k)
{
    // flag to check whether window contains
    // a negative integer or not
    bool flag;

    // Loop for each subarray(window) of size k
    for (int i = 0; i < (n - k + 1); i++)
    {
        flag = false;

        // traverse through the current window
        for (int j = 0; j < k; j++)
        {
            // if a negative integer is found, then
            // it is the first negative integer for
            // current window. Print it, set the flag
            // and break
            if (arr[i + j] < 0)
            {
                Console.Write((arr[i + j]) + " ");
                flag = true;
                break;
            }
        }

        // if the current window does not
        // contain a negative integer
        if (!flag)
            Console.Write("0" + " ");
    }
}

// Driver code
public static void Main(String []args)
{
    int []arr = {12, -1, -7, 8, -15, 30, 16, 28};
    int n = arr.Length;
    int k = 3;
    printFirstNegativeInteger(arr, n, k);
}
}

// This code has been contributed
// by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation to find
// the first negative integer
// in every window of size k
function printFirstNegativeInteger(arr, n, k)
{
    // flag to check whether window contains
    // a negative integer or not
    let flag;

    // Loop for each subarray(window) of size k
    for (let i = 0; i<(n-k+1); i++)        
    {
        flag = false;

        // traverse through the current window
        for (let j = 0; j<k; j++)
        {
            // if a negative integer is found, then
            // it is the first negative integer for
            // current window. Print it, set the flag
            // and break
            if (arr[i+j] < 0)
            {
                document.write((arr[i+j])+" ");
                flag = true;
                break;
            }
        }

        // if the current window does not
        // contain a negative integer
        if (!flag)
            document.write("0"+" ");
    }
}

    // Driver Code

    let arr = [12, -1, -7, 8, -15, 30, 16, 28];
    let n = arr.length;
    let k = 3;
    printFirstNegativeInteger(arr, n, k);

// This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
-1 -1 -7 -15 -15 0
```

**时间复杂度:**对于外环的每次迭代，外环运行 n-k+1 次，内环运行 k 次。所以时间复杂度是 O((n-k+1)*k)，当 k 比 n 小很多的时候也可以写成 O(nk)，否则当 k 趋于达到 n 的时候，复杂度就变成 O(k)。

**有效途径:**是[滑动窗口最大值](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)问题的变种。
我们创建一个出列，容量为 k 的 Di，它只存储 k 个元素的当前窗口的有用元素。如果元素位于当前窗口中并且是负整数，则该元素非常有用。我们逐个处理所有数组元素，并维护 Di 以包含当前窗口的有用元素，这些有用元素都是负整数。对于特定窗口，如果 Di 不为空，那么 Di 前面的元素是该窗口的第一个负整数，否则该窗口不包含负整数。

## C++

```
// C++ implementation to find the first negative
// integer in every window of size k
#include <bits/stdc++.h>

using namespace std;

// function to find the first negative
// integer in every window of size k
void printFirstNegativeInteger(int arr[], int n, int k)
{
    // A Double Ended Queue, Di that will store indexes of
    // useful array elements for the current window of size k.
    // The useful elements are all negative integers.
    deque<int>  Di;

    /* Process first k (or first window) elements of array */
    int i;
    for (i = 0; i < k; i++)
        // Add current element at the rear of Di
        // if it is a negative integer
        if (arr[i] < 0)
            Di.push_back(i);

    // Process rest of the elements, i.e., from arr[k] to arr[n-1]
    for ( ; i < n; i++)
    {
        // if Di is not empty then the element at the
        // front of the queue is the first negative integer
        // of the previous window
        if (!Di.empty())
            cout << arr[Di.front()] << " ";

        // else the window does not have a
        // negative integer
        else
            cout << "0" << " ";

        // Remove the elements which are out of this window
        while ( (!Di.empty()) && Di.front() < (i - k + 1))
            Di.pop_front();  // Remove from front of queue

        // Add current element at the rear of Di
        // if it is a negative integer
        if (arr[i] < 0)
            Di.push_back(i);
    }

    // Print the first negative
    // integer of last window
    if (!Di.empty())
           cout << arr[Di.front()] << " ";
    else
        cout << "0" << " ";      

}

// Driver program to test above functions
int main()
{
    int arr[] = {12, -1, -7, 8, -15, 30, 16, 28};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 3;
    printFirstNegativeInteger(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// first negative integer in
// every window of size k
import java.util.*;
class GFG
{

// function to find the first negative
// integer in every window of size k
static void printFirstNegativeInteger(int arr[],
                                      int n, int k)
{
    // A Double Ended Queue, Di that will
    // store indexes of useful array elements
    // for the current window of size k.
    // The useful elements are all negative integers.
    LinkedList<Integer> Di = new LinkedList<>();

    // Process first k (or first window)
    // elements of array
    int i;
    for (i = 0; i < k; i++)

        // Add current element at the rear of Di
        // if it is a negative integer
        if (arr[i] < 0)
            Di.add(i);

    // Process rest of the elements,
    // i.e., from arr[k] to arr[n-1]
    for ( ; i < n; i++)
    {
        // if Di is not empty then the element
        // at the front of the queue is the first
        // negative integer of the previous window
        if (!Di.isEmpty())
            System.out.print(arr[Di.peek()] + " ");

        // else the window does not have a
        // negative integer
        else
            System.out.print("0" + " ");

        // Remove the elements which are
        // out of this window
        while ((!Di.isEmpty()) &&
                 Di.peek() < (i - k + 1))
            Di.remove(); // Remove from front of queue

        // Add current element at the rear of Di
        // if it is a negative integer
        if (arr[i] < 0)
            Di.add(i);
    }

    // Print the first negative
    // integer of last window
    if (!Di.isEmpty())
        System.out.print(arr[Di.peek()] + " ");
    else
        System.out.print("0" + " ");    
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {12, -1, -7, 8, -15, 30, 16, 28};
    int n = arr.length;
    int k = 3;
    printFirstNegativeInteger(arr, n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find the
# first negative integer in every window
# of size k import deque() from collections
from collections import deque

# function to find the first negative
# integer in every window of size k
def printFirstNegativeInteger(arr, n, k):

    # A Double Ended Queue, Di that will store
    # indexes of useful array elements for the
    # current window of size k. The useful
    # elements are all negative integers.
    Di = deque()

    # Process first k (or first window)
    # elements of array
    for i in range(k):

        # Add current element at the rear of Di
        # if it is a negative integer
        if (arr[i] < 0):
            Di.append(i);

    # Process rest of the elements, i.e.,
    # from arr[k] to arr[n-1]
    for i in range(k, n):

        # if the window does not have
        # a negative integer
        if (not Di):
            print(0, end = ' ')

        # if Di is not empty then the element
        # at the front of the queue is the first
        # negative integer of the previous window
        else:
            print(arr[Di[0]], end = ' ');

        # Remove the elements which are
        # out of this window
        while Di and Di[0] <= (i - k):
            Di.popleft() # Remove from front of queue

        # Add current element at the rear of Di
        # if it is a negative integer
        if (arr[i] < 0):
            Di.append(i);

    # Print the first negative
    # integer of last window
    if not Di:
        print(0)
    else:
        print(arr[Di[0]], end = " ")

# Driver Code
if __name__ =="__main__":
    arr = [12, -1, -7, 8, -15, 30, 16, 28]
    n = len(arr)
    k = 3
    printFirstNegativeInteger(arr, n, k);

# This code is contributed by
# chaudhary_19 (Mayank Chaudhary)
```

## C#

```
// C# implementation to find the
// first negative integer in
// every window of size k
using System;
using System.Collections.Generic;

class GFG
{

// function to find the first negative
// integer in every window of size k
static void printFirstNegativeint(int []arr,
                                  int n, int k)
{
    // A Double Ended Queue, Di that will
    // store indexes of useful array elements
    // for the current window of size k.
    // The useful elements are all
    // negative integers.
    List<int> Di = new List<int>();

    // Process first k (or first window)
    // elements of array
    int i;
    for (i = 0; i < k; i++)

        // Add current element at the rear of Di
        // if it is a negative integer
        if (arr[i] < 0)
            Di.Add(i);

    // Process rest of the elements,
    // i.e., from arr[k] to arr[n-1]
    for ( ; i < n; i++)
    {
        // if Di is not empty then the element
        // at the front of the queue is the first
        // negative integer of the previous window
        if (Di.Count != 0)
            Console.Write(arr[Di[0]] + " ");

        // else the window does not have a
        // negative integer
        else
            Console.Write("0" + " ");

        // Remove the elements which are
        // out of this window
        while ((Di.Count != 0) &&
                Di[0] < (i - k + 1))

            // Remove from front of queue
            Di.RemoveAt(0);

        // Add current element at the rear of Di
        // if it is a negative integer
        if (arr[i] < 0)
            Di.Add(i);
    }

    // Print the first negative
    // integer of last window
    if (Di.Count!=0)
        Console.Write(arr[Di[0]] + " ");
    else
        Console.Write("0" + " ");    
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {12, -1, -7, 8, -15, 30, 16, 28};
    int n = arr.Length;
    int k = 3;
    printFirstNegativeint(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

**输出:**

```
-1 -1 -7 -15 -15 0
```

**时间复杂度:**O(n)
T3】辅助空间: O(k)

**优化方式:**:也可以用不变的空间来完成。想法是有一个变量 firstNegativeIndex 来跟踪 k 大小窗口中的第一个负元素。在每次迭代中，我们都会跳过不再属于当前 k 大小窗口的元素(first negative index<= I–k)以及正元素。

以下是基于这种方法的解决方案。

## C++

```
// C++ code for First negative integer
// in every window of size k
#include <iostream>
using namespace std;

void printFirstNegativeInteger(int arr[], int k, int n)
{
    int firstNegativeIndex = 0;
    int firstNegativeElement;

    for(int i = k - 1; i < n; i++)
    {

        // skip out of window and positive elements
        while((firstNegativeIndex < i ) &&
              (firstNegativeIndex <= i - k ||
               arr[firstNegativeIndex] > 0))
        {
            firstNegativeIndex ++;
        }

        // check if a negative element is found, otherwise use 0
        if(arr[firstNegativeIndex] < 0)
        {
            firstNegativeElement = arr[firstNegativeIndex];
        }
        else
        {
            firstNegativeElement = 0;
        }
        cout<<firstNegativeElement << " ";
    }

}

// Driver code
int main()
{
     int arr[] = { 12, -1, -7, 8, -15, 30, 16, 28};
      int n = sizeof(arr)/sizeof(arr[0]);
     int k = 3;
     printFirstNegativeInteger(arr, k, n);   
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for First negative integer
// in every window of size k
import java.util.*;

class GFG{

static void printFirstNegativeInteger(int arr[],
                                      int k, int n)
{
    int firstNegativeIndex = 0;
    int firstNegativeElement;

    for(int i = k - 1; i < n; i++)
    {

        // Skip out of window and positive elements
        while ((firstNegativeIndex < i ) &&
               (firstNegativeIndex <= i - k ||
            arr[firstNegativeIndex] > 0))
        {
            firstNegativeIndex ++;
        }

        // Check if a negative element is
        // found, otherwise use 0
        if (arr[firstNegativeIndex] < 0)
        {
            firstNegativeElement = arr[firstNegativeIndex];
        }
        else
        {
            firstNegativeElement = 0;
        }
        System.out.print(firstNegativeElement + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 12, -1, -7, 8, -15, 30, 16, 28 };
    int n = arr.length;
    int k = 3;

    printFirstNegativeInteger(arr, k, n);   
}
}

// This code is contributed by amreshkumar3
```

## 蟒蛇 3

```
# Python3 code for First negative integer
# in every window of size k
def printFirstNegativeInteger(arr, k):
    firstNegativeIndex = 0

    for i in range(k - 1, len(arr)):

        # skip out of window and positive elements
        while firstNegativeIndex < i and (firstNegativeIndex <= i - k or arr[firstNegativeIndex] > 0):
            firstNegativeIndex += 1

        # check if a negative element is found, otherwise use 0
        firstNegativeElement = arr[firstNegativeIndex] if arr[firstNegativeIndex] < 0 else 0
        print(firstNegativeElement, end=' ')

if __name__ == "__main__":
    arr = [12, -1, -7, 8, -15, 30, 16, 28]
    k = 3
    printFirstNegativeInteger(arr, k)

# contributed by Arjun Lather
```

## C#

```
// C# code for First negative integer
// in every window of size k
using System;

class GFG{

static void printFirstNegativeInteger(int[] arr,
                                      int k, int n)
{
    int firstNegativeIndex = 0;
    int firstNegativeElement;

    for(int i = k - 1; i < n; i++)
    {

        // Skip out of window and positive elements
        while ((firstNegativeIndex < i ) &&
               (firstNegativeIndex <= i - k ||
            arr[firstNegativeIndex] > 0))
        {
            firstNegativeIndex ++;
        }

        // Check if a negative element is
        // found, otherwise use 0
        if (arr[firstNegativeIndex] < 0)
        {
            firstNegativeElement = arr[firstNegativeIndex];
        }
        else
        {
            firstNegativeElement = 0;
        }
        Console.Write(firstNegativeElement + " ");
    }   
}

// Driver code
static public void Main()
{
    int[] arr = { 12, -1, -7, 8, -15, 30, 16, 28 };
    int n = arr.Length;
    int k = 3;

    printFirstNegativeInteger(arr, k, n);
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        function printFirstNegativeInteger(arr, k, n) {
            let firstNegativeIndex = 0;
            let firstNegativeElement;

            for (let i = k - 1; i < n; i++) {

                // skip out of window and positive elements
                while ((firstNegativeIndex < i) &&
                    (firstNegativeIndex <= i - k ||
                        arr[firstNegativeIndex] > 0)) {
                    firstNegativeIndex++;
                }

                // check if a negative element is found, otherwise use 0
                if (arr[firstNegativeIndex] < 0) {
                    firstNegativeElement = arr[firstNegativeIndex];
                }
                else {
                    firstNegativeElement = 0;
                }
                document.write(firstNegativeElement + " ");
            }

        }

        // Driver code

        let arr = [12, -1, -7, 8, -15, 30, 16, 28];
        let n = arr.length;
        let k = 3;
        printFirstNegativeInteger(arr, k, n);

    // This code is contributed by Potta Lokesh
    </script>
```

**输出:**

```
-1 -1 -7 -15 -15 0
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客网的主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。