# 分数背包问题

> 原文:[https://www.geeksforgeeks.org/fractional-knapsack-problem/](https://www.geeksforgeeks.org/fractional-knapsack-problem/)

给定 n 个物品的重量和值，我们需要将这些物品放在一个容量为 W 的背包中，以获得背包中的最大总值。

在 [0-1 背包问题](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)中，不允许我们破物品。我们要么拿走整个项目，要么不拿。

> **输入:**
> 物品为(值、重量)对
> arr[] = {{60，10}，{100，20}，{120，30}}
> 背包容量，W = 50
> 
> **输出:**
> 最大可能值= 240
> 取 10、20 公斤的物品和 30 公斤的 2/3 分数
> 。因此总价为 60+100+(2/3)(120) = 240

在**分数背包**中，我们可以为了背包的总价值最大化而分解物品。这个我们可以分解一个项目的问题也被称为分数背包问题。

```
Input : 
Same as above

Output :
Maximum possible value = 240
By taking full items of 10 kg, 20 kg and 
2/3rd of last item of 30 kg
```

一个强力的解决方案是用所有不同的分数来尝试所有可能的子集，但是这将花费太多的时间。

一个有效的解决方案是使用贪婪方法。贪婪方法的基本思想是计算每个项目的比率值/权重，并根据该比率对项目进行排序。然后拿比例最高的那一项，把它们加起来，直到我们不能把下一项作为一个整体加进去，最后尽可能多的加下一项。这将永远是这个问题的最佳解决方案。
一个带有我们自己的比较函数的简单代码可以写如下，请更仔细地看排序函数，排序函数的第三个参数是我们的比较函数，它按照值/重量比以非递减顺序对项目进行排序。
分类后，我们需要循环这些物品，并将其添加到满足上述标准的背包中。

下面是上述想法的实现:

## C++

```
// C/C++ program to solve fractional Knapsack Problem
#include <bits/stdc++.h>

using namespace std;

// Structure for an item which stores weight and
// corresponding value of Item
struct Item {
    int value, weight;

    // Constructor
    Item(int value, int weight)
    {
       this->value=value;
       this->weight=weight;
    }
};

// Comparison function to sort Item according to val/weight
// ratio
bool cmp(struct Item a, struct Item b)
{
    double r1 = (double)a.value / (double)a.weight;
    double r2 = (double)b.value / (double)b.weight;
    return r1 > r2;
}

// Main greedy function to solve problem
double fractionalKnapsack(int W, struct Item arr[], int n)
{
    //    sorting Item on basis of ratio
    sort(arr, arr + n, cmp);

    //    Uncomment to see new order of Items with their
    //    ratio
    /*
    for (int i = 0; i < n; i++)
    {
        cout << arr[i].value << "  " << arr[i].weight << " :
    "
             << ((double)arr[i].value / arr[i].weight) <<
    endl;
    }
    */

    int curWeight = 0; // Current weight in knapsack
    double finalvalue = 0.0; // Result (value in Knapsack)

    // Looping through all Items
    for (int i = 0; i < n; i++) {
        // If adding Item won't overflow, add it completely
        if (curWeight + arr[i].weight <= W) {
            curWeight += arr[i].weight;
            finalvalue += arr[i].value;
        }

        // If we can't add current Item, add fractional part
        // of it
        else {
            int remain = W - curWeight;
            finalvalue += arr[i].value
                          * ((double)remain
                             / (double)arr[i].weight);
            break;
        }
    }

    // Returning final value
    return finalvalue;
}

// Driver code
int main()
{
    int W = 50; //    Weight of knapsack
    Item arr[] = { { 60, 10 }, { 100, 20 }, { 120, 30 } };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << "Maximum value we can obtain = "
         << fractionalKnapsack(W, arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve fractional Knapsack Problem
import java.util.Arrays;
import java.util.Comparator;

// Greedy approach
public class FractionalKnapSack {
    // function to get maximum value
    private static double getMaxValue(int[] wt, int[] val,
                                      int capacity)
    {
        ItemValue[] iVal = new ItemValue[wt.length];

        for (int i = 0; i < wt.length; i++) {
            iVal[i] = new ItemValue(wt[i], val[i], i);
        }

        // sorting items by value;
        Arrays.sort(iVal, new Comparator<ItemValue>() {
            @Override
            public int compare(ItemValue o1, ItemValue o2)
            {
                return o2.cost.compareTo(o1.cost);
            }
        });

        double totalValue = 0d;

        for (ItemValue i : iVal) {

            int curWt = (int)i.wt;
            int curVal = (int)i.val;

            if (capacity - curWt >= 0) {
                // this weight can be picked while
                capacity = capacity - curWt;
                totalValue += curVal;
            }
            else {
                // item cant be picked whole
                double fraction
                    = ((double)capacity / (double)curWt);
                totalValue += (curVal * fraction);
                capacity
                    = (int)(capacity - (curWt * fraction));
                break;
            }
        }

        return totalValue;
    }

    // item value class
    static class ItemValue {
        Double cost;
        double wt, val, ind;

        // item value function
        public ItemValue(int wt, int val, int ind)
        {
            this.wt = wt;
            this.val = val;
            this.ind = ind;
            cost = new Double((double)val / (double)wt);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] wt = { 10, 40, 20, 30 };
        int[] val = { 60, 40, 100, 120 };
        int capacity = 50;

        double maxValue = getMaxValue(wt, val, capacity);

        // Function call
        System.out.println("Maximum value we can obtain = "
                           + maxValue);
    }
}
```

## 蟒蛇 3

```
# Python3 program to solve fractional
# Knapsack Problem

class ItemValue:

    """Item Value DataClass"""

    def __init__(self, wt, val, ind):
        self.wt = wt
        self.val = val
        self.ind = ind
        self.cost = val // wt

    def __lt__(self, other):
        return self.cost < other.cost

# Greedy Approach

class FractionalKnapSack:

    """Time Complexity O(n log n)"""
    @staticmethod
    def getMaxValue(wt, val, capacity):
        """function to get maximum value """
        iVal = []
        for i in range(len(wt)):
            iVal.append(ItemValue(wt[i], val[i], i))

        # sorting items by value
        iVal.sort(reverse=True)

        totalValue = 0
        for i in iVal:
            curWt = int(i.wt)
            curVal = int(i.val)
            if capacity - curWt >= 0:
                capacity -= curWt
                totalValue += curVal
            else:
                fraction = capacity / curWt
                totalValue += curVal * fraction
                capacity = int(capacity - (curWt * fraction))
                break
        return totalValue

# Driver Code
if __name__ == "__main__":
    wt = [10, 40, 20, 30]
    val = [60, 40, 100, 120]
    capacity = 50

    # Function call
    maxValue = FractionalKnapSack.getMaxValue(wt, val, capacity)
    print("Maximum value in Knapsack =", maxValue)

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# program to solve fractional Knapsack Problem
using System;
using System.Collections;

class GFG{

// Class for an item which stores weight and
// corresponding value of Item   
class item
{
    public int value;
    public int weight;

    public item(int value, int weight)
    {
        this.value = value;
        this.weight = weight;
    }
}

// Comparison function to sort Item according 
// to val/weight ratio
class cprCompare : IComparer
{
    public int Compare(Object x, Object y)
    {
        item item1 = (item)x;
        item item2 = (item)y;
        double cpr1 = (double)item1.value / 
                      (double)item1.weight;
        double cpr2 = (double)item2.value /
                      (double)item2.weight;

        if (cpr1 < cpr2)
            return 1;

        return cpr1 > cpr2 ? -1 : 0;
    }
}

// Main greedy function to solve problem
static double FracKnapSack(item[] items, int w)
{

    // Sort items based on cost per units
    cprCompare cmp = new cprCompare();
    Array.Sort(items, cmp);

    // Traverse items, if it can fit, 
    // take it all, else take fraction
    double totalVal = 0f;
    int currW = 0;

    foreach (item i in items)
    {
        float remaining = w - currW;

        // If the whole item can be
        // taken, take it
        if (i.weight <= remaining) 
        {
            totalVal += (double)i.value;
            currW += i.weight;
        }

         // dd fraction until we run out of space
        else
        {
            if (remaining == 0)
                break;

            double fraction = remaining / (double)i.weight;
            totalVal += fraction * (double)i.value;
            currW += (int)(fraction * (double)i.weight);
        }
    }
    return totalVal;
}

// Driver code
static void Main(string[] args)
{
    item[] arr = { new item(60, 10), 
                   new item(100, 20),
                   new item(120, 30) };

   Console.WriteLine("Maximum value we can obtain = " + 
                     FracKnapSack(arr, 50));
}
}

// This code is contributed by Mohamed Adel
```

**Output**

```
Maximum value we can obtain = 240
```

由于主要的时间采取步骤是排序，整个问题只能在 O(n log n)中解决。
本文由乌卡什·特里维迪供稿。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。