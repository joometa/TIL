# ⚓ 변수 선언의 실행 시점과 변수 호이스팅
```javascript
console.log(score);  // undefined

var score;  // 변수 선언문
```
한줄씩 인터프리터에 의해 순차적으로 실행되므로 선언하지 않은 변수를 console.log에 넣었으니

**ReferenceError(참조에러)** 가 발생할 것처럼 보인다.

하지만 에러 없이 **"undefined"** 가 출력 된다.

그 이유는 **변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임(runtime)이 아니라 그 이전 단계에서 먼저 실행되기 때문이다.**
<br>

💬
```
자바스크립트 엔진은 소스코드를 한 줄씩 순차적으로 실행하기 앞서(runtime 이전) 먼저 소스코드의 평가과정을 거치면서 

소스코드를 실행하기 위한 준비를 한다.

이때 소스코드 실행을 위한 준비 단계인 소스코드의 평가 과정에서 자바스크립트 엔진은 

변수 선언을 포함한 모든 선언문(변수선언문, 함수선언문 등)을 소스코드에서 찾아내 먼저 실행한다. 

그리고 평가 과정이 끝나면 비로소 변수 선언을 포함한 모든 선언문을 제외하고 한줄씩 순차적으로 실행한다.

```
- - -
![image](https://user-images.githubusercontent.com/61656046/113008698-39829f00-91b2-11eb-9dd8-5102cc93de8c.png)

<br>


### 이처럼 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 
### ✔️**변수 호이스팅(variable hoisting)** 이라 한다.
💬
```
사실 변수 선언 뿐 아니라 var, let const, function, function*, class 키워드를 사용해서 선언하는 

모든 식별자(변수, 함수, 클래스 등)는 호이스팅 된다.

모든 선언문은 런타임 이전 단계에서 먼저 실행되기 때문이다.
```
