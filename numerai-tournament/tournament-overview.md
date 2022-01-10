---
description: 공식규칙 및 시작 전 가이드
---

# 토너먼트 소개

## 소개

Numerai (뉴머라이) 토너먼트란 주식시장의 동향을 예측을 통해 경쟁하는 플랫폼입니다. 참가자는 암호화된 데이터를 사용해 기계학습 모델을 구축한뒤 예측파일을 제출해서 토너먼트에 참가 할 수 있습니다.

토너먼트에 제출 되는 예측파일에 Numeraire (NMR - 뉴머레어) 암호화폐를 걸면 퍼포먼스에 준하는 NMR을 획득할 수 있습니다. 뉴머라이에 제출 된 여러분들의 예측파일은 뉴머라이가 운용하는 헤지펀드의 모델(메타모델)을 설계하는데에 사용됩니다.

밑에 보이는 유튜브 영상을 보시면 어떤 형식으로 데이터가 사용되는지 알 수 있습니다.

{% embed url="https://youtu.be/dhJnt0N497c" %}

## **개요**

1. 뉴머라이에 등록 합니다.&#x20;
2. 학습데이터와 샘플스크립트를 포함한 데이터셋을 다운로드 받습니다.&#x20;
3. 모델을 작성하고 예측치를 뉴머라이에 제출합니다.&#x20;
4. 모델에 NMR을 걸어 퍼포먼스에 따른 NMR을 획득하거나 상실하게 됩니다.
5. 매주 예측파일 제출 절차를 자율화 할 수 있습니다.

## 데이터

뉴머라이 토너먼트에 참여하시면 무료로 고퀄리티 금융 데이터셋을 사용할 수 있습니다. 데이터셋은 정화 후 정규화와 암호화 된 고퀄리티의 재무데이터로 구성 되어 있습니다.

![](../.gitbook/assets/data.png)

제출되는 학습 데이터는 각 id는 암호화 되어 있는 feature set (특징셋)을 주식의 target(타겟)은 4주후 미래의 퍼포먼스를 나타냅니다. <mark style="color:red;background-color:red;">\[다른 시점을 나타내는 eras 로 그룹화 되어있습니다.]</mark>

## 기계학습 모델링

토너먼트 안에서 여러분들의 목표는 과거의 데이터를 통해 예측 모델을 작성하고 해당 모델을 사용하여 미래 주식시장을 예측하는 것이 목적입니다. 과거의 학습 데이터를 사용하여 모델을 학습시키고 라이브 토너먼트 데이터를 예측합니다. 파이썬의 XGBoost를 사용한 기본적인 예를 밑에 보시기 바랍니다.&#x20;

```python
import pandas as pd
from xgboost import XGBRegressor

# training data contains features and targets
training_data = pd.read_csv("numerai_training_data.csv").set_index("id")

# tournament data contains features only
tournament_data = pd.read_csv("numerai_tournament_data.csv").set_index("id")
feature_names = [f for f in training_data.columns if "feature" in f]

# train a model to make predictions on tournament data
model = XGBRegressor(max_depth=5, learning_rate=0.01, \
                     n_estimators=2000, colsample_bytree=0.1)
model.fit(training_data[feature_names], training_data["target"])

# submit predictions to numer.ai
predictions = model.predict(tournament_data[feature_names])
predictions.to_csv("predictions.csv")
```

파이썬이 아니라도 참가자분들은 개개인 좋아하시는 프로그래밍언어를 자유롭게 사용하실 수 있습니다.

## 예측파일 제출

매주 `토요일 18:00 UTC (한국시간 일요일 03:00 KST)`에 새로운 라운드가 시작되며 새로운 토너먼트 데이터가 공개됩니다. 새 라운드에 참여하시려면 그 라운드의 연관된 데이터셋를 사용하셔서 예측값이 들어간 파일을 생성하고 뉴머라이에 제출하시면 됩니다.

![](../.gitbook/assets/data\_release.png)

마감시간은 매주 `월요일 14:30 UTC (한국시간 월요일 23:30 KST)`입니다. 제출이 늦어질 경우 토너먼트 참여에서 제외됩니다.

