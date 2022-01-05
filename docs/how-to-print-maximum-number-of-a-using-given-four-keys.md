# 如何使用给定的四个键

打印最大数量的 A

> 原文:[https://www . geeksforgeeks . org/如何使用给定的四键打印最大数量/](https://www.geeksforgeeks.org/how-to-print-maximum-number-of-a-using-given-four-keys/)

这是在[谷歌](http://www.careercup.com/question?id=7184083)[Paytm](https://www.geeksforgeeks.org/one97paytm-interview-experience/)等很多公司面试中问的一个著名的面试问题。
下面是问题陈述。

```
Imagine you have a special keyboard with the following keys: 
Key 1:  Prints 'A' on screen
Key 2: (Ctrl-A): Select screen
Key 3: (Ctrl-C): Copy selection to buffer
Key 4: (Ctrl-V): Print buffer on screen appending it
                 after what has already been printed. 

If you can only press the keyboard for N times (with the above four
keys), write a program to produce maximum numbers of A's. That is to
say, the input parameter is N (No. of keys that you can press), the 
output is M (No. of As that you can produce).
```

**示例:**

```
Input:  N = 3
Output: 3
We can at most get 3 A's on screen by pressing 
following key sequence.
A, A, A

Input:  N = 7
Output: 9
We can at most get 9 A's on screen by pressing 
following key sequence.
A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V

Input:  N = 11
Output: 27
We can at most get 27 A's on screen by pressing 
following key sequence.
A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V, Ctrl A, 
Ctrl C, Ctrl V, Ctrl V
```

以下是几个需要注意的要点。
a)对于 N < 7，输出为 N 本身。
b) Ctrl V 可以多次使用，打印当前缓冲区(见上面最后两个例子)。这个想法是通过一个简单的洞察来计算 N 次击键的最佳字符串长度。产生最佳字符串长度的 N 次击键的序列将以一个 Ctrl-A 后缀结束，一个 Ctrl-C 后缀，后面只有 Ctrl-V 后缀。(对于 N > 6)
任务是找出 break =点，之后我们得到上面的击键后缀。断点的定义是这样一种情况，在这种情况之后，我们只需要按一次 Ctrl-A、Ctrl-C，然后再按一次 Ctrl-V 就可以生成最佳长度。如果我们从 N-3 循环到 1，选择这些值中的每一个作为断点，并计算它们将产生的最佳字符串。一旦循环结束，我们将拥有各种断点的最佳长度的最大值，从而为我们提供 N 次击键的最佳长度。

以下是基于上述思想的实现。

## C++14

```
/* A recursive C++ program to print maximum number of A's using
following four keys */
#include <bits/stdc++.h>
using namespace std;

// A recursive function that returns the optimal length string
// for N keystrokes
int findoptimal(int N)
{
    // The optimal string length is N when N is smaller than 7
    if (N <= 6)
        return N;

    // Initialize result
    int max = 0;

    // TRY ALL POSSIBLE BREAK-POINTS
    // For any keystroke N, we need to loop from N-3 keystrokes
    // back to 1 keystroke to find a breakpoint 'b' after which we
    // will have Ctrl-A, Ctrl-C and then only Ctrl-V all the way.
    int b;
    for (b = N - 3; b >= 1; b--) {

        // If the breakpoint is s at b'th keystroke then
        // the optimal string would have length
        // (n-b-1)*screen[b-1];
        int curr = (N - b - 1) * findoptimal(b);
        if (curr > max)
            max = curr;
    }
    return max;
}

// Driver program
int main()
{
    int N;

    // for the rest of the array we will rely on the previous
    // entries to compute new ones
    for (N = 1; N <= 20; N++)
        cout << "Maximum Number of A's with " << N <<
        " keystrokes is " << findoptimal(N) << endl;
}

// This code is contributed by shubhamsingh10
```

## C

