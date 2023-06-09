# A게임과 B게임의 신규가입자 매출 성능 비교

## :sunny: 소개
- 최근 출시한 A게임과 B게임의 **매출과 관련된 지표**를 통해 **매출의 성능을 평가**하고자 합니다.
- 각 게임의 매출 성능 **차이에 가장 큰 영향을 준 사항**은 무엇인지 파악해 보고자 합니다.
- 각 게임에서 매출을 **상승시킬 수 있는 전략**을 찾아보고자 합니다.

<br/>

## :sunny: 두 게임의 매출 지표 분석 
### 1) 전체기간 PUR, ARPU, ARPPU 비교

![image](https://user-images.githubusercontent.com/56102116/225817051-e57e9dd3-1a4d-4abc-ae3a-d7c45912ef2a.png)

- PUR은 두 게임 **모두 약 1%** 로 미미한 수준입니다. 실제 구매자수를 늘릴 필요가 있습니다.
- ARPU는 A게임보다 **B게임이 더 높게** 나타났는데 **가입자의 구매 성향은 B게임이 더 높다**는 것을 나타냅니다.
- ARPPU는 B게임보다 **A게임이 더 높게** 나타났는데 **실제 구매자의 구매 성향은 A게임이 더 높다**는 것을 의미합니다.
- A게임과 B게임 **모두 ARPU보다 ARPPU가 더 크게** 나타납니다. 두 게임 **모두 소수의 충성도 높은 고객에 의해 대부분의 매출**이 발생합니다.

<br/>
<br/>

### 2) 월별 ARPU 비교

![image](https://user-images.githubusercontent.com/56102116/226151834-ace283a1-2415-47c0-8c31-a9c402c0901c.png)

- **A게임의 ARPU는 계속해서 상승**하고 있는 반면에 **B게임은 상승하다가 21.01에 갑자기 하락**했습니다.
- 월별 매출액과 월별 가입자수를 자세히 살펴볼 필요가 있습니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/225843724-53cd6e87-cf7e-4479-a28d-b9dc3544bca3.png)

- 매출액은 **계속해서 증가**하고 있습니다.
- 가입자수는 20.11에 감소했지만 다시 증가하고 있습니다.
- **가입자수 증가율보다 매출액 증가율이 더 크므로** ARPU가 상승하고 있음을 알 수 있습니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/225843810-115436cc-a687-48e2-a918-441c808f17b1.png)

- 매출액은 **증가하는 추세**를 보이다가 21.01 소폭 하락했습니다.
- 가입자수는 줄어드는 추세를 보이다가 **21.01에 갑자기 급증**했습니다.
- 21.01에 가입자수가 갑자기 급증한 원인을 알아볼 필요가 있습니다.

<br/>
<br/>

### 3) 월별 ARPPU 비교

![image](https://user-images.githubusercontent.com/56102116/225844611-c49fb582-34e0-4214-bab9-cad8d0875d2c.png)

- **A게임의 ARPPU는 계속해서 상승**하고 있는 반면에 **B게임은 상승하다가 21.01에 갑자기 하락**했습니다.(ARPU와 동일한 패턴)
- 월별 매출액과 월별 구매자수를 자세히 살펴볼 필요가 있습니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/225845028-64dbe398-a2cc-42bb-8c9a-086a2ef47384.png)

- 매출액과 구매자수 **모두 증가하는 추세**를 보입니다.
- **구매자수 증가율 보다 매출액 증가율이 더 크므로** ARPPU가 상승하고 있음을 알 수 있습니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/225845308-b27c2387-3b28-4427-a4de-edfe8e6d5a7b.png)

- 매출액은 증가하는 추세를 보이다가 21.01에 소폭 하락했습니다.
- 구매자수는 감소하는 추세를 보이다가 21.01에 상승했습니다.
- **매출액과 구매자수의 증감이 서로 다르게** 나타나고 있으므로 자세히 살펴볼 필요가 있습니다.

