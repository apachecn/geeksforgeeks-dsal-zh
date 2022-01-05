# 直方图中最大的矩形区域|集合 2

> 原文:[https://www . geesforgeks . org/最大-直方图下矩形/](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)

在给定的直方图中找到可能的最大矩形区域，其中最大矩形可以由多个连续的条组成。为简单起见，假设所有条形都具有相同的宽度，宽度为 1 个单位。
例如，考虑以下具有 7 个高度条的直方图{6，2，5，4，5，1，6}。最大可能矩形为 12(见下图，最大面积矩形以红色突出显示)

![histogram](img/06a8d8b11b0d7e4c39a2695e7523cef8.png)

对于这个问题，我们已经讨论了一个基于[分治的 O(nLogn)解决方案](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/)。在这篇文章中，讨论了 O(n)时间解。像[之前的帖子](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/)一样，为了简单起见，假设所有条的宽度都是 1。对于每个“x”条，我们用“x”作为矩形中最小的条来计算面积。如果我们计算每个条的面积，并找到所有面积的最大值，我们的任务就完成了。如何计算以“x”为最小条的面积？我们需要知道“x”左边第一个较小(小于“x”)条的索引和“x”右边第一个较小条的索引。让我们分别称这些指数为“左指数”和“右指数”。
我们从左到右遍历所有的酒吧，保持一堆酒吧。每个小节都被推到堆栈一次。当看到较小高度的条时，会从堆栈中弹出一个条。当弹出一个条时，我们将弹出的条作为最小条来计算面积。我们如何获得弹出栏的左右索引–当前索引告诉我们“右索引”，堆栈中前一项的索引是“左索引”。下面是完整的算法。
**1)** 创建一个空栈。
**2)** 从第一个小节开始，对每个小节“hist[i]”执行以下操作，其中“I”从 0 到 n-1 不等。
…… **a)** 如果堆栈为空或 hist[i]高于堆栈顶部的条，则按“I”进行堆栈。
…… **b)** 如果该条小于堆叠顶部，则在堆叠顶部较大时继续移除堆叠顶部。让移除的条成为 hist[tp]。用 hist[tp]作为最小条计算矩形的面积。对于 hist[tp]，左索引是堆栈中的前一项(在 tp 之前)，右索引是 I(当前索引)。
**3)** 如果堆栈不为空，则逐个移除堆栈中的所有条，并对每个移除的条执行步骤 2.b。

下面是上述算法的实现。

## C++