```
/* A recursive C program to print maximum number of A's using
   following four keys */
#include <stdio.h>

// A recursive function that returns the optimal length string
// for N keystrokes
int findoptimal(int N)
{
    // The optimal string length is N when N is smaller than 7
    if (N <= 6)
        return N;

    // Initialize result
    int max = 0;

    // TRY ALL POSSIBLE BREAK-POINTS
    // For any keystroke N, we need to loop from N-3 keystrokes
    // back to 1 keystroke to find a breakpoint 'b' after which we
    // will have Ctrl-A, Ctrl-C and then only Ctrl-V all the way.
    int b;
    for (b = N - 3; b >= 1; b--) {
        // If the breakpoint is s at b'th keystroke then
        // the optimal string would have length
        // (n-b-1)*screen[b-1];
        int curr = (N - b - 1) * findoptimal(b);
        if (curr > max)
            max = curr;
    }
    return max;
}

// Driver program
int main()
{
    int N;

    // for the rest of the array we will rely on the previous
    // entries to compute new ones
    for (N = 1; N <= 20; N++)
        printf("Maximum Number of A's with %d keystrokes is %d\n",
               N, findoptimal(N));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A recursive Java program to print
  maximum number of A's using
  following four keys */
import java.io.*;

class GFG {

    // A recursive function that returns
    // the optimal length string  for N keystrokes
    static int findoptimal(int N)
    {
        // The optimal string length is N
        // when N is smaller than 7
        if (N <= 6)
            return N;

        // Initialize result
        int max = 0;

        // TRY ALL POSSIBLE BREAK-POINTS
        // For any keystroke N, we need to
        // loop from N-3 keystrokes back to
        // 1 keystroke to find a breakpoint
        // 'b' after which we will have Ctrl-A,
        // Ctrl-C and then only Ctrl-V all the way.
        int b;
        for (b = N - 3; b >= 1; b--) {
            // If the breakpoint is s at b'th
            // keystroke then the optimal string
            // would have length
            // (n-b-1)*screen[b-1];
            int curr = (N - b - 1) * findoptimal(b);
            if (curr > max)
                max = curr;
        }
        return max;
    }

    // Driver program
    public static void main(String[] args)
    {
        int N;

        // for the rest of the array we
        // will rely on the previous
        // entries to compute new ones
        for (N = 1; N <= 20; N++)
            System.out.println("Maximum Number of A's with keystrokes is " + N + findoptimal(N));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# A recursive Python3 program to print maximum
# number of A's using following four keys

# A recursive function that returns
# the optimal length string for N keystrokes

def findoptimal(N):

    # The optimal string length is
    # N when N is smaller than
    if N<= 6:
        return N

    # Initialize result
    maxi = 0

    # TRY ALL POSSIBLE BREAK-POINTS
    # For any keystroke N, we need
    # to loop from N-3 keystrokes
    # back to 1 keystroke to find
    # a breakpoint 'b' after which we
    # will have Ctrl-A, Ctrl-C and then
    # only Ctrl-V all the way.
    for b in range(N-3, 0, -1):
        curr =(N-b-1)*findoptimal(b)
        if curr>maxi:
            maxi = curr

    return maxi
# Driver program
if __name__=='__main__':

# for the rest of the array we will
# rely on the previous
# entries to compute new ones
    for n in range(1, 21):
        print('Maximum Number of As with ', n, 'keystrokes is ', findoptimal(n))

# this code is contributed by sahilshelangia
```

## C#

