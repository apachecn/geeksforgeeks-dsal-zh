# 检查数组是否可堆栈排序

> 原文:[https://www.geeksforgeeks.org/check-array-stack-sortable/](https://www.geeksforgeeks.org/check-array-stack-sortable/)

给定 N 个不同元素的数组，其中元素介于 1 和 N 之间(包括 1 和 N)，检查它是否可堆栈排序。如果一个数组 A[]可以存储在另一个数组 B[]中，使用一个临时堆栈 s，则称其为堆栈可排序的。

阵列上允许的操作有:

1.  移除数组 A[]的起始元素，并将其推入堆栈。
2.  移除堆栈 S 的顶部元素，并将其附加到数组 b 的末尾。

如果 A[]的所有元素都可以通过执行这些操作移动到 B[]，使得数组 B 按升序排序，那么数组 A[]是堆栈可排序的。

示例:

```
Input : A[] = { 3, 2, 1 }
Output : YES
Explanation : 
Step 1: Remove the starting element of array A[] 
        and push it in the stack S. ( Operation 1)
        That makes A[] = { 2, 1 } ; Stack S = { 3 }
Step 2: Operation 1
        That makes A[] = { 1 } Stack S = { 3, 2 }
Step 3: Operation 1
        That makes A[] = {} Stack S = { 3, 2, 1 }
Step 4: Operation 2
        That makes Stack S = { 3, 2 } B[] = { 1 }
Step 5: Operation 2
        That makes Stack S = { 3 } B[] = { 1, 2 }
Step 6: Operation 2
        That makes Stack S = {} B[] = { 1, 2, 3 }

Input : A[] = { 2, 3, 1}
Output : NO

```

给定，数组 A[]是[1，…，N]的置换，那么让我们假设最初的 B[] = {0}。现在我们可以观察到:

1.  我们只能在堆栈为空或者当前元素小于堆栈顶部的情况下，推送堆栈 S 中的一个元素。
2.  We can only pop from the stack only if the top of the stack is ![B[end] + 1](img/c52f7d71bde4197dfac382ddccee6a9c.png "Rendered by QuickLaTeX.com") as the array B[] will contain {1, 2, 3, 4, …, n}.

    如果我们不能推数组 A[]的起始元素，那么给定的数组是不可堆栈排序的。

    以下是上述思路的实现:

    ## C++

    ```
    // C++ implementation of above approach.
    #include <bits/stdc++.h>
    using namespace std;

    // Function to check if A[] is
    // Stack Sortable or Not.
    bool check(int A[], int N)
    {
        // Stack S
        stack<int> S;

        // Pointer to the end value of array B.
        int B_end = 0;

        // Traversing each element of A[] from starting
        // Checking if there is a valid operation 
        // that can be performed.
        for (int i = 0; i < N; i++) 
        {
            // If the stack is not empty
            if (!S.empty()) 
            {
                // Top of the Stack.
                int top = S.top();

                // If the top of the stack is
                // Equal to B_end+1, we will pop it
                // And increment B_end by 1.
                while (top == B_end + 1) 
                {
                    // if current top is equal to
                    // B_end+1, we will increment 
                    // B_end to B_end+1
                    B_end = B_end + 1;

                    // Pop the top element.
                    S.pop();

                    // If the stack is empty We cannot
                    // further perfom this operation.
                    // Therefore break
                    if (S.empty()) 
                    {
                        break;
                    }

                    // Current Top
                    top = S.top();
                }

                // If stack is empty
                // Push the Current element
                if (S.empty()) {
                    S.push(A[i]);
                }
                else 
                {
                    top = S.top();

                    // If the Current element of the array A[]
                    // if smaller than the top of the stack
                    // We can push it in the Stack.
                    if (A[i] < top) 
                    {
                        S.push(A[i]);
                    }
                    // Else We cannot sort the array
                    // Using any valid operations.
                    else 
                    {
                        // Not Stack Sortable
                        return false;
                    }
                }
            }
            else 
            {
                // If the stack is empty push the current
                // element in the stack.
                S.push(A[i]);
            }
        }

        // Stack Sortable
        return true;
    }

    // Driver's Code
    int main()
    {
        int A[] = { 4, 1, 2, 3 };
        int N = sizeof(A) / sizeof(A[0]);
        check(A, N)? cout<<"YES": cout<<"NO";   
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of above approach.
    import java.util.Stack;

    class GFG {

    // Function to check if A[] is
    // Stack Sortable or Not.
        static boolean check(int A[], int N) {
            // Stack S
            Stack<Integer> S = new Stack<Integer>();

            // Pointer to the end value of array B.
            int B_end = 0;

            // Traversing each element of A[] from starting
            // Checking if there is a valid operation 
            // that can be performed.
            for (int i = 0; i < N; i++) {
                // If the stack is not empty
                if (!S.empty()) {
                    // Top of the Stack.
                    int top = S.peek();

                    // If the top of the stack is
                    // Equal to B_end+1, we will pop it
                    // And increment B_end by 1.
                    while (top == B_end + 1) {
                        // if current top is equal to
                        // B_end+1, we will increment 
                        // B_end to B_end+1
                        B_end = B_end + 1;

                        // Pop the top element.
                        S.pop();

                        // If the stack is empty We cannot
                        // further perfom this operation.
                        // Therefore break
                        if (S.empty()) {
                            break;
                        }

                        // Current Top
                        top = S.peek();
                    }

                    // If stack is empty
                    // Push the Current element
                    if (S.empty()) {
                        S.push(A[i]);
                    } else {
                        top = S.peek();

                        // If the Current element of the array A[]
                        // if smaller than the top of the stack
                        // We can push it in the Stack.
                        if (A[i] < top) {
                            S.push(A[i]);
                        } // Else We cannot sort the array
                        // Using any valid operations.
                        else {
                            // Not Stack Sortable
                            return false;
                        }
                    }
                } else {
                    // If the stack is empty push the current
                    // element in the stack.
                    S.push(A[i]);
                }
            }

            // Stack Sortable
            return true;
        }

    // Driver's Code
        public static void main(String[] args) {

            int A[] = {4, 1, 2, 3};
            int N = A.length;

            if (check(A, N)) {
                System.out.println("YES");
            } else {
                System.out.println("NO");
            }

        }
    }
    //This code is contributed by PrinciRaj1992
    ```

    **输出:**

    ```
    YES

    ```

    **时间复杂度** : O(N)。