```
// C++ program to find maximum rectangular area in
// linear time
#include<bits/stdc++.h>
using namespace std;

// The main function to find the maximum rectangular
// area under given histogram with n bars
int getMaxArea(int hist[], int n)
{
    // Create an empty stack. The stack holds indexes
    // of hist[] array. The bars stored in stack are
    // always in increasing order of their heights.
    stack<int> s;

    int max_area = 0; // Initialize max area
    int tp;  // To store top of stack
    int area_with_top; // To store area with top bar
                       // as the smallest bar

    // Run through all bars of given histogram
    int i = 0;
    while (i < n)
    {
        // If this bar is higher than the bar on top
        // stack, push it to stack
        if (s.empty() || hist[s.top()] <= hist[i])
            s.push(i++);

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with stack
        // top as the smallest (or minimum height) bar.
        // 'i' is 'right index' for the top and element
        // before top in stack is 'left index'
        else
        {
            tp = s.top();  // store the top index
            s.pop();  // pop the top

            // Calculate the area with hist[tp] stack
            // as smallest bar
            area_with_top = hist[tp] * (s.empty() ? i :
                                   i - s.top() - 1);

            // update max area, if needed
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }

    // Now pop the remaining bars from stack and calculate
    // area with every popped bar as the smallest bar
    while (s.empty() == false)
    {
        tp = s.top();
        s.pop();
        area_with_top = hist[tp] * (s.empty() ? i :
                                i - s.top() - 1);

        if (max_area < area_with_top)
            max_area = area_with_top;
    }

    return max_area;
}

// Driver program to test above function
int main()
{
    int hist[] = {6, 2, 5, 4, 5, 1, 6};
    int n = sizeof(hist)/sizeof(hist[0]);
    cout << "Maximum area is " << getMaxArea(hist, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find maximum rectangular area in linear time

import java.util.Stack;

public class RectArea
{
    // The main function to find the maximum rectangular area under given
    // histogram with n bars
    static int getMaxArea(int hist[], int n)
    {
        // Create an empty stack. The stack holds indexes of hist[] array
        // The bars stored in stack are always in increasing order of their
        // heights.
        Stack<Integer> s = new Stack<>();

        int max_area = 0; // Initialize max area
        int tp;  // To store top of stack
        int area_with_top; // To store area with top bar as the smallest bar

        // Run through all bars of given histogram
        int i = 0;
        while (i < n)
        {
            // If this bar is higher than the bar on top stack, push it to stack
            if (s.empty() || hist[s.peek()] <= hist[i])
                s.push(i++);

            // If this bar is lower than top of stack, then calculate area of rectangle
            // with stack top as the smallest (or minimum height) bar. 'i' is
            // 'right index' for the top and element before top in stack is 'left index'
            else
            {
                tp = s.peek();  // store the top index
                s.pop();  // pop the top

                // Calculate the area with hist[tp] stack as smallest bar
                area_with_top = hist[tp] * (s.empty() ? i : i - s.peek() - 1);

                // update max area, if needed
                if (max_area < area_with_top)
                    max_area = area_with_top;
            }
        }

        // Now pop the remaining bars from stack and calculate area with every
        // popped bar as the smallest bar
        while (s.empty() == false)
        {
            tp = s.peek();
            s.pop();
            area_with_top = hist[tp] * (s.empty() ? i : i - s.peek() - 1);

            if (max_area < area_with_top)
                max_area = area_with_top;
        }

        return max_area;

    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int hist[] = { 6, 2, 5, 4, 5, 1, 6 };
        System.out.println("Maximum area is " + getMaxArea(hist, hist.length));
    }
}
//This code is Contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find maximum
# rectangular area in linear time

def max_area_histogram(histogram):

    # This function calculates maximum
    # rectangular area under given
    # histogram with n bars

    # Create an empty stack. The stack
    # holds indexes of histogram[] list.
    # The bars stored in the stack are
    # always in increasing order of
    # their heights.
    stack = list()

    max_area = 0 # Initialize max area

    # Run through all bars of
    # given histogram
    index = 0
    while index < len(histogram):

        # If this bar is higher
        # than the bar on top
        # stack, push it to stack

        if (not stack) or (histogram[stack[-1]] <= histogram[index]):
            stack.append(index)
            index += 1

        # If this bar is lower than top of stack,
        # then calculate area of rectangle with
        # stack top as the smallest (or minimum
        # height) bar.'i' is 'right index' for
        # the top and element before top in stack
        # is 'left index'
        else:
            # pop the top
            top_of_stack = stack.pop()

            # Calculate the area with
            # histogram[top_of_stack] stack
            # as smallest bar
            area = (histogram[top_of_stack] *
                   ((index - stack[-1] - 1)
                   if stack else index))

            # update max area, if needed
            max_area = max(max_area, area)

    # Now pop the remaining bars from
    # stack and calculate area with
    # every popped bar as the smallest bar
    while stack:

        # pop the top
        top_of_stack = stack.pop()

        # Calculate the area with
        # histogram[top_of_stack]
        # stack as smallest bar
        area = (histogram[top_of_stack] *
              ((index - stack[-1] - 1)
                if stack else index))

        # update max area, if needed
        max_area = max(max_area, area)

    # Return maximum area under
    # the given histogram
    return max_area

# Driver Code
hist = [6, 2, 5, 4, 5, 1, 6]
print("Maximum area is",
       max_area_histogram(hist))

# This code is contributed
# by Jinay Shah
```

## C#

