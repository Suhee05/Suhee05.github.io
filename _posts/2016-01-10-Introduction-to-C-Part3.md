---
layout: post
title: Introduction to C programming Part3
---


#Introduction to C programming 

# Part3 - 포인터

## 포인터란 무엇인가?

- 포인터 : 메모리의 주소값을 저장하기 위해 선언되는 변수
- 포인터 변수의 크기는 시스템 주소 값 크기에 따라 다르다

```

/* “정수 7이 저장된 int형 변수 num을 선언하고 
이 변수의 주소 값 저장을 위한 포인터 변수 pnum을 선언하자. 
그리고 나서 pnum에 변수 num의 주소 값을 저장하자.” */

int main(void) 
{
	int num = 7;
	int * pnum; // 포인터 변수 선언
	pnum = &num; //num의 주소값을 pnum에 저장 & 연산자의 피연산자는 변수여야 한다
	//&연산자의 반환값은 항상 포인터변수에 저장해야 한다.
}

// 이 상태를 다음과 같이 표현한다
// 포인터 변수 pnum이 num을 가리킨다


int num1 =5;
double * pnum1 = &num1; //-> 에러. num1 이 정수형이라 포인터 변수의 형도 정수여야 함!!

int main(void) 
{
	int num = 7;
	int * pnum;
	pnum = &num; 
	printf("%d",*pnum);	//*연산자. pnum이 가리키는 메모리 공간인 변수 num에 접근하라
	// *pnum은 num과 메모리 범위와 해석방법이 동일
}

```

- type * ptr;	- type형 변수의 주소 값을 저장하는 포인터 변수 ptr의 선언

- &연산자
	- 변수의 주소값을 반환하는 연산자
	- 상수는 피연산자가 될 수 없다
	- 자료형에 맞지 않는 포인터 변수의 선언은 문제가 될 수 있다
	
- *연산자
	- 포인터가 가리키는 메모리 공간에 접근할 때 사용하는 연산자


###포인터 연산

```
void main(void)
{
    int *pnData2 = NULL; // 포인터변수 선언하고 Null로 초기화
    pnData2 = (int*) malloc(sizeof(int) * 4); //동적으로 할당받은 메모리의 주소를 pnData2에 저장
    memset(pnData2, 0, sizeof(int) * 4); //pnData2 에 저장된 주소부터 시작해서 sizeof(int)*4만큼의 크기 메모리를 0으로 초기화
    printf("%p\n", pnData2);
    printf("%p\n", pnData2 + 1);
    printf("%p\n", pnData2 + 2);
    printf("%p\n", pnData2 + 3);
    free(pnData2);
}

```

- type형 포인터 변수 대상의 증가 감소 연산 시 sizeof(type)의 크기만큼 값이 증가 및 감소한다. 이렇게 자료형에 따른 메모리의 간격을 offset이라 한다.


### 다중포인터

- 포인터의 포인터는 포인터 변수를 가리키는 또 다른 포인터 변수를 뜻한다

```
// 이중 포인터의 선언은 다음과 같다
int ** dptr; //int형 이중 포인터 

int main(void)
{
	double num = 3.14;
	double * ptr = &num; // 변수 num의 주소값 저장 
}
// 포인터 변수도 변수이다. 메모리 공간에 할당이 된다. 
// 이 때 이 값을 가르키는 주소값은 double ** dptr = &ptr; 이렇게 저장이 가능하다. 
// 이제 num변수에 접근하는 법이 여러가지가 되었다...!
// *(*dptr) 로 접근할 수도 있고 *ptr로 접근할 수도 있고 그냥 num으로도 접근할 수 있다.
```

</br>

## 배열

- 배열 : 동일 자료형 메모리들을 일정 개수 묶어서 선언하는 것
- 이를 나타내는 이름을 배열의 이름이라 한다
- 배열의 이름은 첫번째 요소의 주소 상수

```
//배열 선언에 필요한 3가지
int oneDimArr[4];
//변수타입 배열이름[배열크기]

//배열에 접근
arr[0] = 10; //배열의 첫번째 요소에 10을 저장해라

//선언과 동시에 초기화
int arr1[5] = {1,2,3,4,5}
int arr1[5] = {1,2} //초기화 값이 부족한 경우 나머지는 0으로 채워짐
int arr1[] = {1,2} //길이정보 없으면 컴파일러가 메꿔준다

//배열의 크기

sizeof(arr1) //배열의 크기를 바이트 크기 정보로 반환


int arr1[5] = {1,2,3,4,5};
printf("배열 arr1의 크기: %d \n", sizeof(arr1));
ar1Len = sizeof(arr1) / sizeof(int); //  이래야지 배열의 길이를 계산가능

```

