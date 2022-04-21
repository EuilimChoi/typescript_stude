# types

### 다음과 같이 단순히 변수에 대한 type를 지정하려면 아래와 같이 사용하면 간편하다. 그냥 : 뒤에 원하는 타입을 적어주면됨.

```typescript
let a : number = 1;
let b : string = "il";
let c : boolean = true;
```
---
### 배열에 대해 적용하려면 아래와 같이 사용하면 된다.

```typescript
let a : number[] = [];
let b : string[] = ["il"];
let c : boolean[] = [true];
```

*type 추론

```typescript
let a = [1,2,3];
let b = ["il"];
let c = [true];

//이상의 경우 배열에 들어가있는 타입이 기본타입으로 들어가는 것으로 추론한다. 즉 a 에 "foo"를 푸쉬하면 오류를 발생한다.
```
---
