# DOM Element 다루기

# **Element.**innerHTML() vs E**lement.insertAdjacentHTML()**

## **Element.**innerHTML()

element 내에 포함된 HTML 또는 XML 마그업을 가져오거나 설정함. element의 모든 자손이 제거되고 생성된 노드로 대체한다.

```jsx
const content = element.innerHTML;

element.innerHTML = htmlString;
```

## **Element.insertAdjacentHTML()**

특정 위치에 DOM tree 안에 원하는 node들을 추가하는 메소드. 이미 사용중인 element는 다시 파싱하지 않는다. innerHtml보다 작업이 덜 들기 때문에 빠르다.

```jsx
element.insertAdjacentHTML(position, text);
```

### position

1. `'beforebegin'` : element 앞에
2. `'afterbegin'` : element 안에 가장 첫번째 child
3. `'beforeend'` : element 안에 가장 마지막 child
4. `'afterend'` : element 뒤에