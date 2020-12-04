# Type Alias

`type`은 특정 타입에 별징을 붙이는 용도로 사용한다. 타입으로 사용한다는 점에서 인터페이스와 유사하다.

```typescript
interface Person {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은 설정을 해도 되고 안 해도 되는 값이라는 것을 의미한다.
}

// & 는 Intersection 으로서 두개 이상의 타입들을 합쳐준다.
type Developer = Person & {
  skills: string[];
}

const me: Person = {
  name: '위독한미식가',
};

const expert: Developer = {
  name: 'gou5met',
  skills: ['javascript','react','typescript']
};

type People = Person[] // Person[] 를 앞으로 People 이라는 타입으로 사용할 수 있게 해준다.
const people: People = [me,expert];
```

그렇다면 차이점은 무엇일까? Type Alias는 원시값, 유니온 타입, 튜플 등도 타입으로 지정할 수 있다는 점이 있다.

```typescript
// 문자열 리터럴로 타입 지정
type Str = 'Bae';

// 유니온 타입으로 타입 지정
type Union = string | null;

// 문자열 유니온 타입으로 타입 지정
type Name = "Bae" | "Kim";

// 숫자 리터럴 유니온 타입으로 타입 지정
type Num = 1 | 2 | 3 | 4 | 5;

// 객체 리터럴 유니온 타입으로 타입 지정
type Obj = {a: 1} | {b: 2};

// 함수 유니온 타입으로 타입 지정
type Func = (() => string | (() => void))

// 인터페이스 유니온 타입으로 타입 지정
type Shape = Square | Rectangle | Circle;

// 튜플로 타입 지정
type Tuple = [string,boolean];
const t: Tuple = ['',''] // 에러
```

---

## Intersection Types

`Intersection` 타입은 여러 타입을 하나로 결합한다. 이렇게하면 기존 타입을 모두 추가하여 필요한 모든 기능을 갖춘 단일 타입을 얻을 수 있다.

`A` & `B` & `C` 는 `A` 와 `B` 이며 `C` 이다. 즉, 이 타입의 객체는 세 가지 타입의 모든 멤버를 갖게된다. 



## Union Types

`Union` 타입은 `Intersection` 타입과 비슷하지만 매우 다르게 사용된다. `Union` 타입은 여러 타입 중 하나 알 수 있는 값을 나타낸다. 수직 막대(`|`)를 사용하여 각 타입을 구분하므로 `string | number`는 `number` 또는 `string`일 수 있는 값의 타입이다. 

```typescript
function padLeft(value: string, padding: string | number) { ... }

let indentedString = padLeft("Hello",3);
let indentedString2 = padLeft("World",true); // 에러 
```

`Union` 타입을 가진 값이 있다면 `Union` 의 모든 **타입에 공통적인 멤버들만** 접근할 수 있다.

```typescript
interface Bird {
    fly();
    layEggs();
}

interface Fish {
    swim();
    layEggs();
}

function getPet(): Fish | Bird {
    // ...
}

let pet = getPet();
pet.layEggs(); // okay
pet.swim();    // 에러
```



