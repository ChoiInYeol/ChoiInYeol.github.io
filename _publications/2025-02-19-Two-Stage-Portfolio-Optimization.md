---
title: "Two-Stage Portfolio Optimization Framework Using CNN-Based Stock Chart Analysis"
collection: publications
category: thesis
permalink: /publication/2025-02-19-Two-Stage-Portfolio-Optimization
excerpt: 'CNN 기반의 주식 차트 분석을 활용한 2단계 포트폴리오 최적화 프레임워크'
date: 2025-02-19
venue: '경희대학교 대학원'
paperurl: 'https://www.riss.kr/search/detail/DetailView.do?p_mat_type=be54d9b8bc7cdb09&control_no=904a75c30317a6b5ffe0bdc3ef48d419&keyword=%EC%B5%9C%EC%9D%B8%EC%97%B4'
citation: '최인열. (2025). &quot;Two-Stage Portfolio Optimization Framework Using CNN-Based Stock Chart Analysis.&quot; <i>국내석사학위논문 경희대학교 대학원</i>.'
---

## 연구 개요

본 연구는 주식 시장에서의 포트폴리오 최적화를 위해 딥러닝 기술을 활용한 새로운 접근 방식을 제안합니다. 특히, 주식 차트 이미지 분석과 포트폴리오 최적화를 통합한 2단계 프레임워크를 개발하여 투자 전략의 효율성을 높이고자 하였습니다.



## 연구 배경

최근 딥러닝 기술의 발전으로 주식 차트의 시각적 패턴 분석과 시계열 데이터 기반의 예측이 가능해졌습니다. 그러나 기존 연구들은 주로 종목 선정을 위한 신호의 예측력에만 중점을 두어, 포트폴리오 최적화와의 통합적 접근이 부족했습니다. 본 연구는 이러한 한계를 극복하고자 차트 이미지 기반의 신호를 포트폴리오 최적화와 통합하는 새로운 모델을 제시합니다.

## 연구 방법

### 1단계: CNN 기반 차트 이미지 분석
- 합성곱 신경망(CNN)을 활용한 차트 이미지 패턴 학습
- 주가 상승 확률 예측을 통한 유망 종목 식별
- 시각적 패턴의 특징 추출 및 분석

### 2단계: 포트폴리오 최적화
- 선별된 자산에 대한 포트폴리오 최적화 적용
- 투자 전략의 성과 평가
- 최적화 전략의 개선 및 조정

## 실험 및 결과

### CNN 모델 성능
- 차트 이미지 기반 예측 정확도 분석
- 패턴 인식 능력 검증
- 모델 강건성 테스트

### 백테스트 결과
- 포트폴리오 수익률 분석
- 위험 조정 수익률 평가
- 벤치마크 대비 초과 성과 검증

## 결론 및 시사점

본 연구는 차트 이미지 신호와 포트폴리오 최적화를 통합하는 접근 방식의 효과성을 입증하였습니다. 특히:
1. 자산 선정의 정확도 향상
2. 투자 전략의 수익성 개선
3. 시각적 패턴과 포트폴리오 최적화의 시너지 효과 확인

## 목차

1. Introduction
   - 1.1 Contributions
   - 1.2 Organization

2. Literature Review
   - 2.1 Classical Portfolio Optimization
   - 2.2 Momentum and Technical Analysis
   - 2.3 Artificial Intelligence in Finance
   - 2.4 Deep Learning for Portfolio Optimization

3. Method
   - 3.1 Data Collection and Preprocessing
   - 3.2 Generating Chart Data
   - 3.3 Configuring a Data Universe
   - 3.4 CNN-based Chart Image Model
   - 3.5 Time-Series Neural Network Model
      - 3.5.1 Score Block
      - 3.5.2 Portfolio Block
      - 3.5.3 Constraints
      - 3.5.4 Model and Training Hyperparameters

4. Experiment
   - 4.1 Experimental Settings
   - 4.2 CNN Model Result
   - 4.3 Backtest
   - 4.4 Discussion

5. Conclusion

References