[Numerapi](https://github.com/uuazed/numerapi) (파이썬)나 [Rnumerai](https://github.com/Omni-Analytics-Group/Rnumerai) (R)또는 [GraphQL API](https://api-tournament.numer.ai)를 사용해서 제출을 수동화 할 수 도 있습니다. 다음은 코드의 예입니다.

```python
import numerapi
napi = numerapi.NumerAPI("public_id", "secret_key")

# download data
napi.download_current_dataset(unzip=True)

# upload predictions
napi.upload_predictions("predictions.csv", model_id="model_id")
```

또는 [Numerai Compute](https://github.com/numerai/numerai-cli) 툴을 이용해 매주 예측 파일 제출을 자동화 할 수도 있습니다.

```python
# setup your cloud infrastructure
numerai setup

# copy the example model
numerai docker copy-example

# deploy the example model 
numerai docker deploy
```

## 모델 진단

모델의 성능은 Diagnostics 기능을 이용하셔서 진단할 수 있습니다. 과거의 데이터에서 제출한 예측파일의 성능과 리스크를 측정해 주는 기능입니다.

{% hint style="info" %}
**이 진단 툴을 반복적으로 사용하시면 바로 과적합화 될 수 있습니다. 본 툴은 최종 확인용으로 사용하는 것이 좋습니다.**
{% endhint %}

![](../.gitbook/assets/diagnostics.gif)

**더 자세한 내용은** [**이 게시판에 글**](https://forum.numer.ai/t/model-diagnostics-update/902)**을 참고해 주세요.** 이 진단 툴을 반복적으로 사용하시면 바로 과적합화 될 수 있습니다. 본 툴은 최종 확인용으로 사용하는 것이 좋습니다.

## 모델의 평가방법

あなたが提出した予測結果は、あなたの予測と真のターゲットの `correlation` (ここではspearmanの順位相関)でスコアリングされます。相関性が高いほど高いペイアウトを得られます。\\

{% tabs %}
{% tab title="scoring:function.py" %}
```python
# method='first' breaks ties based on order in array
ranked_predictions = predictions.rank(pct=True, method="first")
correlation = np.corrcoef(labels, ranked_predictions)[0, 1]
```
{% endtab %}
{% endtabs %}

予測結果は、メタモデルへの寄与（mmc)と機能の中立的な相関(fnc)についてもスコアが付けられます。\
\
各提出物は、Tournamentが開始してから4週間にわたって評価されます。締め切り後の木曜日に最初の評価を受け取り、4週間後の水曜日に最終スコアを受け取ることができます。合計で20スコアの加重平均値がペイアウトされるNMRの量を決定します。\
![prediction.csv](../.gitbook/assets/schedule1.png)

Tournamentが終了するまでには約4週間かかるため、毎週新しい予測ファイルを提出すると、進行中の4つのラウンドから各スコアリング日に複数（最大4）の評価を受け取ります。 ![prediction.csv](../.gitbook/assets/schedule2.png)

モデルのライブスコアは、プロフィールページで公開されています。これは、過去20ラウンドにわたるモデルの最終スコアの例です。 ![prediction.csv](../.gitbook/assets/schedule3.png)

特定のラウンドにズームインして、ラウンド内の毎日のスコアを確認することもできます。 ![prediction.csv](../.gitbook/assets/schedule4.png)

## 스테이킹과 페이아웃

[シビル攻撃](https://en.wikipedia.org/wiki/Sybil\_attack)などのNumeraiにとって不都合な攻撃を防止しつつNMRをペイアウトするにはどのようなシステムを設計すればよいでしょうか？\
\
その答えはステーキング(=預け入れ)です。各参加者はNMRを掛け金として自分の予測の正確さを担保します。NMRのステーク量が多ければ多いほど予測に自信をもっているとみなします。\
\
Numeraiは正確な予測ファイルの提出を望んでおり、良い予測には高い報酬で報います。\
\
どれだけのNMRを得られるかはNMRのステーク量と、Corr,MMCの値に依存します。\
これは、[Skin in the Game](https://www.amazon.com/dp/B075HYVP7C/)という本で述べられているメゾットを使用しています。\
\
NumeraiにNMRをステーキングする場合、Numeraiはシビル耐性のある方法を提供します。NMRのペイアウトはステーク量に比例するため、複数のアカウントを作成するだけでは多くのペイアウト得ることができません。\
\
もちろん、NMRをステークせずにNumeraiに参加することもできます。\
例えば、Tournamentの詳細や自分のモデルの性能を知るために、NMRをステークしないのは良いテストとなるでしょう。\
自分のモデルに自信が持てるようになったら、そのモデルにステークすることができます。ステークの最小値は3NMRです。\\

## 스테이킹 금액변경

Numeraiのウェブサイトでは、「Manage Stake」をクリックしてステーク量を管理できます。このモーダルを使用すれば、NMRのステーク量を増減したり、`Corr`、`Corr+1/2MMC`、`Corr+MMC`、`Corr+2MMC`にベットできます。\
\
ステーキングとは、NMRをイーサリアムブロックチェーンのスマートコントラクトに固定することを意味します。ステーク中はNumeraiがロックアップされたNMRを増減させる権利を保有します。\
\
![](../.gitbook/assets/image%20\(18\).png)

NMRのステーク量を増やすと、あなたのウォレットからNMRが引き出され、Numeraiの保有しているアカウントにNMRが移送されます。\
NMRのステーク量を減らすと、Numeraiの保有しているアカウントからNMRが移送され、あなたのウォレットに入金されます。

ステーク量への変更はすぐに適用されるのではなく、約4週間後に反映されます。これは、Tournamentの終了期間が4週間であることに起因します。

## 페이아웃

どれだけのNMRを得られるかはNMRのステーク量と、Corr,MMCの値に依存します。\
\
スコアが高いほど、より多くのNMRを得ることができます。もし負のCorr,MMCとなった場合、ステークしたNMRの一部が没収され、バーンされます。\
バーンとはERC-20トークンの持つ機能の一つであり、トークンを永遠に使用できなくする操作のことです。\
ペイアウトされるNMRの量はステークした量の±25％に制限されています。\
\
ペイアウトは以下の式で計算されます。\
\
payout = stake\_value \* payout\_factor \* (corr \* corr\_multiplier + mmc \* mmc\_multiplier)\
\
stake\_value:ラウンド開始時点の最初の木曜日にステークしたNMRの量\
payout\_factor:30万NMR以下では1、30万NMR以上では以下の図に示す値をとります。Numeraiはペイアウトの上限を決めることで持続的なTournamentの開催を行うことができます。\
\
![](../.gitbook/assets/factor.png)\
corr:提出した予測ファイルとターゲットの相関\
corr\_multiplier:現在は1のみ\
mmc:提出した予測ファイルとメタモデルの相関\
mmc\_multiplier:0,0.5,1,2の中で一つ選べる。\
\
ペイアウトファクターの関数やマルチプライヤーは、Numeraiによって変更される可能性があります。\
\
ペイアウト計算の例を下図に示します。\
最初の2つの例は、`corr_multiplier`の影響を示しています。\
3番目の例は、負のスコアがペイアウトに影響を与えるかを示しています。\
4番目の例は、ペイアウトがステーク量の±25％に制限されていることを示しています。\
\\

スコアは毎日更新されますが、ペイアウトはTournamentの終了日（日本時間の木曜日）にのみ行われます。参加者の一人が作成したNumeraiPayoutsアプリを使用すると、毎日の変化を追跡できます。\
\
ステークを開始すると、最初の4ラウンドの間ステーク値は一定に保たれます。その後、4週間前のラウンドの支払いに基づいて、ステーク値が毎週更新されます。\\

![](../.gitbook/assets/payout\_week.png)

提出した予測ファイルがプラスのCorr、MMCを持ち続ける限り、得られたNMRの量は増大します。モデルが52週間、毎週同じ正のスコアを取得すると仮定した場合の支払い予測の例を下図に示します。\\

![](../.gitbook/assets/payout\_predict.png)

## 리더보드 / 순위표

NMRのペイアウトはラウンドごとのパフォーマンスに左右されます。リーダーボードに掲載される評価や順位は20ラウンド分のCorr,MMCの加重平均値を用いています。\
詳しくは、 [Reputation](https://jp.docs.numer.ai/numerai-tournament/reputation) のセクションを参照してください。\\

![](../.gitbook/assets/image%20\(5\).png)

## 도움요청

도움이 필요하신가요?

질문과 피드백은 [RocketChat](https://community.numer.ai/home) (영어) 또는 [Discord](https://discord.gg/TxNzq3Nrcc) (한국어)에 올려 주시기 바랍니다!
