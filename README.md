# KGM_UPGRADE


1. 모델 구조 고도화 (Deep & Light Architecture)

Conv 층 깊이 2배 확장: 기존 블록당 1개였던 합성곱(Conv2d) 층을 2개씩 연달아 배치하여(총 6개 층), 이미지의 복잡한 특징을 더 깊고 정교하게 추출하도록 개선했습니다.

GAP(Global Average Pooling) 도입: 모델의 마지막 분류기 층에 무거운 nn.Linear 대신 AdaptiveAvgPool2d((1, 1))를 도입했습니다. 이를 통해 파라미터(가중치) 수를 획기적으로 줄여 연산 효율을 높이고 과적합(Overfitting)을 방지했습니다.

2. 학습 방식 및 하이퍼파라미터 최적화 (Training Strategy)

에폭(Epoch) 대폭 증가: 문제가 어려워진 만큼 충분한 학습을 위해 에폭을 기존 5회에서 100회로 늘렸습니다.

학습률 스케줄러(CosineAnnealingLR) 적용: 학습 초반에는 넓은 보폭으로, 후반에는 좁은 보폭으로 미세 조정하며 정답에 수렴할 수 있도록 스케줄러를 추가했습니다. (성능 향상의 핵심)

가중치 감소(Weight Decay): Adam 옵티마이저에 L2 정규화(weight_decay=1e-5)를 추가하여, 모델이 학습 데이터를 외워버리는 과적합 현상을 억제했습니다.
