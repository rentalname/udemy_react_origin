# react-redux ランチミーティング 2017/10/21

## TOC
+ Pureなreact-jsにおける状態管理
+ Fluxアーキテクチャ
+ Redux
+ Redux principle
  + Single source of truth
  + State is read-only
  + Changes are made with pure functions
+ Reduxにおける用語解説
  + View
    + Presentational component
    + Container component
  + Action
  + Reducer
  + Middleware
  + Store
  + connect
    + mapStateToProps
    + mapDispatchToProps

## Pureなreact-jsにおける状態管理
+ componentの状態はthis.stateで管理する

### 開発の大規模化
+ 深まるコンポーネントのネスト
+ 状態をつかいやすく管理したい

## Fluxアーキテクチャ
https://reactjs.org/blog/2014/07/30/flux-actions-and-the-dispatcher.html

## Redux
+ Fluxアーキテクチャを実装したライブラリー

## Redux principle
### Single source of truth
+ storeは1つ
+ storeの状態が正

### State is read-only
+ Stateは参照するだけ
+ 更新がしたいときはreducerを経由する

### Changes are made with pure functions
+ reducerによってstoreを更新する場合, 同じ入力に対しては常に同じ出力を返す
  + 同じ入力とは, 変更前のstateとreducerに渡されるオブジェクトの組

## Reduxにおける用語解説
### View
+ reactを使う場合はReact.Component
  + Presentational component
    + Redux的な分類
    + コンポーネント自身のpropsにのみ依存して表示が変わる
  + Container component
    + storeの状態によって表示が変わる
    + actionを介してstoreを更新する
    + connectされるコンポーネント

### Action
+ コンポーネントから呼び出されて, 外部環境との処理結果をreducerに通知する

### Reducer
+ Actionからの通知を受けてstoreを更新する
+ 他のreducerから直接呼ばれることもある(たしか)
+ storeの更新を行えるのはreducerだけ(決まり事)

### Middleware
+ rack middlewareに近い概念
+ reducerの処理に割り込んで, デバッグツールを使えるようにしたり, 非同期のメソッドを同期的に扱えるようにしたりする(らしい)

### Store
+ ブラウザ上に構築された状態のかたまり

### connect
+ 指定したコンポーネントがstoreの更新を検知できるようにする
+ ↓みたいな使い方をする
```js
connect(mapStateToProps, mapDispatchToProps)(myComponent)
```
+ mapStateToProps
  + storeからコンポーネントの表示のために必要な状態を取り出して, 反映させる処理を記述する
+ mapDispatchToProps
  + コンポーネントに必要なactionをpropsに設定するための処理を記述する