<br/>
<br/>

### 4) 리텐션(Retention) 분석
**첫 결제일**을 기반으로 월별 리텐션을 분석했습니다.

![image](https://user-images.githubusercontent.com/56102116/226155641-7dc5eda8-4cf2-40e9-80b7-e44a0f834293.png)

- **모든 월(10월, 11월, 12월, 1월)** 에서 **첫 달 평균결제액(0 Month)보다 마지막 달 평균 결제액이 더 높게** 나타났습니다.
- A게임의 구매자들은 **재 결제 비율이 계속해서 상승** 하고 있습니다.
- **첫 달 평균결제액(0 Month)** 은 147,490원 -> 71,645원 -> 94,073원 -> 105,828원으로 **감소했다가 다시 상승**하는 추세를 보입니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/226155683-79e755f6-e2d0-4224-9843-baa66505f3b3.png)

- 20.10이 첫 구매월인 집단은 월 평균결제액이 **계속해서 감소** 하고 있습니다.
- 20.11이 첫 구매월인 집단은 89,384원 -> 110,251원 -> 85,150원으로 **상승했다가 감소** 하고 있습니다.
- 20.12이 첫 구매월인 집단은 76,746원 -> 98,372원으로 **상승** 했습니다.
- B게임의 구매자들은 **재 결제 비율은 집단별로 다르게** 나타나고 있습니다.
- **첫 달 평균결제액(0 Month)** 은 112,064원 -> 89,384원 -> 76,746원 -> 58,957원으로 **계속해서 감소**하고 있습니다.
- 첫 달 평균결제액이 감소하는 이유를 분석해볼 필요가 있습니다.

<br/>
<br/>

## :sunny: 두 게임 매출의 영향을 준 세부요인분석
### 1) 국가별 매출액 비교