- 문자형 배열

```
char str[14]= "Good Morning!";
//배열로 저장될 때, 문자열의 끝에는 널문자라고 불리는 \0가 삽입된다. 문자열의 끝을 의미한다
//널문자가 공백문자는 아니다
```


- scanf 함수를 통해 입력받을 때 &연산자를 쓰지 않아도 된다

```
scanf("%s", str); //이 때도 널문자가 뒤에 붙어서 저장된다

//하지만 scanf는 공백을 기준으로 문자열을 구분하므로 문장을 입력받기엔 적절치 않음
// 다른 함수가 있다.
``` 
 

###배열과 포인터의 관계

- 포인터 변수를 이용해 배열의 형태의 메모리 공간에 접속

```
int main(void)
{
	int arr[3] = {1,2,3}; //여기선  int로 선언되었으므로 arr도 int형 포인터변수
	printf("배열의 이름: %p \n", arr);
	printf("첫째요소: %p \n", &arr[0]);
	printf("둘째요소: %p \n", &arr[1]);
	printf("셋째요소: %p \n", &arr[2]);
	//실행해보면 배열요소간 주소 값의 크기는 4바이트임을 알 수 있다
}
```

- 포인터 변수를 이용해 배열의 형태로 메모리 공간에 접속

```
int main(void)
{
	int arr[3] = {1,2,3}; 
	int * ptr = arr; //int * ptr = &arr[0];도 같은 문장
	
	printf("첫째요소: %d %d \n", ptr[0], arr[0]); 
	printf("둘째요소: %d %d \n", ptr[1], arr[1]);
	printf("셋째요소: %d %d \n", ptr[2], arr[2]);
	// 포인터변수를 이용해 배열의 형태로 메모리 공간에 접속
	printf("첫째요소: %d %d \n", *ptr, *arr); //포인터는 처음위치를 가리킴
	}
```

- 포인터 연산

```
int main(void)
{
	 int * arr[3] = {11,22,33};
	 int * ptr = arr;
	 
	 printf("%d %d %d \n", *ptr, *(ptr+1), *(ptr+2));
	 printf("%d ", *ptr); ptr++;
	 printf("%d ", *ptr); ptr++;
	 printf("%d ", *ptr); ptr--;
	 printf("%d ", *ptr); ptr--;
	 printf("%d ", *ptr); 
	 return 0
	 
}

```

- 배열이름도 포인터이니, 포인터 변수를 이용한 배열의 접근방식을 배열의 이름에도 사용할 수 있다. 
- 그리고 배열의 이름을 이용한 접근방식도 포인터 변수를 대상으로 사용할 수 있다. 
- arr이 포인터 변수의 이름이건 배열의 이름이건 arr[i] == *(arr+i)


###문자열과 포인터

```
//문자열 선언엔 두 가지 방법이 있다.
int main(void){

char str1[] = "Your team";str1 = "Our team"; //대입 불가. 

char * str2 = "Your team";str2 = "Our team"; // 대입가능
  }

```


- str1은 문자열이 저장된 배열이다. 즉, 문자 배열이다. 따라서 변수성향의 문자열이다. str2는 문자열의 주소 값을 저장한다. 즉, 자동 할당된 문자열의 주소 값을 저장한다. 따라서 상수성향의 문자열이다.

- str1 처럼 선언하나 str2 처럼 선언하나, str1, str2 둘 다 문자열의 시작주소를 담고 있는 것은 같다. 

```
int main(void){
	char str1[ ] = "Suhee Jo";
	char * str2 = "Weback Kim";
    
    str2 = "HyeBin Yoon"; // str2는 가리키는 대상을 변경가능. str1는 불가
    
    str1[0] = 'x';
    str2[0] = 'x'; // str2는 구성요소 변경 불가
}
```

- 즉 str1과 같은 문자 배열은, 변수성향의 문자열이고, 구성요소를 바꿀 수는 있지만, 다른 값을 가리키게 할 수는 없다. str2은 그 반대


```
char * str = "Const String"; //"Const String"은 상수형태의 문자열이고 메모리 어딘가에 저장된다
char * str = 0x1234; // 위의 라인이 실행되면 사실상 다음과 같이 저장되는 것이다
```

###포인터배열

- 포인터 배열 : 포인터 변수들의 배열. 주소값들을 저장할 수 있도록 만든 것!

