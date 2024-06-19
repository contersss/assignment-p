# Assignment #6: "树"算：Huffman,BinHeap,BST,AVL,DisjointSet

Updated 2214 GMT+8 March 24, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）这次作业内容不简单，耗时长的话直接参考题解。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统 win11

Python编程环境：PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 22275: 二叉搜索树的遍历

http://cs101.openjudge.cn/practice/22275/



思路：

依据二叉搜索树的性质进行建树，小于第一个数的位置前都在节点左侧，其余在右侧，递归处理即可

代码

```python
# 
class Tree:
    def __init__(self,x):
        self.val = x
        self.l = None
        self.r = None
def build_tree(pre):
    if len(pre) == 0:
        return None
    ii = len(pre)
    node = Tree(pre[0])
    for i in range(1,len(pre)):
        if pre[i] > pre[0]:
            ii = i
            break
    node.l = build_tree(pre[1:ii])
    node.r = build_tree(pre[ii:])
    return node
def post(root):
    if root is None:
        return []
    output = []
    output.extend(post(root.l))
    output.extend(post(root.r))
    output.append(str(root.val))
    return output
n = int(input())
pre = list(map(int,input().split()))
root = build_tree(pre)
output = post(root)
print(' '.join(output))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240331092447637](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240331092447637.png)



### 05455: 二叉搜索树的层次遍历

http://cs101.openjudge.cn/practice/05455/



思路：一个个按照大小递归插入，然后用栈进行层次遍历



代码

```python
# class Tree:
    def __init__(self,x):
        self.val = x
        self.l = None
        self.r = None
def insert(root,val):
    if root is None:
        return Tree(val)
    if val > root.val:
        root.r = insert(root.r,val)
    if val < root.val:
        root.l = insert(root.l,val)
    return root
def order(root):
    queue = [root]
    res = []
    while queue:
        node = queue.pop(0)
        res.append(node.val)
        if node.l:
            queue.append(node.l)
        if node.r:
            queue.append(node.r)
    return res
pre = list(map(int,input().split()))
root = None
for i in pre:
    root = insert(root,i)
output = order(root)
print(' '.join(str(i) for i in output))

