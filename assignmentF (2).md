笔试cheat sheet

[无向图](https://so.csdn.net/so/search?q=无向图&spm=1001.2101.3001.7020)中，如果任意两个顶点之间都能够连通，则称此无向图为连通图。

无向图边数的两倍等于度数

2.极大连通子图
  子图：设G = <V,E>, G’ = <V’,E’>为两个图（同为无向图或同为有向图），若V’∈ \in∈V 且 E’∈ \in∈E，则称G’是G的子图，G是G’的母图。
  极大连通子图：对于图的某一子图，它包含了图中尽可能多的顶点以及尽可能多的边，以至于它再加上一个点或者边之后它就不连通了，此时这个图就是极大连通子图。
  对于连通无向图：只有一个连通分量也就是只有一个极大连通子图，就是它本身。
  非连通图：有多个极大连通子图，也就是有多个连通分量。

3.连通分量（极大连通子图）

  无向图G的极大连通子图称为G的连通分量。
  如图 2所示，虽然图 2 a) 中的无向图不是连通图，但可以将其分解为3个“ 最大子图”，它们都满足极大连通子图的性质，因此都是连通分量，也都是极大连通子图。

一、基本概念和术语？
1.数据
数据是描述客观事物的符号，是计算机可以操作的对象，是能被计算机识别，并输入到计算机处理的符号集合。

（数据不仅仅包括整型、实型等数值型，还有字符、声音、图像、视频等非数值类型）

2.数据元素
数据元素是组成数据的、有一定意义的基本单位，在计算机中通常作为整体处理，也称为记录（元组、结点、顶点）。

3.数据项（属性、字段）
一个数据元素可以由若干个数据项组成。
数据项是数据不可分割的最小单位。
4.数据对象
数据对象是性质相同的数据元素的集合，是数据的子集。

5.数据结构
在现实世界中，不同数据元素之间不是独立的，而是存在特定的关系，这些关系称为结构。
数据结构是相互之间存在一种或多种特定关系的数据元素的集合。
数据结构包括三方面的内容：逻辑结构、存储结构和数据的运算。数据的逻辑结构和存储结构是密不可分的两个方面，一个算法的设计取决于所选定的逻辑结构，而算法的实现依赖于所采用的存储结构。
 二、逻辑结构和物理结构（存储结构）
1.逻辑结构
1）定义
逻辑结构是指数据对象中数据元素之间相互关系（逻辑关系），即从逻辑关系上描述数据。它与数据的存储无关，是独立于计算机存储器的。

2）分类（线性结构和非线性结构）
根据数据元素之间关系的不同特征，通常有下列4类基本结构，复杂程度依次递进。

①集合：结构中的数据元素之间除了同属于一个集合外，没有其他的关系。

②线性结构：线性结构中的数据元素之间是一对一的关系。

③树形结构：树形结构中的数据元素之间是一对多的关系。

④图状结构或网状结构：结构中的元素之间是多对多的关系。

2.物理结构（存储结构）
1）定义
数据的物理结构是指数据的逻辑结构在计算机中的存储方式。又称存储结构。

它研究的是数据结构在计算机中的实现方法，包括数据元素的表示和元素之间的关系。

数据元素的存储结构形式主要有两种：顺序存储和链式存储

顺序存储：把逻辑上相邻的元素存储在物理位置也相邻的存储单元中，元素之间的关系由存储单元的邻接关系来体现。
链式存储：逻辑上相邻的元素在物理位置上可以不相邻，借助指示元素存储地址的指针来表示元素之间的逻辑关系。
索引存储：在存储元素信息的同时，还建立附加的索引表，索引表中的每项称为索引项，索引项的一般形式是（关键字，地址）
散列存储：根据元素的关键字直接计算出该元素的存储地址，又称哈希（Hash）存储。

算法的特性：
1.有穷性：一个算法必须总在执行有穷步之后结束，且每一步都可在有穷时间内完成。

算法必定是有穷的，程序可以是无穷的

