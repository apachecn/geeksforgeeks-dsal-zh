# 检查给定的堆栈推送和弹出序列是否有效

> 原文:[https://www . geesforgeks . org/check-if-给定的推和弹出堆栈序列是否有效/](https://www.geeksforgeeks.org/check-if-the-given-push-and-pop-sequences-of-stack-is-valid-or-not/)

给定具有不同值的 push[]和 pop[]序列。任务是检查这是否可能是在最初为空的堆栈上的一系列推送和弹出操作的结果。如果返回“真”，则返回“假”。
**例:**

```
Input: pushed = { 1, 2, 3, 4, 5 }, popped = { 4, 5, 3, 2, 1 }
Output: True
Following sequence can be performed:
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1

Input: pushed = { 1, 2, 3, 4, 5 }, popped = { 4, 3, 5, 1, 2 }
Output: False
1 can't be popped before 2.
```

**方法:**如果元素 X 已被推入堆栈，则检查 pop[]序列中的顶部元素是否为 X。如果它是 X，那么现在弹出它，否则推[]序列的顶部将被改变，使序列无效。因此，类似地，对所有元素执行相同的操作，并检查堆栈是否为空。如果空则打印**真**否则打印**假**。
**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <iostream>
#include <stack>

using namespace std;

// Function to check validity of stack sequence
bool validateStackSequence(int pushed[], int popped[], int len){

    // maintain count of popped elements
    int j = 0;

    // an empty stack
    stack <int> st;
    for(int i = 0; i < len; i++){
        st.push(pushed[i]);

        // check if appended value is next to be popped out
        while (!st.empty() && j < len && st.top() == popped[j]){
            st.pop();
            j++;
        }
    }

    return j == len;
}

// Driver code
int main()
{
   int pushed[] = {1, 2, 3, 4, 5};
   int popped[] = {4, 5, 3, 2, 1};
   int len = sizeof(pushed)/sizeof(pushed[0]);

   cout << (validateStackSequence(pushed, popped, len) ? "True" : "False");

   return 0;
}

// This code is contributed by Rituraj Jain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation
import java.util.*;

class GfG
{

    // Function to check validity of stack sequence
    static boolean validateStackSequence(int pushed[],
                                        int popped[], int len)
    {

        // maintain count of popped elements
        int j = 0;

        // an empty stack
        Stack<Integer> st = new Stack<>();
        for (int i = 0; i < len; i++)
        {
            st.push(pushed[i]);

            // check if appended value
            // is next to be popped out
            while (!st.empty() && j < len &&
                    st.peek() == popped[j])
            {
                st.pop();
                j++;
            }
        }

        return j == len;
    }

    // Driver code
    public static void main(String[] args)
    {
        int pushed[] = {1, 2, 3, 4, 5};
        int popped[] = {4, 5, 3, 2, 1};
        int len = pushed.length;

        System.out.println((validateStackSequence(pushed, popped, len) ? "True" : "False"));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Function to check validity of stack sequence
def validateStackSequence(pushed, popped):
    # maintain count of popped elements
    j = 0

    # an empty stack
    stack = []

    for x in pushed:
        stack.append(x)

        # check if appended value is next to be popped out
        while stack and j < len(popped) and stack[-1] == popped[j]:
            stack.pop()
            j = j + 1

    return j == len(popped)

# Driver code
pushed = [1, 2, 3, 4, 5]
popped = [4, 5, 3, 2, 1]
print(validateStackSequence(pushed, popped))
```

## C#

```
// C# program for above implementation
using System;
using System.Collections.Generic;

class GfG
{

    // Function to check validity of stack sequence
    static bool validateStackSequence(int []pushed,
                                        int []popped, int len)
    {

        // maintain count of popped elements
        int j = 0;

        // an empty stack
        Stack<int> st = new Stack<int>();
        for (int i = 0; i < len; i++)
        {
            st.Push(pushed[i]);

            // check if appended value
            // is next to be popped out
            while (st.Count != 0 && j < len &&
                    st.Peek() == popped[j])
            {
                st.Pop();
                j++;
            }
        }

        return j == len;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []pushed = {1, 2, 3, 4, 5};
        int []popped = {4, 5, 3, 2, 1};
        int len = pushed.Length;

        Console.WriteLine((validateStackSequence(pushed,
                        popped, len) ? "True" : "False"));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check validity of stack sequence
function validateStackSequence($pushed, $popped, $len)
{

    // maintain count of popped elements
    $j = 0;

    // an empty stack
    $st = array();
    for($i = 0; $i < $len; $i++)
    {
        array_push($st, $pushed[$i]);

        // check if appended value is next
        // to be popped out
        while (!empty($st) && $j < $len &&
            $st[count($st) - 1] == $popped[$j])
        {
            array_pop($st);
            $j++;
        }
    }

    return $j == $len;
}

// Driver code
$pushed = array(1, 2, 3, 4, 5);
$popped = array(4, 5, 3, 2, 1);
$len = count($pushed);

echo (validateStackSequence($pushed,
                   $popped, $len) ? "True" : "False");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

function validateStackSequence( pushed, popped, len)
{

    // maintain count of popped elements
    var j = 0;

    // an empty stack
    var st=[];
    for(var i = 0; i < len; i++){
        st.push(pushed[i]);

        // check if appended value is next
        // to be popped out
        while (!st.length==0 && j < len &&
        st[st.length-1] == popped[j])
        {
            st.pop();
            j++;
        }
    }

    return j == len;
}

var pushed = [1, 2, 3, 4, 5];
   var popped = [4, 5, 3, 2, 1];
   var len = pushed.length;

  document.write( (validateStackSequence(pushed, popped, len)
  ? "True" : "False"));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
True
```

**时间复杂度:** O(N)，其中 N 为栈的大小。