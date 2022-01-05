# 使用递归反转堆栈

> 原文:[https://www . geesforgeks . org/reverse-a-stack-use-recursive/](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)

编写一个程序来使用递归反转堆栈。不允许使用循环构造，如 while，for..等等，您只能在堆栈 S 上使用以下 ADT 函数:
isEmpty(S)
push(S)
pop(S)

解决方案的思想是将所有值保存在函数调用堆栈中，直到堆栈变空。当堆栈变空时，将所有保存的项目逐一插入堆栈底部。
例如，让输入栈为

```
    1  <-- top
    2
    3
    4    
```

```
First 4 is inserted at the bottom.
    4 <-- top

Then 3 is inserted at the bottom
    4 <-- top    
    3

Then 2 is inserted at the bottom
    4 <-- top    
    3 
    2

Then 1 is inserted at the bottom
    4 <-- top    
    3 
    2
    1
```

因此，我们需要一个使用上面给出的基本堆栈函数在堆栈底部插入的函数。

**void insertAtBottom(():** 首先弹出所有堆栈项，并使用递归将弹出的项存储在函数调用堆栈中。并且当堆栈变空时，推送新项和存储在调用堆栈中的所有项。

**void reverse():** 该功能主要使用 insertAtBottom()将所有项目逐一弹出，并将弹出的项目插入底部。

## C++

```
// C++ code to reverse a
// stack using recursion
#include<bits/stdc++.h>
using namespace std;

// using std::stack for
// stack implementation
stack<char> st;

// initializing a string to store
// result of reversed stack
string ns;

// Below is a recursive function
// that inserts an element
// at the bottom of a stack.
void insert_at_bottom(char x)
{

    if(st.size() == 0)
    st.push(x);

    else
    {

        // All items are held in Function Call
        // Stack until we reach end of the stack
        // When the stack becomes empty, the
        // st.size() becomes 0, the above if
        // part is executed and the item is
        // inserted at the bottom

        char a = st.top();
        st.pop();
        insert_at_bottom(x);

        // push allthe items held in
        // Function Call Stack
        // once the item is inserted
        // at the bottom
        st.push(a);
    }
}

// Below is the function that
// reverses the given stack using
// insert_at_bottom()
void reverse()
{
    if(st.size()>0)
    {

        // Hold all items in Function
        // Call Stack until we
        // reach end of the stack
        char x = st.top();
        st.pop();
        reverse();

        // Insert all the items held
        // in Function Call Stack
        // one by one from the bottom
        // to top. Every item is
        // inserted at the bottom
        insert_at_bottom(x);
    }
}

// Driver Code
int main()
{

    // push elements into
    // the stack
    st.push('1');
    st.push('2');
    st.push('3');
    st.push('4');

    cout<<"Original Stack"<<endl;

    // print the elements
    // of original stack
    cout<<"1"<<" "<<"2"<<" "
        <<"3"<<" "<<"4"
        <<endl;

    // function to reverse
    // the stack
    reverse();
    cout<<"Reversed Stack"
        <<endl;

    // storing values of reversed
    // stack into a string for display
    while(!st.empty())
    {
        char p=st.top();
        st.pop();
        ns+=p;
    }

    //display of reversed stack
    cout<<ns[3]<<" "<<ns[2]<<" "
        <<ns[1]<<" "<<ns[0]<<endl;
    return 0;
}

// This code is contributed by Gautam Singh
```

## C

```
// C program to reverse a
// stack using recursion
#include<stdio.h>
#include<stdlib.h>
#define bool int

// structure of a stack node
struct sNode
{
    char data;
    struct sNode *next;
};

// Function Prototypes
void push(struct sNode** top_ref,
                   int new_data);
int pop(struct sNode** top_ref);
bool isEmpty(struct sNode* top);
void print(struct sNode* top);

// Below is a recursive function
// that inserts an element
// at the bottom of a stack.
void insertAtBottom(struct sNode** top_ref,
                                 int item)
{
    if (isEmpty(*top_ref))
        push(top_ref, item);
    else
    {

        // Hold all items in Function Call
        // Stack until we reach end of the
        // stack. When the stack becomes
        // empty, the isEmpty(*top_ref)becomes
        // true, the above if part is executed
        // and the item is inserted at the bottom
        int temp = pop(top_ref);
        insertAtBottom(top_ref, item);

        // Once the item is inserted
        // at the bottom, push all
        // the items held in Function
        // Call Stack
        push(top_ref, temp);
    }
}

// Below is the function that
// reverses the given stack using
// insertAtBottom()
void reverse(struct sNode** top_ref)
{
    if (!isEmpty(*top_ref))
    {
        // Hold all items in Function
        // Call Stack until we
        // reach end of the stack
        int temp = pop(top_ref);
        reverse(top_ref);

        // Insert all the items (held in
        // Function Call Stack)
        // one by one from the bottom
        // to top. Every item is
        // inserted at the bottom
        insertAtBottom(top_ref, temp);
    }
}

// Driver Code
int main()
{
    struct sNode *s = NULL;
    push(&s, 4);
    push(&s, 3);
    push(&s, 2);
    push(&s, 1);

    printf("\n Original Stack ");
    print(s);
    reverse(&s);
    printf("\n Reversed Stack ");
    print(s);
    return 0;
}

// Function to check if
// the stack is empty
bool isEmpty(struct sNode* top)
{
    return (top == NULL)? 1 : 0;
}

// Function to push an item to stack
void push(struct sNode** top_ref,
                    int new_data)
{

    // allocate node
    struct sNode* new_node =
        (struct sNode*) malloc(sizeof(struct sNode));

    if (new_node == NULL)
    {
        printf("Stack overflow \n");
        exit(0);
    }

    // put in the data
    new_node->data = new_data;

    // link the old list
    // off the new node
    new_node->next = (*top_ref);

    // move the head to
    // point to the new node
    (*top_ref) = new_node;
}

// Function to pop an item from stack
int pop(struct sNode** top_ref)
{
    char res;
    struct sNode *top;

    // If stack is empty then error
    if (*top_ref == NULL)
    {
        printf("Stack overflow \n");
        exit(0);
    }
    else
    {
        top = *top_ref;
        res = top->data;
        *top_ref = top->next;
        free(top);
        return res;
    }
}

// Function to print a
// linked list
void print(struct sNode* top)
{
    printf("\n");
    while (top != NULL)
    {
        printf(" %d ", top->data);
        top = top->next;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to reverse a
// stack using recursion
import java.util.Stack;

class Test {

    // using Stack class for
    // stack implementation
    static Stack<Character> st = new Stack<>();

    // Below is a recursive function
    // that inserts an element
    // at the bottom of a stack.
    static void insert_at_bottom(char x)
    {

        if(st.isEmpty())
            st.push(x);

        else
        {

            // All items are held in Function
            // Call Stack until we reach end
            // of the stack. When the stack becomes
            // empty, the st.size() becomes 0, the
            // above if part is executed and
            // the item is inserted at the bottom
            char a = st.peek();
            st.pop();
            insert_at_bottom(x);

            // push allthe items held
            // in Function Call Stack
            // once the item is inserted
            // at the bottom
            st.push(a);
        }
    }

    // Below is the function that
    // reverses the given stack using
    // insert_at_bottom()
    static void reverse()
    {
        if(st.size() > 0)
        {

            // Hold all items in Function
            // Call Stack until we
            // reach end of the stack
            char x = st.peek();
            st.pop();
            reverse();

            // Insert all the items held
            // in Function Call Stack
            // one by one from the bottom
            // to top. Every item is
            // inserted at the bottom
            insert_at_bottom(x);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // push elements into
        // the stack
        st.push('1');
        st.push('2');
        st.push('3');
        st.push('4');

        System.out.println("Original Stack");

        System.out.println(st);

        // function to reverse
        // the stack
        reverse();

        System.out.println("Reversed Stack");

        System.out.println(st);
    }
}
```

## 蟒蛇 3

```
# Python program to reverse a
# stack using recursion

# Below is a recursive function
# that inserts an element
# at the bottom of a stack.
def insertAtBottom(stack, item):
    if isEmpty(stack):
        push(stack, item)
    else:
        temp = pop(stack)
        insertAtBottom(stack, item)
        push(stack, temp)

# Below is the function that
# reverses the given stack
# using insertAtBottom()
def reverse(stack):
    if not isEmpty(stack):
        temp = pop(stack)
        reverse(stack)
        insertAtBottom(stack, temp)

# Below is a complete running
# program for testing above
# functions.

# Function to create a stack.
# It initializes size of stack
# as 0
def createStack():
    stack = []
    return stack

# Function to check if
# the stack is empty
def isEmpty( stack ):
    return len(stack) == 0

# Function to push an
# item to stack
def push( stack, item ):
    stack.append( item )

# Function to pop an
# item from stack
def pop( stack ):

    # If stack is empty
    # then error
    if(isEmpty( stack )):
        print("Stack Underflow ")
        exit(1)

    return stack.pop()

# Function to print the stack
def prints(stack):
    for i in range(len(stack)-1, -1, -1):
        print(stack[i], end = ' ')
    print()

# Driver Code

stack = createStack()
push( stack, str(4) )
push( stack, str(3) )
push( stack, str(2) )
push( stack, str(1) )
print("Original Stack ")
prints(stack)

reverse(stack)

print("Reversed Stack ")
prints(stack)

# This code is contributed by Sunny Karira
```

## C#

```
// C# code to reverse a
// stack using recursion
using System;
using System.Collections;

public class GFG
{

    // using Stack class for
    // stack implementation
    static Stack st = new Stack();

    // Below is a recursive function
    // that inserts an element
    // at the bottom of a stack.
    static void insert_at_bottom(char x)
    {

        if(st.Count==0)
            st.Push(x);

        else
        {

            // All items are held in Function
            // Call Stack until we reach end
            // of the stack. When the stack becomes
            // empty, the st.size() becomes 0, the
            // above if part is executed and
            // the item is inserted at the bottom
            char a = (char)st.Peek();
            st.Pop();
            insert_at_bottom(x);

            // push all the items held
            // in Function Call Stack
            // once the item is inserted
            // at the bottom
            st.Push(a);
        }
    }

    // Below is the function that
    // reverses the given stack using
    // insert_at_bottom()
    static void reverse()
    {
        if(st.Count > 0)
        {

            // Hold all items in Function
            // Call Stack until we
            // reach end of the stack
            char x = (char)st.Peek();
            st.Pop();
            reverse();

            // Insert all the items held
            // in Function Call Stack
            // one by one from the bottom
            // to top. Every item is
            // inserted at the bottom
            insert_at_bottom(x);
        }
    }

    // Driver Code
    public static void Main(String []args)
    {

        // push elements into
        // the stack
        st.Push('1');
        st.Push('2');
        st.Push('3');
        st.Push('4');

        Console.WriteLine("Original Stack");

        foreach (char i in st)
        {
            Console.WriteLine(i);
        }

        // function to reverse
        // the stack
        reverse();

        Console.WriteLine("Reversed Stack");
        foreach (char i in st)
        {
            Console.WriteLine(i);
        }
    }

}

// This code is Contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript code to reverse a
// stack using recursion

// using Stack class for
// stack implementation
let st = [];

// Below is a recursive function
// that inserts an element
// at the bottom of a stack.
function insert_at_bottom(x)
{
    if(st.length==0)
        st.push(x);
    else
    {
        // All items are held in Function
            // Call Stack until we reach end
            // of the stack. When the stack becomes
            // empty, the st.size() becomes 0, the
            // above if part is executed and
            // the item is inserted at the bottom
            let a = st.pop();
            insert_at_bottom(x);

            // push allthe items held
            // in Function Call Stack
            // once the item is inserted
            // at the bottom
            st.push(a);
    }

}

// Below is the function that
    // reverses the given stack using
    // insert_at_bottom()
function reverse()
{
    if(st.length > 0)
        {

            // Hold all items in Function
            // Call Stack until we
            // reach end of the stack
            let x = st.pop();
            reverse();

            // Insert all the items held
            // in Function Call Stack
            // one by one from the bottom
            // to top. Every item is
            // inserted at the bottom
            insert_at_bottom(x);
        }
}

// Driver Code

// push elements into
// the stack
st.push('1');
st.push('2');
st.push('3');
st.push('4');

document.write("Original Stack<br>");

document.write(st.join(" ")+"<br>");

// function to reverse
// the stack
reverse();

document.write("Reversed Stack<br>");

document.write(st.join(" "));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
 Original Stack 
 1  2  3  4 
 Reversed Stack 
 4  3  2  1 
```

**时间复杂度**:这种方法采用了 O(n^2 最差的时间复杂度，

如果发现以上代码/算法有任何 bug，请写评论，或者找其他方法解决同样的问题。