```
/* A recursive C# program
to print maximum number
of A's using following
four keys */
using System;

class GFG {
    // A recursive function that
    // returns the optimal length
    // string for N keystrokes
    static int findoptimal(int N)
    {
        // The optimal string length
        // is N when N is smaller than 7
        if (N <= 6)
            return N;

        // Initialize result
        int max = 0;

        // TRY ALL POSSIBLE BREAK-POINTS
        // For any keystroke N, we need
        // to loop from N-3 keystrokes
        // back to 1 keystroke to find
        // a breakpoint 'b' after which
        // we will have Ctrl-A, Ctrl-C
        // and then only Ctrl-V all the way.
        int b;
        for (b = N - 3; b >= 1; b--) {
            // If the breakpoint is s
            // at b'th keystroke then
            // the optimal string would
            // have length (n-b-1)*screen[b-1];
            int curr = (N - b - 1) * findoptimal(b);
            if (curr > max)
                max = curr;
        }
        return max;
    }

    // Driver code
    static void Main()
    {
        int N;

        // for the rest of the array
        // we will rely on the
        // previous entries to compute
        // new ones
        for (N = 1; N <= 20; N++)
            Console.WriteLine("Maximum Number of A's with " + N + " keystrokes is " + findoptimal(N));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* A recursive PHP program to print maximum number of A's using
following four keys */

// A recursive function that returns the optimal
//  length string for N keystrokes
function findoptimal($N)
{
    // The optimal string length is
    // N when N is smaller than 7
    if ($N <= 6)
        return $N;

    // Initialize result
    $max = 0;

    // TRY ALL POSSIBLE BREAK-POINTS
    // For any keystroke N, we need to loop from N-3 keystrokes
    // back to 1 keystroke to find a breakpoint 'b' after which we
    // will have Ctrl-A, Ctrl-C and then only Ctrl-V all the way.
    $b;
    for ($b = $N - 3; $b >= 1; $b -= 1)
    {
            // If the breakpoint is s at b'th keystroke then
            // the optimal string would have length
            // (n-b-1)*screen[b-1];
            $curr = ($N - $b - 1) * findoptimal($b);
            if ($curr > $max)
                $max = $curr;
    }
    return $max;
}

// Driver code
$N;

// for the rest of the array we will rely on the previous
// entries to compute new ones
for ($N = 1; $N <= 20; $N += 1)
    echo("Maximum Number of A's with"
        .$N."keystrokes is ".findoptimal($N)."\n");

// This code is contributed by aman neekhara
?>
```

## java 描述语言

```
<script>

// A recursive Javascript program to print
// maximum number of A's using
// following four keys

// A recursive function that returns the
// optimal length string  for N keystrokes
function findoptimal(N)
{

    // The optimal string length is N
    // when N is smaller than 7
    if (N <= 6)
        return N;

    // Initialize result
    let max = 0;

    // TRY ALL POSSIBLE BREAK-POINTS
    // For any keystroke N, we need to
    // loop from N-3 keystrokes back to
    // 1 keystroke to find a breakpoint
    // 'b' after which we will have Ctrl-A,
    // Ctrl-C and then only Ctrl-V all the way.
    let b;

    for(b = N - 3; b >= 1; b--)
    {

        // If the breakpoint is s at b'th
        // keystroke then the optimal string
        // would have length
        // (n-b-1)*screen[b-1];
        let curr = (N - b - 1) * findoptimal(b);

        if (curr > max)
            max = curr;
    }
    return max;
}

// Driver code
let N;

// For the rest of the array we
// will rely on the previous
// entries to compute new ones
for(N = 1; N <= 20; N++)
    document.write("Maximum Number of A's with "+
                   N + " keystrokes is " +
                   findoptimal(N) + "<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Maximum Number of A's with 1 keystrokes is 1
Maximum Number of A's with 2 keystrokes is 2
Maximum Number of A's with 3 keystrokes is 3
Maximum Number of A's with 4 keystrokes is 4
Maximum Number of A's with 5 keystrokes is 5
Maximum Number of A's with 6 keystrokes is 6
Maximum Number of A's with 7 keystrokes is 9
Maximum Number of A's with 8 keystrokes is 12
Maximum Number of A's with 9 keystrokes is 16
Maximum Number of A's with 10 keystrokes is 20
Maximum Number of A's with 11 keystrokes is 27
Maximum Number of A's with 12 keystrokes is 36
Maximum Number of A's with 13 keystrokes is 48
Maximum Number of A's with 14 keystrokes is 64
Maximum Number of A's with 15 keystrokes is 81
Maximum Number of A's with 16 keystrokes is 108
Maximum Number of A's with 17 keystrokes is 144
Maximum Number of A's with 18 keystrokes is 192
Maximum Number of A's with 19 keystrokes is 256
Maximum Number of A's with 20 keystrokes is 324
```

