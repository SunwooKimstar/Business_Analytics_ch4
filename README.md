# Business_Analytics_ch4

# **Ensemble Learning**

## ๐ Contents
-----------------------------
* Background
* Steps
* Dataset
* Hyper-parameter search
* Stump tree์ ๊ฐฏ์์ ๋ฐ๋ฅธ ์ฑ๋ฅ ๋ณํ
* Result

### :pushpin: Background 
-----------------------------

* AdaBoost
- classifier์ accuracy๋ฅผ ํฅ์์ํค๊ธฐ ์ํด ๋ค์์ weak classifier๋ฅผ ๊ฒฐํฉ์ํด 
- weak classifier(learner) : ๋๋ค ๋ชจ๋ธ์ ๋นํด ์ฝ๊ฐ์ ์ฑ๋ฅ ํฅ์์ด ์๋ ๋ชจ๋ธ 
- ์ค๋ฅ ๋ฐ์ดํฐ์ ๊ฐ์ค์น๋ฅผ ๋ถ์ฌํ๋ฉฐ boosting์ ์ํํ๋ ๋ํ์  ์๊ณ ๋ฆฌ์ฆ
- AdaBoost๋ ๋ค์์ weighted training

<p align="center">
    <img src="./imgs/ensemble/adaboost2.png" width = "40%" height = "40%">
</p>


### :pushpin: Steps 
-----------------------------
* Step 1 : ๋ฐ์ดํฐ์ ์์ฑ ๋๋ ๋ถ๋ฌ์ค๊ธฐ
* Step 2 : Model fit (AdaBoostClassifier ์์ฑ)
* Step 3 : ๊ฒฐ๊ณผ๊ฐ ์์ธก
* (Step 4 : ๊ฒฐ๊ณผ ์๊ฐํ)

