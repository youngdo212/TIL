# Function
모든 function은 고유의 this binding을 가진다.  
예외적으로 arrow function은 자신의 this를 바인드 하지 않는다. 대신 자기를 둘러싼 scope의 this binding을 본다.
```
let obj2 = {
  name: 'youngdo',
  setName : (name) => {  // arrow function을 사용했다
    this.name = name;
  },
  speak : function(){
    console.log(this.name);
  }
}

obj2.setName('mando');
obj2.speak(); // youngdo가 출력된다(function 키워드를 사용하면 정상적으로 mando 출력)
```
```
function normalize() {
  console.log(this.coords.map(n => n / this.length));
}
normalize.call({coords: [0, 2, 3], length: 5});
// → [0, 0.4, 0.6]

function normalize() {
  console.log(this.coords.map(function(n){
    return n / this.length
  }));
}
normalize.call({coords: [0, 2, 3], length: 5});
// 정상적으로 작동하지 않음
```
## 모든 function은 object다
**자바스크립트에서 모든 함수는 객체이다.** 이 특성 덕분에 higher-order function(고차원함수, 함수를 인자로 받거나 리턴하는 함수)나 anonymous function이 존재할 수 있다.

## anonymous function
[참고자료](http://helephant.com/2008/08/23/javascript-anonymous-functions/)  
함수를 정의하는 방법은 두 가지다.
```
// function declaration
function fly(){
  ...
}
fly();
```
위의 `function`키워드를 `function declaration`이라고 한다.  
함수선언문에서는 함수 이름(fly)을 정해줘야 한다. 함수선언문으로 생성된 함수는 함수 이름과 함수 변수를 가지는데 그 둘을 완전히 똑같다.
```
// function operator
let fly = function(){
  ...
}
fly();
```
위의 `function`키워드를 `function operator`라고 한다.  
function operator는 함수 객체를 리턴한다. 여기서 리턴되는 함수객체를 `anonymous function`이라고 한다. 함수의 이름이 없기 때문이다. 그렇다면 fly는 무엇일까?  
fly는 리턴되는 익명함수 객체를 저장하는 변수다.

그런데 function operator는 함수의 이름 짓지 못하는게 아니다!
```
let fly = function sky(){
  ...
}
fly();
sky(); // sky is not defined
```
이렇게 이름을 지어놓으면 fly함수 호출 시 콜 스택에 fly가 아니라 sky가 쌓이게 된다.  
하지만 변수에 담아둔게 아니라서 외부에서 (sky를) 사용할 수 없다. 대신 다음과 같이 내부에서는 재귀적으로 사용이 가능하다.
```
let fly = function sky(){
  if(true) sky();
  else return;
}
```
이렇게 이름지어서 사용하게 되면 디버깅 시 편하다고 하는데 아직은 잘 모르겠다...
### 왜 anonymous function을 사용하는가?
1. expression을 사용할 수 있는 모든 곳에서 사용될 수 있기 때문에 함수 선언문보다 유연하다. 이름을 따로 지을필요가 없기 때문.
```
var mando = {
 laugh : function() { alert("ho ho ho ho"); }
}
mando.laugh();
```
2. 함수선언문은 호이스팅이 되기 때문이다. 아직 경험해보지 않아서 잘 모르겠지만 내가 쓴 코드를 다른 개발자가 사용할 때 이미 선언된 이름을 사용하지 못한다는 점이 불편한가보다.

3. 즉시 함수의 정보를 받아볼 수 있기 때문이다. 함수선언문으로 작성한다면 넘겨받은 함수 변수의 정보를 알기 위해 구현된 코드를 뒤져볼 필요가 있다.

## Constructor function
```
function Person(name, age){
  this.name = name;
  this.age = age;
}
let mando = new Person('youngdo', 26);
```
* `new` operator : 사용자 정의 오브젝트나 생성자 함수를 가지는 빌트인 오브젝트의 인스턴스를 만드는 operator, 새 오브젝트를 만든 뒤 생성자 함수에 넣어 만들어진 객체를 리턴한다. 
```
var rufus = new Pet("Rufus", "cat", "miaow");
```
따라서 모든 함수는 `new` operator로 호출할 수 있지만, 생성자가 아닌 함수는 빈 객체를 리턴한다.

다른 언어의 class와는 조금 다르다고 한다.