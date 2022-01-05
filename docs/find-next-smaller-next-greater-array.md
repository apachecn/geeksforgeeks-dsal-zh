# 在数组中寻找下一个更大的更小的

> 原文:[https://www . geesforgeks . org/find-next-small-next-great-array/](https://www.geeksforgeeks.org/find-next-smaller-next-greater-array/)

给定整数数组，求数组中每个元素的下一个较小的[下一个较大的元素](https://www.geeksforgeeks.org/next-greater-element/)。
**注**:不存在大元或大元中不存在小元的元素，打印-1。
示例:

```
Input : arr[] = {5, 1, 9, 2, 5, 1, 7}
Output:          2  2 -1  1 -1 -1 -1
Explanation :  
Next Greater ->      Right Smaller 
   5 ->  9             9 ->  2 
   1 ->  9             9 ->  2
   9 -> -1            -1 -> -1
   2 ->  5             5 ->  1
   5 ->  7             7 -> -1
   1 ->  7             7 -> -1
   7 -> -1            -1 -> -1 

Input  : arr[] = {4, 8, 2, 1, 9, 5, 6, 3}
Output :          2  5  5  5 -1  3 -1 -1 
```

一个**简单的解决方案**就是遍历所有元素。对于每个元素，找到当前元素的下一个较大的元素，然后为当前的下一个较大的元素找到正确的较小的元素。此解决方案花费的时间为 0(n<sup>2</sup>)。
高效解决方案**耗时 0(n)。注意，它是数组中[下一个较大元素](https://www.geeksforgeeks.org/next-greater-element/) & [下一个较小元素](https://www.geeksforgeeks.org/find-maximum-difference-between-nearest-left-and-right-smaller-elements/)的组合。** 

```
Let input array be 'arr[]' and size of array be 'n'
find next greatest element of every element 

 step 1 : Create an empty stack (S) in which we store the indexes
          and NG[] that is user to store the indexes of NGE
          of every element.

 step 2 : Traverse the array in reverse order 
            where i goes from (n-1 to 0)

        a) While S is nonempty and the top element of 
           S is smaller than or equal to 'arr[i]':
              pop S

        b) If S is empty 
             arr[i] has no greater element
             NG[i] = -1

        c) else we have next greater element
             NG[i] = S.top() // here we store the index of NGE

        d). push current element index in stack 
           S.push(i)

Find Right smaller element of every element      

  step 3 : create an array RS[] used to store the index of
           right smallest element 

  step 4 : we repeat step (1 & 2)  with little bit of
           modification in step 1 & 2 .
           they are :

          a). we use RS[] in place of NG[].

          b). In step (2.a)
              we pop element form stack S  while S is not
              empty or the top element of S is greater then 
              or equal to 'arr[i]'  

  step 5 . compute all RSE of NGE :

           where i goes from 0 to n-1 
           if NG[ i ] != -1 && RS[ NG [ i]] ! =-1
              print arr[RS[NG[i]]]
          else
              print -1

```

以下是以上想法的实现

## C++

```
// C++ Program to find Right smaller element of next
// greater element
#include<bits/stdc++.h>
using namespace std;

// function find Next greater element
void nextGreater(int arr[], int n, int next[], char order)
{
    // create empty stack
    stack<int> S;

    // Traverse all array elements in reverse order
    // order == 'G' we compute next greater elements of
    //              every element
    // order == 'S' we compute right smaller element of
    //              every element
    for (int i=n-1; i>=0; i--)
    {
        // Keep removing top element from S while the top
        // element is smaller then or equal to arr[i] (if Key is G)
        // element is greater then or equal to arr[i] (if order is S)
        while (!S.empty() &&
              ((order=='G')? arr[S.top()] <= arr[i]:
                           arr[S.top()] >= arr[i]))
            S.pop();

        // store the next greater element of current element
        if (!S.empty())
            next[i] = S.top();

        // If all elements in S were smaller than arr[i]
        else
            next[i] = -1;

        // Push this element
        S.push(i);
    }
}

// Function to find Right smaller element of next greater
// element
void nextSmallerOfNextGreater(int arr[], int n)
{
    int NG[n]; // stores indexes of next greater elements
    int RS[n]; // stores indexes of right smaller elements

    // Find next greater element
    // Here G indicate next greater element
    nextGreater(arr, n, NG, 'G');

    // Find right smaller element
    // using same function nextGreater()
    // Here S indicate right smaller elements
    nextGreater(arr, n, RS, 'S');

    // If NG[i] == -1 then there is no smaller element
    // on right side. We can find Right smaller of next
    // greater by arr[RS[NG[i]]]
    for (int i=0; i< n; i++)
    {
        if (NG[i] != -1 && RS[NG[i]] != -1)
            cout << arr[RS[NG[i]]] << " ";
        else
            cout<<"-1"<<" ";
    }
}

// Driver program
int main()
{
    int arr[] = {5, 1, 9, 2, 5, 1, 7};
    int n = sizeof(arr)/sizeof(arr[0]);
    nextSmallerOfNextGreater(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Right smaller element of next
// greater element
import java.util.Stack;
public class Main {
    // function find Next greater element
    public static void nextGreater(int arr[], int next[], char order)
    {
        // create empty stack
        Stack<Integer> stack=new Stack<>();

        // Traverse all array elements in reverse order
        // order == 'G' we compute next greater elements of
        //              every element
        // order == 'S' we compute right smaller element of
        //              every element
        for (int i=arr.length-1; i>=0; i--)
        {
            // Keep removing top element from S while the top
            // element is smaller then or equal to arr[i] (if Key is G)
            // element is greater then or equal to arr[i] (if order is S)
            while (!stack.isEmpty() && ((order=='G')? arr[stack.peek()] <= arr[i]:arr[stack.peek()] >= arr[i]))
                stack.pop();

            // store the next greater element of current element
            if (!stack.isEmpty())
                next[i] = stack.peek();

            // If all elements in S were smaller than arr[i]
            else
                next[i] = -1;

            // Push this element
            stack.push(i);
        }
    }

    // Function to find Right smaller element of next greater
    // element
    public static void nextSmallerOfNextGreater(int arr[])
    {
        int NG[]=new int[arr.length]; // stores indexes of next greater elements
        int RS[]=new int[arr.length]; // stores indexes of right smaller elements

        // Find next greater element
        // Here G indicate next greater element
        nextGreater(arr, NG, 'G');

        // Find right smaller element
        // using same function nextGreater()
        // Here S indicate right smaller elements
        nextGreater(arr, RS, 'S');

        // If NG[i] == -1 then there is no smaller element
        // on right side. We can find Right smaller of next
        // greater by arr[RS[NG[i]]]
        for (int i=0; i< arr.length; i++)
        {
            if (NG[i] != -1 && RS[NG[i]] != -1)
                System.out.print(arr[RS[NG[i]]]+" ");
            else
                System.out.print("-1 ");
        }
    } 

    public static void main(String args[]) {
        int arr[] = {5, 1, 9, 2, 5, 1, 7}; 
        nextSmallerOfNextGreater(arr);
    }
}
//This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
# Python 3 Program to find Right smaller element of next
# greater element

# function find Next greater element
def nextGreater(arr, n, next, order):

    S = []

    # Traverse all array elements in reverse order
    # order == 'G' we compute next greater elements of
    #              every element
    # order == 'S' we compute right smaller element of
    #              every element
    for i in range(n-1,-1,-1):

        # Keep removing top element from S while the top
        # element is smaller then or equal to arr[i] (if Key is G)
        # element is greater then or equal to arr[i] (if order is S)
        while (S!=[] and (arr[S[len(S)-1]] <= arr[i]
        if (order=='G') else  arr[S[len(S)-1]] >= arr[i] )):

            S.pop()

        # store the next greater element of current element
        if (S!=[]):
            next[i] = S[len(S)-1]

        # If all elements in S were smaller than arr[i]
        else:
            next[i] = -1

        # Push this element
        S.append(i)

# Function to find Right smaller element of next greater
# element
def nextSmallerOfNextGreater(arr, n):
    NG = [None]*n  #  stores indexes of next greater elements
    RS = [None]*n  # stores indexes of right smaller elements

    # Find next greater element
    # Here G indicate next greater element
    nextGreater(arr, n, NG, 'G')

    # Find right smaller element
    # using same function nextGreater()
    # Here S indicate right smaller elements
    nextGreater(arr, n, RS, 'S')

    # If NG[i] == -1 then there is no smaller element
    # on right side. We can find Right smaller of next
    # greater by arr[RS[NG[i]]]
    for i in range(n):
        if (NG[i] != -1 and RS[NG[i]] != -1):
            print(arr[RS[NG[i]]],end=" ")
        else:
            print("-1",end=" ")

# Driver program
if __name__=="__main__":
    arr = [5, 1, 9, 2, 5, 1, 7]
    n = len(arr)
    nextSmallerOfNextGreater(arr, n)

# this code is contributed by ChitraNayal
```

## C#

```
using System;
using System.Collections.Generic;

// C# Program to find Right smaller element of next
// greater element
public class GFG {
    // function find Next greater element
    public static void nextGreater(int []arr, int []next, char order)
    {
        // create empty stack
        Stack<int> stack=new Stack<int>();

        // Traverse all array elements in reverse order
        // order == 'G' we compute next greater elements of
        //             every element
        // order == 'S' we compute right smaller element of
        //             every element
        for (int i=arr.Length-1; i>=0; i--)
        {
            // Keep removing top element from S while the top
            // element is smaller then or equal to arr[i] (if Key is G)
            // element is greater then or equal to arr[i] (if order is S)
            while (stack.Count!=0 && ((order=='G')? arr[stack.Peek()] <= arr[i]:arr[stack.Peek()] >= arr[i]))
                stack.Pop();

            // store the next greater element of current element
            if (stack.Count!=0)
                next[i] = stack.Peek();

            // If all elements in S were smaller than arr[i]
            else
                next[i] = -1;

            // Push this element
            stack.Push(i);
        }
    }

    // Function to find Right smaller element of next greater
    // element
    public static void nextSmallerOfNextGreater(int []arr)
    {
        int []NG=new int[arr.Length]; // stores indexes of next greater elements
        int []RS=new int[arr.Length]; // stores indexes of right smaller elements

        // Find next greater element
        // Here G indicate next greater element
        nextGreater(arr, NG, 'G');

        // Find right smaller element
        // using same function nextGreater()
        // Here S indicate right smaller elements
        nextGreater(arr, RS, 'S');

        // If NG[i] == -1 then there is no smaller element
        // on right side. We can find Right smaller of next
        // greater by arr[RS[NG[i]]]
        for (int i=0; i< arr.Length; i++)
        {
            if (NG[i] != -1 && RS[NG[i]] != -1)
                Console.Write(arr[RS[NG[i]]]+" ");
            else
                Console.Write("-1 ");
        }
    }

    public static void Main() {
        int []arr = {5, 1, 9, 2, 5, 1, 7};
        nextSmallerOfNextGreater(arr);
    }
}
// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript Program to find Right smaller element of next
// greater element

    // function find Next greater element
    function nextGreater(arr,next,order)
    {

        // create empty stack
        let stack = [];

        // Traverse all array elements in reverse order
        // order == 'G' we compute next greater elements of
        //              every element
        // order == 'S' we compute right smaller element of
        //              every element
        for (let i = arr.length - 1; i >= 0; i--)
        {

            // Keep removing top element from S while the top
            // element is smaller then or equal to arr[i] (if Key is G)
            // element is greater then or equal to arr[i] (if order is S)
            while (stack.length!=0 && ((order=='G')? arr[stack[stack.length-1]] <= arr[i] : arr[stack[stack.length-1]] >= arr[i]))
                stack.pop();

            // store the next greater element of current element
            if (stack.length != 0)
                next[i] = stack[stack.length - 1];

            // If all elements in S were smaller than arr[i]
            else
                next[i] = -1;

            // Push this element
            stack.push(i);
        }
    }

    // Function to find Right smaller element of next greater
    // element
    function nextSmallerOfNextGreater(arr)
    {
        let NG = new Array(arr.length); // stores indexes of next greater elements
        let RS = new Array(arr.length); // stores indexes of right smaller elements
        for(let i = 0; i < arr.length; i++)
        {
            NG[i] = 0;
            RS[i] = 0;
        }

        // Find next greater element
        // Here G indicate next greater element
        nextGreater(arr, NG, 'G');

        // Find right smaller element
        // using same function nextGreater()
        // Here S indicate right smaller elements
        nextGreater(arr, RS, 'S');

        // If NG[i] == -1 then there is no smaller element
        // on right side. We can find Right smaller of next
        // greater by arr[RS[NG[i]]]
        for (let i = 0; i < arr.length; i++)
        {
            if (NG[i] != -1 && RS[NG[i]] != -1)
                document.write(arr[RS[NG[i]]] + " ");
            else
                document.write("-1 ");
        }
    }

    // Driver code
    let arr = [5, 1, 9, 2, 5, 1, 7];
    nextSmallerOfNextGreater(arr);

    // This code is contributed by rag2127
</script>
```

**输出:**

```
2 2 -1 1 -1 -1 -1
```

**时间复杂度:** O(n)
本文由 **Nishant_Singh(Pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。