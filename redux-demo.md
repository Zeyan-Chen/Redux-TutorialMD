# 連雉雞都會的 Redux 教學

create file

```
src
├── store
│   ├── actions.ts
│   ├── reducer.ts
│   ├── index.ts
```

## step1 design state reducer

```javascript
./src/store/reducer.ts

// state
const todolost_state = {
    text: '',
    content: [],
};

// reducer
export const todolist_reducer = (state = todolost_state, action) => {
    switch (action.type) {
        default:
            return state;
    }
};
```

## step2 connect to your module

```javascript
./src/store/index.ts

import { createStore } from 'redux';
import { todolist_reducer } from './reducer';

export default createStore(todolist_reducer);
```

and

```javascript
./src/index.tsx

import { Provider } from 'react-redux';
import store from './store';

render(
    <Provider store={store}>
        <TodoList />
    </Provider>,
    rootElement
);
```

## step2 state render to your module

```javascript
./src/components/App.tsx

import { useSelector } from "react-redux";

const App: React.FC = () => {
  const { text, content } = useSelector(state => state);
  ...
};

```

## step3 action creator

```javascript
./src/store/actions.ts

export const handleOnChange = (e) => ({
    type: 'HANDLEONCHANGE',
    payload: e.target.value,
});
```

and

```javascript
./src/store/reducer.ts

export const todolist_reducer = (state = todolost_state, action) => {
    switch (action.type) {
        case 'HANDLEONCHANGE':
            return { ...state, text: action.payload };
        default:
            return state;
    }
};
```

and

```javascript
./src/components/App.tsx

import { useDispatch } from 'react-redux';
import { handleOnChange } from '../store/actions';

<Input text={text} onChange={(e) => dispatch(handleOnChange(e))} onKeyDown={() => {}} />;
```