2.确定性：算法中每条指令必须有确定的含义，对于相同的输入只能得到相同的输出。
3.可行性：算法中描述的操作都可以通过已经实现的基本运算执行有限次来实现。
4.输入：一个算法有零个或多个输入，这些输入取自于某个特定的对象的集合。
5.输出：一个算法有一个多个输出，这些输出是与输入有着某种特定关系的量
![image-20240617214112773](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240617214112773.png)

栈

1. n个不同元素进栈，出栈元素不同排列的个数为C(n:2n)/n+1，即卡特兰数

2. 栈是一种操作受限的线性表，类似于线性表，它也有对应的两种存储方式

3. 采用顺序存储的栈称为顺序栈；栈空：S.top==-1;栈满：S.top==MaxSize-1；栈长：S.top+1

4. 栈顶指针：S.top，初始时，设置S.top = -1（有的教材中会设置为0，规定top指针指向的是栈顶元素的下一存储单元）

   进栈操作：栈不满时，栈顶指针先加1，在赋值给栈顶元素

   出栈操作：栈非空时，先取栈顶元素值，再将栈顶指针减1

   栈空条件：S.top == -1

   栈满条件：S.top == MaxSize - 1
   


循环队列

初始时：Q.front = Q.rear = 0

队首指针进1：Q.front = (Q.front + 1) % MaxSize

队尾指针进1：Q.rear = (Q.rear + 1) % MaxSize

队列长度：(Q.rear + MaxSize - Q.front) % MaxSize


树

树是n个结点的有限集，当n=0时，称为空树。
树是一种递归的数据结构，树作为一种逻辑结构同时也是一种分层的结构
结点的深度是从根开始自顶向下累加；结点的高度是从叶结点自底向上累加
由于树中的分支是有向的，即从双亲指向孩子，所以树中的路径是从上向下的，同一双亲的两个孩子之间不存在路径
树的结点数等于所有结点度数和加1
度为m的树中第i层上至多有pow(m,i-1)个结点
高度为h的m叉树至多有pow(m,h)-1/(m-1)个结点
树的路径长度是从树根到每个结点的路径长度的总和
二叉树是有序树，二叉树可以为空
一颗高度为h且含有pow(2,h)-1个结点的二叉树为满二叉树，每层结点为pow(2,h-1)
完全二叉树叶子结点只可能出现在最大的两层上；若有度为1的结点只可能有一个且在左孩子上
非空二叉树上的叶子结点数等于度为2的结点数加1，即n0=n2+1
具有n个结点的完全二叉树的高度为log(n+1)或logn+1

![image-20240617230148341](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240617230148341.png)

![image-20240617230229048](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240617230229048.png)



查找

1. 一般线性表的顺序查找：查找成功ASL=(n+1)/2;失败ASL=n+1
2. 有序表的顺序查找：不成功ASL=n/2+n/(n+1)
3. 散列表的查找效率取决于三个因素：散列函数、处理冲突的方法和装填因子



 串的相关概念
