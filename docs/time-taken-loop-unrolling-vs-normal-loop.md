# 循环展开与正常循环所花费的时间

> 原文:[https://www . geesforgeks . org/time-take-loop-unrolling-vs-normal-loop/](https://www.geeksforgeeks.org/time-taken-loop-unrolling-vs-normal-loop/)

我们已经讨论了[循环展开](https://www.geeksforgeeks.org/loop-unrolling/)。其思想是通过对循环语句进行分组来提高性能，从而减少循环控制指令和循环测试指令的数量

## C++

```
// CPP program to compare normal loops and
// loops with unrolling technique
#include <iostream>
#include <time.h>
using namespace std;

int main() {

  // n is 8 lakhs
  int n = 800000;

  // t to note start time
  clock_t t = clock();

  // to store the sum
  long long int sum = 0;

  // Normal loop
  for (int i = 1; i <= n; i++)
    sum += i;

  // to mark end time
  t = clock() - t;

  cout << "sum is: " << sum << endl;
  cout << "time taken by normal loops:"
      "(float)t / CLOCKS_PER_SEC << " seconds"
       << endl;

  // to mark start time of unrolling
  t = clock();

  // Unrolling technique (assuming that
  // n is a multiple of 8).
  sum = 0;
  for (int i = 1; i <= n; i += 8) {
    sum += i sum += (i + 1);
    sum += (i + 2);
    sum += (i + 3);
    sum += (i + 4);
    sum += (i + 5);
    sum += (i + 6);
    sum += (i + 7);
  }

  // to mark the end of loop
  t = clock() - t;

  cout << "Sum is: " << sum << endl;
  cout << "Time taken by unrolling: "
       "(float)t / CLOCKS_PER_SEC << " seconds";
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compare 
// normal loops and loops 
// with unrolling technique

class GFG
{

    public static void main(String[] args)
    {

    // n is 8 lakhs
    int n = 800000;

    // t to note start time
    double t = (double)System.nanoTime();

    // to store the sum
    long sum = 0;

    // Normal loop
    for (int i = 1; i <= n; i++)
        sum += i;

    // to mark end time
    t = (double)System.nanoTime() - t;

    System.out.println("sum is: "+
        Double.toString(sum));
    System.out.println("time taken by normal loops:" +
        Double.toString(t / Math.pow(10.0, 9.0)));

    // to mark start time
    // of unrolling
    t = (double)System.nanoTime();

    // Unrolling technique 
    // (assuming that n is
    // a multiple of 8).
    sum = 0;
    for (int i = 1; i <= n; i += 8) 
    {
        sum += i ;
        sum += (i + 1);
        sum += (i + 2);
        sum += (i + 3);
        sum += (i + 4);
        sum += (i + 5);
        sum += (i + 6);
        sum += (i + 7);
    }

    // to mark the end of loop
    t = (double)System.nanoTime() - t;

    System.out.println("sum is: " +
        Double.toString(sum));
    System.out.println("time taken by normal loops:" + 
        Double.toString(t / Math.pow(10.0, 9.0)));
    }
}

// This code is contributed 
// by Harshit Saini
```

## 蟒蛇 3

```
# Python program to compare 
# normal loops and loops 
# with unrolling technique
from timeit import default_timer as clock

if __name__ == "__main__":

    # n is 8 lakhs
    n = 800000;

    #t to note start time
    t = clock()

    # to store the sum
    sum = 0

    # Normal loop
    for i in range(1, n + 1):
        sum += i

    # to mark end time
    t = clock() - t

    print("sum is: " + str(sum))
    print("time taken by normal " + 
                 "loops:" + str(t))

    # to mark start 
    # time of unrolling
    t = clock()

    # Unrolling technique 
    # (assuming that n is 
    # a multiple of 8).
    sum = 0
    for i in range(1, n + 1, 8):
        sum += i
        sum += (i + 1)
        sum += (i + 2)
        sum += (i + 3)
        sum += (i + 4)
        sum += (i + 5)
        sum += (i + 6)
        sum += (i + 7)

    # to mark the 
    # end of loop
    t = clock() - t

    print("Sum is: " + str(sum))
    print("Time taken by unrolling: " + 
                              str(t))

# This code is contributed
# by Harshit Saini
```

## C#

```
// C# program to compare 
// normal loops and loops 
// with unrolling technique
using System;
using System.Diagnostics; 

class GFG
{
    private static double nanoTime() 
    {
        long nano = 10000L * Stopwatch.GetTimestamp();
        nano /= TimeSpan.TicksPerMillisecond;
        nano *= 100L;
        return nano;
    }
    public static void Main(String[] args)
    {

        // n is 8 lakhs
        int n = 800000;

        // t to note start time
        double t = nanoTime();

        // to store the sum
        long sum = 0;

        // Normal loop
        for (int i = 1; i <= n; i++)
            sum += i;

        // to mark end time
        t = nanoTime() - t;

        Console.WriteLine("sum is: "+ sum);
        Console.WriteLine("time taken by normal loops:" +
                              (t / Math.Pow(10.0, 9.0)));

        // to mark start time
        // of unrolling
        t = nanoTime();

        // Unrolling technique 
        // (assuming that n is
        // a multiple of 8).
        sum = 0;
        for (int i = 1; i <= n; i += 8) 
        {
            sum += i ;
            sum += (i + 1);
            sum += (i + 2);
            sum += (i + 3);
            sum += (i + 4);
            sum += (i + 5);
            sum += (i + 6);
            sum += (i + 7);
        }

        // to mark the end of loop
        t = nanoTime() - t;

        Console.WriteLine("sum is: " + (sum));
        Console.WriteLine("time taken by normal loops:" + 
                              (t / Math.Pow(10.0, 9.0)));
    }
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
Sum is: 320000400000
Time taken: 0.002645 seconds

Sum is: 320000400000
Time taken: 0.001799 seconds

```

普通线圈和线圈展开的比较请参考[线圈展开](https://www.geeksforgeeks.org/loop-unrolling/)。