```
// C# program to find maximum
// rectangular area in linear time
using System;
using System.Collections.Generic;

class GFG
{
// The main function to find the
// maximum rectangular area under
// given histogram with n bars
public static int getMaxArea(int[] hist,
                             int n)
{
    // Create an empty stack. The stack
    // holds indexes of hist[] array
    // The bars stored in stack are always
    // in increasing order of their heights.
    Stack<int> s = new Stack<int>();

    int max_area = 0; // Initialize max area
    int tp; // To store top of stack
    int area_with_top; // To store area with top
                       // bar as the smallest bar

    // Run through all bars of
    // given histogram
    int i = 0;
    while (i < n)
    {
        // If this bar is higher than the
        // bar on top stack, push it to stack
        if (s.Count == 0 || hist[s.Peek()] <= hist[i])
        {
            s.Push(i++);
        }

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with
        // stack top as the smallest (or minimum 
        // height) bar. 'i' is 'right index' for
        // the top and element before top in stack
        // is 'left index'
        else
        {
            tp = s.Peek(); // store the top index
            s.Pop(); // pop the top

            // Calculate the area with hist[tp]
            // stack as smallest bar
            area_with_top = hist[tp] *
                           (s.Count == 0 ? i : i - s.Peek() - 1);

            // update max area, if needed
            if (max_area < area_with_top)
            {
                max_area = area_with_top;
            }
        }
    }

    // Now pop the remaining bars from
    // stack and calculate area with every
    // popped bar as the smallest bar
    while (s.Count > 0)
    {
        tp = s.Peek();
        s.Pop();
        area_with_top = hist[tp] *
                       (s.Count == 0 ? i : i - s.Peek() - 1);

        if (max_area < area_with_top)
        {
            max_area = area_with_top;
        }
    }

    return max_area;

}

// Driver Code
public static void Main(string[] args)
{
    int[] hist = new int[] {6, 2, 5, 4, 5, 1, 6};
    Console.WriteLine("Maximum area is " +
                       getMaxArea(hist, hist.Length));
}
}

// This code is contributed by Shrikant13
```

**Output**

```
Maximum area is 12
```

**时间复杂度:**由于每个条只推弹出一次，因此该方法的时间复杂度为 O(n)。

**另一种有效的方法:**通过为 **O(n)时间复杂度和 O(n)辅助空间**中的每个元素找到下一个更小的元素和前一个更小的元素。

**第一步:**首先我们取两个数组**left _ small[]**和**right _ small[]**分别用-1 和 n 初始化。

**第二步:**对于每个元素，我们将把上一个小元素和下一个小元素的索引分别存储在 left _ smaller 和 right _ smaller 数组中。

(需要 O(n)时间)。

**第三步:**现在，对于每个元素，我们将把这个 ith 元素作为 left _ small[I]和 right _ small[I]范围内的最小元素，并将其乘以 left _ small[I]和 right _ small[I]的差值来计算面积。

**第四步:**我们可以找到第三步计算的所有面积的最大值，得到想要的最大面积。

## C++

