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

## String object

문자 처리를 위한 오브젝트.

### new String()

```jsx
let obj = new String(123); //123은 String 인스턴스의 프리미티브 값으로 설정됨
log(typeof obj) //object
```

### valueOf()

String 인스턴스의 프리미티브 값을 반환한다.

### length

문자 수를 반환한다.

```jsx
var val = "ABC";
log(val.length);
```

> val이 length를 만나면 new String("ABC")라는 인스턴스를 만든다. 그리고 생성한 인스턴스의 length 값을 반환한다.
> 

### trim()

문자열 앞뒤의 화이트 스페이스를 삭제한다.

### toString()

data 위치의 값을 String 타입으로 반환한다.

```jsx
let str = new String(123);
log(str.toString());
```

💬 String 타입을 왜 String 타입으로 변환하는가? 왜 빌트인 String 오브젝트에 toString() 함수가 존재할까?

String 오브젝트에 toString()이 없으면 Object 오브젝트의 toString()이 호출된다. "123"을 Object 타입으로 인식하여 변환하기 때문에 String 오브젝트에 toString()이 있는 것이다. **__proto__** **구조를 이해해야 한다.**

__proto__에 toString()이 없으면 __proto__.__proto__의 toString() 사용. 그래서 대부분의 빌트인 오브젝트에는 toString()과 valueOf()가 있다.

```jsx
let str = toString(123);
log(str); //[object Undefined]
```

> Object 오브젝트의 toString()이 호출된다. 123을 오브젝트로 간주하여 Object 형태를 문자열로 반환한다.
> 

### charAt()

인덱스의 문자를 반환한다. 문자열 길이보다 인덱스가 크면 빈 문자열을 반환한다.

```jsx
let val = "sports";
log(val.charAt(1); //p

//ES5부터 사용 가능
log(val[1]); //p

//문자열 길이보다 인덱스가 크면 빈 문자열을 반환한다.
log(val.charAt(12); //""

//존재하지 않으면 undefined를 반환한다
log(val[12]); //undefined
```

> 개념적으로 undefined 반환이 적절하다. undefined는 시맨틱적으로 인덱스 ?번째가 없다는 뉘앙스가 강하다.
> 

### indexOf()

data 위치의 문자열에서 파라미터의 문자와 같은 첫 번째 인덱스를 반환한다. 두 번째 파라미터를 작성하면 작성한 인덱스부터 검색한다.

```jsx
let val = "123123";
log(val.indexOf(2)); //1
log(val.indexOf(22)); //1
log(val.indexOf(2, 3)); //4 -> 3번 인덱스부터 2를 검색한다.

//같은 문자가 없으면 -1을 반환한다.
log(val.indexOf(15)); //-1

//두 번째 파라미터가 NaN이거나 0보다 작으면 처음부터 검색한다.
log(val.indexOf(2, "A")); //1
log(val.indexOf(2, -1)); //1
```

### lastIndexOf()

indexOf()와 같은 기능을 하는 함수. 단, 뒤에서 앞으로 검색한다.

```jsx
let val = "12334342123";
log(val.lastIndexOf(2)); //9
let val = "1231231";
log(val.lastIndexOf(1, 4)); //3
```

### concat()

data 위치의 값에 파라미터 값을 작성 순서로 연결하여 문자열로 반환한다. String 인스턴스를 작성하면 프리미티브 값을 연결한다.

### toLowerCase()

영문 대문자를 소문자로 변환한다.

### toUpperCase()

영문 소문자를 대문자로 변환한다.

### substring()

파라미터의 시작 인덱스부터 끝 인덱스 *직전*까지 반환한다.

```jsx
let val = "01234567"
log(val.substring(2, 5)); //234
log(val.substring(5)); //567

//두 번째 파라미터를 작성하지 않으면 반환 대상의 끝까지 반환한다.
log(val.substring()); //01234567

//두 번째 파라미터 값이 전체 length보다 크면 전체 문자열 length를 사용한다.
log(val.substring(5, 20)); //567 -> 시작 인덱스부터 끝까지 반환

//파라미터 값이 음수이면 0으로 간주한다.
log(val.substring(-7, 2)); //01

//첫 번째 파라미터 값이 두 번째보다 크면 파라미터 값을 바꿔서 처리한다.
log(val.substring(5, 1)); //1234 -> val.substring(1, 5)로 처리

//NaN은 0으로 간주한다.
log(val.substring(5, "A")); //01234 -> val.substring(0, 5)로 처리
```

### substr()

파라미터의 시작 인덱스부터 지정한 문자 수를 반환한다.

```jsx
let val = "01234567"
log(val.substr(0, 3)); //012 -> 0번 인덱스부터 문자 3개를 반환한다.

//첫 번째 파라미터 값이 음수이면 length에서 파라미터 값을 더해 시작 인덱스로 사용한다.
log(val.substr(-3, 3)); //567

//두 번째 파라미터를 작성하지 않으면 양수 무한대로 간주한다.
log(val.substr(4)); //4567
log(val.substr()); //01234567
```

### slice()

파라미터의 시작 인덱스부터 끝 인덱스 직전까지 반환한다.

```jsx
let val = "01234567"
log(val.slice(1, 4)); //123

//첫 번째 파라미터 값을 작성하지 않거나 NaN(false, undefined, null)이면 0으로 간주한다.
log(val.slice(false, 4)); //0123
log(val.slice("A")); //01234567
log(val.slice()); //01234567

//두 번째 파라미터 값을 작성하지 않으면 length를 사용한다.
log(val.slice(5)); //567

//두 번째 파라미터 값이 음수이면 더해서 사용한다. (뒤에서부터 자른다고 생각하면 편함)
log(val.slice(4, -2)); //45 

//첫 번째가 두 번째보다 크거나 같으면 빈 문자열을 반환한다.
log(val.slice(5, 3)); //""
```