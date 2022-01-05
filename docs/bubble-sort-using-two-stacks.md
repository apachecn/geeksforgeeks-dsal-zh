# 使用两个堆栈进行气泡排序

> 原文:[https://www.geeksforgeeks.org/bubble-sort-using-two-stacks/](https://www.geeksforgeeks.org/bubble-sort-using-two-stacks/)

先决条件:[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)
编写一个函数，使用堆栈对整数数组进行排序，并使用冒泡排序范例。

**算法:**

```
1\. Push all elements of array in 1st stack

2\. Run a loop for 'n' times(n is size of array)
   having the following :
   2.a. Keep on pushing elements in the 2nd 
        stack till the top of second stack is 
        smaller than element being pushed from 
        1st stack.
   2.b. If the element being pushed is smaller 
        than top of 2nd stack  then swap them
        (as in bubble sort)
   *Do above steps alternatively

TRICKY STEP: Once a stack is empty, then the 
top of the next stack will be the largest 
number so keep it at its position in array 
i.e arr[len-1-i] and then pop it from that 
stack.
```

## C++

```
// C++ program for bubble sort
// using stack
#include <bits/stdc++.h>
using namespace std;

// Function for bubble sort using Stack
void bubbleSortStack(int a[], int n)
{
    stack<int> s1;

    // Push all elements of array in 1st stack
    for(int i = 0; i < n; i++)
    {
        s1.push(a[i]);
    }

    stack<int> s2;

    for(int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
        {
            while (!s1.empty())
            {
                int t = s1.top();
                s1.pop();

                if (s2.empty())
                {
                    s2.push(t);
                }

                else
                {
                    // Swapping
                    if (s2.top() > t)
                    {
                        int temp = s2.top();
                        s2.pop();
                        s2.push(t);
                        s2.push(temp);
                    }
                    else
                    {
                        s2.push(t);
                    }
                }
            }

            // Tricky step
            a[n - 1 - i] = s2.top();
            s2.pop();
        }

        else
        {
            while (!s2.empty())
            {
                int t = s2.top();
                s2.pop();

                if (s1.empty())
                {
                    s1.push(t);
                }

                else
                {
                    if (s1.top() > t)
                    {
                        int temp = s1.top();
                        s1.pop();

                        s1.push(t);
                        s1.push(temp);
                    }

                    else
                    {
                        s1.push(t);
                    }
                }
            }

            // Tricky step
            a[n - 1 - i] = s1.top();
            s1.pop();
        }
    }

    cout << "[";
    for(int i = 0; i < n; i++)
    {
        cout << a[i] << ", ";
    }
    cout << "]";
}

// Driver code
int main()
{
    int a[] = { 15, 12, 44, 2, 5, 10 };
    int n = sizeof(a) / sizeof(a[0]);

    bubbleSortStack(a, n);

    return 0;
}

// This code is contributed by pawki
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for bubble sort
// using stack

import java.util.Arrays;
import java.util.Stack;

public class Test
{
    // Method for bubble sort using Stack
    static void bubbleSortStack(int arr[], int n)
    {
        Stack<Integer> s1 = new Stack<>();

        // Push all elements of array in 1st stack
        for (int num : arr)
            s1.push(num);    

        Stack<Integer> s2 = new Stack<>();

        for (int i = 0; i < n; i++)
        {
            // alternatively
            if (i % 2 == 0)
            {
                while (!s1.isEmpty())
                {
                    int t = s1.pop();

                    if (s2.isEmpty())
                        s2.push(t);                    
                    else
                    {
                        if (s2.peek() > t)
                        {
                            // swapping
                            int temp = s2.pop();
                            s2.push(t);
                            s2.push(temp);
                        }
                        else
                        {
                            s2.push(t);
                        }
                    }
                }

                // tricky step
                arr[n-1-i] = s2.pop();
            }            
            else
            {
                while(!s2.isEmpty())
                {
                    int t = s2.pop();

                    if (s1.isEmpty())
                        s1.push(t);

                    else
                    {
                        if (s1.peek() > t)
                        {
                            // swapping
                            int temp = s1.pop();

                            s1.push(t);
                            s1.push(temp);
                        }
                        else
                            s1.push(t);
                    }
                }

                // tricky step
                arr[n-1-i] = s1.pop();
            }
        }        
        System.out.println(Arrays.toString(arr));
    }

    // Driver Method
    public static void main(String[] args)
    {
        int arr[] = {15, 12, 44, 2, 5, 10};    
        bubbleSortStack(arr, arr.length);
    }
}
```

## 蟒蛇 3

```
# Python3 program for bubble sort
# using stack

# Function for bubble sort using Stack
def bubbleSortStack(a, n):
    s1 = []

    # Push all elements of array in 1st stack
    for i in range(n):
        s1.append(a[i]);
    s2 = []
    for i in range(n):
        if (i % 2 == 0):
            while (len(s1) != 0):
                t = s1[-1]
                s1.pop();
                if(len(s2) == 0):
                    s2.append(t);                  
                else:

                    # Swapping
                    if (s2[-1] > t):
                        temp = s2[-1]
                        s2.pop();
                        s2.append(t);
                        s2.append(temp);

                    else:
                        s2.append(t);

            # Tricky step
            a[n - 1 - i] = s2[-1]
            s2.pop();          
        else:

            while(len(s2) != 0):
                t = s2[-1]
                s2.pop();

                if(len(s1) == 0):
                    s1.append(t);
                else:
                    if (s1[-1] > t):
                        temp = s1[-1]
                        s1.pop();

                        s1.append(t);
                        s1.append(temp);
                    else:
                        s1.append(t);

            # Tricky step
            a[n - 1 - i] = s1[-1]
            s1.pop();
    print("[", end = '')
    for i in range(n):
        print(a[i], end = ', ')
    print(']', end = '')

# Driver code
if __name__=='__main__':

    a = [ 15, 12, 44, 2, 5, 10 ]
    n = len(a)

    bubbleSortStack(a, n);

    # This code is contributed by rutvik_56.
```

## C#

```
// C# program for bubble sort
// using stack
using System;
using System.Collections.Generic;

class GFG
{

// Method for bubble sort using Stack
static void bubbleSortStack(int []arr, int n)
{
    Stack<int> s1 = new Stack<int>();

    // Push all elements of array in 1st stack
    foreach (int num in arr)
        s1.Push(num);    

    Stack<int> s2 = new Stack<int>();

    for (int i = 0; i < n; i++)
    {
        // alternatively
        if (i % 2 == 0)
        {
            while (s1.Count != 0)
            {
                int t = s1.Pop();

                if (s2.Count == 0)
                    s2.Push(t);                
                else
                {
                    if (s2.Peek() > t)
                    {
                        // swapping
                        int temp = s2.Pop();
                        s2.Push(t);
                        s2.Push(temp);
                    }
                    else
                    {
                        s2.Push(t);
                    }
                }
            }

            // tricky step
            arr[n - 1 - i] = s2.Pop();
        }        
        else
        {
            while(s2.Count != 0)
            {
                int t = s2.Pop();

                if (s1.Count == 0)
                    s1.Push(t);

                else
                {
                    if (s1.Peek() > t)
                    {
                        // swapping
                        int temp = s1.Pop();

                        s1.Push(t);
                        s1.Push(temp);
                    }
                    else
                        s1.Push(t);
                }
            }

            // tricky step
            arr[n - 1 - i] = s1.Pop();
        }
    }    
    Console.WriteLine("[" + String.Join(", ", arr) + "]");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {15, 12, 44, 2, 5, 10};    
    bubbleSortStack(arr, arr.Length);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for bubble sort
// using stack

// Method for bubble sort using Stack
function bubbleSortStack(arr, n)
{
    let s1 = [];

    // Push all elements of array in 1st stack
    for(let num = 0; num < arr.length; num++)
        s1.push(arr[num]);   

    let s2 = [];

    for(let i = 0; i < n; i++)
    {

        // Alternatively
        if (i % 2 == 0)
        {
            while (s1.length != 0)
            {
                let t = s1.pop();

                if (s2.length == 0)
                    s2.push(t);                   
                else
                {
                    if (s2[s2.length - 1] > t)
                    {

                        // Swapping
                        let temp = s2.pop();
                        s2.push(t);
                        s2.push(temp);
                    }
                    else
                    {
                        s2.push(t);
                    }
                }
            }

            // Tricky step
            arr[n - 1 - i] = s2.pop();
        }           
        else
        {
            while(s2.length != 0)
            {
                let t = s2.pop();

                if (s1.length == 0)
                    s1.push(t);

                else
                {
                    if (s1[s1.length - 1] > t)
                    {

                        // Swapping
                        let temp = s1.pop();

                        s1.push(t);
                        s1.push(temp);
                    }
                    else
                        s1.push(t);
                }
            }

            // Tricky step
            arr[n - 1 - i] = s1.pop();
        }
    }       
    document.write((arr).join(" "));
}

// Driver code
let arr = [ 15, 12, 44, 2, 5, 10 ];
bubbleSortStack(arr, arr.length);

// This code is contributed by rag2127

</script>
```

**输出:**

```
[2, 5, 10, 12, 15, 44]
```

本文由**高拉夫·米格拉尼**和**阿比舍克·索马尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。