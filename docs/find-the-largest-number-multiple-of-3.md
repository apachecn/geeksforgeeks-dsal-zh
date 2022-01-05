# 求 3 的最大倍数|集合 1(使用队列)

> 原文:[https://www . geesforgeks . org/find-最大数倍数 3/](https://www.geeksforgeeks.org/find-the-largest-number-multiple-of-3/)

给定一个非负整数数组。找出由数组元素组成的 3 的最大倍数。
例如，如果输入数组是{8，1，9}，输出应该是“9 8 1”，如果输入数组是{8，1，7，6，0}，输出应该是“8 7 6 0”。
**方法 1(蛮力)**
简单的&直接方法是生成元素的所有组合，并跟踪形成的可被 3 整除的最大数。
时间复杂度:o(n×2^n).)将会有阵列元素的 2^n 组合。将每个组合与迄今为止最大的数字进行比较可能需要 O(n)个时间。
辅助空间:O(n) //为避免整数溢出，假设最大数以数组形式存储。
**方法 2(棘手)**
这个问题可以借助 O(n)个额外空间高效解决。这种方法基于以下关于 3 的倍数的事实。
**1)** 数是 3 的倍数当且仅当数的位数之和是 3 的倍数。比如我们考虑 8760，它是 3 的倍数，因为位数之和是 8 + 7+ 6+ 0 = 21，是 3 的倍数。
**2)** 如果一个数是 3 的倍数，那么它的所有排列也是 3 的倍数。例如，因为 6078 是 3 的倍数，所以数字 8760，7608，7068，…..也是 3 的倍数。
**3)** 我们把数和数的位数和除，得到同样的余数。例如，如果将数字 151 除以数字 7，再除以 3，我们得到相同的余数 1。
*上述事实背后的想法是什么？*
10% 3 和 100%3 的值为 1。所有 10 的高次幂也是如此，因为 3 除 9，99，999，…等等。
让我们考虑一个 3 位数 n 来证明上述事实。设 n 的第一、二、三位数字分别为“a”、“b”和“c”。n 可以写成

```
n = 100.a + 10.b + c 
```

因为(对于任何 x，10^x)%3 都是 1，所以上面的表达式给出了与下面的表达式相同的余数

```
 1.a + 1.b + c 
```

所以数字和“n”的和得到的余数是一样的。
以下是基于上述观察的解决方案。
**1。**按非递减顺序排列数组。
**2。**走三个队列。一个用于存储被 3 除后余数为 0 的元素。第二个队列存储的数字除以 3 得到的余数为 1。第三个队列存储的数字除以 3 得到的余数为 2。称它们为队列 0、队列 1 和队列 2
**3。**求所有数字的和。
**4。**出现三种情况:
…… **4.1** 位数之和可被 3 整除。将三个队列中的所有数字出列。按非递增顺序排序。输出数组。
…… **4.2** 数字之和除以 3 后得出余数 1。
从队列 1 中删除一个项目。如果队列 1 为空，请从队列 2 中删除两个项目。如果 queue2 包含的项目少于两个，则该数量是不可能的。
…… **4.3** 数字之和除以 3 后得出余数 2。
从队列 2 中删除一个项目。如果队列 2 为空，请从队列 1 中删除两个项目。如果 queue1 包含的项目少于两个，则该数量是不可能的。
**5。**最后把所有队列清空成一个辅助数组。按非递增顺序对辅助数组进行排序。输出辅助数组。
**以下代码仅在输入数组的数字范围为 0 到 9 时有效。它可以很容易地扩展到任何正整数数组。我们只需要在代码末尾修改我们按降序排列数组的部分。**

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// This function puts all elements of 3 queues in the auxiliary array
void populateAux(int aux[], queue<int> queue0, queue<int> queue1,
                 queue<int> queue2, int* top)
{
    // Put all items of first queue in aux[]
    while (!queue0.empty()) {
        aux[(*top)++] = queue0.front();
        queue0.pop();
    }

    // Put all items of second queue in aux[]
    while (!queue1.empty()) {
        aux[(*top)++] = queue1.front();
        queue1.pop();
    }

    // Put all items of third queue in aux[]
    while (!queue2.empty()) {
        aux[(*top)++] = queue2.front();
        queue2.pop();
    }
}

