---
layout: post
title: Introduction to C programming Part2
date: 2016-01-09
---



# Part2 - 함수

## 함수

- 함수의 크기는 작을수록 좋고, 하나의 함수는 하나의 일을 담당하게 해야한다
-  유형 1: 전달인자 있고, 반환 값 있다! 전달인자(○), 반환 값(○) 
-  유형 2: 전달인자 있고, 반환 값 없다! 전달인자(○), 반환 값(x) 
-  유형 3: 전달인자 없고, 반환 값 있다! 전달인자(x), 반환 값(○) 
-  유형 4: 전달인자 없고, 반환 값 없다! 전달인자(x), 반환 값(x)


```
int Add(int num1, int num2) //유형1
{
	int result = num1 + num2;
	
	return result;
}

void ShowAddResult(int num) //유형2
{
	printf("덧셈결과출력 : %d \n", num);
}

int ReadNum(void) // 유형3
{
	int num;
	scanf("%d" , &num); //뒤에서 배울테지만, &연산자는 주소값을 반환한다
	return num;
}

void HowToThisProg(void) //유형4
{
	printf("이제 가보자! \n");
}

// 이제 위의 네 개를 사용해보자

int main(void)
{
	int result, num1, num2;
	HowToThisProg();
	num1 = ReadNum();
	num2 = ReadNum();

}

```

- 값을 반환하지 않는 return

```
void NoReturnType(int num) 
{
	if(num<0)
	return;
	
}
```

- 함수의 선언 : 컴파일이 위에서 아래로 진행되어, 미리 선언되지 않은 함수는 쓰일 수가 없다. 그래서 함수를 일단 선언하고 그 다음 정의해줌

```
int Increment(int n); //함수의 선언

int main(void)
{
	int num =2;
	num = Increment(num);
	return 0;
}

int Increment(int n) //함수의 정의
{
	n++;
	return n;
}
```

## 변수의 존재기간과 접근 범위

- 지역변수 : 함수 내에 선언되는 변수를 가리켜 지역변수라 핚다.	- 지역변수는 선언된 이후로부터 함수 내에서만 접근이 가능하다.
	- 해당 지역을 빠져나가면 지역변수는 소멸된다. 그리고 호출될 때마다 새롭게 할당된다.	- 한 지역(함수) 내에 동일한 이름의 변수 선언 불가능하다.
	- for 문의 중괄호 안에 선언된 변수도 일종의 지역변수이다.
	- 매개변수(parameter)는 일종의 지역변수이다 

```
int SimpleFuncOne(void)
{
	int num = 10;
	num++;
	printf("SimpleFuncOne: %d \n" , num);
	return 0;
}

int SimpleFuncTwo(void)
{
	int num1 = 20;
	int num2 = 30;
	num1++ , num2--;
	printf("num1 & num2 : %d %d \n" , num1, num2);
	return 0;
}

int main(void)
{
	int num =17;
	SimpleFuncOne();
	SimpleFuncTwo();
	printf("main num: %d \n", num);
	return 0;
}
```



- 전역변수 : 전역변수는 함수 외부에 선언된다.	- 프로그램의 시작과 동시에 메모리 공갂에 할당되어 종료시까지 존재한다.	- 별도의 값으로 초기화하지 않으면 0으로 초기화된다.	- 프로그램 전체 영역 어디서든 접근이 가능하다.
	- 지역변수의 이름이 전역변수의 이름을 가린다
	- 전역변수는 많이 쓰면 좋지 않다...

- static변수 : 선언된 함수 내에서만 접근이 가능하다. (지역변수 특성)딱 1회 초기화되고 프로그램 종료 시까지 메모리 공간에 존재핚다. (전역변수 특성)

- register변수 : 빈번히 사용하는 변수를 접근이 가장 빠른 메모리에 저장

- static 변수, register 변수 모두 선언할 때 그냥 앞에다 static, register 붙여주면 된다. static int num2 = 10; 이렇게


## 재귀함수에 대한 이해

- 자기 자신을 호출하는 함수
- 한 번 호출되면 계속 자기 자신을 호출하기때문에 탈출조건을 만들어주어야한다.

```
int Factorial(int n)
{
	if(n==0) //탈출조건
		return 1;
	else
		return n * Factorial(n-1);
}

```




