# Date

> 표준 빌드인 객체인 Date는 날짜와 시간 (연, 월, 일, 시, 분, 초, 밀리초)을 위한 메서드를 제공하는 빌트인 객체이면서 생성자함수이다.  

- UTC(협정 세계시 Coordinated Universal Time)은 국제 표준시를 말한다.
- GMT(그리니치 평균시 Greenwich Mean Time)로 불리기도 한다.
- UTC와 GMT는 초의 소수점 단위에서만 차이가 나기때문에 일상에서는 혼용되어 사용.
- 현재 날짜와 시간은 자바스크립트 코드가 실행된 시스템의 시계에 의해 결정된다.

## 30-1. Date 생성자 함수

> Date는 생성자 함수다.  
> Date 생성자 함수로 생성한 Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖는다.  
> 모든 시간의 기점인 1970년 1월 1일 0시를 나타내는 Date 객체는 내부적으로 정수값 0을 가진다.  
> 생성자 함수로 객체를 생성하는 방법은 4가지가 있다.

### 30-1-1. new Date()

- 인수 없이 new연산자와 함께 호출하면 현재 날짜와 시간을 가지는 Date객체를 반환한다.
- 객체는 내부적으로 정수값을 갖지만 출력 시에는 날짜와 시간 정보를 출력한다.
- new연산자 없이 호출 시에는 날짜와 시간 정보를 나타내는 문자열을 반환한다.

### 30-1-2. new Date(milliseconds)

- 숫자 타입의 밀리초를 인수로 정달하면 1970년 1월 1일 00:00:00(UTC)를 기점으로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체를 반환한다.

### 30-1-3. new Date(dateString)

- 생성자 함수에 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date객체를 반환.
- 이때 전달한 문자열은 Date.parse 메서드에 의해 해석 가능한 형식이어야 한다.

### 30-1-4. new Date(year, month[, day, minute, second, millisecond])

#### Date 객체를 만드는 여러가지 방법

```javascript
let today = new Date()
let birthday = new Date('December 17, 1995 03:24:00')
let birthday = new Date('1995-12-17T03:24:00')
let birthday = new Date(1995, 11, 17)            // 월은 0부터 시작
let birthday = new Date(1995, 11, 17, 3, 24, 0)
```
#### 두 자리 연도는 1900년대로
Date의 연도에 0부터 99까지의 정수를 제공하면 1900부터 1999로 처리합니다. 다른 모든 값은 그대로 사용합니다.

1900년대가 아닌, 실제 0 ~ 99년을 지정해야 하면 Date.prototype.setFullYear()와 Date.prototype.getFullYear() 메서드를 사용해야 합니다.

```javascript
let date = new Date(98, 1)  // Sun Feb 01 1998 00:00:00 GMT+0900 (대한민국 표준시)

// 구형 메서드: 여기서도 98을 1998로 처리
date.setYear(98)            // Sun Feb 01 1998 00:00:00 GMT+0900 (대한민국 표준시)

date.setFullYear(98)        // Sat Feb 01 0098 00:00:00 GMT+0827 (대한민국 표준시)

```

#### 경과시간 계산

연, 월, 일(서머타임)의 길이가 계속해서 달라지므로, 두 시간의 간격을 시/분/초보다 큰 단위로 나타낼 땐 여러가지 문제가 생기므로 이 방법을 시도하기 전에 관련 문제를 먼저 자세히 알아보세요.

