# 用于数组旋转的块交换算法的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序换块-交换-算法换数组-旋转/](https://www.geeksforgeeks.org/javascript-program-for-block-swap-algorithm-for-array-rotation/)

编写一个函数 rotate(ar[]，d，n)，将大小为 n 的 arr[]旋转 d 个元素。

![Array](img/ba17844d7fa31a1b00169a41fc3bc3d3.png)

将上面的数组旋转 2 将构成数组

![ArrayRotation1](img/a0ca29059e52fd48e525698f91766984.png)

**算法:**

```
Initialize A = arr[0..d-1] and B = arr[d..n-1]
1) Do following until size of A is equal to size of B

  a)  If A is shorter, divide B into Bl and Br such that Br is of same 
       length as A. Swap A and Br to change ABlBr into BrBlA. Now A
       is at its final place, so recur on pieces of B.  

   b)  If A is longer, divide A into Al and Ar such that Al is of same 
       length as B Swap Al and B to change AlArB into BArAl. Now B
       is at its final place, so recur on pieces of A.

2)  Finally when A and B are of equal size, block swap them.
```

**递归实现:**

## java 描述语言

```
<script>

let leftRotate = (arr, d, n) =>{ 
    /* Return If number of elements to be rotated  
    is zero or equal to array size */
    if(d == 0 || d == n) 
        return; 

    /*If number of elements to be rotated 
    is exactly half of array size */
    if(n - d == d) { 
        arr = swap(arr, 0, n - d, d); 
        return; 
    } 

    /* If A is shorter*/        
    if(d < n - d) { 
        arr = swap(arr, 0, n - d, d); 
        leftRotate(arr, d, n - d);     
    } 
    else{             
    /* If B is shorter*/  
        arr = swap(arr, 0, d, n - d); 
        /*This is tricky*/
        leftRotate(arr + n - d, 2 * d - n, d); 
    } 
} 

/*UTILITY FUNCTIONS*/
/* function to print an array */
let printArray = (arr, size) =>{ 
    ans = ''
    for(let i = 0; i < size; i++) 
        ans += arr[i]+" ";
    document.write(ans)
} 

/*This function swaps d elements 
starting at index fi 
with d elements starting at index si */
let swap = (arr, fi, si, d) =>{  
    for(let i = 0; i < d; i++) { 
        let temp = arr[fi + i]; 
        arr[fi + i] = arr[si + i]; 
        arr[si + i] = temp; 
    } 
    return arr
} 

// Driver Code
arr = [1, 2, 3, 4, 5, 6, 7]; 
leftRotate(arr, 2, 7); 
printArray(arr, 7); 

</script>
```

**输出:**

```
3 5 4 6 7 1 2
```

**迭代实现:**
这里是同样算法的迭代实现。这里使用了相同的实用函数 swap()。

## java 描述语言

```
<script>
// JavaScript code for above implementation
function leftRotate(arr, d, n)
{
    if(d == 0 || d == n)
        return; 
    let i = d;
    let j = n - d;
    while (i != j)
    {
        if(i < j) 
        {

        // A is shorter
            arr = swap(arr, d - i, d + j - i, i);
            j -= i;
        }
        else{ // B is shorter
            arr = swap(arr, d - i, d, j);
            i -= j;
        }
    }
    arr = swap(arr, d - i, d, i);

    // This code is contributed by rohitsingh04052.
}
</script>
```

**时间复杂度:** O(n)
其他阵轮换法请看以下帖子:
[https://www.geeksforgeeks.org/array-rotation/](https://www.geeksforgeeks.org/array-rotation/)
[https://www . geeksforgeeks . org/程序换阵-轮换-续-反转-算法/](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)

**参考文献:**
[【http://www.cs.bell-labs.com/cm/cs/pearls/s02b.pdf】](http://www.cs.bell-labs.com/cm/cs/pearls/s02b.pdf)
如发现以上程序/算法有任何 bug 或想分享任何关于区块交换算法的补充信息，请写评论。

更多详情请参考[数组旋转的块交换算法](https://www.geeksforgeeks.org/block-swap-algorithm-for-array-rotation/)的完整文章！