# 步进编号

> 原文： [https://www.geeksforgeeks.org/stepping-numbers/](https://www.geeksforgeeks.org/stepping-numbers/)

给定两个整数“ n”和“ m”，找到范围为[n，m]的所有步进数。 如果所有相邻数字的绝对差为 1，则此数字称为**步进数**。321 是步进数，而 421 不是。

**示例**：

```
Input : n = 0, m = 21
Output : 0 1 2 3 4 5 6 7 8 9 10 12 21

Input : n = 10, m = 15
Output : 10, 12

```

**方法 1：蛮力方法**

在这种方法中，使用蛮力方法来遍历从 n 到 m 的所有整数，并检查它是否是一个步进数。

## C++

```cpp

// A C++ program to find all the Stepping Number in [n, m] 
#include<bits/stdc++.h> 
using namespace std; 

// This function checks if an integer n is a Stepping Number 
bool isStepNum(int n) 
{ 
    // Initalize prevDigit with -1 
    int prevDigit = -1; 

    // Iterate through all digits of n and compare difference 
    // between value of previous and current digits 
    while (n) 
    { 
        // Get Current digit 
        int curDigit = n % 10; 

        // Single digit is consider as a 
        // Stepping Number 
        if (prevDigit == -1) 
            prevDigit = curDigit; 
        else
        { 
            // Check if absolute difference between 
            // prev digit and current digit is 1 
            if (abs(prevDigit - curDigit) != 1) 
                 return false; 
        } 
        prevDigit = curDigit; 
        n /= 10; 
    } 

    return true; 
} 

// A brute force approach based function to find all 
// stepping numbers. 
void displaySteppingNumbers(int n, int m) 
{ 
    // Iterate through all the numbers from [N,M] 
    // and check if it’s a stepping number. 
    for (int i=n; i<=m; i++) 
        if (isStepNum(i)) 
            cout << i << " "; 
} 

// Driver program to test above function 
int main() 
{ 
    int n = 0, m = 21; 

    // Display Stepping Numbers in 
    // the range [n, m] 
    displaySteppingNumbers(n, m); 

    return 0; 
} 

```

## Java

```java

// A Java program to find all the Stepping Number in [n, m] 
class Main 
{ 
    // This Method checks if an integer n 
    // is a Stepping Number 
    public static boolean isStepNum(int n) 
    { 
        // Initalize prevDigit with -1 
        int prevDigit = -1; 

        // Iterate through all digits of n and compare 
        // difference between value of previous and 
        // current digits 
        while (n > 0) 
        { 
            // Get Current digit 
            int curDigit = n % 10; 

            // Single digit is consider as a 
            // Stepping Number 
            if (prevDigit != -1) 
            { 
                // Check if absolute difference between 
                // prev digit and current digit is 1 
                if (Math.abs(curDigit-prevDigit) != 1) 
                    return false; 
            } 
            n /= 10; 
            prevDigit = curDigit; 
        } 
        return true; 
    } 

    // A brute force approach based function to find all 
    // stepping numbers. 
    public static void displaySteppingNumbers(int n,int m) 
    { 
        // Iterate through all the numbers from [N,M] 
        // and check if it is a stepping number. 
        for (int i = n; i <= m; i++) 
            if (isStepNum(i)) 
                System.out.print(i+ " "); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int n = 0, m = 21; 

        // Display Stepping Numbers in the range [n,m] 
        displaySteppingNumbers(n,m); 
    } 
} 

```

## C#

```cs

// A C# program to find all  
// the Stepping Number in [n, m] 
using System; 

class GFG 
{ 
    // This Method checks if an  
    // integer n is a Stepping Number 
    public static bool isStepNum(int n) 
    { 
        // Initalize prevDigit with -1 
        int prevDigit = -1; 

        // Iterate through all digits  
        // of n and compare difference  
        // between value of previous  
        // and current digits 
        while (n > 0) 
        { 
            // Get Current digit 
            int curDigit = n % 10; 

            // Single digit is considered  
            // as a Stepping Number 
            if (prevDigit != -1) 
            { 
                // Check if absolute difference  
                // between prev digit and current  
                // digit is 1 
                if (Math.Abs(curDigit -  
                             prevDigit) != 1) 
                    return false; 
            } 
            n /= 10; 
            prevDigit = curDigit; 
        } 
        return true; 
    } 

    // A brute force approach based  
    // function to find all stepping numbers. 
    public static void displaySteppingNumbers(int n,  
                                              int m) 
    { 
        // Iterate through all the numbers  
        // from [N,M] and check if it is  
        // a stepping number. 
        for (int i = n; i <= m; i++) 
            if (isStepNum(i)) 
                Console.Write(i+ " "); 
    } 

    // Driver code 
    public static void Main() 
    { 
        int n = 0, m = 21; 

        // Display Stepping Numbers  
        // in the range [n,m] 
        displaySteppingNumbers(n, m); 
    } 
} 

// This code is contributed by nitin mittal. 

```

**Output :**

```
0 1 2 3 4 5 6 7 8 9 10 12 21 

```

**方法 2：使用 BFS / DFS**

这个想法是使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) / [深度优先搜索](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)遍历。

