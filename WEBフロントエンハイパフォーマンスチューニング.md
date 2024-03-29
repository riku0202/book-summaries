# 2 章

## 2.0

- chrome に採用されている Blink は webkit をフォークして作られた
- webkit 系のレンダリングエンジンが大半を占めている

## 2.2

- ブラウザ内のコンポーネント

  - レンダリングエンジン
    - ブラウザ内で利用される HTML の描画エンジン
      - HTML や画像ファイルや CSS、JS などの各種リソースを読み取って、それを画面上の実際のピクセルとして描画する
      - 描画するだけで、ユーザーインターフェースを持っていない
      - メールクライアントでも利用されるケースがある
    - Javascript エンジン
      - JS の実行環境を提供するコンポーネント
      - V8,Chakra,SpiderMonkey など
      - DOM ツリーや CSSOM ツリーなどの内部オブジェクトや API に JS をからアクセスできるようにバインディグが提供される

## 2.3

- loading
  - download
  - parse
- scripting
- rendering
  - calculateStyle
  - layout
- painting
  - paint
  - rasterize
  - compositeLayers

## 2.4

- parse
  - リソースを構文解析し、レンダリングエンジンの内部表現に変換
    - HTML → DOM ツリー
    - CSS → CSSOM ツリー
- リソースの取得フロー
  - URL のホスト名解決
  - HTTPS による取得
    - TCP の接続確立
    - TLS の接続確立
    - リクエスト送信、レスポンスの受け取り
- IP
  - パケットの内容が壊れる事がある
  - 送信したパケットが消失することがある
  - パケット
    - データ通信に利用される最小単位
    - IP ヘッダー + データ
    - 通信速度はパケットが届く速さに依存する
- TCP
  - 相手先にデータが届いてるか確認
  - データの欠損、破損を検知
  - 送信順を保証
  - 相手の IP アドレスとポート番号を指定してコネクションを確立する
  - ３ウェイハンドシェイク
    1. クライアントがサーバーに対して SYN パケットを送信
    2. SYN パケットを受け取ったサーバーは、接続を許可する SYN-ACK パケットをクライアントへ送信
    3. SYN-ACK パケットを受け取ったクライアントは、接続を開始する ACK パケットを送信し通信を開始
  - TCP の確率にパケットを３回やり取りする必要がある
  - CSSOM ツリーの深さは一定

## 2.5

- どのように実行されるかはブラウザの JavaScript エンジンによって異なる
- JS コードを字句解析してトークン列に変換
- トークン文字列を構文解析で抽象構文木に変換
- 抽象構文木をコンパイラで実行可能な形式に変換
  - このコンパイル処理がブラウザ依存
  - JIT コンパイル型が多い
    - 実行時にコンパイルして実行する
    - 事前にコンパイルするのは AOT

## 2.6

- Rendering(レイアウトツリー構築)
  - スタイルの計算(Calculation Style)
    - DOM ツリー内のすべての DOM 要素に対してどのような CSS プロパティが当たるか計算
    - DOM 要素に対して、どの CSS ルールが当たるかを計算したあと、詳細度を算出してどのような CSS プロパティが当たるか判断する
  - レイアウト情報
    - 大きさ・マージン・パディング・位置・ｚ軸の位置

## 2.7

- レンダリング結果の描画（Painting）
  - Paint
    - 低レベルな２ D グラフィックエンジン向けの命令を生成する
    - displayList と呼ばれる命令の列を生成
    - 異なるグラフィックエンジンでも組み込める
  - Rasterize
    - ピクセルへ描画する
    - レイヤーという他にで描画
    - レイヤーはｚ軸の上下関係をもつ
    - レイヤーが生成される条件
      - position:absolute を持っている
      - position:fixed を持っている
      - transform:translate3d などの GPU で描画・ごうせされる CSS プロパティを持っている
      - opacity プロパティを持っていて、背後にコンテンツが表示される必要がある
    - スクロールしたときなどレイヤーが再利用される（移動するだけ）
  - CompositeLayers
    - transformCSS プロパティで 3D 変形関数を指定した時 GPU で合成される

## 3.1

- パフォーマンスチューニングはある前提条件の上で適用することで初めて効果を発揮するものがある

## 3.2

- 推測するな、計測せよ
- ボトルネックを探し出す

## 3.3

- RAIL というパフォーマンス指標
  - Response 100 ミリ秒
  - Animation 16 ミリ秒
    - フレーム中の 1 フレームの処理の時間の目安
  - Idle 50 ミリ秒
  - Load 1000 ミリ秒

## 3.5

- Network パネル
  - 青い線は DOMContentLoaded
  - 赤い線は Load イベントが発生した時点
- Memory パネル
  - メモリの利用状況を計測できる
  - メモリリークの検知
  - メモリの使いすぎ
- JS によるパフォーマンス計測もできる
  - 計測用のコードを仕込む
  - NavigationTimingAPI による計測
    - ブラウザの各段階の処理時間を計測できる
  - UserTimingAPI による計測
  - ResourceTimingAPI による計測
  - PerformanceObserver による継続的な計測
  - 高精度なタイムスタンプの利用

## 3.8

- パフォーマンスの継続的な監視

## 4.1

- リソース取得の最適化
  - 読み込むリソースの大きさと数を減らす
  - レンダリングをブロックする読み込みを減らす
  - ブラウザとサーバー間の遅延を減らす
  - ブラウザのキャッシュを活用する

## 4.3

- 画像ファイルの最適化
  - JPEG
    - jpegtran
    - mozjpeg
  - PNG
    - ZopfliPNG
    - pngquant
    - Pngcrush
  - GIF
    - GIFsicl

## 4.5

- CSS 内での外部 import は避ける
