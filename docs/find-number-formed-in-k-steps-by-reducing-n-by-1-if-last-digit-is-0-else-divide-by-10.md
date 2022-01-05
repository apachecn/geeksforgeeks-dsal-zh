# 如果最后一位数字为 0，则通过将 N 减 1 找到 K 步形成的数字，否则除以 10

> 原文:[https://www . geeksforgeeks . org/find-number-formed-in-k-steps-by-n-by-1-如果最后一位数字为 0-else-divide-10/](https://www.geeksforgeeks.org/find-number-formed-in-k-steps-by-reducing-n-by-1-if-last-digit-is-0-else-divide-by-10/)

给定两个整数 **N** 和 **K** 。在 **N** 上执行以下类型的操作:

*   如果 **N** 的最后一位数字不为零，则减一。
*   如果 **N** 的最后一位数字为零，则用 **10** 除该数字(即去掉最后一位数字)。

任务是在 **K** 这样的操作后打印结果。

**示例:**

> **输入** : N = 512，K = 4
> **输出** : 50
> **说明:**以下是为了得到想要的结果而进行的 K 次操作。
> 操作 1:N 的最后一位数字，即 **2！= 0** 。n 减 1。(N = 512–1**即 **511** )。
> 操作 2:N 的最后一位，即 **1！= 0.** N 减 1。(N = 511–1，即**510** )。
> 操作 3:N 的最后一位为 0。n 除以 10。(N = 510/10，即 **51** )。
> 操作 4:N 的最后一位数字即 2！= 0.n 减 1。(N = 51–1，即 **50** )。
> 因此，4 次手术后 N = 50。**
> 
>  ****输入** : N = 100，K = 2
> **输出** : 1
> **说明:** N 除以 10 两次。**

****方法:**这个问题是基于实现的，类似于数字的最后一位[。按照以下步骤解决给定的问题。](https://www.geeksforgeeks.org/find-first-last-digits-number/)**

*   **重复检查整数 **N** 的最后一位数字。**
*   **如果**最后一位数字**是 **0** ，用 **10** 除 **N** 。**
*   **如果**最后一位数字**是**不是 0** ，则从 **N** 中减去 **1** 。**
*   **重复以上步骤 **K** 次。**

**下面是上述方法的实现。**

## **C++**

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform operations K times
int decreaseNum(int N, int K)
{
    while (K--) {
        // Last digit is 0
        if (N % 10 == 0)
            N /= 10;

        // Last digit is not 0
        else
            N--;
    }
    return N;
}

// Driver Code
int main()
{
    // Declaration and initialisation
    int N, K;
    N = 512;
    K = 4;

    // Function call
    cout << decreaseNum(N, K);

    return 0;
}
```

## **java 描述语言**

```
  <script>
      // JavaScript code for the above approach

      // Function to perform operations K times
      function decreaseNum(N, K)
      {
          while (K--)
          {

              // Last digit is 0
              if (N % 10 == 0)
                  N /= 10;

              // Last digit is not 0
              else
                  N--;
          }
          return N;
      }

      // Driver Code

      // Declaration and initialisation
      let N, K;
      N = 512;
      K = 4;

      // Function call
      document.write(decreaseNum(N, K));

// This code is contributed by Potta Lokesh
  </script>
```

****Output**

```
50
```** 

*****时间复杂度:*** O(K)
***辅助空间:*** O(1)**