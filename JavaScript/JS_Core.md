# Javascript Core
## 목차
- [☑️타입 [*원시타입, *참조타입, *원시 래퍼 타입]](#%EF%B8%8F타입-원시타입-참조타입-원시-래퍼-타입)
- [☑️this](#%EF%B8%8Fthis)
- [☑️ Scope (유효범위)](#%EF%B8%8F-scope-유효범위)
- [☑️ 클로저(closure)](#%EF%B8%8F-클로저closure)
- [☑️ 생성자 (new 연산자 & 함수)](#%EF%B8%8F-생성자-new-연산자--함수)
- [☑️ 프로토 타입(prototype)](#%EF%B8%8F-프로토-타입prototype)
- [☑️ 서브타입 & 슈퍼타입](#%EF%B8%8F-서브타입--슈퍼타입)
- [☑️ Class](#%EF%B8%8F-class)
- [☑️ Hoisting (호이스팅)](#%EF%B8%8F-hoisting-호이스팅)

</br>

# ☑️타입 [*원시타입, *참조타입, *원시 래퍼 타입]
## 🔴 원시타입
* 있는 그대로 저장되는 데이터를 표현한다.
## 원시타입의 종류
* boolean : ture, false
* Number : 1, 2, 3...
* String : "Hello World"
* null
* undefined
* Symbol

## 원시타입의 특징
원시값을 변수에 할당하면 값이 복사되어 들어간다.<br>
즉, 원시값이 할당된 변수들은 모두 자기 자신만의 고유한 값을 가지게 된다.

### 코드예시
```javascript
var one = 1;
var two = 2;

one = two;

one = 3;

// 이때 two의 값은?

console.log(two) // 2
```
## typeof
원시값의 종류를 알 수 있게 해주는 매서드<br>
**null의 타입**에 주의할것
### 코드예시
```javascript
console.log(typeof 1);           // Number
console.log(typeof "hi");        // String
console.log(typeof true);        // boolean
console.log(typeof null);        // object
console.log(typeof undefined);   // undefined
```
### 왜 null의 타입은 object인가?
자바스크립트의 초기 버그이다.


</br> 

## 🔴 참조타입
* 자바스크립트의 객체를 나타낸다.
## 참조타입의 종류
* 객체 : {}
* 배열 : []
* 함수 : function
* Date
* 정규표현식 : RegExp


원시타입 빼고 전부 참조 타입으로 봐도 무방하다.

## 참조타입의 특징
참조타입은 변수에 값을 직접 저장하지 않는다.
변수에 저장되는 것은 메모리 안에서 **객체의 위치를 가리키는 "포인터"** 입니다.
무엇이 저장되느냐, 이것이 원시 타입과 참조타입의 가장 큰 차이이다.

### 코드예시
```javascript
var objOne = { one : 1 }
var objTwo = { two : 2 }

objTwo = objOne;

console.log(objTwo);  // [object Object] { one : 1 }
//같아졌다.

objTwo.one = 3;

// objTwo 에있는 one의 값을 변경했을때 objOne의 값은?
console.log(objOne);  //  [object Object] { one : 3 }
// objTwo의 바뀐값도 서로 공유한다.
```
값을 공유하는것이 아닌 값을 가리키는 "포인터"를 공유하게 되었기 때문에 **objTwo = objOne** 부분에서부터 같은 참조값(포인터)을 사용하게 된다.
그래서 하나의 값을 변경하면 다른 하나의 값도 영향을 받게 되는것이다.

---

## 🔴 원시 래퍼 타입
* 원시 타입을 객체처럼 편리하게 사용하도록 도와준다.

## 원시 래퍼 타입의 종류
* String
* Number
* Boolean

## 원시 래퍼 타입의 특징
원시 타입을 객체처럼 사용하는 순간, 자바스크립트 내부에서 사용하는 데이터의 인스턴스를 만들게 된다.   
이렇게 만들어진 객체는 코드를 실행 후 바로 다음 줄에서 파괴되는데,   
이러한 과정을 **오토박싱(autoboxing)** 이라고 한다.

### 코드예시
```javascript
var name = "bit";

console.log(name.concat("coin"))  // "bitcoin"

// .concat() 은 앞의 문자열과 매개변수로 들어오는 값을 이어붙여준다.
```
* 위 코드의 자바스크립트 내부적 처리 과정(오토박싱 과정)
  ```javascript
  var name = "bit";
  var temp = new String(name);      // 원시타입을 객체처럼 사용하는 순간 임시적으로 생성되는 인스턴스
  console.log(temp.concat("coin")   // 그리고 console.log 가 인스턴스와 함께 실행됨
  temp = null;                      // 볼일을 마쳤으니 인스턴스는 파괴된다.
  ```
* 오토박싱 추가 코드 예시
  ```javascript
  var name = "bit";
  name.coin = "coin";
  console.log(name.coin);     // undefined
  
  // 풀이과정
  var name = "bit";
  var temp = new String(name);    // 객체처럼 사용하려하니 생성된 인스턴스
  temp.coin = "coin";             // 객체처럼 사용
  temp = null;                    // 사용되었으니 다시 파괴
  
  var temp = new String(name);    // 바로 아래에서 객체처럼 사용하려하니 새로 다시 생성된 인스턴스
  console.log(temp.coin);         // 이전에 파괴된 인스턴스에는 값이 할당 되었지만 이번에 다시 생성된 인스턴스(temp)에는 할당된 값이 없음!
                                  // 그래서 undefined 가 출력 됨
  ```
## 💬 정리
* 원시타입은 문자열, 숫자, 불리언, null, undefined, symbol이 있다.
* 참조 타입은 원시타입을 제외한 나머지 데이터 타입이다.
* 원시 타입과 참조타입의 가장 큰 차이는 원시타입은 값 자체가, 참조타입은 데이터의 주소가 저장된다는 것이다.
* 원시 래퍼 타입은 String, Number, Boolean 이다.
* 원시 래퍼 타입은 원시 타입을 객체처럼 사용할 수 있도록 한다.

---

# ☑️this
* 함수를 호출한 객체를 할당한다.
## this가 존재하는 이유
```javascript
var myDiner = {
  name : '김치찌개',
  menu : function( ){
    console.log("오늘 저녁은" + myDiner.name);
  }
}
myDiner.menu();
```
위와 같은 객체가 있을 때 menu 함수는 myDiner 변수 이름이 수정될 경우나, menu 함수 자체를 다른 객체에서 사용하고 싶은 경우 사용이 불편하다.

# this 제어하기
## 🔴 call()
call 메서드는 this 의 값을 바꿀 수도 있고, 함수를 실행할 때 사용할 인수도 전달할 수 있습니다.
### 코드예시
```javascript
function menuGlobal(item){
  console.log("오늘 저녁은" + item + this.name);
}

var myDiner = {
  name : "김치찌개"
}

var yourDiner = {
  name : "된장찌개"
}

menuGlobal.call(myDiner, "묵은지");  // "오늘 저녁은 묵은지김치찌개"
menuGlobal.call(yourDiner, "삼겹살");  // "오늘 저녁은 삼겹살된장찌개"
```
function.call(타겟객체, 넘겨줄 인자)   
menuGlobal.call(myDiner, "묵은지") 의 경우 myDiner을 타겟으로 하여 this의 타겟이 잡히고 "묵은지"를 menueGlobal함수의   
매개변수로 넘겨주어 위 같은 출력값을 얻게 된다.

## 🔴 apply()
함수를 실행할 때 인수를 배열로 묶어 한번에 전달한다. 
### 코드예시
```javascript
function menuGlobal(item1, item2){
  [item1, item2].forEach(function(el){
    console.log("오늘 저녁은" + el + this.name)
  }, this);  
}

var myDiner = {
  name : "김치찌개"
}

var yourDiner = {
  name : "된장찌개"
}

menuGlobal.apply(myDiner,["묵은지", "삼겹살"]); 
// 오늘 저녁은 묵은지김치찌개
// 오늘 저녁은 삼겹살김치찌개

menuGlobal.apply(yourDiner, ["두부", "애호박"]);
// 오늘 저녁은 두부된장찌개
// 오늘 저녁은 애호박된장찌개
```
forEach에서 두번째 인자에 this를 설정해 두지 않고 내부에 this 사용시 this는 객체를 찾기떄문에 자동으로 함수를 호출하는 객체를 바라보게 되는데 이때 함수를 호출하는 객체가 window 객체이기 때문에 window 객체를 타겟으로 설정하게 된다.(전역변수) 그렇기 때문에 forEach내부에서 this를 사용할때는 두번째 항에 this를 설정해 둔다.

## call()과 apply()의 차이
call은 함수를 실행 할 때 전달할 인수를 하나 하나 전달한다면   
apply는 전달할 인수를 배열로 묶어 한번에 전달한다. 그래서 인수를 두개만 사용한다.(target으로 쓸 객체, 인자로 쓸 배열)   
인수를 배열로 보낸다는 점 빼고는 call과 apply는 동일한 기능을 수행한다.


## 🔴 bind() 
bind 메서드는 es5 에서 추가되었다.   
this 값을 어디서 사용하든 호출 객체가 바뀌지 않게 고정시켜버린다.
### 코드 예시
```javascript
function menuGlobal(item){
  console.log("오늘 저녁은" + item + this.name);
}

var myDiner = {
  name : "김치찌개"
}

var yourDiner = {
  name : "된장찌개"
}

var menuGlobalForMe = menuGlobal.bind(myDiner);

console.log(menuGlobalForMe("묵은지"));  // "오늘 저녁은 묵은지김치찌개"

```
menuGlobal.bind(myDiner) 로 인해 menuGlobal함수의 this 객체가 myDiner로 완전히 타겟팅되어 새롭게   
menuGlobalForMe 변수에 할당되었다.

## 🔴 화살표 함수와 this
화살표 함수의 this는 일반적인 this처럼 함수를 호출한 객체를 할당하지 않고,   
바로 상위 스코프의 this를 할당한다.

### 코드예시
```javascript
function menuGlobal(item1, item2){
  console.log(this);                 // [object Object] { name : "김치찌개" }
  [item1, item2].forEach( (el) => {
    console.log("오늘 저녁은" + el + this.name)
  });
}

let myDiner = {
  name : "김치찌개"
}

let yourDiner = {
  name : "된장찌개"
}

menuGlobal.apply(myDiner, ["묵은지", "삼겹살"]); 
```
일반 function을 사용했을 때는 forEach 두번째 항에 this를 지정하여 window객체를 타겟으로 잡지 않도록 막았지만   
화살표 함수를 사용했기 때문에 this는 바로 상위 스코프의 this를 할당하게 되어   
자동으로 forEach의 상위 스코프인 myDiner 객체를 타겟으로 지정하여 console.log(this)에 name : "김치찌개"가 출력되었다.

## 💬 정리
* **this는 함수를 호출하는 객체** 를 의미한다.
* call과 apply는 this에 할당되는 객체를 지정할 수 있다.
* Bind 메서드는 this에 할당되는 객체가 고정된 새로운 함수를 생성한다.
* 화살표 함수에서 this는 상위 스코프의 객체를 할당받는다.


---

# ☑️ Scope (유효범위)
* 변수의 접근성과 생존 기간을 제어한다.

### 코드예시
```javascript
let func1 = function(){
  var a = 1;
  var b = 2;
  console.log(a + b);
  return a + b
};

let a = 20;

// a가 1로 적용될까 20으로 적용될까?
func1();  // 3

```

* 스코프는 이름이 충돌하는 문제를 덜어주고, 자동으로 메모리를 관리한다.


## 🟢 자바스크립트의 유효범위(scope)
* 전역 스코프
* 함수 스코프
* 블록 스코프(es6)

## 🔴 전역 스코프
* 스크립트 어디서든 접근이 가능하기 때문에 사용이 쉽다.
* 타인과의 협업, 라이브러리 사용 시 충돌의 가능성이 있다.

## 🔴 함수 스코프
* 함수 내부에서 정의된 변수와 매개변수는 함수 외부에서 접근할 수 없다.
* 함수 내부에서 정의된 변수라면 함수의 어느 부분에서도 접근 할 수 있다.


### 코드 예시
```javascript
let func = function(){
  var a = 1;
  var b = 2;
  
  let func2 = function(){
    var b = 5;
    var c = 6;
    
    a = a + b + c;  // func2에서는 a가 정의되지 않았는데 에러가 안나는 이유는 
                    // func 함수 내부 즉 해당 func2변수를 포함하고 있는 변수에서 
                    // 정의를 해주었기 때문에 어디서든 접근 할 수 있다는 성질때문에 에러가 안남
    
    console.log(a);
  };
  func2();
};

func();  // 12
```
### 예시 2 (함수 내부 선언이 아닌 값이 할당된 변수는 전역변수로!)
```javascript
function test() {
  hell = "low";
  var hero = "world";
}
test()

console.log(hero);    // error
console.log(hell);    // "low"
```
hero는 함수 외부에서 접근이 안되는데 hell은 접근이 가능한 이유는 hero는 함수 내부에서 let으로 인해 선언이 되었지만, hell은 선언이 아니라 값이 할당이 되었다. 이처럼 함수 내부에서 선언이 아닌 할당만 된 변수는 전역변수로서 활용이 가능하다. 매우 중요한 예시



## 🔴 블록 스코프
* 중괄호 안에서만 접근 가능하다.
* 블록 내부에 정의된 변수는 블록의 실행이 끝나면 해제된다.

### 코드예시
```javascript
if(true){
  var value = "hello";
}
console.log(value);      // "hello"

if(true){
  let value = "world";
}
console.log(value);      // "hello"
```
let은 블록 스코프 키워드이기 때문에 {}안에서만 존재하며 {} 외부에서 접근이 불가하다. 따라서 두번째 console.log(value)값 역시 처음 var로 선언한 hello 값이 출력이 된다.

## 💬 정리
* 스코프는 변수의 접근성과 생존기간을 제어한다.
* 스코프는 이름이 충돌하는 문제를 덜어주고, 자동으로 메모리를 관리한다.
* 자바스크립트에는 전역 스코프, 함수 스코프, 블록 스코프가 존재한다.

---


# ☑️ 클로저(closure)
* closure : 중단하다, 폐쇄하다

## ✔️ 사전 숙지 개념
* 자바스크립트에는 함수 스코프가 있고, 함수 내부에서 정의된 변수라면 함수의 어느 부분에서든 접근 할 수 있었다.
* 이말은 즉, 내부 함수에서 자신을 포함하는 외부 함수의 스코프에 접근 할 수 있다는 얘기이다.

### 코드 예시
```javascript
var outer = function(){
  var a = 1;
  
  var inner = function(){
    var b = 5;
    var c = 6;
    
    a = a + b + c;
    console.log(a);
  };
  inner();
};

outer();   // 12
```
inner함수에서는 자신의 부모함수의 변수에 접근할 권한이 있다. 함수내부에서 선언된 함수이기떄문에

### 하지만, 만약 내부함수가 외부함수보다 오래 살아 있는 경우에, 외부함수에 있던 변수들은 어떻게 되는가?
### 코드 예시
```javascript
var outer = function(){
  var a = 1;
  
  var inner = function(){
    var b = 5;
    var c = 6;
    
    a = a + b + c;
    console.log(a);
  };
  return inner();
};
var newInner = outer();

newInner();   // 12
```
return이 되면 해당 함수는 종료된다.(죽는다)   
하지만 종료되는 함수 안에 있는 내부함수는 죽은함수의 변수에 접근 할 권한을 가진다.(only)   
종료된 함수의 변수에는 종료된 함수의 내부함수만 접근이 가능하다. 이를 클로저라고 한다.

## 🔴 클로저란?
* 폐쇄된 공간에 대한 접근 권한을 가진 함수를 말한다.

**이러한 특징을 이용한다면 비공개 데이터를 가진 객체를 만들어서 활용이 가능하다.**
### 코드 예시
```javascript
var person = (function(){
  var age = 15;
  
  return {
    name : "Wade",
  
    getAge : function(){
     console.log(age);
     return age;
    },
    
    setAge : function(val){
     age = val;
     console.log(age)
    }
  };
})();  // ()(); -> 즉시 실행

person.getAge();      // 15
person.setAge(24);    // 24
 ---------------------------------
person.age = 30;    
person.getAge();   // 15
                   // 외부에서 폐쇄된 함수의 변수에 접근을 못함 30이 아니라 15가 나온 이유
```

## 💬 정리 
* 자바스크립트는 내부 함수에서 자신을 포함하는 외부 함수의 스코프에 접근 할 수 있다.
* 내부 함수가 살아있는 상태에서 외부 함수가 파괴되면 외부 함수의 변수들에 대한 접근 권한은 내부 함수만 가지게 된다.
* 이렇게 폐쇄된 공간(함수)에 대한 접근 권한을 가진 함수가 클로저 이다.

---

# ☑️ 생성자 (new 연산자 & 함수)
## 🔴 생성자란?
* 앞에 new 연산자가 붙은 함수를 의미하며, 인스턴스를 만들 수 있다.
* 예를들어 **new Object(), new Array()** 는 자바스크립트의 내부적으로 존재하는 내장 생성자이다.
```javascript
var myArray = new Array(1, 2, 3);

console.log(myArray);  // [1, 2, 3]
```

* 사용자가 직접 새로운 타입을 만들 수도 있다.
```javascript
// 생성자 함수
function MyOwn(){}

var myObj = new MyOwn();
//인스턴스    생성자
```
* 생성자와 인스턴스의 관계는 instanceof 와 constructor 메소드를 통해 확인할 수 있다.
```javascript
console.log(myObj instanceof MyOwn);  //true

console.log(myObj.constructor === MyOwn); // true
```

## 🟠 생성자를 만드는 이유
* 생성자의 중요한 기능 : 동일한 프로퍼티와 메소드를 가진 객체를 빠르게 **대량생산** 하는 것
```javascript
function Food(name){
  this.name = name;
  this.smell = function(){
    console.log(this.name + " 냄새가 난다!");
  }
}

var myFood1 = new Food("해물 파스타");
var myFood2 = new Food("특제 파스타");
var myFood3 = new Food("토마토 파스타");

myFood1.smell();  // "해물 파스타 냄새가 난다!"
myFood2.smell();  // "특제 파스타 냄새가 난다!"
myFood3.smell();  // "토마토 파스타 냄새가 난다!"
```

## 🔴 생성자의 "new 연산자"
new 연산자가 붙으면 함수의 this는 인스턴스를 참조하게 되며,   
new 연산자가 없을 경우 생성자함수는 단순 평범한 함수이기 때문에 this 는 함수를 호출한 객체를 할당하게되어 window객체(전역객체)를 할당하게 되버린다.   
그리고 new 연산자가 자동으로 인스턴스를 반환하기 때문에 함수안에 return 연산자도 필요 없어지게 된다.

### 코드 예시
```javascript
function Food(name){
  this.name = name;
  this.smell = function(){
    console.log(this.name + " 냄새가 난다!");
  }
}

var myFood1 = Food("해물")

console.log(myFood1.name)   // TypeError : Cannot read property 'name'

myFood1.smell();  // TypeError : Cannot read property 'smell'

// 그냥 함수 안에 console.log(this) 찍엇을 경우 window 객체가 할당되어 찍힘
```

## 💬 정리
* 생성자란 앞에 new 키워드가 붙은 함수를 의미한다.
* 생성자의 중요 기능은 바로 동일한 프로퍼티와 메소드를 가진 객체를 쉽게 대량생산하는데 있다.
* 생성자 함수의 new 연산자는 인스턴스를 참조한다.


---

# ☑️ 프로토 타입(prototype)

### 코드 예제
```javascript
function Food(name){
  this.name = name;
  this.smell = function(){
    console.log(this.name + " 냄새가 난다.")
  }
}

var myFood1 = new Food("김치");
var myFood2 = new Food("계란");

console.log(myFood1.smell() === myFood2.smell());  // false
```
똑같은 함수를 사용했는데 같지 않다고 나온이유는 생성자로 새롭게 객체가 생성될 때마다 별개의 함수가 계속 만들어졌기 때문이다!
그렇기 때문에 서로 다른 주소값을 참조하고있었기 때문에 false가 나온것   
이렇게 되면 비효율적인 메모리할당이 발생하게 된다.   
해당 코드를 효율적으로 바꿔 보자

### 효율적 코드 예제
```javascript
function snell(){
  console.log(this.name + "냄새가 난다.");
}

function Food(name){
  this.name = name;
  this.smell = smell;
}

var myFood = new Food("로제 파스타");          // "로제 파스타냄새가 난다."
var myFood2 = new Food("명란젓");              // "명란젓냄새가 난다."
myFood.smell();
myFood2.smell();
console.log(myFood.smell === myFood2.smell);   // true;

```

### 🟠 의문점
```javascript
console.log(myFood.constructor === Food);  // true
```
Food 라는 생성자를 만들때 .name 과 .smell 만 만들었는데 constructor는 어디서 나온건가??

### 🟢 해답
* 자바스크립트에서는 생성자의 prototype 프로퍼티를 통해 타입의 특징을 정의한다.

앞서 본 constructor 메소드는 Object 타입의 프로퍼티이며 prototype에 의해 정의되었다.   
**Object.prototype.constructor**

### 🔴 모든 인스턴스는 내부에 [[Prototype]] 프로퍼티를 거지며 이를 통해 생성자의 prototype 프로퍼티를 추적한다.
* 이미지 : myFood   


![image](https://user-images.githubusercontent.com/61656046/126896593-8f5afe54-c1b3-4ba7-bdf1-205a7ed9f8d8.png)

## 🛠️ prototype을 사용해보자 ( ex: Object.prototype.constructor)
### 코드 예제
```javascript
// 프로토타입으로 지정해버리기
Food.prototype.smell = function(){
  console.log(this.name + "냄새가 난다.");
}

// 프로토타입으로 smell을 설정했기때문에 더이상 this.smell을 적을 필요가 없어짐
function Food(name){
  this.name = name;
}

var myFood = new Food("로제 파스타");          // "로제 파스타냄새가 난다."
var myFood2 = new Food("명란젓");              // "명란젓냄새가 난다."
myFood.smell();
myFood2.smell();
console.log(myFood.smell === myFood2.smell);   // true;


```
### 🖼️ 그림 설명 (위 코드예제의 프로토타입 추적과정)
![image](https://user-images.githubusercontent.com/61656046/126896766-b05e8572-11ef-4a72-9697-ec7e63c3914a.png)   
자신을 만든 Food 생성자의 constructor를 추적하고 Food의 생성자인(부모) Object의 constructor를 추적하여 그것을 사용했기때문에   
위 의문점에서 따로 생성하지도 않은 myFood.constructor 를 활용할 수 있었던 것이다.
* 이렇게 인스턴스에서 생성자의 [[Prototype]]을 타고 올라가며 프로퍼티를 탐색하는 현상을 **프로토타입 체인** 이라고 한다.

## 💬 정리
* 자바스크립트는 생성자의 prototype 프로퍼티를 통해 타입의 특징을 정의한다.
* 모든 인스턴스는 내부에 [[Prototype]] 프로퍼티를 가지며 이를 통해 생성자의 prototype 프로퍼티를 추적한다.
* 인스턴스에서 생성자의 [[Prototype]] 을 타고 올라가며 프로퍼티를 탐색하는 현상을 프로토타입 체인 이라고 한다.

---


# ☑️ 서브타입 & 슈퍼타입

```javascript
function FireSausage(el1, el2, el3){
  Sausage.call(this, el1, el2);
  this.inside3 = el3;
};

FireSausage.prototype = Object.create(Sausage.prototype);
FireSausage.prototype.constructor = FireSausage;

FireSausage.prototype.flavor = function(){
  return this.inside3 + "의 풍미도 있다.";
};

var mynewSausage = new FireSausagee("돼지고기", "마늘", "불맛");   

console.log(myNewSausage.taste());   // "돼지고기와 마늘 맛이 난다!"
```

## 정리
* call이나 apply를 이용하여 인스턴스를 인수로 전달하고 프로퍼티를 상속받는 방법을 생성자 훔치기라고 한다.
* Object.create() 메소드를 통해 인스턴스의 [[Prototype]] 대상을 지정 할 수 있다.
* 자바스크립트에서는 상속받는 타입을 하위 타입(subtype), 상속하는 타입을 상위 타입(supertype)이라고 부른다.


---

# ☑️ Class
* **클래스** : 자바스크립트만의 사용자 정의 타입 생성방법을 다른 언어의 클래스 문법처럼 바꿔 준 것
* 클래스는 정확히 생성자를 이용한 타입 생성과 그 결과가 일치한다. 코드 예제를 통해 확인해보자.
### 코드 예제
```javascript
class User{
  constructor(name){
    this.name = name;
  }
  sayName(){
    console.log(this.name);
  }
}

var me = new User("Joo");

me.sayName();  // "Joo"
```
### 위 코드예제를 Class 사용없이 만들어보기
```javascript
function UserOld(name){
  this.name = name;
};

UserOld.prototype.sayName = function(){
  console.log(this.name);
};

var me = new UserOld("Joo");

me.sayName();  // "Joo"
```

두가지 코드예제를 통해 확인할 수 있듯이 동일한 결과가 나오게되었다.   

클래스로 만든 객체를 콘솔로그로도 확인 해보자   <br>

![image](https://user-images.githubusercontent.com/61656046/127343168-b2937fae-595d-455a-9474-ab7c42d5e65d.png)

<br>

이전에 만들던 방식과 동일하게 [[Prototype]]과 constructor가 찍히고 있다.

이처럼 내부적인 동작은 동일하지만 더 보기 좋고 편리하게 개선된 문법을 슈가 신텍스(Syntactic sugar)라고 부른다.

## 🔴 Class에서 타입 상속하기
### 코드 예제
```javascript
class Sausage{
  constructor(el1, el2){
    this.inside1 = el1;
    this.inside2 = el2;
  };
  
  taste(){
    return this.inside1 + "와 " + this.inside2 + " 맛이 난다.";
  };
};

var classicSausage = new Sausage("닭고기", "고추");
console.log(classicSausage.taste());   // "닭고기와 고추 맛이 난다."

class FireSausage extends Sausage{}; // Sausage 프로퍼티들을 상속받고 사용하겠다.(extends)

var classicFireSausage = new FireSausage("소고기", "파");
console.log(classicFireSausage.taste());  // "소고기와 파 맛이 난다."
console.log(classicFireSausage.inside1);  // "소고기"
console.log(classicFireSausage.inside2);  // "파"
```
이처럼 **extends** 연산자를 이용해 상위 타입의 프로퍼티를 상속 받는 것이 가능하다.

이제 FireSausage 클래스만의 프로퍼티를 추가시켜 보자
```javascript
class FireSausage extends Sausage{      
  constructor(el1, el2, el3){
    this.inside3 = el3;
  };
  
  flavor(){
    return this.inside3 + "의 풍미도 있다.";
  };
}; 

var classicFireSausage = new FireSausage("소고기", "파", "불맛");

console.log(classicFireSausage.flavor());  // Reference Error : Must call super constructor in derived class before accessing...
```
### 🟢 Reference Error가 발생한 이유
자식 클래스에 constructor 함수를 선언하면 부모 클래스의 constructor 함수를 덮어쓴다.
이를 해결하기 위해 **super 메소드**가 필요하며, **super 메소드는 슈퍼타입의 생성자를 호출한다.**

### 코드 예제(super 메소드 사용)
```javascript
class FireSausage extends Sausage{      
  constructor(el1, el2, el3){
    super(el1, el2);    // <----------------- 여기서 super는 상위 클래스의 constructor 역할이다. Sausage의 constructor(el1, el2)와 동일
    this.inside3 = el3;
  };
  
  flavor(){
    return this.inside3 + "의 풍미도 있다.";
  };
}; 

var classicFireSausage = new FireSausage("소고기", "파", "불맛");

console.log(classicFireSausage.flavor());  // "불맛의 풍미도 있다."
```

## 💬 정리
* 자바스크립트의 타입 생성 방법을 다른 언어와 비슷하도록 보기 쉽게 개선한 것이 바로 자바스크립트 클래스이다.
* extends 연산자를 통해 상위 타입의 프로퍼티를 상속받는다.
* super메소드를 통해 자식클래스의 생성자 함수가 부모 클래스의 생성자 함수를 덮어 씌우는것을 방지할 수 있다.
* IE 에서는 지원하지 않는다...

---

# ☑️ Hoisting (호이스팅)

### ‼️ 호이스팅 테스트(1)
* 두 코드는 정상적으로 작동 할까?

```javascript
console.log(test());
console.log(testValue());

function test(){
  return "test";
};

var testValue = function(){
  return "testValue";
};
```
* 결과
```javascript
"test"   // console.log(test()); 성공

"TypeError : *testValue is not a function ..."    // console.log(testValue()); 실패
```
##  함수에는 두가지 리터럴 형태가 있다.
### 🟠 함수 선언
* 함수 선언은 function 키워드 뒤로 함수의 이름을 적어서 사용한다.
  ```javascript
  function test(){
    return "test";
  };
  ```
  
### 🟠 함수 표현식
* 함수 표현식은 function 키워드 뒤로 이름을 적지 않고 사용한다. 이름이 없기 때문에 익명 함수라고 부르기도 한다.

  ```javascript
  var testValue = function(){
    return "testValue";
  };
  ```
* 함수선언은 코드를 실행할 때 함수를 포함하는 스코프 최상단으로 끌어올려 진다.   
* 그림 예시
  ![image](https://user-images.githubusercontent.com/61656046/127510751-1604f93b-78cb-4d99-a26c-699daae912cd.png)

* 그에 반해 함수 표현식은 변수를 통해서 함수를 참조하기 때문에 호이스팅이 일어나지 않는다.
  * 왜 표현식은 호이스팅이 일어나지 않을까? 변수를 살펴보자

### ‼️ 호이스팅 테스트(2) : 변수
```javascript
console.log(undeclared);      // "error" : "Reference Error : undeclared is not defined..."
console.log(testValue);       // undefined

var testValue = 100;
```
* 선언하지 않은 변수(declared)는 당연히 Reference Error가 난다.
* 하지만 선언한 변수도 "값" 까지 끌어올려지지는 않고 최초 메모리에 할당되는 undefined 만이 남을 뿐이다.(이름만)
* 그렇기 떄문에 변수에 담긴 함수 표현식 역시 변수의 값에 해당하는 함수는 끌어올려 지지 않고 undefined 만 있기 때문에 함수실행이 되지 않는다!

### ‼️ 호이스팅 테스트(3) : 표현식같은 함수 선언
* 함수 선언을 표현식 처럼 사용한 경우는 어떻게 될까?
```javascript
console.log(testValueVar());        // "TypeError : testValueVar is not a function..."

var testValueVar = function testValue(){
  return "hoist test";
};
```
* testValueVar = undefined로 호이스팅 되기때문에 함수로서 사용할 수 없다.
* **변수는 함수와 달리 선언만 끌어올려진다!!**(undefined)

### ‼️ 호이스팅 테스트(4) : 조건문 내부 선언
* if문에서 변수의 선언과 초기화가 이뤄지는 경우는 어떻게?
```javascript
console.log(test);         // undefined

var condition = false;
if(condition){
  var test = "this is test";
};
```
* **에러가 나지 않은 이유** : if문은 함수가 아니다. 근데 안에 var 로 선언되었으니 그냥 전역스코프 라고 볼수 있고 test 변수가 호이스팅 되어 undefined 가 출력되었다.

### ‼️ 호이스팅 테스트(5) : 함수 내부에서의 변수선언
```javascript
console.log(test());       // "hoist test"
console.log(value);        // "Reference Error : value is not defined"

function test(){
  var value = "hoist";
  return value + " test";
};
```
* value 변수는 함수 안에서만 선언된 지역변수이기 때문에 끌어올려져도(본인이속한공간의 최상단) 함수 내부에서 최상단으로 끌어올려지기때문에 외부에서 접근 할 수 없다.

## 🔴 호이스팅이 되지 않는 선언들
```javascript
console.log(test1);         // "error" "ReferenceError : Cannot access 'test1'. before initialization at...."
console.log(test2);         // "error" "ReferenceError : Cannot access 'test1'. before initialization at...."
console.log(Tester);        // "error" "ReferenceError : Cannot access 'test1'. before initialization at...."

let test1 = "let value";
const test2 = "const value";

class Tester{
  constructor(){
    this.name = "test";
  };
};
```
### 🟠 블록스코프를 생성하는 let, const는 호이스팅이 일어나지 않는다. class또한 마찬가지
**var** 로 선언된 변수는 호이스팅 되지만 **let, const**로 선언된 변수와 상수는 **TDZ**(**T**emporal **D**ead **Z**one. 임시 접근 불가구역) 구역에 배치된다.   
이 값들은 선언이 실행된 후에 **TDZ**에서 제거되어 사용 가능한 상태가 된다.


## 💬 정리
* 함수 선언과 변수 선언은 코드를 실행할 때 해당 선언 스코프 최상단으로 끌어올려진다. 이런 현상을 호이스팅이라고 한다.
* 선언한 변수의 값은 끌어올려지지 않는다.
* let, const, class 선언은 호이스팅 현상이 일어나지 않는다.