**如何建立图表？**
图中的每个节点代表一个步进数； 如果可以从 U 转换 V，则从节点 U 到 V 会有一个有向边。（U 和 V 是步进数）可以按照以下方式从 U 转换步进数 V。

**lastDigit** 是指 U 的最后一位数字（即 U％10）。
相邻数字`V`可以是：

*   U * 10 + lastDigit +1（邻居 A）
*   U * 10 + lastDigit – 1（邻居 B）

通过执行上述操作，新的数字将附加到 U，即为 lastDigit-1 或 lastDigit + 1，因此由 U 形成的新数字 V 也是步进数。
因此，每个节点最多具有 2 个相邻节点。

**边情况**：当 U 的最后一位是`0`或`9`

**情况 1**：lastDigit 为 0：在这种情况下，只能附加数字“ 1”。
**情况 2**：lastDigit 为 9：在这种情况下，只能附加数字“ 8”。

**什么是源/起始节点？**

*   每个单个数字都被视为一个步进数字，因此每个数字的 bfs 遍历将给出从该数字开始的所有步进数字​​。
*   对[0,9]中的所有数字进行 bfs / dfs 遍历。

**注意**：对于节点 0，在 BFS 遍历期间无需探索邻居，因为它将导致 01、012、010，并且这些将被从节点 1 开始的 BFS 遍历覆盖。
 **查找从 0 到 21 的所有步进编号的示例**

```
-> 0 is a stepping Number and it is in the range
   so display it.
-> 1 is a Stepping Number, find neighbors of 1 i.e.,
   10 and 12 and push them into the queue

How to get 10 and 12?
Here U is 1 and last Digit is also 1 
V = 10 + 0 = 10 ( Adding lastDigit - 1 )
V = 10 + 2 = 12 ( Adding lastDigit + 1 )

Then do the same for 10 and 12 this will result into
101, 123, 121 but these Numbers are out of range. 
Now any number transformed from 10 and 12 will result
into a number greater than 21 so no need to explore 
their neighbors.

-> 2 is a Stepping Number, find neighbors of 2 i.e. 
   21, 23.
-> 23 is out of range so it is not considered as a 
   Stepping Number (Or a neighbor of 2)

The other stepping numbers will be 3, 4, 5, 6, 7, 8, 9.

```

**基于 BFS 的解决方案**：

## C++

