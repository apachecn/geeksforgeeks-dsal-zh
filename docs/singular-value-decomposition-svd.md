# 奇异值分解

> 原文:[https://www . geesforgeks . org/奇异值分解-svd/](https://www.geeksforgeeks.org/singular-value-decomposition-svd/)

矩阵的奇异值分解是将该矩阵分解成三个矩阵。它有一些有趣的代数性质，传达了关于线性变换的重要几何和理论见解。它在数据科学中也有一些重要的应用。在本文中，我将尝试解释奇异值分解背后的数学直觉及其几何意义。

#### **SVD 背后的数学**

mxn 矩阵 A 的奇异值分解由下式给出:

![A = UWV^{T}](img/2a783c7fb00790b36463a75e23a176ca.png "Rendered by QuickLaTeX.com")

其中:

*   u:*mxn![AA^{T}             ](img/372f5eb3002f6a7c0bbaea503c890eef.png "Rendered by QuickLaTeX.com")的正交特征向量的*矩阵。
*   V <sup>T</sup> :包含 A^{T}A.正交特征向量的 *nxn* 矩阵的转置
*   w:一个 *nxn* 奇异值的对角矩阵，它是![A^{T}A         ](img/8ab9c4bb40119be71065d545a362622d.png "Rendered by QuickLaTeX.com")特征值的平方根。

![](img/307d060d74271d8bb8031c3cd78c4192.png)

#### 例子

*   求矩阵 A 的奇异值分解= ![\begin{bmatrix} 3& 3 & 2 \\ 2&  3& -2 \end{bmatrix}](img/891b16477140d4fad51439098063a5f6.png "Rendered by QuickLaTeX.com")
*   为了计算奇异值分解，首先，我们需要通过寻找 AA^{T}.的特征值来计算奇异值

![A \cdot A^{T} =\begin{bmatrix} 3& 3 & 2 \\ 2&  3& -2 \end{bmatrix} \cdot \begin{bmatrix} 3 & 2 \\ 3 & 3 \\ 2 & -2 \end{bmatrix} = \begin{bmatrix} 17 & 8\\ 8 & 17 \end{bmatrix}](img/75e3a77a025596b36fcc3510b4fc2135.png "Rendered by QuickLaTeX.com")

*   上述矩阵的特征方程为:

![W - \lambda I =0 \\ A A^{T} - \lambda I =0 ](img/b6c354fb479f9720e6d452408effdda0.png "Rendered by QuickLaTeX.com")

![\lambda^{2} - 34 \lambda + 225 =0](img/2d161d81ddffcd3f8e9ab37f4ce8f075.png "Rendered by QuickLaTeX.com")

![= (\lambda-25)(\lambda -9)](img/413dcb0f5dfd75b9cfe15d4894aa1c7b.png "Rendered by QuickLaTeX.com")

所以我们的奇异值是:![\sigma_1 = 5 \, ; \sigma_2 = 3](img/53e01a94b8fc97ee0ecce51a88de8af1.png "Rendered by QuickLaTeX.com")

*   现在我们找到正确的奇异向量，即 A <sup>T</sup> A 的特征向量的正交集合。A <sup>T</sup> A 的特征值是 25，9 和 0，并且由于 A <sup>T</sup> A 是对称的，我们知道特征向量将是正交的。

对于![\lambda =25,](img/18a500a75cac5bc3c4b7031ba58248a5.png "Rendered by QuickLaTeX.com")

![AA^{T} - 25 \cdot I  = \begin{bmatrix} -12 &  12& 2\\ 12 &  -12 & -2\\ 2&  -2 & -17 \end{bmatrix}](img/4b7d289463ee3f2f14429bd0986cb624.png "Rendered by QuickLaTeX.com")

其可以被行缩减为:

![\begin{bmatrix} 1&  -1& 0 \\ 0&  0&  1\\ 0&  0& 0 \end{bmatrix}](img/8e122b586de02ec6d4b3ccc581ff95c3.png "Rendered by QuickLaTeX.com")

方向上的单位向量是:

![v_1 = \begin{bmatrix} \frac{1}{\sqrt{2}}\\ \frac{1}{\sqrt{2}}\\ 0 \end{bmatrix}](img/f96d70e9b3573e4f32ab6eab4a6fd632.png "Rendered by QuickLaTeX.com")

类似地，对于λ= 9，特征向量为:

![v_2 =\begin{bmatrix} \frac{1}{\sqrt{18}}\\ \frac{-1}{\sqrt{18}}\\ \frac{4}{\sqrt{18}}\\ \end{bmatrix}](img/709ebdf0c4080bb6b71eb4b2a23fefa7.png "Rendered by QuickLaTeX.com")

对于第三个特征向量，我们可以利用它垂直于 v1 和 v2 的性质，使得:

![v_1^{T} v_3 =0 \\ v_2^{T} v_3 =0](img/c0c9477de50e7a768fdc4ec42392d802.png "Rendered by QuickLaTeX.com")

求解上述方程以生成第三特征向量

![v_3 = \begin{bmatrix} a\\ b\\ c \end{bmatrix} = \begin{bmatrix} a\\ -a \\ -a/2 \end{bmatrix} = \begin{bmatrix} \frac{2}{3}\\ \frac{-2}{3}\\ \frac{-1}{3} \end{bmatrix}](img/04997a6912684ae8123c86a42e6bfbb0.png "Rendered by QuickLaTeX.com")

现在，我们使用公式 u_i = \frac{1}{\sigma} A v_i 计算 U，这给出了 U = ![\begin{bmatrix} \frac{1}{\sqrt{2}} &\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}}& \frac{-1}{\sqrt{2}} \end{bmatrix}       ](img/4c35c5319241fc65e4c83fbbc4e6ffc6.png "Rendered by QuickLaTeX.com")。因此，我们最终的奇异值分解方程变为:

![A =A = \begin{bmatrix} \frac{1}{\sqrt{2}} &\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}}& \frac{-1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} 5 &  0& 0 \\ 0 &  3& 0 \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}}& \frac{1}{\sqrt{2}} &0 \\ \frac{1}{\sqrt{18}}& \frac{-1}{\sqrt{18}} & \frac{4}{\sqrt{18}}\\ \frac{2}{3}&\frac{-2}{3}  &\frac{1}{3} \end{bmatrix}](img/5a1a3385b472e9b3a4869cc275d46cd3.png "Rendered by QuickLaTeX.com")

### 应用程序

*   **伪逆的计算:**伪逆或 Moore-Penrose 逆是可能不可逆的矩阵逆(如低秩矩阵)的推广。如果矩阵是可逆的，那么它的逆将等于伪逆，但是伪逆对于不可逆的矩阵是存在的。用 A <sup>+</sup> 表示。

假设，我们需要计算矩阵 M 的伪逆:

那么，M 的奇异值分解可以表示为:

![M = U W V^{T}](img/b2824c51128f25dc73225c4a5775f4b4.png "Rendered by QuickLaTeX.com")

将两边乘以 M^{-1}.

![M^{-1} M = M^{-1} U W V^{T}](img/b4f6084b7cf101c17567d596c922637e.png "Rendered by QuickLaTeX.com")

![I= M^{-1} U W V^{T}](img/fba2408a286ab6cdb179041282d7a75f.png "Rendered by QuickLaTeX.com")

将两侧乘以 V:

![V = M^{-1} U W V^{T}V](img/213c29cedde761a82dd00478e29ea28a.png "Rendered by QuickLaTeX.com")

![V = M^{-1} U W](img/6bedbbccb7645ee01b5b9b23944d1401.png "Rendered by QuickLaTeX.com")

乘以 W^{-1}.由于 W 是奇异矩阵，W 的逆![ = diag(a_1, a_2, a_3, ... a_n)^{-1}             ](img/8854973301eda84915370209ebf29d5b.png "Rendered by QuickLaTeX.com")就是![ = diag(1/a_1, 1/a_2, 1/a_3, ... 1/a_n)](img/7b23beca6007f6ef51fd072abd0627a5.png "Rendered by QuickLaTeX.com")

![V W^{-1} =  M^{-1} U W W^{-1}](img/46fe9e4bfe24e92e894b1c9382256202.png "Rendered by QuickLaTeX.com")

![V W^{-1} = M^{-1} U](img/c73f6307513b739ce2ea07265580983a.png "Rendered by QuickLaTeX.com")

乘以![U^T](img/2a73795d8c84d20a039b8e410b2a1af1.png "Rendered by QuickLaTeX.com")

![V W^{-1} U^{T} = M^{-1} U U^{T}](img/d8d81c49eabda913366dcb362fff2daf.png "Rendered by QuickLaTeX.com")

![V W^{-1} U^{T} = M^{-1} = M^{+}](img/8a570d5544f39227a7dc397732957123.png "Rendered by QuickLaTeX.com")

上面的等式给出了伪逆。

*   **求解一组齐次线性方程(Mx =b):** 如果 b=0，计算 SVD，取与奇异值(在 *W* 中)相关联的 V <sup>T</sup> 的任意一列等于 0。