上述函数反复计算相同的子问题。通过存储子问题的解并以自下而上的方式解决问题，可以避免相同子问题的重新计算。

下面是基于动态编程的 C 实现，其中辅助数组屏幕[N]用于存储子问题的结果。

## C++

```
/* A Dynamic Programming based C program to find maximum number of A's
that can be printed using four keys */
#include <iostream>
using namespace std;

// this function returns the optimal length string for N keystrokes
int findoptimal(int N)
{
    // The optimal string length is N when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result of subproblems
    int screen[N];

    int b; // To pick a breakpoint

    // Initializing the optimal lengths array for uptil 6 input
    // strokes.
    int n;
    for (n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom manner
    for (n = 7; n <= N; n++) {
        // Initialize length of optimal string for n keystrokes
        screen[n - 1] = 0;

        // For any keystroke n, we need to loop from n-3 keystrokes
        // back to 1 keystroke to find a breakpoint 'b' after which we
        // will have ctrl-a, ctrl-c and then only ctrl-v all the way.
        for (b = n - 3; b >= 1; b--) {
            // if the breakpoint is at b'th keystroke then
            // the optimal string would have length
            // (n-b-1)*screen[b-1];
            int curr = (n - b - 1) * screen[b - 1];
            if (curr > screen[n - 1])
                screen[n - 1] = curr;
        }
    }

    return screen[N - 1];
}

// Driver program
int main()
{
    int N;

    // for the rest of the array we will rely on the previous
    // entries to compute new ones
    for (N = 1; N <= 20; N++)
        cout << "Maximum Number of A's with "<<N<<" keystrokes is "
        << findoptimal(N) << endl;
}

//This is contributed by shubhamsingh10
```

## C