// The main function that finds the largest possible multiple of
// 3 that can be formed by arr[] elements
int findMaxMultupleOf3(int arr[], int size)
{
    // Step 1: sort the array in non-decreasing order
    sort(arr, arr + size);

    // Create 3 queues to store numbers with remainder 0, 1
    // and 2 respectively
    queue<int> queue0, queue1, queue2;

    // Step 2 and 3 get the sum of numbers and place them in
    // corresponding queues
    int i, sum;
    for (i = 0, sum = 0; i < size; ++i) {
        sum += arr[i];
        if ((arr[i] % 3) == 0)
            queue0.push(arr[i]);
        else if ((arr[i] % 3) == 1)
            queue1.push(arr[i]);
        else
            queue2.push(arr[i]);
    }

    // Step 4.2: The sum produces remainder 1
    if ((sum % 3) == 1) {
        // either remove one item from queue1
        if (!queue1.empty())
            queue1.pop();

        // or remove two items from queue2
        else {
            if (!queue2.empty())
                queue2.pop();
            else
                return 0;

            if (!queue2.empty())
                queue2.pop();
            else
                return 0;
        }
    }

    // Step 4.3: The sum produces remainder 2
    else if ((sum % 3) == 2) {
        // either remove one item from queue2
        if (!queue2.empty())
            queue2.pop();

        // or remove two items from queue1
        else {
            if (!queue1.empty())
                queue1.pop();
            else
                return 0;

            if (!queue1.empty())
                queue1.pop();
            else
                return 0;
        }
    }

    int aux[size], top = 0;

    // Empty all the queues into an auxiliary array.
    populateAux(aux, queue0, queue1, queue2, &top);

    // sort the array in non-increasing order
    sort(aux, aux + top, greater<int>());

    // print the result
    for (int i = 0; i < top; ++i)
        cout << aux[i] << " ";

    return top;
}
int main()
{

    int arr[] = { 8, 1, 7, 6, 0 };
    int size = sizeof(arr) / sizeof(arr[0]);

    if (findMaxMultupleOf3(arr, size) == 0)
        cout << "Not Possible";

    return 0;
}
```

## C

```
/* A program to find the largest multiple of 3 from an array of elements */
#include <stdio.h>
#include <stdlib.h>

// A queue node
typedef struct Queue {
    int front;
    int rear;
    int capacity;
    int* array;
} Queue;

// A utility function to create a queue with given capacity
Queue* createQueue(int capacity)
{
    Queue* queue = (Queue*)malloc(sizeof(Queue));
    queue->capacity = capacity;
    queue->front = queue->rear = -1;
    queue->array = (int*)malloc(queue->capacity * sizeof(int));
    return queue;
}

// A utility function to check if queue is empty
int isEmpty(Queue* queue)
{
    return queue->front == -1;
}

// A function to add an item to queue
void Enqueue(Queue* queue, int item)
{
    queue->array[++queue->rear] = item;
    if (isEmpty(queue))
        ++queue->front;
}

// A function to remove an item from queue
int Dequeue(Queue* queue)
{
    int item = queue->array[queue->front];
    if (queue->front == queue->rear)
        queue->front = queue->rear = -1;
    else
        queue->front++;

    return item;
}

// A utility function to print array contents
void printArr(int* arr, int size)
{
    int i;
    for (i = 0; i < size; ++i)
        printf("%d ", arr[i]);
}