```



代码运行截图 ==（至少包含有"Accepted"）==





### 04078: 实现堆结构

http://cs101.openjudge.cn/practice/04078/

练习自己写个BinHeap。当然机考时候，如果遇到这样题目，直接import heapq。手搓栈、队列、堆、AVL等，考试前需要搓个遍。



思路：核心在于percup和percdown这两个函数，通过反复调用这两个函数保持堆结构的有序性



代码

```python
# class BinHeap:
    def __init__(self):
        self.list = [0]
        self.size = 0
    def percUp(self,i):
        while i//2 > 0:
            if self.list[i] < self.list[i//2]:
                self.list[i],self.list[i//2] = self.list[i//2],self.list[i]
            i = i//2
    def insert(self,k):
        self.list.append(k)
        self.size += 1
        self.percUp(self.size)

    def percDown(self,k):
        while k*2<= self.size:
            mc =  self.min(k)
            if self.list[k] > self.list[mc]:
                self.list[k],self.list[mc] = self.list[mc],self.list[k]
            k = mc

    def min(self,k):
        if k*2+1> self.size:
            return k*2
        else:
            if self.list[k*2] < self.list[k*2+1]:
                return k*2
            else:
                return k*2 + 1

    def delmin(self):
        res = self.list[1]
        self.list[1] = self.list[self.size]
        self.size -= 1
        self.list.pop()
        self.percDown(1)
        return res

    def buildHeap(self,alist):
        i = len(alist) // 2
        self.size = len(alist)
        self.list = [0] + alist[:]
        while i > 0:
            self.percDown(i)
            i = i-1

n = int(input().strip())
bh = BinHeap()
for _ in range(n):
    inp = input().strip()
    if inp[0] == '1':
        bh.insert(int(inp.split()[1]))
    else:
        print(bh.delmin())

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240331092645307](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240331092645307.png)



### 22161: 哈夫曼编码树

http://cs101.openjudge.cn/practice/22161/



思路：这个结构与剪绳子那题很类似，只不过用树形结构表达出来，关键函数在于对heap进行操作和深度搜索匹配字符和其01编码



代码

```python
# import heapq

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
        merged = Node(left.weight + right.weight, min(left.char, right.char))
        merged.left = left
        merged.right = right
        heapq.heappush(heap, merged)

    return heap[0]

def encode_huffman_tree(root):
    codes = {}

    def traverse(node, code):
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

        if node.left is None and node.right is None:
            decoded += node.char
            node = root
    return decoded

n = int(input())
characters = {}
for _ in range(n):
    char, weight = input().split()
    characters[char] = int(weight)


huffman_tree = build_huffman_tree(characters)

codes = encode_huffman_tree(huffman_tree)

strings = []
while True:
    try:
        line = input()
        strings.append(line)

    except EOFError:
        break

results = []
for string in strings:
    if string[0] in ('0','1'):
        results.append(huffman_decoding(huffman_tree, string))
    else:
        results.append(huffman_encoding(codes, string))

for result in results:
    print(result)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240331092805061](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240331092805061.png)



### 晴问9.5: 平衡二叉树的建立

https://sunnywhy.com/sfbj/9/5/359



思路：

左旋和右旋函数比较关键，且简单易懂。此外在insert函数中每次通过递归更新height值是一个比较新奇的做法

代码

```python
# 
class Node:
    def __init__(self,val):
        self.value = val
        self.left = None
        self.right = None
        self.height = 1
class AVL:
    def __init__(self):
        self.root = None
    def insert(self,val):
        if not self.root:
            self.root = Node(val)
        else:
            self.root = self._insert(val,self.root)
    def _insert(self,val,node):
        if not node:
            return Node(val)
        elif val > node.value:
            node.right = self._insert(val,node.right)
        else:
            node.left = self._insert(val,node.left)
        node.height = 1+max(self.gth(node.left),self.gth(node.right))
        balance = self.gtb(node)

        if balance > 1:
            if val < node.left.value:
                return self.rr(node)
            else:
                node.left = self.rl(node.left)
                return self.rr(node)
        if balance < -1:
            if val > node.right.value:
                return self.rl(node)
            else:
                node.right = self.rr(node.right)
                return self.rl(node)
        return node
    def gth(self,node):
        if not node:
            return 0
        else:
            return node.height
    def gtb(self,node):
        if not node:
            return 0
        return self.gth(node.left)-self.gth(node.right)
    def rl(self,node):
        y = node.right
        y1 = y.left
        y.left = node
        node.right = y1
        node.height = 1 + max(self.gth(node.left), self.gth(node.right))
        y.height = 1 + max(self.gth(y.left), self.gth(y.right))
        return y
    def rr(self,node):
        x = node.left
        x1 = x.right
        x.right = node
        node.left = x1
        node.height = 1 + max(self.gth(node.left), self.gth(node.right))
        x.height = 1 + max(self.gth(x.left), self.gth(x.right))
        return x

    def preorder(self):
        return self._preorder(self.root)

    def _preorder(self, node):
        if not node:
            return []
        return [node.value] + self._preorder(node.left) + self._preorder(node.right)
a = int(input())
seq = list(map(int,input().split()))
avl = AVL()
for i in seq:
    avl.insert(i)
res = avl.preorder()
print(" ".join(str(i) for i in res))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240331093035351](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240331093035351.png)



### 02524: 宗教信仰

http://cs101.openjudge.cn/practice/02524/



思路：

通过列表来建立一棵树，索引对应的值是其父，如果是它自己本身则代表多出了一种可能的宗教信仰。

代码

```python
# 
def join(x,y,father):
    xx = gtf(x,father)
    yy = gtf(y,father)
    if xx == yy:
        return
    father[xx] = yy
def gtf(x,father):
    if father[x] != x:
        father[x] = gtf(father[x],father)
    return father[x]


case = 0
while 1:
    n,m = map(int,input().split())
    if n == 0 and m == 0:
        break
    num = 0
    father = list(range(n))
    for _ in range(m):
        x,y = map(int,input().split())
        join(x-1,y-1,father)
    for i in range(n):
        if father[i] == i:
            num += 1
    case += 1
    print(f"Case {case}: {num}")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240331093306164](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240331093306164.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==



这周题目代码都比较繁琐，但对熟悉AVL，哈夫曼编码，堆、二叉搜索树等结构很有帮助，基本上自己手敲一遍就能理解并记住大部分的代码逻辑。

这周课内需要消化的东西有点多，基本上时间都用在反复阅读树那次的课件。
