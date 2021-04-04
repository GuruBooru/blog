# Call by Reference / 포인터 / 매크로

> call by reference가 call by value보다 빠르다?  
> 구조체, 클래스의 경우 call by reference가 더 빠르다 → call by value의 경우 객체의 카피가 일어남
>
> 일반 변수에 대해서는 오히려 더 느리다  
> call by value의 경우 일반 변수를 바로 복사하여 사용하지만, call by reference는 일반 변수가 저장된 주소 포인터를 복사하기 때문에 값에 접근하기 위해서는 포인터를 거쳐서 전달받아야 한다.

#### 

#### 포인터

> void 포인터?  
> 해당 변수에 포인터를 보관만 하는 경우 사용  
> 연산, 값 변환 X

```cpp
/*
*    함수 포인터?
*    함수의 주소를 저장하는 포인터
*    배열로도 선언이 가능하며, switch-case 문을 사용하지 않고 분기문 작성 가능
*/

// 반환형 (*함수 포인터 이름)(인자 목록)으로 선언
void func1()
{
    cout << "func1" << endl;
}


void (*funcPtr)() = func1;
funcPtr();    // 이런 식으로 사용
```

* const 위치에 따른 const 대상
  * const int \* p : int에 대한 const, 상수값 int의 포인터
  * int const \* p : int에 대한 const, 상수값 int의 포인터
  * int \* const p : 포인터에 대한 const, int의 상수 포인터

                          : 포인터 자체가 상수이기 때문에 선언과 동시에 초기화를 해주어야 한다.

```cpp
// 모두 사용 가능하지만, 용도에 맞게 사용하여 코드에 혼동을 줄이자
void* p = nullptr;
        = 0;
        = NULL;
```



#### 매크로

* 매크로가 정의된 cpp 파일과 해당 파일을 include한 cpp 파일에 대해서만 적용
* \#pragma once : 중복 컴파일 방지 → VS에서만 적용되는 매크로
* ```cpp
  /*
  *    해당 고유이름이 정의되지 않았을 경우 정의
  *    중복으로 정의되는 경우 재정의 X
  *    서로 다른 버전을 배포하는 경우 등에 활용하여 각각의 버전에 맞게 define
  */
  #ifndef 고유이름
  #define 고유이름
  /*
      코드 정의
  */
  #endif 고유이름
  ```

> Precomflie header?  
> 가장 많이 사용되고, 변하지 않는 라이브러리를  모아서 빌드  
> VS에서는 stdafx라는 이름으로 사용\(stdafx.h, stdafx.cpp\)  
> 모든 cpp 최상단에 include 해야하며, 해당 파일에 변화가 생길 경우 모든 cpp를 리빌드함  
> 하지만 해당 파일에 변화가 없다면 전체적인 빌드 시간이 크게 단축된다.

* 시스템 정의 매크로

  ```cpp
  /*
  *    해당 매크로는 빌드 시간에 결정되며, 로그 등을 생성하는데 많은 도움을 준다.
  */
  __DATE__ // 날짜
  __TIME__ // 시간
  __FILE__ // 파일명 - 디버그 시 전체 경로, 릴리즈 시 파일 이름만
  ```