```cpp

// A C++ program to find all the Stepping Number from N=n 
// to m using BFS Approach 
#include<bits/stdc++.h> 
using namespace std; 

// Prints all stepping numbers reachable from num 
// and in range [n, m] 
void bfs(int n, int m, int num) 
{ 
    // Queue will contain all the stepping Numbers 
    queue<int> q; 

    q.push(num); 

    while (!q.empty()) 
    { 
        // Get the front element and pop from the queue 
        int stepNum = q.front(); 
        q.pop(); 

        // If the Stepping Number is in the range 
        // [n, m] then display 
        if (stepNum <= m && stepNum >= n) 
            cout << stepNum << " "; 

        // If Stepping Number is 0 or greater than m, 
        // need to explore the neighbors 
        if (num == 0 || stepNum > m) 
            continue; 

        // Get the last digit of the currently visited 
        // Stepping Number 
        int lastDigit = stepNum % 10; 

        // There can be 2 cases either digit to be 
        // appended is lastDigit + 1 or lastDigit - 1 
        int stepNumA = stepNum * 10 + (lastDigit- 1); 
        int stepNumB = stepNum * 10 + (lastDigit + 1); 

        // If lastDigit is 0 then only possible digit 
        // after 0 can be 1 for a Stepping Number 
        if (lastDigit == 0) 
            q.push(stepNumB); 

        //If lastDigit is 9 then only possible 
        //digit after 9 can be 8 for a Stepping 
        //Number 
        else if (lastDigit == 9) 
            q.push(stepNumA); 

        else
        { 
            q.push(stepNumA); 
            q.push(stepNumB); 
        } 
    } 
} 

// Prints all stepping numbers in range [n, m] 
// using BFS. 
void displaySteppingNumbers(int n, int m) 
{ 
    // For every single digit Number 'i' 
    // find all the Stepping Numbers 
    // starting with i 
    for (int i = 0 ; i <= 9 ; i++) 
        bfs(n, m, i); 
} 

//Driver program to test above function 
int main() 
{ 
    int n = 0, m = 21; 

    // Display Stepping Numbers in the 
    // range [n,m] 
    displaySteppingNumbers(n,m); 

    return 0; 
} 

```

## Java

```java

// A Java program to find all the Stepping Number in 
// range [n, m] 
import java.util.*; 

class Main 
{ 
    // Prints all stepping numbers reachable from num 
    // and in range [n, m] 
    public static void bfs(int n,int m,int num) 
    { 
        // Queue will contain all the stepping Numbers 
        Queue<Integer> q = new LinkedList<Integer> (); 

        q.add(num); 

        while (!q.isEmpty()) 
        { 
            // Get the front element and pop from 
            // the queue 
            int stepNum = q.poll(); 

            // If the Stepping Number is in 
            // the range [n,m] then display 
            if (stepNum <= m && stepNum >= n) 
            { 
                System.out.print(stepNum + " "); 
            } 

            // If Stepping Number is 0 or greater 
            // then m ,need to explore the neighbors 
            if (stepNum == 0 || stepNum > m) 
                continue; 

            // Get the last digit of the currently 
            // visited Stepping Number 
            int lastDigit = stepNum % 10; 

            // There can be 2 cases either digit 
            // to be appended is lastDigit + 1 or 
            // lastDigit - 1 
            int stepNumA = stepNum * 10 + (lastDigit- 1); 
            int stepNumB = stepNum * 10 + (lastDigit + 1); 

            // If lastDigit is 0 then only possible 
            // digit after 0 can be 1 for a Stepping 
            // Number 
            if (lastDigit == 0) 
                q.add(stepNumB); 

            // If lastDigit is 9 then only possible 
            // digit after 9 can be 8 for a Stepping 
            // Number 
            else if (lastDigit == 9) 
                q.add(stepNumA); 

            else
            { 
                q.add(stepNumA); 
                q.add(stepNumB); 
            } 
        } 
    } 

    // Prints all stepping numbers in range [n, m] 
    // using BFS. 
    public static void displaySteppingNumbers(int n,int m) 
    { 
        // For every single digit Number 'i' 
        // find all the Stepping Numbers 
        // starting with i 
        for (int i = 0 ; i <= 9 ; i++) 
            bfs(n, m, i); 
    } 

    //Driver code 
    public static void main(String args[]) 
    { 
        int n = 0, m = 21; 

        // Display Stepping Numbers in 
        // the range [n,m] 
        displaySteppingNumbers(n,m); 
    } 
} 

```

**基于 DFS 的解决方案**

## C++

