# 在不使用额外空间的情况下，以{a1，b1，a2，b2，a3，b3，…，an，bn}格式洗牌 2n 个整数

> 原文:[https://www . geesforgeks . org/shuffle-2n-integers-format-a1-B1-a2-B2-a3-B3-bn-不使用-extra-space/](https://www.geeksforgeeks.org/shuffle-2n-integers-format-a1-b1-a2-b2-a3-b3-bn-without-using-extra-space/)

给定以下格式的 2n 个**元素的数组{ a1，a2，a3，a4，…..，an，b1，b2，b3，b4，…，bn }。任务是在不使用额外空间的情况下将数组洗牌到{a1，b1，a2，b2，a3，b3，…，an，bn }。**

****示例:****

```
Input : arr[] = { 1, 2, 9, 15 }
Output : 1 9 2 15

Input :  arr[] = { 1, 2, 3, 4, 5, 6 }
Output : 1 4 2 5 3 6
```

****方法 1:蛮力**
蛮力解决方案包括两个嵌套循环，将数组后半部分的元素向左旋转。第一个循环运行 n 次，以覆盖数组后半部分的所有元素。第二个循环向左旋转元素。请注意，第二个循环中的开始索引取决于我们旋转的元素，结束索引取决于我们需要向左移动多少个位置。**

**下面是这种方法的实现:**

## **C++**

```
// C++ Naive program to shuffle an array of size 2n
#include <bits/stdc++.h>
using namespace std;

// function to shuffle an array of size 2n
void shuffleArray(int a[], int n)
{
    // Rotate the element to the left
    for (int i = 0, q = 1, k = n; i < n; i++, k++, q++)
        for (int j = k; j > i + q; j--)
            swap(a[j - 1], a[j]);
}

// Driven Program
int main()
{
    int a[] = { 1, 3, 5, 7, 2, 4, 6, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    shuffleArray(a, n / 2);

    for (int i = 0; i < n; i++)
        cout << a[i] << " ";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Naive program to shuffle an array of size 2n

import java.util.Arrays;

public class GFG {
    // method to shuffle an array of size 2n
    static void shuffleArray(int a[], int n)
    {
        // Rotate the element to the left
        for (int i = 0, q = 1, k = n; i < n; i++, k++, q++)
            for (int j = k; j > i + q; j--) {
                // swap a[j-1], a[j]
                int temp = a[j - 1];
                a[j - 1] = a[j];
                a[j] = temp;
            }
    }

    // Driver Method
    public static void main(String[] args)
    {
        int a[] = { 1, 3, 5, 7, 2, 4, 6, 8 };

        shuffleArray(a, a.length / 2);

        System.out.println(Arrays.toString(a));
    }
}
```

## **蟒蛇 3**

```
# Python3 Naive program to
# shuffle an array of size 2n

# Function to shuffle an array of size 2n
def shuffleArray(a, n):

    # Rotate the element to the left
    i, q, k = 0, 1, n
    while(i < n):    
        j = k
        while(j > i + q):
            a[j - 1], a[j] = a[j], a[j - 1]
            j -= 1
        i += 1
        k += 1
        q += 1

# Driver Code
a = [1, 3, 5, 7, 2, 4, 6, 8]
n = len(a)
shuffleArray(a, int(n / 2))
for i in range(0, n):
    print(a[i], end = " ")

# This code is contributed by Smitha Dinesh Semwal.
```

## **C#**

```
// C# Naive program to shuffle an
// array of size 2n
using System;

class GFG {
    // method to shuffle an array of size 2n
    static void shuffleArray(int[] a, int n)
    {
        // Rotate the element to the left
        for (int i = 0, q = 1, k = n;
             i < n; i++, k++, q++)
            for (int j = k; j > i + q; j--) {
                // swap a[j-1], a[j]
                int temp = a[j - 1];
                a[j - 1] = a[j];
                a[j] = temp;
            }
    }

    // Driver Code
    public static void Main()
    {
        int[] a = { 1, 3, 5, 7, 2, 4, 6, 8 };

        shuffleArray(a, a.Length / 2);
        for (int i = 0; i < a.Length; i++)
            Console.Write(a[i] + " ");
    }
}

// This code is contributed
// by ChitraNayal
```

## **java 描述语言**

```
<script>
// Javascript Naive program to shuffle an array of size 2n

    // method to shuffle an array of size 2n
    function shuffleArray(a,n)
    {
        // Rotate the element to the left
        for (let i = 0, q = 1, k = n; i < n; i++, k++, q++)
            for (let j = k; j > i + q; j--) {
                // swap a[j-1], a[j]
                let temp = a[j - 1];
                a[j - 1] = a[j];
                a[j] = temp;
            }
    }

    // Driver Method
    let a=[ 1, 3, 5, 7, 2, 4, 6, 8];
    shuffleArray(a, a.length / 2);

    document.write(a.join(" "));

    //This code is contributed by avanitrachhadiya2155

</script>
```

****输出:****

```
1 2 3 4 5 6 7 8 
```

****时间复杂度:** O(n <sup>2</sup>**

****方法二:(分而治之)**
思路就是用分而治之的手法。将给定的数组分成两半(比如 arr1[]和 arr2[])，并用 arr2[]的前半个元素替换 arr1[]的后半个元素。递归地对 arr1 和 arr2 执行此操作。**

**让我们借助一个例子来解释一下。**

1.  **假设数组是 a1、a2、a3、a4、b1、b2、b3、b4**
2.  **将阵列分成两半:a1、a2、a3、a4 : b1、b2、b3、b4**
3.  **围绕中心交换元素:用 b1、b2 对应交换 a3、a4。
    你得到:a1、a2、b1、b2、a3、a4、b3、b4**
4.  **递归地将 a1、a2、b1、b2 拆分成 a1、a2 : b1、b2
    再将 a3、a4、b3、b4 拆分成 a3、a4 : b3、b4。**
5.  **为我们得到的每个子阵列交换中心周围的元素:
    a1、b1、a2、b2 和 a3、b3、a4、b4。**

**注:本解决方案只处理 n = 2 <sup>i</sup> 的情况，其中 i = 0，1，2，…等。**

**下面是这种方法的实现:**

## **C++**

```
// C++ Effective  program to shuffle an array of size 2n

#include <bits/stdc++.h>
using namespace std;

// function to shuffle an array of size 2n
void shufleArray(int a[], int f, int l)
{
    if (f > l) {
        return;
    }

    // If only 2 element, return
    if (l - f == 1)
        return;

    // finding mid to divide the array
    int mid = (f + l) / 2;

    // using temp for swapping first half of second array
    int temp = mid + 1;

    // mmid is use for swapping second half for first array
    int mmid = (f + mid) / 2;

    // Swapping the element
    for (int i = mmid + 1; i <= mid; i++)
        swap(a[i], a[temp++]);

    // Recursively doing for first half and second half
    shufleArray(a, f, mid);
    shufleArray(a, mid + 1, l);
}

// Driven Program
int main()
{
    int a[] = { 1, 3, 5, 7, 2, 4, 6, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    shufleArray(a, 0, n - 1);

    for (int i = 0; i < n; i++)
        cout << a[i] << " ";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Effective  program to shuffle an array of size 2n

import java.util.Arrays;

public class GFG {
    // method to shuffle an array of size 2n
    static void shufleArray(int a[], int f, int l)
    {
        if (f > l)
            return;

        // If only 2 element, return
        if (l - f == 1)
            return;

        // finding mid to divide the array
        int mid = (f + l) / 2;

        // using temp for swapping first half of second array
        int temp = mid + 1;

        // mmid is use for swapping second half for first array
        int mmid = (f + mid) / 2;

        // Swapping the element
        for (int i = mmid + 1; i <= mid; i++) {
            // swap a[i], a[temp++]
            int temp1 = a[i];
            a[i] = a[temp];
            a[temp++] = temp1;
        }

        // Recursively doing for first half and second half
        shufleArray(a, f, mid);
        shufleArray(a, mid + 1, l);
    }

    // Driver Method
    public static void main(String[] args)
    {
        int a[] = { 1, 3, 5, 7, 2, 4, 6, 8 };

        shufleArray(a, 0, a.length - 1);

        System.out.println(Arrays.toString(a));
    }
}
```

## **蟒蛇 3**

```
# Python3 effective program to
# shuffle an array of size 2n

# Function to shuffle an array of size 2n
def shufleArray(a, f, l):

    if (f > l):
        return

    # If only 2 element, return
    if (l - f == 1):
        return

    # Finding mid to divide the array
    mid = int((f + l) / 2)

    # Using temp for swapping first
    # half of the second array
    temp = mid + 1

    # Mid is use for swapping second
    # half for first array
    mmid = int((f + mid) / 2)

    # Swapping the element
    for i in range(mmid + 1, mid + 1):
        (a[i], a[temp]) = (a[temp], a[i])
        temp += 1

    # Recursively doing for first
    # half and second half
    shufleArray(a, f, mid)
    shufleArray(a, mid + 1, l)

# Driver Code
a = [1, 3, 5, 7, 2, 4, 6, 8]
n = len(a)
shufleArray(a, 0, n - 1)

for i in range(0, n):
    print(a[i], end = " ")

# This code is contributed by Smitha Dinesh Semwal
```

## **C#**

```
// C# program program to merge two
// sorted arrays with O(1) extra space.
using System;

// method to shuffle an array of size 2n

public class GFG {
    // method to shuffle an array of size 2n
    static void shufleArray(int[] a, int f, int l)
    {
        if (f > l)
            return;

        // If only 2 element, return
        if (l - f == 1)
            return;

        // finding mid to divide the array
        int mid = (f + l) / 2;

        // using temp for swapping first half of second array
        int temp = mid + 1;

        // mmid is use for swapping second half for first array
        int mmid = (f + mid) / 2;

        // Swapping the element
        for (int i = mmid + 1; i <= mid; i++) {
            // swap a[i], a[temp++]
            int temp1 = a[i];
            a[i] = a[temp];
            a[temp++] = temp1;
        }

        // Recursively doing for first half and second half
        shufleArray(a, f, mid);
        shufleArray(a, mid + 1, l);
    }

    // Driver Method
    public static void Main()
    {
        int[] a = { 1, 3, 5, 7, 2, 4, 6, 8 };

        shufleArray(a, 0, a.Length - 1);
        for (int i = 0; i < a.Length; i++)
            Console.Write(a[i] + " ");
    }
}

/*This code is contributed by 29AjayKumar*/
```

## **java 描述语言**

```
<script>

// Javascript Effective program to
// shuffle an array of size 2n

// method to shuffle an array of size 2n
function shufleArray(a, f, l)
{
    if (f > l)
        return;

    // If only 2 element, return
    if (l - f == 1)
        return;

    // Finding mid to divide the array
    let mid = Math.floor((f + l) / 2);

    // Using temp for swapping first
    // half of second array
    let temp = mid + 1;

    // mmid is use for swapping second
    // half for first array
    let mmid = Math.floor((f + mid) / 2);

    // Swapping the element
    for(let i = mmid + 1; i <= mid; i++)
    {

        // Swap a[i], a[temp++]
        let temp1 = a[i];
        a[i] = a[temp];
        a[temp++] = temp1;
    }

    // Recursively doing for first
    // half and second half
    shufleArray(a, f, mid);
    shufleArray(a, mid + 1, l);
}

// Driver Code
let a = [ 1, 3, 5, 7, 2, 4, 6, 8 ];
shufleArray(a, 0, a.length - 1);

document.write(a.join(" "));

// This code is contributed by rag2127

</script>
```

****输出:****

```
1 2 3 4 5 6 7 8 
```

****时间复杂度:** O(n log n)
[**线性时间解**](https://www.geeksforgeeks.org/shuffle-array-a1-b1-a2-b2-a3-b3-bn-without-using-extra-space/)**

**本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**