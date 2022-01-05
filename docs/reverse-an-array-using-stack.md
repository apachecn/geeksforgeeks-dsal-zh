# 使用堆栈

反转数组

> 原文:[https://www.geeksforgeeks.org/reverse-an-array-using-stack/](https://www.geeksforgeeks.org/reverse-an-array-using-stack/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务为[使用](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)[堆叠](https://www.geeksforgeeks.org/stack-data-structure/)反转阵列。

**示例:**

> **输入:** arr[] = { 10，20，30，40，50 }
> **输出:** 50 40 30 20 10
> **解释:**
> 反转数组将 arr[]修改为{ 50，40，30，20，10 }
> 因此，需要的输出为 50 40 30 20 10。
> 
> **输入:**arr[]= { 1 }
> T3】输出: 1

**迭代递归法:**参考文章[反向一个数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)迭代或者递归的解决这个问题。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**[堆叠](https://www.geeksforgeeks.org/stack-data-structure/)为主的方法:**按照以下步骤解决问题:

*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)来存储数组元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[将所有数组元素推入堆栈](https://www.geeksforgeeks.org/stack-push-method-in-java/)。
*   >从堆栈中弹出元素并插入到数组中。
*   Finally, print the array.

    下面是上述方法的实现:

    ## C++

    ```
    // C++ program to implement
    // the above approach
    #include <bits/stdc++.h>
    using namespace std;

    // Structure of stack
    class Stack {
    public:
        // Stores index of top
        // element of a stack
        int top;

        // Stores maximum count of
        // elements stored in a stack
        unsigned capacity;

        // Stores address of
        // array element
        int* array;
    };

    // Function to Initialize a stack
    // of given capacity.
    Stack* createStack(unsigned capacity)
    {
        Stack* stack = new Stack();
        stack->capacity = capacity;
        stack->top = -1;
        stack->array = new int[(stack->capacity
                                * sizeof(int))];
        return stack;
    }

    // Function to check if
    // the stack is full or not
    int isFull(Stack* stack)
    {
        return stack->top
               == stack->capacity - 1;
    }

    // Function to check if
    // the stack is empty or not
    int isEmpty(Stack* stack)
    {
        return stack->top == -1;
    }

    // Function to insert an element
    // into the stack.
    void push(Stack* stack, int item)
    {

        // If stack is full
        if (isFull(stack))
            return;

        // Insert element into stack
        stack->array[++stack->top] = item;
    }

    // Function to remove an element
    // from stack.
    int pop(Stack* stack)
    {

        // If stack is empty
        if (isEmpty(stack))
            return -1;

        // Pop element from stack
        return stack->array[stack->top--];
    }

    // Function to reverse the array elements
    void reverseArray(int arr[], int n)
    {

        // Initialize a stack of capacity n
        Stack* stack = createStack(n);

        for (int i = 0; i < n; i++) {

            // Insert arr[i] into the stack
            push(stack, arr[i]);
        }

        // Reverse the array elements
        for (int i = 0; i < n; i++) {

            // Update arr[i]
            arr[i] = pop(stack);
        }

        // Print array elements
        for (int i = 0; i < n; i++)
            cout << arr[i] << " ";
    }

    // Driver Code
    int main()
    {

        int arr[] = { 100, 200, 300, 400 };

        int N = sizeof(arr) / sizeof(arr[0]);
        reverseArray(arr, N);
        return 0;
    }
    ```

    ## C

    ```
    // C program to implement
    // the above approach
    #include <limits.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>

    // Structure of stack
    struct Stack {

        // Stores index of top
        // element of a stack
        int top;

        // Stores maximum count of
        // elements stored in a stack
        unsigned capacity;

        // Stores address of
        // array element
        int* array;
    };

    // Function to Initialize a stack
    // of given capacity.
    struct Stack* createStack(unsigned capacity)
    {
        struct Stack* stack
            = (struct Stack*)malloc(
                sizeof(struct Stack));
        stack->capacity = capacity;
        stack->top = -1;
        stack->array
            = (int*)malloc(
                stack->capacity
                * sizeof(int));
        return stack;
    }

    // Function to check if
    // the stack is full or not
    int isFull(struct Stack* stack)
    {
        return stack->top
               == stack->capacity - 1;
    }

    // Function to check if
    // the stack is empty or not
    int isEmpty(struct Stack* stack)
    {
        return stack->top == -1;
    }

    // Function to insert an element
    // into the stack.
    void push(struct Stack* stack, int item)
    {

        // If stack is full
        if (isFull(stack))
            return;

        // Insert element into stack
        stack->array[++stack->top] = item;
    }

    // Function to remove an element
    // from stack.
    int pop(struct Stack* stack)
    {

        // If stack is empty
        if (isEmpty(stack))
            return -1;

        // Pop element from stack
        return stack->array[stack->top--];
    }

    // Function to reverse the array elements
    void reverseArray(int arr[], int n)
    {

        // Initialize a stack of capacity n
        struct Stack* stack = createStack(n);

        for (int i = 0; i < n; i++) {

            // Insert arr[i] into the stack
            push(stack, arr[i]);
        }

        // Reverse the array elements
        for (int i = 0; i < n; i++) {

            // Update arr[i]
            arr[i] = pop(stack);
        }

        // Print array elements
        for (int i = 0; i < n; i++)
            printf("%d ", arr[i]);
    }

    // Driver Code
    int main()
    {

        int arr[] = { 100, 200, 300, 400 };

        int N = sizeof(arr) / sizeof(arr[0]);
        reverseArray(arr, N);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to implement
    // the above approach
    import java.util.*;

    // Structure of stack
    class Stack {

        // Stores maximum count of
        // elements stored in a stack
        int size;

        // Stores index of top
        // element of a stack
        int top;

        // Stores address of
        // array element
        int[] a;

        // Function to check if
        // the stack is empty or not
        boolean isEmpty()
        {
            return (top < 0);
        }

        // Function to Initialize
        // a stack of given capacity.
        Stack(int n)
        {
            top = -1;
            size = n;
            a = new int[size];
        }

        // Function to push
        // an element into Stack
        boolean push(int x)
        {

            // If Stack is full
            if (top >= size) {
                System.out.println(
                    "Stack Overflow");
                return false;
            }
            else {

                // Insert element
                // into stack
                a[++top] = x;
                return true;
            }
        }

        // Function to remove an element
        // from stack.
        int pop()
        {

            // If stack is empty
            if (top < 0) {
                System.out.println(
                    "Stack Underflow");
                return 0;
            }

            // Pop element from stack
            else {
                int x = a[top--];
                return x;
            }
        }
    }

    // Driver Code
    class Main {

        // Function to reverse the array elements
        public static void reverse(int arr[], int n)
        {

            // Initialize a stack of capacity n
            Stack obj = new Stack(n);

            for (int i = 0; i < n; i++) {

                // Insert arr[i] into the stack
                obj.push(arr[i]);
            }

            // Reverse the array elements
            for (int i = 0; i < n; i++) {

                // Update arr[i]
                arr[i] = obj.pop();
            }

            // Print array elements
            for (int i = 0; i < n; i++) {
                System.out.print(arr[i] + " ");
            }
        }

        // Driver function
        public static void main(String args[])
        {
            int n = 4;

            // Create a new array
            int[] a = new int[] { 100, 200, 300, 400 };

            // Call reverse method
            reverse(a, n);
        }
    }
    ```

    **Output:**

    ```
    400 300 200 100

    ```

    ***时间复杂度:**O(N)*
    T5**辅助空间:** O(N) 。