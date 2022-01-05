# 查找无法获得电脑的客户数量的功能

> 原文:[https://www . geesforgeks . org/function-to-find-找不到电脑的客户数量/](https://www.geeksforgeeks.org/function-to-find-number-of-customers-who-could-not-get-a-computer/)

编写一个函数“runCustomerSimulation”，该函数接受以下两个输入
a)一个整数“n”:咖啡馆中的计算机总数和一个字符串:
b)一个大写字母“seq”序列:序列中的字母成对出现。第一个事件表示客户的到来；第二个表示同一客户的离开。
如果有未被占用的电脑，将为客户提供服务。没有一封信会出现两次以上。
不使用电脑离开的客户总是在当前使用电脑的客户之前离开。每个咖啡馆最多有 20 台电脑。
对于每一组输入，该功能应该输出一个数字，告诉有多少客户(如果有的话)没有使用计算机就离开了。如果所有客户都能使用计算机，则返回 0。
runCustomerSimulation (2，“ABBAJJKZKZ”)应返回 0
runCustomerSimulation (3，“GACCBDDBAGEE”)应返回 1 作为“D”未能获得任何计算机
runCustomerSimulation (3，“GACCBGDDBAEE”)应返回 0
runCustomerSimulation (1，“ABCBCA”)应返回 2 作为“B”和“C”未能获得任何计算机。
runcustomerssimulation(1，“ABCBCADEED”)应该返回 3，因为‘B’、‘C’和‘E’都无法获得任何计算机。
来源:[烽火链接(maas360)采访](https://www.geeksforgeeks.org/fiberlink-maas360-interview-set-2-written-test-question/)
**强烈建议尽量减少浏览器，先自己试试这个。**
下面是一些简单的步骤，可以找到一些买不到电脑的顾客。
1)将结果初始化为 0。
2)遍历给定的序列。遍历时，跟踪已占用的计算机(这可以通过跟踪只出现过一次的字符和出现时计算机可用来实现)。在任何时候，如果占用的计算机数等于“n”，并且有一个新客户，则将结果增加 1。
重要的是要以一种可以表明顾客是否有电脑的方式来跟踪咖啡馆现有的顾客。请注意，在“ABCBCADEED”序列中，客户“B”没有获得座位，但仍在咖啡馆中，因为新客户“C”是序列中的下一个。
以下是上述想法的实现。
T22】

## C++

