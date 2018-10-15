C300 - 쌍용 코란도C 모델에만 현재 펌웨어 있음

주광원

DRL & PSTN

LED 노란색 1개 있으면 1Chip

LED 노란색 4개가 일려로 붙어 있으면 4Chip Array



LED

3W(전력량) LED 를 전방 주광원 및 DRL로 주로 사용 (밝기 만족을 위해 와트가 높음)

RCL 및 후방 램프류는 0.5W LED를 사용

LED는 전류로 Control하며

LED를 제조시 밝기, 전압, 색깔에 따른 차이가 있음

| 명칭  | BIN 구분  | 내용                | 비고                                         |
| ----- | --------- | ------------------- | -------------------------------------------- |
| Flux  | Flux BIN  | 밝기 별로 묶음      | 소프트웨어적으로 제어필요                    |
| V~F~  | V~F~ BIN  | 구동 전압 별로 묶음 | 소프트웨어적으로 제어필요 - 저항이 있는 경우 |
| Color | Color BIN | 색상별로 묶음       | 같은 색깔이여도 육안으로 구분이 안됨         |

> IC - Integrated Circuit 집적회로로서 여러 독립된 요소를 집적해서 하나의 칩으로 만든 것
>
> V~F~ - Foward voltage

열저항 계수 

외부온도 x 열저항 계수 = 내부 온도

LED에 작동 온도범위가 있기 때문에 외부온도를 측정해서 내부온도를 알 수 있다.

LED  Spec.

작동온도 범위

보관온도 범위

BIN 코드 분류



Flux BIN이 같은 LED를 회로에 포함시키며 PWM방식으로 제어함

BIN Detect는 회로에 Voltage Divider를 통해 구분한다

![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Voltage_divider.svg/698px-Voltage_divider.svg.png)

 R1은 고정이고 LED BIN에 따라서 R2를 변경해서 맞춘다.

ex) Vin = 5V, R1 = 2kΩ, R2 = 2kΩ 이면 Vout = 2.5V 이다

Vin, R1은 LDM에 포함되는 부분이고 R2는 LAM에 포함되며 LAM에 장착된 LED BIN코드에 따라서 R2(BIN 저항)을 바뀜

전압차로 Flux BIN Detect해서 마이콤에서 읽어서 구별

Driver IC는 정전류 제어(Vf에 관계 없음)

자동차에서 사용하는 전압범위 9V ~ 16V이며 default 값은 13.5V

Boost는 전압 승압

Buck은 전압 강압

ex) C300 모델의 경우 DRL 전류 640mA, PSTN 64mA이며 2개의 신호가 들어올 시 DRL 신호를 우선시 한다.

DRL은 전류가 일정하게  640mA가 흐름 

PSTN의 경우 Max와 Min으로 전류를 반복적으로 흘러서 평균값을 64mA로 맞춘다

ADC를 통해 아날로그 값을 변수에 저장함 ex) 13.5v -> 0x000

main.c에서 

- BIN Detect (전압을 ADC를 통해 읽어서 감지함)
- LED 온도 체크
- 통신 부분 추가(SPI 시리얼 통신방법)
- 레지스트 값(드라이버 IC 컨트롤) - 스펙에 맞게 설정
- 통신포트가 추가로 달림
- 2CH(출력 갯수에 따라 다름)

> 레지스트 값 (홀수 페리티 - 오류 검출, 1bit - Read or Write, 4bit 주소값, 나머지 내용)