```
/* A Dynamic Programming based C program to find maximum number of A's
   that can be printed using four keys */
#include <stdio.h>

// this function returns the optimal length string for N keystrokes
int findoptimal(int N)
{
    // The optimal string length is N when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result of subproblems
    int screen[N];

    int b; // To pick a breakpoint

    // Initializing the optimal lengths array for uptil 6 input
    // strokes.
    int n;
    for (n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom manner
    for (n = 7; n <= N; n++) {
        // Initialize length of optimal string for n keystrokes
        screen[n - 1] = 0;

        // For any keystroke n, we need to loop from n-3 keystrokes
        // back to 1 keystroke to find a breakpoint 'b' after which we
        // will have ctrl-a, ctrl-c and then only ctrl-v all the way.
        for (b = n - 3; b >= 1; b--) {
            // if the breakpoint is at b'th keystroke then
            // the optimal string would have length
            // (n-b-1)*screen[b-1];
            int curr = (n - b - 1) * screen[b - 1];
            if (curr > screen[n - 1])
                screen[n - 1] = curr;
        }
    }

    return screen[N - 1];
}

// Driver program
int main()
{
    int N;

    // for the rest of the array we will rely on the previous
    // entries to compute new ones
    for (N = 1; N <= 20; N++)
        printf("Maximum Number of A's with %d keystrokes is %d\n",
               N, findoptimal(N));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A Dynamic Programming based C
   program to find maximum number
   of A's that can be printed using
   four keys */
import java.io.*;

class GFG {

    // this function returns the optimal
    // length string for N keystrokes
    static int findoptimal(int N)
    {
        // The optimal string length is N
        // when N is smaller than 7
        if (N <= 6)
            return N;

        // An array to store result
        // of subproblems
        int screen[] = new int[N];

        int b; // To pick a breakpoint

        // Initializing the optimal lengths
        // array for uptil 6 input strokes
        int n;
        for (n = 1; n <= 6; n++)
            screen[n - 1] = n;

        // Solve all subproblems in bottom manner
        for (n = 7; n <= N; n++) {
            // Initialize length of optimal
            // string for n keystrokes
            screen[n - 1] = 0;

            // For any keystroke n, we need
            // to loop from n-3 keystrokes
            // back to 1 keystroke to find
            // a breakpoint 'b' after which we
            // will have ctrl-a, ctrl-c and
            // then only ctrl-v all the way.
            for (b = n - 3; b >= 1; b--) {
                // if the breakpoint is
                // at b'th keystroke then
                // the optimal string would
                // have length
                // (n-b-1)*screen[b-1];
                int curr = (n - b - 1) * screen[b - 1];
                if (curr > screen[n - 1])
                    screen[n - 1] = curr;
            }
        }

        return screen[N - 1];
    }

    // Driver program
    public static void main(String[] args)
    {
        int N;

        // for the rest of the array we will rely on the previous
        // entries to compute new ones
        for (N = 1; N <= 20; N++)
            System.out.println("Maximum Number of A's with keystrokes is " + N + findoptimal(N));
    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# A Dynamic Programming based Python program
# to find maximum number of A's
# that can be printed using four keys

# this function returns the optimal
# length string for N keystrokes
def findoptimal(N):

    # The optimal string length is
    # N when N is smaller than 7
    if (N <= 6):
        return N

    # An array to store result of
    # subproblems
    screen = [0]*N

    # Initializing the optimal lengths
    # array for uptil 6 input
    # strokes.

    for n in range(1, 7):
        screen[n-1] = n

    # Solve all subproblems in bottom manner
    for n in range(7, N + 1):

        # Initialize length of optimal
        # string for n keystrokes
        screen[n-1] = 0

        # For any keystroke n, we need to
        # loop from n-3 keystrokes
        # back to 1 keystroke to find a breakpoint
        # 'b' after which we
        # will have ctrl-a, ctrl-c and then only
        # ctrl-v all the way.
        for b in range(n-3, 0, -1):

            # if the breakpoint is at b'th keystroke then
            # the optimal string would have length
            # (n-b-1)*screen[b-1];
            curr = (n-b-1)*screen[b-1]
            if (curr > screen[n-1]):
                screen[n-1] = curr

    return screen[N-1]

# Driver program
if __name__ == "__main__":

    # for the rest of the array we
    # will rely on the previous
    # entries to compute new ones
    for N in range(1, 21):
        print("Maximum Number of A's with ", N, " keystrokes is ",
                findoptimal(N))

# this code is contributed by
# ChitraNayal
```

## C#

