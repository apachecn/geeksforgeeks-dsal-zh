# 通过除以一个数字的因子或者从数组中删除第一个出现的数字来将一个数字转换成另一个数字

> 原文:[https://www . geeksforgeeks . org/将一个数字转换为另一个数字除以其因子或从数组中移除第一个出现的数字/](https://www.geeksforgeeks.org/convert-a-number-to-another-by-dividing-by-its-factor-or-removing-first-occurrence-of-a-digit-from-an-array/)

给定两个正整数 **A** 、 **B** 和一个仅由数字**【0-9】**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**D【】**，任务是检查是否有可能通过重复除以数组**D【】**中存在的任何因子或通过删除数组中存在的任何数字的第一次出现来将 **A** 减少到 **B**

**示例:**

> **输入:** A = 5643，B = 81，D[] = {3，8，1}
> **输出:**是
> **说明:**
> **运算 1:** 将 A (= 5643)除以 3，则 A 的值变为 1881。
> **操作 2:** 从 A(= 1881)中去掉第一个出现的 8，那么 A 的值就变成了 181。
> **操作 3:** 从 A(= 181)中去掉第一个出现的 1，那么 A 的值变成 81。
> 
> **输入:** A = 82，B = 2，D[] = {8，2 }
> T3】输出:是

**方法:**通过使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)对值 **A** 执行所有可能的操作，并检查在任何步骤中 **A** 的值是否修改为 **B** ，可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，说 **Q** ，初始推 **A** 给它。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) ，说 **M** 存储队列中存在的元素 **Q** 并初始化一个变量 **ans** 为**“否”**存储需要的结果。
*   迭代至 [**Q** 不为空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)，执行以下步骤:
    *   将**前面的[Q](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)**T3 存储在一个变量中，**顶**。
    *   如果**顶部**的值等于 **B** ，则将 **ans** 的值更新为**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **D[]** ，对于每个元素， **D[i]** 检查两个条件:
        *   如果 **D[i]** 是 **top** 的因子，则在队列 **Q** 中将 **top** 除以 **D[i]** 得到的值商推送到 **M** 中标记为已访问。
        *   如果号码**顶部**中出现**D【I】**，则删除其第一次出现的号码，并推送队列 **Q** 中获得的新号码，并在 **M** 中将其标记为已访问。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a digit x is
// present in the number N or not
int isPresent(int n, int x)
{
    // Convert N to string
    string num = to_string(n);

    // Traverse the string num
    for (int i = 0; i < num.size();
         i++) {

        // Return first occurrence
        // of the digit x
        if ((num[i] - '0') == x)
            return i;
    }
    return -1;
}

// Function to remove the character
// at a given index from the number
int removeDigit(int n, int index)
{
    // Convert N to string
    string num = to_string(n);

    // Store the resultant string
    string ans = "";

    // Traverse the string num
    for (int i = 0;
         i < num.size(); i++) {
        if (i != index)
            ans += num[i];
    }

    // If the number becomes empty
    // after deletion, then return -1
    if (ans == "" || (ans.size() == 1
                      && ans[0] == '0'))
        return -1;

    // Return the number
    int x = stoi(ans);
    return x;
}

// Function to check if A can be
// reduced to B by performing the
// operations any number of times
bool reduceNtoX(int a, int b,
                int d[], int n)
{
    // Create a queue
    queue<int> q;

    // Push A into the queue
    q.push(a);

    // Hashmap to check if the element
    // is present in the Queue or not
    unordered_map<int, bool> visited;

    // Set A as visited
    visited[a] = true;

    // Iterate while the queue is not empty
    while (!q.empty()) {

        // Store the front value of the
        // queue and pop it from it
        int top = q.front();
        q.pop();

        if (top < 0)
            continue;

        // If top is equal to B,
        // then return true
        if (top == b)
            return true;

        // Traverse the array, D[]
        for (int i = 0; i < n; i++) {

            // Divide top by D[i] if
            // it is possible and
            // push the result in q
            if (d[i] != 0 && top % d[i] == 0
                && !visited[top / d[i]]) {

                q.push(top / d[i]);
                visited[top / d[i]] = true;
            }

            // If D[i] is present at the top
            int index = isPresent(top, d[i]);
            if (index != -1) {

                // Remove the first occurrence
                // of D[i] from the top and
                // store the new number
                int newElement
                    = removeDigit(top, index);

                // Push newElement into the queue q
                if (newElement != -1
                    && (!visited[newElement])) {
                    q.push(newElement);
                    visited[newElement] = true;
                }
            }
        }
    }

    // Return false if A can
    // not be reduced to B
    return false;
}

