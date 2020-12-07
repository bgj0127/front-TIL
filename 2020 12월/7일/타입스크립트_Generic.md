# Generics

**Generics**은 타입스크립트에서 함수, 클래스, 인터페이스, 타입을 사용하게 될 때 여러 종류의 타입에 대하여 호환을 맞춰야 하는 상황에서 사용하는 문법이다.

---

### 함수에서 Generics 사용하기

객체 A, B를 합치는 merge 라는 함수를 만든다고 할 때 A 와 B 가 어떤 타입이 올지 몰라 any라는 타입을 사용할 수 있다.

```typescript
function merge(a: any, b: any) {
    return {
        ...a,
        ...b
    };
}

const merged = merge({ foo: 1 }, {bar: 1 }); 
```

그러나 이렇게 하면 타입스크립트를 사용하는 의미가 없어진다. merged 안에 무엇이 있는지 알 수 없기 때문이다. 이런 문제를 제네릭을 사용하여 해결할 수 있다.

```typescript
function merge<A, B>(a: A, b: B): A & B {
    return {
        ...a,
        ...b
    };
}

const merged = merge({ foo: 1 }, {bar: 1 }); 
```

제네릭을 사용할 때는 < T > 처럼 꺽쇠 안에 타입의 이름을 넣어서 사용한다. 제네릭을 사용하면 함수의 파라미터로 넣은 실제 값의 타입을 활용하게 된다. 

---

### Interface 에서 Generics 사용하기

```typescript
interface Items<T> {
    list: T[];
}

const items: Items<string> = {
    list: ['a', 'b','c']
};
```

---

### Type alias 에서 Generics 사용하기

```typescript
type Items<T> = {
    list: T[];
};

const items: Items<string> = {
    list: ['a', 'b', 'c']
};
```