```
int main (void) {

	int num1 = 10, int num2 = 20, int num3 = 30;
	int * arr[3] = {&num1, &num2, &num3}; //각 변수의 주소값(포인터변수) 저장
	printf("%d \n",  *arr[0]); //*연산자 뜻 알지? 메모리 번지 참조해서 값을 가져와 라는 뜻
	printf("%d \n",  *arr[1]);
	printf("%d \n",  *arr[2]);
	// 프린트 되는 값은 10 20 30 arr[i]는 각 메모리주소를 뜻하고 이것이 가리키는 건 해당값이다
	
}
```

- 문자열을 저장하는 포인터 배열 : char 형 포인터 배열. 실제로 저장하는 건 문자열의 주소값

```
	char * strArr[3] = {"Simple", "String", "Array"}; //문자열 선언
	//큰 따옴표로 묶여서 표현되는 문자열은 그 형태에 상관없이 메모리 공간에 저장된 후 그 주소 값이 반환된다	
	char * strArr[3] = {0x1004, 0x1048, 0x2012)
	//그니까 실제로는 이렇게 됨	

```

### 다차원배열

- 다차원배열에서 주로 거의 다루는 건 2차원 배열. 선언은 Type arr[세로길이][가로길이]; 

```
int main (void){
	int arr1[3][4]; //세로(행)가 3 가로(열) 4
	printf("세로3 가로4: %d \n", sizeof(arr1)); // sizeof 연산자의 피연산자로
	//배열의 이름이 오면, 배열의 크기가 바이트 단위로 계산되어서 반환됨
	//여기선 3x4x4 = 48
}
```

- 2차원 배열요소의 접근은 이름이 arr인 int형 배열을 대상으로 N번째 행 M번째 열에 접근하려면 

```
arr[N-1][M-1] = 20; //이런 식으로 접근해서 값을 변경할 수 있다
```


- 2차원 배열 선언과 동시에 초기화

```
int arr[3][3] = {{1,0,0},{4,5,0},{7,8,9}};
int arr[3][3] = {1,0,0,4,5,0,7,8,9};
// 두 개 다 같은 matrix 초기화이다.
// 만약 배열의 크기만큼 초기화가 안 되면 부족한 부분은 다 0으로 메꿔진다 (1차원과 마찬가지)

int arr[][] = {1,2,3,4,5,6,7,8}; //에러
//배열의 크기를 알려주지 않고 초기화할 수는 있다. 하지만 위의 예에서 보듯이, 저런 경우
// 2x4 행렬도 될 수 있고, 4x2,8x1,1x8도 될 수 있다.
int arr[2][] = {1,2,3,4,5,6,7,8}; //성공
//이런 식으로 하나만 힌트를 주면 행렬모양이 결정되므로 컴터가 알아서 할 수 있는 것
```

- 3차원 배열은 2차원 배열이 여러 개 모여있는 것으로 생각하면 된다. 필요할 때 관련내용은 찾아보길.


###다차원 배열과 포인터

- 2차원 배열의 이름도 배열의 첫번째 요소, 즉 arr[0][0]의 주소이다. 그러나 이에 대해 간접지정연산(*)을 수행하더라도 주소가 나온다. 왜냐하면 arr[0]도 하나의 배열이기 때문.
- arr와 arr[0]의 주소값은 같지만, sizeof 연산을 하면 각 다르게 나온다. 
- 포인터 형에 따라 포인터를 대상으로 하는 증가 및 감소 연산의 결과가 정해진다!

```
int main(void)
{
	int arr1[3][2];
	int arr2[2][3];
	
	printf("arr1: %p \n", arr1); //arr1:004BFBE0
	printf("arr1+1: %p \n", arr1+1); //arr1+1:004BFBE8
	
	printf("arr2: %p \n", arr1); //arr2:004BFBC0
	printf("arr2+1: %p \n", arr1+1); //arr2+1:004BFBCC
	//16진수로 출력되고 있음
}	
```

- 2차원 배열이름을 대상으로 증가 및 감소연산을 할 경우 연산결과는 각 행의 첫 번째 요소의 주소 값이 된다. 
- 2차원 배열이름의 포인터형은 가로 길이에 따라서도 달라진다!
- 이러한 유형의 포인터 변수 선언은 다음과 같이 한다
	- 예를 들어서 int 형 변수를 가리키면서 포인터 연산시 sizeof(int)x4의 크기단위로 증감하는 포인터 변수ptr은 int (*ptr) [4]; 이다. 

- 2차원 배열을 함수의 인자로 전달하기

	- void SimpleFunc(int (*parr1)[7]) 혹은 voidSimpleFunc(int parr1[][7])로 선언. 	
	- 하지만 두 개는 매개변수 선언에서만 같은 것

