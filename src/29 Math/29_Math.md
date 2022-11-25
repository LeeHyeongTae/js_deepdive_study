`Math` 는 표준 빌트인 객체로, 수학적인 상수와 함수를 위한 프로퍼티와 메서드를 제공한다.
`Math` 는 생성자 함수가 아니다. 따라서 정적 프로퍼티와 정적 메서드만 제공한다.

```
new Math(123)
Uncaught TypeError: Math is not a constructor
```

### Math.PI

해당 프로퍼티는 `PI 값` 을 반환한다.

```
Math.PI; // 3.14159...
```

### Math.abs

해당 메서드는 인수로 전달된 `숫자의 절대값` 을 반환한다. 절대값은 `0` 또는 `양수` 이다.

```
Math.abs(-1);        // 1
Math.abs('-1');      // 1
Math.abs('');        // 0
Math.abs([]);        // 0
Math.abs(null);      // 0
Math.abs(undefined); // NaN
Math.abs({});        // NaN
Math.abs('string');  // NaN
Math.abs();          // NaN
```

### Math.round

해당 메서드는 인수로 전달된 숫자의 `소수점 이하` 를 `반올림한 정수` 를 반환한다.

```
Math.round(1.4);  //  1
Math.round(1.6);  //  2
Math.round(-1.4); // -1
Math.round(-1.6); // -2
Math.round(1);    //  1
Math.round();     // NaN
```

### Math.ceil

해당 메서드는 인수로 전달된 숫자의 `소수점 이하` 를 `올림한 정수` 를 반환한다.

```
Math.ceil(1.4);  //  2
Math.ceil(1.6);  //  2
Math.ceil(-1.4); // -1
Math.ceil(-1.6); // -1
Math.ceil(1);    //  1
Math.ceil();     // NaN
```

### Math.floor

해당 메서드는 인수로 전달된 숫자의 `소수점 이하` 를 `내림한 정수` 를 반환한다.

```
Math.floor(1.9);  //  1
Math.floor(9.1);  //  9
Math.floor(-1.9); // -2
Math.floor(-9.1); // -10
Math.floor(1);    //  1
Math.floor();     // NaN
```

`Math.ceil` 과 `Math.floor` 는 반대의 개념이다.

### Math.sqrt

해당 메서드는 인수로 전달된 숫자의 `제곱근` 을 반환한다.

```
Math.sqrt(9);  // 3
Math.sqrt(-9); // NaN
Math.sqrt(2);  // 1.414213562373095
Math.sqrt(1);  // 1
Math.sqrt(0);  // 0
Math.sqrt();   // NaN
```

### Math.random

해당 메서드는 `임의의 난수` 를 반환한다. 반환값은 `0` 에서 `1` 미만의 실수다.
`0` 은 포함되지만, `1` 은 포함되지 않는다.

```
Math.random(); // 0에서 1 미만의 임의의 난수(0.4480066088909287)
```

`random` 메서드와 `floor` 메서드를 사용하여 랜덤한 정수를 만들 수 있다.

```
const random = Math.floor((Math.random() * 10) + 1);
console.log(random); // 3
```

### Math.pow

해당 메서드는 `첫번째 인수`를 `밑`으로, `두 번째 인수`를 `지수`로 `거듭제곱` 한 결과를 반환한다.
지수의 값이 없을 경우엔 `NaN` 을 반환한다.

```
Math.pow(2, 8);  // 256
Math.pow(2, -1); // 0.5
Math.pow(2);     // NaN
```

#### ES7 에 도입된 지수 연산자

`Math.pow` 와 동일한 기능을 하나 가독성 좋은 코드를 만들 수 있다.
`앞` 의 피연산자는 `밑` , `뒤` 의 피연산자는 `지수` 를 의미한다.

```
2 ** 2; // 4
2 ** 2 ** 2; // 16
```

### Math.max

해당 메서드는 전달받은 인수 중에서 `가장 큰 수` 를 반환한다.

```
Math.max(1); // 1
Math.max(1, 2); // 2
Math.max(1, 2, 3); // 3

// 인수가 없는 경우
Math.max(); // -Infinity

// ES6 스프레드 문법
Math.max(...[1, 2, 3]); // 3
```

### Math.min

해당 메서드는 전달받은 인수 중에서 `가장 작은 수` 를 반환한다.

```
Math.min(1); // -> 1
Math.min(1, 2); // -> 1
Math.min(1, 2, 3); // -> 1

// 인수가 없는 경우
Math.min(); // -> Infinity

// ES6 스프레드 문법
Math.min(...[1, 2, 3]); // -> 1
```

`Math.max` 와 `Max.min` 은 반대되는 개념이다.