```
/* A Dynamic Programming based C#
program to find maximum number
of A's that can be printed using
four keys */
using System;
public class GFG {

    // this function returns the optimal
    // length string for N keystrokes
    static int findoptimal(int N)
    {
        // The optimal string length is N
        // when N is smaller than 7
        if (N <= 6)
            return N;

        // An array to store result
        // of subproblems
        int[] screen = new int[N];

        int b; // To pick a breakpoint

        // Initializing the optimal lengths
        // array for uptil 6 input strokes
        int n;
        for (n = 1; n <= 6; n++)
            screen[n - 1] = n;

        // Solve all subproblems in bottom manner
        for (n = 7; n <= N; n++) {
            // Initialize length of optimal
            // string for n keystrokes
            screen[n - 1] = 0;

            // For any keystroke n, we need
            // to loop from n-3 keystrokes
            // back to 1 keystroke to find
            // a breakpoint 'b' after which we
            // will have ctrl-a, ctrl-c and
            // then only ctrl-v all the way.
            for (b = n - 3; b >= 1; b--) {
                // if the breakpoint is
                // at b'th keystroke then
                // the optimal string would
                // have length
                // (n-b-1)*screen[b-1];
                int curr = (n - b - 1) * screen[b - 1];
                if (curr > screen[n - 1])
                    screen[n - 1] = curr;
            }
        }

        return screen[N - 1];
    }

    // Driver program
    public static void Main(String[] args)
    {
        int N;

        // for the rest of the array we will rely on the previous
        // entries to compute new ones
        for (N = 1; N <= 20; N++)
            Console.WriteLine("Maximum Number of A's with {0} keystrokes is {1}\n",
                              N, findoptimal(N));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// A Dynamic Programming based javascript
// program to find maximum number
// of A's that can be printed using
// four keys

// This function returns the optimal
// length string for N keystrokes  
function findoptimal(N)
{

    // The optimal string length is N
    // when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result
    // of subproblems
    let screen = new Array(N);
    for(let i = 0; i < N; i++)
    {
        screen[i] = 0;
    }

    // To pick a breakpoint
    let b;

    // Initializing the optimal lengths
    // array for uptil 6 input strokes
    let n;
    for(n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom manner
    for(n = 7; n <= N; n++)
    {

        // Initialize length of optimal
        // string for n keystrokes
        screen[n - 1] = 0;

        // For any keystroke n, we need
        // to loop from n-3 keystrokes
        // back to 1 keystroke to find
        // a breakpoint 'b' after which we
        // will have ctrl-a, ctrl-c and
        // then only ctrl-v all the way.
        for(b = n - 3; b >= 1; b--)
        {

            // If the breakpoint is
            // at b'th keystroke then
            // the optimal string would
            // have length
            // (n-b-1)*screen[b-1];
            let curr = (n - b - 1) * screen[b - 1];

            if (curr > screen[n - 1])
                screen[n - 1] = curr;
        }
    }
    return screen[N - 1];
}

// Driver code
let N;
for(N = 1; N <= 20; N++)
    document.write("Maximum Number of A's with " +
                   N + " keystrokes is " +
                   findoptimal(N) + "<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Maximum Number of A's with 1 keystrokes is 1
Maximum Number of A's with 2 keystrokes is 2
Maximum Number of A's with 3 keystrokes is 3
Maximum Number of A's with 4 keystrokes is 4
Maximum Number of A's with 5 keystrokes is 5
Maximum Number of A's with 6 keystrokes is 6
Maximum Number of A's with 7 keystrokes is 9
Maximum Number of A's with 8 keystrokes is 12
Maximum Number of A's with 9 keystrokes is 16
Maximum Number of A's with 10 keystrokes is 20
Maximum Number of A's with 11 keystrokes is 27
Maximum Number of A's with 12 keystrokes is 36
Maximum Number of A's with 13 keystrokes is 48
Maximum Number of A's with 14 keystrokes is 64
Maximum Number of A's with 15 keystrokes is 81
Maximum Number of A's with 16 keystrokes is 108
Maximum Number of A's with 17 keystrokes is 144
Maximum Number of A's with 18 keystrokes is 192
Maximum Number of A's with 19 keystrokes is 256
Maximum Number of A's with 20 keystrokes is 324
```

感谢 **Gaurav Saxena** 提供了上述解决这个问题的方法。
随着 A 的数量变大，按下 Ctrl-V 3 次以上的效果开始变得没有实质，相比之下只是再次按下 Ctrl-A、Ctrl-C、Ctrl-V。所以，只检查按 Ctrl-V 1、2、3 次的效果，可以让上面的代码更高效。

## C++

