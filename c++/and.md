# 전위 & 후위 연산자 차이 / 조건문 / 반복문

#### 전위 연산자 / 후위 연산자

* 일반 변수 타입에서는 차이 없음
* 클래스 변수에 대해서는 전위 연산에 경우 성능이 더 좋음
* 후위 연산의 경우 사본 생성

테스트를 위한 더미 클래스

```cpp
class dump
{
public:
	dump()
	{
		data = 0;
	};
	dump(int data)
	{
		this->data = data;
	}

	dump& operator++ () 
	{
		data++;
		return *this;
	}
	dump operator++(int)
	{
		dump retObj(data);
		data++;
		return retObj;
	}
private:
	int data;
};
```

{% tabs %}
{% tab title="전위 연산" %}
![](../.gitbook/assets/.png.png)
{% endtab %}

{% tab title="후위 연산" %}
![](../.gitbook/assets/.png%20%281%29.png)
{% endtab %}
{% endtabs %}



#### 조건문

{% tabs %}
{% tab title="if-else" %}
```cpp
int a = 0;

if(a == 0)
{
    cout << "a is zero";
}
else
{
    cout << "a is not zero";
}
```

위에 있는 간단한 조건문을 어셈블리로 표현할 경우

![](../.gitbook/assets/image.png)

이와 같이 나타난다.

**jne 명령어**의 경우 조건이 같지 않은 경우 해당 위치로 점프하는 명령어이다.  
현재의 경우 if 조건에 맞지 않을 경우 바로 else의 위치로 점프한다.

그렇다면, else if를 사용하는 경우에는 어떤 방식으로 점프하는지 알아보기 위해 else if를 조금 추가하여

```cpp
int a = 0;

if(a == 0)
{
	cout << "a is zero";
}
else if(a == 1)
{
	cout << "a is one";
}
else if (a == 2)
{
	cout << "a is two";
}
else if (a == 3)
{
	cout << "a is three";
}
```

이와 같은 코드를 작성하여 테스트 해보면

![](../.gitbook/assets/image%20%281%29.png)

이와 같은 결과가 나타난다.

즉, if-else문의 경우 조건을 하나씩 확인하고 다음 조건으로 넘어가는 형식으로 어셈블리 코드가 작성된다.
{% endtab %}

{% tab title="switch-case" %}

{% endtab %}

{% tab title="삼항 연산자" %}

{% endtab %}
{% endtabs %}



