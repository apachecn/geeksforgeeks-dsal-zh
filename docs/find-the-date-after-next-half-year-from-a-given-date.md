# 从给定日期

找到下半年之后的日期

> 原文:[https://www . geeksforgeeks . org/从给定日期找到下半年后的日期/](https://www.geeksforgeeks.org/find-the-date-after-next-half-year-from-a-given-date/)

给定一个正整数 **D** 和一个代表闰年的日和月的字符串 **M** ，任务是找到下一个半年后的日期。

**示例:**

> ***输入:** D = 15，M =【一月】*
> ***输出:**7 月 16 日*
> ***说明:****1 月 15 日至下半年的日期为 7 月 16 日。*
> 
> ***输入:** D = 10，M =【十月】*
> T5**输出:**4 月 10 日

**方法:**由于闰年包含 **366 天**，给定的问题可以通过将当前日期增加 **183 天**后找到数据来解决。按照以下步骤解决问题:

*   存储该数组中每个月的天数，比如**天【】**。
*   初始化一个变量，说 **curMonth** 为 **M** ，存储当月的指数。
*   初始化一个变量，说**将**压缩为 **D** ，以存储当前日期。
*   初始化一个变量，说**计数**为 **183** ，代表要递增的天数。
*   迭代直到**计数**的值为正，并执行以下步骤:
    *   如果**计数**的值为正，**凝结**最多为**月**的天数，则**计数**的值递减 **1** ，将**凝结**的值递增 **1** 。
    *   如果**计数**的值为 **0** ，则[退出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   通过 **(curMonth + 1)%12** 更新 **curMonth** 的值。
*   完成以上步骤后，打印**对应的日期，打印结果为**和 **curMonth** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find the date
// after the next half-year
void getDate(int d, string m) {

    // Stores the number of days in the
    // months of a leap year
    int days[] = {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    // List of months
    string month[] = {"January", "February",
             "March", "April",
             "May", "June",
             "July", "August",
             "September", "October",
             "November", "December"};

    // Days in half of a year
    int cnt = 183;

    // Index of current month
    int cur_month;
      for(int i = 0; i < 12; i++)
      if(m == month[i])
          cur_month = i;

    // Starting day
    int cur_date = d;

    while(1) {

        while(cnt > 0 && cur_date <= days[cur_month]) {

            // Decrement the value of
            // cnt by 1
            cnt -= 1;

            // Increment cur_date
            cur_date += 1;
        }

        // If cnt is equal to 0, then
        // break out of the loop
        if(cnt == 0)
            break;

        // Update cur_month
        cur_month = (cur_month + 1) % 12;

        // Update cur_date
        cur_date = 1;
    }

    // Print the resultant date
    cout << cur_date << " " << month[cur_month] << endl;
}

// Driver Code
int main() {

    int D = 15;
    string M = "January";

    // Function Call
    getDate(D, M);

    return 0;
}

// This code is contributed by Dharanendra L V.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the date
// after the next half-year
public static void getDate(int d, String m)
{

    // Stores the number of days in the
    // months of a leap year
    int[] days = { 31, 29, 31, 30, 31, 30,
                   31, 31, 30, 31, 30, 31 };

    // List of months
    String[] month = { "January", "February", "March",
                       "April", "May", "June", "July",
                       "August", "September", "October",
                       "November", "December" };

    // Days in half of a year
    int cnt = 183;

    // Index of current month
    int cur_month = 0;
    for(int i = 0; i < 12; i++)
        if (m == month[i])
            cur_month = i;

    // Starting day
    int cur_date = d;

    while (true)
    {
        while (cnt > 0 && cur_date <= days[cur_month])
        {

            // Decrement the value of
            // cnt by 1
            cnt -= 1;

            // Increment cur_date
            cur_date += 1;
        }

        // If cnt is equal to 0, then
        // break out of the loop
        if (cnt == 0)
            break;

        // Update cur_month
        cur_month = (cur_month + 1) % 12;

        // Update cur_date
        cur_date = 1;
    }

    // Print the resultant date
    System.out.println(cur_date + " " +
                       month[cur_month]);
}

// Driver Code
public static void main(String args[])
{
    int D = 15;
    String M = "January";

    // Function Call
    getDate(D, M);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the date
# after the next half-year
def getDate(d, m):

    # Stores the number of days in the
    # months of a leap year
    days = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

    # List of months
    month = ['January', 'February',
             'March', 'April',
             'May', 'June',
             'July', 'August',
             'September', 'October',
             'November', 'December']

    # Days in half of a year
    cnt = 183

    # Index of current month
    cur_month = month.index(m)

    # Starting day
    cur_date = d

    while(1):

        while(cnt > 0 and cur_date <= days[cur_month]):

            # Decrement the value of
            # cnt by 1
            cnt -= 1

            # Increment cur_date
            cur_date += 1

        # If cnt is equal to 0, then
        # break out of the loop
        if(cnt == 0):
            break

        # Update cur_month
        cur_month = (cur_month + 1) % 12

        # Update cur_date
        cur_date = 1

    # Print the resultant date
    print(cur_date, month[cur_month])

# Driver Code
D = 15
M = "January"

# Function Call
getDate(D, M)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the date
// after the next half-year
static void getDate(int d, string m)
{

    // Stores the number of days in the
    // months of a leap year
    int[] days = { 31, 29, 31, 30, 31, 30,
                   31, 31, 30, 31, 30, 31 };

    // List of months
    string[] month = { "January", "February", "March",
                       "April", "May", "June", "July",
                       "August", "September", "October",
                       "November", "December" };

    // Days in half of a year
    int cnt = 183;

    // Index of current month
    int cur_month = 0;
    for(int i = 0; i < 12; i++)
        if (m == month[i])
            cur_month = i;

    // Starting day
    int cur_date = d;

    while (true)
    {
        while (cnt > 0 && cur_date <= days[cur_month])
        {

            // Decrement the value of
            // cnt by 1
            cnt -= 1;

            // Increment cur_date
            cur_date += 1;
        }

        // If cnt is equal to 0, then
        // break out of the loop
        if (cnt == 0)
            break;

        // Update cur_month
        cur_month = (cur_month + 1) % 12;

        // Update cur_date
        cur_date = 1;
    }

    // Print the resultant date
    Console.WriteLine(cur_date + " " +
                      month[cur_month]);
}

// Driver Code
public static void Main()
{
    int D = 15;
    string M = "January";

    // Function Call
    getDate(D, M);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the date
// after the next half-year
function getDate(d, m)
{

    // Stores the number of days in the
    // months of a leap year
    let days = [ 31, 29, 31, 30, 31, 30,
                 31, 31, 30, 31, 30, 31 ];

    // List of months
    let month = [ "January", "February", "March",
                  "April", "May", "June", "July",
                  "August", "September", "October",
                  "November", "December" ];

    // Days in half of a year
    let cnt = 183;

    // Index of current month
    let cur_month = 0;
    for(let i = 0; i < 12; i++)
        if (m == month[i])
            cur_month = i;

    // Starting day
    let cur_date = d;

    while (true)
    {
        while (cnt > 0 && cur_date <= days[cur_month])
        {

            // Decrement the value of
            // cnt by 1
            cnt -= 1;

            // Increment cur_date
            cur_date += 1;
        }

        // If cnt is equal to 0, then
        // break out of the loop
        if (cnt == 0)
            break;

        // Update cur_month
        cur_month = (cur_month + 1) % 12;

        // Update cur_date
        cur_date = 1;
    }

    // Print the resultant date
    document.write(cur_date + " " +
                   month[cur_month]);
}

// Driver Code
let D = 15;
let M = "January";

// Function Call
getDate(D, M);

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
16 July
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)