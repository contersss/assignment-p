# Assignment #1: 拉齐大家Python水平

Updated 0940 GMT+8 Feb 19, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）数算课程的先修课是计概，由于计概学习中可能使用了不同的编程语言，而数算课程要求Python语言，因此第一周作业练习Python编程。如果有同学坚持使用C/C++，也可以，但是建议也要会Python语言。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：win11

Python编程环境 PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/



思路：按题意复现即可

2min

##### 代码

```python
# n = int(input())
t = [0,1,1]
for i in range(28):
    t.append(t[-1]+t[-2]+t[-3])
print(t[n])

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240220142404366](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240220142404366.png)



### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A

5min

思路：正则表达式



##### 代码

```python
# import re
words = input()
pattern = r'.*h.*e.*l.*l.*o.*'
match = re.search(pattern, words)
if match and 1 <= len(words) <= 100:
    print("YES")
else:
    print("NO")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240220143638389](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240220143638389.png)



### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A

5min

思路：

一个个检查，如果是就删除，不是就小写加点

##### 代码

```python
# word = input()
word = word.lower()
lis = ['a','o','y','e','u','i']
for i in range(len(word)):
    if word[i] not in lis:
        print(".",word[i],end = '',sep = '')
    else:
        pass

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240220144017771](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240220144017771.png)



### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/

5min

思路：

欧拉筛

##### 代码

```
n = 10000
is_prime = [True] * (n + 1)
primes = []
for i in range(2, n + 1):
    if is_prime[i]:
         primes.append(i)
         for j in range(i * i, n + 1, i):
            is_prime[j] = False
is_prime[0] = False
is_prime[1] = False
m = int(input())
for i in range(2,n):
    if is_prime[i] and is_prime[m-i]:
        print(i,m-i)
        break
```

代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240220144721108](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240220144721108.png)



### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/

5min

思路：

多split几次

##### 代码

```python
# 
a = input()
for i in range(len(a)-1):
    if a[i] == '+' and a[i+1] == 'n':
        a = a[0:i+1] + '1' +a[i+1:]
    elif a[i] == 'n' and i == 0:
        a = '1' + a[0:]
num = list(a.split('+'))
maxx = 0 
dict = {}
for item in num:
    a,b = map(int,item.split("n^"))
    dict[a] = b
for i in dict.keys():
    if i != 0:
        maxx = max(maxx,dict[i])
print('n^',maxx,sep = '')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240220144832358](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240220144832358.png)



### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/

5min

思路：

使用数组存储每个编号的票数

##### 代码

```python
# n = [0 for i in range(100001)]
put = map(int,input().split())
for i in put:
    n[i] += 1
maxx = max(n)
res = []
for i in range(100001):
    if n[i] == maxx:
        res.append(i)
res.sort()
for i in res:
    print(i,end = ' ')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240220145346725](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240220145346725.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“数算pre每日选做”、CF、LeetCode、洛谷等网站题目。==

重温了上学期敲python的手感，再次练习了正则表达式的使用方法。这学期的内容上讲，学习了python中类的语法。
