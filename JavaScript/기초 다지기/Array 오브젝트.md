# Array 오브젝트

## ES3 기준

### slice()

배열의 일부를 복사하여 배열로 반환한다. 첫 번째 파라미터의 인덱스부터 두 번째 인덱스 직전까지 반환한다. 두 번째 파라미터를 작성하지 않으면 첫 번째 파라미터부터 끝까지 반환한다. **원본은 바뀌지 않는다.**

### join()

엘리먼트와 분리자를 하나씩 결합하여 문자열로 연결한다. 마지막 엘리먼트는 분리자를 연결하지 않는다.

```jsx
let val = [1, 2, 3];
log(val.join("##")) //1##2#33

//파라미터를 작성하지 않으면 콤마로 분리
log(val.join()) //1,2,3

//파라미터에 빈 문자열 작성 (데이터로 HTML의 마크업을 만들어 한 번에 표시할 때 사용)
log(val.join("")) //123
```

### delete 연산자

delete 연산자를 사용하여 삭제할 경우 삭제한 인덱스에 undefined가 설정된다. 앞으로 하나씩 당겨서 엘리먼트를 이동하면 처리 시간이 걸리기 때문이다.

```jsx
let val = [1, 2, 3];
delete val[1];
log(val); //[1, undefined, 3, 4]
```

### shift()

배열의 첫 번째 엘리먼트 삭제. 삭제한 엘리먼트 값이 undefined로 남지 않고 안전히 삭제 되기 때문에 length 값이 하나 줄어든다.

### pop()

배열의 마지막 엘리먼트 삭제. 삭제한 엘리먼트 값이 undefined로 남지 않고 안전히 삭제 되기 때문에 length 값이 하나 줄어든다.

### splice()

엘리먼트를 삭제하고 삭제한 엘리먼트를 반환한다.

```jsx
let val1 = [1, 2, 3, 4, 5];

//1번 인덱스부터 엘리먼트 3개를 삭제한다.
log(val1.splice(1, 3)); //[2, 3, 4]
log(val1); //[1, 5]

let val2 = [1, 2, 3, 4, 5];

//삭제한 위치에 세 번째 엘리먼트 삽입
log(val2.splice(1, 3, "A", "B")); //[2, 3, 4]
log(val2); //[1, A, B, 5]

let val3 = [1, 2, 3, 4, 5];

//파라미터를 작성하지 않으면 빈 배열을 반환
log(val3.splice()); //[]
log(val3); //[1, 2, 3, 4, 5]
```

### sort()

엘리먼트 값을 승순으로 정렬한다. 원본도 정렬된다. 숫자에 해당하는 Unicode의 코드 포인트로 정렬한다.

```jsx
let val = [101, 26, 7, 1234];
log(val.sort()); //[101, 1234, 26, 7]
```

### sort 알고리즘

```jsx
let val = [101, 26, 7, 1234];
val.sort(function(one, two){
	return one - two;
});
log(val.sort()); //[7, 26, 101, 1234]
```

> 콜백함수의 반환값이 양수이면 값의 위치를 바꾸고 음수이면 바꾸지 않는다. 처음으로 돌아가 바뀌는 것이 없을 때까지 배열의 엘리먼트 위치를 조정하게 된다.
> 

### reverse()

배열의 엘리먼트 위치를 역순으로 바꾼다. 값이 아닌 인덱스 기준이다. 원본도 바꾼다.

## ES6 기준

### reduce()

forEach()처럼 시맨틱 접근.

1. 콜백 함수만 작성한 경우 = 파라미터를 하나만 작성

```jsx
let value = [1, 3, 5, 7];
let fn = function(prev, curr, index, all) {
	log(prev + "," + curr);
	return prev + curr;
};

let result = value.reduce(fn);
log(result);

//1,3
//prev 1 curr 3 index 1
//처음 콜백 함수를 호출할 때
//인덱스 [0]의 값을 직전 값에 설정하고
//[1]의 값을 현재 값에 설정한다
//인덱스에 1을 설정
//4를 리턴

//4,5
//prev 4 curr 5 index 2
//두 번째로 콜백 함수를 호출할 때
//콜백 함수에서 반환된 값을 직전값에 설정
//인덱스 [2]의 값을 현재 값에 설정

//9,7
//prev 9 curr 7 index 3
//종료 (4번이 아니라 3번 반복한 것은 처음 시작할 때 인덱스가 1이기 때문)

//16
//9+7
```

> reduce()는 이와 같이 4개의 파라미터를 가지며 첫 번째 파라미터만 작성하면 두 개의 엘리먼트가 한 번에 설정된다. 따라서 length가 4이지만 3번만 반복하게 된다.
> 

1. 두 번째 파라미터를 작성한 경우

```jsx
let value = [1, 3, 5];
let fn = function(prev, curr, index, all) {
	log(prev + "," + curr);
	return prev + curr;
};

let result = value.reduce(fn, 7); //
log(result);

//7,1
//prev 7 curr 1 index 0
//처음 콜백 함수를 호출할 때
//두 번째 파라미터 값을 직전 값에 설정
//인덱스 [0]의 값을 현재 값에 설정
//인덱스에 0을 설정
//8을 리턴

//8,3
//prev 8 curr 3 index 1
//두 번째로 콜백 함수를 호출할 때
//콜백 함수에서 반환된 값을 직전값에 설정
//인덱스 [1]의 값을 현재 값에 설정

//11,5
//prev 11 curr 5 index 2

//16
//11+5
```

> 두 번째 파라미터 = 초기값으로 사용한다.
> 

### reduceRight()

reduce()와 처리 방법이 같음. 배열 끝에서 앞으로 하나씩 읽어가면서 처리.

```jsx
let value = [1, 3, 5, 7];
let fn = function(prev, curr, index, all) {
	log(prev + "," + curr);
	return prev + curr;
};

let result = value.reduce(fn);
log(result);

//7,5
//prev 7 curr 5 index 1

//12,3
//prev 12 curr 3 index 2

//15,1
//prev 15 curr 1 index 3

//16
//15+1 
```