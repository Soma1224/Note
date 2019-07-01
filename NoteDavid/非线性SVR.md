# 非线性SVR





## 模型原型 

sklearn.svm.SVR(kernel=’rbf’,degree=3,gamma=’auto’,coef0=0.0,tol=0.001,C=1.0,epsilon=0.1,shrinking=True, cache_size=200,verbose=False,max_iter=-1) 

## 参数

### kernel

‘linear’， ‘poly’， ‘rbf’， ‘sigmoid’，‘precomputer’

### degree

### gamma  

gamma是选择RBF函数作为kernel后，该函数自带的一个参数。隐含地决定了数据映射到新的特征空间后的分布，gamma越大，支持向量越少，gamma值越小，支持向量越多。支持向量的个数影响训练与预测的速度。

### coef0

### tol

### C

### epsilon

### shrinking

### cache_size

### verbose

### max_iter



## 属性

### support_



### support_vectors_



### n_support_



### dual_coef_



### coef_



### intercept_



## 方法 

- fit(X,y) 
- predict(X) 
- score(X,y[,sample_weight])

