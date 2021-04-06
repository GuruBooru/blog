# 난수

#### C++ 에서의 난수

* rand\(\)

  * 0 ~ 32767 까지 정수 표현 가능
  * srand\(\) : 난수 생성에 필요한 시드값 설정

  ```cpp
  int a = rand();
  ```

  해당 코드를 디스 어셈블리로 확인해보면

  ```cpp
  int a = rand();
  mov         esi,esp  
  call        dword ptr [__imp__rand (037B170h)]  
  cmp         esi,esp  
  call        __RTC_CheckEsp (037123Ah)  
  mov         dword ptr [a],eax
  ```

  아래와 같은 코드를 확인할 수 있다.

  rand 함수 내부에서  \_\_imp_\_\\_rand\(\) 함수와_ 



