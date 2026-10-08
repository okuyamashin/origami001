# おりがみデータの置き場所と書式

おりがみ1種類ごとに、名前、象徴する画像、折り方のデータと画像をまとめて置く。紙芝居のデータ（`data/<選んだ順のおりがみ名>/`）とは分ける。

## 置き場所

```
data/origami/<おりがみ名>/
  origami_jp.md     名前など（言語別）
  origami_en.md
  symbol.png        そのおりがみを象徴する画像
  steps/            折り方のデータと手順図
```

- `<おりがみ名>` は [adding-a-story.md](adding-a-story.md) の表と同じ綴り（`rabbit`、`clane`、`frog`）。
- おりがみの種類を増やすときは、このディレクトリを1つ足す。

## origami_<言語>.md

書き方は [story-format.md](story-format.md) と同じく、`## <セクション名>` で区切る。

| セクション | 内容 |
| --- | --- |
| `origami` | おりがみ名。ディレクトリ名と同じ。全言語で同じ。 |
| `name` | 画面に出す名前。日本語版は小学校で習わない漢字をひらがなにする。`### speech` に読み上げ用の名前を付ける。 |
| `symbol` | 象徴する画像のファイル名を `image: symbol.png` の形で書く。 |

例（`data/origami/clane/origami_jp.md`）：

```
## origami

clane

## name

つる

### speech

鶴

## symbol

image: symbol.png
```

## symbol.png

選択画面などで、そのおりがみを表す画像。画風や大きさは未定。

## steps/

折り方のデータと手順図を置く。データの書式とファイル名は未定で、[folding-policy.md](folding-policy.md) で検討している。
