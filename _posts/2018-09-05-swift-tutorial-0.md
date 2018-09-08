---
layout: post
title: Swift Tutorial 0
date: 2018-09-05
---

## Why Swift?

**Swift**는 2014년 **Apple** 이 출시한 Compiled Language이다. LLVM 컴파일러를 이용해 컴파일되는데, 이는 **Xcode**에 포함되어있다.

**Swift**에 대해서 내가 느낀 가장 큰 장점은 다음과 같다.

**배우기 쉽다.** **Xcode**를 이용하면 특히 더 쉬워진다.

**Swift** 가 나타나기 이전에는 IOS App 을 만들 때 **Objective-C**가 주로 사용되었다. **Objective-C** 는 C언어를 계승한 언어로, **Swift**와 비교하면 여러모로 복잡하다. **Swift** 는 직관적으로, 빠르게 코드를 쓸 수 있고 **Xcode**가 이때 훌륭하게 보조를 해준다. 하지만 아직까지 참고할만한 코드가 **Objective-C** 로 쓰여진 경우가 많아서, 어느 정도 **Objective-C**를 읽을 줄 아는 것은 필요하다.

**Swift**의 또 다른 장점은 **안전하다**는 것이다. **Swift**는 타입에 굉장히 민감하다. 또한 옵셔널이라는 새로운 개념을 도입한 것만 봐도 프로그램의 안정성에 대해 굉장히 신경을 썼다는 것을 알 수 있다. 

**Objective-C**와 비교해본 적은 없지만, 애플에서 발표하기를 **Swift**는 속도에 있어서도 **굉장히 빠르다**고 한다. 이름 **Swift** 에서 짐작할 수 있는대로다.

![alt text](https://github.com/Suhee05/Suhee05.github.io/blob/master/images/swift1.png?raw=true)

## Xcode

**Xcode** 는 **Apple**에서 출시한 **IDE, Integrated Development Environment** 이다. 지원하는 언어는 여러가지가 있는데, **C** 와 **C++**, **Objective-C**, **Swift**가 대표적이다. 나도 이들 4개 언어들에 대해서 Xcode를 사용해보았는데, 사용해본 다른 어떤 **IDE** 보다 편리했다. **Xcode**와 함께라면 Swift 초보자들도 IOS App을 만드는데 무리가 없다.

### Xcode Features

- **Project**: 앱 개발 공간
	- New project -> template 고르기-> 이름 만들고 옵션 체크 
- **Playground**: 코드 작성을 위한 공간

- Project를 만들면 보이는 화면. 왼쪽에는 프로젝트에 속한 파일들, 오른쪽에는 인스펙터들 인스펙터들의 밑에는 라이브러리들이 있다 그 중 오브젝트 (바, 컨트롤, 뷰 등 UI 요소들) 라이브러리가 가장 많이 쓰인다. 
- 인스펙터의 왼쪽에서 세번째부터 identity inspector, attribute inspector, size inspector, connections inspector
- **Main.storyboard**: 메인 UI를 개발하는 공간
- **Simulator**: Simulator 창이 띄워지면 menu 에서 Hardware 로 가면 기기 버전 변경이라던지 여러가지 조정을 할 수 있다. 옵션키를 누르면 멀티터치가 적용된다


