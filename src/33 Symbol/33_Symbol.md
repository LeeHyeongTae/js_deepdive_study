# 33. 7째 데이터 타입 Symbol

## 1. 심벌이란?

> 심벌은 ES6에서 도입된 7번째 데이터 타입으로 변경 불가능한 원시 타입의 값이다. 실벌 값은 다른 값과 중복되지 않는 유일무이한 값이다. 따라서 주로 이름의 충돌 위험이 없는 유일한 프로퍼티 키를 만들기 위해 사용한다.

## 2. 심벌 값의 생성

### 1. Symbol 함수

> 심벌 값은 Symbol 함수를 호출하여 생성한다. 
> 이때 생성된 심벌 값은 외부로 노출되지 않아 확인할 수 없으며, 다른 값과 절대 중복되지 않는 유일무이한 값이다.

```javascript
// Symbol 함수를 호출하여 유일무이한 실범 값을 생성한다.
const mySymbol = Symbol();
console.log(typeof  mySymbol); // symbol

// 심벌 값은 외부로 노출되지 않아 확인할 수 없다.
console.log(mySymbol) // Symbol()
```

> 언뜻 보면 생성자 함수로 객체를 생성하는 것처럼 보이지만 
> Symbol 함수는 String, Number, Boolean 생성자 함수와 달리 new 연산자와 함꼐 호출하지 않는다.

```javascript
// 심벌 값에 대한 설명이 같더라도 유일무이한 심벌 값을 생성한다.
const mySymbol1 = Symbol('mySymbol'); 
const mySymbol2 = Symbol('mySymbol');

console.log(mySymbol1 === mySymbol2) // fasle
```

- 심벌 값도 문자열, 숫자, 불리언과 같이 객체처럼 접근하면 암묵적으로 래퍼 객체를 생성한다.

```javascript
const mySymbol = Symbol('mySymbol');

// 심벌도 래퍼 객체를 생성한다.
console.log(mySymbol.description); // mySymbol
console.log(mySymbol.toString()); // Symbol(mySymbol)
```

- 심벌 값은 암묵적으로 문자열이나 숫자 타입으로 변환되지 않는다.

```javascript
const mySymbol = Symbol();

// 심벌 값은 암묵적으로 문자열이나 숫자 타입으로 변환되지 않는다.
console.log(mySymbol + ''); // TypeError: Cannot convert a Symbol value to a string
console.log(+mySymbol); // TypeError: Cannot convert a Symbol value to a number
```

- 단, 불리언 타입으로는 암묵적으로 타입 변환된다. 이를 통해 if문 등에서 존재 확인이 가능하다.

```javascript
const mySymbol = Symbol();

// 불리언 타입으로는 암묵적으로 타입 변환된다.
// if 문 등에서 존재 확인이 가능하다.
console.log(!!mySymbol); // true

```

### 2. Symbol.for / Symbol.keyFor 메서드

> Symbol.for 메서드는 인수로 전달받은 문자열을 키로 사용하여 키와 심벌 값의 쌍들이 저장되어 있는 전역 심벌 레지스트리에서 해당 키와 일치하는 심벌 값을 검색한다.

- 검색에 성공하면 새로운 심벌 값을 생성하지 않고 검색된 심벌 값을 반환한다.
- 검색에 실패하면 새로운 심벌 값을 생성하여 Symbol.for 메서드의 인수로 전달된 키로 전역 심벌 레지스트리에 저장한 후, 생성된 심벌 값을 반환한다.

```javascript
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로운 심벌 값을 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 있으면 해당 심벌 값을 반환
const s2 = Symbol.for('mySymbol');

console.log(s1 === s2); // true
```

- Symbol.keyFor 메서드를 사용하면 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출할 수 있다.

```javascript
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로운 심벌 값을 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출
Symbol.keyFor(s1); // mySymbol

// Symbol 함수를 호출하여 생성한 심벌 값은 전역 심벌 레지스트리에 등록되어 관리되지 않는다.
const s2 = Symbol('foo');
// 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출
Symbol.keyFor(s2); // undefined
```

## 3. 심벌과 상수

```javascript
// 위, 아래, 왼쪽, 오르쪽을 나타내는 상수를 정의한다.
// 중복될 가능성이 없는 심벌 값으로 상수 값을 생성한다.
const Direction = {
    UP: Symbol('up'),
    DOWN: Symbol('down'),
    LEFT: Symbol('left'),
    RIGHT: Symbol('right')
};

const myDirection = DIrectio.UP;

if(myDirection === Direction.UP) {
    console.log('You are going UP.')
}
```

### enum

> enum은 명명된 숫자 상수의 집합으로 열거형이라고 부른다. 
> 자바스크립트는 enum을 지원하지 않지만 C, 자바, 파이썬 등 여러 프로그래밍 언어와 자바스크립트의 상위 확장인 타입스크립트에서 enum을 지원한다.

## 4. 심벌과 프로터피 키

> 객체의 프로퍼티 키는 빈 문자열을 포함하는 모든 문자열 또는 심벌 값으로 만들 수 있으며, 동적으로 생성할 수도 있다.

```javascript
const obj = {
    // 심벌 값으로 프로퍼티 키를 생성
    [Symbol.for('mySymbol')]: 1
};
obj[Symbol.for('mySymbol')]; // -> 1
```

- 심벌 값은 유일무이한 값이므로 심벌 값으로 프로퍼티 키를 만들면 다른 프로퍼티 키와 절대 충돌하지 않는다.


## 5. 심벌과 프로퍼티 은닉

> 심벌 값을 프로퍼티 키로 사용하여 생성한 프로퍼티는 for ... in 문이나 Object.keys, Object.getOwnPropertyNames 메서드로 찾을 수 없다.
> 하지만 프로퍼티를 완전하게 숨길수 있는 것은 아니다. getOwnPropertySymbols 메서드를 사용하면 가능하다.

## 6. 심벌과 표준 빌트인 객체 확장

> 일반적으로 표준 빌트인 객체에 사용자 정의 메서드를 직접 추가하여 확장하는 것은 권장하지 않는다. 표준 빌트인 객체는 읽기 전용으로 사용하는 것이 좋다.

## 7. Well-known Symbol

- 자바스크립트가 기본 제공하는 빌트인 심벌 값이 있다. 
- 자바스크립트가 기본 제공하는 빌트인 심벌 값을 ECMAScript 사양에서는 Well-known Symbol 이라 부른다.











