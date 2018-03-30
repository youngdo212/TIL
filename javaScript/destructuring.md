# Destructuring
[참고자료](http://exploringjs.com/es6/ch_destructuring.html#ch_destructuring)  
Destructuring은 ECMAScript6(ES6)에서 제공하는 기능으로서 객체나 배열에 들어있는 여러 값들들 추출하는 효과적인 방법이다. (할당문의 좌변과 같이)데이터를 받는 위치에서 사용된다.
```
const obj = {name: 'mando', age: 26, sex: 'm'};
const {name: student, sex: sex} = obj;
// student = 'mando', sex = 'm'

const {name, sex} = obj;
// student = 'mando', sex = 'm'

const arr = ['a', 'b', 'c'];
const [x, y] = arr;
// x = 'a', y = 'b'
```
* destructing source: 분해되는 데이터, 우변
* destructing target: 값을 받는 데이터, 좌변
* object pattern : { first: pattern, second: patter }
* array pattern : [ pattern, patter ]

Object patter에 사용되는 중괄호{}는 code block과 혼동되지 않기위해 괄호()를 필수적으로 사용해야 한다(단, var나 const, let과 함께 사용하는 경우는 괜찮다.)
```
let {name:a} = {id: 123, name: 'youngo'} // 사용가능
{key: x} = {key: 1001} // error
({key: x} = {key: 1001}) // 사용가능
```
## 작동 방법
### Object pattern
값을 객체로 강제한다.  
undefined와 null에는 사용할 수 없다. 왜냐하면...
```
const {length: len} = 'hello' // len = 5
const {length: len} = [1,2,3,4] // len = 4

const {prop: x} = undefined // TypeError
const {prop: y} = null // TypeError
```
object로 강제 할 시에 `Object()`를 사용하지 않고 `ToObject()`를 사용하기 때문이다. `Object()`와 달리 `ToOject()`는 undefined와 null이 인자로 들어가면 TypeError가 뜬다. 따라서 object pattern에 undefined나 null이 할당되는 경우를 조심하자!
```
Object(null); // {}
Object(undefined) // {}

({} = undefined) // TypeError
```

### Array pattern
이터러블한 객체와 함께 사용한다.  
undefined와 null 이터러블하지 않으므로 사용불가.
```
const [x, ...y] = 'abc' // x = 'a', y = ['b', 'c']
const [a, b] = [1,2,3,4] // a = 1, b = 2
```
`,`를 이용해 생략가능(Elision)
```
const [,,x,y] = [1,2,3,4] // x = 3, y = 4
```

## Default Value
디폴트 값을 사용할 수 있다
```
const [a=3, b] = []; // a = 3, b = undefined
const {key: x = 123, type: y} = {} // x = 123, y = undefined
```

## 활용(Named Parameter)
함수를 호출할 때 넘겨준 인자가 어떤 것을 의미하는지 애매모호한 경우가 있다.  
다음을 보자.
```
selectEntries(3,5);
```
도대체 3과 5는 무엇을 의미하는 걸까? 함수 내부를 들여다 보기 전 까지는 인자가 무엇을 나타내는지 알 수 없다. 이런 불편함을 해결하기 위해서 **파이썬**에서는 named parameter 기능을 제공한다.
```
//파이썬에서
selectEntries(from = 3, to = 5);
selectEntries(to = 5, from = 3); // 똑같이 작동한다
```
아, 3과 5는 시작과 끝을 나타내는군!

인자가 사용될 변수의 이름을 함께 적어주면서 함수호출문 만으로도 인자의 의미를 파악할 수 있다. 그렇다면 우리의 자바스크립트는? 다행히도 ECMAScript6(ES6)의 destructuring을 이용하면 비슷하게 표현할 수 있다.
```javascript
//ES6
selectEntries({from: 3, to: 5});
selectEntries({to: 5, from: 3}); // 같음

function selectEntries({from = 0, to = 1} = {}){
  ...
}
// = {} 는 TypeError를 방지하지 위해 디폴트 값을 넣어준 것
```

Destructuring을 활용해 함수 호출 의도를 잘 드러내보자!

Q. built-in 매소드 중에 객체를 인자로 받는 메소드가 있었나? 객체를 인자로 받아야 named para를 쓸텐데.. 지금까지 사용한 메소드는 전부 `,`로 인자를 받았던 것 같다. 잘 사용하지 않는듯한 방법을 사용해도 좋을까? 통일감이 없어서 별로인거 같은데.. 크롱한테 물어봐야겠다.