# React에서 TypeScript 사용하기

타입스크립트의 핵심요소들을 알아보았으니 니제 실전을 위해 리액트와 함께 사용할 것이다. 우선, 타입스크립트를 사용하는 리액트 프로젝트를 만들어 보겠다.

```
yarn create react-app react-typescript --template typescript
```

만약, 이미 있는 프로젝트에 타입스크립트를 적용하는 방법은

```
yarn add typescript @types/node @types/react @types/react-dom @types/jest
```

를 입력한 후, 파일이름을 바꾸어주어야 한다. (`App.js` => `App.tsx`) 그리고 development server를 재시작해주면 된다.

---

### App.tsx

프로젝트를 열어보면 src 디렉터리 안에 App.tsx라는 파일이 있다. 타입스크립트를 사용하는 리액트 컴포넌트는 `.tsx`확장자를 사용한다.

```react
import React from 'react';
import logo from './logo.svg';
import './App.css';

const App: React.FC = () => {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.tsx</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

기존의 App.js와 거의 다를게 없지만 새로운 무언가가 추가되었다.

```react
const App: React.FC = () => { ... }
```

`React.FC`라는 것을 사용하여 컴포넌트의 타입을 지정했다. `React.FC`는 해당 컴포넌트가 리액트의 함수형 컴포넌트라는 것을 알려주는 방법이다.

### 새로운 컴포넌트 만들기

Greetings 라는 컴포넌트를 작성하면서 자세히 알아보자

```react
import React from 'react';

type GreetingsProps = {
    name: string;
};

const Greetings: React.FC<GreetingsProps> = ({ name }) => (
	<div>Hello, {name}</div>
);

export default Greetings;
```

`React.FC`를 사용할 땐 props의 타입을 Generics로 넣어서 사용한다. `React.FC`를 사용하면 얻을 수 있는 이점으로 첫번째는 props에 기본적으로 children이 들어가있다는 것이다. 두번째는 컴포넌트의 defaultProps, propTypes, contextTypes를 설정할 때 자동완성이 될 수 있다는 것이다. 

물론 단점또한 존재한다. children이 옵셔널 형태로 들어가서 컴포넌트의 props의 타입이 명백하지 않다고 느낄 수 있다. 그리고 defaultProps가 제대로 작동하지 않는다. 예를 들어 코드를 작성해 보겠다.

```react
import React from 'react';

type GreetingsProps = {
  name: string;
  mark: string;
};

const Greetings: React.FC<GreetingsProps> = ({ name, mark }) => (
  <div>
    Hello, {name} {mark}
  </div>
);

Greetings.defaultProps = {
  mark: '!'
};

export default Greetings;
```

App에서 해당 컴포넌트를 렌더링한다면 `mark`를 `defaultProps`로 넣었음에도 불구하고 `mark`값이 없다면서 제대로 작동하지 않는다. `React.FC`를 생략하면 이 문제는 해결된다. 

이러한 이슈때문에 `React.FC`를 쓰지 말라는 말도 나온다. 