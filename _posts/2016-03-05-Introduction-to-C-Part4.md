#Introduction to C programming 

# Part4 - 메모리의 동적할당, 구조체, 전처리기



## 메모리의 동적 할당

- 원할 때 메모리를 할당하고 해제할 수 있는 변수를 만들 때, malloc과 free 함수를 쓴다
- 이 때 힙영역의 메모리에 할당된다
- malloc 함수는 지정하는 크기만큼의 메모리 공간을 할당하고 그 메모리의 주소값을 반환하지만, 어떤 값을 가리킬지는 포인터변수를 통해 직접 결정해야한다

```
int main(void)
{
	int * ptr = (int*)malloc(sizeof(int));
	
	*ptr = 20;
	
	free(ptr);
}

```

- calloc 함수는 malloc 함수와 동일하지만, 인자를 두 개로 받는다. 첫 인자는 블록의 개수, 두번째 인자는 블록 당 바이트 크기이다. 따라서 malloc에서 총 20 바이트를 할당받는다면 calloc 에서는 4,5로 표현가능하다.

```
#include <stdlib.h>

int * a;
a = (int*)calloc(n, sizeof(int));
```

- realloc 함수는 이미 할당된 메모리를 확장해준다

```
#include <stdlib.h>

   char *str;
   str = (char *) malloc(15);
   str = (char *) realloc(str, 25);

```

</br>

## 구조체

- 구조체는 하나 이상의 변수를 묶어서 새로운 자료형을 정의하는 도구

```
struct point 
{
	int xpos;
	int ypos;
};
// 이렇게 정의된 struct point란 자료형을 바탕으로 새로운 변수를 생성할 수 있다.

struct point pos // pos라는 이름의 구조체 변수 선언
pos.xpos = 20; //구조체 변수 pos의 멤버 xpos에 20을 저장

//구조체 정의와 동시에 변수선언
struct point 
{
	int xpos;
	int ypos;
}pos1,pos2,pos3;

struct point 
{
	int xpos;
	int ypos;
};
struct point pos1,pos2,pos3 //구조체 변수의 선언

//구조체 변수의 초기화
struct point pos = {10,20} //멤버 순서대로 초기화

//구조체변수선언 이후에 구조체 멤버에 문자열 저장하기 위해선 strcpy함수 필요
//하지만 초괴화과정에서는 불필요

struct person
{	
	char name[20];
	char phoneNum[20];
	int age;
};

struct person man1;
strcpy(man1.name, "윤혜삔");

struct person man2 = {"조수희","010-3030-2039",12};
```

### 구조체와 배열 그리고 포인터

- 구조체 배열의 선언과 접근

별 거 아니고 구조체 변수들의 배열을 만드는 것. struct point arr[4];와 같이 선언. 배열의 두번째 요소의 멤버에 접근하고 싶다면 arr[1].xpos 이렇게 접근

- 구조체 배열의 초기화

```
struct person arr[3] = { {"윤혜삔","010-3030-2039",12},  {"김위백","010-3453-2039",27}, {"조수희","010-9879-2039",23}}
```

- 구조체 변수와 포인터

```
struct point pos = {11,12};
struct *pptr = &pos; //포인터변수 pptr이 구조체 변수 pos를 가리킴
// 포인터변수니까 *를 이용해서 변수에 접근가능
(*pptr).xpos =10; // pptr이 가리키는 구조체 변수의 멤버 xpos에 10저장
//* 연산과 . 연산을 한방에 하는 방법이 있다
pptr->xpos = 10; //이것은 위와 같은 연산이다.

```

- 포인터 변수를 구조체의 멤버로 둘 수 있다.

```
struct point
{
	int xpos;
	int ypos;
};

struct circle
{
	double radius;
	struct point * center;
};

int main (void)
{
	struct point cen = {2,7};
	double rad = 5.5;
	
	struct circle ring = {rad, &cen};
	printf("원의 반지름: %g \n", ring.radius);
	printf("원의 중심: [%d, %d] \n", (ring.center)->pos, (ring.center)->ypos);
	return 0;
}

```

- Type형 구조체 변수의 멤버로 Type형 포인터 변수를 둘 수 있다

이로써 같은 타입의 구조체 변수들 끼리 연결이 가능하다!

```
struct point
{
	int xpos;
	int ypos;
	struct point * ptr; //구조체 point의 포인터 변수 선언
};
```

### 구조체의 정의와 typedef선언



- typedef선언: 기존에 존재하는 자료형의 이름에 새 이름을 부여하는 것을 목적으로 하는 선언. 새로운 이름의 부여는 가장 마지막 단어에 의해 이루어진다.

	- 예를 들면 typedef name1 name2 name3; 에서 가장 마지막의 name3 가 'name1 name2'에 부여된 새로운 이름이 되는 것이다. 

```
typedef unsigned int UNIT; // unsigned int 에 UNIT이란 이름 새로 부여!

struct point
{
	int xpos;
	int ypos;

};

typedef struct point Point; //이제부터 struct point 데이터 타입을 Point라 하겠다

Point pos; // Point 타입의 pos 변수가 선언 

typedef struct point //이런식으로도 선언가능. 
{
	int xpos;
	int ypos;

}Point;

typedef struct {
	int xpos;
	int ypos;

}Point; //구조체의 이름은 이제 필요하지 않다. 어차피 Point란 새로운 이름이 생겼으니!

```

- 함수로의 구조체 변수 전달과 반환


