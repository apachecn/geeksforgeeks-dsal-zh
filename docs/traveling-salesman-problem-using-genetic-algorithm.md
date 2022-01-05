# 使用遗传算法的旅行商问题

> 原文:[https://www . geesforgeks . org/旅行推销员-使用遗传算法解决问题/](https://www.geeksforgeeks.org/traveling-salesman-problem-using-genetic-algorithm/)

**先决条件:** [遗传算法](https://www.geeksforgeeks.org/genetic-algorithms/)[旅行商问题](https://www.geeksforgeeks.org/traveling-salesman-problem-tsp-implementation/)
本文提出一种遗传算法来求解[旅行商问题](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)。
遗传算法是受支持生命进化过程启发的启发式搜索算法。该算法旨在复制自然选择过程来进行世代，即适者生存。标准遗传算法分为五个阶段:

1.  创造初始人口。
2.  计算适合度。
3.  选择最佳基因。
4.  穿过去。
5.  变异以引入变异。

这些算法可以被实现来寻找各种类型的优化问题的解决方案。其中一个问题就是[旅行推销员问题](https://www.geeksforgeeks.org/traveling-salesman-problem-tsp-implementation/)。问题说的是，给一个推销员一组城市，他必须找到最短的路线，以便准确地访问每个城市一次，然后返回出发城市。
**方法:**在下面的实现中，城市被视为基因，使用这些字符生成的字符串被称为染色体，而等于所提到的所有城市的路径长度的适应度分数被用于目标人群。
适应度评分定义为基因描述的路径长度。路径长度越短，基因越合适。基因库中所有基因中最合适的一个通过了群体测试，进入下一个迭代。迭代次数取决于冷却变量的值。冷却变量值随着每次迭代不断减小，并在一定次数的迭代后达到阈值。
**算法:**

```
1\. Initialize the population randomly.
2\. Determine the fitness of the chromosome.
3\. Until done repeat:
    1\. Select parents.
    2\. Perform crossover and mutation.
    3\. Calculate the fitness of the new population.
    4\. Append it to the gene pool.
```

**伪码**

```
Initialize procedure GA{
    Set cooling parameter = 0;
    Evaluate population P(t);
    While( Not Done ){
        Parents(t) = Select_Parents(P(t));
        Offspring(t) = Procreate(P(t));
        p(t+1) = Select_Survivors(P(t), Offspring(t));
        t = t + 1; 
    }
}
```

**突变是如何工作的？**
假设有 5 个城市:0、1、2、3、4。销售员在城市 0，他必须找到最短的路线，穿过所有城市回到城市 0。代表所选路径的染色体可以表示为:

![](img/2be697ba4973c0ad1bec0221af102575.png)

这条染色体发生突变。在突变过程中，染色体中两个城市的位置互换，形成新的配置，除了第一个和最后一个细胞，因为它们代表起点和终点。

![](img/9039efed9faabe724d6e850359ec7461.png)

根据下面定义的输入，原始染色体的路径长度等于 **INT_MAX** ，因为城市 1 和城市 4 之间的路径不存在。变异后形成的新子路径长度等于 **21** ，这是比原假设优化很多的答案。这就是遗传算法如何优化难题的解决方案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#include <limits.h>
using namespace std;

// Number of cities in TSP
#define V 5

// Names of the cities
#define GENES ABCDE

// Starting Node Value
#define START 0

// Initial population size for the algorithm
#define POP_SIZE 10

// Structure of a GNOME
// string defines the path traversed
// by the salesman while the fitness value
// of the path is stored in an integer

struct individual {
    string gnome;
    int fitness;
};

// Function to return a random number
// from start and end
int rand_num(int start, int end)
{
    int r = end - start;
    int rnum = start + rand() % r;
    return rnum;
}

// Function to check if the character
// has already occurred in the string
bool repeat(string s, char ch)
{
    for (int i = 0; i < s.size(); i++) {
        if (s[i] == ch)
            return true;
    }
    return false;
}

// Function to return a mutated GNOME
// Mutated GNOME is a string
// with a random interchange
// of two genes to create variation in species
string mutatedGene(string gnome)
{
    while (true) {
        int r = rand_num(1, V);
        int r1 = rand_num(1, V);
        if (r1 != r) {
            char temp = gnome[r];
            gnome[r] = gnome[r1];
            gnome[r1] = temp;
            break;
        }
    }
    return gnome;
}

// Function to return a valid GNOME string
// required to create the population
string create_gnome()
{
    string gnome = "0";
    while (true) {
        if (gnome.size() == V) {
            gnome += gnome[0];
            break;
        }
        int temp = rand_num(1, V);
        if (!repeat(gnome, (char)(temp + 48)))
            gnome += (char)(temp + 48);
    }
    return gnome;
}

// Function to return the fitness value of a gnome.
// The fitness value is the path length
// of the path represented by the GNOME.
int cal_fitness(string gnome)
{
    int map[V][V] = { { 0, 2, INT_MAX, 12, 5 },
                    { 2, 0, 4, 8, INT_MAX },
                    { INT_MAX, 4, 0, 3, 3 },
                    { 12, 8, 3, 0, 10 },
                    { 5, INT_MAX, 3, 10, 0 } };
    int f = 0;
    for (int i = 0; i < gnome.size() - 1; i++) {
        if (map[gnome[i] - 48][gnome[i + 1] - 48] == INT_MAX)
            return INT_MAX;
        f += map[gnome[i] - 48][gnome[i + 1] - 48];
    }
    return f;
}

// Function to return the updated value
// of the cooling element.
int cooldown(int temp)
{
    return (90 * temp) / 100;
}

// Comparator for GNOME struct.
bool lessthan(struct individual t1,
            struct individual t2)
{
    return t1.fitness < t2.fitness;
}

// Utility function for TSP problem.
void TSPUtil(int map[V][V])
{
    // Generation Number
    int gen = 1;
    // Number of Gene Iterations
    int gen_thres = 5;

    vector<struct individual> population;
    struct individual temp;

    // Populating the GNOME pool.
    for (int i = 0; i < POP_SIZE; i++) {
        temp.gnome = create_gnome();
        temp.fitness = cal_fitness(temp.gnome);
        population.push_back(temp);
    }

    cout << "\nInitial population: " << endl
        << "GNOME     FITNESS VALUE\n";
    for (int i = 0; i < POP_SIZE; i++)
        cout << population[i].gnome << " "
            << population[i].fitness << endl;
    cout << "\n";

    bool found = false;
    int temperature = 10000;

    // Iteration to perform
    // population crossing and gene mutation.
    while (temperature > 1000 && gen <= gen_thres) {
        sort(population.begin(), population.end(), lessthan);
        cout << "\nCurrent temp: " << temperature << "\n";
        vector<struct individual> new_population;

        for (int i = 0; i < POP_SIZE; i++) {
            struct individual p1 = population[i];

            while (true) {
                string new_g = mutatedGene(p1.gnome);
                struct individual new_gnome;
                new_gnome.gnome = new_g;
                new_gnome.fitness = cal_fitness(new_gnome.gnome);

                if (new_gnome.fitness <= population[i].fitness) {
                    new_population.push_back(new_gnome);
                    break;
                }
                else {

                    // Accepting the rejected children at
                    // a possible probability above threshold.
                    float prob = pow(2.7,
                                    -1 * ((float)(new_gnome.fitness
                                                - population[i].fitness)
                                        / temperature));
                    if (prob > 0.5) {
                        new_population.push_back(new_gnome);
                        break;
                    }
                }
            }
        }

        temperature = cooldown(temperature);
        population = new_population;
        cout << "Generation " << gen << " \n";
        cout << "GNOME     FITNESS VALUE\n";

        for (int i = 0; i < POP_SIZE; i++)
            cout << population[i].gnome << " "
                << population[i].fitness << endl;
        gen++;
    }
}

int main()
{

    int map[V][V] = { { 0, 2, INT_MAX, 12, 5 },
                    { 2, 0, 4, 8, INT_MAX },
                    { INT_MAX, 4, 0, 3, 3 },
                    { 12, 8, 3, 0, 10 },
                    { 5, INT_MAX, 3, 10, 0 } };
    TSPUtil(map);
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from random import randint

INT_MAX = 2147483647
# Number of cities in TSP
V = 5

# Names of the cities
GENES = "ABCDE"

# Starting Node Value
START = 0

# Initial population size for the algorithm
POP_SIZE = 10

# Structure of a GNOME
# defines the path traversed
# by the salesman while the fitness value
# of the path is stored in an integer

class individual:
    def __init__(self) -> None:
        self.gnome = ""
        self.fitness = 0

    def __lt__(self, other):
        return self.fitness < other.fitness

    def __gt__(self, other):
        return self.fitness > other.fitness

# Function to return a random number
# from start and end
def rand_num(start, end):
    return randint(start, end-1)

# Function to check if the character
# has already occurred in the string
def repeat(s, ch):
    for i in range(len(s)):
        if s[i] == ch:
            return True

    return False

# Function to return a mutated GNOME
# Mutated GNOME is a string
# with a random interchange
# of two genes to create variation in species
def mutatedGene(gnome):
    gnome = list(gnome)
    while True:
        r = rand_num(1, V)
        r1 = rand_num(1, V)
        if r1 != r:
            temp = gnome[r]
            gnome[r] = gnome[r1]
            gnome[r1] = temp
            break
    return ''.join(gnome)

# Function to return a valid GNOME string
# required to create the population
def create_gnome():
    gnome = "0"
    while True:
        if len(gnome) == V:
            gnome += gnome[0]
            break

        temp = rand_num(1, V)
        if not repeat(gnome, chr(temp + 48)):
            gnome += chr(temp + 48)

    return gnome

# Function to return the fitness value of a gnome.
# The fitness value is the path length
# of the path represented by the GNOME.
def cal_fitness(gnome):
    mp = [
        [0, 2, INT_MAX, 12, 5],
        [2, 0, 4, 8, INT_MAX],
        [INT_MAX, 4, 0, 3, 3],
        [12, 8, 3, 0, 10],
        [5, INT_MAX, 3, 10, 0],
    ]
    f = 0
    for i in range(len(gnome) - 1):
        if mp[ord(gnome[i]) - 48][ord(gnome[i + 1]) - 48] == INT_MAX:
            return INT_MAX
        f += mp[ord(gnome[i]) - 48][ord(gnome[i + 1]) - 48]

    return f

# Function to return the updated value
# of the cooling element.
def cooldown(temp):
    return (90 * temp) / 100

# Comparator for GNOME struct.
# def lessthan(individual t1,
#               individual t2)
# :
#     return t1.fitness < t2.fitness

# Utility function for TSP problem.
def TSPUtil(mp):
    # Generation Number
    gen = 1
    # Number of Gene Iterations
    gen_thres = 5

    population = []
    temp = individual()

    # Populating the GNOME pool.
    for i in range(POP_SIZE):
        temp.gnome = create_gnome()
        temp.fitness = cal_fitness(temp.gnome)
        population.append(temp)

    print("\nInitial population: \nGNOME     FITNESS VALUE\n")
    for i in range(POP_SIZE):
        print(population[i].gnome, population[i].fitness)
    print()

    found = False
    temperature = 10000

    # Iteration to perform
    # population crossing and gene mutation.
    while temperature > 1000 and gen <= gen_thres:
        population.sort()
        print("\nCurrent temp: ", temperature)
        new_population = []

        for i in range(POP_SIZE):
            p1 = population[i]

            while True:
                new_g = mutatedGene(p1.gnome)
                new_gnome = individual()
                new_gnome.gnome = new_g
                new_gnome.fitness = cal_fitness(new_gnome.gnome)

                if new_gnome.fitness <= population[i].fitness:
                    new_population.append(new_gnome)
                    break

                else:

                    # Accepting the rejected children at
                    # a possible probability above threshold.
                    prob = pow(
                        2.7,
                        -1
                        * (
                            (float)(new_gnome.fitness - population[i].fitness)
                            / temperature
                        ),
                    )
                    if prob > 0.5:
                        new_population.append(new_gnome)
                        break

        temperature = cooldown(temperature)
        population = new_population
        print("Generation", gen)
        print("GNOME     FITNESS VALUE")

        for i in range(POP_SIZE):
            print(population[i].gnome, population[i].fitness)
        gen += 1

if __name__ == "__main__":

    mp = [
        [0, 2, INT_MAX, 12, 5],
        [2, 0, 4, 8, INT_MAX],
        [INT_MAX, 4, 0, 3, 3],
        [12, 8, 3, 0, 10],
        [5, INT_MAX, 3, 10, 0],
    ]
    TSPUtil(mp)
```

**Output:** 

```
Initial population: 
GNOME     FITNESS VALUE
043210   24
023410   2147483647
031420   2147483647
034210   31
043210   24
023140   2147483647
032410   2147483647
012340   24
012340   24
032410   2147483647

Current temp: 10000
Generation 1 
GNOME     FITNESS VALUE
013240   21
013240   21
012430   31
012430   31
031240   32
024310   2147483647
013420   2147483647
032140   2147483647
034210   31
012430   31

Current temp: 9000
Generation 2 
GNOME     FITNESS VALUE
031240   32
043210   24
012340   24
042130   32
043210   24
012340   24
034210   31
014320   2147483647
014320   2147483647
023140   2147483647

Current temp: 8100
Generation 3 
GNOME     FITNESS VALUE
013240   21
042310   21
013240   21
013240   21
031240   32
013240   21
012430   31
034120   2147483647
041320   2147483647
043120   2147483647

Current temp: 7290
Generation 4 
GNOME     FITNESS VALUE
031240   32
043210   24
043210   24
043210   24
012340   24
042130   32
013240   21
014320   2147483647
021340   2147483647
043210   24

Current temp: 6561
Generation 5 
GNOME     FITNESS VALUE
043210   24
042310   21
042310   21
013240   21
042310   21
034210   31
013240   21
042310   21
024310   2147483647
024310   2147483647
```