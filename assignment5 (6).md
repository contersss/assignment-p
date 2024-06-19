# Assignment #5: "树"算：概念、表示、解析、遍历

Updated 2124 GMT+8 March 17, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：WIN11

Python编程环境： PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 27638: 求二叉树的高度和叶子数目

http://cs101.openjudge.cn/practice/27638/



思路：比较模板，没啥技巧，10min

代码

```python
# class tree:
    def __init__(self):
        self.l = None
        self.r = None


def maxx(root):
    if root is None:
        return -1
    else:
        ld = maxx(root.l)
        rd = maxx(root.r)
        return max(ld,rd)+1
def leaf(root):
    if root is None:
        return 0
    elif root.l is None and root.r is None:
        return 1

    return leaf(root.l)+leaf(root.r)


n = int(input())
nodes = [tree() for _ in range(n)]
has_parent = [False]*n
for _ in range(n):
    l,r = map(int,input().split())
    if l != -1:
        nodes[_].l = nodes[l]
        has_parent[l] = True
    if r != -1:
        nodes[_].r =nodes[r]
        has_parent[r] = True
root_index = has_parent.index(False)
root = nodes[root_index]
print(maxx(root),leaf(root),sep = ' ',end = '')

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240324210410770](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240324210410770.png)



### 24729: 括号嵌套树

http://cs101.openjudge.cn/practice/24729/



思路：主要在于理解栈的作用在于记录信息，左右括号代表子节点的出现与结束。20min



代码

```python
# 
class tree:
    def __init__(self,x):
        self.val = x
        self.child = []
def pre(node):
    output = [node.val]
    for chi in node.child:
        output.extend(pre(chi))
    return "".join(output)

def pos(node):
    output = []
    for chi in node.child:
        output.extend(pos(chi))
    output.append(node.val)
    return  "".join(output)
stack = []
string = input()
node = None
for i in string:
    if i.isalpha():
        node = tree(i)
        if stack:
            stack[-1].child.append(node)
    elif i == "(":
        if node:
            stack.append(node)
            node = None
    elif i == ")":
        if stack:
            node = stack.pop()
print(pre(node))
print(pos(node))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240324210454843](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240324210454843.png)



### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/



思路：对着题解写的，本质上还是树，只不过换了一层壳，25min



代码

```python
# 
from sys import exit

class dir:
    def __init__(self, dname):
        self.name = dname
        self.dirs = []
        self.files = []
    
    def getGraph(self):
        g = [self.name]
        for d in self.dirs:
            subg = d.getGraph()
            g.extend(["|     " + s for s in subg])
        for f in sorted(self.files):
            g.append(f)
        return g

n = 0
while True:
    n += 1
    stack = [dir("ROOT")]
    while (s := input()) != "*":
        if s == "#": exit(0)
        if s[0] == 'f':
            stack[-1].files.append(s)
        elif s[0] == 'd':
            stack.append(dir(s))
            stack[-2].dirs.append(stack[-1])
        else:
            stack.pop()
    print(f"DATA SET {n}:")
    print(*stack[0].getGraph(), sep='\n')
    print()
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240324210728455](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240324210728455.png)



### 25140: 根据后序表达式建立队列表达式

http://cs101.openjudge.cn/practice/25140/



思路：

建立列表解析树然后层次遍历即可，20min

代码

```python
# class tree:
    def __init__(self,x):
        self.val = x
        self.l = None
        self.r = None
def build_tree(postfix):
    stack = []
    for char in postfix:
        node = tree(char)
        if char.isupper():
            node.r = stack.pop()
            node.l = stack.pop()
        stack.append(node)
    return stack[0]

def level(root):
    queue = [root]
    t = []
    while queue:
        node = queue.pop(0)
        t.append(node.val)
        if node.l:
            queue.append(node.l)
        if node.r:
            queue.append(node.r)
    return t
n = int(input())
for _ in range(n):
    postfix = input().strip()
    root = build_tree(postfix)
    res= level(root)[::-1]
    print(''.join(res))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240324210744971](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240324210744971.png)



### 24750: 根据二叉树中后序序列建树

http://cs101.openjudge.cn/practice/24750/



思路：需要理解前序和中序中根节点的位置，然后递归处理即可解决，25min



代码

```python
# def build_tree(inorder,postorder):
    if not inorder or not postorder:
        return []
    root_val = postorder[-1]
    root_index = inorder.index(root_val)

    left_inorder = inorder[:root_index]
    right_inorder = inorder[root_index+1:]

    left_postorder = postorder[:len(left_inorder)]
    right_postorder = postorder[len(left_inorder):-1]

    root = [root_val]
    root.extend(build_tree(left_inorder,left_postorder))
    root.extend(build_tree(right_inorder,right_postorder))

    return root
inorder = input().strip()
postorder = input().strip()
preorder = build_tree(inorder, postorder)
print(''.join(preorder))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240324210944472](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240324210944472.png)



### 22158: 根据二叉树前中序序列建树

http://cs101.openjudge.cn/practice/22158/



思路：

与上一题类似。20min

代码

```python
class Tree:
    def __init__(self,x):
        self.val = x
        self.l = None
        self.r = None
def build_tree(pre,inn):
    if not pre or not inn:
        return None
    root_value = pre[0]
    root = Tree(root_value)
    root_index = inn.index(root_value)
    root.l = build_tree(pre[1:1+root_index],inn[:root_index])
    root.r = build_tree(pre[1+root_index:],inn[root_index+1:])
    return root

def post(root):
    if root is None:
        return
    post(root.l)
    post(root.r)
    print(root.val,end = '')


while 1:
    try:
        pre = input().strip()
        inn = input().strip()
        root = build_tree(pre,inn)
        post(root)
        print()
    except EOFError:
        break
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240324211011777](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240324211011777.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周作业依旧并保持对栈的高要求运用，同时引入了前中后序和层次遍历，最后两题说明了不仅要能正着写出遍历代码，而且需要

深入理解每种遍历顺序的特性，比如前序遍历根节点在第一个，中序遍历根节点分开两个子树等。

去力扣上写了一些二叉树的题目，感觉对二叉树的运用越来越顺了



