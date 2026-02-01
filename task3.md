## 3.2 多元回归分析

**模型1：评委分数影响因素**

$$S_{i,t} = \alpha_0 + \alpha_1 Age_i + \alpha_2 1_{Industry} + \alpha_3 Partner_i + \alpha_4 Week_t + \varepsilon_{i,t}$$

**模型2：观众投票影响因素**（使用对数变换处理偏态分布）

$$\log(V_{i,t}) = \beta_0 + \beta_1 S_{i,t} + \beta_2 Age_i + \beta_3 1_{Industry} + \beta_4 Partner_i + \beta_5 Week_t + u_{i,t}$$

**模型3：最终排名影响因素**

$$Placement_i = \gamma_0 + \gamma_1 \bar{S}_i + \gamma_2 Age_i + \gamma_3 1_{Industry} + \gamma_4 Partner_i + \eta_i$$

其中 $\bar{S}_i = \frac{1}{T_i} \sum_{t=1}^{T_i} S_{i,t}$ 是平均评委分数。

![image-20260201133046727](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260201133046727.png)

------

## 3.3 舞者效应分析

**固定效应模型：**

$$Y_{i,t} = X_{i,t}'\beta + \alpha_{partner_i} + \varepsilon_{i,t}$$

其中 $\alpha_{partner_i}$ 是舞者固定效应。

**舞者排名：**

根据固定效应系数 $\hat{\alpha}_{partner}$ 对舞者排名：

$$\text{Partner Rank} = \text{rank}(\hat{\alpha}_{partner})$$

**方差分解与占比计算：**

$$\text{Total Var}(Y) = \text{Var}(X'\beta) + \text{Var}(\alpha_{partner}) + \text{Var}(\varepsilon)$$

![Code_Generated_Image (1)](/Users/yangxiaomao/Downloads/Code_Generated_Image (1).png)

------

## 3.4 明星特征影响分析

### 年龄效应

1. **线性效应：** $\frac{\partial Y}{\partial Age} = \beta_{age}$
2. **非线性效应（二次项）：** $Y = \beta_0 + \beta_1 Age + \beta_2 Age^2 + \dots$
3. **最优年龄：** $Age^* = -\frac{\beta_1}{2\beta_2}$

### 职业类别与交互效应

- **职业类别（虚拟变量）：** $Y = \beta_0 + \sum_{k=1}^K \beta_k 1_{Industry_k} + \dots$
- **交互效应：** $Y = \beta_0 + \beta_1 Age + \beta_2 1_{Athlete} + \beta_3 (Age \times 1_{Athlete}) + \dots$

![image-20260201133822428](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260201133822428.png)

![image-20260201133838346](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260201133838346.png)

------

## 3.5 差异性检验

**评委 vs 观众偏好差异：**

- **检验假设：**
  - $H_0: \beta^{Judge} = \beta^{Fan}$
  - $H_1: \beta^{Judge} \neq \beta^{Fan}$
- **方法：** 使用 **Chow 检验** 或 **似然比检验**。