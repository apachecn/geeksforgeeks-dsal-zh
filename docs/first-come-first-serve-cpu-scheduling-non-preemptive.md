# 先到先得——CPU 调度|(非抢先)

> 原文:[https://www . geesforgeks . org/先到先得-CPU-调度-非抢先/](https://www.geeksforgeeks.org/first-come-first-serve-cpu-scheduling-non-preemptive/)

**先决条件:** [操作系统中的 CPU 调度](https://www.geeksforgeeks.org/cpu-scheduling-in-operating-systems/)
给定 **N** 个进程，它们的到达时间为[] 处的**，突发时间为 **bt[]** 。任务是使用[先来先服务(FCFS)](https://www.geeksforgeeks.org/program-for-fcfs-cpu-scheduling-set-1/) 算法找到每个进程的等待时间和平均等待时间。
**示例**** 

> **输入:** N = 5，at[] = {0，1，2，3，4}，bt[] = {4，3，1，2，5}
> 
> <figure class="table">
> 
> | 处理 | 到达时间 | 突发时间 |
> | --- | --- | --- |
> | 第一亲代 | Zero | four |
> | P2 | one | three |
> | P3 | Two | one |
> | P4 | three | Two |
> | 孕烯醇酮 | four | five |
> 
> **输出:**每个进程的等待时间为:
> 
> <figure class="table">
> 
> | 处理 | 等待时间 |
> | --- | --- |
> | 第一亲代 | Zero |
> | P2 | three |
> | P3 | five |
> | P4 | five |
> | 孕烯醇酮 | six |
> 
> 平均等待时间= 3.8
> 
> </figure>
> 
> </figure>

**进场:**

1.  第一个进程的等待时间为 0，因为它是首先执行的。
2.  即将到来的过程的等待时间可以通过下式计算:

```
wt[i] =  ( at[i - 1] + bt[i - 1] + wt[i - 1] ) - at[i]
```

1.  其中**wt【I】**=当前进程
    **在【I-1】**的等待时间=前一进程
    **Bt【I-1】**的到达时间=前一进程
    **wt【I-1】**=前一进程
    **在【I】**的等待时间=当前进程
    的到达时间
2.  平均等待时间可以通过
    计算

```
Average Waiting Time = (sum of all waiting time)/(Number of processes)
```

以下是上述方法的实现:

## C++

```
// C++ program to Calculate Waiting
// Time for given Processes
#include <iostream>
using namespace std;

// Function to Calculate waiting time
// and average waiting time
void CalculateWaitingTime(int at[],
                          int bt[], int N)
{

    // Declare the array for waiting
    // time
    int wt[N];

    // Waiting time for first process
    // is 0
    wt[0] = 0;

    // Print waiting time process 1
    cout << "P.No.\tArrival Time\t"
         << "Burst Time\tWaiting Time\n";
    cout << "1"
         << "\t\t" << at[0] << "\t\t"
         << bt[0] << "\t\t" << wt[0] << endl;

    // Calculating waiting time for
    // each process from the given
    // formula
    for (int i = 1; i < 5; i++) {
        wt[i] = (at[i - 1] + bt[i - 1] + wt[i - 1]) - at[i];

        // Print the waiting time for
        // each process
        cout << i + 1 << "\t\t" << at[i]
             << "\t\t" << bt[i] << "\t\t"
             << wt[i] << endl;
    }

    // Declare variable to calculate
    // average
    float average;
    float sum = 0;

    // Loop to calculate sum of all
    // waiting time
    for (int i = 0; i < 5; i++) {
        sum = sum + wt[i];
    }

    // Find average waiting time
    // by dividing it by no. of process
    average = sum / 5;

    // Print Average Waiting Time
    cout << "Average waiting time = "
         << average;
}

// Driver code
int main()
{
    // Number of process
    int N = 5;

    // Array for Arrival time
    int at[] = { 0, 1, 2, 3, 4 };

    // Array for Burst Time
    int bt[] = { 4, 3, 1, 2, 5 };

    // Function call to find
    // waiting time
    CalculateWaitingTime(at, bt, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Calculate Waiting
// Time for given Processes
class GFG
{

// Function to Calculate waiting time
// and average waiting time
static void CalculateWaitingTime(int at[],
                          int bt[], int N)
{

    // Declare the array for waiting
    // time
    int []wt = new int[N];

    // Waiting time for first process
    // is 0
    wt[0] = 0;

    // Print waiting time process 1
    System.out.print("P.No.\tArrival Time\t"
        + "Burst Time\tWaiting Time\n");
    System.out.print("1"
        + "\t\t" +  at[0]+ "\t\t"
         + bt[0]+ "\t\t" +  wt[0] +"\n");

    // Calculating waiting time for
    // each process from the given
    // formula
    for (int i = 1; i < 5; i++) {
        wt[i] = (at[i - 1] + bt[i - 1] + wt[i - 1]) - at[i];

        // Print the waiting time for
        // each process
        System.out.print(i + 1+ "\t\t" +  at[i]
            + "\t\t" +  bt[i]+ "\t\t"
             + wt[i] +"\n");
    }

    // Declare variable to calculate
    // average
    float average;
    float sum = 0;

    // Loop to calculate sum of all
    // waiting time
    for (int i = 0; i < 5; i++) {
        sum = sum + wt[i];
    }

    // Find average waiting time
    // by dividing it by no. of process
    average = sum / 5;

    // Print Average Waiting Time
    System.out.print("Average waiting time = "
         + average);
}

// Driver code
public static void main(String[] args)
{
    // Number of process
    int N = 5;

    // Array for Arrival time
    int at[] = { 0, 1, 2, 3, 4 };

    // Array for Burst Time
    int bt[] = { 4, 3, 1, 2, 5 };

    // Function call to find
    // waiting time
    CalculateWaitingTime(at, bt, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to Calculate Waiting
# Time for given Processes

# Function to Calculate waiting time
# and average waiting time
def CalculateWaitingTime(at, bt, N):

    # Declare the array for waiting
    # time
    wt = [0]*N;

    # Waiting time for first process
    # is 0
    wt[0] = 0;

    # Prwaiting time process 1
    print("P.No.\tArrival Time\t" , "Burst Time\tWaiting Time");
    print("1" , "\t\t" , at[0] , "\t\t" , bt[0] , "\t\t" , wt[0]);

    # Calculating waiting time for
    # each process from the given
    # formula
    for i in range(1,5):
        wt[i] = (at[i - 1] + bt[i - 1] + wt[i - 1]) - at[i];

        # Print the waiting time for
        # each process
        print(i + 1 , "\t\t" , at[i] , "\t\t" , bt[i] , "\t\t" , wt[i]);

    # Declare variable to calculate
    # average
    average = 0.0;
    sum = 0;

    # Loop to calculate sum of all
    # waiting time
    for i in range(5):
        sum = sum + wt[i];

    # Find average waiting time
    # by dividing it by no. of process
    average = sum / 5;

    # PrAverage Waiting Time
    print("Average waiting time = " , average);

# Driver code
if __name__ == '__main__':
    # Number of process
    N = 5;

    # Array for Arrival time
    at = [ 0, 1, 2, 3, 4 ];

    # Array for Burst Time
    bt = [ 4, 3, 1, 2, 5 ];

    # Function call to find
    # waiting time
    CalculateWaitingTime(at, bt, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to Calculate Waiting
// Time for given Processes
using System;

class GFG
{

// Function to Calculate waiting time
// and average waiting time
static void CalculateWaitingTime(int []at,
                          int []bt, int N)
{

    // Declare the array for waiting
    // time
    int []wt = new int[N];

    // Waiting time for first process
    // is 0
    wt[0] = 0;

    // Print waiting time process 1
    Console.Write("P.No.\tArrival Time\t"
        + "Burst Time\tWaiting Time\n");
    Console.Write("1"
        + "\t\t" +  at[0]+ "\t\t"
         + bt[0]+ "\t\t" +  wt[0] +"\n");

    // Calculating waiting time for
    // each process from the given
    // formula
    for (int i = 1; i < 5; i++) {
        wt[i] = (at[i - 1] + bt[i - 1] + wt[i - 1]) - at[i];

        // Print the waiting time for
        // each process
        Console.Write(i + 1+ "\t\t" +  at[i]
            + "\t\t" +  bt[i]+ "\t\t"
             + wt[i] +"\n");
    }

    // Declare variable to calculate
    // average
    float average;
    float sum = 0;

    // Loop to calculate sum of all
    // waiting time
    for (int i = 0; i < 5; i++) {
        sum = sum + wt[i];
    }

    // Find average waiting time
    // by dividing it by no. of process
    average = sum / 5;

    // Print Average Waiting Time
    Console.Write("Average waiting time = "
         + average);
}

// Driver code
public static void Main(String[] args)
{
    // Number of process
    int N = 5;

    // Array for Arrival time
    int []at = { 0, 1, 2, 3, 4 };

    // Array for Burst Time
    int []bt = { 4, 3, 1, 2, 5 };

    // Function call to find
    // waiting time
    CalculateWaitingTime(at, bt, N);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
P.No.    Arrival Time    Burst Time    Waiting Time
1        0        4        0
2        1        3        3
3        2        1        5
4        3        2        5
5        4        5        6
Average waiting time = 3.8
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)