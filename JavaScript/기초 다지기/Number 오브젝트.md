# Number 오브젝트

숫자 처리를 위한 오브젝트.

### Number()

파라미터 값을 Number 타입으로 변환한다.

```jsx
log(Number("a")); //NaN
log(Number(undefined); //NaN
log(Number(null); //0
log(Number()); //0
```

### Number 상수

상수는 값을 변경, 삭제할 수 없음. 영문 대문자 사용이 관례.

### new Number()

prototype에 있는 것만 인스턴스에 할당한다. (__proto__의 값으로) 나머지는 복사되지 않는다.

### valueOf()

Number 인스턴스의 프리미티브 값을 반환한다.

### toString()

data를 String 타입으로 변환한다. 파라미터의 디폴트 값은 10진수이다.

```jsx
log(20.toString()); //error (=20toString())
log(20..toString()); //20 (=20.0.toString())
```

### toLocaleString()

숫자를 브라우저가 지원하는 지역화 문자로 변환한다. 지역화를 지원하지 않으면 toString()으로 반환한다. ES5 파라미터 사용 불가, ES6 파라미터에 언어 타입 사용 가능

### toExponential()

숫자를 지수 표기로 변환하여 문자열로 반환한다.

### toFixed()

고정 소숫점 표기로 변환하여 문자열로 반환한다. 파라미터에 -0에서 20까지 소수 이하 자릿수를 작성한다. 파라미터 값보다 소수 자릿수가 길면 작성한 자리수에 1을 더한 위치에서 반올림한다.

```jsx
let val = 1234.567;
log(val.toFixed(2)); //1234.57

//파라미터 값을 작성하지 않으면 0으로 간주하며 소수 첫째 자리에서 반올림하여 정수값을 표시한다.
log(val.toFixed()); //1235

//변환 대상 자릿수보다 파라미터 값이 크면 나머지를 0으로 채워 반환한다.
log(val.toFixed(5); //1234.56700
```