```cpp

// A C++ program to find all the Stepping Numbers 
// in range [n, m] using DFS Approach 
#include<bits/stdc++.h> 
using namespace std; 

// Prints all stepping numbers reachable from num 
// and in range [n, m] 
void dfs(int n, int m, int stepNum) 
{ 
    // If Stepping Number is in the 
    // range [n,m] then display 
    if (stepNum <= m && stepNum >= n) 
        cout << stepNum << " "; 

    // If Stepping Number is 0 or greater 
    // than m, then return 
    if (stepNum == 0 || stepNum > m) 
        return ; 

    // Get the last digit of the currently 
    // visited Stepping Number 
    int lastDigit = stepNum % 10; 

    // There can be 2 cases either digit 
    // to be appended is lastDigit + 1 or 
    // lastDigit - 1 
    int stepNumA = stepNum*10 + (lastDigit-1); 
    int stepNumB = stepNum*10 + (lastDigit+1); 

    // If lastDigit is 0 then only possible 
    // digit after 0 can be 1 for a Stepping 
    // Number 
    if (lastDigit == 0) 
        dfs(n, m, stepNumB); 

    // If lastDigit is 9 then only possible 
    // digit after 9 can be 8 for a Stepping 
    // Number 
    else if(lastDigit == 9) 
        dfs(n, m, stepNumA); 
    else
    { 
        dfs(n, m, stepNumA); 
        dfs(n, m, stepNumB); 
    } 
} 

// Method displays all the stepping 
// numbers in range [n, m] 
void displaySteppingNumbers(int n, int m) 
{ 
    // For every single digit Number 'i' 
    // find all the Stepping Numbers 
    // starting with i 
    for (int i = 0 ; i <= 9 ; i++) 
        dfs(n, m, i); 
} 

//Driver program to test above function 
int main() 
{ 
    int n = 0, m = 21; 

    // Display Stepping Numbers in 
    // the range [n,m] 
    displaySteppingNumbers(n,m); 
    return 0; 
} 

```

## Java

```java

// A Java program to find all the Stepping Numbers 
// in range [n, m] using DFS Approach 
import java.util.*; 

class Main 
{ 
    // Method display's all the stepping numbers 
    // in range [n, m] 
    public static void dfs(int n,int m,int stepNum) 
    { 
        // If Stepping Number is in the 
        // range [n,m] then display 
        if (stepNum <= m && stepNum >= n) 
            System.out.print(stepNum + " "); 

        // If Stepping Number is 0 or greater 
        // than m then return 
        if (stepNum == 0 || stepNum > m) 
            return ; 

        // Get the last digit of the currently 
        // visited Stepping Number 
        int lastDigit = stepNum % 10; 

        // There can be 2 cases either digit 
        // to be appended is lastDigit + 1 or 
        // lastDigit - 1 
        int stepNumA = stepNum*10 + (lastDigit-1); 
        int stepNumB = stepNum*10 + (lastDigit+1); 

        // If lastDigit is 0 then only possible 
        // digit after 0 can be 1 for a Stepping 
        // Number 
        if (lastDigit == 0) 
            dfs(n, m, stepNumB); 

        // If lastDigit is 9 then only possible 
        // digit after 9 can be 8 for a Stepping 
        // Number 
        else if(lastDigit == 9) 
            dfs(n, m, stepNumA); 
        else
        { 
            dfs(n, m, stepNumA); 
            dfs(n, m, stepNumB); 
        } 
    } 

    // Prints all stepping numbers in range [n, m] 
    // using DFS. 
    public static void displaySteppingNumbers(int n, int m) 
    { 
        // For every single digit Number 'i' 
        // find all the Stepping Numbers 
        // starting with i 
        for (int i = 0 ; i <= 9 ; i++) 
            dfs(n, m, i); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int n = 0, m = 21; 

        // Display Stepping Numbers in 
        // the range [n,m] 
        displaySteppingNumbers(n,m); 
    } 
} 

```

输出：

```
0 1 10 12 2 21 3 4 5 6 7 8 9 

```

本文由 **Chirag Agarwal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

