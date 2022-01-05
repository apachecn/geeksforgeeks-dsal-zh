# 写一个函数，根据给定的概率生成 3 个数字中的一个

> 原文:[https://www . geesforgeks . org/write-a-function-to-generate-3-numbers-根据给定概率/](https://www.geeksforgeeks.org/write-a-function-to-generate-3-numbers-according-to-given-probabilities/)

给你一个函数 rand(a，b)，它生成介于[a，b]之间的等概率随机数。用给定的 rand(a，b)函数生成 3 个概率为 P(x)，P(y)，P(z)的数字 x，y，z，使得 P(x) + P(y) + P(z) = 1。
想法是利用所提供的 rand(a，b)的等概率特征。 ***假设给定的概率是百分比形式，例如 P(x)=40%，P(y)=25%，P(z)=35%。*** 。

以下是详细步骤。
**1)** 生成一个 1 到 100 之间的随机数。因为它们是等概率的，所以每个数出现的概率是 1/100。
**2)** 以下是生成随机数“r”需要注意的一些要点。
a)‘r’小于或等于 P(x)，概率 P(x)/100。
b)‘r’大于 P(x)，小于或等于 P(x) + P(y)，P(y)/100。
c)‘r’大于 P(x) + P(y)且小于或等于 100(或 P(x) + P(y) + P(z))，概率 P(z)/100。

## C

```
// This function generates 'x' with probability px/100, 'y' with
// probability py/100  and 'z' with probability pz/100:
// Assumption: px + py + pz = 100 where px, py and pz lie
// between 0 to 100
int random(int x, int y, int z, int px, int py, int pz)
{      
        // Generate a number from 1 to 100
        int r = rand(1, 100);

        // r is smaller than px with probability px/100
        if (r <= px)
            return x;

         // r is greater than px and smaller than or equal to px+py
         // with probability py/100
        if (r <= (px+py))
            return y;

         // r is greater than px+py and smaller than or equal to 100
         // with probability pz/100
        else
            return z;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// This function generates 'x' with probability px/100, 'y'
// with probability py/100  and 'z' with probability pz/100:
// Assumption: px + py + pz = 100 where px, py and pz lie
// between 0 to 100
static int random(int x, int y, int z, int px, int py,
                  int pz)
{
    // Generate a number from 1 to 100
    int r = (int)(Math.random() * 100);

    // r is smaller than px with probability px/100
    if (r <= px)
        return x;

    // r is greater than px and smaller than or equal to
    // px+py with probability py/100
    if (r <= (px + py))
        return y;

    // r is greater than px+py and smaller than or equal to
    // 100 with probability pz/100
    else
        return z;
}

// This code is contributed by subhammahato348.
```

## 计算机编程语言

```
import random

# This function generates 'x' with probability px/100, 'y' with
# probability py/100  and 'z' with probability pz/100:
# Assumption: px + py + pz = 100 where px, py and pz lie
# between 0 to 100
def random(x, y, z, px, py, pz): 

    # Generate a number from 1 to 100
    r = random.randint(1, 100)

    #  r is smaller than px with probability px/100
    if (r <= px):
        return x

    # r is greater than px and smaller than
    # or equal to px+py with probability py/100
    if (r <= (px+py)):
        return y

    # r is greater than px+py and smaller than
    # or equal to 100 with probability pz/100
    else:
        return z

# This code is contributed by rohan07
```

## C#

```
// This function generates 'x' with probability px/100, 'y'
// with probability py/100  and 'z' with probability pz/100:
// Assumption: px + py + pz = 100 where px, py and pz lie
// between 0 to 100
static int random(int x, int y, int z, int px, int py,
                  int pz)
{
    // Generate a number from 1 to 100
    Random rInt = new Random();
    int r = rInt.Next(0, 100);

    // r is smaller than px with probability px/100
    if (r <= px)
        return x;

    // r is greater than px and smaller than or equal to
    // px+py with probability py/100
    if (r <= (px + py))
        return y;

    // r is greater than px+py and smaller than or equal to
    // 100 with probability pz/100
    else
        return z;
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
// This function generates 'x' with probability px/100, 'y' with
// probability py/100  and 'z' with probability pz/100:
// Assumption: px + py + pz = 100 where px, py and pz lie
// between 0 to 100
function random(x, y, z, px, py, pz)
{      
        // Generate a number from 1 to 100
        let r = Math.floor(Math.random() * 100) + 1;

        // r is smaller than px with probability px/100
        if (r <= px)
            return x;

         // r is greater than px and smaller than or equal to px+py
         // with probability py/100
        if (r <= (px+py))
            return y;

         // r is greater than px+py and smaller than or equal to 100
         // with probability pz/100
        else
            return z;
}

// This code is contributed by subhammahato348.
```

时间复杂度:0(1)

辅助空间:0(1)

这个函数将解决用给定的三个概率生成三个数字的问题。
本文由**哈什·阿加瓦尔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息