```
typedef struct point{
	int xpos;
	int ypos;

}Point;

void ShowPosition(Point pos) //구조체인 매개변수를 다음과 같이 받는다
{
	printf("[%d, %d] \n", pos.xpos, pos.ypos);
} 

Point GetCurrentPostion(void) //구조체를 반환하는 함수이다
{
	Point cen;
	printf("Input current pos: ");
	scanf("%d %d", &cen.xpos, &cen.ypos);
	retrun cen;
}

//여기에서 정의된 함수들은 CallbyValue임을 잊지말자. 
//메모리주소(포인터)값을 전달하지 않는 경우 모두 CallbyValue. 
//즉 매개변수로 들어온 값들을 복사해서 함수 내에서 쓰는 것
```

- 구조체 변수를 대상으로 가능한 연산 : 대입연산(복사해서 값 집어넣기) , &연산, sizeof연산 정도.

```
typedef struct point
{
	int xpos;
	int ypos;
}
 

int main (void)
{
	Point pos1 {1,2}
}


```

- 중첩된 구조체: 먼저 정의된 구조체는 기본 자료형의 이름과 마찬가지로 사용될 수 있다

```
typedef struct point{
	int xpos;
	int ypos;

}Point;

typedef struct circle{
	Point center;
	double rad;

}Circle;
```

### 공용체 

- 공용체 : 선언 시 구조체와 차이는 구조체의 struct부분이 union 으로 바뀐다는 것이다.
- 구조체 변수가 선언되면 그 안의 멤버들은 각각 메모리에 할당이 되지만, 공용체 변수가 선언되면 그 안 멤버들은 각각 할당되는 것이 아니라 크기가 가장 큰 멤버의 변수만 할당되고, 나머지 멤버들은 이를 공유한다.

### 열거형

- 저장이 가능한 값 자체를 정수의 형태로 결정. 구조체가 각 멤버에 저장할 값의 유형을 결정했다면, 이건 저장이 가능한 값 자체를 정수 형태로 결정

```
typedef enum juniors
{
	HyeBin = 1, Weback =2, Suhee =3
}Juniors;

void workload(Juniors jy)
{
	switch(jy)
	{
	case HyeBin:
		puts("조금만 더 일하세요"); return;
	case Weback:
		puts("많이 더 일하세요"); return;
	case Suhee:
		puts("일하지 마세요"); return;
	}
}


//여기서 HyeBin =1 의 뜻은 HyeBin을 1을 의미하는 상수로 정의. 
그리고 이 값을 syllabe형 변수에 저장 가능하다는 뜻
```
- 만약 열거형 정의시 상수값 명시 안하면 기본적으로 첫 상수값은 0에서 시작해서 1씩 증가한다. 

## 전처리기

- 전처리기, 다른 말로는 선행처리기 (Preprocessor)는 컴파일 되기 전에 먼저 실행되는 구문
 


### 매크로

- Object like macro : #define PI 3.1415
	- 지시자 매크로 매크로몸체로 구성되어 있고, 매크로를 매크로몸체로 치환하라는 지시이다
- Function like macro : #define SQUARE(X) X*X
	- 지시자 패턴 유형으로 구성되어 있고, 패턴을 유형으로 치환하라는 지시이다
	- 여기서는 SQUARE(X)라는 패턴이 등장하면 X*X로 무조권 바꾸라는 지시이다
	- 먼저 정의된 매크로는 뒤에서도 사용가능


- 매크로 함수의 장/단점
	- 장점 : 일반함수에 비해 실행속도 빠르고 별도의 함수 정의가 필요 없음.
	- 단점 : 정의하기 어렵고 디버깅도 어려움
	- 작지만 호출 빈도가 높은 함수를 정의하는 것이 좋다


- 조건부 컴파일을 위한 매크로 : #if...#endif 
	- 특정 조건에 따라 소스코드 일부를 삽입이나 삭제
	- if 다음 조건이 참이라면, endif 전까지의 문장들을 실행하라
	- \#ifndef...#endif ifndef 다음 조건이 정의되지 않았다면, endif전까지의 문장들을 실행하라

	```
	# define MUL 1
	# define DIV 0
	
	int num1, num2;
	printf("두 개의 정수 입력");
	scanf("%d %d", &num1, &num2);
	
	#if MUL
		printf("%d\n", num1*num2);
	#endif
	
	#if DIV
		printf("%d\n", num1/num2);
	#endif
	
	```
	
	- \#if... #endif 사이에 #elif 나 #else 구문이 삽입되면 조건에 따라서 if 와 elif, else 사이에 하나만 컴파일된다는 뜻

- 문자열 내에서 매크로
	- 문자열 내에서는 매크로가 치환되지 않는다
	- \#define STR(ABC) #ABC
	- \# 연산자 : 매개변수 ABC에 전달되는 인자를 문자열 "ABC"로 치환하라는뜻
	- 둘 이상의 문자열을 나란히 선언되면 연결된다
	- \#define CON(UP,LO) UP##00##LO
	- \##연산자 : 매개변수 

	
### 헤더파일

- 하나의 프로그램을 여러가지 파일로 분할할 때, 해당 함수나 변수가 다른 파일에 있다는 것을 알리기 위해 extern 을 사용한다

```
extern int num;
extern void Increment(void);
```

- 표준헤더파일의 포함: #include <표준파일이름>
- 사용자정의헤더파일의 포함: #include "파일이름"