# 递归练习题|第 1 集

> 原文:[https://www . geesforgeks . org/practice-questions-for-recursion/](https://www.geeksforgeeks.org/practice-questions-for-recursion/)

解释以下功能的功能。

**问题 1**

## C++

```
int fun1(int x, int y)
{
    if (x == 0)
        return y;
    else
        return fun1(x - 1, x + y);
}
```

## C

```
int fun1(int x, int y)
{
    if (x == 0)
        return y;
    else
        return fun1(x - 1, x + y);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static int fun1(int x, int y)
{
    if (x == 0)
        return y;
    else
        return fun1(x - 1, x + y);
}
```

## 蟒蛇 3

```
def fun1(x, y) :

    if (x == 0) :
        return y
    else :
        return fun1(x - 1, x + y)

# This code is contributed by divyesh072019
```

## C#

```
static int fun1(int x, int y)
{
    if (x == 0)
        return y;
    else
        return fun1(x - 1, x + y);
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

function fun1(x, y)
{
     if (x == 0)
        return y
    else
        return fun1(x - 1, x + y)
}

// This code is contributed by gottumukkalabobby

</script>
```

**回答:**fun()函数计算并返回((1 + 2 … + x-1 + x) +y)，为 x(x+1)/2 + y，例如 x 为 5，y 为 2，那么 fun 应该返回 15 + 2 = 17。

**问题 2**

## C++

```
// minimum index finder

int minIndex(int arr[], int s, int e)
{
    int sml = INT32_MAX;
    int mindex;
    for (int i = s; i < e; i++) {
        if (sml > arr[i]) {
            sml = arr[i];
            mindex = i;
        }
    }
    return mindex;
}

void fun2(int arr[], int start_index, int end_index)
{
    if (start_index >= end_index)
        return;
    int min_index;
    int temp;

    // minIndex() returns index of minimum value in
    // array arr[start_index...end_index]
    min_index = minIndex(arr, start_index, end_index);

    // swap the element at start_index and min_index
    swap(arr[start_index], arr[min_index]);

    fun2(arr, start_index + 1, end_index);
}

// This code is contributed by nishant_0073
```

## C

```
// minimum index finder

int minIndex(int arr[], int s, int e)
{
    int sml = INT32_MAX;
    int mindex;
    for (int i = s; i < e; i++) {
        if (sml > arr[i]) {
            sml = arr[i];
            mindex = i;
        }
    }
    return mindex;
}

void fun2(int arr[], int start_index, int end_index)
{
    if (start_index >= end_index)
        return;
    int min_index;
    int temp;

    // minIndex() returns index of minimum value in
    // array arr[start_index...end_index]
    min_index = minIndex(arr, start_index, end_index);

    temp = arr[start_index];
    arr[start_index] = arr[min_index];
    arr[min_index] = temp;

    fun2(arr, start_index + 1, end_index);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// minimum index finder
static int minIndex(int arr[], int s, int e)
{
    int sml = Integer.MAX_VALUE;
    int mindex = ;
    for (int i = s; i < e; i++) {
        if (sml > arr[i]) {
            sml = arr[i];
            mindex = i;
        }
    }
    return mindex;
}

static void fun2(int arr[], int start_index, int end_index)
{
    if (start_index >= end_index)
        return;
    int min_index;
    int temp;

    // minIndex() returns index of minimum value in
    //   array arr[start_index...end_index]
    min_index = minIndex(arr, start_index, end_index);

    temp = arr[start_index];
    arr[start_index] = arr[min_index];
    arr[min_index] = temp;

    fun2(arr, start_index + 1, end_index);
}

// This code is contributed by nishant_0073
```

## 蟒蛇 3

```
# Minimum index finder
def minIndex(arr, s, e):

    sml = sys.maxsize
    mindex = 0

    for i in range(s, e):
        if (sml > arr[i]):
            sml = arr[i]
            mindex = i

    return mindex

def fun2(arr, start_index, end_index):

    if (start_index >= end_index):
        return

    # minIndex() returns index of minimum value in
    # array arr[start_index...end_index]
    min_index = minIndex(arr, start_index, end_index)
    arr[start_index], arr[min_index] = arr[min_index], arr[start_index]
    fun2(arr, start_index + 1, end_index)

# This code is contributed by rag2127
```

## C#

```
// minimum index finder
static int minIndex(int[] arr, int s, int e)
{
    int sml = Int32.MaxValue;
    int mindex;
    for(int i = s; i < e; i++)
    {
        if(sml > arr[i])
        {
            sml = arr[i];
            mindex = i;
        }
    }
    return mindex;  
}
static void fun2(int[] arr, int start_index, int end_index)   
{
    if(start_index >= end_index)
    {
        return;
    }
    int min_index;
    int temp;

    // minIndex() returns index of minimum value in
    //   array arr[start_index...end_index]
    min_index = minIndex(arr, start_index, end_index);
    temp = arr[start_index];
    arr[start_index] = arr[min_index];
    arr[min_index] = temp;

    fun2(arr, start_index + 1, end_index);
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
//Javascript Implementation
// minimum index finder

function minIndex(arr, s, e)
{
    var sml = Number.MAX_SAFE_INTEGER;
    var mindex;
    for (int i = s; i < e; i++) {
        if (sml > arr[i]) {
            sml = arr[i];
            mindex = i;
        }
    }
    return mindex;
}

function fun2(arr, start_index, end_index)
{
    if (start_index >= end_index)
        return;
    var min_index;
    var temp;

    // minIndex() returns index of minimum value in
    // array arr[start_index...end_index]
    min_index = minIndex(arr, start_index, end_index);

    // swap the element at start_index and min_index
    temp = arr[start_index];
    arr[start_index] = arr[min_index];
    arr[min_index] = temp;

    fun2(arr, start_index + 1, end_index);
}
// This code is contributed by shubhamsingh10
</script>
```

**答案:【fun2()函数是 Selection Sort 的递归实现。**

如果您发现任何答案/代码不正确，或者您想分享关于上述主题的更多信息，请写评论。