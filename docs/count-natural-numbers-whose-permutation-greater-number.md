# 计算所有排列都大于该数的自然数

> 原文:[https://www . geeksforgeeks . org/count-自然数-谁的-排列-更大-数/](https://www.geeksforgeeks.org/count-natural-numbers-whose-permutation-greater-number/)

有些自然数所有置换都大于或等于该数，例如 123，其所有置换(123，231，321)都大于或等于 123。
给定一个自然数 **n** ，任务是将所有这样的数从 1 数到 n

**示例:**

> **输入:** n = 15。
> **输出:** 14
> **说明:**
> 1、2、3、4、5、6、7、8、9、11、12、
> 13、14、15 是所有
> 排列大于数字
> 本身的数字。输出 14。
> 
> **输入:** n = 100。
> T3【输出: 54

一个**简单的解决方案**是运行一个从 1 到 n 的循环，并且对于每个数字检查它的数字是否按非递减顺序。

一个**有效的解决方案**是基于下面的观察。
观察 1:从 1 到 9，所有数字都有这个性质。所以，对于 n < = 9，输出 n.
观察 2:所有排列大于或等于该数的数，其所有数字的顺序递增。
想法是把所有的数字从 1 推到 9。现在，弹出顶部元素，说 **topel** ，试着做一个数字，数字的位数是递增的，第一个数字是 **topel** 。要做这样的数字，第二个数字可以是从**到 10** 到 9。如果该数字小于 **n** ，则递增计数并推入堆栈中的数字，否则忽略。

下面是该方法的实现:

## C++

```
// C++ program to count the number less than N,
// whose all permutation is greater
// than or equal to the number.
#include <bits/stdc++.h>
using namespace std;

// Return the count of the number having all
// permutation greater than or equal to the number.
int countNumber(int n)
{
    int result = 0;

    // Pushing 1 to 9 because all number from 1
    // to 9 have this property.
    stack<int> s;
    for (int i = 1; i <= 9; i++)
    {

        if (i <= n)
        {
            s.push(i);
            result++;
        }

        // take a number from stack and add
        // a digit smaller than or equal to last digit
        // of it.
        while (!s.empty())
        {
            int tp = s.top();
            s.pop();
            for (int j = tp % 10; j <= 9; j++)
            {
                int x = tp * 10 + j;
                if (x <= n)
                {
                    s.push(x);
                    result++;
                }
            }
        }
    }

    return result;
}

// Driven Code
int main()
{
    int n = 15;
    cout << countNumber(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number less than N,
// whose all permutation is greater
// than or equal to the number.
import java.util.Stack;

class GFG
{
    // Return the count of the number having all
    // permutation greater than or equal to the number.

    static int countNumber(int n)
    {
        int result = 0;

        // Pushing 1 to 9 because all number from 1
        // to 9 have this property.
        Stack<Integer> s = new Stack<>();
        for (int i = 1; i <= 9; i++)
        {

            if (i <= n)
            {
                s.push(i);
                result++;
            }

            // take a number from stack and add
            // a digit smaller than or equal to last digit
            // of it.
            while (!s.empty())
            {
                int tp = s.pop();

                for (int j = tp % 10; j <= 9; j++)
                {
                    int x = tp * 10 + j;
                    if (x <= n) {
                        s.push(x);
                        result++;
                    }
                }
            }
        }

        return result;
    }

    // Driven Code
    public static void main(String[] args)
    {
        int n = 15;
        System.out.println(countNumber(n));
    }
}

// this code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count the number less
# than N, whose all permutation is greater
# than or equal to the number.

# Return the count of the number having
# all permutation greater than or equal
# to the number.

def countNumber(n):
    result = 0

    # Pushing 1 to 9 because all number
    # from 1 to 9 have this property.
    s = []
    for i in range(1, 10):

        if (i <= n):
            s.append(i)
            result += 1

        # take a number from stack and add
        # a digit smaller than or equal to last digit
        # of it.
        while len(s) != 0:
            tp = s[-1]
            s.pop()
            for j in range(tp % 10, 10):
                x = tp * 10 + j
                if (x <= n):
                    s.append(x)
                    result += 1

    return result

# Driver Code
if __name__ == '__main__':

    n = 15
    print(countNumber(n))

# This code is contributed by PranchalK
```

## C#

```
// C# program to count the number less than N,
// whose all permutation is greater than
// or equal to the number.
using System;
using System.Collections.Generic;

class GFG {

    // Return the count of the number
    // having all permutation greater than
    // or equal to the number.
    static int countNumber(int n)
    {
        int result = 0;

        // Pushing 1 to 9 because all number from 1
        // to 9 have this property.
        Stack<int> s = new Stack<int>();
        for (int i = 1; i <= 9; i++)
        {

            if (i <= n)
            {
                s.Push(i);
                result++;
            }

            // take a number from stack and add
            // a digit smaller than or equal to last digit
            // of it.
            while (s.Count != 0)
            {
                int tp = s.Peek();
                s.Pop();
                for (int j = tp % 10; j <= 9; j++)
                {
                    int x = tp * 10 + j;
                    if (x <= n) {
                        s.Push(x);
                        result++;
                    }
                }
            }
        }

        return result;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 15;
        Console.WriteLine(countNumber(n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
  <script>

        // JavaScript program for the above approach

        // Return the count of the number having all
        // permutation greater than or equal to the number.
        function countNumber(n)
        {
            let result = 0;

            // Pushing 1 to 9 because all number from 1
            // to 9 have this property.
            let s = [];
            for (let i = 1; i <= 9; i++)
            {

                if (i <= n)
                {
                    s.push(i);
                    result++;
                }

                // take a number from stack and add
                // a digit smaller than or equal to last digit
                // of it.
                while (s.length != 0)
                {
                    let tp = s[s.length - 1];
                    s.pop();
                    for (let j = tp % 10; j <= 9; j++)
                    {
                        let x = tp * 10 + j;
                        if (x <= n)
                        {
                            s.push(x);
                            result++;
                        }
                    }
                }
            }

            return result;
        }

        // Driven Code

        let n = 15;
        document.write(countNumber(n));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
14
```

**时间复杂度:** O(x)，其中 x 是输出中打印的元素数量。

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。