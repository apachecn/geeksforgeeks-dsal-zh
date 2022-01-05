# 代码不工作怎么办？

> 原文:[https://www . geesforgeks . org/如果代码不起作用怎么办/](https://www.geeksforgeeks.org/what-to-do-if-the-code-doesnt-work/)

本文将讨论如果他们的代码无法在各种场景中工作，可以采取的不同途径。

如果一个人，至少看起来，在语句中包含的测试用例中完美地编码了一切，测试了解决方案，但是在代码提交到系统中之后，它在测试中失败了，并且没有明确的错误代码来帮助识别和解决问题。该问题可能由多种原因引起，但通常是以下原因之一:

*   回答错误
*   [超过时间/内存限制](https://www.geeksforgeeks.org/overcome-time-limit-exceedtle/)
*   [失败(运行时错误)](https://www.geeksforgeeks.org/errors-in-cc/)

尽管方法可能因原因而异，但通常可以遵循以下步骤:

*   **检查** [**边缘情况**](https://www.geeksforgeeks.org/dont-forget-edge-cases/) :例如，如果 N = 1 或 N 是满足约束的最大可能数。检查给定的输入是否在所有可能的意义上符合约束，程序的行为是否正确。
*   **生成一些你知道正确答案的通用测试用例:**。在用纸笔弄清楚答案应该是什么之前，不要看这些测试的代码答案。否则，很容易说服自己它是正确的，却看不到一些愚蠢的错误。
*   **时间限制超过了误差**，测量程序对于较大输入的工作时间。以下功能有助于测量程序启动后的 CPU 时间:
    *   *包含时间的 C++(双)时钟()/时钟/秒。*
    *   *python time.clock()以秒为单位返回浮点值。*
    *   *Java System.nanoTime()返回以纳秒为单位的长值。*

**测量小测试、中测试和大测试的时间。可能会遇到以下结果之一:**

*   该程序在时间上适用于中小型测试，但它比需要的速度慢 10 倍以上(或者在大型测试中挂起)。在这种情况下，程序可能存在复杂性问题，我们可以尝试使用以下选项来解决问题:
    *   测量程序各部分分别花费的时间。例如，读取输入/打印输出需要多长时间)。
    *   计算你的算法和它的部分所做的实际操作数，看看它是否是预期的。
    *   检查引用是否已经被传递到仅适用于 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 、在 [Java](https://www.geeksforgeeks.org/java/) 和在 [Python](https://www.geeksforgeeks.org/python-programming-language/) 中的函数。它总是被引用)。
*   该程序在小型或中型测试中挂起。检查无限循环/递归。在循环和函数的前置条件和后置条件上添加断言(c++、python 和 java 中的断言)，看看它们是否失败。使用调试输出/调试器查看导致挂起的代码路径。
*   如果是[运行时错误](https://www.geeksforgeeks.org/runtime-errors/)，消息可能是未知信号，那么可能是一个好的信号。这是信息最丰富的原因之一，意味着程序可能会因以下因素之一而崩溃:
    *   在内存中访问不属于该程序的位置。在 C++中，它可以采取两种形式:试图访问数组中不存在的元素，试图计算一个[空指针](https://www.geeksforgeeks.org/few-bytes-on-null-pointer-in-c/)或指向不属于程序的位置的指针。
    *   做一个[算术错误](https://www.geeksforgeeks.org/floating-point-error-in-python/) : [除以零](https://www.geeksforgeeks.org/java-program-to-handle-divide-by-zero-and-multiple-exceptions/)，[溢出一个浮点数](https://www.geeksforgeeks.org/overflow-in-arithmetic-addition-in-binary-number-system/)等等。
    *   (特定于 C++的)超出堆栈大小，这可能是由无限递归或在函数内部创建大对象(如数组)引起的。

**生成不同的测试，并对它们运行您的程序，直到它崩溃:**

*   “答案错误”的原因可能是最具挑战性的；很多事情都会导致它。要查找失败的测试，可以执行以下操作之一:
    *   找到一个在效率方面可能不正确的替代解决方案(有些情况下甚至不适用于某些类型的测试)，但可以用来检查主解决方案的答案是否正确。
    *   如果有不一致的地方，让程序崩溃。这意味着为函数和循环的后置条件和前置条件添加断言。

**如何生成测试:**生成测试最简单的方法是编写一个程序，将测试打印到文本文件中。下面是一个例子来说明这一点:

**程序 1:** 生成最大成对相异的测试:

## 蟒蛇 3

```
import sys
n = int(sys.argv[1])
print(n)
print(' '.join([str(i∗2)for i in range(n)])
```

这里最神秘的可能是 sys.argv[1]。这是第一个命令行参数的 getter。现在，如何用这个来运行程序？将可执行文件或 python 脚本复制到与生成脚本相同的目录，并运行以下命令:

> *python script . py 17>input . txt*
> *。/your _ program _ name<input . txt*

建议使用 Python3 而不是 Python。在少数情况下，它可以帮助解决问题。因此，一些测试可以自动生成，程序可以针对它们运行，但是以下问题仍然没有答案:

*   如何随机化测试？
*   如何生成大量的？
*   如何核对答案？

**生成随机测试并在其上运行您的程序:**可以使用以下由 3 部分组成的技术:

*   测试生成器，接受种子作为命令行参数，如程序 2 中所述。
*   另一种解决方案。
*   使用来自(1)的生成器重复生成测试的脚本在生成的测试上运行主解决方案和模型解决方案，并检查程序 2 中的答案是否一致。

**程序 2:** 从命令行接受种子的生成器:

## 蟒蛇 3

```
import random
import sys

# Input the number N
n = int(sys.argv[1])
myseed = int(sys.argv[2])
random.seed(myseed)

print(n)

# 1000 could also be moved to
# parameters instead of making it
# a hard constant in the code
print(' '.join([str(random.randint(1, 1000)) for i in range(n)])
```

**程序三:**实际脚本:

## 蟒蛇 3

```
import random
import sys
import os

# Accept the number of tests as a
# command line parameter

tests = int(sys.argv[1])

# Accept the parameter for the
# tests as a command line parameter

n = int(sys.argv[2])
for i in range(tests):
    print("Test #" + str(i))

    # Run the generator gen.py with
    # parameter n and the seed i
os.system("python3 gen.py " + str(n) + " " + str(i) + " > input.txt")

# Run the model solution model.py
# Notice that it is not necessary
# that solution is implemented in
# python, you can as well run
# ./model < input.txt > model.txt
# for a C++ solution.

os.system("python3 model.py < input.txt > model.txt")

# Run the main solution

os.system("python3 main.py < input.txt > main.txt")

# Read the output of the
# model solution

with open('model.txt') as f:
    model = f.read()
print("Model: ", model)

# Read the output of the
# main solution :

with open('main.txt') as f:
    main = f.read()
print("Main: ", main)
if model != main:
    break
```

**如何添加断言:**在 Java、Python 和 C++中，断言表达式、断言表达式、断言(表达式)；如果布尔表达式为假，将产生运行时错误。断言的一种可能用法是验证程序的答案是否一致。另一个常见的用例是验证程序的中间步骤是否一致。