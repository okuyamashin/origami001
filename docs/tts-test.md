# 読み上げのテスト手順（Amazon Polly）

タイトルのIPA `ot͡sɯkisama no sɯzɯ` をPollyで読み上げたところ、「お月さまのすず」に聞こえなかった（`data/rabbit-clane-frog/sample-title.mp3`）。原因を切り分けるため、同じ声で4通りの渡し方を聞き比べる。

## 最初の結果（sample-title.mp3）

`ot͡sɯkisama no sɯzɯ` が「おりつーくいさんおりすーずー」と聞こえた。IPA自体は日本語の書き方として合っており、声が一部の記号を正しく扱えていないときの崩れ方と考えられる。

| 書いたIPA | 本来の音 | 聞こえた音 | 考えられること |
| --- | --- | --- | --- |
| `o` | お | おり | 先頭の音に余計な音が付いた |
| `t͡sɯ` | つ | つー | `ɯ` が長い「ウー」になった |
| `ki` | き | くい | 「き」の音がうまく作れていない |
| `sama` | さま | さん | 後半の音が落ちた |
| `no` | の | おり | 別の音に置き換わった |
| `sɯzɯ` | すず | すーずー | `ɯ` が長い「ウー」になった |

一番はっきりしているのは `ɯ`。日本語の「う」を表す正しい記号だが、2か所とも「ウー」と長く読まれている。声が `ɯ` を知らず、英語の長い「ウー」のような音で代用したときによく起きる。

原因の候補：

- 日本語以外の声（英語の声など）で読ませた
- 日本語の声だが、その声が受け付けるIPAの記号が、書いたものと違う

確かめること：

- 使った声（`--voice-id`）とエンジン（`neural` か `standard` か）を記録する。
- 下の B・C を同じ日本語の声で試す。B は `ɯ` の代わりに `u` を使った B2 も試し、`ɯ` が原因かどうか切り分ける。

## 考えられる原因

1. **IPAが発音の指定として渡っていない**：`<phoneme>` タグで囲まずに文字のまま渡すと、アルファベットとして読まれる。
2. **声がIPAの記号を正しく扱えていない**：声ごとに受け付ける記号が決まっている。つなぎ記号（`t͡s` の `͡`）や単語間のスペースで崩れることがある。
3. **日本語以外の声で読ませた**：`ɯ` や `ɕ` は英語にない音なので、近い英語の音に置き換えられる。
4. **アクセントがない**：IPAでは音の高低を書いていないので、音が合っていても平らで不自然になる。

## 比べる4つの渡し方

どれも日本語の声（`Kazuha`、`Takumi`、`Tomoko` など）で、すべて同じ声を使う。

| 記号 | 渡し方 | SSML |
| --- | --- | --- |
| A | 文字のまま | `<speak>お月さまのすず</speak>` |
| B | IPA（つなぎ記号とスペースなし） | `<speak><phoneme alphabet="ipa" ph="otsɯkisamanosɯzɯ">お月さまのすず</phoneme></speak>` |
| B2 | IPA（`ɯ` を `u` に置き換え） | `<speak><phoneme alphabet="ipa" ph="otsukisamanosuzu">お月さまのすず</phoneme></speak>` |
| C | よみがな指定 | `<speak><phoneme alphabet="x-amazon-yomigana" ph="おつきさまのすず">お月さまのすず</phoneme></speak>` |

C の `x-amazon-yomigana` は、Polly の日本語向けの読み指定。エラーになる場合は、そのエラー内容を記録する。

## 実行例（AWS CLI）

```sh
aws polly synthesize-speech \
  --engine neural \
  --voice-id Kazuha \
  --text-type ssml \
  --output-format mp3 \
  --text '<speak><phoneme alphabet="ipa" ph="otsɯkisamanosɯzɯ">お月さまのすず</phoneme></speak>' \
  sample-title-B.mp3
```

- `--text` の中身を A・B・B2・C で入れ替え、出力ファイル名を `sample-title-A.mp3`・`sample-title-B.mp3`・`sample-title-B2.mp3`・`sample-title-C.mp3` にする。
- `--engine neural` でタグがエラーになる場合は、`--engine standard`（声は `Takumi` または `Mizuki`）でも試す。

## 結果の記録

| 記号 | 声・エンジン | 聞こえ方 | エラー |
| --- | --- | --- | --- |
| A | | | |
| B | | | |
| B2 | | | |
| C | | | |

## 判断の目安

- **C が一番自然な場合**（「おつきさまのすず」と正しく聞こえる）：日本語はよみがな、ほかの言語はIPAで書く形に、`docs/story-format.md` の書式を変える。
- **B がよくなる場合**：IPAの書き方をその声に合わせて直す（つなぎ記号やスペースを使わないなど）。
- **B2 だけがよくなる場合**：`ɯ` が原因。IPAでは「う」を `u` で書く。
- **A で十分な場合**：読み指定は、間違えた語だけに付ける。
