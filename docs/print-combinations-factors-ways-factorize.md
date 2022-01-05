# 打印所有因子组合(因子分解方式)

> 原文:[https://www . geeksforgeeks . org/print-complements-factors-way-factorsize/](https://www.geeksforgeeks.org/print-combinations-factors-ways-factorize/)

写一个程序，打印给定数字 n 的所有因子组合。

**示例:**

```
Input : 16
Output :2 2 2 2 
        2 2 4 
        2 8 
        4 4 

Input : 12
Output : 2 2 3
         2 6
         3 4
```

为了解决这个问题，我们采用一个整数数组或整数列表来存储给定 n 的所有可能的因子组合。因此，为了实现这一点，我们可以有一个递归函数来存储每次迭代中的因子组合。每个列表都应该存储在最终结果列表中。

下面是上述方法的实现。

**Output**

```
2 2 2 2 
2 2 4 
2 8 
4 4 
```

#### 另一种方法:

下面的代码是用于打印所有因子组合的纯递归代码:

它使用整数向量来存储单个因子列表，使用整数向量来存储所有因子组合。它不是使用迭代循环，而是使用相同的递归函数来计算所有因子组合。

## C++

```
// C++ program to print all factors combination
#include <bits/stdc++.h>
using namespace std;

// vector of vector for storing
// list of factor combinations
vector<vector<int> > factors_combination;

// recursive function
void compute_factors(int current_no, int n, int product,
                     vector<int> single_list)
{

    // base case: if the pruduct
    // exceeds our given number;
    // OR
    // current_no exceeds half the given n
    if (current_no > (n / 2) || product > n)
        return;

    // if current list of factors
    // is contributing to n
    if (product == n) {

        // storing the list
        factors_combination.push_back(single_list);

        // into factors_combination
        return;
    }

    // including current_no in our list
    single_list.push_back(current_no);

    // trying to get required
    // n with including current
    // current_no
    compute_factors(current_no, n, product * current_no,
                    single_list);

    // excluding current_no from our list
    single_list.pop_back();

    // trying to get required n
    // without including current
    // current_no
    compute_factors(current_no + 1, n, product,
                    single_list);
}

// Driver Code
int main()
{
    int n = 16;

    // vector to store single list of factors
    // eg. 2,2,2,2 is one of the list for n=16
    vector<int> single_list;

    // compute_factors ( starting_no, given_n,
    // our_current_product, vector )
    compute_factors(2, n, 1, single_list);

    // printing all possible factors stored in
    // factors_combination
    for (int i = 0; i < factors_combination.size(); i++) {
        for (int j = 0; j < factors_combination[i].size();
             j++)
            cout << factors_combination[i][j] << " ";
        cout << endl;
    }
    return 0;
}

// code contributed by Devendra Kolhe
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all factors combination
import java.util.*;

class GFG{

// vector of vector for storing
// list of factor combinations
static Vector<Vector<Integer>> factors_combination =
   new Vector<Vector<Integer>>();

// Recursive function
static void compute_factors(int current_no, int n, int product,
                            Vector<Integer> single_list)
{

    // base case: if the pruduct
    // exceeds our given number;
    // OR
    // current_no exceeds half the given n
    if (current_no > (n / 2) || product > n)
        return;

    // If current list of factors
    // is contributing to n
    if (product == n)
    {

        // Storing the list
        factors_combination.add(single_list);

        // Printing all possible factors stored in
        // factors_combination
        for(int i = 0; i < factors_combination.size(); i++)
        {
            for(int j = 0; j < factors_combination.get(i).size(); j++)
                System.out.print(factors_combination.get(i).get(j) + " ");
        }
        System.out.println();
        factors_combination = new Vector<Vector<Integer>>();

        // Into factors_combination
        return;
    }

    // Including current_no in our list
    single_list.add(current_no);

    // Trying to get required
    // n with including current
    // current_no
    compute_factors(current_no, n,
                    product * current_no,
                    single_list);

    // Excluding current_no from our list
    single_list.remove(single_list.size() - 1);

    // Trying to get required n
    // without including current
    // current_no
    compute_factors(current_no + 1, n, product,
                    single_list);
}

// Driver code
public static void main(String[] args)
{
    int n = 16;

    // Vector to store single list of factors
    // eg. 2,2,2,2 is one of the list for n=16
    Vector<Integer> single_list = new Vector<Integer>();

    // compute_factors ( starting_no, given_n,
    // our_current_product, vector )
    compute_factors(2, n, 1, single_list);
}
}

// This code is contributed by decode2207
```

## 蟒蛇 3

```
# Python3 program to print all factors combination

# vector of vector for storing
# list of factor combinations
factors_combination = []

# recursive function
def compute_factors(current_no, n, product, single_list):
    global factors_combination

    # base case: if the pruduct
    # exceeds our given number;
    # OR
    # current_no exceeds half the given n
    if ((current_no > int(n / 2)) or (product > n)):
        return

    # if current list of factors
    # is contributing to n
    if (product == n):
        # storing the list
        factors_combination.append(single_list)

        # printing all possible factors stored in
        # factors_combination
        for i in range(len(factors_combination)):
            for j in range(len(factors_combination[i])):
                print(factors_combination[i][j], end=" ")
        print()
        factors_combination = []
        # into factors_combination
        return

    # including current_no in our list
    single_list.append(current_no)

    # trying to get required
    # n with including current
    # current_no
    compute_factors(current_no, n, product * current_no, single_list)

    # excluding current_no from our list
    single_list.pop()

    # trying to get required n
    # without including current
    # current_no
    compute_factors(current_no + 1, n, product, single_list)

n = 16

# vector to store single list of factors
# eg. 2,2,2,2 is one of the list for n=16
single_list = []

# compute_factors ( starting_no, given_n,
# our_current_product, vector )
compute_factors(2, n, 1, single_list)

# This code is contributed by ukasp.
```

## C#

```
// C# program to print all factors combination
using System;
using System.Collections.Generic;
class GFG {

    // vector of vector for storing
    // list of factor combinations
    static List<List<int>> factors_combination = new List<List<int>>();

    // recursive function
    static void compute_factors(int current_no, int n, int product, List<int> single_list)
    {

        // base case: if the pruduct
        // exceeds our given number;
        // OR
        // current_no exceeds half the given n
        if (current_no > (n / 2) || product > n)
            return;

        // if current list of factors
        // is contributing to n
        if (product == n) {

            // storing the list
            factors_combination.Add(single_list);
            // printing all possible factors stored in
            // factors_combination
            for(int i = 0; i < factors_combination.Count; i++)
            {
                for(int j = 0; j < factors_combination[i].Count; j++)
                Console.Write(factors_combination[i][j] + " ");
            }
            Console.WriteLine();
            factors_combination = new List<List<int>>();
            // into factors_combination
            return;
        }

        // including current_no in our list
        single_list.Add(current_no);

        // trying to get required
        // n with including current
        // current_no
        compute_factors(current_no, n, product * current_no, single_list);

        // excluding current_no from our list
        single_list.RemoveAt(single_list.Count - 1);

        // trying to get required n
        // without including current
        // current_no
        compute_factors(current_no + 1, n, product, single_list);
    }

  static void Main() {
    int n = 16;

    // vector to store single list of factors
    // eg. 2,2,2,2 is one of the list for n=16
    List<int> single_list = new List<int>();

    // compute_factors ( starting_no, given_n,
    // our_current_product, vector )
    compute_factors(2, n, 1, single_list);
  }
}

// This code is contributed by divyesh072019.
```

**Output**

```
2 2 2 2 
2 2 4 
2 8 
4 4 
```