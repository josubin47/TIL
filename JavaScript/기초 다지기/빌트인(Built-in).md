# 빌트인(Built-in)

값 타입, 연산자, 오브젝트를 JS 코드를 처리하는 영역에 사전에 미리 만들어 놓은 것. 사전 처리를 하지 않고 즉시 사용할 수 있다. (Number, String, Boolean, Object, Array, Function, Math, Date, JSON, RegExp, Global)

## Number object

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