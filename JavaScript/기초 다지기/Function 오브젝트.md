# Function 오브젝트

### new Function()

Function 인스턴스를 생성한다. 파라미터에 문자열로 함수의 파라미터와 함수 코드를 작성한다.

```jsx
let obj = new Function("book", "return book;");
obj("JS 책");
```

 파라미터 수에 따라 인스턴스를 생성하는 기준이 다르다.

1. 파라미터 2개 이상 작성
    - 마지막 파라미터에 함수에서 실행할 함수 코드 작성
    - 마지막을 제외한 파라미터에 이름 작성

```jsx
let obj = new Function("one", "two", "return one + two;");
log(obj(100, 200)); //300
```

1. 파라미터 하나 작성
    - 함수에서 실행할 함수 코드 작성
    - 파라미터가 없을 때 사용

```jsx
let obj = new Function("return 1 + 2;");
log(obj()); //3
```

1. 파라미터를 작성하지 않음
    - 함수 코드가 없는 Function 인스턴스 생성

### Function()

new 연산자를 사용하지 않고 Function 인스턴스를 생성한다.

### length

함수의 파라미터 수가 생성되는 function 오브젝트에 설정된다. 함수를 호출한 곳에서 보낸 파라미터 수가 아니다. JS 엔진이 자동으로 설정한다.

```jsx
function add(one, two){
	return one + two;
}
log(add.length); //2

add(1, 2, 3, 4);
log(add.length); //2
```

### call()

파라미터 수가 고정일 때 사용한다.

```jsx
function getTotal(a, b){
	return a + b;
};

//첫 번째 파라미터 : 호출된 함수에서 this로 참조할 오브젝트
let result = getTotal.call(this, 10, 20);
log(result); //30

//첫 번째 파라미터에 this가 아닌 다른 오브젝트를 작성하는 경우
let val = {a : 10, b : 20};
function getTotal(a, b){
	return this.a + this.b; //this가 value 오브젝트 참조
};
let result = getTotal.call(val);
log(result); //30
```

### apply()

파라미터 수가 유동적일 때 사용한다. 두 번째 파라미터에 배열을 사용한다.

```jsx
function getTotal(a, b){
	return a + b;
};

//첫 번째 파라미터 : 호출된 함수에서 this로 참조할 오브젝트
let result = getTotal.apply(this, [10, 20]);
log(result); //30
```

### call(), apply()의 부가적인 목적

첫 번째 파라미터에 호출된 함수에서 this로 참조할 오브젝트 사용.

### toString()

거의 모든 빌트인 오브젝트에 toString()이 있지만 오브젝트마다 반환되는 형태가 다르다. function 오브젝트의 toString()은 함수 코드를 문자열로 반환한다.

```jsx
let getBook = function(){
	return 100 + 23;
};
log(getBook.toString()); //function(){ return 100 + 23; }
```

## Argument 오브젝트

함수를 생성하면 Argument 오브젝트를 생성한다. 함수가 호출되어 함수 안으로 이동했을 때 arguments 이름으로 생성되는 오브젝트. 항수를 호출한 곳에서 넘겨 준 값을 순서대로 저장한다.

호출된 함수에 파라미터를 작성한 경우 호출된 함수의 파라미터에도 값을 설정하고 아규먼트 오브젝트에도 저장한다.

checkbox 선택의 경우 apply() + argument 오브젝트 조합으로 대응.

함수 밖에서는 argument 오브젝트에 접근할 수 없다.