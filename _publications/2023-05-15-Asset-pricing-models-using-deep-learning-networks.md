---
title: "딥러닝 네트워크를 활용한 주식 가격 결정 모델"
collection: publications
category: manuscripts
permalink: /publication/2023-05-15-Asset-pricing-models-using-deep-learning-networks
excerpt: '딥러닝 네트워크를 활용하여 한국 주식 시장의 자산 가격 결정 모델을 구현한 연구입니다.'
date: 2023-05-15
paperurl: 'https://www.riss.kr/search/detail/DetailView.do?p_mat_type=1a0202e37d52c72d&control_no=df3837feed728c3bd18150b21a227875&keyword=%EC%B5%9C%EC%9D%B8%EC%97%B4'
citation: 'Choi, I. Y. (2024). &quot;딥러닝 네트워크를 활용한 주식 가격 결정 모델.&quot;'
---

## 연구 개요

본 연구는 딥러닝 네트워크를 활용하여 한국 주식 시장의 자산 가격 결정 모델을 구현하였습니다. Gu, Kelly, and Xiu(2021)의 연구를 바탕으로, 한국 시장의 특성을 반영한 자산 가격 결정 모델을 개발하고 그 성능을 검증하였습니다.



## 연구 배경

금융 시장에서 자산의 가격을 결정하는 요인들을 이해하는 것은 매우 중요합니다. 특히 잠재 팩터를 발견할 수 있다면, 비정상 초과 수익률을 해석할 수 있게 됩니다. 본 연구는 한국 시장의 요인과 외부 요인을 딥러닝 네트워크에 입력으로 제공하여 팩터의 비선형적 관계를 분석하고자 하였습니다.

## 데이터 및 방법론

### 데이터 수집
- KOSPI 상장 기업 858개 대상
- 기간: 2000-01-04 ~ 2023-05-08
- 일별 OHLCV 데이터 및 주간 수익률 계산

### 기업 특성 변수
총 16개의 특성 변수를 사용하여 분석:
1. 가격 트렌드 지표 (6개)
   - 단기 반전, 주식 모멘텀, 모멘텀 변화 등
2. 유동성 지표 (5개)
   - 거래회전율, 시가총액, 거래량 등
3. 위험 측정 지표 (4개)
   - 수익률 변동성, 시장 베타 등
4. 메타 데이터
   - 주간 수익률

## 모델 구조

### 입력 베타 처리
- 15개의 베타 값 사용
- 히든 레이어 구성: [8, 16, 32] 유닛
- ReLU 활성화 함수와 배치 정규화 적용
- K개 팩터로 가중치 전달 (K = [2,3,4,5,6])

### 데이터 처리
- 제너레이터 방식 활용으로 메모리 효율성 확보
- Lazy evaluation 통한 연산 최적화
- Out-Of-Memory 방지를 위한 코드 최적화

## 실증 분석 결과

### 수익률 분석
- Period Wise Return 분석 (5, 10, 21일 단위)
- Factor 분위별 수익률 변동폭 분석
- Top minus Bottom Quantile 평균 수익률 분석

<img src='/images/DeepAsset_250317/figure1.png'>

### 정보 계수(IC) 분석
- 2019-2023년 테스트 기간 동안 양의 IC 값 유지
- 정규분포 형태의 IC 분포 확인
- 월별 IC 평균의 안정성 검증

<img src='/images/DeepAsset_250317/figure2.png'>

## 결론 및 시사점

1. 한국 시장 특성 반영
   - KOSPI 시장 데이터로 검증된 Factor 도출
   - IC 값의 통계적 유의성 확인

2. 연구의 한계
   - 미국 시장 대비 제한된 데이터
   - 약 800개의 종목으로 제한된 표본

3. 향후 연구 방향
   - 백테스트 및 통계적 검정 강화
   - BatchNorm, Ensemble 등 최적화 기법 적용
   - IC 개선을 위한 모델 고도화

## 참고 문헌

1. Gu, S., Kelly, B., & Xiu, D. (2021). Autoencoder asset pricing models. Journal of Econometrics, 222(1), 429-450.
2. Kelly, B. T., Pruitt, S., & Su, Y. (2019). Characteristics are covariances: A unified model of risk and return. Journal of Financial Economics, 134(3), 501-524.

## 코드

전체 코드는 [GitHub 저장소](https://github.com/ChoiInYeol/Asset-pricing-models-using-deep-learning-networks)에서 확인하실 수 있습니다.