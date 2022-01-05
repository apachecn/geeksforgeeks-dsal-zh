# 通过用字符串中的任何其他数字替换“$”来打印字符串的所有可能组合

> 原文:[https://www . geeksforgeeks . org/print-通过用字符串中的任何其他数字替换字符串的所有可能组合/](https://www.geeksforgeeks.org/print-all-possible-combinations-of-the-string-by-replacing-with-any-other-digit-from-the-string/)

给定一个数字作为字符串，其中一些数字被**“{ content }”替换；**，任务是通过替换**“{ content }”来生成所有可能的号码；**使用给定字符串中的任意数字。
**例:**

> **输入:** str = "23$"
> **输出:**
> 2322
> 2323
> 2332
> 2333
> **输入:**str = " 45 $ "
> **输出:**
> 445
> 545

**进场:**

*   通过将字符 **$** 替换为字符串的任何一个数字来查找字符串的所有组合，为此，检查当前字符是否为数字，如果是，则将该字符存储到数组中 **pre[]** ，然后递归查找其所有组合，否则，如果当前字符为**' { content }；**然后用数组中存储的数字替换，递归查找所有组合。
*   要找到所有可能的数字，初始化存储所有可能数字的数组**集合[]** ，要生成数字，采取两个嵌套循环，外环用于输入字符串，内环用于存储所有可能数字组合的数组**集合[]** 。初始化布尔标志，检查输入字符串的字符是否已经出现在**集合[]** 中，如果输入字符串的字符已经出现在**集合[]** 中，则设置**标志=假**否则如果标志为真，则将输入字符串的当前字符移动到**集合[]** 中，并递归查找输入字符串的所有组合并将其存储在数组集合[]。最后打印数组**集合[]** 中的每个数字

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 20
#define DIGITS 10

// Array to store all the
// possible numbers
string st(DIGITS,'0');

// Index to st[] element
int ed;

// Function to find all the combinations
// of the string by replacing '{content}apos; with
// the other digits of the string
void combinations(string& num, string& pre, int curr, int lvl)
{

    // Check if current length is less than
    // the length of the input string
    if (curr < (int)num.length()) {

        // If current character is a digit
        // then store digit into pre[] and
        // recursively find all the combinations
        if (num[curr] >= '0' && num[curr] <= '9') {
            pre[lvl] = num[curr];
            combinations(num, pre, curr + 1, lvl + 1);
        }

        // If current character is a '{content}apos; then replace
        // it with the other digits of the string and
        // recursively find all the combinations
        // Else go to the next character and
        // recursively find all the combinations
        else if (num[curr] == '{content}apos;)
            for (int i = 0; i < ed; i++) {
                pre[lvl] = st[i];
                combinations(num, pre, curr + 1, lvl + 1);
            }
        else
            combinations(num, pre, curr + 1, lvl);
    }

    // Print the array pre[]
    else {
        pre[lvl] = '\0';
        cout << pre << '\n';
    }
}

// Function to find all the numbers formed
// from the input string by replacing '{content}apos; with
// all the digits of the input string
int findNumUtil(string& num)
{
    // Array that stores the digits before
    // the character $ in the input string
    string pre((int)num.length(),'0');

    ed = 0;

    // Traverse the input string and check if
    // the current character is a digit
    // if it is then set flag to true
    for (int i = 0; i < num.length(); i++)
        if (num[i] >= '0' && num[i] <= '9') {
            bool flag = true;

            // Check if current character of the input
            // string is already present in the array set[]
            // then set flag to false
            for (int j = 0; j < ed; j++)
                if (st[j] == num[i])
                    flag = false;

            // Flag is true then store the character
            // into st[] and recursively find all
            // the combinations of numbers and store
            // it in the st[] array

            if (flag == true)
                st[ed++] = num[i];
        }

    combinations(num, pre, 0, 0);

    return 0;
}

// Function to print all the combinations
// of the numbers by replacing '{content}apos; with
// the other digits of the input string
int findNum(string& num, vector<int>& result_count)
{
    int i;
    if (num[i]) {
        result_count[i] = findNumUtil(num);
        return (result_count[i]);
    }
    return 0;
}

// Driver code
int main()
{
    string num;
      num = "23$";
    vector<int> result_count(MAX);

    findNum(num, result_count);

    return 0;
}
```

## C

```
// C implementation of the approach
#include <stdbool.h>
#include <stdio.h>
#include <string.h>
#define MAX 20
#define DIGITS 10

// Array to store all the
// possible numbers
char set[DIGITS];

// Index to set[] element
int end;

// Function to find all the combinations
// of the string by replacing '{content}apos; with
// the other digits of the string
void combinations(char* num, char* pre, int curr, int lvl)
{

    // Check if current length is less than
    // the length of the input string
    if (curr < strlen(num)) {

        // If current character is a digit
        // then store digit into pre[] and
        // recursively find all the combinations
        if (num[curr] >= '0' && num[curr] <= '9') {
            pre[lvl] = num[curr];
            combinations(num, pre, curr + 1, lvl + 1);
        }

        // If current character is a '{content}apos; then replace
        // it with the other digits of the string and
        // recursively find all the combinations
        // Else go to the next character and
        // recursively find all the combinations
        else if (num[curr] == '{content}apos;)
            for (int i = 0; i < end; i++) {
                pre[lvl] = set[i];
                combinations(num, pre, curr + 1, lvl + 1);
            }
        else
            combinations(num, pre, curr + 1, lvl);
    }

    // Print the array pre[]
    else {
        pre[lvl] = '\0';
        printf("%s\n", pre);
    }
}

// Function to find all the numbers formed
// from the input string by replacing '{content}apos; with
// all the digits of the input string
int findNumUtil(char num[])
{
    // Array that stores the digits before
    // the character $ in the input string
    char pre[MAX];

    end = 0;

    // Traverse the input string and check if
    // the current character is a digit
    // if it is then set flag to true
    for (int i = 0; i < strlen(num); i++)
        if (num[i] >= '0' && num[i] <= '9') {
            bool flag = true;

            // Check if current character of the input
            // string is already present in the array set[]
            // then set flag to false
            for (int j = 0; j < end; j++)
                if (set[j] == num[i])
                    flag = false;

            // Flag is true then store the character
            // into set[] and recursively find all
            // the combinations of numbers and store
            // it in the set[] array

            if (flag == true)
                set[end++] = num[i];
        }

    combinations(num, pre, 0, 0);

    return 0;
}

// Function to print all the combinations
// of the numbers by replacing '{content}apos; with
// the other digits of the input string
int findNum(char* num, int* result_count)
{
    int i;
    if (num[i]) {
        result_count[i] = findNumUtil(num);
        return (result_count[i]);
    }
    return 0;
}

// Driver code
int main()
{
    char num[MAX] = "23$";
    int result_count[MAX];

    findNum(num, result_count);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX=20
DIGITS=10

# Array to store all the
# possible numbers
st=['0']*DIGITS
pre=[]

# Index to st[] element
ed=0

# Function to find all the combinations
# of the string by replacing '{content}apos; with
# the other digits of the string
def combinations(curr, lvl):
    global num,pre

    # Check if current length is less than
    # the length of the input string
    if (curr < len(num)):

        # If current character is a digit
        # then store digit into pre[] and
        # recursively find all the combinations
        if (num[curr] >= '0' and num[curr] <= '9'):
            pre[lvl] = num[curr]
            combinations(curr + 1, lvl + 1)

        # If current character is a '{content}apos; then replace
        # it with the other digits of the string and
        # recursively find all the combinations
        # Else go to the next character and
        # recursively find all the combinations
        elif (num[curr] == '{content}apos;):
            for i in range(ed):
                pre[lvl] = st[i]
                combinations(curr + 1, lvl + 1)
        else:
            combinations(curr + 1, lvl)

    # Print array pre[]
    else:
        print(''.join(pre))

# Function to find all the numbers formed
# from the input string by replacing '{content}apos; with
# all the digits of the input string
def findNumUtil():
    # Array that stores the digits before
    # the character $ in the input string
    global pre,ed
    pre=['0']*len(num)

    ed = 0

    # Traverse the input string and check if
    # the current character is a digit
    # if it is then set flag to True
    for i in range(len(num)):
        if (num[i] >= '0' and num[i] <= '9'):
            flag = True

            # Check if current character of the input
            # string is already present in the array set[]
            # then set flag to False
            for j in range(ed):
                if (st[j] == num[i]):
                    flag = False

            # Flag is True then store the character
            # into st[] and recursively find all
            # the combinations of numbers and store
            # it in the st[] array

            if flag:
                st[ed] = num[i]
                ed+=1

    combinations(0, 0)

    return 0

# Function to prall the combinations
# of the numbers by replacing '{content}apos; with
# the other digits of the input string
def findNum(result_count):
    i=0
    if (num[i]):
        result_count[i] = findNumUtil()
        return (result_count[i])
    return 0

# Driver code
if __name__ == '__main__':
    num = "23$"
    result_count=[0]*MAX

    findNum(result_count)
```

**Output**

```
2322
2323
2332
2333
```

**基于内置库/数据集的方法:-**

## C++

```
#include <bits/stdc++.h>
using namespace std;

// stores all possible non-repetitive combinations
// of string by replacing ‘{content}#x2019; with any
//    other digit from the string
unordered_set<string> possible_comb;

void combinations(string s,int i,int n)
{

    if(i==n)
        return;
      // to check whether a string is
      // valid combination
    bool is_combination = true;
    for(int i=0;i<(int)s.length();i++)
    {
        if(s[i]=='{content}apos;)
        {
            is_combination = false;
            break;
        }
    }

    if(is_combination &&  possible_comb.find(s)==possible_comb.end())
    {
        possible_comb.insert(s);
        return;
    }

    for(int i=0;i<n;i++)
    {
        if(s[i]=='{content}apos;)
        {
            for(int j=0;j<n;j++)
            {
                if(s[j]!='{content}apos;)
                {
                      // replace the character having '{content}apos;
                      //    with one of the digit from the
                      // string  and recur in the combination
                      // function
                    s[i] = s[j];
                    combinations(s,j,n);
                    s[i] = '{content}apos;;
                }
            }
        }
    }
}

int main() {
    string s;
    s = "23$";
      int len = (int)s.size();
    combinations(s,0,len);
    for(auto x:possible_comb)
    {
        cout << x << '\n';
    }
    return 0;
}
```

## 蟒蛇 3

```
# stores all possible non-repetitive combinations
# of string by replacing ‘{content}#x2019; with any
#    other digit from the string
possible_comb=set()

def combinations(s,i,n):
    list_s=list(s)
    if(i==n):
        return
    # to check whether a string is
    # valid combination
    is_combination = True
    for i in range(len(s)):
        if(s[i]=='{content}apos;):
            is_combination = False
            break

    if(is_combination and s not in possible_comb):
        possible_comb.add(s)
        return

    for i in range(n):
        if(s[i]=='{content}apos;):
            for j in range(n):
                if(s[j]!='{content}apos;):
                      # replace the character having '{content}apos;
                      #    with one of the digit from the
                      # string  and recur in the combination
                      # function
                    list_s[i] = list_s[j]
                    combinations(''.join(list_s),j,n)
                    list_s[i] = '{content}apos;

if __name__ == '__main__':
    s = "23$"
    combinations(s,0,len(s))
    for x in possible_comb:
        print(x)
```

**Output**

```
2333
2332
2322
2323
```

**时间复杂度:-** O(n^x)其中 x 是字符串中$的实例数，n 是字符串的长度

**辅助空间:-** O(1)