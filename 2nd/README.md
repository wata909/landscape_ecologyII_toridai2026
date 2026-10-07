# 連続性マップ（景観生態学II 第2回）

Colab で算出した森林連続性指数（GeoJSON）を、地図上で白→赤の塗り分けで表示するページ。

**サイト：<https://wata909.github.io/landscape_ecologyII_toridai2026/2nd/>**

## 使い方

1. 上のサイトを開く
2. 「GeoJSON を選ぶ」から `forest_connectivity_53341135.geojson` を選ぶ（地図へのドラッグ＆ドロップでも可）
3. 「色を塗る列を選ぶ」で `connect_rev` が選ばれていることを確認（`connect_rev` があれば自動で選択される）
4. 赤いほど値が大きい（連続性が高い）。ポリゴンをクリックすると属性が表示される

## 仕様

- 背景地図：地理院タイル（淡色地図／標準地図／写真）
- 塗り分け：選択した数値列の最小値〜最大値を白→赤に線形に割り当て
- 数値でない列（`MESH2_C`、`grid_code` など文字列の列）は列リストに出ない
- 座標が緯度経度でない GeoJSON（投影座標系のまま書き出したもの）はエラーメッセージを表示
- ファイルはブラウザ内で読むだけで、どこにも送信しない
- URL に `?data=<GeoJSONのURL>` を付けると、そのファイルを読み込んだ状態で開く（授業での提示用）
  - 例：<https://wata909.github.io/landscape_ecologyII_toridai2026/2nd/?data=sample/forest_connectivity_53341135.geojson>

## ファイル構成

```
index.html                                  ビューア本体（1ファイル完結）
sample/forest_connectivity_53341135.geojson 連続性指数（Ct = Σ(Ai/At)²、Ci = Ct×Ai/At）を算出済みのサンプル
```

## 依存

- Leaflet 1.9.4（cdnjs から読み込み）
- BIZ UDPゴシック（Google Fonts）
