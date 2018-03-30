# Regular Expression
[참고자료](https://javascript.info/regular-expressions)

## regular expression(정규표현식)이란
문자열을 찾거나 대체하는 아주 강력한 방법이다.  
regexp를 사용하는 방법은  
1. RegExp라는 빌트인 오브젝트를 이용한다.  
2. regexp를 이용하는 다양한 문자열 메소드를 이용한다. 

정규표현식은 다른 프로그래밍 언어에서도 사용된다. 각 언어별 정규표현식은 공통점이 많지만 차이점도 있다.


## regex의 용례
0. 모든 언어에 서브랭귀지로 존재함
1. nsername, hex value(#FF0000같은 html 컬러 코드), slug(리소스 접근할때의 url의 일부분), Email, IP address, password, url, html tag등 다양한 문자열 탐색 및 수정에 이용됨  

[참고자료](https://code.tutsplus.com/tutorials/8-regular-expressions-you-should-know--net-6149)

## regexp 의 구성
정규표현식은 pattern과 flag로 구성되어 있다
```
regexp = new RegExp("pattern", "flags");
```
`/`를 사용하면 더 간단하게 표현할 수 있다
```
regexp = /pattern/; // no flags
regexp = /pattern/gmi; // with flags g,m and i (to be covered soon)
```

## flag
5개의 flag가 존재한다.

`i`  
대소문자 구분이 없어진다. `A`와 `a`가 같아짐

`g`  
매칭되는 모든 패턴들을 찾아준다.

`m`  
멀티라인 모드

`u`  
full unicode를 지원하게 해준다. 

`y`  
sticky 모드

## 메소드

### str.match(reg) 

인자로 입력한 패턴(reg)을 찾아 가장 첫번째로 찾은 패턴을 출력한다.(`/`이용)
```
let result = "hello, world";

console.log(result.match(/hello/));
// returns  ['hello', index: 0, input: 'hello, world' ]

alert( result[0] );    // hello
alert( result.index ); // 0
alert( result.input ); // "hello, world"
```

flag `i`를 이용하면
```
let result = "Hello, world";
console.log(result.match(/hello/i)[0]);
// returns Hello
```

flag `g`를 이용하면
```
let result = "Ho-ho-ho";
console.log(result.match(/ho/));
// returns [ 'ho', index: 3, input: 'Ho-ho-ho' ]

console.log(result.match(/ho/g));
// returns [ 'ho', 'ho' ]
// 출력이 두 개 이상이면 값을 담은 배열이 출력되는군

console.log(result.match(/ho/gi));
// returns [ 'Ho', 'ho', 'ho' ]
```

### str.split(regexp|substr)
문자열을 나눈다.
```
let result = "12-34-56";
console.log(result.split('-'));
console.log(result.split(/-/));
// return ['12', '34', '56']
```