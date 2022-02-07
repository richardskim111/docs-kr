---
description: この記事は、tit_BTCQASHのqiita記事に従います。元記事そのままなので、そっちを読んだ方が良いかもしれません。
---

# Numerai-CLI와 Compute

## 소개

numerai-cli (명령 줄 인터페이스)는 기계학습 모델의 시스템 리소스를 클라우드에서 프로비저닝하여 매주 자동으로 제출할 수 있게 해주는 툴 입니다. 본 툴을 사용하면 예측 파일이 늦게 제출될 염려를 없앨 수 있습니다.

![Prediction Nodes in the Numerai Network](../.gitbook/assets/numerai\_compute.png)

numerai-cli를 사용하여 고유한 클라우드 인프라를 프로비저닝하고 뉴머라이가 트리거할 수 있는 예측 노드로 사전 훈련된 모델을 배포할 수 있습니다. 그 후 새 라운드 데이터를 다운로드를 한 다음 추론을 실행하고 예측 파일을 뉴머라이에 업로드하게 할 수 있습니다.

## 시작 방법

Docker, Python3, Numerai API Key, AWS API Key의 네가지의 요소들를 갖추고 있다면 numerai-cli를 즉시 사용할 수 있습니다.

```
pip3 install numerai-cli

mkdir example-numerai
cd example-numerai

# set up your compute node in AWS
numerai setup

# copy a python example model
numerai docker copy-example

# build the docker container and deploys it to AWS
numerai docker deploy

# trigger your compute node in AWS
numerai compute test-webhook

# watch the logs of the running compute node from AWS
numerai compute logs -f
```

자세한 정보는 [Github Repo](https://github.com/numerai/numerai-cli)의 다큐멘테이션을 참조하기 바랍니다.

## 타이밍

예측 노드에 할당된 웹훅 URL은 자동으로 뉴머라이 모델에 등록됩니다.

뉴머라이는 웹훅을 토요일 19:00 UTC (한국시간 일요일 04:00 KST) - 라운드 시작 1시간 후 트리거가 실행됩니다. 일요일 02:00 UTC (한국시간 일요일 11:00 KST)까지 예측 파일을 제출하지 못한 경우 컴퓨팅 작업이 실패했다는 경고의 메시지를 이메일로 보내집니다.

실패했을 경우 일요일 19:00 UTC (한국시간 월요일 04:00 KST)에 해당 웹훅을 트리거하도록 다시 시도합니다. 또 다시 실패했을 경우 월요일 2:00 UTC (한국시간 월요일 11:00 KST)에 최종 메시지가 이메일로 보내집니다.

## 업그레이드

새 버전(v0.3)으로 업그레이드하는 방법은 간단합니다.

```
pip3 install --upgrade numerai-cli --user
numerai upgrade
```

\*최신 버전(v0.3)은 v0.1 및 v0.2 버전과 호환되지 않습니다.

## **도움요청**

단계별 [튜토리얼](https://docs.numer.ai/help/compute-tutorial)을 읽으시거나 [유튜브 비디오](https://youtu.be/-3y0N7fqfOI)를 시청하기 바랍니다.

더 자세한 도움이 필요하시면 [RocketChat](https://community.numer.ai)에 [#Compute](https://community.numer.ai/channel/compute) 채널 또는 [Slack](https://join.slack.com/t/numerai-kr/shared\_invite/zt-1009d7ws3-hWRKdy8EkbSzwwzxaURlQw) (한국어)에 에 도움을 요청하기 바랍니다.