// Driver Code
int main()
{

    int A = 5643, B = 81;
    int D[] = { 3, 8, 1 };
    int N = sizeof(D) / sizeof(D[0]);

    if (reduceNtoX(A, B, D, N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to check if a digit x is
// present in the number N or not
static int isPresent(int n, int x)
{

    // Convert N to string
    String num = String.valueOf(n);

    // Traverse the string num
    for (int i = 0; i < num.length();
         i++) {

        // Return first occurrence
        // of the digit x
        if ((num.charAt(i) - '0') == x)
            return i;
    }
    return -1;
}

// Function to remove the character
// at a given index from the number
static int removeDigit(int n, int index)
{

    // Convert N to string
    String num = String.valueOf(n);

    // Store the resultant string
    String ans = "";

    // Traverse the string num
    for (int i = 0;
         i < num.length(); i++)
    {
        if (i != index)
            ans += num.charAt(i);
    }

    // If the number becomes empty
    // after deletion, then return -1
    if (ans == "" || (ans.length() == 1
                      && ans.charAt(0) == '0'))
        return -1;

    // Return the number
    int x = Integer.valueOf(ans);
    return x;
}

// Function to check if A can be
// reduced to B by performing the
// operations any number of times
static boolean reduceNtoX(int a, int b,
                int d[], int n)
{

    // Create a queue
    Queue<Integer> q=new LinkedList<>();

    // Push A into the queue
    q.add(a);

    // Hashmap to check if the element
    // is present in the Queue or not
    Map<Integer, Boolean> visited= new HashMap<>();

    // Set A as visited
    visited.put(a,true);

    // Iterate while the queue is not empty
    while (!q.isEmpty()) {

        // Store the front value of the
        // queue and pop it from it
        int top = q.peek();
        q.poll();

        if (top < 0)
            continue;

        // If top is equal to B,
        // then return true
        if (top == b)
            return true;

        // Traverse the array, D[]
        for (int i = 0; i < n; i++) {

            // Divide top by D[i] if
            // it is possible and
            // push the result in q
            if (d[i] != 0 && top % d[i] == 0
                && !visited.getOrDefault(top / d[i], false)) {

                q.add(top / d[i]);
                visited.put(top / d[i], true);
            }

            // If D[i] is present at the top
            int index = isPresent(top, d[i]);
            if (index != -1) {

                // Remove the first occurrence
                // of D[i] from the top and
                // store the new number
                int newElement
                    = removeDigit(top, index);

                // Push newElement into the queue q
                if (newElement != -1
                    && (!visited.getOrDefault(newElement,false))) {
                    q.add(newElement);
                    visited.put(newElement, true);
                }
            }
        }
    }

    // Return false if A can
    // not be reduced to B
    return false;
}

  // Driver code
public static void main (String[] args)
{

      // Given inputs
    int A = 5643, B = 81;
    int D[] = { 3, 8, 1 };
    int N = D.length;

    if (reduceNtoX(A, B, D, N))
        System.out.println("Yes");
    else
        System.out.println("No");

    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to check if a digit x is
# present in the number N or not
def isPresent(n, x):

    # Convert N to string
    num = str(n)

    # Traverse the num
    for i in range(len(num)):

        # Return first occurrence
        # of the digit x
        if ((ord(num[i]) - ord('0')) == x):
            return i

    return -1

# Function to remove the character
# at a given index from the number
def removeDigit(n, index):

    # Convert N to string
    num = str(n)

    # Store the resultant string
    ans = ""

    # Traverse the num
    for i in range(len(num)):
        if (i != index):
            ans += num[i]

    # If the number becomes empty
    # after deletion, then return -1
    if (ans == "" or (len(ans) == 1 and
        ans[0] == '0')):
        return -1

    # Return the number
    x = int(ans)
    return x

# Function to check if A can be
# reduced to B by performing the
# operations any number of times
def reduceNtoX(a, b, d, n):

    # Create a queue
    q = deque()

    # Push A into the queue
    q.append(a)

    # Hashmap to check if the element
    # is present in the Queue or not
    visited = {}

    # Set A as visited
    visited[a] = True

    # Iterate while the queue is not empty
    while (len(q) > 0):

        # Store the front value of the
        # queue and pop it from it
        top = q.popleft()

        if (top < 0):
            continue

        # If top is equal to B,
        # then return true
        if (top == b):
            return True

        # Traverse the array, D[]
        for i in range(n):

            # Divide top by D[i] if
            # it is possible and
            # push the result in q
            if (d[i] != 0 and top % d[i] == 0 and
               (top // d[i] not in visited)):
                q.append(top // d[i])
                 visited[top // d[i]] = True

            # If D[i] is present at the top
            index = isPresent(top, d[i])

            if (index != -1):

                # Remove the first occurrence
                # of D[i] from the top and
                # store the new number
                newElement = removeDigit(top, index)

                # Push newElement into the queue q
                if (newElement != -1 and
                   (newElement not in  visited)):
                    q.append(newElement)
                    visited[newElement] = True

    # Return false if A can
    # not be reduced to B
    return False

# Driver Code
if __name__ == '__main__':

    A, B = 5643, 81
    D = [ 3, 8, 1 ]
    N = len(D)

    if (reduceNtoX(A, B, D, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to check if a digit x is
// present in the number N or not
static int isPresent(int n, int x)
{
    // Convert N to string
    string num = n.ToString();

    // Traverse the string num
    for (int i = 0; i < num.Length;
         i++) {

        // Return first occurrence
        // of the digit x
       if (((int)num[i] - 97) == x)
            return i;
    }
    return -1;
}

// Function to remove the character
// at a given index from the number
static int removeDigit(int n, int index)
{
    // Convert N to string
    string num = n.ToString();

    // Store the resultant string
    string ans = "";

    // Traverse the string num
    for (int i = 0;
         i < num.Length; i++) {
        if (i != index)
            ans += num[i];
    }

    // If the number becomes empty
    // after deletion, then return -1
    if (ans == "" || (ans.Length == 1
                      && ans[0] == '0'))
        return -1;

    // Return the number
    int x =  Int32.Parse(ans);;
    return x;
}

// Function to check if A can be
// reduced to B by performing the
// operations any number of times
static bool reduceNtoX(int a, int b,
                int []d, int n)
{
    // Create a queue
    Queue<int> q = new Queue<int>();

    // Push A into the queue
    q.Enqueue(a);

    // Hashmap to check if the element
    // is present in the Queue or not
    Dictionary<int,bool> visited = new Dictionary<int,bool>();

    // Set A as visited
    visited[a] = true;

    // Iterate while the queue is not empty
    while (q.Count>0) {

        // Store the front value of the
        // queue and pop it from it
        int top = q.Peek();
        q.Dequeue();

        if (top < 0)
            continue;

        // If top is equal to B,
        // then return true
        if (top == b)
            return true;

        // Traverse the array, D[]
        for (int i = 0; i < n; i++) {

            // Divide top by D[i] if
            // it is possible and
            // push the result in q
            if (d[i] != 0 && top % d[i] == 0 &&
                visited.ContainsKey(top / d[i]) && visited[top / d[i]]==false) {

                q.Enqueue(top / d[i]);
                   visited[top / d[i]] = true;

            }

            // If D[i] is present at the top
            int index = isPresent(top, d[i]);
            if (index != -1) {

                // Remove the first occurrence
                // of D[i] from the top and
                // store the new number
                int newElement = removeDigit(top, index);

                // Push newElement into the queue q
                if (newElement != -1 && (visited.ContainsKey(newElement) && visited[newElement]==false)) {
                    q.Enqueue(newElement);

                        visited[newElement] = true;
                }
            }
        }
    }

    // Return false if A can
    // not be reduced to B
    return true;
}

// Driver Code
public static void Main()
{

    int A = 5643, B = 81;
    int []D = { 3, 8, 1 };
    int N = D.Length;

    if (reduceNtoX(A, B, D, N))
        Console.Write("Yes");
    else
        Console.Write("No");

}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if a digit x is
// present in the number N or not
function isPresent(n,x)
{
// Convert N to string
    let num = (n).toString();

    // Traverse the string num
    for (let i = 0; i < num.length;
         i++) {

        // Return first occurrence
        // of the digit x
        if ((num[i].charCodeAt(0) - '0'.charCodeAt(0)) == x)
            return i;
    }
    return -1;
}

// Function to remove the character
// at a given index from the number
function removeDigit(n,index)
{
    // Convert N to string
    let num = (n).toString();

    // Store the resultant string
    let ans = "";

    // Traverse the string num
    for (let i = 0;
         i < num.length; i++)
    {
        if (i != index)
            ans += num[i];
    }

    // If the number becomes empty
    // after deletion, then return -1
    if (ans == "" || (ans.length == 1
                      && ans[0] == '0'))
        return -1;

    // Return the number
    let x = parseInt(ans);
    return x;
}

// Function to check if A can be
// reduced to B by performing the
// operations any number of times
function reduceNtoX(a,b,d,n)
{
    // Create a queue
    let q=[];

    // Push A into the queue
    q.push(a);

    // Hashmap to check if the element
    // is present in the Queue or not
    let visited= new Map();

    // Set A as visited
    visited.set(a,true);

    // Iterate while the queue is not empty
    while (q.length!=0) {

        // Store the front value of the
        // queue and pop it from it
        let top = q.shift();

        if (top < 0)
            continue;

        // If top is equal to B,
        // then return true
        if (top == b)
            return true;

        // Traverse the array, D[]
        for (let i = 0; i < n; i++) {

            // Divide top by D[i] if
            // it is possible and
            // push the result in q

            if(!visited.has(top / d[i]))
                visited.set(top / d[i],false);

            if (d[i] != 0 && top % d[i] == 0
                && !visited.get(top / d[i])) {

                q.push(top / d[i]);
                visited.set(top / d[i], true);
            }

            // If D[i] is present at the top
            let index = isPresent(top, d[i]);
            if (index != -1) {

                // Remove the first occurrence
                // of D[i] from the top and
                // store the new number
                let newElement
                    = removeDigit(top, index);

                if(!visited.has(newElement))
                    visited.set(newElement,false);

                // Push newElement into the queue q
                if (newElement != -1
                    && (!visited.get(newElement))) {
                    q.push(newElement);
                    visited.set(newElement, true);
                }
            }
        }
    }

    // Return false if A can
    // not be reduced to B
    return false;
}

// Driver code
// Given inputs
let A = 5643, B = 81;
let D = [ 3, 8, 1 ];
let N = D.length;

if (reduceNtoX(A, B, D, N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*