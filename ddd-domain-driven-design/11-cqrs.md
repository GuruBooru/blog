# 11장 CQRS

## 단일 모델의 단점

* 어떤 기능을 구현하기 위해서는 여러 애그리거트에서 데이터를 가져와야 할 경우가 생긴다.
* 조회의 경우 특성 상 속도가 빠를수록 좋은데, 여러 애그리거트에서 데이터를 가져올 경우, 구현 방법에 대해서 고민해야 한다.
* ID를 이용해서 애그리거트를 참조하는 방식을 사용하면, 즉시 로딩과 같은 최적화 기능을 사용하기 어려워질 수 있어 이는 조회 속도에 문제가 생길 수 있다.
* 애그리거트 간 직접 참조하는 방식을 사용한다면, 조회 화면의 특성에 따라 같은 연관도 즉시 로딩이나 지연 로딩으로 처리해야 하기 때문에 경우에 따라 프레임워크가 제공하는 기능을 사용하지 못할 수 있다.
* 객체 지향으로 도메인 모델을 구현할 때 주로 사용하는 ORM 기법은 도메인의 상태 변경을 구현하는데는 적합하지만, 여러 애그리거트에서 데이터를 가져와 출력하는 기능을 구현하기에는 고려할 것들이 많아 구현이 복잡해진다.

## CQRS \(Command Query Responsibility Segregation\)

* 상태 변경을 위한 모델과 조회를 위한 모델을 분리하는 패턴
* 상태 변경의 경우 주로 한 애그리거트의 상태를 변경 조회의 경우 여러 애그리거트에서 데이터를 조회하는 경우가 종종 있음
* 상태 변경 범위와 상태 조회 범위가 정확하게 일치하지 않기 때문에 단일 모델로 두 종류의 기능을 구현하면 모델이 불필요하게 복잡해짐 
* 복잡한 도메인에 적합한 패턴
  * 복잡할수록 변경과 조회 기능에 대한 데이터 범위에 차이가 발생
  * 두 기능을 단일 모델로 처리하게 되면 조회 기능의 로딩 속도를 위해 모델 구현이 필요 이상으로 복잡해지는 문제 
* 명령 모델, 조회 모델에 맞는 구현 기술을 선택하여 구현 가능
* 두 모델이 서로 다른 데이터 저장소를 사용할 수 있음

  * 이 경우 이벤트를 활용하여 데이터 동기화 처리
  * 명령 모델에서 상태 변경 시 이에 해당하는 이벤트 발생, 이벤트를 조회 모델에 전달하여 변경 내역 반영
  * 데이터 동기화 시점에 따라 구현 방식이 달라질 수 있음
    * 데이터가 바뀌자마자 변경 내역을 조회 모델에 반영 시 동기 이벤트와 글로벌 트랜잭션 사용하여 실시간 동기화 → 전반적인 성능이 떨어지는 단점
    * 특정 시간 안에만 동기화 시 비동기로 데이터 전송

* CQRS 패턴을 적용하기 위해 반드시 사용해야 하는 기술이 존재하는 것은 아님

### 웹과 CQRS

* 일반적인 웹 서비스에서 상태를 변경하는 요청보다 조회하는 요청이 더 많음
* 따라서 조회 성능을 높이기 위해 다양한 기법 사용

  1. 쿼리 최적화
  2. 메모리에 조회 데이터 캐시
  3. 조회 전용 저장소 사용

  이러한 다양한 기법을 사용하는 것은 `결과적으로 CQRS를 적용하는 것과 같은 효과`

  1. 쿼리 최적화  : 조회 화면에 보여질 데이터를 빠르게 읽어 올 수 있도록 쿼리 작성 
  2. 메모리에 캐시 : DB에 보관된 데이터를 그대로 저장하기 보단 화면에 맞는 모양으로 저장 

* `조회 속도를 높이기 위해 별도 처리`를 하고 있다면, `명시적으로 명령 모델과 조회 모델을 구분`
  * 조회 기능으로 인해 명령 모델이 복잡해지는 것을 방지
  * 명령 모델에 관계 없이 조회 기능에 특화된 구현 기법을 보다 쉽게 적용

### CQRS 장단점

* 장점
  * 명령 모델을 구현할 때 도메인 자체에 집중할 수 있음
  * 조회 성능 향상에 유리 
* 단점
  * 구현해야 할 코드가 더 많음
    * 단일 모델을 사용할 때 발생하는 복잡함에 따른 구현 비용과 조회 전용 모델을 만들면서 나오는 비용을 따져봐야 함
  * 더 많은 구현 기술 필요
    * 명령 모델과 조회 모델을 다른 구현 기술을 사용하여 구현할 수 있는 만큼, 사용해야 할 기술이 더 많이 필요할 수 있음 
* 위에 장단점을 고려하여 CQRS 패턴을 도입할지 여부를 결정해야함
* 도메인이 복잡하지 않은데 CQRS를 도입하게 되면,  두 모델을 유지하는 비용만 높아지고, 얻을 수 있는 이점은 없음
