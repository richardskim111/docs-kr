# 시그널스 소개

## 소개

[뉴머라이 시그널스](https://signals.numer.ai/tournament)는 전 세계 주식시장을 대상으로 한 경진대회입니다.

대회에 참여하신분들은 주식거래의 기반이 되는 signal (시그널)을 작성한뒤 제출하시면 뉴머라이는 모두의 시그널을 크라우드소싱을 이용해 메타모델을 작성해 헤지펀드의 운영에 사용되게 됩니다. 시그널스는 참가자들의 시그널이 얼마나 톡창적이고 우수한 시그널인지 비교할 수 있고 또 제출한 시그널의 성능의 따라 스테이킹 관계량에 비례한 NMR 토큰을 얻을 수 있습니다.

뉴머라이 시그널스 는 뉴머라이 헤지펀드를 구축하기 위해 사용되며 뉴머라이 마스터플랜의 일부입니다. [Medium Post](https://medium.com/numerai/building-the-last-hedge-fund-introducing-numerai-signals-12de26dfa69c)나 [short film](https://www.youtube.com/watch?v=GWeC2PK4yXQ\&feature=youtu.be)에서 상세한 내용이 설명되어 있습니다.

{% embed url="https://youtu.be/GWeC2PK4yXQ" %}

## **개요**

1. 뉴머라이 시그널스에 계정을 가입하거나 기존 뉴머라이 토너먼트 계정으로 가입하셔도 됩니다.
2. 대상이 된 주식시장에 대응한 시그널들을 업로드 하면 과거의 성능, 리스크 등 수익성을 진단할 수 있습니다.
3. 시행중인 라운드에 NMR을 스테이킹 하시면 시그널 제출 치의 성능 (Corr과 MMC)에 근거해 NMR을 얻을 수 있습니다. 단 성능이 낮은 시그널들에 대해서는 NMR을 잃을 수도 있습니다.
4. 뉴머라이의 API에 직접 접속하여 매주 시그널스에 에측파일 제출을 자동화할 수 있습니다.

## **주식시장의 시그널이란?**

주식시장의 시그널이란 뉴머라이와 같은 quant (퀀트) 헤지펀드들이 포트폴리오를 구축하기 위하여 사용하는 데이터입니다.

![](../.gitbook/assets/signals.png)

주식시장 시그널의 예로는 다음과 같은 것이 있습니다.

* [펀더멘털 시그널](https://www.investopedia.com/terms/f/fundamentalanalysis.asp) ([P/E ratio](https://www.investopedia.com/terms/p/price-earningsratio.asp), [dividend yield](https://www.investopedia.com/terms/d/dividendyield.asp), [analyst ratings](https://www.investopedia.com/terms/r/rating.asp#:\~:text=A%20rating%20is%20conducted%20by,this%20action%20for%20the%20stock.))
* [테크니컬 시그널](https://www.investopedia.com/terms/t/technicalindicator.asp) ([MACD](https://www.investopedia.com/terms/m/macd.asp), [RSI](https://www.investopedia.com/terms/r/rsi.asp), [MFI](https://www.investopedia.com/terms/m/mfi.asp))
* [대안 데이터 시그널](https://en.wikipedia.org/wiki/Alternative\_data\_\(finance\)) ([신용카드 거래](https://secondmeasure.com), [위생이미지](https://www.theatlantic.com/magazine/archive/2019/05/stock-value-satellite-images-investing/586009/), [소셜미디어 감정](https://www.swaggystocks.com/dashboard/wallstreetbets/realtime))
* [혼합 시그널](https://www.investopedia.com/terms/m/multifactor-model.asp) ([Barra risk factors](https://www.investopedia.com/terms/b/barra-risk-factor-analysis.asp#:\~:text=The%20Barra%20Risk%20Factor%20Analysis%20is%20a%20multi%2Dfactor%20model,turnover%20and%20senior%20debt%20rating.), [Fama French factors](https://www.investopedia.com/terms/f/famaandfrenchthreefactormodel.asp))

이런 시그널들을 작성하기 위해 사용되는 기초데이터는 여러 성질을 가질 가능성이 높습니다. 예를 들면 주식회사의 연결재무제표와 그회사의 주차장의 이미지는 전혀 다른 데이터입니다만 미래의 주식 값을 예측하는 지표가 포함되어 있을지도 모릅니다. 뉴머라이가 참가자 데이터를 이용하기 위해서는 규격화가 필요합니다. 참가자는 티커와 시그널 데이터가 일대일로 대응할 수 있도록 목록을 작성해야 합니다.

## **시그널 작성법**

### **데이터와 툴**

자체 시그널을 작성하기 위해서는 먼저 여러 주식시장의 데이터를 가져와야 합니다.

{% hint style="info" %}
주식시장의 데이터를 접하기 어려우시다면 [뉴머라이 토너먼트](../numerai-tournament/tournament-overview.md)에 참여해 주세요.
{% endhint %}

아직 주식시장의 데이터에 접하지 못한 경우 [Yahoo Finance](https://finance.yahoo.com), [Quandl](https://www.quandl.com), [Koyfin](https://www.koyfin.com) 등 인터넷상에 무료 또는 저렴한 데이터 공급자가 다수 존재합니다.

또한 [Quantopian](https://www.quantopian.com), [QuantConnect](https://www.quantconnect.com), [Alpaca](https://alpaca.markets)와 같은 시그널 데이터를 쉽게 만들 수 있는 플랫폼도 있습니다. 특히 [Risk Model](https://www.quantopian.com/risk-model)과 [AlphaLens Tearsheets](https://www.quantopian.com/tutorials/alphalens#lesson1)는 시그널의 품질을 분석하는데 가장 적합한 방법입니다. 저희 커뮤니티에서 사용되고 있는 인기 있는 데이터 소스, 플랫폼, 툴 리스트는 [이 게시판 thread](https://forum.numer.ai/t/free-or-cheap-data-for-erasure-numerai-quant/350)를 체크하시기 바랍니다.

{% hint style="success" %}
독특하고 차별화된 데이터셋을 찾아 사용하는 것이 독창적인 시그널을 만들어내는 열쇠입니다.
{% endhint %}

### **유니버스 (대상 주식)**

유니버스는 세계의 상위 5,000개의 대형주를 포함하고 있습니다. 유니버스는 매주 갱신됩니다만 갱신 대상이 되는 것은 거래량이 적은 몇 종목 뿐입니다.

최신 유니버스는 [latest universe file](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/universe/latest.csv)을 다운로드 받아 볼 수 있습니다.

과거의 유니버스 정보는 [historical targets file](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/signals\_train\_val\_bbg.csv) 다운로드 받아 보실 수 있습니다. 이 파일에는 `target_4d`와 `target_20d`의 두 개의 대상 컬럼이 있습니다. `target_20d`가 점수 매기기 및 지불을 위해 시그널이 평가 되는 대상입니다.

`target_4d`와 `target_20d`의 값은 라운드 오픈에서 각각 11일과 33일 후에 표기 됩니다. `target_4d`과는 달리 `target_20d`는 확인 되는 데 더 오래 걸리므로 가장 최근의 날짜의 `target_20d`은 `NaN` 값을 갖습니다.

### **시그널 제출**

작성한 데이터를 뉴머라이 시그널스에 제출할 때는 최소 2개의 컬럼을 포함해야 합니다.

* `cusip`, `sedol` 또는 `bloomberg_ticker`열 - 값은 헤더의 ticker 유형과 관련된 활성 티커여야 합니다.
* `signal` 열-값은 0에서 1 사이여야 합니다. (0,1 제외)

또한, 유효한 제출을 하기 위해서는

* 현재 `live` 기간 예측을 포함하는 행이 최소 10 줄이어야 합니다.
* 현재 `live` 기간에는 티커가 두 번 이상 나타날 수 없습니다.

두 줄만 예측한 결과는 현재 `live` 시간대를 지원한다고 가정합니다.

또한 signal 파일을 제출하면 과거의 퍼포먼스, 리스크, 잠재적인 수익에 대한 진단을 할 수 있습니다. 검증 기간은 20130104 부터 입니다.

검증기간을 포함한 예측결과에는 `friday_date`, `data_type`열을 포함해야 합니다.

* `friday_date` 열 - 뉴머라이 시그널스에서는 라운드의 시작이 금요일이기 때문에 금요일에 해당하는 날짜를 쓰셔야 합니다.
* `data_type` 열 - 값은 `live` 또는 `validation`만을 취할 수 있습니다. `data_type`이 `live`인 행에는 가장 최근 금요일 날짜가 포함되어 있어야 합니다.

![](<../.gitbook/assets/signals (1).png>)

최신의 제출예는 [이 링크](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/example\_signal/latest.csv)를 통해 다운로드 할 수 있습니다.

### **시그 진단**

시그널 데이터를 제출하면 과거의 성능, 리스크, 잠재적인 수익을 진단할 수 있습니다. 이 절차는 보통 제출파일에 포함되어 있는 주 수와 티커 수에 따라 10\~15분 정도 소요됩니다.

![An example diagnostic report](../.gitbook/assets/signal\_diagnostics.png)

이러한 진단을 이용하면 NMR을 스테이킹 할 가치가 있는지를 평가할 수 있습니다. 단 과거의 검증기간 중에 높은 퍼포먼스가 나온 시그널은 현재 또는 미래의 라운드에서 좋은 점수를 얻지 못할 수 있다는 점에 주의해야 합니다.

{% hint style="danger" %}
이 진단 툴을 반복적으로 사용하면 바로 overfitting(과적합)으로 연결됩니다. 진단 툴은 시그널 데이터 작성 과정에 최종 점검으로만 사용하는걸 추천합니다.
{% endhint %}

진단을 계산할 때 사용한 과거의 타겟은 모두 [이 파일](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/signals\_train\_val\_bbg.csv)에서 찾을 수 있습니다.

### **제출 자동화**

{% hint style="info" %}
최신 시그널 데이터를 매주 뉴머라이에 제출해야 합니다.
{% endhint %}

[Numerai-CLI](https://docs.numer.ai/tournament/compute), [GraphQL API](https://api-tournament.numer.ai), 공식 python 클라이언트를 사용하여 제출 절차를 자율화할 수 있습니다.

{% embed url="https://github.com/uuazed/numerapi#usage-example---numerai-signals" %}

## 시그널스 평가방법

### **중화**

뉴머라이는 기존의 다양한 시그널 데이터를 가지고 있습니다. 그 중에는 Barra 팩터 (사이즈, 가치, 모멘텀 등), 국가 및 섹터의 리스크 팩터, 주식별 특징 등이 포함되어 있습니다.

{% hint style="info" %}
“중화”를 정의하자면 제출된 시그널 (타겟)은 Barra 팩터, 국가 및 섹터의 팩터, 기타 주식별 특징 등 뉴머라이의 기존 시그널과의 상관관계가 0이 되도록 변환된것을 뜻합니다.
{% endhint %}

뉴머라이 시그널스에 업로드된 모든 시그널 데이터는 평가가 되기 전에 중화됩니다. 중화의 핵심은 기존의 시그널에 존재하지 않는 새로운 시그널의 자체 성분 혹은 orthogonal (직교) 성분을 분리하는 것입니다.

![A visualization of neutralization against a single known signal](../.gitbook/assets/orthogonal.png)

{% hint style="warning" %}
잘 알려진 몇 가지 시그널의 단순한 선형합된 수치를 제출하면 중화 후에 직교 성분이 거의 남지 않습니다.
{% endhint %}

시그널을 평가하기 위해 사용되는 타겟도 중화됩니다. 타겟은 실질적으로는 뉴머라이 커스텀의 '특정 리턴' 또는 '잔류 리턴'입니다.

중화를 실행하는데 사용되는 데이터는 제공되지 않으므로 이 프로세스는 "블랙박스"로 운영 됩니다. 단, 과거 기간에 강한 스코어를 갖는 시그널은 현재의 라운드든 미래의 라운드에 좋은 평가를 얻지 못할 수 있다는 점에 주의해야 합니다. 시그널의 과거의 진단을 사용하여 중화가 미래 시그널에 미치는 영향을 추정할 수 있습니다.

중화를 시행하기 위해서 사용되고 있는 코드는 오픈 소스입니다. 중화 과정은 이 노트북에서 자세히 볼 수 있습니다.

{% embed url="https://github.com/numerai/example-scripts/blob/master/SignalsScoringExample.ipynb" %}

혹은 특징 변수와 중화 절차의 보다 넓은 의미를 이해하기 위해 이 게시판의 글(영어)을 참조해 보시기 바랍니다.

{% embed url="https://forum.numer.ai/t/model-diagnostics-feature-exposure/899" %}

후속 주식 리턴과의 상관성이 매우 높은 시그널는 뉴머라이 시그널스 안의 점수가 매우 낮고 후속 상관성이 낮은 시그널은 높은 점수를 낼 수도 있습니다.

다시 말하면 강한 예측치를 가진 좋은 시그널을 단독적으로 볼 경우 뉴머라이 시그널스에서는 평가가 낮을 수도 있습니다. 그럼으로 뉴머라이 안에서는 시그널 데이터의 독창적인 특징을 강조합니다. 뉴머라이 시그널스의 대회에서는 주식 리턴을 예측하는 것이 목표가 아니고 뉴머라이에는 없는 독창적인 자체 시그널을 찾는 것을 목표로 삼고 있습니다.

### **20일간의 중화 된 리턴 타겟**

시그널스는 뉴머라이에 의해 작성된 타겟에 대해 평가됩니다.

해당 타겟은 블랙박스화되어 있어 참가자들은 내용을 알 수 없습니다. 이 타겟은 22일간의 중화된 후속 리턴에 근거하고 있습니다. (첫 2일간은 제외)

시그널스가 20일 동안 평가되는 이유는 짧은 시간 축으로밖에 기능하지 않는 시그널은 대규모 헤지펀드가 구현할 수 없기 때문입니다. 예를 들어 시그널이 주식의 1시간 후 리턴을 정확하게 예측할 수 있다 하더라도 헤지펀드가 그 자리를 완전히 거래하는데 24시간이 걸린다면 그다지 유용하지 않습니다.

대규모 헤지펀드에 가장 유용한 시그널은 low-alpha decay (저알파 감쇠)라고도 불리는 긴 시간 축의 예측력을 가지고 있습니다.

정확한 날짜는 [주요 날짜와 마감](signals-overview.md#undefined-7) 섹션을 참조해 주세요.

### **스코어링**

평가되기 전에 시그널은 처음에 \[0, 1] 사이에 등급이 매겨지고 다음으로 중화됩니다. 마지막으로 중화된 시그널과 타겟 사이의 스피어먼 상관계수로 점수가 계산됩니다. 이 점수는 이 문서와 웹사이트에서는 단순히 `Corr`이라고 부르고 있습니다.

제출된 시그널은 스코어링전에 중화됩니다. 그렇게 함으로써 시그널과 타겟의 데이터를 규격화하고 타겟에 대한 퍼포먼스를 향상시킬 수 있습니다.

이 절차에서 타겟도 중화되고 중화에 사용되는 데이터는 뉴머라이가 제공하지 않습니다. 뉴머라이는 참가자로부터 얻은 시그널을 최적화하여 최고의 퍼포먼스의 포트폴리오를 얻을 수 있습니다.

예를 들어 시그널이 국가 리스크에 대해 중화되지 않은 데이터를 제출했다고 합시다. 이 경우 뉴머라이 시그널스는 평가 전에 국가 리스크에 대한 중화를 하기 때문에 국가 리스크의 영향은 없어집니다. 따라서 참가자는 각 팩터의 영향을 신경 쓰지 않고 독자적인 시그널 작성에 집중할 수 있습니다.

유니버스 일부 종목 (예: 미국주식 시그널)에 대해서만 시그널을 제출할 경우에도 뉴머라이 시그널스에 참여할 수 있습니다. 데이터가 없는 종목에 대해서는 등급이 매겨진 후 뉴머라이가 자동으로 중앙값으로 채워줍니다.

### **메타 모델에의 공헌**

`Corr`은 제출한 시그널과 뉴머라이가 보유한 시그널 (타겟은 중화제)가 어느 정도 상관관계가 있는지를 나타내는 지표입니다. 한편 Meta Model Contribution (MMC)는 제출한 시그널가 뉴머라이가 보유한 Signals (타겟은 중화제)와의 상관관계를 가질 뿐만 아니라 다른 사람이 NMR을 이해관계한 시그널과도 상관관계를 갖고 계산한 지표입니다. 이 문서 및 웹사이트에서는 단순히 `mmc`라고 부르고 있습니다.

시그널의 `mmc`는 첫 번째 Signals' Meta Model이라고 불리는 특별한 Signals를 구축함으로써 계산됩니다.여기서 시그널스 메타 모델이란 주어진 라운드에 대해서 뉴머라이 시그널스 상의 모든(랭크 매겨지고 중화 된) 데이터의 스테이크 가중평균으로 정의된 것입니다. 시그널스의 `mmc`는 메타 모델에 중화된 이후 타겟에 대한 시그널의 상관관계를 나타내는 지표입니다.

{% hint style="success" %}
참가자가 제출한 시그널이 높은 `mmc`를 나타낼 경우 다른 사람이 제출한 시그널보다 우위를 나타냅니다.
{% endhint %}

`mmc`는 뉴머라이 토너먼트에서 따온 개념으로 스코어링 시스템은 매우 유사합니다. 뉴머라이에서의 `mmc` 계산방법에 대한 자세한 내용은 뉴머라이 토너먼트 문서의 [메타모델 공헌도 (MMC)](../numerai-tournament/meta-model-contribution-mmc.md) 섹션을 참조해 주세요.

뉴머라이 시그널스의 `mmc` 계산은 뉴머라이 토너먼트와 완전히 분리되어 있음에 유의하시기 바랍니다. 구체적으로는 뉴머라이 시그널스 에 제출하는 것만이 시그널스의 메타모델을 구축하는데 사용됩니다.

## **스테이킹**

提出したSignalsに自信がある場合、`corr` または `corr_plus_mmc` にNMRをステークすることができます。\
ステーキングとは、NMRをイーサリアムブロックチェーンのスマートコントラクトに固定することを意味します。NumeraiはロックアップされたNMRに報酬を追加したり、NMRを没収することができます。\\

{% hint style="info" %}
あなたがNMRをSignalsにステークする行為は、以下の行為に参加する機会をオファーするもの**ではない**ことに注意してください。\
\*投資契約、証券、金融資産のリターンに基づくスワップ、Numeraiヘッジファンドへの参加、Numeraiのヘッジファンドの利息、Numerai自体が得た手数料の提供\\

Numerai Signalsは、ユーザーが自分のSignalsの価値を評価できるサービスです。\
基本的に、Numerai Signalsは、提出されたSignalsが「本物」であるかを検証する方法としてNMRステーキングを使用します。\
また、ペイアウトは、ユーザーに開示されないブラックボックスターゲットに基づいて、Numeraiの裁量で行われます。\
ペイアウトを行う見返りとして、NumeraiはステークされたSignalsと関連データをNumeraiヘッジファンドで使用します。\
これらに異なる期待を持つユーザーは、SignalsにNMRをステークすべきではありません。\
詳細については、[利用規約](https://numer.ai/terms)をお読みください。\\
{% endhint %}

あなたはウェブサイトであなたのステーク量を管理できます。ステークを増やすと、NMRはウォレットからステーキングコントラクト（Numeraiの保有しているETHアカウント）に転送されます。ステークを減らすと、NMRは約4週間の遅延後にウォレットに戻されます。また、ステークの種類を変更することもできます。これにより、ステークしたいスコア（Corr,MMC）を決められます。

ステークを作成するには、ウェブサイトの"manage stake"ボタンをクリックし、ステークを増加させるためのリクエストを作成します。ここでは、`corr`と`corr_plus_mmc`のどちらにステークするかを選択することができます。ステークを減らしたい場合は、"change request"を作成し、ステークを減少させることもできます。

![](../.gitbook/assets/stake.png)

change requestsはすぐに反映されません。変更を適用する前に、必ずウェブサイトに表示されている"effective date"を再確認してください。

## **페이아웃**

どれだけのNMRを得られるかはNMRのステーク量と、Corr,MMCの値に依存します。\
スコアが高いほど、より多くのNMRを得ることができます。もし負のCorr,MMCとなった場合、ステークしたNMRの一部が没収され、バーンされます。\
バーンとはERC-20トークンの持つ機能の一つであり、トークンを永遠に使用できなくする操作のことです。\
ペイアウトされるNMRの量はステークした量の±25％に制限されています。\
ペイアウトは以下の式で計算されます。\
payout = stake\_value \* payout\_factor \* (corr \* corr\_multiplier + mmc \* mmc\_multiplier)\
stake\_value:ラウンド開始時点の最初の金曜日にステークしたNMRの量\
payout\_factor:10万NMR以下では1になります。10万NMR以上では以下の図に示す値をとります。Numeraiはペイアウトの上限を決めることで持続的なTournamentの開催を行うことができます。\
![](../.gitbook/assets/factor2.png)\
corr:提出した予測ファイルとターゲットの相関\
corr\_multiplier:現在は2のみ\
mmc:提出した予測ファイルとメタモデルの相関\
mmc\_multiplier:0,0.5,1,2の中で一つ選べる。\
![](../.gitbook/assets/factor3.JPG)\\

{% hint style="info" %}
ペイアウトファクターの関数やマルチプライヤーは、Numeraiによって変更される可能性があります。\\
{% endhint %}

ペイアウト計算の例を次に示します。 最初の2つの例は、`corr_multiplier`の影響を示しています。\
3番目の例は、負のスコアがペイアウトに影響を与えるかを示しています。\
4番目の例は、ペイアウトがステーク量の±25％に制限されていることを示しています。\\

![](../.gitbook/assets/Payout2.JPG)\\

### ステーク量の成長

スコアは毎日更新されますが、ペイアウトはTournamentの終了日（日本時間の木曜日）にのみ行われます。 提出した予測ファイルがプラスのCorr、MMCを持ち続ける限り、得られるNMRの量は増大します。モデルが52週間、毎週同じ正のスコアを取得すると仮定した場合の支払い予測の例を下図に示します。\
![](../.gitbook/assets/payout\_predict2.png)

## **주요 날짜와 마감**

### 데이터 날짜 vs 유효한 날짜

Numerai signalsには2種類の日付があります。

* `data_date` - 基礎となる株式市場データに対応する日付です。すべての`data_date`は、その日の市場の終値を参照しており、時刻は含まれていません。例えば、submissionsの`friday_date`列の値は`data_date`型です。
* `effective_date`- Numerai Signals で行われるアクションやイベントに対応する日付で、常にUTCで指定された時間を含む場合があります。時間帯や株式市場データの処理に時間がかかるため、`data_date`と`effective_date`の間には通常遅延が発生します。特に指定がない限り、本ウェブサイトおよび本文書に記載されている日付はすべて effective\_date 型です。

### 라운드

提出、ステーク、スコア、ペイアウトは、見やすいようにグループ化されています。このグループのことを「ラウンド」とよびます。

新しいラウンドは毎週`土曜日の18:00 UTC`に開始します。データの提出とステークの締め切りは`月曜日の14:30 UTC`です。遅刻した場合は評価されず、ペイアウトにもカウントされません。締め切り後に行われたステーク量の変更は次のラウンドに適用されます。

提出期限に間に合ったSignalsは評価され、保留中のペイアウト量は金曜日、土曜日、火曜日、水曜日に計算されます。 また、ステークしたNMRは金曜日までロックされます。これは、前のラウンドからのペイアウトと次のラウンドのペイアウトを統合することを意味します。水曜日のスコアとペイアウトは、そのラウンドの最終スコアとペイアウトとなります。

![](../.gitbook/assets/image%20\(14\).png)

ラウンドのユニバースは、前の金曜日の`data_date`で定義されています。4 日間のスコアリングとペイアウトは、`3 日目-2 日目`、`4 日目-2 日目`、`5 日目-2 日目`、`6 日目-2 日目`の中和リターンに基づいています。ある日のマーケットクローズから、スコアリングのためにデータが利用可能になるまでには2日のラグがあります。例えば、`6日目-2日目`の中和リターンは月曜日のマーケットクローズまでですが、このデータが利用可能になるのは水曜日です。

![](../.gitbook/assets/image%20\(15\).png)

## **리더보드**

NMRのペイアウトはラウンドごとのパフォーマンスに左右されます。リーダーボードに掲載される評価や順位は20ラウンド分のCorr,MMCの加重平均値を用いています。

![](../.gitbook/assets/leader.png)

## **도움요청**

도움이 필요하신가요?&#x20;

질문과 피드백은 [RocketChat](https://community.numer.ai/home) (영어) 또는 [Discord](https://discord.gg/TxNzq3Nrcc) (한국어)에 올려 주시기 바랍니다!
