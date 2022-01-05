# 标准正态分布(SND)–Java 程序

> 原文:[https://www . geesforgeks . org/standard-normal-distribution-snd/](https://www.geeksforgeeks.org/standard-normal-distribution-snd/)

标准正态分布是正态分布的特例。当一个正态随机变量的**均值为 0** 且**标准差为 1** 时，就会出现这种情况。标准正态分布的正态随机变量称为**标准分数**或 **z 分数**。
从正态分布到标准正态分布值的转换通过以下公式进行:

```
Z = (X - u) / s
where:
Z = value on the standard normal distribution
X = value on the original distribution
u = mean of the original distribution
s = standard deviation of the original distribution

```

**代码–**

```
// Java code to demonstrate the naive method
// of finding Z-value

import java.io.*;
import java.util.*;

class SDN {
    public static void main(String[] args)
    {

        // initialization of variables
        double Z, X, s, u;
        X = 26;
        u = 50;
        s = 10;

        // master formula
        Z = (X - u) / s;

        // print the z-value
        System.out.println("the Z-value obtained is: " + Z);
    }
}
```

**输出–**

```
the Z-value obtained is: -2.4

```

**生成随机标准正态函数–使用 nextGaussian()在 Java 中:**
使用 **nextGaussian()** 方法获得下一个随机正态分布的双值，平均值为 0.0，标准差为 1.0。

```
Declaration :
public double nextGaussian()
Parameters :
NA
Return Value :
The method call returns the random, Normally distributed double value
with mean 0.0 and standard deviation 1.0.
Exception :
NA

```

下面的例子展示了 java.util.Random.nextGaussian()的用法:

**代码–**

```
// Java code to demonstrate the working
// of nextGaussian()
import java.util.*;

public class NextGaussian {

    public static void main(String[] args)
    {

        // create random object
        Random ran = new Random();

        // generating integer
        double nxt = ran.nextGaussian();

        // Printing the random Number
        System.out.println("The next Gaussian value generated is : " + nxt);
    }
}
```

**输出–**

```
The next Gaussian value generated is : -0.24283691098606316

```