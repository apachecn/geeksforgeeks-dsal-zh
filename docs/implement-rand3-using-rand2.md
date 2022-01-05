# 使用 rand2()

实现 rand3()

> 原文:[https://www.geeksforgeeks.org/implement-rand3-using-rand2/](https://www.geeksforgeeks.org/implement-rand3-using-rand2/)

给定一个以相等概率返回 0 或 1 的函数 rand2()，使用以相等概率返回 0、1 或 2 的 rand2()实现 rand3()。尽量减少对 rand2()方法的调用次数。此外，不允许使用任何其他库函数和浮点运算。

思路是用表达式 **2 * rand2() + rand2()** 。它以相等的概率返回 0，1，2，3。为了使它以相等的概率返回 0，1，2，我们消除了不需要的事件 3。
以下是上述想法的实现–

## C++

```
// C++ Program to print 0, 1 or 2 with equal
// probability
#include <iostream>
using namespace std;

// Random Function to that returns 0 or 1 with
// equal probability
int rand2()
{
    // rand() function will generate odd or even
    // number with equal probability. If rand()
    // generates odd number, the function will
    // return 1 else it will return 0.
    return rand() & 1;
}

// Random Function to that returns 0, 1 or 2 with
// equal probability 1 with 75%
int rand3()
{
    // returns 0, 1, 2 or 3 with 25% probability
    int r = 2 * rand2() + rand2();

    if (r < 3)
        return r;

    return rand3();
}

// Driver code to test above functions
int main()
{
    // Initialize random number generator
    srand(time(NULL));

    for(int i = 0; i < 100; i++)
        cout << rand3();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print 0, 1 or 2 with equal 
// probability
import java.util.Random;
class GFG
{

  // Random Function to that returns 0 or 1 with
  // equal probability
  static int rand2()
  {

    // rand() function will generate odd or even
    // number with equal probability. If rand()
    // generates odd number, the function will
    // return 1 else it will return 0.
    Random rand = new Random(); 
    return (rand.nextInt() & 1);
  }

  // Random Function to that returns 0, 1 or 2 with 
  // equal probability 1 with 75%
  static int rand3()
  {

    // returns 0, 1, 2 or 3 with 25% probability
    int r = 2 * rand2() + rand2();

    if (r < 3)
      return r;
    return rand3();
  }

  // Driver code
  public static void main(String[] args) {
    for(int i = 0; i < 100; i++)
      System.out.print(rand3());
  }
}
// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 Program to print 0, 1 or 2 with equal
# Probability

import random
# Random Function to that returns 0 or 1 with
# equal probability

def rand2():

    # randint(0,100) function will generate odd or even
    # number [1,100] with equal probability. If rand()
    # generates odd number, the function will
    # return 1 else it will return 0
    tmp=random.randint(1,100)
    return tmp%2

# Random Function to that returns 0, 1 or 2 with
# equal probability 1 with 75%
def rand3():

    # returns 0, 1, 2 or 3 with 25% probability
    r = 2 * rand2() + rand2()
    if r<3:
        return r
    return rand3()

# Driver code to test above functions
if __name__=='__main__':
    for i in range(100):
        print(rand3(),end="")

#This code is contributed by sahilshelangia
```

## C#

```
// C# Program to print 0, 1 or 2 with equal 
// probability
using System;
class GFG
{

  // Random Function to that returns 0 or 1 with
  // equal probability
  static int rand2()
  {

    // rand() function will generate odd or even
    // number with equal probability. If rand()
    // generates odd number, the function will
    // return 1 else it will return 0.
    Random rand = new Random();
    return (rand.Next() & 1);
  }

  // Random Function to that returns 0, 1 or 2 with 
  // equal probability 1 with 75%
  static int rand3()
  {

    // returns 0, 1, 2 or 3 with 25% probability
    int r = 2 * rand2() + rand2();

    if (r < 3)
      return r;
    return rand3();
  }

  // Driver code
  static void Main()
  {
    for(int i = 0; i < 100; i++)
      Console.Write(rand3());
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print 0, 1 or
// 2 with equal probability

// Random Function to that
// returns 0 or 1 with
// equal probability
function rand2()
{
    // rand() function will generate
    // odd or even number with equal
    // probability. If rand() generates
    // odd number, the function will
    // return 1 else it will return 0.
    return rand() & 1;
}

// Random Function to that
// returns 0, 1 or 2 with
// equal probability 1 with 75%
function rand3()
{
    // returns 0, 1, 2 or 3
    // with 25% probability
    $r = 2 * rand2() + rand2();

    if ($r < 3)
        return $r;

    return rand3();
}

// Driver Code

// Initialize random
// number generator
srand(time(NULL));

for($i = 0; $i < 100; $i++)
    echo rand3();

// This code is contributed by aj_36
?>
```

**输出:**

```
2111011101112002111002020210112022022022211100100121202021102100010200121121210122011022111020
```

**另一种解决方案–**
如果 x = rand2()和 y = rand2()，x + y 将以 25%的概率返回 0 和 2，以 50%的概率返回 1。为了使 1 的概率等于 0 和 2 的概率，即 25%，我们消除了一个导致 x + y = 1 的不良事件，即(x = 1，y = 0)或(x = 0，y = 1)。

```
int rand3()
{
    int x, y;

    do {
        x = rand2();
        y = rand2();
    } while (x == 0 && y == 1);

    return x + y;
}
```

请注意，以上解决方案在我们每次运行时都会产生不同的结果。
本文由**阿迪亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。