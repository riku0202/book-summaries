# 2 章

## 2.0

- chrome に採用されている Blink は webkit をフォークして作られた
- webkit 系のレンダリングエンジンが大半を占めている

## 2.2.1

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

- 
