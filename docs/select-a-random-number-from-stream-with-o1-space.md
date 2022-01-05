# 从流中选择一个随机数，用 O(1)空格

> 原文:[https://www . geesforgeks . org/select-a-random-number-from-stream-with-O1-space/](https://www.geeksforgeeks.org/select-a-random-number-from-stream-with-o1-space/)

给定一个数字流，从该流中生成一个随机数。您只能使用 O(1)空间，并且输入是流的形式，因此不能存储以前看到的数字。
那么我们如何从整个流中生成一个随机数，使得在有 O(1)个额外空间的情况下，挑选任意数的概率为 1/n 呢？这个问题是[油藏取样](https://www.geeksforgeeks.org/reservoir-sampling/)的一个变种。这里 k 的值是 1。
**1)** 将“计数”初始化为 0，“计数”用于存储到目前为止在流中看到的数字计数。
**2)** 对于流中的每个数字“x”，请执行以下操作
….. **a)** 将“计数”增加 1。
….. **b)** 如果计数为 1，将结果设置为 x，并返回结果。
….. **c)** 生成一个从 0 到“计数-1”的随机数。让生成的随机数为 i.
….. **d)** 如果 I 等于‘计数–1’，则将结果更新为 x。

## C++

```
// An efficient C++ program to randomly select
// a number from stream of numbers.
#include <bits/stdc++.h>
#include <time.h>
using namespace std;

// A function to randomly select a item
// from stream[0], stream[1], .. stream[i-1]
int selectRandom(int x)
{
    static int res; // The resultant random number
    static int count = 0; // Count of numbers visited
                          // so far in stream

    count++; // increment count of numbers seen so far

    // If this is the first element from stream,
    // return it
    if (count == 1)
        res = x;
    else
    {
        // Generate a random number from 0 to count - 1
        int i = rand() % count;

        // Replace the prev random number with
        // new number with 1/count probability
        if (i == count - 1)
            res = x;
    }
    return res;
}

// Driver Code
int main()
{
    int stream[] = {1, 2, 3, 4};
    int n = sizeof(stream) / sizeof(stream[0]);

    // Use a different seed value for every run.
    srand(time(NULL));
    for (int i = 0; i < n; ++i)
        cout << "Random number from first " << i + 1
             << " numbers is " << selectRandom(stream[i]) << endl;
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// An efficient C program to randomly select a number from stream of numbers.
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// A function to randomly select a item from stream[0], stream[1], .. stream[i-1]
int selectRandom(int x)
{
    static int res;    // The resultant random number
    static int count = 0;  //Count of numbers visited so far in stream

    count++;  // increment count of numbers seen so far

    // If this is the first element from stream, return it
    if (count == 1)
        res = x;
    else
    {
        // Generate a random number from 0 to count - 1
        int i = rand() % count;

        // Replace the prev random number with new number with 1/count probability
        if (i == count - 1)
            res  = x;
    }
    return res;
}

// Driver program to test above function.
int main()
{
    int stream[] = {1, 2, 3, 4};
    int n = sizeof(stream)/sizeof(stream[0]);

    // Use a different seed value for every run.
    srand(time(NULL));
    for (int i = 0; i < n; ++i)
        printf("Random number from first %d numbers is %d \n",
                                i+1, selectRandom(stream[i]));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//An efficient Java program to randomly select a number from stream of numbers.

import java.util.Random;

public class GFG
{
    static int res = 0;    // The resultant random number
    static int count = 0;  //Count of numbers visited so far in stream

    //A method to randomly select a item from stream[0], stream[1], .. stream[i-1]
    static int selectRandom(int x)
    {
        count++; // increment count of numbers seen so far

        // If this is the first element from stream, return it
        if (count == 1)
            res = x;
        else
        {
             // Generate a random number from 0 to count - 1
            Random r = new Random();
            int i = r.nextInt(count);

            // Replace the prev random number with new number with 1/count probability
            if(i == count - 1)
                res = x;
        }
        return res;
    }

    // Driver program to test above function.
    public static void main(String[] args)
    {
        int stream[] = {1, 2, 3, 4};
        int n = stream.length;
        for(int i = 0; i < n; i++)
            System.out.println("Random number from first " + (i+1) +
                               " numbers is " + selectRandom(stream[i]));
    }
}
//This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# An efficient python3 program
# to randomly select a number
# from stream of numbers.
import random

# A function to randomly select a item
# from stream[0], stream[1], .. stream[i-1]
def selectRandom(x):

    # The resultant random number
    res = 0;

    # Count of numbers visited
    # so far in stream
    count = 0;

    # increment count of numbers
    # seen so far
    count += 1;

    # If this is the first element
    # from stream, return it
    if (count == 1):
        res = x;
    else:

        # Generate a random number
        # from 0 to count - 1
        i = random.randrange(count);

        # Replace the prev random number
        # with new number with 1/count
        # probability
        if (i == count - 1):
            res = x;
    return res;

# Driver Code
stream = [1, 2, 3, 4];
n = len(stream);

# Use a different seed value
# for every run.
for i in range (n):
    print("Random number from first",
         (i + 1), "numbers is",
          selectRandom(stream[i]));

# This code is contributed by mits
```

