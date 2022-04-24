# TS에서도 class를 사용할 수 있다.

```typescript

class Player {
    constructor(
        private firstname : string,
        private lastname : string,
        public nickname : string
    ){}
}
//player class 생성 

const lim = new Player("lim", "choi", "림");


```

이상의 코드를 JS로 컴파일하면 아래와 같다.

```javascript

class Player {
    constructor(fristname, lastname, nickname)
        this.fristname = fristname;
        this.lastname = lastname;
        this.nickname = nickname;
    )
}
//player class 생성 

const lim = new Player("lim", "choi", "림");

```

이상 처럼 만들어놓은 lim은 fristname, lastname은 보호가 되어 접근 또는 변경이 안된다.
하지만 nickname은 가능하다.

```typescript

const lim = new Player("lim", "choi", "림");

lim.firstname // err
lim.lastname // err
lim.nicknmae // "림"
```

# Abstract (추상) class
- 쉽게 말해서 다른 클래사가 상속받을 수 있는 클래스다.
- 하지만 이 클래스는 직접 새로운 인스턴스를 만들 수 없다.

```typescript

Abstract class user {
    constructor(
        private firstname : string,
        private lastname : string,
        public nickname : string
    ){}
    
    getfullname(){
        return `${this.firstname} ${this.lastname}`
    }
}

class Player extends user{} 

//player class를 상속받음


const lim = new Player("lim", "choi", "림");

lim.getfullname() // "lim choi"
```


