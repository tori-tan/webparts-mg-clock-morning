# webparts-mg-clock-morning

## 概要

時計ウィジェットです。12 時間表記、日付、LIVE チップ、3:2 メディア枠とオーバーレイを表示します。数字は桁ぶれ防止のレイアウトで描画されます。

## clock.htm の使い方（OBS 想定）

### OBS Browser Source に読み込む

1. ソースに追加
   1. OBS で「ソース」→「+」→「ブラウザ」を追加。「ローカルファイル」をオンにして、本リポジトリの `clock.htm` を指定。
   2. または `clock.htm` を OBS へドラッグ。
2. 幅/高さは任意（推奨: 幅 350, 高さ 320）。コンポーネントは中身にフィット表示されます。
3. 必要に応じて「表示されたときにブラウザをリフレッシュ」をオン。
4. 「カスタム CSS」に好みのスタイルを貼り付けて外観を調整できます（下記サンプル）。

ヒント

- フォント「Delius Swash Caps」は Google Fonts から読み込まれます（OBS の Chromium 内で自動取得）。ネットワーク制限がある環境では表示が変わる場合があります。
- 1 秒ごとに更新、日付は深夜 0 時に更新されます。

## カスタマイズ（カスタム CSS）

以下を OBS の「カスタム CSS」に貼り付けて使ってください。必要な部分だけで OK です。

### デフォルトメディア画像 非表示

```css
/* デフォルトメディア画像 非表示 */
.wp-media-slot-inner {
  display: none;
}
```

デフォルトメディアを非表示にし、クロマキーで色を抜くことで、枠内を透明にできます。つまり別の画像などを配置することができます。

デフォルトのメディア枠の色は緑です。  
フィルター → エフェクトフィルター → クロマキーを追加してください。  
削除されるものが多い場合は、類似性、滑らかさを調整してください。

### メディア枠の背景色変更(クロマキー色変更用)

```css
/* デフォルトメディア画像 非表示 */
.wp-media-slot-inner {
  display: none;
}
/* メディア枠の背景色変更(クロマキー色変更用) */
.wp-media-slot {
  background-color: #ffff00;
}
```

クロマキー用の色と、アイコンなどの色が被る場合に、適当な色に変更してください。  
クロマキーの色キーの種類を変更してください。

### アイコンの差し替え

```css
/* アイコン差し替え */
.wp-media-effect1::before {
  content: "⭐";
}
.wp-media-effect2::before {
  content: "🎉";
}
```

### アイコンを画像に差し替え

```css
/* アイコンを画像に変更(右) */
.wp-media-effect1::before {
  content: none;
}
.wp-media-effect1 {
  /* サイズ */
  width: 80px;
  height: 80px;
  /* 画像を指定(WEB上のファイルを指定) */
  background-image: url("https://example.com/icon1.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}
/* アイコンを画像に変更(左) */
.wp-media-effect2::before {
  content: none;
}
.wp-media-effect2 {
  /* サイズ */
  width: 80px;
  height: 80px;
  /* 画像を指定(WEB上のファイルを指定) */
  background-image: url("https://example.com/icon1.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}
```

画像の URL、サイズを調整してください。

ローカルファイルは以下のように指定したら大丈夫なはず……だけど表示されないのでどこか間違ってるのか。

```css
/* 画像を指定(ローカルのファイルを指定) */
background-image: url("file:///C:/Users/you/Pictures/obs-icon.png");
```

### アイコンの位置

```css
/* アイコン配置を調整 */
.wp-media-effect1 {
  top: 4px;
  right: 12px;
}
.wp-media-effect2 {
  bottom: 4px;
  left: 12px;
}
```

### アイコン非表示

```css
/* アイコン(右)を非表示 */
.wp-media-effect1 {
  display: none !important;
}
/* アイコン(左)を非表示 */
.wp-media-effect2 {
  display: none !important;
}
```

### 色・バッジ

```css
/* LIVEバッジの色変更 */
.wp-live {
  background: #d81b60;
}
/* AM/PMバッジの色変更 */
.wp-ampm {
  background: #37474f;
}
```

### メディア枠の比率調整

```css
/* メディア枠の比率調整 */
.wp-media-slot {
  aspect-ratio: 3 / 2;
}
```

### メディア枠非表示

```css
/* メディア枠非表示 */
.wp-media-slot {
  display: none !important;
}
```

### (参考)OBS 追加時の標準

```css
body {
  background-color: rgba(0, 0, 0, 0);
  margin: 0px auto;
  overflow: hidden;
}
```

## ファイル構成（抜粋）

- `clock.htm` … OBS 向けの時計ウィジェット本体
- `LICENSE` … ライセンス
- `README.md` … この説明

## トラブルシュート

- フォントが反映されない: ネットワーク制限で Google Fonts にアクセスできない可能性。OBS の「ブラウザ」ソースがインターネットにアクセスできるか確認。

## ライセンス

`LICENSE` を参照してください。
