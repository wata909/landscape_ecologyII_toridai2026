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
- スマホ幅（640px以下）ではパネルが下に移り、「閉じる／開く」で畳める。共有URLから開いたときは畳んだ状態で始まる
- 塗り分け：選択した数値列の最小値〜最大値を白→赤に線形に割り当て
- 数値でない列（`MESH2_C`、`grid_code` など文字列の列）は列リストに出ない
- 座標が緯度経度でない GeoJSON（投影座標系のまま書き出したもの）はエラーメッセージを表示
- ファイルはブラウザ内で読むだけで、どこにも送信しない
- 全地物が同じ値の列（例：1メッシュ分のサンプルの `connect`）は中間色で塗り、凡例に「全地物が同じ値」と表示
- URL に `?data=<GeoJSONのURL>` を付けると、そのファイルを読み込んだ状態で開く（授業での提示用）
  - 例（1メッシュ）：<https://wata909.github.io/landscape_ecologyII_toridai2026/2nd/?data=sample/forest_connectivity_53341135.geojson>
  - 例（96メッシュ）：<https://wata909.github.io/landscape_ecologyII_toridai2026/2nd/?data=sample/forest_grid_connect.geojson>

## 共有URL

パネルの「3 共有する」→「この表示の共有URLを作る」で、今の表示（データ・塗る列・透明度・背景地図）をそのまま開けるURLを作る。

| 読み込み方 | 共有URLの形 | 備考 |
|---|---|---|
| `?data=` で開いた | `…/2nd/?data=<URL>#col=..&op=..&base=..` | 短い。データは元のURLから読む |
| 手元のファイルを選んだ | `…/2nd/#gz=<圧縮データ>&name=..&col=..&op=..&base=..` | データ本体を圧縮してURLに入れる |

- `#` 以降はサーバーに送られない。データはURLの中だけにあり、URLを知っている人は誰でも見られる
- 座標は小数6桁（約0.1m）に丸めて圧縮する。属性値はそのまま
- 目安：1メッシュ分（11地物）で約4KB、96メッシュ分（314地物）で約190KB
- 8,000文字を超えると注意を表示する（メール・LMS・チャットで切れることがある）。切れる場合は GeoJSON を GitHub 等に置き、`?data=` で共有する
- `?data=` に指定する外部URLは CORS を許可している必要がある（`raw.githubusercontent.com`、Gist の raw は可）

## ファイル構成

```
index.html                                  ビューア本体（1ファイル完結）
sample/forest_connectivity_53341135.geojson 連続性指数（Ct = Σ(Ai/At)²、Ci = Ct×Ai/At）を算出済みのサンプル（1メッシュ・11地物）
sample/forest_grid_connect.geojson          同上、3次メッシュ96区画分（314地物）。メッシュ間の差を見る提示用
```

## 依存

- Leaflet 1.9.4（cdnjs から読み込み）
- BIZ UDPゴシック（Google Fonts）
