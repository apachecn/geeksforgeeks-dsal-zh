# 生成交替增减数组

> 原文:[https://www . geeksforgeeks . org/生成一个交替递增递减的数组/](https://www.geeksforgeeks.org/generate-an-alternate-increasing-and-decreasing-array/)

给定一个大小为 **N** 的字符串**字符串**，该字符串仅包含两种类型的字符，即**“I”**或**“D”**。任务是生成一个数组 **arr[0，1，.。尺寸为 **N + 1** 的**满足以下条件:

*   如果字符串[I]= =“I”，则 arr[i] < arr[i+1]
*   如果字符串[i] == "D "，则 arr[i] > arr[i+1]

**示例:**

> **输入:** str = "IDID"
> **输出:** 0 4 1 3 2
> **解释:**T8】str[0]= " I "因此 arr[0]<arr[1]
> str[1]= " D "因此 arr[1]>arr[2]
> str[2]= " I "因此 arr[2]<arr[3]
> str[3]= " D "因此
> 
> **输入:**str = " III "
> T3】输出: 0 1 2 3

**进场:**

1.  将变量**初始化为 **0** ，将**结束**初始化为 **N** 。**
2.  迭代整个数组。
3.  如果**str【I】**= =**“I”**，则在**arr【I】**处分配 **START** ，并增加 **START** 。
4.  如果**str【I】**= =**“D”**，则在**分配**END**arr【I】**，递减 **END** 。
5.  现在数组的最后一个元素没有赋值，所以在**A【N】**处赋值 **START** 。

下面是该方法的实现。

## C++

```
// C++ program to Generate an increasing
// and decreasing array

#include <iostream>
using namespace std;

// Function that returns generated array
int* DiStirngMatch(string Str)
{
    int N = Str.length();

    // Dynamically allocate array
    int* arr = new int[N];

    // START=0, END=N
    int START = 0, END = N;

    // iterate over array
    for (int i = 0; i < N; i++) {

        // if Str[i]=='I' assign arr[i]
        // as START and increment START
        if (Str[i] == 'I')
            arr[i] = START++;

        // if str[i]=='D' assign arr[i]
        // as END and decrement END
        if (Str[i] == 'D')
            arr[i] = END--;
    }

    // assign A[N] as START
    arr[N] = START;

    // return starting
    // address of array A
    return arr;
}

// Driver Program
int main()
{
    string Str = "IDID";
    int N = Str.length();
    int* ptr = DiStirngMatch(Str);
    for (int i = 0; i <= N; i++)
        cout << ptr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate an increasing
// and decreasing array
class GFG{

// Function that returns generated array
static int []DiStirngMatch(String Str)
{
    int N = Str.length();

    // Dynamically allocate array
    int []arr = new int[N + 1];

    // START=0, END=N
    int START = 0, END = N;

    // Iterate over array
    for(int i = 0; i < N; i++)
    {

        // if Str[i]=='I' assign arr[i]
        // as START and increment START
        if (Str.charAt(i) == 'I')
            arr[i] = START++;

        // if str[i]=='D' assign arr[i]
        // as END and decrement END
        if (Str.charAt(i) == 'D')
            arr[i] = END--;
    }

    // Assign A[N] as START
    arr[N] = START;

    // Return starting
    // address of array A
    return arr;
}

// Driver code
public static void main(String[] args)
{
    String Str = "IDID";
    int N = Str.length();
    int[] ptr = DiStirngMatch(Str);

    for(int i = 0; i <= N; i++)
        System.out.print(ptr[i] + " ");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to generate an
# increasing and decreasing array

# Function that returns generated array
def DiStirngMatch(Str):

    N = len(Str)

    # Dynamically allocate array
    arr = (N + 1) * [0]

    # START, END= 0 ,N
    START, END = 0, N

    # Iterate over array
    for i in range (N):

        # If Str[i]=='I' assign arr[i]
        # as START and increment START
        if (Str[i] == 'I'):
            arr[i] = START
            START += 1

        # If str[i]=='D' assign arr[i]
        # as END and decrement END
        if (Str[i] == 'D'):
            arr[i] = END
            END -= 1

    # Assign A[N] as START
    arr[N] = START

    # Return starting
    # address of array A
    return arr

# Driver code
if __name__ == "__main__":

    Str = "IDID"
    N = len(Str)
    ptr = DiStirngMatch(Str)

    for i in range (N + 1):
        print(ptr[i], end = " ")

# This code is contributed by chitranayal
```

## C#

```
// C# program to generate an increasing
// and decreasing array
using System;

class GFG{

// Function that returns generated array
static int []DiStirngMatch(String Str)
{
    int N = Str.Length;

    // Dynamically allocate array
    int []arr = new int[N + 1];

    // START=0, END=N
    int START = 0, END = N;

    // Iterate over array
    for(int i = 0; i < N; i++)
    {

        // if Str[i]=='I' assign arr[i]
        // as START and increment START
        if (Str[i] == 'I')
            arr[i] = START++;

        // if str[i]=='D' assign arr[i]
        // as END and decrement END
        if (Str[i] == 'D')
            arr[i] = END--;
    }

    // Assign A[N] as START
    arr[N] = START;

    // Return starting
    // address of array A
    return arr;
}

// Driver code
public static void Main(String[] args)
{
    String Str = "IDID";
    int N = Str.Length;
    int[] ptr = DiStirngMatch(Str);

    for(int i = 0; i <= N; i++)
        Console.Write(ptr[i] + " ");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to Generate an increasing
// and decreasing array

// Function that returns generated array
function DiStirngMatch( Str)
{
    var N = Str.length;

    // Dynamically allocate array
    var arr = Array(N).fill(0);

    // START=0, END=N
    var START = 0, END = N;

    // iterate over array
    for (var i = 0; i < N; i++) {

        // if Str[i]=='I' assign arr[i]
        // as START and increment START
        if (Str[i] == 'I')
            arr[i] = START++;

        // if str[i]=='D' assign arr[i]
        // as END and decrement END
        if (Str[i] == 'D')
            arr[i] = END--;
    }

    // assign A[N] as START
    arr[N] = START;

    // return starting
    // address of array A
    return arr;
}

// Driver Program
var Str = "IDID";
var N = Str.length;
var ptr = DiStirngMatch(Str);
for (var i = 0; i <= N; i++)
    document.write( ptr[i] + " ");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
0 4 1 3 2
```

***时间复杂度:** O (N)*
***辅助空间:** O (N)*