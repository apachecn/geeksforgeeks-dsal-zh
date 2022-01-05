# 磁带上的垂直和水平检索(MRT)

> 原文:[https://www . geesforgeks . org/纵横检索-磁带上的 mrt/](https://www.geeksforgeeks.org/vertical-and-horizontal-retrieval-mrt-on-tapes/)

**先决条件:** [磁带上的最佳存储](https://www.geeksforgeeks.org/optimal-storage-tapes/)
您将获得不同大小的**磁带[]** 和不同卷的**记录[]** 。任务是水平或垂直填充磁带中的卷，以便最大限度地减少检索时间。
**举例:**

> **输入:**磁带[] = { 25，80，160}，记录[] = { 15，2，8，23，45，50，60， 120 }
> **输出:**
> **水平填充:**
> 第一盘磁带:【2 8 15】捷运:12.3333
> 第二盘磁带:【23 45】捷运:45.5
> 第三盘磁带:【50 60】捷运:80
> **垂直填充:**
> 第一盘磁带:【2 23】捷运:13.5
> 第二盘磁带:【8 45】捷运:

对于最短检索时间，我们将按照记录大小的递增顺序插入大量记录。
最小检索时间公式为:

```
MRT = (1/N)*Σ(A(i)*(N-i))
where 0 &leq; i < N
```

有两种在磁带上添加卷以减少检索时间的方法:

1.  水平检索
2.  垂直检索

**<u>横向检索</u>**

<u>我们有，
磁带[] = { 25，80，160}
记录[] = { 2，8，15，23，45，50，60，120 } *(按递增顺序)*
**磁带上的水平填充:**</u> 

1.  <u>插入 2</u> 

```
1st tape : [ 2 ]
2nd tape : [ ]
3rd tape : [ ]
```

2.  <u>插入 8</u> 

```
1st tape : [ 2 8 ]
2nd tape : [ ]
3rd tape : [ ]
```

1.  <u>插入 15</u> 

```
1st tape : [ 2 8 15 ]
2nd tape : [ ]
3rd tape : [ ]
```

1.  <u>插入 23</u> 

```
1st tape : [ 2 8 15 ]
2nd tape : [ 23 ]
3rd tape : [ ]
```

1.  <u>插入 45</u> 

```
1st tape : [ 2 8 15 ]
2nd tape : [ 23 45 ]
3rd tape : [ ]
```

1.  <u>插入 50</u> 

```
1st tape : [ 2 8 15 ]
2nd tape : [ 23 45 ]
3rd tape : [ 50 ]
```

1.  <u>插入 60</u> 

```
1st tape : [ 2 8 15 ]
2nd tape : [ 23 45 ]
3rd tape : [ 50 60 ]
```

<u>以下是水平填充的程序</u> 

## <u>C++</u>

```
// C++ program to print Horizontal
// filling
#include <bits/stdc++.h>
using namespace std;

void horizontalFill(int records[],
                    int tape[], int nt)
{
    // It is used for checking whether
    // tape is full or not
    int sum = 0;

    // It is used for calculating
    // total retrieval time
    int Retrieval_Time = 0;

    // It is used for calculating
    // mean retrieval time
    double Mrt;
    int current = 0;

    // vector is used because n number of
    // records can insert in one tape with
    // size constraint
    vector<int> v;

    for (int i = 0; i < nt; i++) {

        // Null vector obtained to use fresh
        // vector 'v'
        v.clear();
        Retrieval_Time = 0;

        // initialize variables to
        // 0 for each iteration
        sum = 0;
        cout << "tape " << i + 1 << " : [ ";

        // sum is used for checking whether
        // i'th tape is full or not
        sum += records[current];

        // check sum less than size of tape
        while (sum <= tape[i]) {
            cout << records[current] << " ";
            v.push_back(records[current]);

            // increment in j for next record
            current++;
            sum += records[current];
        }
        cout << "]";

        // calculating total retrieval
        // time
        for (int i = 0; i < v.size(); i++) {

            // MRT formula
            Retrieval_Time += v[i] * (v.size() - i);
        }

        // calculating mean retrieval time
        // using formula
        Mrt = (double)Retrieval_Time / v.size();

        // v.size() is function of vector is used
        // to get size of vector
        cout << "\tMRT : " << Mrt << endl;
    }
}

// Driver Code
int main()
{
    int records[] = { 15, 2, 8, 23, 45, 50, 60, 120 };
    int tape[] = { 25, 80, 160 };

    // store the size of records[]
    int n = sizeof(records) / sizeof(records[0]);

    // store the size of tapes[]
    int m = sizeof(tape) / sizeof(tape[0]);

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    sort(records, records + n);
    horizontalFill(records, tape, m);
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to print Horizontal
// filling
import java.util.*;

class GFG
{

static void horizontalFill(int records[],
                    int tape[], int nt)
{
    // It is used for checking whether
    // tape is full or not
    int sum = 0;

    // It is used for calculating
    // total retrieval time
    int Retrieval_Time = 0;

    // It is used for calculating
    // mean retrieval time
    double Mrt;
    int current = 0;

    // vector is used because n number of
    // records can insert in one tape with
    // size constraint
    Vector<Integer> v = new Vector<Integer>();

    for (int i = 0; i < nt; i++)
    {

        // Null vector obtained to use fresh
        // vector 'v'
        v.clear();
        Retrieval_Time = 0;

        // initialize variables to
        // 0 for each iteration
        sum = 0;
        System.out.print("tape " + (i + 1) + " : [ ");

        // sum is used for checking whether
        // i'th tape is full or not
        sum += records[current];

        // check sum less than size of tape
        while (sum <= tape[i])
        {
            System.out.print(records[current] + " ");
            v.add(records[current]);

            // increment in j for next record
            current++;
            sum += records[current];
        }
        System.out.print("]");

        // calculating total retrieval
        // time
        for (int j = 0; j < v.size(); j++)
        {

            // MRT formula
            Retrieval_Time += v.get(j) * (v.size() - j);
        }

        // calculating mean retrieval time
        // using formula
        Mrt = (double)Retrieval_Time / v.size();

        // v.size() is function of vector is used
        // to get size of vector
        System.out.print("\tMRT : " + Mrt +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int records[] = { 15, 2, 8, 23, 45, 50, 60, 120 };
    int tape[] = { 25, 80, 160 };

    // store the size of records[]
    int n = records.length;

    // store the size of tapes[]
    int m = tape.length;

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    Arrays.sort(records);
    horizontalFill(records, tape, m);
}
}

// This code is contributed by 29AjayKumar
```

## <u>蟒蛇 3</u>

```
# Python3 program to print Horizontal
# filling

def horizontalFill(records,  tape, nt) :

    # It is used for checking whether
    # tape is full or not
    sum = 0;

    # It is used for calculating
    # total retrieval time
    Retrieval_Time = 0;

    # It is used for calculating
    # mean retrieval time
    current = 0;

    # vector is used because n number of
    # records can insert in one tape with
    # size constraint
    v = [];

    for i in range(nt) :

        # Null vector obtained to use fresh
        # vector 'v'
        v.clear();
        Retrieval_Time = 0;

        # initialize variables to
        # 0 for each iteration
        sum = 0;
        print("tape" , i + 1  ,": [ ",end ="");

        # sum is used for checking whether
        # i'th tape is full or not
        sum += records[current];

        # check sum less than size of tape
        while (sum <= tape[i]) :
            print(records[current],end= " ");
            v.append(records[current]);

            # increment in j for next record
            current += 1;
            sum += records[current];

        print("]",end="");

        # calculating total retrieval
        # time
        for i in range(len(v)) :

            # MRT formula
            Retrieval_Time += v[i] * (len(v) - i);

        # calculating mean retrieval time
        # using formula
        Mrt = Retrieval_Time / len(v);

        # v.size() is function of vector is used
        # to get size of vector
        print("tMRT :", Mrt);

# Driver Code
if __name__ == "__main__" :

    records = [ 15, 2, 8, 23, 45, 50, 60, 120 ];
    tape = [ 25, 80, 160 ];

    # store the size of records[]
    n = len(records);

    # store the size of tapes[]
    m = len(tape);
    # sorting of an array is required to
    # attain greedy approach of
    # algorithm
    records.sort();
    horizontalFill(records, tape, m);

# This code is contributed by AnkitRai01
```

## <u>C#</u>

```
// C# program to print Horizontal
// filling
using System;
using System.Collections.Generic;

class GFG
{

static void horizontalFill(int []records,
                    int []tape, int nt)
{
    // It is used for checking whether
    // tape is full or not
    int sum = 0;

    // It is used for calculating
    // total retrieval time
    int Retrieval_Time = 0;

    // It is used for calculating
    // mean retrieval time
    double Mrt;
    int current = 0;

    // vector is used because n number of
    // records can insert in one tape with
    // size constraint
    List<int> v = new List<int>();

    for (int i = 0; i < nt; i++)
    {

        // Null vector obtained to use fresh
        // vector 'v'
        v.Clear();
        Retrieval_Time = 0;

        // initialize variables to
        // 0 for each iteration
        sum = 0;
        Console.Write("tape " + (i + 1) + " : [ ");

        // sum is used for checking whether
        // i'th tape is full or not
        sum += records[current];

        // check sum less than size of tape
        while (sum <= tape[i])
        {
            Console.Write(records[current] + " ");
            v.Add(records[current]);

            // increment in j for next record
            current++;
            sum += records[current];
        }
        Console.Write("]");

        // calculating total retrieval
        // time
        for (int j = 0; j < v.Count; j++)
        {

            // MRT formula
            Retrieval_Time += v[j] * (v.Count - j);
        }

        // calculating mean retrieval time
        // using formula
        Mrt = (double)Retrieval_Time / v.Count;

        // v.Count is function of vector is used
        // to get size of vector
        Console.Write("\tMRT : " + Mrt +"\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []records = { 15, 2, 8, 23, 45, 50, 60, 120 };
    int []tape = { 25, 80, 160 };

    // store the size of records[]
    int n = records.Length;

    // store the size of tapes[]
    int m = tape.Length;

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    Array.Sort(records);
    horizontalFill(records, tape, m);
}
}

// This code is contributed by 29AjayKumar
```

## <u>java 描述语言</u>

```
<script>
    // Javascript program to print Horizontal filling

    function horizontalFill(records, tape, nt)
    {
        // It is used for checking whether
        // tape is full or not
        let sum = 0;

        // It is used for calculating
        // total retrieval time
        let Retrieval_Time = 0;

        // It is used for calculating
        // mean retrieval time
        let Mrt;
        let current = 0;

        // vector is used because n number of
        // records can insert in one tape with
        // size constraint
        let v = [];

        for (let i = 0; i < nt; i++)
        {

            // Null vector obtained to use fresh
            // vector 'v'
            v = [];
            Retrieval_Time = 0;

            // initialize variables to
            // 0 for each iteration
            sum = 0;
            document.write("tape " + (i + 1) + " : [ ");

            // sum is used for checking whether
            // i'th tape is full or not
            sum += records[current];

            // check sum less than size of tape
            while (sum <= tape[i])
            {
                document.write(records[current] + " ");
                v.push(records[current]);

                // increment in j for next record
                current++;
                sum += records[current];
            }
            document.write("]");

            // calculating total retrieval
            // time
            for (let j = 0; j < v.length; j++)
            {

                // MRT formula
                Retrieval_Time += v[j] * (v.length - j);
            }

            // calculating mean retrieval time
            // using formula
            Mrt = Retrieval_Time / v.length;

            // v.size() is function of vector is used
            // to get size of vector
            if(i == 0)
            {
                document.write(" MRT : " + Mrt.toFixed(4) +"</br>");
            }
            else{
                document.write(" MRT : " + Mrt +"</br>");
            }
        }
    }

    let records = [ 15, 2, 8, 23, 45, 50, 60, 120 ];
    let tape = [ 25, 80, 160 ];

    // store the size of records[]
    let n = records.length;

    // store the size of tapes[]
    let m = tape.length;

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    records.sort(function(a, b){return a - b});
    horizontalFill(records, tape, m);

// This code is contributed by suresh07.
</script>
```

<u>**Output:** 

```
tape 1 : [ 2 8 15 ]    MRT : 12.3333
tape 2 : [ 23 45 ]    MRT : 45.5
tape 3 : [ 50 60 ]    MRT : 80
```</u> 

<u>**<u>垂直检索</u>**</u>

<u>**磁带上的垂直填充:**</u> 

1.  <u>插入 2</u> 

```
1st tape : [ 2 ]
2nd tape : [ ]
3rd tape : [ ]
```

2.  <u>插入 8</u> 

```
1st tape : [ 2 ]
2nd tape : [ 8 ]
3rd tape : [ ]
```

1.  <u>插入 15</u> 

```
1st tape : [ 2 ]
2nd tape : [ 8 ]
3rd tape : [ 15 ]
```

1.  <u>插入 23</u> 

```
1st tape : [ 2 23 ]
2nd tape : [ 8 ]
3rd tape : [ 15 ]
```

1.  <u>插入 45</u> 

```
1st tape : [ 2 23 ]
2nd tape : [ 8 45 ]
3rd tape : [ 15 ]
```

1.  <u>插入 50</u> 

```
1st tape : [ 2 23 ]
2nd tape : [ 8 45 ]
3rd tape : [ 15 50 ]
```

1.  <u>插入 60</u> 

```
1st tape : [ 2 23 60 ]
2nd tape : [ 8 45 ]
3rd tape : [ 15 50 ]
```

<u>以下是垂直填充的程序</u> 

## <u>C++</u>

```
// C++ program to print Vertical filling
#include <bits/stdc++.h>
using namespace std;

void vertical_Fill(int records[], int tape[],
                   int m, int n)
{
    // 2D matrix for vertical insertion on
    // tapes
    int v[m][n] = { 0 };

    // It is used for checking whether tape
    // is full or not
    int sum = 0;

    // It is used for calculating total
    // retrieval time
    int Retrieval_Time = 0;

    // It is used for calculating mean
    // retrieval time
    double Mrt;

    // It is used for calculating mean
    // retrieval time
    int z = 0, j = 0;

    // vertical insertion on tape
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // initialize variables to
            // 0 for each iteration
            sum = 0;

            // Used for getting 'sum' sizes
            // of records in tape to determine
            // whether tape is full or not
            for (int k = 0; k < i; k++) {
                sum += v[j][k];
            }

            // if tape is not full
            if (sum + records[z] <= tape[j]) {
                v[j][i] = records[z];
                z++;
            }
        }

        // check for ability of tapes to hold
        // value
        if (v[2][i] == 0) {
            break;
        }
    }

    for (int i = 0; i < m; i++) {

        // initialize variables to 0 for each
        // iteration
        Retrieval_Time = 0;

        // display elements of tape
        cout << "tape " << i + 1 << " : [ ";
        for (j = 0; j < n; j++) {

            if (v[i][j] != 0) {
                cout << v[i][j] << " ";
            }
            else {
                break;
            }
        }
        cout << "]";

        // calculating total retrieval time
        for (int k = 0; v[i][k] != 0; k++) {
            // MRT formula
            Retrieval_Time += v[i][k] * (j - k);
        }

        // calculating mean retrieval time
        // using formula
        Mrt = (double)Retrieval_Time / j;

        // v.size() is function of vector is used
        // to get size of vector
        cout << "\tMRT : " << Mrt << endl;
    }
}

// Driver Code
int main()
{
    int records[] = { 15, 2, 8, 23, 45, 50, 60, 120 };
    int tape[] = { 25, 80, 160 };

    // store the size of records[]
    int n = sizeof(records) / sizeof(records[0]);

    // store the size of tapes[]
    int m = sizeof(tape) / sizeof(tape[0]);

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    sort(records, records + n);
    vertical_Fill(records, tape, m, n);
    return 0;
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to print Vertical filling
import java.util.*;

class GFG
{

static void vertical_Fill(int records[], int tape[],
                        int m, int n)
{
    // 2D matrix for vertical insertion on
    // tapes
    int [][]v = new int[m][n];

    // It is used for checking whether tape
    // is full or not
    int sum = 0;

    // It is used for calculating total
    // retrieval time
    int Retrieval_Time = 0;

    // It is used for calculating mean
    // retrieval time
    double Mrt;

    // It is used for calculating mean
    // retrieval time
    int z = 0, j = 0;

    // vertical insertion on tape
    for (int i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
        {

            // initialize variables to
            // 0 for each iteration
            sum = 0;

            // Used for getting 'sum' sizes
            // of records in tape to determine
            // whether tape is full or not
            for (int k = 0; k < i; k++)
            {
                sum += v[j][k];
            }

            // if tape is not full
            if (sum + records[z] <= tape[j])
            {
                v[j][i] = records[z];
                z++;
            }
        }

        // check for ability of tapes to hold
        // value
        if (v[2][i] == 0)
        {
            break;
        }
    }

    for (int i = 0; i < m; i++)
    {

        // initialize variables to 0 for each
        // iteration
        Retrieval_Time = 0;

        // display elements of tape
        System.out.print("tape " + (i + 1)+ " : [ ");
        for (j = 0; j < n; j++)
        {

            if (v[i][j] != 0)
            {
                System.out.print(v[i][j]+ " ");
            }
            else
            {
                break;
            }
        }
        System.out.print("]");

        // calculating total retrieval time
        for (int k = 0; v[i][k] != 0; k++)
        {

            // MRT formula
            Retrieval_Time += v[i][k] * (j - k);
        }

        // calculating mean retrieval time
        // using formula
        Mrt = (double)Retrieval_Time / j;

        // v.size() is function of vector is used
        // to get size of vector
        System.out.print("\tMRT : " + Mrt +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int records[] = { 15, 2, 8, 23, 45, 50, 60, 120 };
    int tape[] = { 25, 80, 160 };

    // store the size of records[]
    int n = records.length;

    // store the size of tapes[]
    int m = tape.length;

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    Arrays.sort(records);
    vertical_Fill(records, tape, m, n);
}
}

// This code is contributed by 29AjayKumar
```

## <u>蟒蛇 3</u>

```
# Python3 program to print Vertical filling
import numpy as np

def vertical_Fill(records, tape, m, n) :

    # 2D matrix for vertical insertion on
    # tapes
    v = np.zeros((m, n)) ;

    # It is used for checking whether tape
    # is full or not
    sum = 0;

    # It is used for calculating total
    # retrieval time
    Retrieval_Time = 0;

    # It is used for calculating mean
    # retrieval time
    Mrt = None;

    # It is used for calculating mean
    # retrieval time
    z = 0; j = 0;

    # vertical insertion on tape
    for i in range(n) :
        for j in range(m) :

            # initialize variables to
            # 0 for each iteration
            sum = 0;

            # Used for getting 'sum' sizes
            # of records in tape to determine
            # whether tape is full or not
            for k in range(i) :
                sum += v[j][k];

            # if tape is not full
            if (sum + records[z] <= tape[j]) :
                v[j][i] = records[z];
                z += 1;

        # check for ability of tapes to hold
        # value
        if (v[2][i] == 0) :
            break;

    for i in range(m) :

        # initialize variables to 0 for each
        # iteration
        Retrieval_Time = 0;

        # display elements of tape
        print("tape" , i + 1 ,": [", end = "");
        for j in range(n) :

            if (v[i][j] != 0) :
                print(v[i][j], end= " ");

            else :
                break;

        print("]", end="");

        k = 0;

        # calculating total retrieval time
        while v[i][k] != 0 :

            # MRT formula
            Retrieval_Time += v[i][k] * (j - k);
            k += 1;

        # calculating mean retrieval time
        # using formula
        Mrt = Retrieval_Time / j;

        # v.size() is function of vector is used
        # to get size of vector
        print("MRT :", Mrt);

# Driver Code
if __name__ == "__main__" :

    records = [ 15, 2, 8, 23, 45, 50, 60, 120 ];
    tape = [ 25, 80, 160 ];

    # store the size of records[]
    n = len(records);

    # store the size of tape[]
    m = len(tape);

    # sorting of an array is required to
    # attain greedy approach of
    # algorithm
    records.sort();
    vertical_Fill(records, tape, m, n);

# This code is contributed by AnkitRai01
```

## <u>C#</u>

```
// C# program to print Vertical filling
using System;

class GFG
{

static void vertical_Fill(int []records, int []tape,
                        int m, int n)
{
    // 2D matrix for vertical insertion on
    // tapes
    int [,]v = new int[m, n];

    // It is used for checking whether tape
    // is full or not
    int sum = 0;

    // It is used for calculating total
    // retrieval time
    int Retrieval_Time = 0;

    // It is used for calculating mean
    // retrieval time
    double Mrt;

    // It is used for calculating mean
    // retrieval time
    int z = 0, j = 0;

    // vertical insertion on tape
    for (int i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
        {

            // initialize variables to
            // 0 for each iteration
            sum = 0;

            // Used for getting 'sum' sizes
            // of records in tape to determine
            // whether tape is full or not
            for (int k = 0; k < i; k++)
            {
                sum += v[j, k];
            }

            // if tape is not full
            if (sum + records[z] <= tape[j])
            {
                v[j, i] = records[z];
                z++;
            }
        }

        // check for ability of tapes to hold
        // value
        if (v[2, i] == 0)
        {
            break;
        }
    }

    for (int i = 0; i < m; i++)
    {

        // initialize variables to 0 for each
        // iteration
        Retrieval_Time = 0;

        // display elements of tape
        Console.Write("tape " + (i + 1) + " : [ ");
        for (j = 0; j < n; j++)
        {

            if (v[i, j] != 0)
            {
                Console.Write(v[i, j]+ " ");
            }
            else
            {
                break;
            }
        }
        Console.Write("]");

        // calculating total retrieval time
        for (int k = 0; v[i, k] != 0; k++)
        {

            // MRT formula
            Retrieval_Time += v[i, k] * (j - k);
        }

        // calculating mean retrieval time
        // using formula
        Mrt = (double)Retrieval_Time / j;

        // v.Count is function of vector is used
        // to get size of vector
        Console.Write("\tMRT : " + Mrt +"\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []records = { 15, 2, 8, 23, 45, 50, 60, 120 };
    int []tape = { 25, 80, 160 };

    // store the size of records[]
    int n = records.Length;

    // store the size of tapes[]
    int m = tape.Length;

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    Array.Sort(records);
    vertical_Fill(records, tape, m, n);
}
}

// This code is contributed by 29AjayKumar
```

## <u>java 描述语言</u>

```
<script>
    // Javascript program to print Vertical filling

    function vertical_Fill(records, tape, m, n)
    {
        // 2D matrix for vertical insertion on
        // tapes
        let v = new Array(m);
        for(let i = 0; i < m; i++)
        {
            v[i] = new Array(n);
            for(let j = 0; j < n; j++)
            {
                v[i][j] = 0;
            }
        }

        // It is used for checking whether tape
        // is full or not
        let sum = 0;

        // It is used for calculating total
        // retrieval time
        let Retrieval_Time = 0;

        // It is used for calculating mean
        // retrieval time
        let Mrt;

        // It is used for calculating mean
        // retrieval time
        let z = 0, j = 0;

        // vertical insertion on tape
        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < m; j++)
            {

                // initialize variables to
                // 0 for each iteration
                sum = 0;

                // Used for getting 'sum' sizes
                // of records in tape to determine
                // whether tape is full or not
                for (let k = 0; k < i; k++)
                {
                    sum += v[j][k];
                }

                // if tape is not full
                if (sum + records[z] <= tape[j])
                {
                    v[j][i] = records[z];
                    z++;
                }
            }

            // check for ability of tapes to hold
            // value
            if (v[2][i] == 0)
            {
                break;
            }
        }

        for (let i = 0; i < m; i++)
        {

            // initialize variables to 0 for each
            // iteration
            Retrieval_Time = 0;

            // display elements of tape
            document.write("tape " + (i + 1)+ " : [ ");
            for (j = 0; j < n; j++)
            {

                if (v[i][j] != 0)
                {
                    document.write(v[i][j]+ " ");
                }
                else
                {
                    break;
                }
            }
            document.write("]");

            // calculating total retrieval time
            for (let k = 0; v[i][k] != 0; k++)
            {

                // MRT formula
                Retrieval_Time += v[i][k] * (j - k);
            }

            // calculating mean retrieval time
            // using formula
            Mrt = Retrieval_Time / j;

            // v.size() is function of vector is used
            // to get size of vector
            if(i != m - 1)
            {
                document.write(" MRT : " + Mrt +"</br>");
            }
            else{
                document.write(" MRT : " + Mrt.toFixed(4) +"</br>");
            }

        }
    }

    let records = [ 15, 2, 8, 23, 45, 50, 60, 120 ];
    let tape = [ 25, 80, 160 ];

    // store the size of records[]
    let n = records.length;

    // store the size of tapes[]
    let m = tape.length;

    // sorting of an array is required to
    // attain greedy approach of
    // algorithm
    records.sort(function(a, b){return a - b});
    vertical_Fill(records, tape, m, n);

 // This code is contributed divyesh072019.
</script>
```

<u>**Output:** 

```
tape 1 : [ 2 23 ]    MRT : 13.5
tape 2 : [ 8 45 ]    MRT : 30.5
tape 3 : [ 15 50 60 ]    MRT : 68.3333
```</u> 

<u>比较两种结果，我们可以使用一种特殊的胶带填充技术，这种技术可以提供最好的结果(最小的 MRT)。</u>