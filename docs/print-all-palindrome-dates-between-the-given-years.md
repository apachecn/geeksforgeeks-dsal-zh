# 打印给定年份之间的所有回文日期

> 原文:[https://www . geesforgeks . org/print-all-回文-给定年份之间的日期/](https://www.geeksforgeeks.org/print-all-palindrome-dates-between-the-given-years/)

给定两年 **Y1** 和 **Y2** ，其中**10<sup>3</sup>≤Y1≤Y2≤10<sup>6</sup>**，任务是查找并打印给定年份之间回文的所有日期。

**示例:**

> **输入:** Y1 = 2001，Y2 = 2005
> T3】输出:T5】10022001
> 20022002
> 
> **输入:** Y1 = 5000，Y2 = 5010
> **输出:**
> 10055001
> 20055002
> 30055003
> 01055010

**方法:**由于前四位数字(即日和月)必须与后四位数字(年)相反，日期才能成为回文。所以，每年最多会有一个回文日期。为了找到日期，对于每一年，反转年数并检查形成的[日期是否有效](https://www.geeksforgeeks.org/program-check-date-valid-not/)。如果它是有效的，那么打印它。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX_VALID_YR = 9999;
const int MIN_VALID_YR = 1800;

// Returns true if
// given year is valid
bool isLeap(int year)
{
    // Return true if year
    // is a multiple pf 4 and
    // not multiple of 100.
    // OR year is multiple of 400.
    return (((year % 4 == 0)
             && (year % 100 != 0))
            || (year % 400 == 0));
}

// Returns true if given
// year is valid or not.
bool isValidDate(int d, int m, int y)
{
    // If year, month and day
    // are not in given range
    if (y > MAX_VALID_YR || y < MIN_VALID_YR)
        return false;
    if (m < 1 || m > 12)
        return false;
    if (d < 1 || d > 31)
        return false;

    // Handle February month
    // with leap year
    if (m == 2) {
        if (isLeap(y))
            return (d <= 29);
        else
            return (d <= 28);
    }

    // Months of April, June,
    // Sept and Nov must have
    // number of days less than
    // or equal to 30.
    if (m == 4 || m == 6 || m == 9 || m == 11)
        return (d <= 30);

    return true;
}

// Function to print the palindrome
// dates between the given years
void printPalindromeDates(int y1, int y2)
{

    // For every year
    for (int year = y1; year <= y2; year++) {

        // Current year as a string
        string str = to_string(year);

        // To store the reverse of year
        string rev = str;
        reverse(rev.begin(), rev.end());

        // Get the day and the month
        int day = stoi(rev.substr(0, 2));
        int month = stoi(rev.substr(2, 2));

        // If the current palindrome date is valid
        if (isValidDate(day, month, year)) {
            cout << rev << str << endl;
        }
    }
}

// Driver code
int main()
{
    int y1 = 2001, y2 = 2005;

    printPalindromeDates(y1, y2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX_VALID_YR = 9999;
static int MIN_VALID_YR = 1800;

// Returns true if
// given year is valid
static boolean isLeap(int year)
{
    // Return true if year
    // is a multiple pf 4 and
    // not multiple of 100.
    // OR year is multiple of 400.
    return (((year % 4 == 0)
            && (year % 100 != 0))
            || (year % 400 == 0));
}

// Returns true if given
// year is valid or not.
static boolean isValidDate(int d, int m, int y)
{
    // If year, month and day
    // are not in given range
    if (y > MAX_VALID_YR || y < MIN_VALID_YR)
        return false;
    if (m < 1 || m > 12)
        return false;
    if (d < 1 || d > 31)
        return false;

    // Handle February month
    // with leap year
    if (m == 2) 
    {
        if (isLeap(y))
            return (d <= 29);
        else
            return (d <= 28);
    }

    // Months of April, June,
    // Sept and Nov must have
    // number of days less than
    // or equal to 30.
    if (m == 4 || m == 6 || m == 9 || m == 11)
        return (d <= 30);

    return true;
}

// Function to print the palindrome
// dates between the given years
static void printPalindromeDates(int y1, int y2)
{

    // For every year
    for (int year = y1; year <= y2; year++)
    {

        // Current year as a String
        String str = String.valueOf(year);

        // To store the reverse of year
        String rev = str;
        rev = reverse(rev);

        // Get the day and the month
        int day = Integer.parseInt(rev.substring(0, 2));
        int month = Integer.parseInt(rev.substring(2, 2 + 2));

        // If the current palindrome date is valid
        if (isValidDate(day, month, year))
        {
            System.out.print(rev + str +"\n");
        }
    }
}
static String reverse(String input) 
{
        char[] a = input.toCharArray();
        int l, r = a.length - 1;
        for (l = 0; l < r; l++, r--) 
        {
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.valueOf(a);
    }

// Driver code
public static void main(String[] args)
{
    int y1 = 2001, y2 = 2005;

    printPalindromeDates(y1, y2);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX_VALID_YR = 9999
MIN_VALID_YR = 1800

# Returns true if given year is valid
def isLeap(year):

    # Return true if year
    # is a multiple pf 4 and
    # not multiple of 100.
    # OR year is multiple of 400.
    return (((year % 4 == 0) and 
             (year % 100 != 0)) or 
             (year % 400 == 0))

# Returns true if given
# year is valid or not.
def isValidDate(d, m, y):

    # If year, month and day
    # are not in given range
    if (y > MAX_VALID_YR or y < MIN_VALID_YR):
        return False
    if (m < 1 or m > 12):
        return False
    if (d < 1 or d > 31):
        return False

    # Handle February month
    # with leap year
    if (m == 2):
        if (isLeap(y)):
            return (d <= 29)
        else:
            return (d <= 28)

    # Months of April, June,
    # Sept and Nov must have
    # number of days less than
    # or equal to 30.
    if (m == 4 or m == 6 or 
        m == 9 or m == 11):
        return (d <= 30)

    return True

# Function to print the palindrome
# dates between the given years
def printPalindromeDates(y1, y2):

    # For every year
    for year in range(y1, y2 + 1, 1):

        # Current year as a string
        str1 = str(year)

        # To store the reverse of year
        rev = str1
        rev = rev[::-1]

        # Get the day and the month
        day = int(rev[0 : 2])
        month = int(rev[2 : 4])

        # If the current palindrome date is valid
        rev += str1
        if (isValidDate(day, month, year)):
            print(rev)

# Driver code
if __name__ == '__main__':
    y1 = 2001
    y2 = 2005

    printPalindromeDates(y1, y2)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX_VALID_YR = 9999;
static int MIN_VALID_YR = 1800;

// Returns true if
// given year is valid
static bool isLeap(int year)
{
    // Return true if year
    // is a multiple pf 4 and
    // not multiple of 100.
    // OR year is multiple of 400.
    return (((year % 4 == 0) && 
             (year % 100 != 0)) || 
             (year % 400 == 0));
}

// Returns true if given
// year is valid or not.
static bool isValidDate(int d, int m, int y)
{
    // If year, month and day
    // are not in given range
    if (y > MAX_VALID_YR || y < MIN_VALID_YR)
        return false;
    if (m < 1 || m > 12)
        return false;
    if (d < 1 || d > 31)
        return false;

    // Handle February month
    // with leap year
    if (m == 2) 
    {
        if (isLeap(y))
            return (d <= 29);
        else
            return (d <= 28);
    }

    // Months of April, June,
    // Sept and Nov must have
    // number of days less than
    // or equal to 30.
    if (m == 4 || m == 6 || m == 9 || m == 11)
        return (d <= 30);

    return true;
}

// Function to print the palindrome
// dates between the given years
static void printPalindromeDates(int y1, int y2)
{

    // For every year
    for (int year = y1; year <= y2; year++)
    {

        // Current year as a String
        String str = String.Join("", year);

        // To store the reverse of year
        String rev = str;
        rev = reverse(rev);

        // Get the day and the month
        int day = Int32.Parse(rev.Substring(0, 2));
        int month = Int32.Parse(rev.Substring(2, 2));

        // If the current palindrome date is valid
        if (isValidDate(day, month, year))
        {
            Console.Write(rev + str +"\n");
        }
    }
}

static String reverse(String input) 
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) 
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("", a);
}

// Driver code
public static void Main(String[] args)
{
    int y1 = 2001, y2 = 2005;

    printPalindromeDates(y1, y2);
}
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
10022001
20022002

```