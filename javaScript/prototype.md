# prototype
[참고자료](http://eloquentjavascript.net/06_object.html)
```javascript
const obj = {};
console.log(obj.toString());
// [object objecy]
```
아무것도 정의되지 않은 객체 `obj`에서 어떻게 toString이라는 메소드를 사용할 수 있었을까? 답은 바로 prototype에게 있다.

대부분의 객체는 prototype라는 일종의 대비책 같은 객체를 가지고 있다. 만약 객체가 가지고 있지 않은 프로퍼티에 접근하게 되면 객체는 prototype을 살펴본다. 거기에도 없으면 다시 prototype의 prototype을 살펴보고, 끝까지 반복한다.

그렇다면 위의 빈 객체 { } `obj`가 살펴본 prototype은 무엇일까? 바로 모든 객체의 제일 마지막에 존재하는 `Object.prototype`객체다. 

당연히 모든 객체가 바로 `Object.prototype`을 살펴보지는 않는다. 함수는 `Function.prototype`을, 배열은 `Array.prototype`을 우선적으로 살펴본 뒤에 상위 prototype을 찾게 된다. 
```javascript
console.log(Object.getPrototypeOf(Math.max) == Function.prototype);
// → true
console.log(Object.getPrototypeOf([]) == Array.prototype);
// → true
```
## 프로토타입 정의하기
```javascript
let Person = {
  type: 'human'
}
let student1 = Object.create(Person);
student1.name = 'youngdo';

console.log(student1);
// {name: 'youngdo'}
console.log(student1.type);
// human
console.log(Object.getPrototypeOf(student1));)
// {type: 'human'}
```
객체 리터럴로 `Person`을 정의하고 `Object.create()`이용해 객체를 생성하면 `Person`객체가 프로토타입으로 작동한다.  
물론 `Person`을 생성자 함수로 정의하고 `Person.prototype.`으로 접근할 수도 있다.

클래스 변수를 이런 Javscript 방식으로 생성할 수 있겠구나!

## 생성자 함수(constructor)와 prototype
모든 객체가 prototype을 가지고 있다는 말은 `obj.prototype`으로 접근할 수 있다는 말이 **아니다!**  
prototype을 알고싶으면 `Object.getPrototypeOf()`를 이용하자.

```javascript
function Person(name){
  this.name = name;
}

Person.prototype.type = 'human';

const student = new Person('mando');
const master = new Person('crong');

console.log(student.type); // human
console.log(master.type); // human
```
그렇다면 위의 `Person.prototype.type = 'human';`은 무엇일까?

생성자 함수는 두 개의 prototype을 가진다.

1. 모든 인스턴스가 공유하는 property로서의 prototype
2. 생성자 함수가 가지는 **진짜** prototype

생성자 함수는 자동적으로 prototype 이름을 가진 property를 가진다. 이 prototype은 빈 객체 { }를 디폴트 값으로 가진다. `new`를 사용해 인스턴스를 생성하면 각 인스턴스들은 이 prototype을 공유하게 된다. 그래서 `Person.prototype`는 결국 property에 접근하는 키워드다. 이 키워드를 통해 인스턴스의 prototype을 덮어쓰거나 수정할 수 있다.
```javascript
console.log(Object.getPrototypeOf(student));
// {type: 'human'}
console.log(Object.getPrototypeOf(Person));
// [function]
```
이렇게 `Person`의 prototype에 접근하면 함수 객체로서 가지는 Function.prototype을 출력하게 된다.