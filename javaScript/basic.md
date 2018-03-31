# 기본
[참고자료](http://eloquentjavascript.net/01_values.html)

## Value
컴퓨터가 수 많은 비트들로 이루어진 거대한 바다라고 생각하자. 비트를 이용해 무언가를 만들려면 비트들이 나타내는 작은 정보들을 따로 구분할 필요가 있다. 구분된 작은 정보들을 `Value`라고 한다. `1`이나 `'cat'`같이 특정 정보들을 나타내는 값들을 `value`라고 할 수 있다.

## Expression
`value`를 제공하는 코드의 조각들을 `Expression`이라고 한다. `1`과 `'cat'` 모두 `value`이자 `expression`이다. 당연히 연산자로 이루어진 `2 * 2`, `'I' + 'love' + 'cat'`과 같은 코드 조각들도 expression이다. expression은 expression을 포함할 수 있다.

## Statement
expression은 문장의 조각이다. 한 개의 제대로된 문장을 `statement`라고 한다. `statement`는 세미콜론(;)으로 끝난다.
```
1;
!true;
```
물론 위의 문장도 statement라고 할 수 있지만 불필요한 문장이다. 왜냐하면 statement는 기계의 내부 상태를 바꾸기 위해 주로 사용되기 때문이다. 이러한 변화를 'side effect'라고 한다.

## Binding(Variable)
value를 담거나 저장해서 사용할 수 있게 해주는 것들을 `binding`(`variable`, 변수)이라고 한다. 변수에 값이 담기게 되면 값을 제공할 수 있으므로 expression으로 사용될 수 있다.
```
let k = 5 * 5;
```