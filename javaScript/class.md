# class

ES6에서 지원하는 문법

```javascript
class Person{
  constructor(name){
    this.name = name;
  }
  speakYourName(){
    console.log(this.name);
  }
  setName(name){
    this.name = name;
  }
}

let student = new Person('youngdo');
student.speakYourName();
//'youngdo'
console.log(student);
// {name: 'youngdo'}
Person.prototype.getName = function(){return this.name};
console.log(student.getName())
//'youngdo'
```
* constructor 함수는 생성자함수와 똑같은 기능을 한다
  * this.name을 가진 인스턴스를 생성
* speakYourName과 setName은 prototype에 정의된 메소드와 같다
* 여전히 `.prototype`을 이용해 프로토타입에 접근 가능
* **다만** 여전히 non-function value는 prototype으로 정의해줘야 한다  
 `Person.prototype.sex = 'male'`


표현식으로도 사용할 수 있다

```javascript
let obj = new class Person{constructor(){this.name = 'hi'} get(){return this.name;}}
console.log(obj.get())
// hi
console.log(obj);
// Person {name: 'hi'}

let obj2 = new class {constructor(){this.name = 'hi'} get(){return this.name;}}
console.log(obj2);
// {name: 'hi'}

```

## Map

```javascript
let myMap = new Map();
myMap.set("A", 001);
myMap.set("B", 002);
myMap.set("C", 003);
```
* 맵을 사용하면 key값에 string을 사용하지 않아도 된다.

## Polymorphism
```javascript
class Person{
  constructor(name){
    this.name = name;
  }
  speakYourName(){
    console.log(this.name);
  }
  setName(name){
    this.name = name;
  }
}
Person.prototype.toString = function(){return `hello, my name is ${this.name}`;}

const student = new Person('youngdo');
console.log(String(student))
// hello, my name is youngdo
```
`String()`이라는 함수는 인자로 들어가는 객체의 prototype의 `toString`메소드에 접근한다. 즉 toSring메소드를 객체 상황에 맞게 다르게 설정하면 `String()`함수를 다양하게 사용할 수 있다. 이것을 다형성(Polymorphism)이라고 한다.

## Symbols(ES6)

```javascript
let sym = Symbol("speakYourName");
Person.prototype[sym] = function(){
  console.log("symbol!")
}
student.speakYourName();
// youngdo
student[sym]();
// symbol!
```
`Symbol`키워드는 유일한 값을 가지는 value이다.  

```javascript
console.log(Symbol("a") === Symbol("a"));
//false
```
아직 왜 사용하는지 모르겠다...