```javascript
// Date 객체 사용법
let start = Date.now()

// 시간이 오래 걸리는 어떤 작업
doSomethingForALongTime()
let end = Date.now()
let elapsed = end - start // 밀리초로 나타낸 경과시간

// 내장 메서드 사용법
let start = new Date()

// 시간이 오래 걸리는 어떤 작업
doSomethingForALongTime()
let end = new Date()
let elapsed = end.getTime() - start.getTime() // 밀리초로 나타낸 경과시간

// 임의의 함수를 테스트하고, 호출에 걸린 시간을 출력하려면
function printElapsedTime(fTest) {
  let nStartTime = Date.now(),
      vReturn = fTest(),
      nEndTime = Date.now()

  console.log(`Elapsed time: ${ String(nEndTime - nStartTime) } milliseconds`)
  return vReturn
}

let yourFunctionReturn = printElapsedTime(yourFunction)

```
> 참고: Web Performance API (en-US)의 고해상도 시간 기능을 지원하는 브라우저에서는 Performance.now()를 사용해서 Date.now()보다 더 안정적이고 정확한 경과 시간을 알아낼 수 있습니다.

#### ECMAScript 시간으로부터 경과한 시간을 초 단위로 가져오기

```javascript
let seconds = Math.floor(Date.now() / 1000)
```
여기서는 정수만 반환하는 것이 중요하므로, 단순히 나누기만 해서는 충분하지 않습니다. 그리고 실제로 "지나간" 초를 반환해야 하므로 Math.round()를 사용하지 않고 Math.floor()를 사용합니다.

## 30-2. Date method

### 30-2-1. 정적 메서드

#### Date.now()
1970년 1월 1일 00:00:00 UTC로부터 지난 시간을 밀리초 단위의 숫자 값으로 반환합니다. 윤초는 무시합니다.

#### Date.parse()
날짜를 나타내는 문자열을 분석한 후, 해당 날짜와 1970년 1월 1일 00:00:00 UTC의 시간 차이를 밀리초 단위의 숫자 값으로 반환합니다.

> Date.parse()를 사용한 날짜 분석은 브라우저 간 차이 및 일관적이지 못한 동작을 가지고 있으므로 사용하지 않는 것이 좋다.

#### Date.UTC()
생성자가 받을 수 있는 제일 많은 매개변수(구성요소 각각, 2개 ~ 7개)를 동일하게 받아서, 1970년 1월 1일 00:00:00 UTC의 시간 차이를 밀리초 단위의 숫자 값으로 반환합니다. 윤초는 무시합니다.

### 30-2-2. 인스턴스 메서드

#### Date.prototype.getDate()
Date에서 현지 시간 기준 일(1–31)을 반환합니다.

#### Date.prototype.getDay()
Date에서 현지 시간 기준 요일(0–6)을 반환합니다.

#### Date.prototype.getFullYear()
Date에서 현지 시간 기준 연도(네 자리 연도면 네 자리로)를 반환합니다.

#### Date.prototype.getHours()
Date에서 현지 시간 기준 시(0–23)를 반환합니다.

#### Date.prototype.getMilliseconds()
Date에서 현지 시간 기준 밀리초(0–999)를 반환합니다.

#### Date.prototype.getMinutes()
Date에서 현지 시간 기준 분(0–59)을 반환합니다.

#### Date.prototype.getMonth()
Date에서 현지 시간 기준 월(0–11)을 반환합니다.

#### Date.prototype.getSeconds()
Date에서 현지 시간 기준 초(0–59)를 반환합니다.

#### Date.prototype.getTime()
1970년 1월 1일 00:00:00 UTC로부터의 경과시간을 밀리초 단위로 반환합니다. Date가 기준 시간 이전을 나타낼 경우 음수 값을 반환합니다.

#### Date.prototype.getTimezoneOffset()
현지 시간대와 UTC의 차이를 분 단위로 반환합니다.

#### Date.prototype.getUTCDate()
Date에서 국제 시간 기준 일(1–31)을 반환합니다.

#### Date.prototype.getUTCDay()
Date에서 국제 시간 기준 요일(0–6)을 반환합니다.

#### Date.prototype.getUTCFullYear()
Date에서 국제 시간 기준 연도(네 자리 연도면 네 자리로)를 반환합니다.

#### Date.prototype.getUTCHours()
Date에서 국제 시간 기준 시(0–23)를 반환합니다.

