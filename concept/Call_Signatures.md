# Call Signatures
- 호출 시그니처는 타입스크립트에서 함수의 타입을 지정할 때 사용하는 문법이다. 함수에 함수를 인수로 전달하거나, 함수를 반환하는 경우 이 문법을 통해 인수나 반환 함수의 타입을 지정할 수 있다.
- 쉽게 말해 함수의 결괏값의 type를 지정해주는 문법이라 보면 된다.


```typescript
type LogFn = (text:string) => void // 호출 시그니처를 통해 LogFn 함수 타입 지정
let log: LogFn = (text) => console.log(text) // 함수 log를 선언하며 LogFn 타입임을 명시
```

# Overloading
- 동일한 이름에 매개 변수만 다른 여러 버전의 함수를 만드는 것을 함수의 오버로딩이라고 한다.
- 파라미터의 형태가 다양한 여러 케이스에 대응하는 같은 이름을 가진 함수를 만드는 것
- 함수의 다형성(다양한 형태)을 지원하는 것
- function 키워드로만 함수 오버로딩을 할 수 있으며 arrow function으로는 오버로딩을 할 수 없다.

## 주의해야할 점
- 함수의 이름은 같아야 한다.
- 매개변수의 순서는 서로 같아야 한다. (매개변수가 추가되는 것은 괜찮다! 순서는 꼭 지켜줘야 된다.)
- 매개변수의 개수도 같아야 한다. (없으면 ?로 선택사항이라고 표기해줘야한다.)
- 매개변수의 타입도 상식적으로 일치해야 한다. (number와 string을 합치는건 이상하잖아 이런 경우 예외처리를 해줘야 한다).

```typescript
//매개변수의 개수가 다를 때
type add = {
  (a: number, b:number):number
  (a: number, b:number, c:number) : number
}

const Abb : add = (a,b) =>{
  return a+b
}

// 오류를 발생시킴 매개변수의 수가 다르기 때문에 아래와 같이 변경해줘야함

const Abb : add = (a,b,c?:number) =>{
  return a+b+c
}
```


```typescript
//매개변수의 타입이 다를 때
type add = {
  (a: number, b:number):number
  (a: number, b:string) : number
}

const Abb : add = (a,b) =>{
  return a+b
}
// 오류를 발생시킴 매개변수의 타입이 다르기 때문에 정상적인 더하기를 할 수 없다. 아래와 같이 수정해보자

const Abb : add = (a,b) =>{
  if(typeof b === "string) {
    return a
  }
}
//정상 작동
```

# Polymorphism
- 프로그램 언어의 다형성(多形性, polymorphism; 폴리모피즘)은 그 프로그래밍 언어의 자료형 체계의 성질을 나타내는 것으로, 프로그램 언어의 각 요소들(상수, 변수, 식, 오브젝트, 함수, 메소드 등)이 다양한 자료형(type)에 속하는 것이 허가되는 성질을 가리킨다. 
- 쉽게 말해 한 함수에 여러가지 call signatures를 집어 넣는건데 그냥 모든 type을 혀용하는 방식이다. (any type이랑은 다르다)

```typescript
type Printsomething = {
  (arr : number[]):void
  (arr : string[]):void
  (arr : boolean[]):void
}

const printsomething : Printsomething = (arr) => {
  arr.forEach(i => console.log(i))
}

//위 처럼 선언하고 함수 호출시
printsomething([1,2,3,4,5,6]) // 작동
printsomething(["foo","bar","cor"]) //작동
printsomething([1,"foo",ture]) // 작동 안함, number, string, boolean을 섞은 call signatures는 정의 안해줬음!
```

### 여기서 등장하는 개념이 generic
- Generic이란 데이터의 타입을 일반화한다(generalize)한다는 것을 뜻한다.
- Generic은 자료형을 정하지 않고 여러 타입을 사용할 수 있게 해준다.
- 쉽게 말해서 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법이다.

```typescript
type Printsomething = {
 <T>(arr : T[]):void
}
//대부분 "Type"의 "T"를 사용해 generic을 표기한다.

const printsomething : Printsomething = (arr) => {
  arr.forEach(i => console.log(i))
}

//위 처럼 선언하고 함수 호출시
printsomething([1,2,3,4,5,6]) // 작동
printsomething(["foo","bar","cor"]) //작동
printsomething([1,"foo",ture]) // 작동 
```
