# XUnit으로 가는 첫걸음
## 테스트 프레임워크에 대한 할일 목록
* 테스트 메서드 호출하기
* 먼저 setUp 호출하기
* 나중에 tearDown 호출하기
* 테스트 메서드가 실패하더라도 tearDown 호출하기
* 여러 개의 테스트 실행하기
* 수집된 결과를 출력하기

## 첫번째 작은 단계는 아직 프레임워크가 없기 때문에 수동으로 테스트 케이스를 검증하자.
클래스를 정의하기 전에 테스트 코드부터 작성하기
클래스와 메서드를 정의하고 리팩토링 진행하기

## 리팩토링의 일반적인 패턴
하나의 특별한 사례에 대해서만 작동하는 코드를 가져다가 다른 여러 사례에 대해서도 작동할 수 있도록 상수를 변수로 변화시켜 일반화하는 것

일단 한 번만 수동으로 검증하면 앞으로는 이 과정을 자동화할 수 있다. 
- 하드코딩을 한 다음에 상수를 변수로 대체하여 일반성을 이끌어내는 방식으로 기능을 구현했다.
- Plugubble selector를 사용

부트스트랩: to load a program into a computer using a much smaller initial program to load in the desired program (which is usually an operating system)
플러거블 셀렉터(pluggable selector)란 Replace subclasses with dynamically generated method calls. 장점은 객체 별로 서로다른 메서드가 동적으로 호출되게 함으로써 필요 없는 하위클래스의 생성을 피한다. (run메서드를 의미하는 듯)

# 테이블 차리기
테스트를 작성하다보면 공통된 패턴을 발견하게 된다. 
* 준비(arrange): 객체를 생성
* 행동(act): 어떠한 자극을 준다.
* 확인(assert): 결과를 검사한다.

# 실패 처리하기
테스트가 작동하도록 하려면 예외를 잡아야하고 현재까지의 구현에서는 예외가 보고되지 않기 때문에 이를 위한 작업 진행.
테스트 결과를 반환해주는 클래스를 만들고 n개 성공 n개 실패라는 결과문을 봔환해줌.
 