#### Date.prototype.getUTCMilliseconds()
Date에서 국제 시간 기준 밀리초(0–999)를 반환합니다.

#### Date.prototype.getUTCMinutes()
Date에서 국제 시간 기준 분(0–59)을 반환합니다.

#### Date.prototype.getUTCMonth()
Date에서 국제 시간 기준 월(0–11)을 반환합니다.

#### Date.prototype.getUTCSeconds()
Date에서 국제 시간 기준 초(0–59)를 반환합니다.

#### Date.prototype.setDate()
현지 시간 기준으로 일을 설정합니다.

#### Date.prototype.setFullYear()
현지 시간 기준으로 연도(네 자리 연도면 네 자리로)를 설정합니다.

#### Date.prototype.setHours()
현지 시간 기준으로 시를 설정합니다.

#### Date.prototype.setMilliseconds()
현지 시간 기준으로 밀리초를 설정합니다.

#### Date.prototype.setMinutes()
현지 시간 기준으로 분을 설정합니다.

#### Date.prototype.setMonth()
현지 시간 기준으로 월을 설정합니다.

#### Date.prototype.setSeconds()
현지 시간 기준으로 초를 설정합니다.

#### Date.prototype.setTime()
Date가 나타낼 시간을 1970년 1월 1일 00:00:00 UTC로부터의 경과시간(밀리초)으로 설정합니다. 기준 이전의 시간은 음수 값을 사용해 설정할 수 있습니다.

#### Date.prototype.setUTCDate()
국제 시간 기준으로 일을 설정합니다.

#### Date.prototype.setUTCFullYear()
국제 시간 기준으로 연도(네 자리 연도면 네 자리로)를 설정합니다.

#### Date.prototype.setUTCHours()
국제 시간 기준으로 시를 설정합니다.

#### Date.prototype.setUTCMilliseconds()
국제 시간 기준으로 밀리초를 설정합니다.

#### Date.prototype.setUTCMinutes()
국제 시간 기준으로 분을 설정합니다.

#### Date.prototype.setUTCMonth()
국제 시간 기준으로 월을 설정합니다.

#### Date.prototype.setUTCSeconds()
국제 시간 기준으로 초를 설정합니다.

#### Date.prototype.toDateString()
Date의 날짜 부분만 나타내는, 사람이 읽을 수 있는 문자열을 반환합니다.

#### Date.prototype.toISOString()
Date를 나타내는 문자열을 ISO 8601 확장 형식에 맞춰 반환합니다.

#### Date.prototype.toJSON()
toISOString()을 사용해서 Date를 나타내는 문자열을 반환합니다. JSON.stringify()에서 사용합니다.

#### Date.prototype.toLocaleDateString() (en-US)
Date의 날짜 부분을 나타내는 문자열을 시스템에 설정된 현재 지역의 형식으로 반환합니다.

#### Date.prototype.toLocaleFormat()
형식 문자열을 사용해서 Date를 나타내는 문자열을 생성합니다.

#### Date.prototype.toLocaleString()
Date를 나타내는 문자열을 현재 지역의 형식으로 반환합니다. Object.prototype.toLocaleString() 메서드를 재정의합니다.

#### Date.prototype.toLocaleTimeString() (en-US)
Date의 시간 부분을 나타내는 문자열을 시스템에 설정된 현재 지역의 형식으로 반환합니다.

#### Date.prototype.toString()
Date를 나타내는 시간 문자열을 반환합니다. Object.prototype.toString() 메서드를 재정의합니다.

#### Date.prototype.toTimeString() (en-US)
Date의 시간 부분만 나타내는, 사람이 읽을 수 있는 문자열을 반환합니다.

#### Date.prototype.toUTCString() (en-US)
Date를 나타내는 문자열을 UTC 기준으로 반환합니다.

#### Date.prototype.valueOf()
Date 객체의 원시 값을 반환합니다. Object.prototype.valueOf() 메서드를 재정의합니다.

