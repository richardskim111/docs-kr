# 평가방법에 대해서

## 모델 평가방법에 대해서서

提出した予測ファイルが高いCorr,MMC,FNCを示すかはTournament開始時点ではわかりません。\
NMRのペイアウトは1回のラウンドでのパフォーマンスに左右されますが、リーダーボードに掲載される評価や順位は20ラウンド分の評価の平均値を用います。

## 평가의 계산방법

ラウンド`n`での評価は、過去20ラウンドのCorr・MMC・FNCを加重平均することで計算できます。

各ラウンドの「ウェイト」は、Tournamentが終了した日を基準として変化します。新しいラウンドでは低い「ウェイト」を用い、Tournamentの終了日に近づくにつれて「ウェイト」を大きくします。Tournament終了時での「ウェイト」は１ですが、一定に数が経過するとウェイトの大きさを小さくします。以下に、加重平均を計算するコードを示します。

```python
# delta is the difference between the current and target round number
def round_weight(delta, day):
  if delta <= 4:
      return (5 * delta + day) / 20
  elif delta >= 16:
      return (5 * (20 - delta) - day) / 20
  else:
      return 1
```

例えば、ラウンド204の3日目の「ウェイト」 は以下の通りです。

![](<../.gitbook/assets/image (17).png>)

## 예측파일을제출하지 않았을때의 영향

予測ファイルが提出されなかった場合ペナルティが課せられます。

最初の提出が遅れるか、失敗した場合、`example_predictions`と同等のスコアが与えられます。それ以降、予測ファイルが提出されなかった場合、-0.1という非常に低いスコアが与えられます。 このペナルティを回避するためには、[Numerai－CLI](https://jp.docs.numer.ai/numerai-tournament/numerai-compute)が役立ちます。Numerai－CLIを使用すれば毎週の提出ワークフローを自動化できます。