如果![b \neq 0             ](img/81e1b8cc25125f0ff2a6da1f711ab576.png "Rendered by QuickLaTeX.com")、![Mx =b](img/a9c31d36ead41296cab4e3c1a7242e31.png "Rendered by QuickLaTeX.com")

乘以![M^{-1}](img/fbbf183bb45eeff7df3a4593c0c030ec.png "Rendered by QuickLaTeX.com")

![M^{-1} M x = M^{-1} b ](img/359fabad1725fab78621989930ea06be.png "Rendered by QuickLaTeX.com")

![x = M^{-1} b](img/d584f3b2a4ec7acc2b792cb8b07d41c2.png "Rendered by QuickLaTeX.com")

从伪逆，我们知道![M^{-1} = V W^{-1} U^{T}](img/bbb6479b9e234a16dd5e2d609952cc02.png "Rendered by QuickLaTeX.com")

因此，

![x = V W^{-1} U^{T} b](img/a1e6d725ae03072520b0c4436be34c83.png "Rendered by QuickLaTeX.com")

*   **等级、范围和零空间:**
    *   矩阵 M 的秩可以由奇异值分解通过非零奇异值的个数来计算。
    *   矩阵 M 的范围是对应非零奇异值的 U 的左奇异向量。
    *   矩阵 M 的零空间是与零奇异值对应的 V 的右奇异向量。

![M = U W V^{T}](img/b2824c51128f25dc73225c4a5775f4b4.png "Rendered by QuickLaTeX.com")

*   **曲线拟合问题:**奇异值分解可以用来最小化最小二乘误差。它使用伪逆来近似它。
*   除了上述应用，奇异值分解和伪逆也可以用于数字信号处理和图像处理

### 履行

*   在这段代码中，我们将尝试使用 Numpy 和 Scipy 计算奇异值分解。我们将计算奇异值分解，并执行伪逆。最后，我们可以应用奇异值分解对图像进行压缩

## 蟒蛇 3

```
# Imports

import numpy as np
from scipy.linalg import svd

"""
Singular Value Decomposition
"""
# define a matrix
X = np.array([[3, 3, 2], [2,3,-2]])
print(X)
# perform SVD
U, singular, V_transpose = svd(X)
# print different components
print("U: ",U)
print("Singular array",s)
print("V^{T}",V_transpose)

"""
Calculate Pseudo inverse
"""
# Onverse of singular matrix is just the reciprocal of each element
singular_inv = 1.0 / singular
# create m x n matrix of zeroes and put singular values in it
s_inv = np.zeros(A.shape)
s_inv[0][0]= singular_inv[0]
s_inv[1][1] =singular_inv[1]
# calculate pseudoinverse
M = np.dot(np.dot(V_transpose.T,s_inv.T),U.T)
print(M)

"""
SVD on image compression
"""

import numpy as np
import matplotlib.pyplot as plt
from skimage import data
from skimage.color import rgb2gray

cat = data.chelsea()
plt.imshow(cat)
# convert to grayscale
gray_cat = rgb2gray(cat)

# calculate the SVD and plot the image
U,S,V_T = svd(gray_cat, full_matrices=False)
S = np.diag(S)
fig, ax = plt.subplots(5, 2, figsize=(8, 20))

curr_fig=0
for r in [5, 10, 70, 100, 200]:
  cat_approx =U[:, :r] @  S[0:r, :r] @ V_T[:r, :]
  ax[curr_fig][0].imshow(256-cat_approx)
  ax[curr_fig][0].set_title("k = "+str(r))
  ax[curr_fig,0].axis('off')
  ax[curr_fig][1].set_title("Original Image")
  ax[curr_fig][1].imshow(gray_cat)
  ax[curr_fig,1].axis('off')
  curr_fig +=1
plt.show()
```

**输出:**

```
[[ 3  3  2]
 [ 2  3 -2]]
---------------------------
U:  [[-0.7815437 -0.6238505]
 [-0.6238505  0.7815437]]
---------------------------
Singular array [5.54801894 2.86696457]
---------------------------
V^{T} [[-0.64749817 -0.7599438  -0.05684667]
 [-0.10759258  0.16501062 -0.9804057 ]
 [-0.75443354  0.62869461  0.18860838]]
--------------------------
# Inverse 
array([[ 0.11462451,  0.04347826],
       [ 0.07114625,  0.13043478],
       [ 0.22134387, -0.26086957]])
---------------------------
```

![](img/421463f3a78f6b4f6d27aa61d59c51cb.png)

原始与奇异值分解 k 图像

## 参考文献:

*   [奇异值分解示例](https://www.d.umn.edu/~mhampton/m4326svd_example.pdf)