---
layout: post
title: Kernel Fisher Discriminant Analysis
date: 2018-11-20
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>


## Kernel Fisher Discriminant Analysis

고려대학교 Business Analytics 강의 내용 중 Kernel Fisher Discriminant Analysis 에 대해 정리했습니다.

### Linear Discriminant Analysis

Linear Discriminant Analysis, 즉 LDA는 projection 후 두 class를 가장 잘 분리하는 projection 축을 찾는 것입니다. Projection이란 말에서 알 수 있듯, LDA는 고차원의 데이터를 저차원의 데이터로 차원축소하는 것도 포함하고 있습니다.

데이터 공간 상의 한 점 x를 project한 뒤 다음과 같이 나타낼 수 있습니다.

$$y=w^{\mathsf{T}}x$$





데이터 공간 상의 각 점들이 projection 평면 위에 표현되면 다음과 같이 나타납니다

![Alt text](https://github.com/Suhee05/Suhee05.github.io/blob/master/images/lda.jpg?raw=true)

이 때, 우리의 목적은 분류를 해내는 것이므로 왼쪽과 같은 그림은 목적에 비추어 생각해보면 바람직하지 않습니다. Projection 후를 기준으로 삼아 분류를 해내기 위해서 두 가지 기준을 생각해볼 수 있습니다. "between class variance" 와 "within class variance" 가 그 두 가지입니다. 첫번째 between class variance는 두 class 가 얼마나 멀리 떨어져 있는지에 대한 지표입니다. 두번째 within class variance는 한 class의 샘플들이 서로 얼마나 가까이 밀집해있는지에 대한 지표입니다. between class variance가 커질수록 두 class는 멀리 떨어지게 될 것이고, within class variance가 작아질수록 한 class 에 속한 sample 들은 가까이 모이게 될 것입니다. 따라서 '분류'라는 목적을 생각해보면 between class variance를 크게 하고, within class variance를 작게 해야한다는 것을 알 수 있습니다. 이에 따라 우리의 목적함수를 나타내면 다음과 같습니다.

$$J(w) = \frac{w^{\mathsf{T}}S_{b}w}{w^{\mathsf{T}}S_{w}w}$$

\(S_{b}\) 와 \(S_{w}\) 는 각각 between class, within class 의 covariance matrix 입니다.


<script type="math/tex; mode=display">S_b =(m_1 - m_2)(m_1 - m_2)^T 
</script>
<script type="math/tex; mode=display">S_w = \sum (X_n - m_1)(X_n - m_1)^T</script>



### Kernel Fisher Discriminant 


```

```

References
http://mlpy.sourceforge.net/docs/3.5/
http://goelhardik.github.io/2016/10/04/fishers-lda/