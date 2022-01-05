# 程序求简单均线

> 原文:[https://www . geesforgeks . org/program-find-simple-move-average/](https://www.geeksforgeeks.org/program-find-simple-moving-average/)

**简单移动平均线**是从某个 t 时间段的数据中获得的平均值。在正常平均值中，它的值随着数据的变化而变化，但在这种平均值中，它也随着时间间隔而变化。我们得到某个周期 t 的平均值，然后我们去掉一些以前的数据。我们再次得到新的平均值，这个过程继续。这就是为什么它是移动平均线。这在金融市场上有很大的应用。

示例:

```
Input : { 1, 3, 5, 6, 8 } 
        Period = 3
Output :New number added is 1.0, SMA = 0.3333333333333333
        New number added is 3.0, SMA = 1.3333333333333333
        New number added is 5.0, SMA = 3.0
        New number added is 6.0, SMA = 4.666666666666667
        New number added is 8.0, SMA = 6.333333333333333

```

**逼近**
给定一系列数字和一个固定的子集大小，移动平均线的第一个元素通过取数字系列的初始固定子集的平均值获得。然后通过*【前移】修改子集，即排除数列的第一个数，包含子集的下一个值。*

*这是一个计算简单移动平均线的 java 程序。* 

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java program to calculate
// Simple Moving Average
import java.util.*;

public class SimpleMovingAverage {

    // queue used to store list so that we get the average
    private final Queue<Double> Dataset = new LinkedList<Double>();
    private final int period;
    private double sum;

    // constructor to initialize period
    public SimpleMovingAverage(int period)
    {
        this.period = period;
    }

    // function to add new data in the
    // list and update the sum so that
    // we get the new mean
    public void addData(double num)
    {
        sum += num;
        Dataset.add(num);

        // Updating size so that length
        // of data set should be equal
        // to period as a normal mean has
        if (Dataset.size() > period)
        {
            sum -= Dataset.remove();
        }
    }

    // function to calculate mean
    public double getMean()
    {
        return sum / period;
    }

    public static void main(String[] args)
    {
        double[] input_data = { 1, 3, 5, 6, 8,
                                12, 18, 21, 22, 25 };
        int per = 3;
        SimpleMovingAverage obj = new SimpleMovingAverage(per);
        for (double x : input_data) {
            obj.addData(x);
            System.out.println("New number added is " +
                                x + ", SMA = " + obj.getMean());
        }
    }
}*
```

## *C#*

```
*// C# program to calculate
// Simple Moving Average
using System;
using System.Collections.Generic; 

public class SimpleMovingAverage 
{

    // queue used to store list so that we get the average
    private Queue<Double> Dataset = new Queue<Double>();
    private int period;
    private double sum;

    // constructor to initialize period
    public SimpleMovingAverage(int period)
    {
        this.period = period;
    }

    // function to add new data in the
    // list and update the sum so that
    // we get the new mean
    public void addData(double num)
    {
        sum += num;
        Dataset.Enqueue(num);

        // Updating size so that length
        // of data set should be equal
        // to period as a normal mean has
        if (Dataset.Count > period)
        {
            sum -= Dataset.Dequeue();
        }
    }

    // function to calculate mean
    public double getMean()
    {
        return sum / period;
    }

    // Driver code
    public static void Main(String[] args)
    {
        double[] input_data = { 1, 3, 5, 6, 8,
                                12, 18, 21, 22, 25 };
        int per = 3;
        SimpleMovingAverage obj = new SimpleMovingAverage(per);
        foreach (double x in input_data) {
            obj.addData(x);
            Console.WriteLine("New number added is " +
                                x + ", SMA = " + obj.getMean());
        }
    }
}

// This code contributed by Rajput-Ji*
```

***输出:***

```
*New number added is 1.0, SMA = 0.3333333333333333
New number added is 3.0, SMA = 1.3333333333333333
New number added is 5.0, SMA = 3.0
New number added is 6.0, SMA = 4.666666666666667
New number added is 8.0, SMA = 6.333333333333333
New number added is 12.0, SMA = 8.666666666666666
New number added is 18.0, SMA = 12.666666666666666
New number added is 21.0, SMA = 17.0
New number added is 22.0, SMA = 20.333333333333332
New number added is 25.0, SMA = 22.666666666666668* 
```

*参考文献:
[维基](https://en.wikipedia.org/wiki/Moving_average#Simple_moving_average)*