串：即字符串（String）是由零个或多个字符组成的有限序列。
串的长度：中字符的个数 n，n = 0 n = 0n=0 时的串称为空串。
子串：串中任意个连续的字符组成的子序列。
主串：包含子串的串。
字符在主串中的位置：字符在串中的序号。
子串在主串中的位置：子串的第一个字符在主串中的位置 。
![请添加图片描述](https://img-blog.csdnimg.cn/70d9f4c5faf14e2893203debf054d067.png)

![image-20240617222614290](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240617222614290.png)

![image-20240617222624074](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240617222624074.png)

中转后代码

```
  for char in expression:
        if char.isnumeric() or char == '.':
            number += char
        else:
            if number:
                num = float(number)
                postfix.append(int(num) if num.is_integer() else num)
                number = ''
            if char in '+-*/':
                while stack and stack[-1] in '+-*/' and precedence[char] <= precedence[stack[-1]]:
                    postfix.append(stack.pop())
                stack.append(char)
            elif char == '(':
                stack.append(char)
            elif char == ')':
                while stack and stack[-1] != '(':
                    postfix.append(stack.pop())
                stack.pop()
```

哈夫曼

```
import heapq

class Node:
    def __init__(self, weight, char=None):
        self.weight = weight
        self.char = char
        self.left = None
        self.right = None

    def __lt__(self, other):
        if self.weight == other.weight:
            return self.char < other.char
        return self.weight < other.weight

def build_huffman_tree(characters):
    heap = []
    for char, weight in characters.items():
        heapq.heappush(heap, Node(weight, char))

    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)
        #merged = Node(left.weight + right.weight) #note: 合并后，char 字段默认值是空
        merged = Node(left.weight + right.weight, min(left.char, right.char))
        merged.left = left
        merged.right = right
        heapq.heappush(heap, merged)

    return heap[0]

def encode_huffman_tree(root):
    codes = {}

    def traverse(node, code):
        #if node.char:
        if node.left is None and node.right is None:
            codes[node.char] = code
        else:
            traverse(node.left, code + '0')
            traverse(node.right, code + '1')

    traverse(root, '')
    return codes

def huffman_encoding(codes, string):
    encoded = ''
    for char in string:
        encoded += codes[char]
    return encoded

def huffman_decoding(root, encoded_string):
    decoded = ''
    node = root
    for bit in encoded_string:
        if bit == '0':
            node = node.left
        else:
            node = node.right

        #if node.char:
        if node.left is None and node.right is None:
            decoded += node.char
            node = root
    return decoded

# 读取输入
n = int(input())
characters = {}
for _ in range(n):
    char, weight = input().split()
    characters[char] = int(weight)

#string = input().strip()
#encoded_string = input().strip()

# 构建哈夫曼编码树
huffman_tree = build_huffman_tree(characters)

# 编码和解码
codes = encode_huffman_tree(huffman_tree)

strings = []
while True:
    try:
        line = input()
        strings.append(line)

    except EOFError:
        break

results = []
#print(strings)
for string in strings:
    if string[0] in ('0','1'):
        results.append(huffman_decoding(huffman_tree, string))
    else:
        results.append(huffman_encoding(codes, string))

for result in results:
    print(result)
```

堆

```
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0

    def percUp(self, i):
        while i // 2 > 0:
            if self.heapList[i] < self.heapList[i // 2]:
                tmp = self.heapList[i // 2]
                self.heapList[i // 2] = self.heapList[i]
                self.heapList[i] = tmp
            i = i // 2

    def insert(self, k):
        self.heapList.append(k)
        self.currentSize = self.currentSize + 1
        self.percUp(self.currentSize)

    def percDown(self, i):
        while (i * 2) <= self.currentSize:
            mc = self.minChild(i)
            if self.heapList[i] > self.heapList[mc]:
                tmp = self.heapList[i]
                self.heapList[i] = self.heapList[mc]
                self.heapList[mc] = tmp
            i = mc

    def minChild(self, i):
        if i * 2 + 1 > self.currentSize:
            return i * 2
        else:
            if self.heapList[i * 2] < self.heapList[i * 2 + 1]:
                return i * 2
            else:
                return i * 2 + 1

    def delMin(self):
        retval = self.heapList[1]
        self.heapList[1] = self.heapList[self.currentSize]
        self.currentSize = self.currentSize - 1
        self.heapList.pop()
        self.percDown(1)
        return retval

    def buildHeap(self, alist):
        i = len(alist) // 2
        self.currentSize = len(alist)
        self.heapList = [0] + alist[:]
        while (i > 0):
            #print(f'i = {i}, {self.heapList}')
            self.percDown(i)
            i = i - 1
        #print(f'i = {i}, {self.heapList}')


n = int(input().strip())
bh = BinHeap()
for _ in range(n):
    inp = input().strip()
    if inp[0] == '1':
        bh.insert(int(inp.split()[1]))
    else:
        print(bh.delMin())
```

拓扑

```python
from collections import deque, defaultdict

def topological_sort(graph):
    indegree = defaultdict(int)
    result = []
    queue = deque()

    # 计算每个顶点的入度
    for u in graph:
        for v in graph[u]:
            indegree[v] += 1

    # 将入度为 0 的顶点加入队列
    for u in graph:
        if indegree[u] == 0:
            queue.append(u)

    # 执行拓扑排序
    while queue:
        u = queue.popleft()
        result.append(u)

        for v in graph[u]:
            indegree[v] -= 1
            if indegree[v] == 0:
                queue.append(v)

    # 检查是否存在环
    if len(result) == len(graph):
        return result
    else:
        return None
```

floyd

```
def floyd_warshall(graph):
    n = len(graph)
    dist = [[float('inf')] * n for _ in range(n)]

    for i in range(n):
        for j in range(n):
            if i == j:
                dist[i][j] = 0
            elif j in graph[i]:
                dist[i][j] = graph[i][j]

    for k in range(n):
        for i in range(n):
            for j in range(n):
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

    return dist
```

kruskal

```
class DisjointSet:
    def __init__(self, num_vertices):
        self.parent = list(range(num_vertices))
        self.rank = [0] * num_vertices

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)

        if root_x != root_y:
            if self.rank[root_x] < self.rank[root_y]:
                self.parent[root_x] = root_y
            elif self.rank[root_x] > self.rank[root_y]:
                self.parent[root_y] = root_x
            else:
                self.parent[root_x] = root_y
                self.rank[root_y] += 1


def kruskal(graph):
    num_vertices = len(graph)
    edges = []

    # 构建边集
    for i in range(num_vertices):
        for j in range(i + 1, num_vertices):
            if graph[i][j] != 0:
                edges.append((i, j, graph[i][j]))

    # 按照权重排序
    edges.sort(key=lambda x: x[2])

    # 初始化并查集
    disjoint_set = DisjointSet(num_vertices)

    # 构建最小生成树的边集
    minimum_spanning_tree = []

    for edge in edges:
        u, v, weight = edge
        if disjoint_set.find(u) != disjoint_set.find(v):
            disjoint_set.union(u, v)
            minimum_spanning_tree.append((u, v, weight))

    return minimum_spanning_tree
```

dijkstra

```
def dijkstra(graph, start):
    pq = []
    start.distance = 0
    heapq.heappush(pq, (0, start))
    visited = set()

    while pq:
        currentDist, currentVert = heapq.heappop(pq)    # 当一个顶点的最短路径确定后（也就是这个顶点
                                                        # 从优先队列中被弹出时），它的最短路径不会再改变。
        if currentVert in visited:
            continue
        visited.add(currentVert)

        for nextVert in currentVert.getConnections():
            newDist = currentDist + currentVert.getWeight(nextVert)
            if newDist < nextVert.distance:
                nextVert.distance = newDist
                nextVert.pred = currentVert
                heapq.heappush(pq, (newDist, nextVert))
```

prim

```
def prim(graph, start):
    pq = []
    start.distance = 0
    heapq.heappush(pq, (0, start))
    visited = set()

    while pq:
        currentDist, currentVert = heapq.heappop(pq)
        if currentVert in visited:
            continue
        visited.add(currentVert)

        for nextVert in currentVert.getConnections():
            weight = currentVert.getWeight(nextVert)
            if nextVert not in visited and weight < nextVert.distance:
                nextVert.distance = weight
                nextVert.pred = currentVert
                heapq.heappush(pq, (weight, nextVert))
```

kora

```
def dfs1(graph, node, visited, stack):
    visited[node] = True
    for neighbor in graph[node]:
        if not visited[neighbor]:
            dfs1(graph, neighbor, visited, stack)
    stack.append(node)

def dfs2(graph, node, visited, component):
    visited[node] = True
    component.append(node)
    for neighbor in graph[node]:
        if not visited[neighbor]:
            dfs2(graph, neighbor, visited, component)

def kosaraju(graph):
    # Step 1: Perform first DFS to get finishing times
    stack = []
    visited = [False] * len(graph)
    for node in range(len(graph)):
        if not visited[node]:
            dfs1(graph, node, visited, stack)
    
    # Step 2: Transpose the graph
    transposed_graph = [[] for _ in range(len(graph))]
    for node in range(len(graph)):
        for neighbor in graph[node]:
            transposed_graph[neighbor].append(node)
    
    # Step 3: Perform second DFS on the transposed graph to find SCCs
    visited = [False] * len(graph)
    sccs = []
    while stack:
        node = stack.pop()
        if not visited[node]:
            scc = []
            dfs2(transposed_graph, node, visited, scc)
            sccs.append(scc)
    return sccs

# Example
graph = [[1], [2, 4], [3, 5], [0, 6], [5], [4], [7], [5, 6]]
sccs = kosaraju(graph)
print("Strongly Connected Components:")
for scc in sccs:
    print(scc)
```

kmp

```
def compute_lps(pattern):
    """
    计算pattern字符串的最长前缀后缀（Longest Proper Prefix which is also Suffix）表
    :param pattern: 模式字符串
    :return: lps表
    """

    m = len(pattern)
    lps = [0] * m
    length = 0
    for i in range(1, m):
        while length > 0 and pattern[i] != pattern[length]:
            length = lps[length - 1]    # 跳过前面已经比较过的部分
        if pattern[i] == pattern[length]:
            length += 1
        lps[i] = length
    return lps


def kmp_search(text, pattern):
    n = len(text)
    m = len(pattern)
    if m == 0:
        return 0
    lps = compute_lps(pattern)
    matches = []

    j = 0  # j是pattern的索引
    for i in range(n):  # i是text的索引
        while j > 0 and text[i] != pattern[j]:
            j = lps[j - 1]
        if text[i] == pattern[j]:
            j += 1
        if j == m:
            matches.append(i - j + 1)
            j = lps[j - 1]
    return matches


text = "ABABABABCABABABABCABABABABC"
pattern = "ABABCABAB"
index = kmp_search(text, pattern)
print("pos matched：", index)
# pos matched： [4, 13]
```

骑士周游

```
def knight_graph(board_size):
    kt_graph = Graph()
    for row in range(board_size):           #遍历每一行
        for col in range(board_size):       #遍历行上的每一个格子
            node_id = pos_to_node_id(row, col, board_size) #把行、列号转为格子ID
            new_positions = gen_legal_moves(row, col, board_size) #按照 马走日，返回下一步可能位置
            for row2, col2 in new_positions:
                other_node_id = pos_to_node_id(row2, col2, board_size) #下一步的格子ID
                kt_graph.add_edge(node_id, other_node_id) #在骑士周游图中为两个格子加一条边
    return kt_graph

def pos_to_node_id(x, y, bdSize):
    return x * bdSize + y

def gen_legal_moves(row, col, board_size):
    new_moves = []
    move_offsets = [                        # 马走日的8种走法
        (-1, -2),  # left-down-down
        (-1, 2),  # left-up-up
        (-2, -1),  # left-left-down
        (-2, 1),  # left-left-up
        (1, -2),  # right-down-down
        (1, 2),  # right-up-up
        (2, -1),  # right-right-down
        (2, 1),  # right-right-up
    ]
    for r_off, c_off in move_offsets:
        if (                                # #检查，不能走出棋盘
            0 <= row + r_off < board_size
            and 0 <= col + c_off < board_size
        ):
            new_moves.append((row + r_off, col + c_off))
    return new_moves

# def legal_coord(row, col, board_size):
#     return 0 <= row < board_size and 0 <= col < board_size


def knight_tour(n, path, u, limit):
    u.color = "gray"
    path.append(u)              #当前顶点涂色并加入路径
    if n < limit:
        neighbors = ordered_by_avail(u) #对所有的合法移动依次深入
        #neighbors = sorted(list(u.get_neighbors()))
        i = 0

        for nbr in neighbors:
            if nbr.color == "white" and \
                knight_tour(n + 1, path, nbr, limit):   #选择“白色”未经深入的点，层次加一，递归深入
                return True
        else:                       #所有的“下一步”都试了走不通
            path.pop()              #回溯，从路径中删除当前顶点
            u.color = "white"       #当前顶点改回白色
            return False
    else:
        return True

def ordered_by_avail(n):
    res_list = []
    for v in n.get_neighbors():
        if v.color == "white":
            c = 0
            for w in v.get_neighbors():
                if w.color == "white":
                    c += 1
            res_list.append((c,v))
    res_list.sort(key = lambda x: x[0])
    return [y[1] for y in res_list]
```
