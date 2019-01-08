# TypeScript 스터디 0 - 소개 및 config 설정


* 이 스터디의 설명은 중급자 기준으로 초점이 맞춰져있습니다.
* 하지만 예제는 초급자도 알 수 있게 실사용 예시를 다양하게 넣었습니다.
* 여기서 소개되는 타입은 InfiniteGrid를 Javascript에서 TypeScript를 전환하는 작업에서 대부분 사용한 타입들입니다. 나머지는 다른 프로젝트에서 사용했으며 여러분들이 알면 좋겠다는 타입들입니다.
* 이 스터디에서는 실시간으로 Javascript에서 TypeScript로 전환하는 작업을 할 것입니다.
  * 노트북은 필수 지참이며
  * 여러분은 본인의 Javascript 프로젝트를 가져오시거나
  * TypeSciprt 프로젝트로 시작하시거나
  * 스터디에서 제공한 예제 파일을 사용하시면 됩니다.
* 목차는 다음과 같이 진행하며 순서가 바뀔 수 있습니다.

### 목차
0. config 설정
1. Keyword와 Literal타입
2. Array과 Tuple타입
3. type, interface, Object 타입
4. Generic 타입과 extends(constraint)
5. Function과 Function 타입과 Overload
6. Method과 Method 타입과 Overload
7. Union과  Intersection 타입
8. Union 타입과 Generic타입의 차이
8. 조건부 타입
10. predicate 타입 체크
11. Require과 Partial
12. readonly와 optional과 제거 접두사(-)
13. interface와 Class의 차이와 Constructor 타입
14. type과 interface의 오묘한 차이 (매핑 타입)
15. typeof, keyof, 인덱스접근타입(IndexedAccessType)
16. enum vs consts
17. 극한의 타입들....(함수형)


## Config 설정
## 1. Install

```sh
npm i typescript -D
```
## 2. tsconfig.json 설정
tsconfig설정에 중요한 옵션 몇개만 소개하고자 합니다.
### module
module은 소스코드가 동작하는 환경입니다. 주로 파일을 읽어오고(import), 파일을 내보내는(export) 코드가 다음 환경에 맞게 소스코드가 고쳐집니다
* **CommonJS**: ```require(...)```, ```"exports.a = ...```
* **ES2015**: ES Module로 바뀌게 됩니다. ```import```, ```export``` 
* None
* UMD: ```require```, ```define```
* AMD: ```define```
* SYSTEM
* ESNext

번들러를 쓰는 경우라면 ```ES2015``` 또는 ```CommonJS```를 쓰실거라고 생각됩니다. 

번들러를 쓰지 않는 경우라면 ```ES2015```과 ```CommonJS```버전 둘 다 있거나 ```CommonJS``` 버전 하나만 있는 경우입니다.

테스트(karma, jest, mocha)에서는 Node.js가 import와 export를 지원하지 않기 때문에 ES2015를 쓰면 안 될 수 있습니다. 이 때는 CommonJS를 사용하시는게 좋습니다.

되는 경우가 있다면 테스트 환경에서 번들러를 사용하거나 테스트 프레임워크가 알아서 변환과정이 있는 경우입니다.


### target
target은 소스 코드가 변하는 범위입니다.

* **ES3**(default)
* **ES5**
* ES6/ES2015: ```class```, ```const```, ```let```, ...
* ES2016: ```**```, ```**=```
* ES2017: ```async```, ```await```
* ES2018: ```for await of```, ```Object(Rest, Spread)```, ...
* ESNext: ```catch **e** 생략```, ...

ES가 낮을수록 브라우저의 지원범위가 커집니다.많은 브라우저를 지원하기 위해 주로 ES3나 ES5를 선택합니다.

> (문법에 대한 폴리필은 추가되나 ```Promise, Object.assign``` 같은 메소드 폴리필은 추가되지 않습니다.)

ESNext를 선택한 경우 type을 제외하고 소스코드가 변하지 않습니다.

> (소스코드가 변하지 않기 때문에 추가되는 문법이나 함수/메소드 에러가 날 수 있습니다.)

