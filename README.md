# Dog Image Classification

## Introduction
Purpose: 총 14종의 강아지 품종 이미지를 분류하는 모델 만들기
<br/>
species | label | species | label
---|---|---|---|
코카스파이니엘 | 1 | 삽살개 | 8
푸들 | 2 | 시베리안 허스키 | 9
그레이하운드 | 3 | 말라뮤트 | 10
말티즈 | 4 | 닥스훈트 | 11
퍼그 | 5 | 웰시코기 | 12
비숑 | 6 | 리트리버 | 13
진도개 | 7 | 포메라니안 | 14

</br>

## Methods and Materials
1. Materials
- NAVER, GOOGLE Image
- 총 11,289
2. Methods
- Crawling method: Selenium library
- Preprocessing: Resizing(crawling한 이미지 사이즈가 제각각이라 resizing 작업으로 동일하게 만듬), Zero centering, Gray scale
- Modeling: ResNet50, Transfer learning, Fine-tuning

## Results

## Discussion
