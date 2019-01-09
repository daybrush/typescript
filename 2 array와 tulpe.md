# TypeScript 스터디 2 - Array와 Tuple
---
## Array
배열은 number[]과 Array<number> 이렇게 2가지 표현법이 있습니다.
  
다른 언어에서 리터럴 배열과 배열 오브젝트지만 타입스크립트에서는 같습니다. 리터럴 배열이라고 해도 타입스크립트에서는 둘 다 오브젝트입니다.

---

타입의 차이가 있다면
* ```number[]``` 는 array문법을 사용(```ArrayType```)한 것이고
* ```Array<number>``` 는 ```Array<T>```타입을 사용(```TypeReference```)한 것입니다.
 Array라는 Interface가 존재하며 T는 Generic 타입입니다.


또한 tslint에서는
* 타입이 1개만 있는 경우엔 리터럴 배열 형태를 사용하기를 권장하고
* 1개가 아닌 경우에는 Array 오브젝트 형태를 사용하기를 권장합니다.

---
## 문제

```
const a = [1, 2, 3];
```
a는 무슨 타입일까요?
1. number[]
2. [1, 2, 3]

---
```
const a = [1, 2, 3];
```
1번(```number[]```)입니다.

a가 상수라도 length가 고정될 수 없기 때문에 리터럴이 될 수 없습니다.

하지만 a를 고정시킬 수 있는 방법이 있습니다.


---
## Tuple
배열의 값의 타입을 정하고 length를 제한합니다.
```ts
const a = [1, 2, 3];
```
a는 1, 2, 3 모두 number이기 때문에 ```[number, number, number]```타입으로 쓸 수 있습니다.

```ts
const a: [number, number, number] = [1, 2, 3]
```
a배열은 더 이상 추가할 수 없게 됩니다.
하지만 a의 원소는 변경이 가능합니다. 다음과 같이 쓰면 원소도 변경이 안됩니다.
```ts
const a: [1, 2, 3] = [1, 2, 3]
```

---
## 실습


---
## 마무리
* [1, 2, 3] < [number, number, number] < number[] < any[]

