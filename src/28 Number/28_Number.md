표준 빌트인 객체인 `Number` 는 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공한다.

## 1. Number 생성자 함수

Number 객체는 생성자 함수 개체다. 따라서 new 연산자와 함께 호출하여 Number 인스턴스를 생성 할 수 있다.

```
const numObj = new Number();

console.log(numObj);
```

Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.

```
const numObj = new Number();
console.log(numObj); // Number { [[PrimitiveValue]]: 0 }

const numObj = new Number(10);
console.log(numObj); // Number { [[PrimitiveValue]]: 10 }
```

Number 생성자 함수의 인수로 숫자가 아닌 값을 전달하면 인수를 숫자로 강제 변환한다.

```
const numbObj2 = new Number(`10`);
console.log(numObj); // Number { [[PrimitiveValue]]: 10 }

const numbObj3 = new Number(`Hi`);
console.log(numObj); // Number { [[PrimitiveValue]]: NaN }
```

new 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 Number 인스턴스가 아닌 숫자를 반환한다. 이를 이용해서 명시적으로 타입을 변환하기도 한다.

```
// 문자열 타입 => 숫자 타입
Number('0');     // -> 0
Number('-1');    // -> -1
Number('10.53'); // -> 10.53

// 불리언 타입 => 숫자 타입
Number(true);  // -> 1
Number(false); // -> 0
```

## 2. Number 프로퍼티

### 1) Number.EPSILON

`Number.EPSILION` 은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이가 같다.

```
0.1 + 0.2 // 0.3000000000000004
0.1 + 0.2 === 0.3 // false
```

2진법으로 변환했을 때 무한소수가 되어 미세한 오차가 발생한다.

```
function isEqual(a, b){
	return Math.abs(a-b) < Number.EPSILON;
}
```

위와 같이 사용한다.

### 2) Number.MAX_VALUE

자바스크립트에서 표현할 수 있는 가장 큰 양수 값이다. `Number.MAX_VALUE` 보다 큰 숫자는 `Infinity` 뿐이다.

### 3) Number.MIN_VALUE

자바스크립트에서 표현할 수 있는 가장 작은 양수 값이다. `Number.MIN_VALUE` 보다 작은 숫자는 0이다.

### 4) Number.MAX_SAFE_INTEGER

자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수 값이다.

### 5) Number.MIN_SAFE_INTEGER

자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수 값이다.

### 6) Number.POSITIVE_INFINITY

양의 무한대를 나타내는 숫자 값 Infinity와 같다.

### 7) Number.NEGATIVE_INFINITY

음의 무한대를 나타내는 숫자 값 -Infinity와 같다.

### 8) Number.NaN

숫자가 아님을 나타내는 숫자 값이다. Number.NaN은 window.NaN과 같다.

## 3. Number 메서드

### 1) Number.isFinite

인수로 전달된 숫자 값이 정상적인 유한수인지 검사하여 그 결과를 `Boolean` 값으로 반환한다.

```
// 인수가 정상적인 유한수이면 true를 반환한다.
Number.inFinite(0)                // true
Number.inFinite(Number.MAX_VALUE) // true
Number.inFinite(Number.MIN_VALUE) // true

Number.inFinite(Infinity)  // false
Number.inFinite(-Infinity) // false
```

### 2) Number.isInteger

인수로 전달된 숫자 값이 정수인지 검사하여 그 결과를 `Boolean` 값으로 반환한다.

```
// 인수가 정수이면 true를 반환한다.
Number.isInteger(0)    // true
Number.isInteger(11)   // true
Number.isInteger(-11)  // true

// 0.5는 정수가 아니다.
Number.isInteger(0.5)   // false

// '123'을 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger('123') // false

// false를 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger(false) // false

// Infinity/-Infinity는 정수가 아니다.
Number.isInteger(Infinity)  // false
Number.isInteger(-Infinity) // false
```

### 3) Number.isNaN

인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 `Boolean` 값으로 반환한다.

```
// 인수가 NaN이면 true를 반환한다.
Number.isNaN(NaN); // true
```

Number.isNaN 메서드는 빌트인 전역 함수 isNaN과 차이가 있다. 빌트인 전역 함수 isNaN은 전달받은 인수를 숫자로 암묵적 타입 변환하고 검사를 수행하지만  Number.isNaN 메서드는 변환하지 않는다.

```
// Number.isNaN은 인수를 숫자로 암묵적 타입 변환하지 않는다.
Number.isNaN(undefined); // false

// isFinite는 인수를 숫자로 암묵적 타입 변환한다. undefined는 NaN으로 암묵적 타입 변환된다.
isNaN(undefined); // true
```

### 4) Number.isSafeInteger

인수로 전달된 숫자값이 안전한 정수인지 검사하여 그 결과를 `Boolean` 값으로 반환한다.여기서 안전한 정수 값은 -(253-1)과 253-1 사이의 정수 값이다.

### 5) Number.prototype.toExponential

숫자를 지수 표기법으로 변환하여 문자열로 반환한다.

```
(77.1234).toExponential(); // "7.71234e+1"
```

### 6) Number.prototype.toFixed

숫자를 반올림하여 문자열로 반환한다.

### 7) Number.prototype.toPrecision

인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.
인수를 생략하면 기본값이 0이 지정된다.

```
// 소수점 이하 반올림. 인수를 생략하면 기본값 0이 지정된다.
(12345.6789).toFixed(); // -> "12346"

// 소수점 이하 1자리수 유효, 나머지 반올림
(12345.6789).toFixed(1); // -> "12345.7"

// 소수점 이하 2자리수 유효, 나머지 반올림
(12345.6789).toFixed(2); // -> "12345.68"
```

### 8) Number.prototype.toString

숫자를 문자열로 변환하여 반환한다.

```
// 인수를 생략하면 10진수 문자열을 반환한다.
(10).toString(); // "10"
// 2진수 문자열을 반환한다.

(16).toString(2); // "10000"
// 8진수 문자열을 반환한다.

(16).toString(8); // "20"
// 16진수 문자열을 반환한다.

(16).toString(16); // "10"

10.toString(); // Uncaught SyntaxError: Invalid or unexpected token
```
