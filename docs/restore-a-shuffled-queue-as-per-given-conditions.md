# 根据给定条件

恢复混洗队列

> 原文:[https://www . geeksforgeeks . org/restore-a-shuffled-queue-as-at-给定条件/](https://www.geeksforgeeks.org/restore-a-shuffled-queue-as-per-given-conditions/)

给定 **N** 人排队两阵 **A[]** 和 **B[]** 。数组 A[]代表人的名字，数组 B[]代表站在那个人面前的特定的人比多少人高。现在队列被打乱了。任务是按照上述属性打印队列的原始序列。

**示例:**

> **输入:** N = 4，A[] = {'a '，' B '，' c '，' d'}，B[] = {0，2，0，0}
> **输出:**
> A 1
> c 3
> d 4
> B 2
> **说明:**
> 看输出队列及其生成的高度，很容易理解:
> 1) a 是队列中的第一个，所以我们有第 0 个索引的人所以 a 在输入中与 0 相关联。
> 2) c 前面只有一个 a，但 a 比 c 短，因此 c 在输入中与 0 相关联。
> 3) d 前面有 c 和 a，但都比 d 短，因此 d 在输入中与 0 相关联。
> 4) b 前面有 d、c 和 a，但只有 c 和 d 比 b 高，所以 b 在输入中与 2 相关联。
> 
> **输入:** N = 4，A[] = { 'a '，' B '，' c '，' d'}，B[] = { 0，1，3，3}
> **输出:** -1
> **解释:**
> 给定的顺序是队列的原始顺序。

**进场:**

*   首先制作一对人名及其相关整数[并排序](https://www.geeksforgeeks.org/sorting-algorithms/)对。
*   创建一个数组**回答[]** 来存储人的可能高度。
*   迭代所有的对，如果站在前面的人数比他们当前的站立位置高，那么返回 **-1** 。
*   否则，将当前站立位置与比他高的人的身高之差存储在答案数组中。
*   对于每一个人，迭代该对，如果我们当前人的答案数组的值**大于我们与之比较的人**，则增加当前对的答案数组中的值。
*   最后，根据存储在**答案[]** 数组中的值，打印给定序列中的可能对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate the Queue
void OriginalQueue(char A[], int B[],
                   int N)
{
    // Making a pair
    pair<int, string> a[N + 1];

    // Answer array
    int ans[N + 1];
    bool possible = true;

    // Store the values in the pair
    for (int i = 0; i < N; i++) {
        a[i].second = A[i];
        a[i].first = B[i];
    }

    // Sort the pair
    sort(a, a + N);

    // Traverse the pairs
    for (int i = 0; i < N; i++) {

        int len = i - a[i].first;

        // If it is not possible to
        // generate the Queue
        if (len < 0) {

            cout << "-1";
            possible = false;
        }

        if (!possible)
            break;
        else {
            ans[i] = len;

            for (int j = 0; j < i; j++) {

                // Increment the answer
                if (ans[j] >= ans[i])
                    ans[j]++;
            }
        }

        // Finally printing the answer
        if (i == N - 1 && possible) {
            for (int i = 0; i < N; i++) {
                cout << a[i].second << " "
                     << ans[i] + 1 << endl;
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 4;

    // Given name of person as char
    char A[N] = { 'a', 'b', 'c', 'd' };

    // Associated integers
    int B[N] = { 0, 2, 0, 0 };

    // Function Call
    OriginalQueue(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to generate the Queue
static void OriginalQueue(char A[], int B[],
                                    int N)
{
    // Making a pair
    int[][] a = new int[N][2];

    // Answer array
    int[] ans = new int[N];
    boolean possible = true;

    // Store the values in the pair
    for(int i = 0; i < N; i++)
    {
        a[i][0] = B[i];
        a[i][1] = (int)A[i];
    }

    // Sort the pair
    Arrays.sort(a, (o1, o2) -> o1[0] - o2[0]);

    // Traverse the pairs
    for(int i = 0; i < N; i++)
    {
        int len = i - a[i][0];

        // If it is not possible to
        // generate the Queue
        if (len < 0)
        {
            System.out.print("-1");
            possible = false;
        }

        if (!possible)
            break;
        else
        {
            ans[i] = len;

            for(int j = 0; j < i; j++)
            {

                // Increment the answer
                if (ans[j] >= ans[i])
                    ans[j]++;
            }
        }

        // Finally printing the answer
        if (i == N - 1 && possible)
        {
            for(int k = 0; k < N; k++)
            {
                System.out.println((char)a[k][1] +
                                 " "+ (ans[k] + 1));
            }
        }
    }
}

// Driver Code
public static void main (String[] args)
{
    int N = 4;

    // Given name of person as char
    char A[] = { 'a', 'b', 'c', 'd' };

    // Associated integers
    int B[] = { 0, 2, 0, 0 };

    // Function Call
    OriginalQueue(A, B, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to generate the Queue
def OriginalQueue(A, B, N):

    # Making a pair
    a = [[0, ""] for i in range(N)]

    # Answer array
    ans = [0 for i in range(N)]
    possible = True

    # Store the values in the pair
    for i in range(N):
        a[i][1] = str(A[i])
        a[i][0] = B[i]

    # Sort the pair
    a.sort(reverse = False)

    # Traverse the pairs
    for i in range(N):
        len1 = i - a[i][0]

        # If it is not possible to
        # generate the Queue
        if (len1 < 0):
            print("-1",end = "")
            possible = False

        if (possible == False):
            break
        else:
            ans[i] = len1

            for j in range(i):

                # Increment the answer
                if (ans[j] >= ans[i]):
                    ans[j] += 1

        # Finally printing the answer
        if (i == N - 1 and possible):
            for i in range(N):
                print(a[i][1], ans[i] + 1)

# Driver Code
if __name__ == '__main__':

    N = 4

    # Given name of person as char
    A = [ 'a', 'b', 'c', 'd' ]

    # Associated integers
    B = [ 0, 2, 0, 0 ]

    # Function Call
    OriginalQueue(A, B, N)

# This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to generate the Queue
function OriginalQueue(A, B, N)
{

    // Making a pair
    var a = Array(N + 1);
    for(var i = 0; i < N; i++)
    {
        a[i] = [0, ""];
    }

    // Answer array
    var ans = Array(N + 1);
    var possible = true;

    // Store the values in the pair
    for(var i = 0; i < N; i++)
    {
        a[i][1] = A[i];
        a[i][0] = B[i];
    }

    // Sort the pair
    a.sort()

    // Traverse the pairs
    for(var i = 0; i < N; i++)
    {
        var len = i - a[i][0];

        // If it is not possible to
        // generate the Queue
        if (len < 0)
        {
            document.write("-1");
            possible = false;
        }

        if (!possible)
            break;
        else
        {
            ans[i] = len;

            for(var j = 0; j < i; j++)
            {

                // Increment the answer
                if (ans[j] >= ans[i])
                    ans[j]++;
            }
        }

        // Finally printing the answer
        if (i == N - 1 && possible)
        {
            for(var i = 0; i < N; i++)
            {
                document.write(a[i][1] + " " +
                               (ans[i] + 1) + "<br>");
            }
        }
    }
}

// Driver Code
var N = 4;

// Given name of person as char
var A = [ 'a', 'b', 'c', 'd' ];

// Associated integers
var B = [ 0, 2, 0, 0 ];

// Function Call
OriginalQueue(A, B, N);

// This code is contributed by itsok

</script>
```

**Output:** 

```
a 1
c 3
d 4
b 2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*