# types

### 1. 다음과 같이 단순히 변수에 대한 type를 지정하려면 아래와 같이 사용하면 간편하다. 그냥 : 뒤에 원하는 타입을 적어주면됨.
기본 타입 : Boolean, Number, String, Object, Array, Tuple, Enum, Any, Void, Null, Undefined, Never


```typescript
let a : number = 1;
let b : string = "il";
let c : boolean = true;
```
---
### 2.배열에 대해 적용하려면 아래와 같이 사용하면 된다.

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
### 3. 객체에 대한 type 정의하기.

```typescript
const player : {
  name : string;
  age : number;
} = {
    name : "Limchoi"
}
```
이런 식으로 객체의 각 속성에 대한 type을 지정할 수 있다. 
하지만 이상의 예시에서는 에러를 발생한다 왜냐면 age를 채워주지 않았기 때문, 따라서 age를 채워주거나 아니면 선택적으로 받을 수 있는지 없는지를 정해줘야 한다.

```typescript
const player : {
  name : string;
  age? : number; // ? 하나면 끝난다
} = {
    name : "Limchoi"
}
```

이상태에서 아래와 같은 if문을 만들면

```typescript
const player : {
  name : string;
  age? : number; // ? 하나면 끝난다
} = {
    name : "Limchoi"
}

if(player.age < 10){
 // something....
 }
```
player.age가 undefined 일수도 있다고 경고문이 뜬다 (에러가 아니다) 이럴때는

```typescript
const player : {
  name : string;
  age? : number; // ? 하나면 끝난다
} = {
    name : "Limchoi"
}

if(player.age && player.age < 10){
 // something....
 }
```

정도로 지정해서 사용하면 더 완벽하게 오류 없이 사용할 수 있다.

---
### 4. type preset 정의하기.
예를 들면 아래와 같이 미리 preset을 만들어서 type을 정의할 수 있다.

```typescript
type Player = {
  name : string,
  age?: number
}
// 먼저 선언을 프리셋을 type로 선언한 후

const limchoi : Player = {
  name : "limchoi"
}

const ahchoi : Player = {
  name : "ahchoi",
  age : "32"
}
// Player를 type 처럼 사용하면 된다.
// 또한 함수로 불러서 사용도 가능하다

funtion playermaker(name:string):Player{
  retrun {
    name // 그냥 name만 
  }
}

const lalala = playermaker("lalala") //works!
lalala.age = 12 //works!
```