/* Following two functions are needed for library function qsort().
   Refer following link for help of qsort()
   http:// www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
int compareAsc(const void* a, const void* b)
{
    return *(int*)a > *(int*)b;
}
int compareDesc(const void* a, const void* b)
{
    return *(int*)a < *(int*)b;
}

// This function puts all elements of 3 queues in the auxiliary array
void populateAux(int* aux, Queue* queue0, Queue* queue1,
                 Queue* queue2, int* top)
{
    // Put all items of first queue in aux[]
    while (!isEmpty(queue0))
        aux[(*top)++] = Dequeue(queue0);

    // Put all items of second queue in aux[]
    while (!isEmpty(queue1))
        aux[(*top)++] = Dequeue(queue1);

    // Put all items of third queue in aux[]
    while (!isEmpty(queue2))
        aux[(*top)++] = Dequeue(queue2);
}

// The main function that finds the largest possible multiple of
// 3 that can be formed by arr[] elements
int findMaxMultupleOf3(int* arr, int size)
{
    // Step 1: sort the array in non-decreasing order
    qsort(arr, size, sizeof(int), compareAsc);

    // Create 3 queues to store numbers with remainder 0, 1
    // and 2 respectively
    Queue* queue0 = createQueue(size);
    Queue* queue1 = createQueue(size);
    Queue* queue2 = createQueue(size);

    // Step 2 and 3 get the sum of numbers and place them in
    // corresponding queues
    int i, sum;
    for (i = 0, sum = 0; i < size; ++i) {
        sum += arr[i];
        if ((arr[i] % 3) == 0)
            Enqueue(queue0, arr[i]);
        else if ((arr[i] % 3) == 1)
            Enqueue(queue1, arr[i]);
        else
            Enqueue(queue2, arr[i]);
    }

    // Step 4.2: The sum produces remainder 1
    if ((sum % 3) == 1) {
        // either remove one item from queue1
        if (!isEmpty(queue1))
            Dequeue(queue1);

        // or remove two items from queue2
        else {
            if (!isEmpty(queue2))
                Dequeue(queue2);
            else
                return 0;

            if (!isEmpty(queue2))
                Dequeue(queue2);
            else
                return 0;
        }
    }

    // Step 4.3: The sum produces remainder 2
    else if ((sum % 3) == 2) {
        // either remove one item from queue2
        if (!isEmpty(queue2))
            Dequeue(queue2);

        // or remove two items from queue1
        else {
            if (!isEmpty(queue1))
                Dequeue(queue1);
            else
                return 0;

            if (!isEmpty(queue1))
                Dequeue(queue1);
            else
                return 0;
        }
    }

    int aux[size], top = 0;

    // Empty all the queues into an auxiliary array.
    populateAux(aux, queue0, queue1, queue2, &top);

    // sort the array in non-increasing order
    qsort(aux, top, sizeof(int), compareDesc);

    // print the result
    printArr(aux, top);

    return top;
}

// Driver program to test above functions
int main()
{
    int arr[] = { 8, 1, 7, 6, 0 };
    int size = sizeof(arr) / sizeof(arr[0]);

    if (findMaxMultupleOf3(arr, size) == 0)
        printf("Not Possible");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find the largest multiple
of 3 that can be formed from an array
of elements */
import java.util.Arrays;
import java.util.Queue;
import java.util.LinkedList;
import java.util.Collections;

public class Geeks {

    // This function puts all elements of 3 queues in the
    // array auxiliary
    public static int populateAux(int aux[], Queue<Integer> queue0,
                        Queue<Integer> queue1, Queue<Integer> queue2)
    {
        int top=0;
        // Put all items of first queue in aux[]
        while(!queue0.isEmpty())
        {
            aux[top++]=queue0.remove();
        }

        // Put all items of second queue in aux[]
        while(!queue1.isEmpty())
        {
            aux[top++]=queue1.remove();
        }

        // Put all items of third queue in aux[]
        while(!queue2.isEmpty())
        {
            aux[top++]=queue2.remove();
        }

        //Return number of integer added to aux[]
        return top;
    }

