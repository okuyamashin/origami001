# おりがみデータの置き場所と書式

おりがみ1種類ごとに、名前、象徴する画像、折り方のデータと画像をまとめて置く。紙芝居のデータ（`data/<選んだ順のおりがみ名>/`）とは分ける。

## 置き場所

```
data/origami/<おりがみ名>/
  origami_jp.md     名前など（言語別）
  origami_en.md
  card-front.png    象徴するカードの表（ボタニカルアート）
  card-back.png     象徴するカードの裏（折り上がったおりがみ）
  card-prompts.md   カードの画像を作るプロンプト
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
| `card` | 象徴するカードの画像のファイル名を、`front: card-front.png` と `back: card-back.png` の2行で書く。 |

例（`data/origami/clane/origami_jp.md`）：

```
## origami

clane

## name

つる

### speech

鶴

## card

front: card-front.png
back: card-back.png
```

## 象徴するカード（card-front.png・card-back.png）

選択画面などで、そのおりがみを表すカード。表と裏の2枚の画像で作る。

| 項目 | 内容 |
| --- | --- |
| 比率 | トランプと同じ縦長の 5:7（63×88mm）。縦向き。 |
| 表（`card-front.png`） | ストーリーと同じボタニカルアートの画風で、その動物を1匹描く。外見と小物はストーリーと同じ（例：うさぎは青いスカーフ）。 |
| 裏（`card-back.png`） | 折り上がったおりがみの画像。 |
| 文字・枠 | 画像には文字、数字、四隅のマーク、枠を入れない。必要ならアプリ側で付ける。 |

- 画像生成で 5:7 が指定できない場合は、縦長（例：1024×1536）で作り、上下を切って 5:7（例：1024×1434）にする。切っても動物が欠けないよう、上下に余白をとった構図にする。
- 表のプロンプトは `card-prompts.md` の `## front` に、ストーリーの `prompts.md` と同じ分け方（style・character・scene・composition・constraints）で書く。

### 作る順番

1. 表：ストーリーの画像と同じように、いつでも作れる。
2. 裏：完成形がほぼ決まっているおりがみ（うさぎ、鶴、蛙）は先に作る。`steps/` の折り方のデータを作った後、形が違っていたら、それに合わせて作り直す。
   - 裏のプロンプトは `card-prompts.md` の `## back` に、style・paper（紙の表裏の色）・model（折り上がりの形）・composition・constraints で書く。
   - 紙の表裏の色は、折り方のデータ（表と裏で色が違う正方形）とそろえる。

## steps/

折り方のデータと手順図を置く。データの書式とファイル名は未定で、[folding-policy.md](folding-policy.md) で検討している。