```
#include <bits/stdc++.h>
using namespace std;

//Function to find largest rectangular area possible in a given histogram.
int getMaxArea(int arr[], int n)
{
    // Your code here
    //we create an empty stack here.
    stack<int> s;
    //we push -1 to the stack because for some elements there will be no previous
    //smaller element in the array and we can store -1 as the index for previous smaller.
    s.push(-1);
    int area = arr[0];
    int i = 0;
    //We declare left_smaller and right_smaller array of size n and initialize them with -1 and n as their default value.
    //left_smaller[i] will store the index of previous smaller element for ith element of the array.
    //right_smaller[i] will store the index of next smaller element for ith element of the array.
    vector<int> left_smaller(n, -1), right_smaller(n, n);
    while(i<n){
        while(!s.empty()&&s.top()!=-1&&arr[s.top()]>arr[i]){
            //if the current element is smaller than element with index stored on the
            //top of stack then, we pop the top element and store the current element index
            //as the right_smaller for the poped element.
            right_smaller[s.top()] = i;
            s.pop();
        }
        if(i>0&&arr[i]==arr[i-1]){
            //we use this condition to avoid the unnecessary loop to find the left_smaller.
            //since the previous element is same as current element, the left_smaller will always be the same for both.
            left_smaller[i] = left_smaller[i-1];
        }else{
            //Element with the index stored on the top of the stack is always smaller than the current element.
            //Therefore the left_smaller[i] will always be s.top().
            left_smaller[i] = s.top();
        } 
        s.push(i);
        i++;
    }
    for(int j = 0; j<n; j++){
        //here we find area with every element as the smallest element in their range and compare it with the previous area.
        // in this way we get our max Area form this.
        area = max(area, arr[j]*(right_smaller[j]-left_smaller[j]-1));
    }
    return area;
}

int main()
 {
    int hist[] = {6, 2, 5, 4, 5, 1, 6};
    int n = sizeof(hist)/sizeof(hist[0]);
      cout << "maxArea = " << getMaxArea(hist, n) << endl;
    return 0;
}

//This code is Contributed by Arunit Kumar.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
import java.lang.*;
import java.io.*;

public class RectArea
{

    //Function to find largest rectangular area possible in a given histogram.
    public static int getMaxArea(int arr[], int n)
    {
        // your code here
        //we create an empty stack here.
        Stack<Integer> s = new Stack<>();
        //we push -1 to the stack because for some elements there will be no previous
        //smaller element in the array and we can store -1 as the index for previous smaller.
        s.push(-1);
        int max_area = arr[0];
        //We declare left_smaller and right_smaller array of size n and initialize them with -1 and n as their default value.
        //left_smaller[i] will store the index of previous smaller element for ith element of the array.
        //right_smaller[i] will store the index of next smaller element for ith element of the array.
        int left_smaller[] = new int[n];
        int right_smaller[] = new int[n];
        for (int i = 0; i < n; i++){
            left_smaller[i] = -1;
            right_smaller[i] = n;
        }

        int i = 0;
        while (i < n)
        {
            while(!s.empty()&&s.peek()!=-1&&arr[i]<arr[s.peek()]){
                //if the current element is smaller than element with index stored on the
                //top of stack then, we pop the top element and store the current element index
                //as the right_smaller for the poped element.
                right_smaller[s.peek()] = (int)i;
                s.pop();
            }
            if(i>0&&arr[i]==arr[(i-1)]){
                //we use this condition to avoid the unnecessary loop to find the left_smaller.
                //since the previous element is same as current element, the left_smaller will always be the same for both.
                left_smaller[i] = left_smaller[(int)(i-1)];
            }else{
                //Element with the index stored on the top of the stack is always smaller than the current element.
                //Therefore the left_smaller[i] will always be s.top().
                left_smaller[i] = s.peek();
            }
            s.push(i);
            i++;
        }

        for(i = 0; i<n; i++){
            //here we find area with every element as the smallest element in their range and compare it with the previous area.
            // in this way we get our max Area form this.
            max_area = Math.max(max_area, arr[i]*(right_smaller[i] - left_smaller[i] - 1));
        }

        return max_area;
    }

    public static void main(String[] args)
    {
        int hist[] = { 6, 2, 5, 4, 5, 1, 6 };
        System.out.println("Maximum area is " + getMaxArea(hist, hist.length));
    }
}
//This code is Contributed by Arunit Kumar.
```

## 蟒蛇 3

```
#this is single line comment
"""
this
is
multiline
comment
"""
def getMaxArea(arr):
  s = [-1]
  n = len(arr)
  area = 0
  i = 0
  left_smaller = [-1]*n
  right_smaller = [n]*n
  while i < n:
      while s and (s[-1] != -1) and (arr[s[-1]] > arr[i]):
          right_smaller[s[-1]] = i
          s.pop()
      if((i > 0) and (arr[i] == arr[i-1])):
          left_smaller[i] = left_smaller[i-1]
      else:
          left_smaller[i] = s[-1]
      s.append(i)
      i += 1
  for j in range(0, n):
      area = max(area, arr[j]*(right_smaller[j]-left_smaller[j]-1))
  return area

hist = [6, 2, 5, 4, 5, 1, 6]
print("maxArea = ", getMaxArea(hist))

#This code is contributed by Arunit Kumar
```

**Output**

```
maxArea = 12
```

**时间复杂度:** O(n)

**空间复杂度:** O(n)

**参考文献**
[http://www . informatik . uni-ulm . de/ACM/local/2003/html/直方图. html](http://www.informatik.uni-ulm.de/acm/Locals/2003/html/histogram.html)
[http://www . informatik . uni-ulm . de/ACM/local/2003/html/judge . html](http://www.informatik.uni-ulm.de/acm/Locals/2003/html/judge.html)
感谢 [Ashish Anand](https://www.facebook.com/aasshishh?fref=ts) 提出初步解决方案。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。