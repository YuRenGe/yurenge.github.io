---
layout: post
title: KNN算法简单实现!
subheading: 
author: Dongfang Z
categories: KNN
banner:
  video: 
  loop: true
  volume: 0.8
  start_at: 8.5
  image: https://bit.ly/3xTmdUP
  opacity: 0.618
  background: "#000"
  height: "100vh"
  min_height: "38vh"
  heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
  subheading_style: "color: gold"
tags: KNN code
sidebar: []
---

```python
import pandas as pd
```

这里是用的是在机器学习教学中非常常用的种子数据，该数据集也会放在该博客中


```python
seed_dataset = pd.read_excel("../Datasets/seed.csv")
```


```python
seed_dataset
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>area</th>
      <th>perimeter</th>
      <th>compactness</th>
      <th>length of kernel</th>
      <th>width of kernel</th>
      <th>asymmetry coefficient</th>
      <th>length of kernel groove</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.26</td>
      <td>14.84</td>
      <td>0.8710</td>
      <td>5.763</td>
      <td>3.312</td>
      <td>2.221</td>
      <td>5.220</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14.88</td>
      <td>14.57</td>
      <td>0.8811</td>
      <td>5.554</td>
      <td>3.333</td>
      <td>1.018</td>
      <td>4.956</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.29</td>
      <td>14.09</td>
      <td>0.9050</td>
      <td>5.291</td>
      <td>3.337</td>
      <td>2.699</td>
      <td>4.825</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13.84</td>
      <td>13.94</td>
      <td>0.8955</td>
      <td>5.324</td>
      <td>3.379</td>
      <td>2.259</td>
      <td>4.805</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.14</td>
      <td>14.99</td>
      <td>0.9034</td>
      <td>5.658</td>
      <td>3.562</td>
      <td>1.355</td>
      <td>5.175</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>205</th>
      <td>12.19</td>
      <td>13.20</td>
      <td>0.8783</td>
      <td>5.137</td>
      <td>2.981</td>
      <td>3.631</td>
      <td>4.870</td>
      <td>3</td>
    </tr>
    <tr>
      <th>206</th>
      <td>11.23</td>
      <td>12.88</td>
      <td>0.8511</td>
      <td>5.140</td>
      <td>2.795</td>
      <td>4.325</td>
      <td>5.003</td>
      <td>3</td>
    </tr>
    <tr>
      <th>207</th>
      <td>13.20</td>
      <td>13.66</td>
      <td>0.8883</td>
      <td>5.236</td>
      <td>3.232</td>
      <td>8.315</td>
      <td>5.056</td>
      <td>3</td>
    </tr>
    <tr>
      <th>208</th>
      <td>11.84</td>
      <td>13.21</td>
      <td>0.8521</td>
      <td>5.175</td>
      <td>2.836</td>
      <td>3.598</td>
      <td>5.044</td>
      <td>3</td>
    </tr>
    <tr>
      <th>209</th>
      <td>12.30</td>
      <td>13.34</td>
      <td>0.8684</td>
      <td>5.243</td>
      <td>2.974</td>
      <td>5.637</td>
      <td>5.063</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
<p>210 rows × 8 columns</p>
</div>



将数据分为特征部分和标签部分


```python
features = seed_dataset.iloc[:,:-1].values
labels = seed_dataset.iloc[:,7].values
```


```python
features
```
    array([[15.26  , 14.84  ,  0.871 , ...,  3.312 ,  2.221 ,  5.22  ],
           [14.88  , 14.57  ,  0.8811, ...,  3.333 ,  1.018 ,  4.956 ],
           [14.29  , 14.09  ,  0.905 , ...,  3.337 ,  2.699 ,  4.825 ],
           ...,
           [13.2   , 13.66  ,  0.8883, ...,  3.232 ,  8.315 ,  5.056 ],
           [11.84  , 13.21  ,  0.8521, ...,  2.836 ,  3.598 ,  5.044 ],
           [12.3   , 13.34  ,  0.8684, ...,  2.974 ,  5.637 ,  5.063 ]])

```python
labels
```
    array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
           1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
           1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
           1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
           2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
           2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
           2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3,
           3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3,
           3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3,
           3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3], dtype=int64)

使用不同k值查看其预测准确性
```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection  import cross_val_score
k_range = range(1, 31)
k_error = []
for k in k_range:
    knn = KNeighborsClassifier(n_neighbors=k, p=2, metric="minkowski")
    scores = cross_val_score(knn, features, labels, cv=6, scoring='accuracy')
    knn.fit(features, labels)
    k_error.append(1 - scores.mean())
```


```python
import matplotlib.pyplot as plt
plt.plot(k_range, k_error)
plt.xlabel('Value of K for KNN')
plt.ylabel('Error')
plt.show()
```


​    
![png](output_11_0.png)
​    


由上图可知，当K=11时，预测的准确性最高


```python
knn = KNeighborsClassifier(n_neighbors=11,p=2, metric="minkowski")
knn.fit(features,pred)
```




    KNeighborsClassifier(n_neighbors=11)




```python
predict_name = ["aaa", "bbb", "ccc"]
ret = knn.predict([[13,13,0.9,6,3.232,1.355,4.825]])
print(predict_name[ret[0] - 1])
```

    aaa

