# 読み上げのテスト手順（Amazon Polly）

タイトルのIPA `ot͡sɯkisama no sɯzɯ` をPollyで読み上げたところ、「お月さまのすず」に聞こえなかった（`data/rabbit-clane-frog/sample-title.mp3`）。原因を切り分けるため、同じ声で3通りの渡し方を聞き比べる。

## 考えられる原因

1. **IPAが発音の指定として渡っていない**：`<phoneme>` タグで囲まずに文字のまま渡すと、アルファベットとして読まれる。
2. **声がIPAの記号を正しく扱えていない**：声ごとに受け付ける記号が決まっている。つなぎ記号（`t͡s` の `͡`）や単語間のスペースで崩れることがある。
3. **日本語以外の声で読ませた**：`ɯ` や `ɕ` は英語にない音なので、近い英語の音に置き換えられる。
4. **アクセントがない**：IPAでは音の高低を書いていないので、音が合っていても平らで不自然になる。

## 比べる3つの渡し方

どれも日本語の声（`Kazuha`、`Takumi`、`Tomoko` など）で、3つとも同じ声を使う。

| 記号 | 渡し方 | SSML |
| --- | --- | --- |
| A | 文字のまま | `<speak>お月さまのすず</speak>` |
| B | IPA（つなぎ記号とスペースなし） | `<speak><phoneme alphabet="ipa" ph="otsɯkisamanosɯzɯ">お月さまのすず</phoneme></speak>` |
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

- `--text` の中身を A・B・C で入れ替え、出力ファイル名を `sample-title-A.mp3`・`sample-title-B.mp3`・`sample-title-C.mp3` にする。
- `--engine neural` でタグがエラーになる場合は、`--engine standard`（声は `Takumi` または `Mizuki`）でも試す。

## 結果の記録

| 記号 | 声・エンジン | 聞こえ方 | エラー |
| --- | --- | --- | --- |
| A | | | |
| B | | | |
| C | | | |

## 判断の目安

- **C が一番自然な場合**：日本語はよみがな、ほかの言語はIPAで書く形に、`docs/story-format.md` の書式を変える。
- **B がよくなる場合**：IPAの書き方をその声に合わせて直す（つなぎ記号やスペースを使わないなど）。
- **A で十分な場合**：読み指定は、間違えた語だけに付ける。
