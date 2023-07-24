# React Hooks まとめ

## useState

コンポーネントの状態を管理
state が更新されるとコンポーネントの再レンダリングが行われる

```
const [state, setState] = useState(initialState);
```

### state の遅延初期化

※callback 関数は初回レンダリング時のみ実行される

```
const [state, setState] = useState(() => {
  // 重い処理
  return initialState;
});
```

### state の更新

```
setState(updateState);

// prevState(前回 state)を使用してstateを更新する場合
setState((prevState) => {
  return updateState;
});
```

## useEffect

副作用のある処理を実行させる

※依存配列には state や property 等の useEffect 内で使用されている値を設定する

※依存配列が空の場合は初回レンダリング時のみ実行される

※依存配列が第 2 引数に渡されていない場合、レンダリングの度に実行される

```
use.Effect(() => {
  // DOM の更新、timer 処理、async 関数実行など

  // クリーンアップ
  return () => {
    // ここにクリーンアップ処理を記述
  };
}, [依存配列]);
```

## useRef

DOM 参照、値を保持したいけど再レンダリングさせたくない場合に使用する

```
// 値の設定
const exampleRef = useRef(保持する値);

// 値の参照
console.log(exampleRef.current); // 保持する値
```

DOM 参照する場合
→ ref 属性に渡す

```
const buttonRef = useRef(null);
return (
  <button ref={buttonRef}>button</button>
);
```

## useReducer

state と似ている
違いは更新関数を定義できる

```
// 更新関数
const reducer = (state, action) => {
  switch(action) {
  // action による処理の分岐
  }

  return newState; // 新しく設定する state を返す
};

const [state, dispatch] = useReducer(reducer, initialState);

// action を呼び出す
dispach('action 名');
```

## useContext

グローバルステートが必要な場合に使用
以下の例は ExampleProvider で囲まれたコンポーネントで useContext を使用して exampleState にアクセスできる

```
const ExampleContext = createContext();

const ExampleProvider = ({children}) => {
  const exampleState = {}; // グローバルステート

  return (
    <ExampleContext.Provider value={exampleState}>
    {children}
    </ExampleContext.Provider>
  );
};

// 使用時
const exampleState = useContext(ExampleContext);
```

## useCallback

関数のキャッシュを行う
React.memo でメモ化したコンポーネントに props で関数を渡す場合に使用
→ 親コンポーネントの再レンダリングで関数が生成され Object.is で等価にならない
→ React.memo でメモ化しても props の変更を検知し再レンダリングされる

```
const func = useCallback(メモ化する関数, [依存配列]);
```

## useMemo

値や関数、JSX 等なんでもキャッシュする
計算コストが高い場合に有効
※コストがかかるためなるべく使わない

```
const memo = useMemo(メモ化する値, [依存配列]);
```
