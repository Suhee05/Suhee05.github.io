---
layout: post
title: Algorithm - Merge sort
date: 2017-03-14
---



## Merge sort 병합정렬

2016년 1학기 자료구조 수업시간에 배운 내용이 이번 알고리즘 수업 시간에서도 나와서 여기에 정리한다.


### 그림

![Alt text](https://github.com/Suhee05/Suhee05.github.io/blob/master/images/mergesort.jpg?raw=true)

### 알고리즘 설명

병합정렬 *merge sort* 의 핵심 알고리즘은 이것이다 - Divide and Conquer.
</br>한번에 해결할 수 없는 문제를 작은 단위로 쪼개서 해결한 다음 이어붙이는 것.
</br>그런데 어떻게 쪼개고 이어붙일 것인가?
</br>임의의 단위로 쪼개고 이어붙이면 알고리즘이 복잡해지고 비용도 많이 들 것이다
</br>일정한 단위로 쪼개고 이어붙이는 행위를 반복할 수 있도록 하는 재귀함수 *recursive function* 을 만들면 이 문제를 해결할 수 있다.

병합정렬에서는 숫자들의 배열을 둘로 쪼개는 것을 반복한 뒤 *divide* ,
</br> 가장 끝에 쪼개진 요소들끼리 대소비교 후 차례대로 배열에 집어넣는다. *conquer* 




### 알고리즘 구현

대략의 작동원리를 알았으니 이제 그림으로 넘어가서 어떻게 실제로 코드로 구현되는지 살펴보겠다.
</br> merge sort는 함수로 구현되는데, 이 함수는 두 부분으로 이루어져있다. 
</br> Divide 부분인 mergesort, Conquer 부분인 merge 이다.
</br> mergesort 는 주어진 array를 두 부분으로 쪼개는 것을 반복하며 merge는 쪼개진 두 부분을 합치게 된다.
</br> merge 에서 두 array를 합칠 땐 당연히 각 element 간 대소비교를 해서 합친다.

#### mergesort

mergesort는 재귀함수 *recursive function* 이다. 어떤 mergesort(tmp,A,p,r)


#### merge


