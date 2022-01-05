# 找出数列的第 n 项，其中每项交替相差 6 和 2

> 原文:[https://www . geeksforgeeks . org/find-系列的第 n 个术语，其中每个术语交替地相差 6 和 2/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-where-each-term-differs-by-6-and-2-alternately/)

给定一个数字 **N** ，任务是找到数列的第**N**项，其中每个项交替相差 6 和 2。
**例:**

> **输入:** N = 6
> **输出:** 24
> **解释:**
> 第 N 项为 0 + 6 + 2 + 6 + 2 + 6 + 2 = 24
> **输入:** N = 3
> **输出:** 14
> **解释:**
> 第 N 项为 0 + 6 + 2 + 6 = 14

**天真方法:**想法是从 **1** 开始迭代，交替增加 **6** 和 **2** ，直到我们到达**第 n 个**项。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find Nth term
void findNthTerm(int N)
{
    int ans = 0;

    // Iterate from 1 till Nth term
    for (int i = 0; i < N; i++) {

        // Check if i is even and
        // then add 6
        if (i % 2 == 0) {
            ans = ans + 6;
        }

        // Else add 2
        else {
            ans = ans + 2;
        }
    }

    // Print ans
    cout << ans << endl;
}

// Driver Code
int main()
{
    int N = 3;
    findNthTerm(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find Nth term
static void findNthTerm(int N)
{
    int ans = 0;

    // Iterate from 1 till Nth term
    for (int i = 0; i < N; i++) {

        // Check if i is even and
        // then add 6
        if (i % 2 == 0) {
            ans = ans + 6;
        }

        // Else add 2
        else {
            ans = ans + 2;
        }
    }

    // Print ans
    System.out.print(ans +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    findNthTerm(N);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find Nth term
def findNthTerm(N):
    ans = 0

    # Iterate from 1 till Nth term
    for i in range(N):

        # Check if i is even and
        # then add 6
        if (i % 2 == 0) :
            ans = ans + 6

        # Else add 2
        else :
            ans = ans + 2

    # Print ans
    print(ans)

# Driver Code
if __name__=='__main__':

    N = 3
    findNthTerm(N)

# This code is contributed by AbhiThakur
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find Nth term
static void findNthTerm(int N)
{
    int ans = 0;

    // Iterate from 1 till Nth term
    for (int i = 0; i < N; i++) {

        // Check if i is even and
        // then add 6
        if (i % 2 == 0) {
            ans = ans + 6;
        }

        // Else add 2
        else {
            ans = ans + 2;
        }
    }

    // Print ans
    Console.Write(ans +"\n");
}

// Driver Code
public static void Main()
{
    int N = 3;
    findNthTerm(N);
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find Nth term
    function findNthTerm(N)
    {
        let ans = 0;

        // Iterate from 1 till Nth term
        for (let i = 0; i < N; i++) {

            // Check if i is even and
            // then add 6
            if (i % 2 == 0) {
                ans = ans + 6;
            }

            // Else add 2
            else {
                ans = ans + 2;
            }
        }

        // Print ans
        document.write(ans + "<br>");
    }

    // Driver Code
       let N = 3;
       findNthTerm(N);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
14
```

***时间复杂度:**O(N)*
T5】高效方法:我们可以通过使用以下公式找到**第 N 个**项:

1.  **如果 N 为奇数:**第 N 项由(N/2 + 1)*6 + (N/2)*2 给出。
2.  **如果 N 为偶数:**第 N 项由(N/2)*6 + (N/2)*2 给出。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find Nth term
void findNthTerm(int N)
{
    int ans;

    // Check if N is even
    if (N % 2 == 0) {

        // Formula for n is even
        ans = (N / 2) * 6
              + (N / 2) * 2;
    }

    // Check if N is odd
    else {
        // Formula for N is odd
        ans = (N / 2 + 1) * 6
              + (N / 2) * 2;
    }

    // Print ans
    cout << ans << endl;
}

// Driver Code
int main()
{
    int N = 3;
    findNthTerm(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG{

// Function to find Nth term
static void findNthTerm(int N)
{
    int ans;

    // Check if N is even
    if (N % 2 == 0) {

        // Formula for n is even
        ans = (N / 2) * 6
              + (N / 2) * 2;
    }

    // Check if N is odd
    else {
        // Formula for N is odd
        ans = (N / 2 + 1) * 6
              + (N / 2) * 2;
    }

    // Print ans
    System.out.print(ans +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    findNthTerm(N);
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find Nth term
def findNthTerm(N):
    ans = 0;

    # Check if N is even
    if (N % 2 == 0):

        # Formula for n is even
        ans = (N // 2) * 6 + (N // 2) * 2;

    # Check if N is odd
    else:

        # Formula for N is odd
        ans = (N // 2 + 1) * 6 + (N // 2) * 2;

    # Print ans
    print(ans);

# Driver Code
if __name__ == '__main__':

    N = 3;
    findNthTerm(N);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find Nth term
static void findNthTerm(int N)
{
    int ans;

    // Check if N is even
    if (N % 2 == 0) {

        // Formula for n is even
        ans = (N / 2) * 6
              + (N / 2) * 2;
    }

    // Check if N is odd
    else {
        // Formula for N is odd
        ans = (N / 2 + 1) * 6
              + (N / 2) * 2;
    }

    // Print ans
    Console.Write(ans +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    findNthTerm(N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find Nth term
function findNthTerm( N)
{
    let ans;

    // Check if N is even
    if (N % 2 == 0) {

        // Formula for n is even
        ans = parseInt(N / 2) * 6
              + parseInt(N / 2) * 2;
    }

    // Check if N is odd
    else {
        // Formula for N is odd
        ans = parseInt(N / 2 + 1) * 6
              + parseInt(N / 2) * 2;
    }

    // Print ans
     document.write(ans);
}

// Driver Function

    // get the value of N
    let N = 3;

    // Calculate and print the Nth term
    findNthTerm(N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(1)*