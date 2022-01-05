# 当最小值字符串在每次操作中连接起来时打印最终字符串

> 原文:[https://www . geeksforgeeks . org/print-the-final-string-when-minimum-value-strings-get-串接 in-ever-operation/](https://www.geeksforgeeks.org/print-the-final-string-when-minimum-value-strings-get-concatenated-in-every-operation/)

给定一个字符串数组和一个整数数组，其中数组中的第 **i <sup>第</sup>T3【整数】对应于字符串数组中的第 **i <sup>第</sup>T7】字符串的值。现在选择整数数组中具有最小值的两个字符串，将两个整数相加并连接两个字符串，将相加的整数加到整数数组中，将连接的字符串加到字符串数组中，并继续重复整个过程，直到两个数组中只剩下一个元素。此外，请注意，一旦选择了任意两个字符串和整数，它们就会从数组中删除，并且新的字符串和整数会添加回各自的数组中。
任务是打印得到的最终字符串。****

**示例:**

> **输入:** str = {“极客”、“For”、“极客”}，num = {2，3，7}
> **输出:**极客 ForGeeks
> 选择 2 和 3 添加它们，形成“极客 For”和 5
> 将它们添加回数组，str = {“极客 For”、“极客”}，num = {5，7}
> 现在选择 7 和 5 添加它们，形成“极客 ForGeeks”，这是最后的字符串。
> 
> **输入:**str = { " ABC "，" def "，" ghi "，" jkl " }，num = {1，4，2，6}
> **输出:**jklabcghdef

**方法:**思路是使用一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，制作一对字符串及其对应的值，存储在优先级队列中，保持两对从优先级队列中出列，将整数相加并串接，重新排入优先级队列，直到队列的大小减为 1，然后打印队列中唯一剩余的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Class that represents a pair
struct Priority
{
    string s;
    int count;
};

struct Compare
{
    int operator()(Priority a, Priority b)
    {
        if (a.count > b.count)
            return 1;
        else if (a.count < b.count)
            return -1;

        return 0;
    }
};

// Function that prints the final string
static void FindString(string str[], int num[],
                                     int n)
{
    priority_queue<int, vector<Priority>, Compare> p;

    // Add all the strings and their corresponding
    // values to the priority queue
    for(int i = 0; i < n; i++)
    {
        Priority x;
        x.s = str[i];
        x.count = num[i];
        p.push(x);
    }

    // Take those two strings from the priority
    // queue whose corresponding integer values
    // are smaller and add them up as well as
    // their values and add them back to the
    // priority queue while there are more
    // than a single element in the queue
    while (p.size() > 1)
    {

        // Get the minimum valued string
        Priority x = p.top();
        p.pop();
        // p.remove(x);

        // Get the second minimum valued string
        Priority y = p.top();
        p.pop();

        // Updated integer value
        int temp = x.count + y.count;
        string sb = x.s + y.s;

        // Create new entry for the queue
        Priority z;
        z.count = temp;
        z.s = sb;

        // Add to the queue
        p.push(z);
    }

    // Print the only remaining string
    Priority z = p.top();
    p.pop();

    cout << z.s << endl;
}

// Driver code
int main()
{
    string str[] = { "Geeks", "For", "Geeks" };
    int num[] = { 2, 3, 7 };
    int n = sizeof(num) / sizeof(int);

    FindString(str, num, n);
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;

// Class that represents a pair
class Priority {
    String s;
    int count;
}

class PQ implements Comparator<Priority> {
    public int compare(Priority a, Priority b)
    {
        if (a.count > b.count)
            return 1;
        else if (a.count < b.count)
            return -1;
        return 0;
    }
}

class GFG {

    // Function that prints the final string
    static void FindString(String str[], int num[], int n)
    {
        Comparator<Priority> comparator = new PQ();
        PriorityQueue<Priority> p
            = new PriorityQueue<Priority>(comparator);

        // Add all the strings and their corresponding
        // values to the priority queue
        for (int i = 0; i < n; i++) {
            Priority x = new Priority();
            x.s = str[i];
            x.count = num[i];
            p.add(x);
        }

        // Take those two strings from the priority
        // queue whose corresponding integer values are smaller
        // and add them up as well as their values and
        // add them back to the priority queue
        // while there are more than a single element in the queue
        while (p.size() > 1) {

            // Get the minimum valued string
            Priority x = p.poll();
            p.remove(x);

            // Get the second minimum valued string
            Priority y = p.poll();
            p.remove(y);

            // Updated integer value
            int temp = x.count + y.count;
            String sb = x.s + y.s;

            // Create new entry for the queue
            Priority z = new Priority();
            z.count = temp;
            z.s = sb;

            // Add to the queue
            p.add(z);
        }

        // Print the only remaining string
        Priority z = p.poll();
        System.out.println(z.s);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str[] = { "Geeks", "For", "Geeks" };
        int num[] = { 2, 3, 7 };
        int n = num.length;

        FindString(str, num, n);
    }
}
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that prints the final string
function FindString(str, num, n)
{
    var p = [];

    // Add all the strings and their corresponding
    // values to the priority queue
    for(var i = 0; i < n; i++)
    {
        var x = [0,0];
        x[0] = str[i];
        x[1] = num[i];
        p.push(x);
    }

    // Take those two strings from the priority
    // queue whose corresponding integer values
    // are smaller and add them up as well as
    // their values and add them back to the
    // priority queue while there are more
    // than a single element in the queue
    while (p.length > 1)
    {

        // Get the minimum valued string
        var x = p[p.length-1];
        p.pop();
        // p.remove(x);

        // Get the second minimum valued string
        var y = p[p.length-1];
        p.pop();

        // Updated integer value
        var temp = x[1] + y[1];
        var sb = x[0] + y[0];

        // Create new entry for the queue
        var z = [0,0];
        z[1] = temp;
        z[0] = sb;

        // Add to the queue
        p.push(z);
    }

    // Print the only remaining string
    var z = p[p.length-1];
    p.pop();

    document.write(z[0] + "<br>");
}

// Driver code
var str = ["Geeks", "For", "Geeks"];
var num = [2, 3, 7];
var n = num.length;

FindString(str, num, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
GeeksForGeeks
```

**时间复杂度:** O(N * log(N))
**辅助空间:** O(N)