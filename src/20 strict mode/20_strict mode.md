# 20. strict mode

## 1. strict mode란?

> 전역 스코프에도 x 변수의 선언이 존재하지 않기 때문에 ReferenceError를 발생시킬 것 같지만 자바스크립트 엔진은 암묵적으로 전역 객체에 x 프로 퍼티를 동적 생성한다. 이때 전역 객체의 x 프로퍼티는 마치 전역 변수처럼 사용할 수 있다. 이런한 현상을 암묵적 전역이라 한다.

- 개발자의 의도와 상관없이 발생한 암묵적 전역은 오류를 발생시키는 원인이 될 가능성이 크다. 따라서 반드시 var, let, const 키워드를 사용하여 변수를 선언한 다음에 사용해야 한다.
- strict mode는 자바스크립트 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.

## 2. strict mode의 적용

> 'use strict' 를 전역의 선두 또는 함수 모체의 선두에 추가하면 된다.

## 3. 전역에 strict mode를 적용하는 것은 피하자.

> 외부 서드파티 라이브러리를 사용하는 경우 문제가 생길 수 있기 때문에 전역으로 사용하는건 바람직하지 않다.

## 4. 함수 단위로 strict mode를 적용하는 것도 피하자.

```javascript
(function () {
    // non-strict-mode
    var a = 10; // 에러가 발생하지 않는다.
    
    function foo() {
        'use strict'
        a = 20; // 예제에서 변수명으로 사용한 let은 예약어이기 떄문에 사용할수 없다.
    }
    foo();
}())
```

- strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.

## 5. strict mode가 발생시키는 에러

### 1. 암묵적 전역

```javascript
(function (){
    'use strict';
    x = 1;
    console.log(x); // ReferenceError: x is not defined
}());
```

- 선언하지 않는 변수를 참조하면 ReferenceError가 발생한다.

### 2. 변수, 함수, 매개변수의 삭제

```javascript
(function (){
    'use strict';
    
    var x = 1;
    delete x; // SyntaxError: Delete of an unqualified identifier in strict mode.
    
    function foo(a) {
        delete a; // SyntaxError: Delete of an unqualified identifier in strict mode.
    }
    delete foo; // SyntaxError: Delete of an unqualified identifier in strict mode.
}());
```

- delete 연사자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.

### 3. 매개변수 이름의 중복

```javascript
(function (){
    'use strict';
    
    //SyntaxError: Duplicate parameter name not allowed in this context
    function foo(x, x) {
       return x + x; 
    }
    console.log(foo(1, 2));
}());
```
- 중복된 매개변수 이름을 사용하면 SyntaxError가 발생한다.

### 4. with문의 사용

```javascript
(function (){
    'use strict';
    
    //SyntaxError: Strict mode code may not include a with statement
    with({ x: 1}){
        console.log(x);
    }
}());
```
- with문은 사용하지 않는 것이 좋다. // 사용 해본적이 없다.





