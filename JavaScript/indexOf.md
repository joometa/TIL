# indexOf 함수
```javascript
string.indexOf(searchvalue, position)
```
### 정의
```
indexOf 함수는, 문자열(string)에서 특정 문자열(searchvalue)을 찾고, 

검색된 문자열이 '첫번째'로 나타나는 위치 index를 리턴합니다.
```

### 파라미터
* **searchvalue** : 필수 입력값, 찾을 문자열
* **position**: optional, 기본값은 0, string에서 searchvalue를 찾기 시작할 위치
```
찾는 문자열이 없으면 -1을 리턴한다.
문자열을 찾을 때 대소문자를 구분함
```
* 리액트에서도 활용되며 필터링 목적으로 쓰이는 듯 하다.

### 예제
```javascript
const str = "abab";

document.writeln(str.indexOf('ab')); // 0
document.writeln(str.indexOf('ba')); // 1
document.writeln(str.indexOf('abc')); // -1
document.writeln(str.indexOf('AB')); // -1
```

* 예제 1
```
문자열 'abab'에서 'ab'가 처음으로 나타나는 위치의 인덱스 값을 리턴한다.
```
* 예제 2
```
문자열 'abab'에서 'ba'가 처음으로 나타나는 위치의 인덱스 값을 리턴한다.
```
* 예제 3
```
문자열 'abab'에는 'abc'라는 문자열이 없으므로 숫자 -1을 리턴하였다.
```
* 예제 4
```
indexOf 함수는 대소문자를 구분합니다.

문자열 'abab'에는 대문자 'AB'는 없으므로 숫자 -1을 리턴하였습니다.
```


[출처](https://hianna.tistory.com/379)
