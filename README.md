# 음주측정smartkey

## 목차

[1.프로젝트 목적](#프로젝트-목적)

[2.조원](#조원)

[3.개발 환경](#개발-환경)

[4.작동 원리](#작동-원리)

[5.사용 부품](#사용-부품)

[6.코드](#코드)

[7.결과](#결과)



## 프로젝트 목적

* 음주운전 사고를 우리가 제작한 음주측정 스마트키로 사전에 방지한다.

## 조원

이원균, 조은영, 최종일, 하성혁
* 이원균 : 차량 SW 개발
* 조은영 : 기술 조사, 부품 선정
* 최종일 : 알고리즘 순서도 작성, 차량 하드웨어제작
* 하성혁 : 차량 SW개발
  
## 개발 환경

<br/>

* Arduino IDE
* Fritzing

<br/>

## 작동 원리

<br/>

<img src="https://github.com/bellday/smartkey/assets/92672351/3feea71f-1c90-4a90-9555-cb8033cd2900" width="450px" height="600px"  alt="설계도면"></img><br/>

<br/>

## 사용 부품

* 설계도면
  
<img src="https://github.com/bellday/smartkey/assets/92672351/b562822c-030e-487a-9642-bd899a0cd407" width="450px" height="300px"  alt="설계도면"></img><br/>


* 스마트키
  
<img src="https://github.com/bellday/smartkey/assets/92672351/0c549258-38ee-48b2-a60d-6491e5223e7f" width="450px" height="300px"  alt="스마트키"></img>

#### 스마트키에 사용된 부품

<br/>

----

1. 블루투스 센서(HM-10)

2. 심박 측정 센서 (SZH-SSBH-035)

3. 아두이노 Uno 보드

4. 조이스틱 모듈

----

<br/>

* RC카
  
<img src="https://github.com/bellday/smartkey/assets/92672351/0542c334-d6b6-43e3-ad8a-27d87ee09d2b" width="450px" height="300px"  alt="RC카"></img>

---

#### RC카에 사용된 부품

<br/>

1. 음주측정 센서(MQ-3)

2. 블루투스 센서(HM-10)

3. 아두이노 Uno 보드

4. LCD

5. LED

<br/>

## 코드

<br/>

* 스마트키 내부의 심박 센서를 통해 음주여부를 판단

<br/>

### 심박수 측정 코드 

<pre>
<code>
int myBPM = pulseSensor.getBeatsPerMinute();
  if (btn1 == 0) {
    delay(1000);
    sum = 0;
    avg = 0;
    for (int i = 0; i < 20; i++) {
      int myBPM = pulseSensor.getBeatsPerMinute();

      sum = sum + myBPM;
      delay(200);
    }

    delay(1000);

  }

  avg = sum / 20; //심박수 평균

  if (avg >= 30 && avg <= 150) {
    lcd.clear();
    lcd.setCursor(0, 0);          // 첫번째 줄 문자열 출력
    lcd.print("BPM : ");
    lcd.print(avg);
    lcd.display();

  }

  else {
    lcd.setCursor(0, 0);          // 첫번째 줄 문자열 출력
    lcd.print("BPM NOT ESTIMATE");
    lcd.setCursor(0, 1);          // 첫번째 줄 문자열 출력
    lcd.display();

  }

  Serial.println(avg);
</code>
</pre>

### 알코올 측정

<br/>

* RC car내부의 음주측정센서(MQ-3)를 통해 음주여부를 확인
  
<br/>

<pre>
<code>
 int alco_value = analogRead(alco_pin); //alcohol senser pin read

      digitalWrite(LED_B, HIGH);     // LED blue
      digitalWrite(LED_G, LOW);
      digitalWrite(LED_R, LOW);
      delay(500);
      

      Serial.println(analogRead(alco_pin));

      //범위 알아서 지정
      if (alco_value < 100) { //alcohol sensor value is normal, drive RC car
        digitalWrite(LED_G, HIGH);     //LED green
        digitalWrite(LED_B, LOW);
        digitalWrite(LED_R, LOW);
        drive(pwmL, pwmR);
      }

      else {
        digitalWrite(LED_R, HIGH);      //LED red
        digitalWrite(LED_G, LOW);
        digitalWrite(LED_B, LOW);

      }
</code>
</pre>

## 결과

### 결과사진

<img src="https://github.com/bellday/smartkey/assets/92672351/c89f374d-eb46-42a4-949a-320744e08408" width="450px" height="300px"  alt="스마트키"></img>

### 테스트 결과

<img src="https://github.com/bellday/smartkey/assets/92672351/c797dc2c-3433-4b61-80b6-a1d77ab066eb" width="450px" height="300px"  alt="스마트키"></img>