### :pushpin: Dataset 
-----------------------------
* make_classification ํจ์ ์ด์ฉํ์ฌ ์์์ ๋ฐ์ดํฐ์ ์์ฑ
* Email Spam Classification Dataset (csv) [download](https://www.kaggle.com/datasets/balaka18/email-spam-classification-dataset-csv)
* breast_cancer 

### ๐ **[์ฌํ๊ณผ์ ] Hyperparameter Search**
---------
1. **base_estimator** : ensemble์ ํ  model. ํ์ต์ ์ฌ์ฉํ๋ ์๊ณ ๋ฆฌ์ฆ
2. **n_estimators** : ์์ฑํ  ์ฝํ ํ์ต๊ธฐ ๊ฐฏ์ ์ง์  (default = 50)
3. **learning_rate** : ํ์ต์ ์งํํ  ๋๋ง๋ค ์ ์ฉํ๋ ํ์ต๋ฅ (0~1)/weak learner๊ฐ ์์ฐจ์ ์ผ๋ก ์ค๋ฅ๊ฐ์ ๋ณด์ ํด๋๊ฐ ๋ ์ ์ฉํ๋ ๊ณ์ (default = 1.0)
4. **random_state** : ์คํ์ ๋์ผํ ๋๋ค ์ซ์๊ฐ์ด ๋์ค๋๋ก ์ค์ 
  - **max_feature** : ๊ฐ๊ฐ์ base estimator์์ ์ถ์ถํ๋ feature ์

### ๐ณ **[์ฌํ๊ณผ์ ]** Stump tree์ ๊ฐฏ์์ ๋ฐ๋ฅธ ์ฑ๋ฅ ๋ณํ
-------
* ์ด๋ฒ์๋ stump tree์ ๊ฐฏ์๊ฐ ๋ฌ๋ผ์ง์ ๋ฐ๋ผ ์ด๋ป๊ฒ ์ฑ๋ฅ ๋ณํ๊ฐ ์ผ์ด๋๋์ง ์ดํด๋ณด๋๋ก ํ๊ฒ ์ต๋๋ค.
> #### stump tree๋?
decision tree์์ 1๊ฐ์ node์ 2๊ฐ์ leaf๋ฅผ ๊ฐ์ง๋ ๋ชจ์์ ์๋ฏธํฉ๋๋ค. stump๋ 1๊ฐ์ node๋ฅผ ๊ฐ์ง๊ธฐ์ ์ค์ง ํ๋์ ๋ณ์๋ง์ ์ฌ์ฉํ๋ค๊ณ  ๋ณผ ์ ์์ผ๋ฉฐ _weak learner_ ๋ผ๊ณ  ํ  ์ ์์ต๋๋ค.

<p align="center">
    <img src="./imgs/ensemble/stump1.jpg" width = "50%" height = "50%">
</p>

AdaBoost๋ ๊ฐ ํธ๋ฆฌ๋ณ ์ค์๋์ ์์ด ์ฐจ์ด๊ฐ ๋๋ค๋ ํน์ง์ด ์์ต๋๋ค. ํ๋จ์ ๊ทธ๋ฆผ์ ์ฐธ๊ณ ํ์ฌ ๋ณด์๋ฉด ๊ฐ stump์ ํฌ๊ธฐ๊ฐ ๋ค๋ฅธ ๊ฒ์ ํ์ธํ  ์ ์๊ณ , boosting์ ํน์ง์ ๋ฐ๋ผ ์ด์  stump์ ์ ๋ณด๋ฅผ ์ฐธ๊ณ ํ๋ฉฐ ์ข์์ ์ด๊ณ  sequentialํ๊ฒ ๋ชจ๋ธ์ ์์ฑํ๊ฒ ๋ฉ๋๋ค.

<p align="center">
    <img src="./imgs/ensemble/stump2.jpg" width = "50%" height = "50%">
</p>

### [Result] 
-----------------------------
* make_classification
<p align="center">
    <img src="./imgs/ensemble/img0.png" width = "50%" height = "50%">
</p>
ํด๋น ๊ฒฐ๊ณผ์์ 1์ ๋ชจ๋ ์ ๋ถ๋ฅ๊ฐ ๋์์ง๋ง, ์ผ๋ถ 0๋ผ๋ฒจ์ ํด๋น๋๋ ๋ฐ์ดํฐ๋ ์ ๋ถ๋ฆฌ๋์ง ๋ชปํ ๋ชจ์ต์ ํ์ธํ  ์ ์์์ต๋๋ค.

* Email Spam Classification
<p align="center">
    <img src="./imgs/ensemble/img1.png" width = "50%" height = "50%">
</p>

* Hyper-parameter search
<p align="center">
    <img src="./imgs/ensemble/img2.png" width = "50%" height = "50%">
</p>
n_estimator๊ฐ 100์ธ ๊ฒฝ์ฐ๋ฅผ ์ ์ธํ 3๊ฐ์ง ๊ฒฝ์ฐ learning rate๊ฐ ์ฆ๊ฐํจ์ ๋ฐ๋ผ ์ฑ๋ฅ ํฅ์์ด ์์์ ํ์ธํ  ์ ์์์ต๋๋ค. ์ถ๊ฐ์ ์ผ๋ก n_estimator๊ฐ 256์ธ ๊ฒฝ์ฐ ๊ฐ์ฅ ์ฑ๋ฅ ๋ณํํญ์ด ๋๋๋ฌ์ง์ ํ์ธํ  ์ ์์์ต๋๋ค. learning_rate๋ฅผ ์ค์ธ๋ค๋ฉด ๊ฐ์ค์น ๊ฐฑ์ ์ ๋ณ๋ํญ์ด ๊ฐ์ํด์ ์ฌ๋ฌ ํ์ต๊ธฐ๋ค์ decision boundary ์ฐจ์ด๊ฐ ์ค์ด๋ค๋ฉฐ ์ฑ๋ฅ์ด ํ๋ฝํ๋ค๊ณ  ์ถ๊ฐ์ ์ธ ํด์์ ํด๋ณผ ์ ์์ต๋๋ค.

<p align="center">
    <img src="./imgs/ensemble/img3.png" width = "50%" height = "50%">
</p>
learning_rate๊ฐ 0.5์ธ ๊ฒฝ์ฐ n_estimator๊ฐ ์ฆ๊ฐํจ์ ๋ฐ๋ผ ์ฑ๋ฅ ํฅ์์ด ์์์ ํ์ธํ  ์ ์์์ต๋๋ค. ์ด์๋ ๋ฐ๋๋ก ๋ค๋ฅธ ๊ฒฝ์ฐ์๋ ์ค๊ฐ n_estimator์ ํด๋น๋  ๋ ์ฑ๋ฅ์ด ๊ฐ์ฅ ๋์ ๋ชจ์ต์ ํ์ธํ  ์ ์์์ต๋๋ค. n_estimators๋ฅผ ๋๋ฆฐ๋ค๋ฉด ์์ฑํ๋ weak learner์ ์ ์ฆ๊ฐํ๊ณ , ๋ณต์กํ decision boundary๋ฅผ ์์ฑํ๊ฒ ๋๋ฉฐ ๋ชจ๋ธ์ด ๋ณต์กํด์ง๋ค๋ ์ ์ ๊ณ ๋ คํด๋ณด๋ฉด ์์ ๊ฐ์ ์ฑ๋ฅ ๋ณํ ๊ฒฐ๊ณผ์ ํด์์ด ๊ฐ๋ฅํฉ๋๋ค.

* Stump tree์ ๊ฐฏ์์ ๋ฐ๋ฅธ ์ฑ๋ฅ ๋ณํ

|**Stump**|1|5|10|100|1000|
|:--:|:--:|:--:|:--:|:--:|:--:|
|**Accuracy**|0.895|0.959|0.971|0.982|0.977|

### **๐ฒ AdaBoost์ ์ฅ๋จ์ **
------

- **์ฅ์ **
    * overfitting์ ๋น๊ต์  ๋ ์ทจ์ฝํจ
    * bias์ variance๋ฅผ ์ค์ด๋๋ฐ ๋์์ ์ค
    * ํด๋น ๋ฐฉ๋ฒ๋ก ์ ํตํด weak classifier์ accuracy๊ฐ ํฅ์๋  ์ ์์
    * ์ฌ์ฉ์ด ๋น๊ต์  ์ฌ์
- **๋จ์ **
    * ์์ง์ ๋ฐ์ดํฐ์์ด ํ์ํจ
    * outlier์ noise์ ๋ฏผ๊ฐํจ
    * XGBoost๋ณด๋ค ๋๋ฆฐ ์๋

### ๐ References
------------------------------
* https://github.com/pilsung-kang/Business-Analytics-IME654-