    // The main function that finds the largest possible multiple of
    // 3 that can be formed by arr[] elements
    public static boolean findMaxMultupleOf3(int arr[])
    {
        // Step 1: sort the array in non-decreasing order
        Arrays.sort(arr);

        // Create 3 queues to store numbers with remainder 0, 1
        // and 2 respectively
        Queue<Integer> queue0=new LinkedList<>();
        Queue<Integer> queue1=new LinkedList<>();
        Queue<Integer> queue2=new LinkedList<>();

        // Step 2 and 3 get the sum of numbers and place them in
        // corresponding queues
        int sum=0;
        for (int i = 0; i < arr.length; ++i)
        {
            sum += arr[i];
            if ((arr[i] % 3) == 0)
                queue0.add(arr[i]);
            else if ((arr[i] % 3) == 1)
                queue1.add(arr[i]);
            else
                queue2.add(arr[i]);
        }

        // Step 4.2: The sum produces remainder 1
        if ((sum % 3) == 1)
        {
            // either remove one item from queue1
            if (!queue1.isEmpty())
                queue1.remove();

            // or remove two items from queue2
            else
            {
                if (!queue2.isEmpty())
                    queue2.remove();
                else
                    return false;

                if (!queue2.isEmpty())
                    queue2.remove();
                else
                    return false;
            }
        }
        // Step 4.3: The sum produces remainder 2
        else if ((sum % 3) == 2)
        {
            // either remove one item from queue2
            if (!queue2.isEmpty())
                queue2.remove();
            // or remove two items from queue1
            else
            {
                if (!queue1.isEmpty())
                    queue1.remove();
                else
                    return false;

                if (!queue1.isEmpty())
                    queue1.remove();
                else
                    return false;
            }
        }

        int aux[]=new int[arr.length];
        // Empty all the queues into an auxiliary array
        // and get the number of integers added to aux[]
        int top=populateAux(aux,queue0,queue1,queue2);

        // sort the array in non-increasing order
        Arrays.sort(aux,0,top);

        // print the result
        for (int i = top-1; i>=0; i--)
            System.out.print(aux[i]+" ") ;

        return true;
    }

    public static void main(String args[])
    {
        int arr[] = { 8, 1, 7, 6, 0 };
        if (!findMaxMultupleOf3(arr))
        System.out.println("Not possible") ;
    }
}

// This code is contributed by Gaurav Tiwari
```

## C#

```
/* C# program to find the largest multiple
of 3 that can be formed from an array
of elements */
using System;
using System.Collections.Generic;

class Geeks
{

    // This function puts all elements of 3 queues in the
    // array auxiliary
    public static int populateAux(int []aux, Queue<int> queue0,
                        Queue<int> queue1, Queue<int> queue2)
    {
        int top = 0;
        // Put all items of first queue in aux[]
        while(queue0.Count != 0)
        {
            aux[top++] = queue0.Dequeue();
        }

        // Put all items of second queue in aux[]
        while(queue1.Count != 0)
        {
            aux[top++] = queue1.Dequeue();
        }

        // Put all items of third queue in aux[]
        while(queue2.Count != 0)
        {
            aux[top++] = queue2.Dequeue();
        }

        //Return number of integer added to aux[]
        return top;
    }

