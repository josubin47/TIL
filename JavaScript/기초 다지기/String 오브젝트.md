# String 오브젝트

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

## 정규 표현식을 사용할 수 있는 함수

정규 표현식 : 문자열을 패턴(^, $ 등)으로 매치한다.

### match()

매치 결과를 배열로 반환한다. 매치 대상에 정규 표현식의 패턴을 적용하여 매치하고 매치 결과를 반환한다. 문자열을 작성할 수 있다. 엔진이 정규 표현식으로 반환하여 매치한다.

```jsx
let val = "Sports";
log(val.match(/s/)); //[s]
log(val.match("spo")); //null
```

### replace()

매치 결과를 파라미터에 작성한 값으로 대체하여 반환한다.

```jsx
let val = "abcabc"

//처음에 한 번 매치가 되면 거기서 실행이 끝난다.
log(val.replace("a", "바꿈")); //바꿈bcabc
log(val.replace(/a/, "바꿈")); //바꿈bcabc

//두 번째 파라미터에 함수를 작성하면 먼저 함수를 실행하고 함수에서 반환한 값으로 대체한다.
fuction change(){
	return "함수";
}
log(val.replace(/a/, change()); //함수bcabc
```

### search()

검색된 첫 번째 인덱스를 반환한다. indexOf()와 비슷하지만 indexOf()로는 복합적인 조건(정규식 처리)을 줄 수 없다.

```jsx
let val = "cbacba"

//처음에 한 번 매치가 되면 거기서 실행이 끝난다.
log(val.search(/a/)); //2

//매치되지 않으면 -1을 반환한다.
log(val.search("K")); //-1
```

### split()

분리 대상을 분리자로 분리하여 배열로 반환한다.

```jsx
log("12_34_56".split("_")); //[12, 34, 56]

let val = "123";

//분리자에 빈 문자열을 작성하면 문자를 하나씩 분리하여 반환한다.
log(val.split("")); //[1, 2, 3]
//분리자를 작성하지 않으면 원본을 하나의 배열로 반환한다.
log(val.split()); //[123]

let val = "12_34_56_78";
//두 번째 파라미터에 숫자를 작성하면 앞에서부터 수만큼만 반환한다.
log(val.split("_", 3)); //[12, 34, 56]
//분리자가 분리 대상에 없으면 분리 대상 전체를 하나의 배열로 반환한다.
log(val.split("A")); //[123]
```

## Unicode 관련 함수

### charCodeAt()

인덱스 번째의 문자를 유니코드의 코드 포인트 값을 반환다. 인덱스가 문자열 길이보다 크면 NaN을 반환한다.

### fromCharCode()

파라미터의 유니코드를 문자열로 변환하고 연결하여 반환한다. 작성하지 않으면 빈 문자열을 반환한다.

```jsx
//data 위치에 String 오브젝트를 작성한다. 변환 대상 값을 작성하지 않는다.
log(String.fromCharCode(49, 65, 97, 44032)); //1Aa가
```

🧐 왜 이렇게 사용할까?

💬 파라미터에 다수를 작성할 수 있게 하기 위해서. [49, 65, 97, 44032]의 배열 형태로 작성하면 배열은 object이기 때문에 String 오브젝트의 fromCharCode()를 부를 수 없다. (자바스크립트 구조상 어쩔 수 없음)

### localeCompare()

값을 비교하여 위치를 나타내는 값으로 반환한다.

```jsx
//위치 값이 앞
log(val.fromCharCode("가")); //1
//위치 값이 동일
log(val.fromCharCode("나")); //0
//위치 값이 뒤
log(val.fromCharCode("다")); //-1
```