# 11장. 모든 악의 근원
Money의 하위 클래스(Dollar, Franc)를 제거하고 필요 없어진 테스트를 정리했다.

- [x] testFrancMultiplication 제거

# 12장. 드디어, 더하기

이번 장에서는 통화가 다른 화폐간의 더하기에 앞서 더 작은 테스트로 먼저 수행했다.

- [ ] $5 + 10CHF = $10(환율이 2 : 1일 경우) ->  환율 전환
- [ ] `new` $5 + $5 = $10

### 다중통화 연산에 대한 고민
- 다중 통화 사용에 대한 내용을 시스템의 나머지 코드에 숨기고 싶다
- 가능한 방법으로 모든 내부값을 참조통화(달러라던지)로 전환할 수 있다.
  - cons. 여러 환율을 쓰기 쉽지 않다. (Franc:Won=1:2)
- 다른 해법?
- Money와 비슷하게 동작하지만 사실은 두 Money의 합을 나타내는 `객체` 생성
  - idea1. 지갑처럼 취급. 지갑에 여러 금액, 통화가 들어감.
  - [v] idea2. 수식처럼 취급. (2+3)*5. 연산이 끝나면 환율을 이용해 단일 통화로 축약한다.

다중 통화 사용에 대한 부분을 bank에게 넘겨주려고 함.

# 13장. 진짜로 만들기

- [ ] $5 + $5 에서 Money 반환하기
- [x] Bank.reduce(Money) -> 다형성 지원(Sum,Money) 테스트
- [ ] Money에 대한 통화 변환을 수행하는 Reduce
- [ ] Reduce(Bank, String)

# 14장. 바꾸기
환전을 수행하는 메서드를 생성하고   
Bank 객체에 rate 라는 환율 필드를 생성했다.

- [x] $5 + $5 = $10 -> 더하기의 작은 테스트 완성
- [x] Money에 대한 통화 변환을 수행하는 reduce 메서드 
- [x] reduce(Bank bank, String to) -> 메서드 파라미터를 통일

# 15장. 서로 다른 통화 더하기
달러와 프랑간 더하기 test case 성공함.
- [x] $5 + 10CHF = $10(환율이 2 : 1일 경우) ->  환율 전환
  - [ ] Sum.plus 구현하기
  - [ ] Expression.times 구현하기

# 16장. 드디어, 추상화
잠시 실험을 시도했는데 제대로 되지 않아서 버렸다.
- [x] ~~$5 + $5 에서 Money 반환하기~~ -> test failed.
- [x] Sum.plus 구현하기
- [x] Expression.times 구현하기

## 인상적인 문구
```
TDD로 구현할 땐 테스트 코드의 줄 수와 모델 코드의 줄 수가 거의 비슷한 상태로 끝난다.
TDD가 경제적이기 위해서는 매일 만들어 내는 코드의 줄 수가 두 배가 되거나 
동일한 기능을 구현하되 절반의 줄 수로 해내야 할 것이다.
TDD가 자신의 방법에 비해 어떻게 다른지 직접 측정해 보아야 할 것이다.
이 때 디버깅, 통합 작업, 다른 사람에게 설명하는 데 걸리는 시간 등의 요소를 반드시 포함해야 한다는 것을 기억하기 바란다.
```

# 17장. Money 회고

## 다음에 할일
- Sum.plus(), Money.plus() 사이의 코드 중복 정리 -> Expression 을 class로 수정하고 plus()를 구현한다.
- 린트 프로그램을 돌려본다
- 테스트 케이스를 추가한다.
- 설계를 검토한다. "할일 목록이 빌 때가 그때까지 설계한 것을 검토하기에 적절한 시기다."
  - 말과 개념이 서로 잘 통하는가?
  - 현재의 설계로는 제거하기 힘든 중복이 있는가?

## 메타포
### 메타포란?
- `문학` 은유, 비유. 행동, 개념, 물체 등이 지닌 특성을 그것과는 다르거나 상관없는 말로 대체하여, 간접적이며 암시적으로 나타내는 일.  
  네이버 국어사전
- 잘 모르거나 새로운 사물이나 개념을 이해하기 위해 잘 알고 친숙한 사물이나 개념에 빗대 표현하는 것을 메타포(metaphor)라고 한다. 컴퓨터 화면을 책상에 빗대 데스크탑이라 부르고 파일 삭제를 휴지통에 종이를 던지기에 빗대는 것이 그 예이다.  
  Robert C. Martin, 〖UML 실전에서는 이것만 쓴다〗, 이용원・정지호(역), 인사이트, 2013년, p.13

저자는 Wallet에서 Expression 라는 메타포를 사용하면서 설계가 좋아졌다고 함.  
구현을 수십번 다시 하는 것보다 더 잘 들어맞는 메타포를 고민하는게 낫다는 뜻으로 이해했다.

Wallet(지갑)
- Money의 집합이 딱 떨어지는 숫자로 된다는걸 암시.  
  2USD+5CHF+3USD = 4USD + 5CHF

Expression(수식)
- Wallet과 마찬가지로, 같은 통화는 합칠 수 있다.
- 코드도 더 명확해졌다. (plus, times 같은 method가 들어가도 어색하지 않음)

## JUnit 사용도
1-16장까지 125번 눌렀다. 매 챕터당 평균 7.8125회 실행했다.

## 코드 메트릭스
테스트 코드 라인수(89 line)와 실제 코드의 라인수(91 line)가 비슷하다. 
method당 line수가 실제 코드 4.1, test code 5.9로 그리 길지 않다.(선언부, 닫는 괄호 포함)
test code의 line수는 공통된 테스트 fixture를 뽑아내면 줄일 수 있다.

## 프로세스
TDD의 주기
- 작은 테스트를 추가한다.
- 모든 테스트를 실행하고, 실패하는 것을 확인한다.
- 코드에 변화를 준다.
- 모든 테스트를 실행하고, 성공하는 것을 확인한다.
- 중복을 제거하기 위해 리팩토링한다.

## 테스트의 질
TDD가 커버할 수 없는 부분
- 성능 테스트
- 스트레스 테스트
- 사용성 테스트

그렇지만, TDD 코드의 결함 밀도가 충분히 낮다면 "실수를 감지"하는것뿐만 아니라 "의사소통 증폭기"의 역할도 수행 가능하다.

책에서 말하는 의사소통이란
- "시스템이 무엇을 해야 하는지에 대해 일반적으로 어떤 느낌을 갖고 있는 사람들과  
  시스템이 실제로 그 일을 하도록 만들 사람들 간의 의사소통" - p.155
- 실제 코드가 어떻게 돌아가는지에 대한 가이드 역할이라고 이해함.

테스트 커버리지를 높이려면?
- 테스트 코드 갯수를 늘려서 모든 경우의 수를 다 커버하도록 하는 방법도 있지만 
- 프로그램의 로직을 단순화하는 방법도 있다. (ex. 리팩토링)

## 개인적인 소감
- 실제 method를 구현하기 전에 없는 메서드를 상상하면서 test code로 작성하고 구현에 들어가더라
- 저자가 메타포가 너무 좋은지 챕터 제목도 비유, 설명도 비유를 쓰는데 번역되어오면서 그 비유를 이해할만큼 충분한 설명이 되지 않은 것 같다.
  - 그래서 삼각측량은 뭘까
- 일단 눈에 밟히는건 todo 에 추가하고 넘어가는 것은 쓸만한 것 같다.