```
// A Dynamic Programming based C++ program to find maximum
// number of A's that can be printed using four keys

#include <bits/stdc++.h>
using namespace std;

// This function returns the optimal length string for N keystrokes
int findoptimal(int N)
{
    // The optimal string length is N when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result of subproblems
    int screen[N];

    int b; // To pick a breakpoint

    // Initializing the optimal lengths array for uptil 6 input
    // strokes.
    int n;
    for (n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom-up manner
    for (n = 7; n <= N; n++) {

        // for any keystroke n, we will need to choose between:-
        // 1\. pressing Ctrl-V once after copying the
        // A's obtained by n-3 keystrokes.

        // 2\. pressing Ctrl-V twice after copying the A's
        // obtained by n-4 keystrokes.

        // 3\. pressing Ctrl-V thrice after copying the A's
        // obtained by n-5 keystrokes.
        screen[n - 1] = max(2 * screen[n - 4],
                            max(3 * screen[n - 5],
4 * screen[n - 6]));
    }

    return screen[N - 1];
}

// Driver program
int main()
{
    int N;

    // for the rest of the array we will rely on the previous
    // entries to compute new ones
    for (N = 1; N <= 20; N++)
        printf("Maximum Number of A's with %d keystrokes is %d\n",
               N, findoptimal(N));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java program
// to find maximum number of A's that
// can be printed using four keys
class GFG
{

// This function returns the optimal length
// string for N keystrokes
static int findoptimal(int N)
{
    // The optimal string length is N
    // when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result of subproblems
    int []screen = new int[N];

    int b; // To pick a breakpoint

    // Initializing the optimal lengths array
    // for uptil 6 input strokes.
    int n;
    for (n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom-up manner
    for (n = 7; n <= N; n++)
    {

        // for any keystroke n, we will need to choose between:-
        // 1\. pressing Ctrl-V once after copying the
        // A's obtained by n-3 keystrokes.

        // 2\. pressing Ctrl-V twice after copying the A's
        // obtained by n-4 keystrokes.

        // 3\. pressing Ctrl-V thrice after copying the A's
        // obtained by n-5 keystrokes.
        screen[n - 1] = Math.max(2 * screen[n - 4],
                        Math.max(3 * screen[n - 5],
                                 4 * screen[n - 6]));
    }
    return screen[N - 1];
}

// Driver Code
public static void main(String[] args)
{
    int N;

    // for the rest of the array we will rely
    // on the previous entries to compute new ones
    for (N = 1; N <= 20; N++)
        System.out.printf("Maximum Number of A's with" +
                               " %d keystrokes is %d\n",
                                     N, findoptimal(N));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# A Dynamic Programming based Python3 program
# to find maximum number of A's
# that can be printed using four keys

# this function returns the optimal
# length string for N keystrokes
def findoptimal(N):

    # The optimal string length is
    # N when N is smaller than 7
    if (N <= 6):
        return N

    # An array to store result of
    # subproblems
    screen = [0] * N

    # Initializing the optimal lengths
    # array for uptil 6 input
    # strokes.

    for n in range(1, 7):
        screen[n - 1] = n

    # Solve all subproblems in bottom manner
    for n in range(7, N + 1):

        # for any keystroke n, we will need to choose between:-
        # 1\. pressing Ctrl-V once after copying the
        # A's obtained by n-3 keystrokes.

        # 2\. pressing Ctrl-V twice after copying the A's
        # obtained by n-4 keystrokes.

        # 3\. pressing Ctrl-V thrice after copying the A's
        # obtained by n-5 keystrokes.
        screen[n - 1] = max(2 * screen[n - 4],
                        max(3 * screen[n - 5],
                            4 * screen[n - 6]));

    return screen[N - 1]

# Driver Code
if __name__ == "__main__":

    # for the rest of the array we
    # will rely on the previous
    # entries to compute new ones
    for N in range(1, 21):
        print("Maximum Number of A's with ", N,
              " keystrokes is ", findoptimal(N))

# This code is contributed by ashutosh450
```

## C#

