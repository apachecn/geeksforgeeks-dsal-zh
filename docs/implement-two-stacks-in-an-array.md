# 在一个数组中实现两个栈

> 原文： [https://www.geeksforgeeks.org/implement-two-stacks-in-an-array/](https://www.geeksforgeeks.org/implement-two-stacks-in-an-array/)

创建代表两个栈的数据结构 **twoStacks**。 **twoStacks** 的实现应该仅使用一个数组，即两个栈都应使用相同的数组来存储元素。 **twoStacks** 必须支持以下函数。

`push1(int x)`：将`x`推送到第一栈。

`push2(int x)`：将`x`推送到第二栈。

`pop1()`：从第一个栈中弹出一个元素，然后返回弹出的元素。

`pop2()`：从第二个栈中弹出一个元素，然后返回弹出的元素。

**twoStacks** 的实现应节省空间。



**方法 1（将空间分成两半）**：

实现两个栈的简单方法是将数组分成两半，并将一半的一半空间分配给两个栈，即使用`arr[0]`到`arr[n / 2]`（对于`stack1`），以及`arr[(n / 2) + 1]`到`arr[n-1]`（对于`stack2`），其中`arr[]`是要用于实现两个栈的数组，数组的大小为`n`。

这种方法的问题是无法有效利用数组空间。 即使`arr[]`中有可用空间，栈推入操作也可能导致栈溢出。 例如，假设数组大小为 6，我们将 3 个元素压入`stack1`，而不压入第二个`stack2`。 当我们将第 4 个元素压入`stack1`时，即使我们在数组中还有 3 个元素的空间，也会有溢出。

```

#include <iostream> 
#include <stdlib.h> 

using namespace std; 

class twoStacks { 
    int* arr; 
    int size; 
    int top1, top2; 

public: 
    // Constructor 
    twoStacks(int n) 
    { 
        size = n; 
        arr = new int[n]; 
        top1 = n / 2 + 1; 
        top2 = n / 2; 
    } 

    // Method to push an element x to stack1 
    void push1(int x) 
    { 
        // There is at least one empty 
        // space for new element 
        if (top1 > 0) { 
            top1--; 
            arr[top1] = x; 
        } 
        else { 
            cout << "Stack Overflow"
                 << " By element :" << x << endl; 
            return; 
        } 
    } 

    // Method to push an element 
    // x to stack2 
    void push2(int x) 
    { 

        // There is at least one empty 
        // space for new element 
        if (top2 < size - 1) { 
            top2++; 
            arr[top2] = x; 
        } 
        else { 
            cout << "Stack Overflow"
                 << " By element :" << x << endl; 
            return; 
        } 
    } 

    // Method to pop an element from first stack 
    int pop1() 
    { 
        if (top1 <= size / 2) { 
            int x = arr[top1]; 
            top1++; 
            return x; 
        } 
        else { 
            cout << "Stack UnderFlow"; 
            exit(1); 
        } 
    } 

    // Method to pop an element 
    // from second stack 
    int pop2() 
    { 
        if (top2 >= size / 2 + 1) { 
            int x = arr[top2]; 
            top2--; 
            return x; 
        } 
        else { 
            cout << "Stack UnderFlow"; 
            exit(1); 
        } 
    } 
}; 

/* Driver program to test twStacks class */
int main() 
{ 
    twoStacks ts(5); 
    ts.push1(5); 
    ts.push2(10); 
    ts.push2(15); 
    ts.push1(11); 
    ts.push2(7); 
    cout << "Popped element from stack1 is "
         << " : " << ts.pop1() 
         << endl; 
    ts.push2(40); 
    cout << "\nPopped element from stack2 is "
         << ": " << ts.pop2() 
         << endl; 
    return 0; 
} 

```

**输出**：

```
Stack Overflow By element :7
Popped element from stack1 is  : 11
Stack Overflow By element :40
Popped element from stack2 is : 15

```

**复杂度分析**：

*   **时间复杂度**：

    *   **推入操作**：`O(1)`。

    *   **弹出操作**：`O(1)`。

*   **辅助空间**：`O(n)`。

    这样使用数组来实现栈。 这不是如上所述的空间优化方法。

**方法 2（节省空间的实现）**：

此方法有效地利用了可用空间。 如果`arr[]`中有可用空间，则不会导致溢出。 这个想法是从`arr[]`的两个极端角开始两个栈。 `stack1`从最左边的元素开始，`stack1`中的第一个元素被推入索引 0。`stack2`从最右边的角开始，`stack2`中的第一个元素被推入索引`n - 1`。 两个堆叠都沿相反的方向生长（或收缩）。 要检查溢出，我们需要检查的是两个栈的顶部元素之间的空间。 此检查在下面的代码中突出显示。

## C++

```cpp
#include <iostream> 
#include <stdlib.h> 
  
using namespace std; 
  
class twoStacks { 
    int* arr; 
    int size; 
    int top1, top2; 
  
public: 
    twoStacks(int n) // constructor 
    { 
        size = n; 
        arr = new int[n]; 
        top1 = -1; 
        top2 = size; 
    } 
  
    // Method to push an element x to stack1 
    void push1(int x) 
    { 
        // There is at least one empty space for new element 
        if (top1 < top2 - 1) { 
            top1++; 
            arr[top1] = x; 
        } 
        else { 
            cout << "Stack Overflow"; 
            exit(1); 
        } 
    } 
  
    // Method to push an element x to stack2 
    void push2(int x) 
    { 
        // There is at least one empty 
        // space for new element 
        if (top1 < top2 - 1) { 
            top2--; 
            arr[top2] = x; 
        } 
        else { 
            cout << "Stack Overflow"; 
            exit(1); 
        } 
    } 
  
    // Method to pop an element from first stack 
    int pop1() 
    { 
        if (top1 >= 0) { 
            int x = arr[top1]; 
            top1--; 
            return x; 
        } 
        else { 
            cout << "Stack UnderFlow"; 
            exit(1); 
        } 
    } 
  
    // Method to pop an element from second stack 
    int pop2() 
    { 
        if (top2 < size) { 
            int x = arr[top2]; 
            top2++; 
            return x; 
        } 
        else { 
            cout << "Stack UnderFlow"; 
            exit(1); 
        } 
    } 
}; 
  
/* Driver program to test twStacks class */
int main() 
{ 
    twoStacks ts(5); 
    ts.push1(5); 
    ts.push2(10); 
    ts.push2(15); 
    ts.push1(11); 
    ts.push2(7); 
    cout << "Popped element from stack1 is "
         << ts.pop1(); 
    ts.push2(40); 
    cout << "\nPopped element from stack2 is "
         << ts.pop2(); 
    return 0; 
}
```

## Java

```java
// Java program to implement two stacks in a 
// single array 
class TwoStacks { 
    int size; 
    int top1, top2; 
    int arr[]; 
  
    // Constructor 
    TwoStacks(int n) 
    { 
        arr = new int[n]; 
        size = n; 
        top1 = -1; 
        top2 = size; 
    } 
  
    // Method to push an element x to stack1 
    void push1(int x) 
    { 
        // There is at least one empty space for 
        // new element 
        if (top1 < top2 - 1) { 
            top1++; 
            arr[top1] = x; 
        } 
        else { 
            System.out.println("Stack Overflow"); 
            System.exit(1); 
        } 
    } 
  
    // Method to push an element x to stack2 
    void push2(int x) 
    { 
        // There is at least one empty space for 
        // new element 
        if (top1 < top2 - 1) { 
            top2--; 
            arr[top2] = x; 
        } 
        else { 
            System.out.println("Stack Overflow"); 
            System.exit(1); 
        } 
    } 
  
    // Method to pop an element from first stack 
    int pop1() 
    { 
        if (top1 >= 0) { 
            int x = arr[top1]; 
            top1--; 
            return x; 
        } 
        else { 
            System.out.println("Stack Underflow"); 
            System.exit(1); 
        } 
        return 0; 
    } 
  
    // Method to pop an element from second stack 
    int pop2() 
    { 
        if (top2 < size) { 
            int x = arr[top2]; 
            top2++; 
            return x; 
        } 
        else { 
            System.out.println("Stack Underflow"); 
            System.exit(1); 
        } 
        return 0; 
    } 
  
    // Driver program to test twoStack class 
    public static void main(String args[]) 
    { 
        TwoStacks ts = new TwoStacks(5); 
        ts.push1(5); 
        ts.push2(10); 
        ts.push2(15); 
        ts.push1(11); 
        ts.push2(7); 
        System.out.println("Popped element from"
                           + " stack1 is " + ts.pop1()); 
        ts.push2(40); 
        System.out.println("Popped element from"
                           + " stack2 is " + ts.pop2()); 
    } 
} 
// This code has been contributed by 
// Amit Khandelwal(Amit Khandelwal 1).
```

## Python

```py
# Python Script to Implement two stacks in a list 
class twoStacks: 
      
    def __init__(self, n):     # constructor 
        self.size = n 
        self.arr = [None] * n 
        self.top1 = -1
        self.top2 = self.size 
          
    # Method to push an element x to stack1 
    def push1(self, x): 
          
        # There is at least one empty space for new element 
        if self.top1 < self.top2 - 1 : 
            self.top1 = self.top1 + 1
            self.arr[self.top1] = x 
  
        else: 
            print("Stack Overflow ") 
            exit(1) 
  
    # Method to push an element x to stack2 
    def push2(self, x): 
  
        # There is at least one empty space for new element 
        if self.top1 < self.top2 - 1: 
            self.top2 = self.top2 - 1
            self.arr[self.top2] = x 
  
        else : 
           print("Stack Overflow ") 
           exit(1) 
  
    # Method to pop an element from first stack 
    def pop1(self): 
        if self.top1 >= 0: 
            x = self.arr[self.top1] 
            self.top1 = self.top1 -1
            return x 
        else: 
            print("Stack Underflow ") 
            exit(1) 
  
    # Method to pop an element from second stack 
    def pop2(self): 
        if self.top2 < self.size: 
            x = self.arr[self.top2] 
            self.top2 = self.top2 + 1
            return x 
        else: 
            print("Stack Underflow ") 
            exit() 
  
# Driver program to test twoStacks class 
ts = twoStacks(5) 
ts.push1(5) 
ts.push2(10) 
ts.push2(15) 
ts.push1(11) 
ts.push2(7) 
  
print("Popped element from stack1 is " + str(ts.pop1())) 
ts.push2(40) 
print("Popped element from stack2 is " + str(ts.pop2())) 
  
# This code is contributed by Sunny Karira
```

## C#

```cs
// C# program to implement two 
// stacks in a single array 
using System; 
  
public class TwoStacks { 
    public int size; 
    public int top1, top2; 
    public int[] arr; 
  
    // Constructor 
    public TwoStacks(int n) 
    { 
        arr = new int[n]; 
        size = n; 
        top1 = -1; 
        top2 = size; 
    } 
  
    // Method to push an element x to stack1 
    public virtual void push1(int x) 
    { 
        // There is at least one empty 
        // space for new element 
        if (top1 < top2 - 1) { 
            top1++; 
            arr[top1] = x; 
        } 
        else { 
            Console.WriteLine("Stack Overflow"); 
            Environment.Exit(1); 
        } 
    } 
  
    // Method to push an element x to stack2 
    public virtual void push2(int x) 
    { 
        // There is at least one empty 
        // space for new element 
        if (top1 < top2 - 1) { 
            top2--; 
            arr[top2] = x; 
        } 
        else { 
            Console.WriteLine("Stack Overflow"); 
            Environment.Exit(1); 
        } 
    } 
  
    // Method to pop an element 
    // from first stack 
    public virtual int pop1() 
    { 
        if (top1 >= 0) { 
            int x = arr[top1]; 
            top1--; 
            return x; 
        } 
        else { 
            Console.WriteLine("Stack Underflow"); 
            Environment.Exit(1); 
        } 
        return 0; 
    } 
  
    // Method to pop an element 
    // from second stack 
    public virtual int pop2() 
    { 
        if (top2 < size) { 
            int x = arr[top2]; 
            top2++; 
            return x; 
        } 
        else { 
            Console.WriteLine("Stack Underflow"); 
            Environment.Exit(1); 
        } 
        return 0; 
    } 
  
    // Driver Code 
    public static void Main(string[] args) 
    { 
        TwoStacks ts = new TwoStacks(5); 
        ts.push1(5); 
        ts.push2(10); 
        ts.push2(15); 
        ts.push1(11); 
        ts.push2(7); 
        Console.WriteLine("Popped element from"
                          + " stack1 is " + ts.pop1()); 
        ts.push2(40); 
        Console.WriteLine("Popped element from"
                          + " stack2 is " + ts.pop2()); 
    } 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```php
<?php 
// PHP program to implement two  
// stacks in a single array      
class twoStacks  
{  
    private $arr;  
    private $size;  
    private $top1; 
    private $top2;  
    function __construct($n) 
    { 
        $this->size = $n;  
        $this->arr = array();  
        $this->top1 = -1;  
        $this->top2 = $this->size;  
    } 
  
// Method to push an element x to stack1  
function push1($x)  
{  
    // There is at least one empty  
    // space for new element  
    if ($this->top1 < $this->top2 - 1)  
    {  
        $this->top1++;  
        $this->arr[$this->top1] = $x;  
    }  
    else
    {  
        echo "Stack Overflow";  
        exit();  
    }  
}  
  
// Method to push an element x to stack2  
function push2($x)  
{  
    // There is at least one empty space 
    // for new element  
    if ($this->top1 < $this->top2 - 1)  
    {  
        $this->top2--;  
        $this->arr[$this->top2] = $x;  
    }  
    else
    {  
        echo "Stack Overflow";  
        exit();  
    }  
}  
  
// Method to pop an element  
// from first stack  
function pop1()  
{  
    if ($this->top1 >= 0 )  
    {  
        $x = $this->arr[$this->top1];  
        $this->top1--;  
        return $x;  
    }  
    else
    {  
        echo "Stack UnderFlow";  
        exit();  
    }  
}  
  
// Method to pop an element from  
// second stack  
function pop2()  
{  
    if ($this->top2 < $this->size)  
    {  
        $x = $this->arr[$this->top2];  
        $this->top2++;  
        return $x;  
    }  
    else
    {  
        echo "Stack UnderFlow";  
        exit();  
    }  
}  
};  
  
  
// Driver Code 
$ts = new twoStacks(5);  
$ts->push1(5);  
$ts->push2(10);  
$ts->push2(15);  
$ts->push1(11);  
$ts->push2(7);  
echo "Popped element from stack1 is " .  
                           $ts->pop1();  
$ts->push2(40);  
echo "\nPopped element from stack2 is " .  
                             $ts->pop2();  
  
// This code is contributed by 
// rathbhupendra 
?>
```

输出：

```
Popped element from stack1 is 11
Popped element from stack2 is 40
```

复杂度分析：

+   时间复杂度：
    +   推入操作：`O(1)`。
    +   弹出操作：`O(1)`。
+   辅助空间：`O(N)`。
    
    使用数组实现栈，因此它是一种空间优化的方法。