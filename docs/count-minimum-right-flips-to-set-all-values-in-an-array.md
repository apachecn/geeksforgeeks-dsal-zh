# 计算最小右翻转以设置数组中的所有值

> 原文:[https://www . geesforgeks . org/count-minimum-right-flips-to-set-all-values-in-a-array/](https://www.geeksforgeeks.org/count-minimum-right-flips-to-set-all-values-in-an-array/)

n 个灯泡用电线连接起来。每个灯泡都有一个与之相关的开关，但是由于线路故障，一个开关也会改变当前灯泡右侧所有灯泡的状态。给定所有灯泡的初始状态，找到打开所有灯泡所需按下的最小开关数。您可以多次按下同一个开关。
注意:0 表示灯泡关闭，1 表示灯泡开启。
**例:**

```
Input :  [0 1 0 1]
Output : 4
Explanation :
    press switch 0 : [1 0 1 0]
    press switch 1 : [1 1 0 1]
    press switch 2 : [1 1 1 0]
    press switch 3 : [1 1 1 1]

Input : [1 0 0 0 0] 
Output : 1
```

我们从左到右遍历给定的数组，并持续按下关闭灯泡的开关。我们记录了到目前为止按下开关的次数。如果按压次数是奇数，这意味着当前开关处于其原始状态，否则它处于另一状态。根据灯泡的状态，我们可以增加按压次数。

## C++

```
// CPP program to find number switch presses to
// turn all bulbs on.
#include<bits/stdc++.h>
using namespace std;

int bulbs(int a[],int n)
{
    // To keep track of switch presses so far
    int count = 0;

    int res = 0;
    for (int i = 0; i < n; i++)
    {
        /* if the bulb's original state is on and count
        is even, it is currently on...*/
        /* no need to press this switch */
        if (a[i] == 1 && count % 2 == 0)
            continue;

        /* If the bulb's original state is off and count
        is odd, it is currently on...*/
        /* no need to press this switch */
        else if(a[i] == 0 && count % 2 != 0)
            continue;

        /* if the bulb's original state is on and count   
        is odd, it is currently off...*/
        /* Press this switch to on the bulb and increase
        the count */
        else if (a[i] == 1 && count % 2 != 0)
        {
            res++;
            count++;
        }

        /* if the bulb's original state is off and
        count is even, it is currently off...*/
        /* press this switch to on the bulb and
        increase the count */
        else if (a[i] == 0 && count % 2 == 0)
        {
            res++;
            count++;
        }
    }
    return res;
}

// Driver code
int main()
{
    int states[] = {0,1,0,1};
    int n = sizeof(states)/sizeof(states[0]);
    cout << "The minimum number of switches needed are " << bulbs(states,n);
}

// This code is contributed by
// Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number switch presses to
// turn all bulbs on.
import java.util.*;

public class GFG
{
    public int bulbs(ArrayList<Integer> a)
    {
        // To keep track of switch presses so far
        int count = 0;

        int res = 0;
        for (int i = 0; i < a.size(); i++)
        {
            /* if the bulb's original state is on and count
               is even, it is currently on...*/
            /* no need to press this switch */
            if (a.get(i) == 1 && count%2 == 0)
                continue;

            /* If the bulb's original state is off and count
               is odd, it is currently on...*/
            /* no need to press this switch */
            else if(a.get(i) == 0 && count%2 != 0)
                continue;

            /* if the bulb's original state is on and count
               is odd, it is currently off...*/
            /* Press this switch to on the bulb and increase
               the count */
            else if (a.get(i) == 1 && count%2 != 0)
            {
                res++;
                count++;
            }

            /* if the bulb's original state is off and
               count is even, it is currently off...*/
            /* press this switch to on the bulb and
               increase the count */
            else if (a.get(i) == 0 && count%2 == 0)
            {
                res++;
                count++;
            }
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        GFG gfg = new GFG();

        ArrayList<Integer> states = new ArrayList<Integer>();

        states.add(0);
        states.add(1);
        states.add(0);
        states.add(1);

        System.out.println("The minimum number of switches" +
                           " needed are " + gfg.bulbs(states));
    }
}
```

## 蟒蛇 3

```
# Python program to find number switch presses to
# turn all bulbs on.

def bulbs(a, n):
    # To keep track of switch presses so far
    count = 0

    res = 0
    for i in range(n):
        # if the bulb's original state is on and count
        # is even, it is currently on...
        # no need to press this switch
        if (a[i] == 1 and count % 2 == 0):
            continue

        # If the bulb's original state is off and count
        # is odd, it is currently on...
        # no need to press this switch
        elif(a[i] == 0 and count % 2 != 0):
            continue

        # if the bulb's original state is on and count
        # is odd, it is currently off...
        # Press this switch to on the bulb and increase
        # the count
        elif (a[i] == 1 and count % 2 != 0):
            res += 1
            count += 1

        # if the bulb's original state is off and
        # count is even, it is currently off...
        # press this switch to on the bulb and
        # increase the count
        elif (a[i] == 0 and count % 2 == 0):
            res += 1
            count += 1
    return res

# Driver code
states = [0, 1, 0, 1]
n = len(states)
print("The minimum number of switches needed are", bulbs(states, n))

# This code is contributed by ankush_953
```

## C#

```
// C# program to find number switch presses
// to turn all bulbs on.
using System;
using System.Collections.Generic;

class GFG
{
public virtual int bulbs(List<int> a)
{
    // To keep track of switch presses so far
    int count = 0;

    int res = 0;
    for (int i = 0; i < a.Count; i++)
    {
        /* if the bulb's original state is on
        and count is even, it is currently on...*/
        /* no need to press this switch */
        if (a[i] == 1 && count % 2 == 0)
        {
            continue;
        }

        /* If the bulb's original state is off
        and count is odd, it is currently on...*/
        /* no need to press this switch */
        else if (a[i] == 0 && count % 2 != 0)
        {
            continue;
        }

        /* if the bulb's original state is on
        and count is odd, it is currently off...*/
        /* Press this switch to on the bulb and
        increase the count */
        else if (a[i] == 1 && count % 2 != 0)
        {
            res++;
            count++;
        }

        /* if the bulb's original state is off and
        count is even, it is currently off...*/
        /* press this switch to on the bulb and
        increase the count */
        else if (a[i] == 0 && count % 2 == 0)
        {
            res++;
            count++;
        }
    }
    return res;
}

// Driver code
public static void Main(string[] args)
{
    GFG gfg = new GFG();

    List<int> states = new List<int>();

    states.Add(0);
    states.Add(1);
    states.Add(0);
    states.Add(1);

    Console.WriteLine("The minimum number of switches" +
                    " needed are " + gfg.bulbs(states));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to find number switch presses to
// turn all bulbs on.
function bulbs(a, n)
{

    // To keep track of switch presses so far
    let count = 0;

    let res = 0;
    for (let i = 0; i < n; i++)
    {
        /* if the bulb's original state is on and count
        is even, it is currently on...*/
        /* no need to press this switch */
        if (a[i] == 1 && count % 2 == 0)
            continue;

        /* If the bulb's original state is off and count
        is odd, it is currently on...*/
        /* no need to press this switch */
        else if(a[i] == 0 && count % 2 != 0)
            continue;

        /* if the bulb's original state is on and count   
        is odd, it is currently off...*/
        /* Press this switch to on the bulb and increase
        the count */
        else if (a[i] == 1 && count % 2 != 0)
        {
            res++;
            count++;
        }

        /* if the bulb's original state is off and
        count is even, it is currently off...*/
        /* press this switch to on the bulb and
        increase the count */
        else if (a[i] == 0 && count % 2 == 0)
        {
            res++;
            count++;
        }
    }
    return res;
}

// Driver code

    let states = [0,1,0,1];
    let n = states.length;
    document.write("The minimum number of switches needed are " + bulbs(states,n));

    // This code is contributed by vaibhavrabadiya117.
</script>
```

**输出:**

```
The minimum number of switches needed are 4.
```

本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
https://www.interviewbit.com/problems/bulbs/
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。