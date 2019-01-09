# TypeScript 스터디 1 - keyword와 Literal

---
JavaScript 프로젝트에서 TypeScript로 전환하게 되면 가장 먼저 변환하는 파일은 consts.js입니다.

consts.ts에 가장 많이 들어가는 타입이 keyword와 literal이 됩니다.

---
## Keyword

키워드는 타입스크립트에서 지원하는 가장 기본 타입에 해당한다.
* boolean: **```BooleanKeyword```**
* number: **```NumberKeyword```**
* string: **```StringKeyword```**
* undefined: **```UndefinedKeyword```**
* void: **```VoidKeyword```**
* never: **```NeverKeyword```**
* any: **```AnyKeyword```**

---
이 중 조금 별난 타입이 있다면 never, any, void입니다.

* any는 아무거나 전부입니다.
  어떤 값이든 다 들어와도 되는게 아니라면 any를 제외한 타입을 쓰는게 좋습니다.
   악마같은 존재입니다
* void는 undefined와 비슷합니다. 하지만 함수에서 리턴값이 없을 때 void로 나타냅니다.
* never은 any와 반대의 타입입니다.     
  어디에도 속하지 못할 때 떠돌이 같은 타입입니다.     
  주로 if를 통해 type을 체크하는 작업이 있는데 마지막 타입이 never인 경우가 있습니다. 이건 타입을 잘못 짠 경우입니다.

---
## Literal

리터럴은 사전적 정의로는 고정된 값입니다. 상수에서 쓰입니다.
타입으로 사용할 수 있는 리터럴은 3가지가 있다.

* true / false: **```BooleanLiteral```**
* -2, -1, 0, 1, 2: **```NumericLiteral```**
* "1", "2", "3", "aabcc": **```StringLiteral```**


상수에서 위의 3종류 값을 쓴다면 리터럴 타입으로 부여해줍니다.

---
### 실습

---
### 문제
```
const a = "1";
let b = "1";
```

a 와 b는 각각 무슨 타입일까요?
1. string 키워드 타입일까요?
2. string 리터럴 타입일까요?

---
a는 2번 string 리터럴 타입이고 b는 1번 string 키워드 타입입니다.
```
const a = "1";
let b = "1";
```
* a는 상수이기 때문에 타입은 ```"1"``` 타입입니다.
* b는 변수이기 때문에 ```string```타입입니다.

---

하지만 저는 a에 string을 부여할 수 있습니다. 
```
const a: string = "1";
```

왜냐하면  ```"1"``` 이라는 타입은 string키워드에 **포함**되기 때문이죠.

---

하지만 아래 코드는 "1"은 number에 **포함**되지 않기 때문에 에러가 납니다.
```
const a: number = "1";
```

---
### 마무리
* "1"(literal) < string (keyword) < any
* ```"포함"```: 매 강의마다 나오며 가장 중요한 단어입니다. 포함관계가 얼마나 중요한지 매번 설명하게 될겁니다.
