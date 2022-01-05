# 检查堆栈或队列中的移动是否可能

> 原文:[https://www . geeksforgeeks . org/check-if-moves-in-a-stack-in-a-queue-is-on-or-not/](https://www.geeksforgeeks.org/check-if-moves-in-a-stack-or-queue-are-possible-or-not/)

给定一个二进制数组，其中 1 表示[推送](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)操作，0 表示[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)或[队列](https://www.geeksforgeeks.org/queue-data-structure/)中的[弹出](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)操作。任务是检查可能的操作集是否有效。
**举例:**

> **输入:** a[] = {1，1，0，0，1}
> **输出:**有效
> **输入:** a[] = {1，1，0，0，0}
> **输出:**无效
> 无法进行第三次弹出操作，因为堆栈或队列在该时刻将为空。

一种**天真的方法**是当数组元素为 1 时使用堆栈或队列并执行推送操作，当数组元素为 0 时执行弹出操作。当要执行弹出操作时，如果堆栈或队列为空，则移动无效。如果我们能完成所有的操作，那么这些动作就是有效的。
**时间复杂度** : O(N)
**辅助空间** : O(N)
一种**高效的方法**将对推送操作进行计数，并在执行 pop 操作时减少它们。如果在任何实例中，计数小于 0，则这组操作无效。
以下是上述办法的实施情况。

## C++

```
// C++ program to Check if moves in a stack
// or queue are possible or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// operations are valid or not
bool check(int a[], int n)
{

    // count number of push operations
    int ones = 0;

    // traverse in the array
    for (int i = 0; i < n; i++) {

        // push operation
        if (a[i])
            ones++;

        // pop operation
        else
            ones--;

        // if at any moment pop() operations
        // exceeds the number of push operations
        if (ones < 0)
            return false;
    }

    return true;
}

// Driver Code
int main()
{
    int a[] = { 1, 1, 0, 0, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    if (check(a, n))
        cout << "Valid";
    else
        cout << "Invalid";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if moves in a stack
// or queue are possible or not

public class GFG {

// Function to check if
// operations are valid or not
    static boolean check(int a[], int n) {

        // count number of push operations
        int ones = 0;

        // traverse in the array
        for (int i = 0; i < n; i++) {

            // push operation
            if (a[i] ==1) {
                ones++;
            } // pop operation
            else {
                ones--;
            }

            // if at any moment pop() operations
            // exceeds the number of push operations
            if (ones < 0) {
                return false;
            }
        }

        return true;
    }

// Driver Code
    static public void main(String[] args) {
        int a[] = {1, 1, 0, 0, 1};
        int n = a.length;
        if (check(a, n)) {
            System.out.println("Valid");
        } else {
            System.out.println("Invalid");
        }

    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to Check if moves
# in a stack or queue are possible or not

# Function to check if
# operations are valid or not
def check(a, n):

    # count number of push operations
    ones = 0;

    # traverse in the array
    for i in range (0, n):

        # push operation
        if (a[i]):
            ones = ones + 1;

        # pop operation
        else:
            ones = ones - 1;

        # if at any moment pop() operations
        # exceeds the number of push operations
        if (ones < 0):
            return False;

    return True;

# Driver Code
a = [ 1, 1, 0, 0, 1 ];
n = len(a);
if (check(a, n)):
    print("Valid");
else:
    print("Invalid");

# This code is contributed
# by Akanksha Rai
```

## C#

```
using System;

// C# program to Check if moves in a stack
// or queue are possible or not

public class GFG {

// Function to check if
// operations are valid or not
    static bool check(int []a, int n) {

        // count number of push operations
        int ones = 0;

        // traverse in the array
        for (int i = 0; i < n; i++) {

            // push operation
            if (a[i] ==1) {
                ones++;
            } // pop operation
            else {
                ones--;
            }

            // if at any moment pop() operations
            // exceeds the number of push operations
            if (ones < 0) {
                return false;
            }
        }

        return true;
    }

// Driver Code
    static public void Main() {
        int []a = {1, 1, 0, 0, 1};
        int n = a.Length;
        if (check(a, n)) {
            Console.Write("Valid");
        } else {
            Console.Write("Invalid");
        }

    }
}
// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Check if moves in a
// stack or queue are possible or not

// Function to check if
// operations are valid or not
function check($a, $n)
{

    // count number of push operations
    $ones = 0;

    // traverse in the array
    for ($i = 0; $i < $n; $i++)
    {

        // push operation
        if ($a[$i])
            $ones++;

        // pop operation
        else
            $ones--;

        // if at any moment pop() operations
        // exceeds the number of push operations
        if ($ones < 0)
            return false;
    }

    return true;
}

// Driver Code
$a = array( 1, 1, 0, 0, 1 );
$n = count($a);
if (check($a, $n))
    echo "Valid";
else
    echo "Invalid";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript program to Check if moves in a stack
// or queue are possible or not

    // Function to check if
    // operations are valid or not
    function check(a , n) {

        // count number of push operations
        var ones = 0;

        // traverse in the array
        for (i = 0; i < n; i++) {

            // push operation
            if (a[i] == 1) {
                ones++;
            } // pop operation
            else {
                ones--;
            }

            // if at any moment pop() operations
            // exceeds the number of push operations
            if (ones < 0) {
                return false;
            }
        }

        return true;
    }

    // Driver Code
        var a = [ 1, 1, 0, 0, 1 ];
        var n = a.length;
        if (check(a, n)) {
            document.write("Valid");
        } else {
            document.write("Invalid");
        }

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
Valid
```

**时间复杂度**:O(N)
T3】辅助空间 : O(1)