# Object 오브젝트

## 자바스크립트의 오브젝트

### 빌트인 오브젝트

사전에 만들어 놓은 11개의 오브젝트 (ES5 기준)

### 네이티브 오브젝트

Arguments 오브젝트 등. JS 스펙에서 정의한 오브젝트. 빌트인 오브젝트를 포함한다. JS 코드를 실행할 때 만드는 오브젝트.

### 호스트 오브젝트

window, DOM 오브젝트 등. DOM에서 제공하는 오브젝트를 호스트 오브젝트라고 한다. JS는 호스트 환경에서 브라우저의 모든 요소 기술을 연결하고 융합하며 이를 제어한다.

```jsx
let node = document.querySelector("div");
log(node.nodeName); //DIV
```

> querySelector() 는JS 스펙에 작성된 함수가 아니라 DOM에서 제공한다. 마치 JS 함수처럼 DOM 함수를 사용할 수 있다. 호스트 오브젝트가 JS가 사용할 수 있는 형태로 만들어 제공함. -> 호스트 환경이라고 함
> 

## Object object (ES3 기준)

### new Object()

인스턴스를 생성하여 반환한다. 파라미터의 데이터 타입에 따라 생성할 인스턴스의 타입이 결정된다. Number 타입이면 Number 인스턴스를 생성하고 String 타입이면 String 인스턴스를 생성한다.

```jsx
let val = new Object();

//파라미터 값이 undefined, null이면 빈 object 인스턴스를 반환한다.
log(val); //{}
```

### Object()

Object 인스턴스를 생성한다. 파라미터는 {name : value} 형태.

```jsx
let val = Object({name : "테스트"});
log(val); //{name : 테스트}

//파라미터를 작성하지 않으면 new Object()와 같다.
let val = Object();
log(val); //{}
```

👉 let abc = {}와 let abc = Object()는 같다.

### valueOf()

data 위치에 작성한 Object 인스턴스의 프리미티브 값을 반환한다.

```jsx
let val = {name : "테스트"};
log(val.valueOf()); //{name : 테스트}
```

## 프로퍼티 처리 메소드

### hasOwnProperty()

인스턴스에 파라미터 이름이 존재하면 true를 반환한다.

```jsx
var obj = {value : 123};
var own = obj.hasOwnProperty("value");
log(own); //true

//값은 체크하지 않고 존재 여부만 체크한다.
var obj = {value : undefined};
var own = obj.hasOwnProperty("value");
log(own); //true

//자신이 만든 것이 아니라 상속받은 프로퍼티면 false를 반환한다.
var obj = {};
var own = obj.hasOwnProperty("hasOwnProperty");
log(own); //false
```

### propertyIsEnumerable()

오브젝트에서 프로퍼티를 열거할 수 있으면 true를 반환한다.

```jsx
var obj = {sports : "축구"};
var own = obj.propertyIsEnumerable("sports");
log(own); //true

//ES5 내용
var obj = {sports : "축구"};
Object.defineProperty({obj, "sports", {
	eummerable : false
});
var own = obj.propertyIsEnumerable("sports");
log(own); //false

for(let name in obj) {
	log(name); //아무것도 출력되지 않음. 열거할 수 없는 상태이기 때문
}
```

### isPrototypeOf()

파라미터에 작성한 오브젝트에 object 위치에 작성한 prototype이 존재하면 true를 반환한다.

```jsx
var numObj = new Number(123);
log(Object.prototype.isPrototypeOf(numObj)); //true
```

### toString()

인스턴스 타입을 문자열로 표시한다.

```jsx
var point = {book : "책"};
log(point.toString()); //[object Object]

var obj = new Number(123);
log(Object.prototype.toString.call(obj)); //[object Number] -> [인스턴스 타입]
```

> object는 인스턴스를 나타내고 Object는 빌트인 Object를 나타낸다.
> 

### toLocaleString()

지역화 문자 변환 메소드를 대체하여 호출한다. Array, Number, Date 오브젝트의 toLocaleString() 메소드가 먼저 호출되고 Array, Number, Date 오브젝트가 아닐 경우 빌트인 오브젝트의 toLocaleString() 메소드가 호출된다. 에러 발생을 방지하기 위한 것이다(Object의 toLocaleString()이 없으면 에러가 발생하니까).