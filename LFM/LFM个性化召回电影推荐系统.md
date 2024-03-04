### LFM算法（隐语义模型）
本质：矩阵分解

- 训练模型时，可以基于标签内容来提取物品特征，也可以让模型去发掘物品的潜在特征，这样模型称为隐语义模型（LFM）。
- 通过矩阵分解进行降维分析（偏好数据是稀疏的，需要对原始数据做降维处理，分解之后的矩阵，也代表了用户和物品的隐藏特征）

$$
p(u,i)=p_u^Tq_i=\sum_{f=1}^F{p_{uf}q_{if}}
$$
$ p_u $：用户向量    $q_i$：物品向量     $f$：隐特征
LFM loss function:
$$
loss=\sum_{(u,i)\in{D}}{(p(u,i)-p^{LFM}(u,i))^2}
$$

$$
loss=\sum_{(u,i)\in{D}}{({{p(u,i)-\sum_{f=1}^F{p_{uf}q_{if}}})}^2}+\alpha|p_u|^2+\alpha|q_i|^2
$$

#### LFM算法迭代

$$
\frac{\partial loss}{\partial p_{uf}}=-2(p(u,i)-p^{LFM}(u,i))q_{if}+2\alpha p_{uf}
$$

$$
p_{uf}=p_{uf}-\beta \frac{\partial loss}{\partial p_{uf}}
$$

$$
\frac{\partial loss}{\partial q_{if}}=-2(p(u,i)-p^{LFM}(u,i))p_{uf}+2\alpha q_{if}
$$

$$
q_{if}=q_{if}-\beta \frac{\partial loss}{\partial q_{if}}
$$



##### 模型的求解算法_——_ALS交替最小二乘法

<img src="C:\Users\56234\AppData\Roaming\Typora\typora-user-images\image-20240228202024711.png" alt="image-20240228202024711" style="zoom:67%;" />
