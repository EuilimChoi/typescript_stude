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
