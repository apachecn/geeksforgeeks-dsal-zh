# 给定数字的 2 次方排列

> 原文:[https://www . geesforgeks . org/给定数字的排列是 2 的幂/](https://www.geeksforgeeks.org/permutations-of-a-given-number-that-are-a-powers-of-2/)

给定一个由 **N** 个数字组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是打印 **S** 个数字的所有可能组合，这是 2 的[完美幂。](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)

**示例:**

> **输入:** S = "614"
> **输出:** 4
> **解释:**
> S 的数字的所有可能的 2 的完美幂的组合是 1，4，16，64。
> 
> **输入:**S = " 6 "
> T3】输出: 0

**方法:**给定的问题可以通过[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。想法是[生成字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/) **S** [的所有可能排列，如果是 **2**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 的完美幂，那么打印出来。按照以下步骤解决问题:

*   定义[功能](https://www.geeksforgeeks.org/methods-in-java/) **检查(整数)**以检查给定的**数**是否为 **2** 的幂，并执行以下任务:
    *   如果**号**等于 **0，**则返回**假。**
    *   如果**号**和**号-1 的[位](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/) ，则**返回**真，**否则返回**假。**
*   定义一个[函数](https://www.geeksforgeeks.org/methods-in-java/) **计算(int arr[]，string ans)** 并执行以下任务:
    *   如果[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)和的长度不等于 **0** 和[功能](https://www.geeksforgeeks.org/methods-in-java/)的值。**检查(integer . parsent(ans . trim()))**返回 **true，**然后将该值添加到 HashSet **H[]** 。
    *   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/for-each-loop-in-java/)**【0，10】**，并执行以下任务:
        *   如果**arr【I】**等于 **0** ，则[继续](https://www.geeksforgeeks.org/continue-statement-in-java/)。
        *   否则，通过 **1** 减少**arr【I】**的值，调用[函数](https://www.geeksforgeeks.org/methods-in-java/) **计算(temp)、“”**找到[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**的其他可能排列，并通过 **1** 增加**arr【I】**的值。
*   [初始化一个 HashSet](https://www.geeksforgeeks.org/initializing-hashset-java/) **H[]** 来存储可能的[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)个 2 的幂的数字。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-java/)，比如**temp【】**来存储[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**中整数的频率。
*   [循环迭代](https://www.geeksforgeeks.org/java-while-loop-with-examples/#:~:text=Java%20while%20loop%20is%20a, as%20a%20repeating%20if%20statement.&text=If%20the%20condition%20evaluates%20to, and%20go%20to%20update%20expression.)直到 **N** 不等于 **0** ，执行以下步骤:
    *   将变量 **rem** 初始化为 **N%10** ，并将**温度【rem】**的值增加 **1** 。
    *   将 **N** 的值除以 **10** 。
*   调用[函数](https://www.geeksforgeeks.org/methods-in-java/) **计算(temp，")**找到[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 的可能排列。
*   执行上述步骤后，打印哈希表作为结果。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Stores the all possible generated
// integers from the given string
unordered_set<int> hs;

// Function to check if the
// number is power of 2
bool check(int number)
{
    // If number is 0, then it
    // can't be a power of 2
    if (number == 0) {
        return false;
    }

    // If the bitwise AND of n
    // and n-1 is 0, then only
    // it is a power of 2
    if ((number & (number - 1)) == 0) {
        return true;
    }

    return false;
}

// Function to generate the numbers
void calculate(int* arr, string ans)
{

    if (ans.length() != 0) {

        // Checking the number
        if (check(stoi(ans))) {
            hs.insert(stoi(ans));
        }
    }

    // Iterate over the range
    for (int i = 0; i < 10; ++i) {

        if (arr[i] == 0) {
            continue;
        }

        else {

            // Use the number
            arr[i]--;
            calculate(arr,(ans +  to_string(i)));

            // Backtracking Step
            arr[i]++;
        }
    }
}

// Function to find the all possible
// permutations
void generatePermutation(int n)
{
    hs.clear();
    // Stores the frequency of digits
    int temp[10];
    for (int i = 0; i < 10; i++) {
        temp[i] = 0;
    }

    // Iterate over the number
    while (n != 0) {
        int rem = n % 10;
        temp[rem]++;
        n = n / 10;
    }

    // Function Call
    calculate(temp, "");

    // Print the result
    cout << hs.size() << "\n";
    for (auto i : hs) {
        cout << i << " ";
    }
}

int main()
{

    int N = 614;
    generatePermutation(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

public class GFG {

    // Stores the all possible generated
    // integers from the given string
    static HashSet<Integer> H = new HashSet<>();

    // Function to check if the
    // number is power of 2
    static boolean check(int number)
    {
        // If number is 0, then it
        // can't be a power of 2
        if (number == 0) {
            return false;
        }

        // If the bitwise AND of n
        // and n-1 is 0, then only
        // it is a power of 2
        if ((number & (number - 1)) == 0) {
            return true;
        }

        return false;
    }

    // Function to generate the numbers
    static void calculate(
        int arr[], String ans)
    {

        if (ans.length() != 0) {

            // Checking the number
            if (check(Integer.parseInt(
                    ans.trim()))) {
                H.add(Integer.parseInt(
                    ans.trim()));
            }
        }

        // Iterate over the range
        for (int i = 0; i < arr.length; ++i) {

            if (arr[i] == 0) {
                continue;
            }

            else {

                // Use the number
                arr[i]--;
                calculate(arr, ans + i);

                // Backtracking Step
                arr[i]++;
            }
        }
    }

    // Function to find the all possible
    // permutations
    static void generatePermutation(int n)
    {
        // Stores the frequency of digits
        int temp[] = new int[10];

        // Iterate over the number
        while (n != 0) {
            int rem = n % 10;
            temp[rem]++;
            n = n / 10;
        }

        // Function Call
        calculate(temp, "");

        // Print the result
        System.out.println(H.size());
        System.out.println(H);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 614;
        generatePermutation(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the all possible generated
# integers from the given string
H = set()

# Function to check if the
# number is power of 2
def check(number):

    # If number is 0, then it
    # can't be a power of 2
    if (number == 0):
        return False

    # If the bitwise AND of n
    # and n-1 is 0, then only
    # it is a power of 2
    if ((number & (number - 1)) == 0):
        return True

    return False

# Function to generate the numbers
def calculate(arr, ans):
    if (len(ans) != 0):
        # Checking the number
        if (check(int(ans))):
            H.add(int(ans))

    # Iterate over the range
    for i in range(len(arr)):
        if (arr[i] == 0):
            continue
        else:
            # Use the number
            arr[i]-=1
            calculate(arr, ans + str(i))

            # Backtracking Step
            arr[i]+=1

# Function to find the all possible
# permutations
def generatePermutation(n):

    # Stores the frequency of digits
    h = [16, 64, 1, 4]
    temp = [0]*(10)

    # Iterate over the number
    while (n != 0):
        rem = n % 10
        temp[rem]+=1
        n = int(n / 10)

    # Function Call
    calculate(temp, "")

    # Print the result
    print(len(H))
    print(h)

N = 614
generatePermutation(N)

# This code is contributed by divyesh072019.
```

## C#

```
using System;
using System.Collections.Generic;
public class GFG{

  // Stores the all possible generated
    // integers from the given string
    static HashSet<int> H = new HashSet<int>();

    // Function to check if the
    // number is power of 2
    static bool check(int number)
    {
        // If number is 0, then it
        // can't be a power of 2
        if (number == 0) {
            return false;
        }

        // If the bitwise AND of n
        // and n-1 is 0, then only
        // it is a power of 2
        if ((number & (number - 1)) == 0) {
            return true;
        }

        return false;
    }

    // Function to generate the numbers
    static void calculate(
        int[] arr, String ans)
    {

        if (ans.Length != 0) {

            // Checking the number
            if (check(int.Parse(
                    ans))) {
                H.Add(int.Parse(
                    ans));
            }
        }

        // Iterate over the range
        for (int i = 0; i < arr.Length; ++i) {

            if (arr[i] == 0) {
                continue;
            }

            else {

                // Use the number
                arr[i]--;
                calculate(arr, ans + i);

                // Backtracking Step
                arr[i]++;
            }
        }
    }

    // Function to find the all possible
    // permutations
    static void generatePermutation(int n)
    {
        // Stores the frequency of digits
        int[] temp = new int[10];

        // Iterate over the number
        while (n != 0) {
            int rem = n % 10;
            temp[rem]++;
            n = n / 10;
        }

        // Function Call
        calculate(temp, "");

        // Print the result
        Console.WriteLine(H.Count);
      foreach(var val in H){
        Console.Write(val+" ");
      }
    }
    static public void Main (){

      int N = 614;
      generatePermutation(N);
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Stores the all possible generated
    // integers from the given string
    let H = new Set();

    // Function to check if the
    // number is power of 2
    function check(number)
    {
        // If number is 0, then it
        // can't be a power of 2
        if (number == 0) {
            return false;
        }

        // If the bitwise AND of n
        // and n-1 is 0, then only
        // it is a power of 2
        if ((number & (number - 1)) == 0) {
            return true;
        }

        return false;
    }

    // Function to generate the numbers
    function calculate(arr, ans)
    {

        if (ans.length != 0) {

            // Checking the number
            if (check(parseInt(ans))) {
                H.add(parseInt(ans));
            }
        }

        // Iterate over the range
        for (let i = 0; i < arr.length; ++i) {

            if (arr[i] == 0) {
                continue;
            }

            else {

                // Use the number
                arr[i]--;
                calculate(arr, ans + i);

                // Backtracking Step
                arr[i]++;
            }
        }
    }

    // Function to find the all possible
    // permutations
    function generatePermutation(n)
    {
        // Stores the frequency of digits
        let temp = new Array(10);
        let h = [16, 64, 1, 4];
        temp.fill(0);

        // Iterate over the number
        while (n != 0) {
            let rem = n % 10;
            temp[rem]++;
            n = parseInt(n / 10, 10);
        }

        // Function Call
        calculate(temp, "");

        // Print the result
        document.write(H.size + "</br>" + "[");
        for(let i = 0; i < h.length - 1; i++)
        {
            document.write(h[i] + ", ");
        }
        document.write(h[h.length - 1] + "]");
    }

    let N = 614;
      generatePermutation(N);

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
4
[16, 64, 1, 4]
```

***时间复杂度:**O(N * 9<sup>N</sup>)*
***辅助空间:** O(1)*

***【高效方法】*** :想法是最初生成 2 的所有幂，并将它们存储在适当的数据结构中(在这种情况下为“CPP 的集合”)，并检查字符串中是否存在 2 的幂

*   这里的难点是检查两个幂是否成串存在。
*   检查字符串中两个出口的幂是否为 2 的一种简单方法是生成所有可能的字符串排列，并验证该字符串是否为或字符串的幂为 2。不建议使用这种方法，因为时间复杂度约为 O(n！)
*   一种有效的方法是使用计数数组，该数组存储十进制数字的计数，并验证 2 的幂的每个十进制数字的计数是否小于或等于字符串中存在的十进制数字的计数。

## C++14

```
#include<bits/stdc++.h>
using namespace std;

void calculatePower(string s,int n,set<long long>&ans)
{
    // cnt_s is stores the count of each decimal digits of string s
    int cnt_s[10]={0};
    // Here we calculate the count of each decimal digit of string s
    for(int i=0;i<n;i++)
    {
        cnt_s[s[i]-'0']++;
    }
    // our main logic is to generate powers of 2 and store the count of decimal digit of powers of 2 in
    // cnt_a i.e we check for every i in range(0,10): if(cnt_s[i]>=cnt_[a])
    long val=2,one=1;
    long maxval=(one<<62);
    // maxval has max power of 2 in range of long
    // in this loop we generate powers of 2
    while(val<=maxval&&val>0)
    {
        long temp=val;
        int cnt_a[10]={0};
        // cnt_a has count of decimal digits in kth power of 2
        while(temp)
        {
            long remainder=(temp%10);
            cnt_a[remainder]++;
            temp/=10;
        }
        // checking if a power of 2 present in string s
        bool fl=true;
        for(int i=0;i<10;i++)
        {
            if(cnt_a[i]>cnt_s[i])
            {
                fl=false;
                break;
            }
        }
        // if the power of 2 present in s we add it to set
        if(fl)
        {
            ans.insert(val);
        }
        val*=2;
    }
}
int main()
{
     string s="614";
      int n=s.length();

    // set-ans has all possible powers of 2 that are present in string
    set<long long>ans;
      calculatePower(s,n,ans);
    cout<<"THE TOTAL POSSIBLE COMBINATIONS THAT ARE POWER OF 2 ARE:  "<<ans.size()<<"\n";
      for(auto i:ans)
    {
        cout<<i<<"\n";
    }
}
```

## C

```
#include<stdio.h>
#include<string.h>

void calculatePower(char s[],int n)
{
    // cnt_s is stores the count of each decimal digits of string s
    int cnt_s[10]={0};
    // Here we calculate the count of each decimal digit of string s
    for(int i=0;i<n;i++)
    {
        cnt_s[s[i]-'0']++;
    }
    // our main logic is to generate powers of 2 and store the count of decimal digit of powers of 2 in
    // cnt_a i.e we check for every i in range(0,10): if(cnt_s[i]>=cnt_[a])
    long val=2,one=1;
    long maxval=(one<<62);
    // maxval has max power of 2 in range of long
    // in this loop we generate power of 2
    while(val<=maxval&&val>0)
    {
        long temp=val;
        int cnt_a[10]={0};
        // cnt_a has count of decimal digits in kth power of 2
        while(temp)
        {
            long remainder=(temp%10);
            cnt_a[remainder]++;
            temp/=10;
        }
        // checking if a power of 2 present in string s
        int fl=1;
        for(int i=0;i<10;i++)
        {
            if(cnt_a[i]>cnt_s[i])
            {
                fl=0;
                break;
            }
        }
        if(fl)
        {
            printf("%ld  is present in string\n",val);
        }
        val*=2;
    }
}
int main()
{
    char s[]="614";
    int n=strlen(s);
      calculatePower(s,n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
public class Main
{
    public static void calculatePower(String s,int n)
    {
        ArrayList<Long> ans=new ArrayList<Long>();
        // cnt_s is stores the count of each decimal digits of string s
        int cnt_s[]=new int[10];
        // Here we calculate the count of each decimal digit of string s
        for(int i=0;i<n;i++)
        {
            cnt_s[s.charAt(i)-'0']++;
        }
        // our main logic is to generate powers of 2 and store the count of decimal digit of powers of 2 in
        // cnt_a i.e we check for every i in range(0,10): if(cnt_s[i]>=cnt_[a])
        long value=2,one=1;
        long maxvalue=(one<<62);
        // maxval has max power of 2 in range of long
        // in this loop we generate powers of 2
        while(value<=maxvalue && value>=0)
        {
            long temp=value;
            int cnt_a[]=new int[10];
            // cnt_a has count of decimal digits in kth power of 2
            while(temp>0)
            {
                long remainder=(temp%10);
                cnt_a[(int)remainder]++;
                temp/=10;
            }
            // checking if a power of 2 present in string s
            boolean fl=true;
            for(int i=0;i<10;i++)
            {
                if(cnt_a[i]>cnt_s[i])
                {
                    fl=false;
                    break;
                }
            }
            // if the power of 2 present in s we add it to ans
            if(fl)
            {
                ans.add(value);
            }
            value*=2;
        }
        System.out.println("THE TOTAL POSSIBLE COMBINATIONS THAT ARE POWER OF 2 ARE: "+ans.size());
        for(Long i:ans)
        {
            System.out.println(i);
        }
    }
    public static void main(String[] args) {
        String s="614";
        int n=s.length();
        calculatePower(s,n);
    }
}
```

## 蟒蛇 3

```
def calculatePower(s,n):
    # cnt_s is stores the count of each decimal digits of string s
    cnt_s=[0]*10
    # Here we calculate the count of each decimal digit of string s
    for i in s:
        cnt_s[int(i)]+=1
    # our main logic is to generate powers of 2 and store the count of decimal digit of powers of 2 in  cnt_a i.e we check for every i in range(0,10): if(cnt_s[i]>=cnt_[a])

    one=1
    value=2
    maxvalue=(one<<62)
    ans=[]
    # maxval has max power of 2 in range of long in this loop we generate powers of 2
    while(value<=maxvalue):
        # cnt_a has count of decimal digits in kth power of 2
        cnt_a=[0]*10
        fl=True
        temp=value
        while(temp>0):
            remainder=temp%10
            cnt_a[remainder]+=1
            temp=int(temp/10)
        # checking if a power of 2 present in string s
        for i in range(0,10):
            if(cnt_a[i]>cnt_s[i]):
                fl=False
                break
        # if the power of 2 present in s we add it to ans
        if(fl):
            ans.append(value)
        value*=2
    print("THE TOTAL POSSIBLE COMBINATIONS THAT ARE POWER OF 2 ARE: ",len(ans))
    for i in ans:
        print(i)

s="614"
n=len(s)
calculatePower(s,n)
```

***时间复杂度:O(log(2^62) * N)其中 n 是字符串和 log(2^62 的长度)因为 2^62 是长范围内的最大有效功率***
***辅助空间:O(10+10)***