```
void ShowArr2DStyle(int (*arr)[4], int column) //배열요소 전체출력
{
	int i, j;
	for(i =0, i<column; i++)
	{
		for(j =0, j<4; i++)
			printf("%d ", arr[i][j]);
		printf("\n");
	}
	printf("\n")
}

void Sum2DArr(int (*arr)[][4]. int column) //배열요소의 합 반환
{
	int i, j, sum =0;
	for(i =0, i<column; i++)
		for(j =0, j<4; i++)
			sum += arr[i][j];
	return sum;
}

int main(void)
{
	int arr1[2][4] = {1,2,3,4,5,6,7,8};
	int arr1[3][4] = {1,1,1,1,3,3,3,3,5,5,5,5};
	ShowArr2DStyle(arr1,  sizeof(arr1) / sizeof(arr1[0]));
	ShowArr2DStyle(arr2,  sizeof(arr2) / sizeof(arr2[0]));
	printf("arr1의 합: %d \n",Sum2DArr(arr1,  sizeof(arr1) / sizeof(arr1[0])));
	printf("arr2의 합: %d \n",Sum2DArr(arr2,  sizeof(arr2) /sizeof(arr2[0])));

	return 0
}

```

- 2차원 배열에서도 arr[i]와 *(arr+i)는 같다


</br>


### 함수와 포인터

- 함수 호출 시 전달되는 인자(argument)의 값은 매개변수(parameter)에 복사가 된다
- 하지만 매개변수로 배열을 선언할 수 없기때문에, 함수 내에서 배열에 접근할 수 있도록 배열의 주소값을 전달

```
void ShowArayElem(int * param) //int형 포인터변수로 매개변수 설정.매개변수는 int param[] 이렇게도 설정가능 
{
	int i;
	for(i=0; i<len; i++)
		printf("%d ", param[i]);
	printf("\n");
}

int main(void)
{
	int arr1[3] = {1,2,3};
	int arr2[5] = {4,5,6,7,8};
	ShowArayElem(arr1, sizeof(arr1) / sizeof(int));
	ShowArayElem(arr2, sizeof(arr2) / sizeof(int));
	return 0
}

void AddArayElem(int * Param, int len, int add)
{
	int i;
	for(i=0; i<len; i++)
		param[i] += add;
}

```
- 배열의 값 변경도 가능하다


- Call by value vs Call by reference
- 함수를 호출할 때 단순히 값을 전달하는지, 아니면 주소값을 전달하는지. (전자, 후자)
- 아까 배열을 인자로 전달하는 함수는 Call by reference. 보통 우리가 정의했던 함수들은 Call by value

- Call by reference 함수가 Call by value 함수와 다른 점은 Call by value 함수는 전달받은 인자의 값을 복사해서 함수 결과값을 돌려주지만, 인자 자체에는 손댈 수 없는 반면에 Call by reference는 인자 자체에 접근할 수 있다는 점이다


- 포인터 대상의 const (상수) 선언

```
int main(void)
{
	int num =20;
	const int * ptr = &num; //포인터 변수 ptr을 이용해서 ptr이 가리키는 변수에 ...
	//저장된 값을 변경하는 것을 허용하지 않는다
	// int * const ptr = &num; 이렇게 하면 포인터변수 ptr이 상수가 된다.
	// 이 말은, 한 번 가리키기 시작한 변수를 끝까지 가리켜야 한다는 것
	* ptr = 30; //컴파일 에러
	num = 40; //컴파일 성공
}


```


</br>

###함수포인터와 void 포인터

- 프로그래머가 정의하는 모든 함수는 프로그램 실행 시 메인 메모리에 저장되어서 실행된다. 
- 함수의 이름은 메모리상 저장된 함수의 주소 값이다 (배열과 마찬가지)
- 함수의 이름도 상수이다 (배열과 마찬가지)
- 함수의 주소 값 저장을 위해 포인터 변수를 별도로 선언할 수 있고 이렇게 선언된 변수가 함수포인터변수
- 함수의포인터변수의 형은 반환형과 매개변수의 선언형태를 기준으로 구분
- int(*fptr)(int) 이렇게 선언한다
- 그리고 이 함수 포인터 변수에 함수SoSimple의 주소값을 저장하려면 fptr = SoSimple;
- 이후에는 동일하게 호출가능 ftpr(3,4);

```
int WhoIsFirst(int age1, int age2, int (*cmp)(int n1, int n2))
{
	return cmp(age1,age2);
}
```

- 형이 존재하지 않는 void 포인터
- void * ptr; 이렇게 선언
- void 포인터는 형이 정해져 있지 않아서 연산도 못하고 값 변경, 참조도 못한다.
