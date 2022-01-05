# 堆栈|集合 3(使用堆栈反转字符串)

> 原文:[https://www . geesforgeks . org/stack-set-3-reverse-string-use-stack/](https://www.geeksforgeeks.org/stack-set-3-reverse-string-using-stack/)

给定一个字符串，使用堆栈反转它。比如“GeeksQuiz”应该转换成“ziuQskeeG”。

下面是使用堆栈反转字符串的简单算法。

```
1) Create an empty stack.
2) One by one push all characters of string to stack.
3) One by one pop all characters from stack and put 
   them back to string.
```

以下程序实现了上述算法。

## C++

```
// C++ program to reverse a string using stack
#include <bits/stdc++.h>
using namespace std;

// A structure to represent a stack
class Stack
{
    public:
    int top;
    unsigned capacity;
    char* array;
};

// function to create a stack of given
// capacity. It initializes size of stack as 0
Stack* createStack(unsigned capacity)
{
    Stack* stack = new Stack();
    stack->capacity = capacity;
    stack->top = -1;
    stack->array = new char[(stack->capacity * sizeof(char))];
    return stack;
}

// Stack is full when top is equal to the last index
int isFull(Stack* stack)
{ return stack->top == stack->capacity - 1; }

// Stack is empty when top is equal to -1
int isEmpty(Stack* stack)
{ return stack->top == -1; }

// Function to add an item to stack.
// It increases top by 1
void push(Stack* stack, char item)
{
    if (isFull(stack))
        return;
    stack->array[++stack->top] = item;
}

// Function to remove an item from stack.
// It decreases top by 1
char pop(Stack* stack)
{
    if (isEmpty(stack))
        return -1;
    return stack->array[stack->top--];
}

// A stack based function to reverse a string
void reverse(char str[])
{
    // Create a stack of capacity
    //equal to length of string
    int n = strlen(str);
    Stack* stack = createStack(n);

    // Push all characters of string to stack
    int i;
    for (i = 0; i < n; i++)
        push(stack, str[i]);

    // Pop all characters of string and
    // put them back to str
    for (i = 0; i < n; i++)
        str[i] = pop(stack);
}

// Driver code
int main()
{
    char str[] = "GeeksQuiz";

    reverse(str);
    cout << "Reversed string is " << str;

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to reverse a string using stack
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <limits.h>

// A structure to represent a stack
struct Stack
{
    int top;
    unsigned capacity;
    char* array;
};

// function to create a stack of given
// capacity. It initializes size of stack as 0
struct Stack* createStack(unsigned capacity)
{
    struct Stack* stack = (struct Stack*) malloc(sizeof(struct Stack));
    stack->capacity = capacity;
    stack->top = -1;
    stack->array = (char*) malloc(stack->capacity * sizeof(char));
    return stack;
}

// Stack is full when top is equal to the last index
int isFull(struct Stack* stack)
{ return stack->top == stack->capacity - 1; }

// Stack is empty when top is equal to -1
int isEmpty(struct Stack* stack)
{ return stack->top == -1; }

// Function to add an item to stack.
// It increases top by 1
void push(struct Stack* stack, char item)
{
    if (isFull(stack))
        return;
    stack->array[++stack->top] = item;
}

// Function to remove an item from stack.
// It decreases top by 1
char pop(struct Stack* stack)
{
    if (isEmpty(stack))
        return INT_MIN;
    return stack->array[stack->top--];
}

// A stack based function to reverse a string
void reverse(char str[])
{
    // Create a stack of capacity
    //equal to length of string
    int n = strlen(str);
    struct Stack* stack = createStack(n);

    // Push all characters of string to stack
    int i;
    for (i = 0; i < n; i++)
        push(stack, str[i]);

    // Pop all characters of string and
    // put them back to str
    for (i = 0; i < n; i++)
        str[i] = pop(stack);
}

// Driver program to test above functions
int main()
{
    char str[] = "GeeksQuiz";

    reverse(str);
    printf("Reversed string is %s", str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to reverse
String using Stack */

import java.util.*;

//stack
class Stack
{
    int size;
    int top;
    char[] a;

    //function to check if stack is empty
    boolean isEmpty()
    {
        return (top < 0);
    }

    Stack(int n)
    {
        top = -1;
        size = n;
        a = new char[size];
    }

    //function to push element in Stack
    boolean push(char x)
    {
        if (top >= size)
        {
        System.out.println("Stack Overflow");
        return false;
        }
        else
        {
            a[++top] = x;
            return true;
        }
    }

    //function to pop element from stack
    char pop()
    {
        if (top < 0)
        {
        System.out.println("Stack Underflow");
        return 0;
        }
        else
        {
            char x = a[top--];
            return x;
        }
    }
}

// Driver code
class Main
{
    //function to reverse the string
    public static void reverse(StringBuffer str)
    {
        // Create a stack of capacity
        // equal to length of string
        int n = str.length();
        Stack obj = new Stack(n);

        // Push all characters of string
        // to stack
        int i;
        for (i = 0; i < n; i++)
        obj.push(str.charAt(i));

        // Pop all characters of string
        // and put them back to str
        for (i = 0; i < n; i++)
        {
            char ch = obj.pop();
            str.setCharAt(i,ch);
        }
    }

    //driver function
    public static void main(String args[])
    {
        //create a new string
        StringBuffer s= new StringBuffer("GeeksQuiz");

        //call reverse method
        reverse(s);

        //print the reversed string
        System.out.println("Reversed string is " + s);
    }
}
```

## 计算机编程语言

```
# Python program to reverse a string using stack

# Function to create an empty stack.
# It initializes size of stack as 0
def createStack():
    stack=[]
    return stack

# Function to determine the size of the stack
def size(stack):
    return len(stack)

# Stack is empty if the size is 0
def isEmpty(stack):
    if size(stack) == 0:
        return true

# Function to add an item to stack .
# It increases size by 1
def push(stack,item):
    stack.append(item)

#Function to remove an item from stack.
# It decreases size by 1
def pop(stack):
    if isEmpty(stack): return
    return stack.pop()

# A stack based function to reverse a string
def reverse(string):
    n = len(string)

    # Create a empty stack
    stack = createStack()

    # Push all characters of string to stack
    for i in range(0,n,1):
        push(stack,string[i])

    # Making the string empty since all
    #characters are saved in stack
    string=""

    # Pop all characters of string and
    # put them back to string
    for i in range(0,n,1):
        string+=pop(stack)

    return string

# Driver program to test above functions
string="GeeksQuiz"
string = reverse(string)
print("Reversed string is " + string)

# This code is contributed by Sunny Karira
```

## C#

```
/* C# program to reverse
String using Stack */
using System;
using System.Text;
//stack
class Stack
{
    public int size;
    public int top;
    public char[] a;

    // function to check if stack is empty
    public Boolean isEmpty()
    {
        return (top < 0);
    }

    public Stack(int n)
    {
        top = -1;
        size = n;
        a = new char[size];
    }

    // function to push element in Stack
    public Boolean push(char x)
    {
        if (top >= size)
        {
            Console.WriteLine("Stack Overflow");
            return false;
        }
        else
        {
            a[++top] = x;
            return true;
        }
    }

    // function to pop element from stack
    public char pop()
    {
        if (top < 0)
        {
            Console.WriteLine("Stack Underflow");
            return ' ';
        }
        else
        {
            char x = a[top--];
            return x;
        }
    }
}

class GFG
{
    // function to reverse the string
    public static void reverse(StringBuilder str)
    {
        // Create a stack of capacity
        // equal to length of string
        int n = str.Length;
        Stack obj = new Stack(n);

        // Push all characters of string
        // to stack
        int i;
        for (i = 0; i < n; i++)
        obj.push(str[i]);

        // Pop all characters of string
        // and put them back to str
        for (i = 0; i < n; i++)
        {
            char ch = obj.pop();
            str[i] = ch;
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        // create a new string
        StringBuilder s = new StringBuilder("GeeksQuiz");

        // call reverse method
        reverse(s);

        // print the reversed string
        Console.WriteLine("Reversed string is " + s);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to reverse
// String using Stack

// stack
class Stack
{
    size;
    top;
    a = [];

    // Function to check if stack is empty
    isEmpty()
    {
        return(this.top < 0);
    }

    constructor(n)
    {
        this.top = -1;
        this.size = n;
        this.a = new Array(this.size);
    }

    // Function to push element in Stack
    push(x)
    {
        if (this.top >= this.size)
        {
            document.write("Stack Overflow<br>");
            return false;
        }
        else
        {
            this.a[++this.top] = x;
            return true;
        }
    }

    // Function to pop element from stack
    pop()
    {
        if (this.top < 0)
        {
            document.write("Stack Underflow<br>");
            return 0;
        }
        else
        {
            let x = this.a[this.top--];
            return x;
        }
    }
}

// Function to reverse the string
function reverse(str)
{

    // Create a stack of capacity
    // equal to length of string
    let n = str.length;
    let obj = new Stack(n);

    // Push all characters of string
    // to stack
    let i;
    for(i = 0; i < n; i++)
        obj.push(str[i]);

    // Pop all characters of string
    // and put them back to str
    for(i = 0; i < n; i++)
    {
        let ch = obj.pop();
        str[i] = ch;
    }
}

// Driver Code
let s = "GeeksQuiz".split("");

// Call reverse method
reverse(s);

// Print the reversed string
document.write("Reversed string is " +
               s.join(""));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Reversed string is ziuQskeeG
```

**时间复杂度:** O(n)，其中 n 为栈中字符数。
**辅助空间:** O(n)为叠加。

字符串也可以颠倒，不使用任何辅助空格。跟随 C、Java、C#和 Python 程序实现逆向而不使用栈。

## C++

```
// C++ program to reverse a string without using stack
#include <bits/stdc++.h>
using namespace std;

// A utility function to swap two characters
void swap(char *a, char *b)
{
    char temp = *a;
    *a = *b;
    *b = temp;
}

// A stack based function to reverse a string
void reverse(char str[])
{
    // get size of string
    int n = strlen(str), i;

    for (i = 0; i < n/2; i++)
        swap(&str[i], &str[n-i-1]);
}

// Driver program to test above functions
int main()
{
    char str[] = "abc";

    reverse(str);
    cout<<"Reversed string is "<< str;

    return 0;
}

//This is code is contributed by rathbhupendra
```

## C

```
// C program to reverse a string without using stack
#include <stdio.h>
#include <string.h>

// A utility function to swap two characters
void swap(char *a, char *b)
{
    char temp = *a;
    *a = *b;
    *b = temp;
}

// A stack based function to reverse a string
void reverse(char str[])
{
    // get size of string
    int n = strlen(str), i;

    for (i = 0; i < n/2; i++)
        swap(&str[i], &str[n-i-1]);
}

// Driver program to test above functions
int main()
{
    char str[] = "abc";

    reverse(str);
    printf("Reversed string is %s", str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a string without using stack
public class GFG {
// A utility function to swap two characters

    static void swap(char a[], int index1, int index2) {
        char temp = a[index1];
        a[index1] = a[index2];
        a[index2] = temp;
    }

// A stack based function to reverse a string
    static void reverse(char str[]) {
        // get size of string
        int n = str.length, i;

        for (i = 0; i < n / 2; i++) {
            swap(str, i, n - i - 1);
        }
    }

// Driver program to test above functions
    public static void main(String[] args) {
        char str[] = "abc".toCharArray();

        reverse(str);
        System.out.printf("Reversed string is " + String.valueOf(str));
    }
}
// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python program to reverse a string without stack

# Function to reverse a string
def reverse(string):
    string = string[::-1]
    return string

# Driver program to test above functions
string = "abc"
string = reverse(string)
print("Reversed string is " + string)

# This code is contributed by Sunny Karira
```

## C#

```
// C# program to reverse a string without using stack
using System;
public class GFG {
// A utility function to swap two characters

    static void swap(char []a, int index1, int index2) {
        char temp = a[index1];
        a[index1] = a[index2];
        a[index2] = temp;
    }

// A stack based function to reverse a string
    static void reverse(char []str) {
        // get size of string
        int n = str.Length, i;

        for (i = 0; i < n / 2; i++) {
            swap(str, i, n - i - 1);
        }
    }

// Driver program to test above functions
    public static void Main() {
        char []str = "abc".ToCharArray();

        reverse(str);
        Console.WriteLine("Reversed string is " + String.Join("",str));
    }
}
// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to reverse a string without using stack

// A stack based function to reverse a string
function reverse(str)
{
    // get size of string
    let n = (str).length;
    let i;
    let arr = str.split('');
    for (i = 0; i < n/2; i++)
    {
        let temp = arr[i];
        arr[i] = arr[n-i-1];
        arr[n-i-1] = temp;
    }
    return arr.join('');
}

// Driver program to test above functions
let str = "abc";
str = reverse(str);
document.write("Reversed string is " +str);

</script>
```

**输出:**

```
Reversed string is cba
```

如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。