```
// C++ program to find number of customers who couldn't get a resource.
#include<iostream>
#include<cstring>
using namespace std;

#define MAX_CHAR 26

// n is number of computers in cafe.
// 'seq' is given sequence of customer entry, exit events
int runCustomerSimulation(int n, const char *seq)
{
    // seen[i] = 0, indicates that customer 'i' is not in cafe
    // seen[1] = 1, indicates that customer 'i' is in cafe but
    //             computer is not assigned yet.
    // seen[2] = 2, indicates that customer 'i' is in cafe and
    //             has occupied a computer.
    char seen[MAX_CHAR] = {0};

    // Initialize result which is number of customers who could
    // not get any computer.
    int res = 0;

    int occupied = 0; // To keep track of occupied computers

    // Traverse the input sequence
    for (int i=0; seq[i]; i++)
    {
        // Find index of current character in seen[0...25]
        int ind = seq[i] - 'A';

        // If First occurrence of 'seq[i]'
        if (seen[ind] == 0)
        {
            // set the current character as seen
            seen[ind] = 1;

            // If number of occupied computers is less than
            // n, then assign a computer to new customer
            if (occupied < n)
            {
                occupied++;

                // Set the current character as occupying a computer
                seen[ind] = 2;
            }

            // Else this customer cannot get a computer,
            // increment result
            else
                res++;
        }

        // If this is second occurrence of 'seq[i]'
        else
        {
        // Decrement occupied only if this customer
        // was using a computer
        if (seen[ind] == 2)
            occupied--;
        seen[ind] = 0;
        }
    }
    return res;
}

// Driver program
int main()
{
    cout << runCustomerSimulation(2, "ABBAJJKZKZ") << endl;
    cout << runCustomerSimulation(3, "GACCBDDBAGEE") << endl;
    cout << runCustomerSimulation(3, "GACCBGDDBAEE") << endl;
    cout << runCustomerSimulation(1, "ABCBCA") << endl;
    cout << runCustomerSimulation(1, "ABCBCADEED") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find number of
//customers who couldn't get a resource.
class GFG
{

static int MAX_CHAR = 26;

// n is number of computers in cafe.
// 'seq' is given sequence of customer entry, exit events
static int runCustomerSimulation(int n, char []seq)
{
    // seen[i] = 0, indicates that customer 'i' is not in cafe
    // seen[1] = 1, indicates that customer 'i' is in cafe but
    //         computer is not assigned yet.
    // seen[2] = 2, indicates that customer 'i' is in cafe and
    //         has occupied a computer.
    char []seen = new char[MAX_CHAR];

    // Initialize result which is number of customers who could
    // not get any computer.
    int res = 0;

    int occupied = 0; // To keep track of occupied computers

    // Traverse the input sequence
    for (int i=0; i< seq.length; i++)
    {
        // Find index of current character in seen[0...25]
        int ind = seq[i] - 'A';

        // If First occurrence of 'seq[i]'
        if (seen[ind] == 0)
        {
            // set the current character as seen
            seen[ind] = 1;

            // If number of occupied computers is less than
            // n, then assign a computer to new customer
            if (occupied < n)
            {
                occupied++;

                // Set the current character as occupying a computer
                seen[ind] = 2;
            }

            // Else this customer cannot get a computer,
            // increment result
            else
                res++;
        }

        // If this is second occurrence of 'seq[i]'
        else
        {

        // Decrement occupied only if this customer
        // was using a computer
        if (seen[ind] == 2)
            occupied--;
        seen[ind] = 0;
        }
    }
    return res;
}

// Driver program
public static void main(String[] args)
{
    System.out.println(runCustomerSimulation(2, "ABBAJJKZKZ".toCharArray()));
    System.out.println(runCustomerSimulation(3, "GACCBDDBAGEE".toCharArray()));
    System.out.println(runCustomerSimulation(3, "GACCBGDDBAEE".toCharArray()));
    System.out.println(runCustomerSimulation(1, "ABCBCA".toCharArray()));
    System.out.println(runCustomerSimulation(1, "ABCBCADEED".toCharArray()));
}
}

// This code is contributed by Princi Singh
```

## 计算机编程语言

```
# Python program function to find Number of customers who
# could not get a computer
MAX_CHAR = 26

# n is number of computers in cafe.
# 'seq' is given sequence of customer entry, exit events
def runCustomerSimulation(n, seq):

    # seen[i] = 0, indicates that customer 'i' is not in cafe
    # seen[1] = 1, indicates that customer 'i' is in cafe but
    #             computer is not assigned yet.
    # seen[2] = 2, indicates that customer 'i' is in cafe and
    #             has occupied a computer.
    seen = [0] * MAX_CHAR

    # Initialize result which is number of customers who could
    # not get any computer.
    res = 0
    occupied = 0    # To keep track of occupied

    # Traverse the input sequence
    for i in xrange(len(seq)):

        # Find index of current character in seen[0...25]
        ind = ord(seq[i]) - ord('A')

        # If first occurrence of 'seq[i]'
        if seen[ind] == 0:

            # set the current character as seen
            seen[ind] = 1

            # If number of occupied computers is less than
            # n, then assign a computer to new customer
            if occupied < n:
                occupied+=1

                # Set the current character as occupying a computer
                seen[ind] = 2

            # Else this customer cannot get a computer,
            # increment
            else:
                res+=1

        # If this is second occurrence of 'seq[i]'
        else:
            # Decrement occupied only if this customer
            # was using a computer
            if seen[ind] == 2:
                occupied-=1
            seen[ind] = 0

    return res

# Driver program
print runCustomerSimulation(2, "ABBAJJKZKZ")
print runCustomerSimulation(3, "GACCBDDBAGEE")
print runCustomerSimulation(3, "GACCBGDDBAEE")
print runCustomerSimulation(1, "ABCBCA")
print runCustomerSimulation(1, "ABCBCADEED")

# This code is contributed BHAVYA JAIN
```

## C#