## C#

```
// An efficient C# program to randomly
// select a number from stream of numbers.
using System;

class GFG
{
    // The resultant random number
    static int res = 0;

    // Count of numbers visited
    // so far in stream
    static int count = 0;

    // A method to randomly select
    // a item from stream[0],
    // stream[1], .. stream[i-1]
    static int selectRandom(int x)
    {
        // increment count of
        // numbers seen so far
        count++;

        // If this is the first
        // element from stream,
        // return it
        if (count == 1)
            res = x;
        else
        {
            // Generate a random number
            // from 0 to count - 1
            Random r = new Random();
            int i = r.Next(count);

            // Replace the prev random
            // number with new number
            // with 1/count probability
            if(i == count - 1)
                res = x;
        }
        return res;
    }

// Driver Code
public static void Main()
{
        int[] stream = {1, 2, 3, 4};
        int n = stream.Length;
        for(int i = 0; i < n; i++)
            Console.WriteLine("Random number from " +
                              "first {0} numbers is {1}" ,
                          i + 1, selectRandom(stream[i]));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient php program to randomly
// select a number from stream of numbers.

// A function to randomly select a item
// from stream[0], stream[1], .. stream[i-1]
function selectRandom($x)
{

    // The resultant random number
    $res;

    // Count of numbers visited so far
    // in stream
    $count = 0;

    // increment count of numbers seen
    // so far
    $count++;

    // If this is the first element
    // from stream, return it
    if ($count == 1)
        $res = $x;
    else
    {

        // Generate a random number from
        // 0 to count - 1
        $i = rand() % $count;

        // Replace the prev random number
        // with new number with 1/count
        // probability
        if (i == $count - 1)
            $res = $x;
    }
    return $res;
}

// Driver program to test above function.
    $stream = array(1, 2, 3, 4);
    $n = sizeof($stream)/sizeof($stream[0]);

    // Use a different seed value for
    // every run.
    srand(time(NULL));

    for ($i = 0; $i < $n; ++$i)
        echo "Random number from first ",
                   $i+1, "numbers is " ,
        selectRandom($stream[$i]), "\n" ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
//An efficient Javascript program to randomly select a number from stream of numbers.

let res = 0;    // The resultant random number
let count = 0;  //Count of numbers visited so far in stream

//A method to randomly select a item from stream[0], stream[1], .. stream[i-1]
function selectRandom(x)
{
    count++; // increment count of numbers seen so far

        // If this is the first element from stream, return it
        if (count == 1)
            res = x;
        else
        {
             // Generate a random number from 0 to count - 1

            let i = Math.floor(Math.random()*(count));

            // Replace the prev random number with new number with 1/count probability
            if(i == count - 1)
                res = x;
        }
        return res;
}

// Driver program to test above function.
let stream=[1, 2, 3, 4];
let n = stream.length;
for(let i = 0; i < n; i++)
    document.write("Random number from first " + (i+1) + " numbers is " + selectRandom(stream[i])+"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Random number from first 1 numbers is 1
Random number from first 2 numbers is 1
Random number from first 3 numbers is 3
Random number from first 4 numbers is 4
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
**这是如何工作的**
我们需要证明每一个元素都是以 1/n 的概率被拾取的，其中 n 是到目前为止看到的物品数量。对于每一个新的流项 x，我们从 0 到‘count-1’之间选取一个随机数，如果选取的数是‘count-1’，我们用 x 替换先前的结果。
为了简化证明，让我们首先考虑最后一个元素，最后一个元素用 1/n 的概率替换先前存储的结果。所以得到最后一个元素作为结果的概率是 1/n
现在我们来说第二个最后一个元素。当第二个最后一个元素第一次处理时，它替换前一个结果的概率是 1/(n-1)。考虑第 n 项时，前一个结果保留的概率是(n-1)/n，所以最后一次迭代中第二个最后一个元素被拾取的概率是[1/(n-1)] * [(n-1)/n]，也就是 1/n.
同样，我们可以对第三个最后一个元素等进行证明。
参考资料:
[油藏取样](https://www.geeksforgeeks.org/reservoir-sampling/)

**方法 2:** 用 numpy random.choice()方法从流中生成一个随机数。

## 蟒蛇 3

```
import numpy as np

# initializing list
stream = [1, 4, 5, 2, 7]

# using random.choice() to
# get a random number
random_num = np.random.choice(stream)

# printing random number
print("random number is ",random_num)
```

**输出:**

```
7
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*