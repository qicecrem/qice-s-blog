
### 一、问题描述
#### 1. 问题背景

#### 2. 输入与输出
- **输入**：矩阵序列的维度数组 \( \text{dim} = [d_0, d_1, d_2, \dots, d_n] \)，其中 \( d_i \) 表示第 \( i \) 个矩阵的行数，\( d_{i+1} \) 表示第 \( i \) 个矩阵的列数（共 \( n \) 个矩阵）。  
- **输出**：计算所有矩阵连乘的最小乘法次数，以及最优括号化方案（可选）。



### 四、代码框架（Python）
```python
def matrix_chain_order(dim):
    n = len(dim) - 1  # 矩阵个数
    dp = [[0] * (n + 1) for _ in range(n + 1)]  # dp[i][j] 存储最小次数
    split = [[0] * (n + 1) for _ in range(n + 1)]  # 存储拆分点
    
    # 按链长度递增计算
    for L in range(2, n + 1):  # L为链长度（2到n）
        for i in range(1, n - L + 2):
            j = i + L - 1
            dp[i][j] = float('inf')
            for k in range(i, j):
                cost = dp[i][k] + dp[k+1][j] + dim[i-1] * dim[k] * dim[j]
                if cost < dp[i][j]:
                    dp[i][j] = cost
                    split[i][j] = k
    
    # 输出最优括号化方案（递归函数）
    def print_parenthesis(i, j):
        if i == j:
            print(f"A{i}", end="")
        else:
            k = split[i][j]
            print("(", end="")
            print_parenthesis(i, k)
            print_parenthesis(k+1, j)
            print(")", end="")
    
    print("最优括号化方案：", end="")
    print_parenthesis(1, n)
    print("\n最小乘法次数：", dp[1][n])
    return dp[1][n]

# 示例调用
dim = [10, 20, 30, 40]
matrix_chain_order(dim)
```

### 五、总结
动态规划通过将矩阵连乘问题拆解为重叠子问题，利用表格存储中间结果避免重复计算，从而高效求解最优解。其核心在于合理定义状态、状态转移方程及计算顺序，适用于具有最优子结构和重叠子问题的场景。