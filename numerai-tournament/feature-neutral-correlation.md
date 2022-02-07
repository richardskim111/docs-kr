# 특성중화 상관계수 (FNC)

## **동기**

Feature Neutral Correlation (특성중화 상관계수 - `fnc`)란 모델의 예측치를 뉴머라이 데이터의 모든 특성셋으로 중화한 후의 타겟과의 상관관계를 뜻하고 있습니다.

소수의 특성셋에 의존하는 모델들은 단기적으로는 높은 `corr`을 달성할 수도 있지만 `fnc`가 낮게 측정되게 되어 있습니다. 또한 이러한 모델의 경우 장기적인 퍼포먼스가 낮을 가능성이 있습니다.

다양한 특성들을 사용하면서 타겟과의 상관성이 높은 모델은 `fnc`가 높고 장기적으로도 안정적인 퍼포먼스을  발휘할 가능성이 높습니다.

## **계산방법**

* 라운드에서 사용자의 `fnc`를 계산하기 위해 제출된 예측값을 정규화 합니다.
* 뉴머라이가 가지는 특성셋에 대해서 중화를 합니다.
* 중화된 예측값과 타겟과의 스피어먼 상관계수을 계산합니다.

```python
def calculate_fnc(sub, targets, features):
    """    
    Args:
        sub (pd.Series)
        targets (pd.Series)
        features (pd.DataFrame)
    """
    
    # Normalize submission
    sub = (sub.rank(method="first").values - 0.5) / len(sub)

    # Neutralize submission to features
    f = features.values
    sub -= f.dot(np.linalg.pinv(f).dot(sub))
    sub /= sub.std()
    
    sub = pd.Series(np.squeeze(sub)) # Convert np.ndarray to pd.Series

    # FNC: Spearman rank-order correlation of neutralized submission to target
    fnc = np.corrcoef(sub.rank(pct=True, method="first"), targets)[0, 1]

    return fnc
```

## 논의

보다 자세한 `fnc`의 계산에 대해서는 [이 링크](https://forum.numer.ai/t/model-diagnostics-feature-exposure/899)를 참조해 주세요.