### lib
지금 작성/사용하시는 타입의 지원 범위입니다.
* **DOM**
* **ES6/ES2015**: ```Symbol```, ```Promise```, ```Iterable```
* ES2015.Promise, ES2015.Generator, ...: 전체를 가져오는게 아니라 일부 타입만 가져올 수 있습니다.
* ES2016: ```Array.prototype.include```, ...
* ES2017: ```String.prototype.padStart, padEnd```, ...
* ES2018: ```Promise.prototype.finally```
* ....
* ESNext: ...


ES높을수록 타입 지원 범위가 커집니다. 하지만 타입을 지원하는 것 뿐 코드에 영향을 끼치지 않습니다.

> (lib은 문법의 지원범위가 아니지만 문법을 사용해서 나온 결과의 타입은 지원을 해줘야 합니다.)

많은 분들이 ```lib: ["ES2015", "DOM"]```를 쓰시겠죠.


### experimentalDecorators
decorator같은 경우 experimentalDecorators를 활성화를 해줘야 typescript에서 쓸 수 있습니다.


### jsx
react를 쓰시는 분을 위한 옵션입니다.
* **react** : react쓰신다면 ```"react"```
* Preserve: 기본값


### noImplicitAny
이 옵션을 활성화하면 any를 쓸 수 있게 하는게 아니라 type이 불분명해서 any를 발생시키는 요인이 있더라도 에러를 일으키지 않겠다는 뜻입니다.

> (any는 원래 쓸 수 있습니다.)

### esModuleInterop
Javascript 프로젝트를 TypeScript에서 쓰는 경우 ```import * as A from "aaa";``` 이렇게 쓰는 경우가 있습니다.

해당 라이브러리가 commonjs를 이용해 ```module.exports```를 사용했기 때문입니다.

그래서 esModuleInterop를 활성화하면 위 같은 경우에도 ```import A from "aaa"```를 사용할 수 있습니다.

### skipLibCheck
* esModuleInterop와 같이 Javascript 프로젝트를 가져오는 경우 ```*.d.ts```가 없는 경우가 많습니다. ```@types/***```가 있으면 사용하지만 없는 경우인데 사용하고 싶으면 skipLibCheck를 활성화시키면 됩니다.
* 사용하는 라이브러리에 있는 타입이 내가 사용하는 lib보다 높은 경우에도 컴파일이 되지 않습니다. 이 경우더 높은 lib을 추가하는 방법도 있고 skipLibCheck 옵션을 활성화하면 lib을 무시할 수 있습니다.

### declaration, declarationDir, emitDeclarationOnly, removeComments
4개의 옵션을 동시에 쓰는 옵션입니다.(아마도)
* declaration: 활성화하면 declaration파일이 생성됩니다.
* declarationDir: declaration파일이 생성되는 디렉토리를 가르킵니다.
* emitDeclarationOnly: 컴파일시 변환없이 declaration파일만 생성됩니다.
* removeComments: 활성화하면 주석제거합니다.(주석은 declaration파일에 있을 필요가 없습니다.)

이 옵션들은 tsconfig파일을 하나 더 만듭니다.

**tsconfig.declaration.json**
```
{
  "extends": "./tsconfig",
  "compilerOptions": {
    "removeComments": true,
    "declaration": true,
    "emitDeclarationOnly": true,
    "declarationDir": "declaration"
  }
}
```
사용 방법은 다음과 같이 합니다.
```
$ tsc -p tsconfig.declaration.json
```

## tsconfig 복붙 예제
* decorator를 사용하는 경우(experimentalDecorators)와 esnext 타입을 무시하는 경우(skipLibCheck)
  https://github.com/daybrush/scenejs/blob/master/tsconfig.json
* type이 없는 프로젝트를 가져오는 경우: https://github.com/naver/egjs-axes/blob/master/tsconfig.json
* Generator와 async을 사용하는 경우: https://github.com/daybrush/fjx/blob/master/tsconfig.json  (test는 jest지만 파일은 동일)
* test(karma-typescript)를 사용하는 경우: https://github.com/daybrush/scenejs/blob/master/tsconfig.test.json
* test(karma-webpack)를 사용하는 경우: https://github.com/daybrush/scenejs/blob/master/tsconfig.test.json
* declaration 파일을 생성하는 경우: 


#### 참조 문서
https://www.typescriptlang.org/docs/handbook/compiler-options.html

https://babeljs.io/docs/en/babel-types
