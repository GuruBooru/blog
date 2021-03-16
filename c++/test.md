# 변수 키워드 / 타입 캐스팅

#### C언어 변수 키워드

* 자동 변수 auto

  * 생략이 가능하며, 보통 생략하여 default로 사용
  * 변수의 위치를 컴파일러가 함수 스택에 맞춰서 알아서 지정

* 정적 변수 static

  * 데이터 영역에 메모리 위치
  * 지역 변수 : 해당 블록 내에서만 사용할 수 있는 전역 변수
  * 전역 변수 : 같은 파일 내에서만 사용할 수 있는 변수

* 외부 변수 extern

  * 전역변수로 지정된 값을 링크 단계에서 찾아 사용

* 레지스터 변수 register
  * 컴파일러에게 **가능하다면** CPU 레지스터에 선언하도록 지시

    * 레지스터가 남는 경우, 남아있는 레지스터 1개를 메모리로 활용
    * 최적화 컴파일 시 적용
* 최적화 제외 volatile
  * 해당 변수를 사용하는 모든 부분에서 최적화 제외



#### 타입 캐스팅

* 어셈블리 코드 상 바뀌는 것은 없음 &gt; 데이터는 메모리에 그대로 있음
* CPU는 리틀 엔디안으로 메모리를 읽고 쓰기 때문에 LSB부터 읽으면서 필요없는 부분은 더 이상 읽지 않는 방식
  * _정수-실수 변환의 경우 표현하는 방식이 다르기 때문에 변환 함수 호출_ 

{% tabs %}
{% tab title="정수 > 실수" %}
```cpp
	int intValue = 1000;

	cout << intValue;
	cout << (double)intValue;
```

![](../.gitbook/assets/int-double-.png)

double 타입으로 변환하기 위해 **cvtsi2sd** 라는 명령어가 호출
{% endtab %}

{% tab title="실수 > 정수" %}
```cpp
double doubleValue = 10.0;

	cout << doubleValue;
	cout << (int)doubleValue;
```

![](../.gitbook/assets/double-int-.png)

int 타입으로 변환하기 위해 cvttsd2si 명령어 호출
{% endtab %}
{% endtabs %}

어셈블리는 Visual Studio 2019의 디스어셈블리를 사용하였습니다.

