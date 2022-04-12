# Type Guard

직접 지정한 타입은 typeof로 검사할 수 없다. 직접 지정한 타입을 Type Guard 할 수 있는 방법들을 정리한다.

## instanceof

instanceof는 객체가 특정 클래스에 속하는지 판단한다.

```tsx
class A {
}

class B {
}

function test(data: A | B) {
	if (data instanceof A) {
		// to do
	}
}
```

## **Truthiness narrowing**

typeof null == object이므로 `truthiness narrowing` 을 사용해 null 여부를 판단해야 한다.

```tsx
function printAll(strs: string | string[] | null) {
  if (strs && typeof strs === "object") {
    for (const s of strs) {
      console.log(s);
    }
  } else if (typeof strs === "string") {
    console.log(strs);
  }
}
```

## **Equality narrowing**

null을 판단은 Truthiness narrowing보다 Equality narrowing을 사용하는 것이 더 안전하다. undefined도 같이 체크하자.

```tsx
function example(x: string | number, y: string | boolean) {
  if (x === y) {
    // We can now call any 'string' method on 'x' or 'y'.
  } 
}
```

## in

in은 객체가 특정 프로퍼티를 가지고 있는지 판단한다.

```tsx
type A = { a : number }
type B = { b : number }

function test(data: A | B) {
	if ('a' in data) {
		return data.a;
	}
	return data.b;
}
```

## user defined type guards

특정 프로퍼티의 유무에 따라 타입 추론.

```tsx
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```