# 完成多项式生成的序列

> 原文:[https://www . geesforgeks . org/complete-sequence-generated-polythone/](https://www.geeksforgeeks.org/complete-sequence-generated-polynomial/)

给定一个含有某些项的序列，我们需要计算这个序列的下一个 K 项。给定序列由某个多项式生成，无论该多项式有多复杂。注意多项式是以下形式的表达式:
P(x) = a0 + a1 x +a2 x^2 + a3 x^3 ……..+ an x^n
给定的序列总是可以用多个多项式来描述，在这些多项式中，我们需要找到具有最低次数的多项式，并且仅使用该多项式来生成下一项。

示例:

```
If given sequence is 1, 2, 3, 4, 5 then its next term will be 6, 7, 8, etc
and this correspond to a trivial polynomial.
If given sequence is 1, 4, 7, 10 then its next term will be 13, 16, etc.
```

我们可以用一种叫做差分法的技巧来解决这个问题，这种技巧可以从[拉格朗日多项式](https://en.wikipedia.org/wiki/Lagrange_polynomial)推导出来。

技巧很简单，我们取连续项之间的差，如果差相等，那么我们停止并建立序列的下一项，否则我们再次取这些差之间的差，直到它们变成常数。
下图举例说明了该技术，给定的序列是 8、11、16、23，我们应该找到这个序列的下 3 个项。

![generate-polynomial](img/b2198293947fe7f05799d0d0b98e9c34.png)

在下面的代码中，实现了相同的技术，首先我们循环，直到我们得到一个恒定的差值，将每个差值序列的第一个数字保存在一个单独的向量中，以便再次重建该序列。然后，我们将相同常数差的 K 个实例添加到我们的数组中，以生成新的序列 K 项，并按照相反的顺序遵循相同的过程来重建序列。

为了更好地理解，请参见下面的代码。

## C++

```
// C++ code to generate next terms of a given polynomial
// sequence
#include <bits/stdc++.h>
using namespace std;

//  method to print next terms term of sequence
void nextTermsInSequence(int sequence[], int N, int terms)
{
    int diff[N + terms];

    //  first copy the sequence itself into diff array
    for (int i = 0; i < N; i++)
        diff[i] = sequence[i];

    bool more = false;
    vector<int> first;
    int len = N;

    // loop until one difference remains or all
    // difference become constant
    while (len > 1)
    {
        // keeping the first term of sequence for
        // later rebuilding
        first.push_back(diff[0]);
        len--;

        // converting the difference to difference
        // of differences
        for (int i = 0; i < len; i++)
            diff[i] = diff[i + 1] - diff[i];

        // checking if all difference values are
        // same or not
        int i;
        for (i = 1; i < len; i++)
            if (diff[i] != diff[i - 1])
                break;

        // If some difference values were not same
        if (i != len)
           break;
    }

    int iteration = N - len;

    //  padding terms instance of constant difference
    // at the end of array
    for (int i = len; i < len + terms; i++)
        diff[i] = diff[i - 1];
    len += terms;

    //  iterating to get actual sequence back
    for (int i = 0; i < iteration; i++)
    {
        len++;

        //  shifting all difference by one place
        for (int j = len - 1; j > 0; j--)
            diff[j] = diff[j - 1];

        // copying actual first element
        diff[0] = first[first.size() - i - 1];

        // converting difference of differences to
        // difference array
        for (int j = 1; j < len; j++)
            diff[j] = diff[j - 1] + diff[j];
    }

    //  printing the result
    for (int i = 0; i < len; i++)
        cout << diff[i] << " ";
    cout << endl;
}

//  Driver code to test above method
int main()
{
    int sequence[] = {8, 11, 16, 23};
    int N = sizeof(sequence) / sizeof(int);

    int terms = 3;
    nextTermsInSequence(sequence, N, terms);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate next terms
// of a given polynomial sequence
import java.util.*;

class GFG{

// Method to print next terms term of sequence
static void nextTermsInSequence(int []sequence,
                                int N, int terms)
{
    int []diff = new int[N + terms];

    // First copy the sequence itself
    // into diff array
    for(int i = 0; i < N; i++)
        diff[i] = sequence[i];

    //bool more = false;
    ArrayList<Object> first = new ArrayList<Object>();
    int len = N;

    // Loop until one difference remains
    // or all difference become constant
    while (len > 1)
    {

        // Keeping the first term of
        // sequence for later rebuilding
        first.add(diff[0]);
        len--;

        // Converting the difference to
        // difference of differences
        for(int i = 0; i < len; i++)
            diff[i] = diff[i + 1] - diff[i];

        // Checking if all difference values
        // are same or not
        int j;
        for(j = 1; j < len; j++)
            if (diff[j] != diff[j - 1])
                break;

        // If some difference values
        // were not same
        if (j != len)
           break;
    }

    int iteration = N - len;

    // Padding terms instance of constant
    // difference at the end of array
    for(int i = len; i < len + terms; i++)
        diff[i] = diff[i - 1];

    len += terms;

    // Iterating to get actual sequence back
    for(int i = 0; i < iteration; i++)
    {
        len++;

        // Shifting all difference by one place
        for(int j = len - 1; j > 0; j--)
            diff[j] = diff[j - 1];

        // Copying actual first element
        diff[0] = (int)first.get(first.size() - i - 1);

        // Converting difference of differences
        // to difference array
        for(int j = 1; j < len; j++)
            diff[j] = diff[j - 1] + diff[j];
    }

    // Printing the result
    for(int i = 0; i < len; i++)
    {
        System.out.print(diff[i] + " ");
    }

    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    int []sequence = { 8, 11, 16, 23 };
    int N = sequence.length;
    int terms = 3;

    nextTermsInSequence(sequence, N, terms);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 code to generate next terms
# of a given polynomial sequence

# Method to print next terms term of sequence
def nextTermsInSequence(sequence, N, terms):

    diff = [0] * (N + terms)

    # First copy the sequence itself
    # into diff array
    for i in range(N):
        diff[i] = sequence[i]

    more = False
    first = []
    length = N

    # Loop until one difference remains
    # or all difference become constant
    while (length > 1):

        # Keeping the first term of sequence
        # for later rebuilding
        first.append(diff[0])
        length -= 1

        # Converting the difference to difference
        # of differences
        for i in range(length):
            diff[i] = diff[i + 1] - diff[i]

        # Checking if all difference values are
        # same or not
        for i in range(1, length):
            if (diff[i] != diff[i - 1]):
                break

        # If some difference values
        # were not same
        if (i != length):
            break

    iteration = N - length

    # Padding terms instance of constant
    # difference at the end of array
    for i in range(length, length + terms):
        diff[i] = diff[i - 1]

    length += terms

    # Iterating to get actual sequence back
    for i in range(iteration):
        length += 1

        # Shifting all difference by one place
        for j in range(length - 1, -1, -1):
            diff[j] = diff[j - 1]

        # Copying actual first element
        diff[0] = first[len(first) - i - 1]

        # Converting difference of differences to
        # difference array
        for j in range(1, length):
            diff[j] = diff[j - 1] + diff[j]

    # Printing the result
    for i in range(length):
        print(diff[i], end = " ")

    print ()

# Driver code
if __name__ == "__main__":

    sequence = [ 8, 11, 16, 23 ]
    N = len(sequence)
    terms = 3

    nextTermsInSequence(sequence, N, terms)

# This code is contributed by chitranayal
```

## C#

```
// C# code to generate next terms
// of a given polynomial sequence
using System;
using System.Collections;
class GFG{

// Method to print next terms term of sequence
static void nextTermsInSequence(int []sequence,
                                int N, int terms)
{
    int []diff = new int[N + terms];

    // First copy the sequence itself
    // into diff array
    for(int i = 0; i < N; i++)
        diff[i] = sequence[i];

    //bool more = false;
    ArrayList first = new ArrayList();
    int len = N;

    // Loop until one difference remains
    // or all difference become constant
    while (len > 1)
    {

        // Keeping the first term of
        // sequence for later rebuilding
        first.Add(diff[0]);
        len--;

        // Converting the difference to
        // difference of differences
        for(int i = 0; i < len; i++)
            diff[i] = diff[i + 1] - diff[i];

        // Checking if all difference values
        // are same or not
        int j;
        for(j = 1; j < len; j++)
            if (diff[j] != diff[j - 1])
                break;

        // If some difference values
        // were not same
        if (j != len)
           break;
    }

    int iteration = N - len;

    // Padding terms instance of constant
    // difference at the end of array
    for(int i = len; i < len + terms; i++)
        diff[i] = diff[i - 1];

    len += terms;

    // Iterating to get actual sequence back
    for(int i = 0; i < iteration; i++)
    {
        len++;

        // Shifting all difference by one place
        for(int j = len - 1; j > 0; j--)
            diff[j] = diff[j - 1];

        // Copying actual first element
        diff[0] = (int)first[first.Count - i - 1];

        // Converting difference of differences
        // to difference array
        for(int j = 1; j < len; j++)
            diff[j] = diff[j - 1] + diff[j];
    }

    // Printing the result
    for(int i = 0; i < len; i++)
    {
        Console.Write(diff[i] + " ");
    }

    Console.Write("\n");
}

// Driver Code
public static void Main(string[] args)
{
    int []sequence = { 8, 11, 16, 23 };
    int N = sequence.Length;
    int terms = 3;

    nextTermsInSequence(sequence, N, terms);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript code to generate next terms
// of a given polynomial sequence

    // Method to print next terms term of sequence
    function nextTermsInSequence(sequence, N,terms)
    {
        let diff = new Array(N + terms);
        // First copy the sequence itself
        // into diff array
        for(let i = 0; i < N; i++)
            diff[i] = sequence[i];

        //bool more = false;
        let first=[];  
        let len = N;

        // Loop until one difference remains
        // or all difference become constant
        while (len > 1)
        {

            // Keeping the first term of
            // sequence for later rebuilding
            first.push(diff[0]);
            len--;

            // Converting the difference to
            // difference of differences
            for(let i = 0; i < len; i++)
                diff[i] = diff[i + 1] - diff[i];

            // Checking if all difference values
            // are same or not
            let j;
            for(j = 1; j < len; j++)
                if (diff[j] != diff[j - 1])
                    break;

            // If some difference values
            // were not same
            if (j != len)
               break;
        }
        let iteration = N - len;

        // Padding terms instance of constant
        // difference at the end of array
        for(let i = len; i < len + terms; i++)
            diff[i] = diff[i - 1];

        len += terms;

        // Iterating to get actual sequence back
        for(let i = 0; i < iteration; i++)
        {
            len++;

            // Shifting all difference by one place
            for(let j = len - 1; j > 0; j--)
                diff[j] = diff[j - 1];

            // Copying actual first element
            diff[0] = first[first.length - i - 1];

            // Converting difference of differences
            // to difference array
            for(let j = 1; j < len; j++)
                diff[j] = diff[j - 1] + diff[j];
        }

        // Printing the result
        for(let i = 0; i < len; i++)
        {
            document.write(diff[i] + " ");
        }

        document.write("<br>");
    }

    // Driver Code
    let sequence=[8, 11, 16, 23];
    let N = sequence.length;
    let terms = 3;
    nextTermsInSequence(sequence, N, terms);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
8 11 16 23 30 37 44
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。