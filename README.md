# Motion Planning Connectivity and Robustness Analysis

원형 로봇과 원형 장애물로 구성된 2차원 정적 환경에서
형상 공간의 연결성, 격자 기반 A*의 이산화 오차,
장애물 위치 섭동에 대한 통과 가능성의 견고성을 분석한 프로젝트입니다.

## 프로젝트 개요

이 프로젝트는 로봇 반지름과 장애물 배치가 좌우 통과 가능성에 미치는 영향을
다음 두 단계로 분석합니다.

1. 연속 공간의 이론적 임계반지름과 격자 A*의 관측 임계값 비교
2. 장애물 위치 오차가 연속 공간 임계반지름과 병목 구조에 미치는 영향 분석

접촉은 충돌로 처리하며, A*와 최소 최대 장벽 알고리즘은 직접 구현했습니다.

## 노트북

### 1. Connectivity threshold and grid A*

`notebooks/01_connectivity_threshold_and_grid_astar.ipynb`

- 장애물 접촉 임계값 계산
- 전체 접촉 그래프 구성
- 최소 최대 장벽을 이용한 이론적 임계반지름 계산
- 격자 기반 8방향 A* 구현
- 연속 공간 임계값과 격자 관측값 비교
- 좁은 통로와 격자점 정렬에 따른 이산화 오차 분석

### 2. Geometry perturbation robustness

`notebooks/02_geometry_perturbation_robustness.ipynb`

- 장애물 위치에 균등분포 또는 정규분포 섭동 적용
- 각 표본에서 전체 접촉 그래프 재구성
- 임계반지름과 통과 가능성 판정 변화 측정
- 전역 장벽과 병목 간선의 전환 분석
- 명목 여유와 판정 전환율의 관계 분석

## 핵심 결과

- 접촉 그래프의 최소 최대 경로를 이용해 연속 공간의 임계반지름을 계산했습니다.
- 전체 그래프 계산과 구간별 이론식이 181개 장애물 배치에서 일치했습니다.
- 격자 간격을 줄이면 전반적으로 이론값에 가까워졌지만, 오차는 격자 간격뿐 아니라 좁은 통로와 격자점의 상대적 정렬에도 영향을 받았습니다.
- 위치 섭동 실험에서 안정적인 평탄 구간은 임계반지름과 판정이 변하지 않았습니다.
- 선형 구간의 명목 여유가 0.005인 조건에서는 200개 표본 중 22%에서 판정 전환이 관측되었습니다.
- V자 꼭짓점에서는 섭동 방향에 따라 병목 간선이 전환되는 현상을 확인했습니다.

22%는 고정 난수 시드로 생성한 200개 표본에서 관측된 값이며,
분포 전체에 대한 정확한 이론 확률을 의미하지 않습니다.

## 저장소 구조

```text
motion-planning-connectivity/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── 01_connectivity_threshold_and_grid_astar.ipynb
│   └── 02_geometry_perturbation_robustness.ipynb
└── results/
    ├── 01_connecticity/
    └── 02_perturbation/
