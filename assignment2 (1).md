# Assignment #2: 编程练习

Updated 0953 GMT+8 Feb 24, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：win11

Python编程环境：PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 27653: Fraction类

http://cs101.openjudge.cn/2024sp_routine/27653/



思路：简单的类定义基础

5min

##### 代码

```python
# class Fraction:
    def __init__(self,top,bot):
        self.top = top
        self.bot = bot

    def show(self):
        print(self.top,"/",self.bot,sep = '')
    def __add__(self,other):
        newbot = self.bot*other.bot
        newtop = self.top*other.bot + self.bot*other.top
        s = self.gcd(newtop,newbot)

        return Fraction(newtop//s,newbot//s)
    @staticmethod
    def gcd(m,n):
        while m%n != 0:
            oldm = m
            oldn = n
            m = oldn
            n = oldm%oldn
        return n
c = list(map(int,(input().split())))
f1 = Fraction(c[0],c[1])
f2 = Fraction(c[2],c[3])
f3 = f1+f2
f3.show()

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240304144801693](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240304144801693.png)



### 04110: 圣诞老人的礼物-Santa Clau’s Gifts

greedy/dp, http://cs101.openjudge.cn/practice/04110

3min 做过

思路：

贪心，根据单位价值排序，然后逐个放入背包

##### 代码

```python
# 
a,v= map(int,input().split())
summ = 0
gift = []
for _ in range(a):
  b= map(int,input().split())  
  gift.append(tuple(b))
gift.sort(key = lambda x : x[0]/x[1],reverse = True)

for i in gift:
  if v >= i[1]:
    summ += i[0]
    v -= i[1]
  else:
    summ += i[0] *(v/i[1])
    break
print('%.1f'%(summ))
```



代码运行截图 ==（至少包含有"Accepted"）==





### 18182: 打怪兽

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

3min做过

思路：使用字典代替列表存储，避免爆内存的问题



##### 代码

```python
# 
a = int(input())
for _ in range(a):
    n,m,b = map(int,input().split())
    dict1 = {}
    h = True
    for __ in range(n):
        ti,xi = map(int,input().split())
        if ti in dict1.keys():
            dict1[ti].append(xi)
        else:
            dict1[ti] = [xi]
    p = max(dict1.keys())
    for i in dict1.keys():
        dict1[i].sort()
    lis = list(sorted(dict1.keys()))
    for ii in lis:
        b -= sum(dict1[ii][max(0,len(dict1[ii])-m):])
        if b<= 0:
            h = False
            break
    if h:
        print('alive')
    else:
        print(ii)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227172439598](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240227172439598.png)



### 230B. T-primes

binary search/implementation/math/number theory, 1300, http://codeforces.com/problemset/problem/230/B

3min做过

思路：欧拉筛+真值表



##### 代码

```python
# import math
 
def tprime(aa, arr,aaa):
    res = [False] * (10000000)
    prime = set()
 
    for i in range(2, int(math.sqrt(aa)) + 1):
        if not res[i]:
            if aaa<=i * i <=aa:
                prime.add(i * i)
 
            for j in range(i * i, int(math.sqrt(aa) + 1), i):
                res[j] = True
 
    for h in arr:
        if h in prime:
            print("YES")
        else:
            print("NO")
 
a = int(input())
arr = list(map(int, input().split()))
 
tprime(max(arr), arr,min(arr))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227172314978](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240227172314978.png)



### 1364A. XXXXX

brute force/data structures/number theory/two pointers, 1200, https://codeforces.com/problemset/problem/1364/A

3min做过

思路：维护四个变量

##### 代码

```python
# a = int(input())
for _ in range(a):
    b,hate = map(int,input().split())
    arr = list(map(int,input().split()))
    maxl = 0
    maxr = 0
    suml = 0
    sumr = 0
    for num in range(0,len(arr)):
        suml += arr[num]
        if suml % hate != 0:
           maxl = max(maxl,num+1)
    for numr in range(len(arr)-1,-1,-1):
        sumr += arr[numr]
        if sumr % hate != 0:
           maxr = max(maxr,len(arr)-numr)
    if maxr != 0 or maxl != 0:
        print(max(maxl,maxr))
    else:
        print(-1)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img src="C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240227172208843.png" alt="image-20240227172208843" style="zoom:80%;" />



### 18176: 2050年成绩计算

http://cs101.openjudge.cn/practice/18176/



思路：欧拉筛

3min做过

##### 代码

```python
# import math
zhii = [True for i in range(10001)]
for i in range(2,100):
    if zhii[i]:
        for ii in range(i*2,10001,i):
            zhii[ii] = False


a,b = map(int,input().split())
for _ in range(a):
    summ = 0
    score = list(map(int,input().split()))
    for s in score:
        if s**0.5 - (s**0.5)//1 != 0:
            continue
        if zhii[int(s**0.5)]:
            summ += s
    if summ == 0:
        print(0)
    else:
        print('%.2f' %(summ/len(score)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240227171841328](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240227171841328.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

作业大部分都是 上学期做过的，现在主要在洛谷和力扣上做一些简单的链表和树的题目。



