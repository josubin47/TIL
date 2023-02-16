# DOM Element 다루기

# Element.innerHTML() vs Element.insertAdjacentHTML()

## Element.innerHTML()

element 내에 포함된 HTML 또는 XML 마그업을 가져오거나 설정함. element의 모든 자손이 제거되고 생성된 노드로 대체한다.

```jsx
const content = element.innerHTML;

element.innerHTML = htmlString;
```

## Element.insertAdjacentHTML()

특정 위치에 DOM tree 안에 원하는 node들을 추가하는 메소드. 이미 사용중인 element는 다시 파싱하지 않는다. innerHtml보다 작업이 덜 들기 때문에 빠르다.

```jsx
element.insertAdjacentHTML(position, text);
```

### position

1. `'beforebegin'` : element 앞에
2. `'afterbegin'` : element 안에 가장 첫번째 child
3. `'beforeend'` : element 안에 가장 마지막 child
4. `'afterend'` : element 뒤에

# Element.classList()

# Element.closest()

자기 자신을 포함해 위쪽으로 문서 트리를 순회하면서 일치하는 가장 가까운 element를 찾는다

# textContent vs innerText

div, span 등의 요소 안에 있는 텍스트를 읽고 싶을 때 사용

### value

input과 같은 form 요소의 값을 가져올 때 사용

### innerHTML()

마크업 태그를 핸들링할 수 있다. 그렇기 때문에 XSS 공격에 취약.

### textContent()

마크업 태그를 제외한 모든 문자열을 읽을 때

innerHTML은 매번 스타일링까지 적용해서 헤비한 메소드이기 때에 textContent가 더 좋은 퍼포먼스를 냄

사용자에게 보이지 않는 텍스트 값까지 가져옴

### innerText()

HTML의 요소가 제거된 텍스트만 읽고 싶을 때

사용자에게 보이지 않는 텍스트는 가져오지 않음
