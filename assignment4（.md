# Assignment #4: 排序、栈、队列和树

Updated 0005 GMT+8 March 11, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：win11

Python编程环境：PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



思路：按题目要求实现即可

10min

代码

```python
# from collections import deque
t = int(input())
for _ in range(t):
    n = int(input())
    lis = deque()
    for __ in range(n):
        a,b = map(int,input().split())
        if a == 1:
            lis.append(b)
        elif a == 2:
            if b == 0:
                lis.popleft()
            else:
                lis.pop()
    if len(lis) != 0:
        for i in lis:
            print(i,end = ' ')
        print()
    else:
        print("NULL")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240317091002641](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240317091002641.png)



### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/



思路：使用栈，中间那段判断是否为数字写的过于复杂了，可以写一个包含运算符的列表，然后用in语法即可判断

15min

代码

```python
# lis = list(input().split())
stack = []
for i in lis:
    stack.append(i)
    if len(stack) >= 2:
        if ((stack[-1].replace('.','0')).isdigit() and (stack[-2].replace('.','0')).isdigit()) or ((stack[-2][0] == '-' and len(stack[-2]) != 1) and ((stack[-1].replace('.','0')).isdigit())) or ((stack[-1][0] == '-' and len(stack[-1]) != 1) and (stack[-2].replace('.','0')).isdigit()) or ((stack[-1][0] == '-' and len(stack[-1]) != 1) and (stack[-2][0] == '-' and len(stack[-2]) != 1)):
            while  ((stack[-1].replace('.','0')).isdigit() and (stack[-2].replace('.','0')).isdigit()) or ((stack[-2][0] == '-' and len(stack[-2]) != 1) and ((stack[-1].replace('.','0')).isdigit())) or ((stack[-1][0] == '-' and len(stack[-1]) != 1) and (stack[-2].replace('.','0')).isdigit()) or ((stack[-1][0] == '-' and len(stack[-1]) != 1) and (stack[-2][0] == '-' and len(stack[-2]) != 1)):
                b = stack.pop();a = stack.pop()
                if stack[-1] == "+":
                    stack.pop()
                    stack.append(str(float(a)+float(b)))
                elif stack[-1] == "-":
                    stack.pop()
                    stack.append(str(float(a)-float(b)))
                elif stack[-1] == "*":
                    stack.pop()
                    stack.append(str(float(a)*float(b)))
                elif stack[-1] == "/":
                    stack.pop()
                    stack.append(str(float(a)/float(b)))
                if len(stack) == 1:
                    break
print('%.6f'%(float(stack[0])))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240317091021665](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240317091021665.png)



### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/

30min

思路：按照题解思路写的，建立两个栈，一个运算符一个数字，然后按照加减乘除和括号的优先顺序依次pop



代码

```python
# 
def infix_to_postfix(expression):
    precedence = {'+':1, '-':1, '*':2, '/':2}
    stack = []
    postfix = []
    number = ''

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

    if number:
        num = float(number)
        postfix.append(int(num) if num.is_integer() else num)

    while stack:
        postfix.append(stack.pop())

    return ' '.join(str(x) for x in postfix)

n = int(input())
for _ in range(n):
    expression = input()
    print(infix_to_postfix(expression))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240317091251126](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240317091251126.png)



### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/

20min

思路：依旧是栈的题目，思路是依次比对原始序列和目标序列的最前一个元素是否相同，如不相同则继续压栈



代码

```python
# def is_valid_pop_sequence(origin, output):
    if len(origin) != len(output):
        return False 

    stack = []
    bank = list(origin)
    
    for char in output:
        while (not stack or stack[-1] != char) and bank:
            stack.append(bank.pop(0))
       
        if not stack or stack[-1] != char:
            return False
        
        stack.pop() 
    
    return True  
origin = input().strip()

while True:
    try:
        output = input().strip()
        if is_valid_pop_sequence(origin, output):
            print('YES')
        else:
            print('NO')
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240317091308629](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240317091308629.png)



### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



思路：二叉树的基本语法，主要难点在于如何建立二叉树

15min

代码

```python
# 
class tree:
    def __init__(self,x):
        self.val = x
        self.l = None
        self.r = None

def build_tree(node):
    nodes = {i:tree(i) for i in range(1,len(node) + 1)}
    for i,(l,r) in enumerate(node,1):
         if l != -1:
             nodes[i].l = nodes[l]
         if r != -1:
             nodes[i].r = nodes[r]
    return nodes[1]
def maxx(root):
    if root is None:
        return 0
    else:
        ld = maxx(root.l)
        rd = maxx(root.r)
        return max(ld,rd)+1

n = int(input())
node = []
for _ in range(n):
    l,r = map(int,input().split())
    node.append([l,r])
root = build_tree(node)
res = maxx(root)
print(res)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240317091457334](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240317091457334.png)



### 02299: Ultra-QuickSort

http://cs101.openjudge.cn/practice/02299/



思路：求逆序数+归并优化时间复杂度



代码

```python
# 
def merge(l1, l2):
    i, j = 0, 0
    res, inv = [], 0
    length1, length2 = len(l1), len(l2)
    while i < length1 and j < length2:
        if l1[i] <= l2[j]:
            res.append(l1[i])
            i += 1
        else:
            res.append(l2[j])
            j += 1
            inv += length1 - i
    if i < len(l1):
        res.extend(l1[i:])
    else:
        res.extend(l2[j:])
    return res, inv

def inversions(l :list):
    if len(l) <= 1:
        return l, 0
    elif len(l) == 2:
        return [min(l), max(l)], 0 if l[0]<=l[1] else 1
    mid = len(l) // 2
    left,a=inversions(l[:mid])
    right,b=inversions(l[mid:])
    r, inv = merge(left, right)
    return r, inv + a + b

while 1:
    n = int(input())
    if n == 0:
        break
    lis = []
    for _ in range(n):
        lis.append(int(input()))
    minn = 0
    res,a = inversions(lis)
    print(a)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240317091550499](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240317091550499.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周作业难度明显上升，对栈的灵活运用显得尤为重要。其次是二叉树不同题目给出的数据格式不同，要考虑在不同方法下建立二叉树。

本周搞懂课内知识花费时间较多，暂时没有别的练习题目