    // The main function that finds the largest possible multiple of
    // 3 that can be formed by arr[] elements
    public static bool findMaxMultupleOf3(int []arr)
    {
        // Step 1: sort the array in non-decreasing order
        Array.Sort(arr);

        // Create 3 queues to store numbers with remainder 0, 1
        // and 2 respectively
        Queue<int> queue0 = new Queue<int>();
        Queue<int> queue1 = new Queue<int>();
        Queue<int> queue2 = new Queue<int>();

        // Step 2 and 3 get the sum of numbers and place them in
        // corresponding queues
        int sum=0;
        for (int i = 0; i < arr.Length; ++i)
        {
            sum += arr[i];
            if ((arr[i] % 3) == 0)
                queue0.Enqueue(arr[i]);
            else if ((arr[i] % 3) == 1)
                queue1.Enqueue(arr[i]);
            else
                queue2.Enqueue(arr[i]);
        }

        // Step 4.2: The sum produces remainder 1
        if ((sum % 3) == 1)
        {
            // either remove one item from queue1
            if (queue1.Count != 0)
                queue1.Dequeue();

            // or remove two items from queue2
            else
            {
                if (queue2.Count != 0)
                    queue2.Dequeue();
                else
                    return false;

                if (queue2.Count != 0)
                    queue2.Dequeue();
                else
                    return false;
            }
        }
        // Step 4.3: The sum produces remainder 2
        else if ((sum % 3) == 2)
        {
            // either remove one item from queue2
            if (queue2.Count != 0)
                queue2.Dequeue();
            // or remove two items from queue1
            else
            {
                if (queue1.Count != 0)
                    queue1.Dequeue();
                else
                    return false;

                if (queue1.Count != 0)
                    queue1.Dequeue();
                else
                    return false;
            }
        }

        int []aux = new int[arr.Length];

        // Empty all the queues into an auxiliary array
        // and get the number of integers added to aux[]
        int top = populateAux(aux,queue0,queue1,queue2);

        // sort the array in non-increasing order
        Array.Sort(aux,0,top);

        // print the result
        for (int i = top-1; i >= 0; i--)
            Console.Write(aux[i]+" ") ;

        return true;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 8, 1, 7, 6, 0 };
        if (!findMaxMultupleOf3(arr))
        Console.WriteLine("Not possible") ;
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

/* Javascript program to find the largest multiple
of 3 that can be formed from an array
of elements */

// This function puts all elements of 3 queues in the
    // array auxiliary
function populateAux(aux, queue0, queue1, queue2)
{
    let top = 0;

        // Put all items of first queue in aux[]
        while(queue0.length != 0)
        {
            aux[top++] = queue0.shift();
        }

        // Put all items of second queue in aux[]
        while(queue1.length != 0)
        {
            aux[top++] = queue1.shift();
        }

        // Put all items of third queue in aux[]
        while(queue2.length != 0)
        {
            aux[top++] = queue2.shift();
        }

        //Return number of integer added to aux[]
        return top;
}

// The main function that finds the largest possible multiple of
    // 3 that can be formed by arr[] elements
function findMaxMultupleOf3(arr)
{
    // Step 1: sort the array in non-decreasing order
        arr.sort(function(a, b){return a - b;});

        // Create 3 queues to store numbers with remainder 0, 1
        // and 2 respectively
        let queue0 = [];
        let queue1 = [];
        let queue2 = [];

        // Step 2 and 3 get the sum of numbers and place them in
        // corresponding queues
        let sum = 0;
        for (let i = 0; i < arr.length; ++i)
        {
            sum += arr[i];
            if ((arr[i] % 3) == 0)
                queue0.push(arr[i]);
            else if ((arr[i] % 3) == 1)
                queue1.push(arr[i]);
            else
                queue2.push(arr[i]);
        }

        // Step 4.2: The sum produces remainder 1
        if ((sum % 3) == 1)
        {
            // either remove one item from queue1
            if (queue1.length != 0)
                queue1.shift();

            // or remove two items from queue2
            else
            {
                if (queue2.length != 0)
                    queue2.shift();
                else
                    return false;

                if (queue2.length != 0)
                    queue2.shift();
                else
                    return false;
            }
        }
        // Step 4.3: The sum produces remainder 2
        else if ((sum % 3) == 2)
        {
            // either remove one item from queue2
            if (queue2.length != 0)
                queue2.shift();
            // or remove two items from queue1
            else
            {
                if (queue1.length != 0)
                    queue1.shift();
                else
                    return false;

                if (queue1.length != 0)
                    queue1.shift();
                else
                    return false;
            }
        }

        let aux=new Array(arr.length);
        // Empty all the queues into an auxiliary array
        // and get the number of integers added to aux[]
        let top=populateAux(aux, queue0, queue1, queue2);

        // sort the array in non-increasing order
        aux.sort(function(a, b){return a - b;});

        // print the result
        for (let i = top - 1; i >= 0; i--)
            document.write(aux[i]+" ") ;

        return true;
}

// Driver code
let arr = [ 8, 1, 7, 6, 0 ];
if (!findMaxMultupleOf3(arr))
        document.write("Not possible") ;

// This code is contributed by rag2127.
</script>
```

**Output:** 

```
8 7 6 0
```

上述方法可以通过以下方式进行优化。
1)我们可以使用堆排序或合并排序来使时间复杂度为 O(nLogn)。
2)我们可以避免额外的排队空间。我们知道最多有两个项目将从输入数组中移除。所以我们可以跟踪两个变量中的两个项目。
3)最后，不用再按降序对数组进行排序，我们可以反过来打印升序排序的数组。以相反的顺序打印时，我们可以跳过要删除的两个元素。
时间复杂度:O(nLogn)，假设使用 O(nLogn)算法进行排序。
[**找到 3 的最大倍数|集合 2 (In O(n)时间和 O(1)空间)**](https://www.geeksforgeeks.org/find-largest-multiple-3-array-digits-set-2-time-o1-space/)
如果发现有不正确的地方，或者想分享更多关于以上讨论话题的信息，请写评论。