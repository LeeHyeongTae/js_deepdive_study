# 31. RegExp

## 1. 정규 표현식이란?

> 정규 표현식은 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다. 정규 표현식은 자바스크립트의 고유 문법이 아니며, 대부분의 프로그래밍 언어와 코드 에디터에 내장되어 있다.

```javascript
const tel = '010-1234-567팔'

const regExp = /^\d{3}-\d{4}-\d{4}$/;

regExp.test(tel); // false
```

## 2. 정규 표현식의 생성

- 정규 표현식 리터럴은 패턴과 플래그로 구성된다.

```javascript
const target = 'Is this all there is?';

// 패턴: is
// 플레그: i => 대소문자를 구별하지 않고 검색한다.
// '/' = 시작 종료 기호
const regexp = /is/i;

// test 메서드는 target 문자열에 대해 정규 표현식 regexp의 패턴을 검색하여 매칭 결과물
// 불리언 값으로 반환한다.
regexp.text(target); // true
```

## 3. RegExp 메서드

### 1. RegExp.prototype.exec

> exec 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다.

```javascript
const target = 'Is this all there is?';
const regExp = /is/;

regExp.exec(target);
// -> ["is", index: 5, input: "Is this all there is?", groups: undefined] 
```

- exec 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫 번째 매칭 결과만 반환하므로 주의해야한다.

### 2. RegExp.prototype.test

> test 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴ㅇ르 검색하여 매칭 결과를 불리언 값으로 반환한다.

### 3. RegExp.prototype.match

> String 표준 빌트인 객체가 제공하는 match 메서드는 대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환한다.
> exec 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫 번째 매칭 결과만 반환하지만 match 메서드는 모든 결과를 배열로 반환한다.

```javascript
const target = 'Is this all there is?';
const regExp = /is/g;

target.match(regExp); // -> ["is", "is"]
```

## 4. 플래그

| 플래그 |     의미      |                  설명                  |
|:---:|:-------------:|:-----------------------------------------:|
|  i  | ignore case |       대소문자를 구별하지 않고 패턴을 검색한다.        |
|  g  |   Global    | 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다. |
|  m  | Multi line |       문자열의 행이 바뀌더라도 패턴 검색을 계속한다.        |

- 플래그는 옵션이므로 선택적으로 사용할 수 있으며, 순서와 상관없이 하나 이상의 플래그를 동시에 설정할 수 있다.

```javascript
const target = 'Is this all there is?'

target.match(/is/g);
// -> ["is", "is"]

target.match(/is/ig);
// -> ["is", "is", "is"]
```

## 5. 패턴

> 정규 표현식은 일정한 규칙(패턴)을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다.
> 정규 표현식은 패턴과 플래그로 구성된다. 정규 표현식의 패턴은 무자열의 일정한 규칙을 표현하기 위해 사용하며, 정규 표현식의 플래그는 정규 표현식의 검색방식을 설정하기 위해 사용한다.

### 1. 문자열 검색

> 정규 표현식의 패턴에 문자 또는 문자열을 지정하면 검색 대상 문자열에서 패턴으로 젖ㅇ한 문자 또는 문자열을 검색한다. 물론 RegExp 메서드를 사용하여야 한다.

### 2. 임의의 문자열 검색

```javascript
const target = 'Is this all there is?'

// 임의의 3자리 문자열을 대소문자를 구별하여 전역 검색한다.
const regExp = /.../g;

target.match(regExp); // -> ["Is ", "thi", "s a", "ll ", "the", "re ", "is?" ]
```

### 3. 반복 검색
- {m, n}은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다.
- {n}은 {n, n} 과 같은 의미이다.
- {n,}은 최소 n번 이상 반복되는 문자열을 의미한다.
- +는 앞선 패턴이 최소 한번 이상 반복되는 문자열을 의미한다.
- ?는 앞선 패턴이 최대 한 번(0번 포함) 이상 반복되는 문자열을 의미한다.

```javascript
const target = 'A AA B BB Aa Bb AAA';
const color = 'color colour';

// 'A' 가 최소 1번, 최대 2번 반복되는 문자열을 전역 검색한다.
const regExp1 = /A{1,2}/g;
const regExp2 = /A{2,}/g;
const regExp3 = /A+/g;
const regExp4 = /colou?r/g;

target.match(regExp1); // -> ["A", "AA", "A", "AA", "A" ]

target.match(regExp2); // -> ["AA", "AAA"]

target.match(regExp3); // -> ["A", "AA", "A", "AAA"]

color.match(regExp4); // -> ["color", "colour"]

```

### 4. OR 검색

- |은 or의 의미를 갖는다.
- 범위를 지정하려면 [] 내에 -를 사용한다.
- 대소문자를 구별하지 않고 알파벳을 검색하는 방법은 [A-za-z] 이다.
- 숫자는 [0-9] or \d 로 검색한다. \D는 숫자가 아닌 문자를 의미한다.
- \w 는 알파벳, 숫자, 언더스코어를 의미한다. 즉, \w는 [A-Za-z0-9_] 와 같다. /W는 그 반대이다.

```javascript
const target = 'A AA BB ZZ Aa Bb';

const regExp1 = /[A-Z]+/g;
const regExp2 = /[A-za-z]+/g;

target.match(regExp1); // -> ["A", "AA", "BB", "ZZ", "A", "B"]
```

### 5. NOT 검색

- [...] 내의 ^는 not의 의미를 갖는다.
- [^0-9]는 숫자를 제외한 문자를 의미한다. \D와 같은 동작을 한다.

### 6. 시작위치로 검색

- [...] 밖의 ^은 문자열의 시작을 의미한다.

### 7. 마지막 위치로 검색

- $는 문자열의 마지막을 의미한다.

```javascript

const target = 'https://poiemaweb.com';

const regExp1 = /^https/;
const regExp2 = /com$/;


regExp1.test(target); // true
regExp2.test(target); // true
```


## 6. 자주 사용하는 정규표현식

### 1. 특정 단어로 시작하는지 검사

```javascript
const url = 'https://example.com';

/^https?:\/\//.test(url); // true
```

### 2. 특정 단어로 끝나는지 검사

```javascript
const fileName = 'index.html';

/html$/.test(fileName); // true
```

### 3. 숫자로만 이루어진 문자열인지 검사
 - 처음부터 끝까지 숫자로 이루어진 문자열 검색
```javascript
const target = '1234';

/^\d+$/.test(target); // true
```
### 4. 하나 이상의 공백으로 시작하는지 검사

- \s는 여러가지 공백 문자를 의미한다. [\t\r\n\v\f]와 같은 의미이다.

### 5. 아이디로 사용 가능한지 검사

- /^[A-Az-z0-9]{4,10}$/ 알파벳 대소문자, 숫자로 시작하고 끝나며 4~10자리인지 검색

### 6. 메일 주소 형식에 맞는지 검색

- /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/
- 인터넷 메시지 형식 규약인 RFC 5322에 맞는 정교한 패턴 매칭이 필요하다면 다음과 같은 패턴을 사용해야할 필요가 있다.

### 7. 핸드폰 번호 형식에 맞는지 검사

- /^\d{3}-\d{3,4}-\d{4}$/

### 8. 특수 문자 포함 여부 검사

- /[^A-Za-z0-9]/gi 특수문자 포함 여부 확인
- 제거할때는 replace 메서드를 사용한다.


