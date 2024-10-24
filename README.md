## 牛客2024年1024程序员节娱乐赛题解（Player: WhkSoft）

# A. LLM

直接输出`YES`或者`NO`即可

# B. 猜数字

题目中提到它会随着时间的流逝而**线性增加**，此处可以联想到10位时间戳与13位时间戳。  
此时输出毫秒级时间戳会导致`答案错误`(太大了) 
输出秒级时间戳会提示`格式错误`(太小了)。  
尝试添加偏移值，可以尝试二分法找这个`offset`，最终得出`offset=1024`。  
于是输出`time.time()+1024`即可AC

# C. 诗之美

题目描述如下  
`诗甚美美于其词如边城柳之首美于其题如过零丁洋美于其调如平平仄仄美于其式如起承转合`

加上标点符号，就是：
```
诗甚美，
美于其词，
如《边城柳》之首。
美于其题，
如《过零丁洋》。
美于其调，
如平平仄仄。
美于其式，
如起承转合。
```

《边城柳》之首，第一句话就是`一株新柳色`，第一位数就是`1`。  
《过**零**丁洋》中有一个数字`0`，第二位数就是`0`。  
`平平仄仄` 有2个不同的汉字，第三位数就是`2`。  
`起承转合` 有4个不同的汉字，第四位数就是`4`。

答案就是`1024`

# D. 十七倍的牛牛

根据里面的C++代码，逆一下就行，每个数除以17，然后转ASCII，得到`flag{welcome_to_the_Nowcoder_1O24}`

# E. 赛博抽卡

首先，判题的计算器会计算 1024/(a+b+c+d) 次，为了能尽快AC，我们可以让分母的和最小，此处直接给出一个AC率高的答案：  
`1 2 9 10 <<`

# F. Enchant

题目上面是银河标准字母，转过来是：
```
please output the binary representation
of the square of a000290(x).
```

A000290 指的是完全平方，详细可看OEIS。

输出x的四次方就行。

# G. 昨日重现

$$
\begin{bmatrix}
F_{n+1} & F_{n} \\
F_{n} & F_{n-1}
\end{bmatrix}
= 
\begin{bmatrix}
1 & 1 \\
1 & 0
\end{bmatrix}^n
=
\underbrace{
\begin{bmatrix}


1 & 1 \\
1 & 0
\end{bmatrix}
\cdots
\begin{bmatrix}
1 & 1 \\
1 & 0
\end{bmatrix}
}_{n \text{ times}}.
$$

这是斐波那契数列用矩阵表示的递推关系，算矩阵乘法与快速幂即可，记得处理n=0与n=1的情况，时间复杂度O(log n)

代码参考(python)
```python
def matrix_mult(A, B, mod):
    return [
        [
            (A[0][0] * B[0][0] + A[0][1] * B[1][0]) % mod,
            (A[0][0] * B[0][1] + A[0][1] * B[1][1]) % mod
        ],
        [
            (A[1][0] * B[0][0] + A[1][1] * B[1][0]) % mod,
            (A[1][0] * B[0][1] + A[1][1] * B[1][1]) % mod
        ]
    ]

def matrix_pow(mat, exp, mod):
    res = [[1, 0], [0, 1]]
    base = mat
    
    while exp > 0:
        if exp % 2 == 1:
            res = matrix_mult(res, base, mod)
        base = matrix_mult(base, base, mod)
        exp //= 2
        
    return res

def fibonacci(n, mod):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    
    F = [[1, 1], [1, 0]]
    result = matrix_pow(F, n - 1, mod)
    return result[0][0]

inputs = []
while True:
    n = int(input().strip())
    if n == -1:
        break
    inputs.append(n)

mod = 10**3

for n in inputs:
    print(fibonacci(n, mod))
```

# H. 小苯的括号计数


没写完呢，别急

# I. 字符串与渲染

# J. KNN