![image](https://user-images.githubusercontent.com/56102116/226160664-e7ce0b6e-ecf8-4fac-b6aa-97f5d40a92a6.png)

- 두 게임 **모두 S국가에서 매출이 가장 높게** 나타났습니다.
- 두 게임 **모두 S, F, Z, ETC 순**으로 높게 나타났습니다.

<br/>
<br/>

### 2) 매출 상위 4개국가(S, F, Z, ETC) 첫 접속 당시 미디어별 매출 비교

![image](https://user-images.githubusercontent.com/56102116/226160733-6cc9f459-66dc-4b2d-99f8-8e6924486c21.png)

- A게임은 **Organic(13점), Google(11점), Facebook(6점), ADNW(5점) 순**으로 매출이 높은것으로 나타났습니다.(순위별로 차등 점수 부여)
- B게임은 **Organic(16점), Google(8점), Facebook(6점), ADNW(4점) 순**으로 매출이 높은것으로 나타났습니다.(순위별로 차등 점수 부여)

<br/>
<br/>

### 3) 매출 상위 4개국가(S, F, Z, ETC)의 첫 접속 당시 OS별 매출 비교

![image](https://user-images.githubusercontent.com/56102116/226160986-65b83c40-4491-4f58-927b-d729e1837879.png)

- A게임은 **Android(7점), Ios(5점) 순**으로 매출이 높게 나타났습니다.(순위별로 점수 차등 부여)
- B게임은 **Android(8점), Ios(4점) 순**으로 매출이 높게 나타났습니다.(순위별로 점수 차등 부여)

<br/>
<br/>

### 4) 매출 상위 4개국가(S, F, Z, ETC) ARPU, ARPPU 비교

![image](https://user-images.githubusercontent.com/56102116/226163294-53cbcf8a-04fb-4e60-aaf3-fa4f97afa2a0.png)

- **전체 매출**은 Z국가보다 **F국가가 더 높지만**, **ARPU와 ARPPU**는 F국가보다 **Z국가가 더 높게** 나타났습니다.
- **Z국가에는 소수의 충성도 높은 고객**을 상대로 하는 전략이 필요합니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/226163333-6eea794e-4890-43eb-92e1-6f5bd5168d90.png)

- **전체 매출**은 Z국가보다 **F국가가 더 높지만**, **ARPU와 ARPPU**는 F국가보다 **Z국가가 더 높게** 나타났습니다.
- **Z국가에는 소수의 충성도 높은 고객**을 상대로 하는 전략이 필요합니다.

<br/>
<br/>

## :sunny: 각 게임에서 매출을 상승시킬 수 있는 전략 분석
### 1) 고객별 RFM 분석
- Recency(A, B, C), Frequency(A, B, C), Money(A, B, C)를 나누어 총 **9가지 집단**으로 분류했습니다.
- 각 **카테고리별로 데이터 분포를 확인**하여 등급 간 분류 기준을 선정했습니다.
- 각 **집단별로 다른 정책이 필요**합니다.
- **A게임은 상위 50명이, B게임은 상위 34명이 전체 매출액의 33%를 차지**합니다. 소수의 충성도 높은 고객의 특별 관리가 필요합니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/226164052-ae9a4919-3b4a-4b02-aa0f-5791b6063335.png)

- Recency는 A등급(1 ~ 18일), B등급(19 ~ 56일), C등급(57 ~ 123일)
- Frequency는 A등급(7 ~ 670회), B등급(3 ~ 6회), C등급(1 ~ 2회)
- Money는 A등급(17,967,900 ~ 148,023,900원), B등급(2,801,100 ~ 17,464,800원), C등급(1,800 ~ 2,795,400
원)
- AAA등급을 받은 유저에게는 **N개를 사면 1개를 더 증정**하는 로열티 정책이 필요합니다.
- ACC등급을 받은 유저에게는 **첫 결제 구매 이벤트** 정책이 필요합니다.
- CAA등급을 받은 유저에게는 **컴백 이벤트** 정책이 필요합니다.
- CCB등급을 받은 유저에게는 **가격 할인 이벤트** 정책이 필요합니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/226164750-eb1ca5b5-3289-4f72-9182-6a1027563d15.png)

- Recency는 A등급(1 ~ 37일), B등급(38 ~ 95일), C등급(96 ~ 123일)
- Frequency는 A등급(6 ~ 956회), B등급(2 ~ 5회), C등급(1회)
- Money는 A등급(24,955,200 ~ 177,168,600원), B등급(3,294,000 ~ 24,827,400원), C등급(1,800 ~ 3,290,400원)
- AAA등급을 받은 유저에게는 **N개를 사면 1개를 더 증정**하는 로열티 정책이 필요합니다.
- ACC등급을 받은 유저에게는 **첫 결제 구매 이벤트** 정책이 필요합니다.
- CAA등급을 받은 유저에게는 **컴백 이벤트** 정책이 필요합니다.
- CCB등급을 받은 유저에게는 **가격 할인 이벤트** 정책이 필요합니다.

<br/>
<br/>

### 2) 특정 상품 주문시 함께 가장 많이 주문된 다른 상품 분석
- **같이 잘 팔리는 상품은 세트상품 판매 정책**으로 매출의 상승을 기대할 수 있습니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/226165151-c70d1bbf-0a6e-47df-95fb-54b30c677e60.png)

- **상품412번&상품95번, 상품808번&상품24번, 상품65번&상품24번** 등 **묶음 할인 정책**을 통해 매출 상승을 기대할 수 있습니다.

<br/>
<br/>

![image](https://user-images.githubusercontent.com/56102116/226165248-20763264-bfe7-48de-bbf1-2f4ca7a14a34.png)

- **상품807번&상품423번, 상품566번&상품541번, 상품66번&상품541번** 등 **묶음 할인 정책**을 통해 매출 상승을 기대할 수 있습니다.

<br/>
<br/>