```
// C# program to find number of
// customers who couldn't get a resource.
using System;

class GFG
{
static int MAX_CHAR = 26;

// n is number of computers in cafe.
// 'seq' is given sequence of customer entry,
// exit events
static int runCustomerSimulation(int n, char []seq)
{
    // seen[i] = 0, indicates that customer 'i' is not in cafe
    // seen[1] = 1, indicates that customer 'i' is in cafe but
    // computer is not assigned yet.
    // seen[2] = 2, indicates that customer 'i' is in cafe and
    // has occupied a computer.
    char []seen = new char[MAX_CHAR];

    // Initialize result which is number of customers
    // who could not get any computer.
    int res = 0;

    int occupied = 0; // To keep track of occupied computers

    // Traverse the input sequence
    for (int i = 0; i < seq.Length; i++)
    {
        // Find index of current character in seen[0...25]
        int ind = seq[i] - 'A';

        // If First occurrence of 'seq[i]'
        if (seen[ind] == 0)
        {
            // set the current character as seen
            seen[ind] = (char)1;

            // If number of occupied computers is less than
            // n, then assign a computer to new customer
            if (occupied < n)
            {
                occupied++;

                // Set the current character as
                // occupying a computer
                seen[ind] = (char)2;
            }

            // Else this customer cannot get a computer,
            // increment result
            else
                res++;
        }

        // If this is second occurrence of 'seq[i]'
        else
        {

        // Decrement occupied only if this customer
        // was using a computer
        if (seen[ind] == 2)
            occupied--;
        seen[ind] = (char)0;
        }
    }
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    Console.WriteLine(runCustomerSimulation(2,
                      "ABBAJJKZKZ".ToCharArray()));
    Console.WriteLine(runCustomerSimulation(3,
                      "GACCBDDBAGEE".ToCharArray()));
    Console.WriteLine(runCustomerSimulation(3,
                      "GACCBGDDBAEE".ToCharArray()));
    Console.WriteLine(runCustomerSimulation(1,
                      "ABCBCA".ToCharArray()));
    Console.WriteLine(runCustomerSimulation(1,
                      "ABCBCADEED".ToCharArray()));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        let MAX_CHAR = 26;

        // n is number of computers in cafe.
        // 'seq' is given sequence of customer entry, exit events
        function runCustomerSimulation(n, seq) {
            // seen[i] = 0, indicates that customer 'i' is not in cafe
            // seen[1] = 1, indicates that customer 'i' is in cafe but
            //              computer is not assigned yet.
            // seen[2] = 2, indicates that customer 'i' is in cafe and
            //              has occupied a computer.
            let seen = new Array(MAX_CHAR).fill(0);

            // Initialize result which is number of customers who could
            // not get any computer.
            let res = 0;

            let occupied = 0;  // To keep track of occupied computers

            // Traverse the input sequence
            for (let i = 0; i < seq.length; i++) {
                // Find index of current character in seen[0...25]
                let ind = seq[i].charCodeAt(0) - 'A'.charCodeAt(0);

                // If First occurrence of 'seq[i]'
                if (seen[ind] == 0) {
                    // set the current character as seen
                    seen[ind] = 1;

                    // If number of occupied computers is less than
                    // n, then assign a computer to new customer
                    if (occupied < n) {
                        occupied++;

                        // Set the current character as occupying a computer
                        seen[ind] = 2;
                    }

                    // Else this customer cannot get a computer,
                    // increment result
                    else
                        res++;
                }

                // If this is second occurrence of 'seq[i]'
                else {
                    // Decrement occupied only if this customer
                    // was using a computer
                    if (seen[ind] == 2) {
                        occupied--;
                    }
                    seen[ind] = 0;
                }
            }
            return res;
        }

        // Driver program

        document.write(runCustomerSimulation(2, "ABBAJJKZKZ") + "<br>");
        document.write(runCustomerSimulation(3, "GACCBDDBAGEE") + "<br>");
        document.write(runCustomerSimulation(3, "GACCBGDDBAEE") + "<br>");
        document.write(runCustomerSimulation(1, "ABCBCA") + "<br>");
        document.write(runCustomerSimulation(1, "ABCBCADEED") + "<br>");

    // This code is contributed by Potta Lokesh
    </script>
```

**输出:**

```
0
1
0
2
3 
```

上述解决方案的时间复杂度为 O(n)，所需的额外空间为 O(CHAR_MAX)，其中 CHAR_MAX 是给定序列中可能的字符总数。
本文由**洛克士**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息