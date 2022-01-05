# 能够获得所需口味冰淇淋的顾客数量

> 原文:[https://www . geeksforgeeks . org/能够获得所需口味冰淇淋的顾客数量/](https://www.geeksforgeeks.org/number-of-customers-able-to-get-desired-flavor-of-ice-cream/)

给定两种口味的冰淇淋巧克力和香草，分别用 **0** 和 **1** 表示。人们排队从一堆冰淇淋中挑选他们想要的口味。

*   如果排在队伍最前面的顾客更喜欢放在最上面的冰淇淋包，他们会拿着它离开队伍。
*   否则，他们会离开它，走到队列的尽头。

这个过程一直持续到队列中没有人想拿走最上面的冰淇淋包。

给定两个数组**顾客[]** 和**冰淇淋[]** ，其中**顾客[i]** 是顾客的偏好 **i** 第一个顾客(i =0 是队列的前面)**冰淇淋[i]** 表示堆叠中第一个冰淇淋的类型**I**(I = 0 是堆叠的顶部)。任务是找到能够得到他们想要的冰淇淋口味的顾客数量。

**示例:**

> **输入:**客户= {1，1，0，0}，冰淇淋= {0，1，0，1}
> **输出:** 4
> **说明:**以下是客户得到他们想要的口味冰淇淋的顺序。
> 前排顾客离开顶部冰淇淋包，移到队伍的最后。现在客户= {1，0，0，1}。
> 前面的顾客离开顶部的冰淇淋包，走向生产线的末端。现在客户= {0，0，1，1}。
> 前台顾客拿到冰淇淋后离开排队。现在冰淇淋= [1，0，1]和顾客= {0，1，1}。
> 前排顾客离开顶部冰淇淋包，移动到最后。现在客户= {1，1，0}。
> 前排顾客拿到冰淇淋包后离开队伍。现在冰淇淋= {0，1}和顾客= {1，0}。
> 前台客户离开队伍，走向终点。现在客户= {0，1}。
> 前顾客拿到冰淇淋包，离开排队。现在顾客= {1}和冰淇淋{1}。
> 前面顾客拿到冰激淋包，现在线空了。
> 因此，四位顾客都能得到想要冰淇淋包。
> 
> **输入:**客户= {1，1，1，0，0，1}，冰淇淋= {1，0，0，0，1，1}
> **输出:** 3

**进场 1:** 这个问题可以用[栈](https://www.geeksforgeeks.org/stack-data-structure/)和[队列](https://www.geeksforgeeks.org/queue-data-structure/)解决。按照以下步骤解决给定的问题。

*   创建一个**堆叠**，在**堆叠**中推送**冰淇淋【】**阵列。
*   创建一个**队列**，在**队列**中推送**客户[]** 数组
*   初始化一个变量，比如 **topRejected=0** 来跟踪被拒绝的元素。
*   如果**队列**的前面等于**堆栈**从**堆栈**中弹出顶级元素，并从**队列**中移除该元素，并更新 **topRejected=0** 。
*   否则，增加 topRejected 的计数，从队列的前面移除元素，最后添加。
*   如果队列大小等于 **topRejected** ，则中断循环。
*   打印**冰淇淋.长度**–**队列.大小**作为所需答案(因为队列中的剩余元素将无法获得所需的冰淇淋包)。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Java implementation of above approach*/

import java.io.*;
import java.util.*;
class GFG {
    public static void NumberOfCustomer(
        int[] customer, int[] icecream)
    {
        Stack<Integer> stack = new Stack<>();
        Queue<Integer> queue = new LinkedList<>();

        for (int i = icecream.length - 1; i >= 0; i--) {
            stack.push(icecream[i]);
        }

        for (int i = 0; i < customer.length; i++) {
            queue.add(customer[i]);
        }

        int topRejected = 0;

        while (true) {
            if (topRejected == queue.size())
                break;

            if (queue.peek() == stack.peek()) {
                queue.remove();
                stack.pop();
                topRejected = 0;
            }
            else {
                topRejected++;
                queue.add(queue.remove());
            }
        }

        System.out.println(
            icecream.length - queue.size());
    }

    public static void main(String[] args)
    {
        int customer[] = { 1, 1, 0, 0 };
        int icecream[] = { 0, 1, 0, 1 };
        NumberOfCustomer(customer, icecream);
    }
}
```

## C#

```
/*C# implementation of above approach*/
using System;
using System.Collections.Generic;

public class GFG {
    public static void NumberOfCustomer(
        int[] customer, int[] icecream)
    {
        Stack<int> stack = new Stack<int>();
        Queue<int> queue = new Queue<int>();

        for (int i = icecream.Length - 1; i >= 0; i--) {
            stack.Push(icecream[i]);
        }

        for (int i = 0; i < customer.Length; i++) {
            queue.Enqueue(customer[i]);
        }

        int topRejected = 0;

        while (true) {
            if (topRejected == queue.Count)
                break;

            if (queue.Peek() == stack.Peek()) {
                queue.Dequeue();
                stack.Pop();
                topRejected = 0;
            }
            else {
                topRejected++;
                queue.Enqueue(queue.Dequeue());
            }
        }

        Console.WriteLine(
            icecream.Length - queue.Count);
    }

    public static void Main(String[] args)
    {
        int[]customer = { 1, 1, 0, 0 };
        int[] icecream = { 0, 1, 0, 1 };
        NumberOfCustomer(customer, icecream);
    }
}

// This code is contributed by 29AjayKumar
```

**Output**

```
4
```

**时间复杂度:** O(N)

**辅助空间:** O(N)

**方法 2:** 上述方法可以进一步优化，避免额外的 O(N)空间。按照以下步骤解决给定的问题。

*   存储队列的顺序是没有用的。
*   声明一个数组，比如 **count[]** ，它将跟踪客户的偏好。
*   如果**客户【I】**为 **0** ，则增加**计数**，否则增加**计数【1】**。
*   现在，初始化 **k** ，它将存储获得所需冰淇淋包的顾客数量。
*   迭代通过冰淇淋阵列，并检查是否有人在左顾客将采取的食物。
*   最后打印 **k** 作为最终答案。

## C++

```
// c++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of customers who will
// get their desired flavor of ice cream
int NumberOfCustomer(int customer[], int icecream[], int n)
{

    // Count array stores the count
    // of preference of the customer
    int count[] = { 0, 0 };

    int k = 0;
    for (int a = 0; a < n; a++) {
        count[customer[a]]++;
    }

    for (k = 0; k < n && count[icecream[k]] > 0; ++k) {
        count[icecream[k]]--;
    }

    // Return k as the final answer
    return k;
}

int main()
{
    int customer[] = { 1, 1, 0, 0 };
    int icecream[] = { 0, 1, 0, 1 };
    int n = sizeof(customer) / sizeof(customer[0]);

    int ans = NumberOfCustomer(customer, icecream, n);

    // Print the final answer
    cout << (ans);
    return 0;
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;
class GFG {

    // Function to find the number
    // of customers who will
    // get their desired flavor of ice cream
    public static int NumberOfCustomer(
        int[] customer, int[] icecream)
    {

        // Count array stores the count
        // of preference of the customer
        int count[] = { 0, 0 };
        int n = customer.length;
        int k;
        for (int a : customer) {
            count[a]++;
        }

        for (k = 0;
             k < n && count[icecream[k]] > 0;
             ++k) {
            count[icecream[k]]--;
        }

        // Return k as the final answer
        return k;
    }

    public static void main(String[] args)
    {
        int customer[] = { 1, 1, 0, 0 };
        int icecream[] = { 0, 1, 0, 1 };

        int ans = NumberOfCustomer(
            customer, icecream);

        // Print the final answer
        System.out.print(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find the number
# of customers who will
# get their desired flavor of ice cream
def NumberOfCustomer(customer, icecream) :

    # Count array stores the count
    # of preference of the customer
    count = [ 0, 0 ];
    n = len(customer);

    for a in customer :
        count[a] += 1;

    k = 0
    while k < n and count[icecream[k]] > 0 :
        count[icecream[k]] -= 1;

        k += 1;

    # Return k as the final answer
    return k;

if __name__ == "__main__" :

    customer = [1, 1, 0, 0];
    icecream = [0, 1, 0, 1];
    ans = NumberOfCustomer(customer, icecream);

    print(ans);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for above approach
using System;
class GFG {

    // Function to find the number
    // of customers who will
    // get their desired flavor of ice cream
    public static int NumberOfCustomer( int[] customer, int[] icecream)
    {

        // Count array stores the count
        // of preference of the customer
        int[] count = { 0, 0 };
        int n = customer.Length;
        int k;
        foreach(int a in customer) {
            count[a]++;
        }

        for (k = 0;
             k < n && count[icecream[k]] > 0;
             ++k) {
            count[icecream[k]]--;
        }

        // Return k as the final answer
        return k;
    }

    public static void Main()
    {
        int[] customer = { 1, 1, 0, 0 };
        int[] icecream = { 0, 1, 0, 1 };

        int ans = NumberOfCustomer( customer, icecream);

        // Print the final answer
        Console.Write(ans);
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to find the number
// of customers who will
// get their desired flavor of ice cream
function NumberOfCustomer(customer, icecream)
{

  // Count array stores the count
  // of preference of the customer
  let count = [0, 0];
  let n = customer.length;
  let k;
  for (a of customer) {
    count[a]++;
  }

  for (k = 0; k < n && count[icecream[k]] > 0; ++k) {
    count[icecream[k]]--;
  }

  // Return k as the final answer
  return k;
}

let customer = [1, 1, 0, 0]
let icecream = [0, 1, 0, 1]

let ans = NumberOfCustomer(customer, icecream);

// Prlet the final answer
document.write(ans);

// This code is contributed by gfgking

</script>
```

**Output**

```
4
```

**时间复杂度:** O(N)

**辅助空间:** O(1)