```
// A Dynamic Programming based C# program
// to find maximum number of A's that
// can be printed using four keys
using System;

class GFG
{

// This function returns the optimal length
// string for N keystrokes
static int findoptimal(int N)
{
    // The optimal string length is N
    // when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result of subproblems
    int []screen = new int[N];

    // Initializing the optimal lengths array
    // for uptil 6 input strokes.
    int n;
    for (n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom-up manner
    for (n = 7; n <= N; n++)
    {

        // for any keystroke n, we will need to choose between:-
        // 1\. pressing Ctrl-V once after copying the
        // A's obtained by n-3 keystrokes.

        // 2\. pressing Ctrl-V twice after copying the A's
        // obtained by n-4 keystrokes.

        // 3\. pressing Ctrl-V thrice after copying the A's
        // obtained by n-5 keystrokes.
        screen[n - 1] = Math.Max(2 * screen[n - 4],
                        Math.Max(3 * screen[n - 5],
                                4 * screen[n - 6]));
    }
    return screen[N - 1];
}

// Driver Code
public static void Main(String[] args)
{
    int N;

    // for the rest of the array we will rely
    // on the previous entries to compute new ones
    for (N = 1; N <= 20; N++)
        Console.Write("Maximum Number of A's with" +
                            " {0} keystrokes is {1}\n",
                                    N, findoptimal(N));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// A Dynamic Programming based
// JavaScript program to find maximum
// number of A's that can be printed
// using four keys

// This function returns the optimal
// length string for N keystrokes
function findoptimal(N){
    // The optimal string length is N
    // when N is smaller than 7
    if (N <= 6)
        return N;

    // An array to store result
    // of subproblems
    let screen = [];

    let b; // To pick a breakpoint

    // Initializing the optimal lengths
    // array for uptil 6 input
    // strokes.
    let n;
    for (n = 1; n <= 6; n++)
        screen[n - 1] = n;

    // Solve all subproblems in bottom-up manner
    for (n = 7; n <= N; n++) {

        // for any keystroke n, we will
        // need to choose between:-
        // 1\. pressing Ctrl-V once
        // after copying the
        // A's obtained by n-3 keystrokes.

        // 2\. pressing Ctrl-V twice after
        // copying the A's
        // obtained by n-4 keystrokes.

        // 3\. pressing Ctrl-V thrice
        // after copying the A's
        // obtained by n-5 keystrokes.
        screen[n - 1] = Math.max(2 * screen[n - 4],
                        Math.max(3 * screen[n - 5],
4 * screen[n - 6]));
    }

    return screen[N - 1];
}

// Driver program
let N;
// for the rest of the array we will rely on the previous
// entries to compute new ones
for (N = 1; N <= 20; N++)
    document.write(
    "Maximum Number of A's with "+ N +" keystrokes is "
    +findoptimal(N)+"<br>"
    );

</script>
```

**输出:**

```
Maximum Number of A's with 1 keystrokes is 1
Maximum Number of A's with 2 keystrokes is 2
Maximum Number of A's with 3 keystrokes is 3
Maximum Number of A's with 4 keystrokes is 4
Maximum Number of A's with 5 keystrokes is 5
Maximum Number of A's with 6 keystrokes is 6
Maximum Number of A's with 7 keystrokes is 9
Maximum Number of A's with 8 keystrokes is 12
Maximum Number of A's with 9 keystrokes is 16
Maximum Number of A's with 10 keystrokes is 20
Maximum Number of A's with 11 keystrokes is 27
Maximum Number of A's with 12 keystrokes is 36
Maximum Number of A's with 13 keystrokes is 48
Maximum Number of A's with 14 keystrokes is 64
Maximum Number of A's with 15 keystrokes is 81
Maximum Number of A's with 16 keystrokes is 108
Maximum Number of A's with 17 keystrokes is 144
Maximum Number of A's with 18 keystrokes is 192
Maximum Number of A's with 19 keystrokes is 256
Maximum Number of A's with 20 keystrokes is 324
```

感谢 [Sahil](https://www.linkedin.com/in/sahil-singh-abba28162/) 提供上述解决这个问题的方法。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息